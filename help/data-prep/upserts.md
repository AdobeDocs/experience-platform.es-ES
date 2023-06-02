---
keywords: Experience Platform;inicio;temas populares;preparación de datos;preparación de datos;streaming;upsert;streaming upsert
title: Envío De Actualizaciones Parciales De Filas Al Servicio De Perfiles Mediante La Preparación De Datos
description: Este documento proporciona información sobre cómo enviar actualizaciones de filas parciales al servicio de perfil mediante la preparación de datos.
exl-id: f9f9e855-0f72-4555-a4c5-598818fc01c2
source-git-commit: d167975c9c7a267f2888153a05c5857748367822
workflow-type: tm+mt
source-wordcount: '1177'
ht-degree: 1%

---

# Enviar actualizaciones parciales de fila a [!DNL Profile Service] usando [!DNL Data Prep]

Actualizaciones de streaming en [!DNL Data Prep] le permite enviar actualizaciones parciales de fila a [!DNL Profile Service] datos, al tiempo que se crean y establecen nuevos vínculos de identidad con una única solicitud de API.

Al transmitir las actualizaciones, puede conservar el formato de los datos mientras los traduce a [!DNL Profile Service] solicitudes del PATCH durante la ingesta. En función de las entradas que proporcione, [!DNL Data Prep] le permite enviar una sola carga útil de API y traducir los datos a ambos [!DNL Profile Service] PATCH y [!DNL Identity Service] CREAR solicitudes.

Este documento proporciona información sobre cómo transmitir actualizaciones en [!DNL Data Prep].

## Primeros pasos

Esta descripción general requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Data Prep]](./home.md): [!DNL Data Prep] permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el modelo de datos de Experience (XDM).
* [[!DNL Identity Service]](../identity-service/home.md): obtenga una mejor vista de los clientes individuales y su comportamiento uniendo identidades entre dispositivos y sistemas.
* [Perfil del cliente en tiempo real](../profile/home.md): Proporciona un perfil de cliente unificado en tiempo real en función de los datos agregados de varias fuentes.
* [Fuentes](../sources/home.md): Experience Platform permite la ingesta de datos desde varias fuentes y, al mismo tiempo, le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.

## Uso de actualizaciones de flujo continuo en [!DNL Data Prep] {#streaming-upserts-in-data-prep}

>[!NOTE]
>
>Las siguientes fuentes admiten el uso de actualizaciones de flujo continuo:<ul><li>[[!DNL Amazon Kinesis]](../sources/connectors/cloud-storage/kinesis.md)</li><li>[[!DNL Azure Event Hubs]](../sources/connectors/cloud-storage/eventhub.md)</li><li>[[!DNL HTTP API]](../sources/connectors/streaming/http.md)</li></ul>

### Flujo de trabajo de alto nivel de actualizaciones de streaming

Actualizaciones de streaming en [!DNL Data Prep] funciona de la siguiente manera:

* Primero debe crear y habilitar un conjunto de datos para [!DNL Profile] consumo. Consulte la guía de [habilitar un conjunto de datos para [!DNL Profile]](../catalog/datasets/enable-for-profile.md) para obtener más información.
* Si se deben vincular nuevas identidades, también se debe crear un conjunto de datos adicional **con el mismo esquema** como su [!DNL Profile] conjunto de datos.
* Una vez preparados los conjuntos de datos, debe crear un flujo de datos para asignar la solicitud entrante a [!DNL Profile] conjunto de datos;
* A continuación, debe actualizar la solicitud entrante para incluir los encabezados necesarios. Estos encabezados definen:
   * La operación de datos que se debe realizar con [!DNL Profile]: `create`, `merge`, y `delete`.
   * La operación de identidad opcional que se va a realizar con [!DNL Identity Service]: `create`.

### Configuración del conjunto de datos de identidad

Si se deben vincular nuevas identidades, debe crear y pasar un conjunto de datos adicional en la carga útil entrante. Al crear un conjunto de datos de identidad, debe asegurarse de que se cumplan los siguientes requisitos:

* El conjunto de datos de identidad debe tener su esquema asociado como [!DNL Profile] conjunto de datos. Una discrepancia en los esquemas puede provocar un comportamiento incoherente del sistema.
* Sin embargo, debe asegurarse de que el conjunto de datos de identidad sea diferente al de [!DNL Profile] conjunto de datos. Si los conjuntos de datos son los mismos, los datos se sobrescribirán en lugar de actualizarse.
* Mientras que el conjunto de datos inicial debe estar habilitado para [!DNL Profile], el conjunto de datos de identidad **no debe estar habilitado** para [!DNL Profile]. De lo contrario, los datos también se sobrescribirán en lugar de actualizarse. Sin embargo, el conjunto de datos de identidad **debe estar habilitado** para [!DNL Identity Service].

#### Campos obligatorios en los esquemas asociados al conjunto de datos de identidad {#identity-dataset-required-fileds}

Si el esquema contiene campos obligatorios, la validación del conjunto de datos debe suprimirse para habilitar [!DNL Identity Service] para recibir solo las identidades. Puede suprimir la validación aplicando la variable `disabled` valor para `acp_validationContext` parámetro. Consulte el ejemplo siguiente:

```shell
curl -X POST 'https://platform.adobe.io/data/foundation/catalog/dataSets/62257bef7a75461948ebcaaa' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "tags": {
        "acp_validationContext": [
            "disabled"
        ],
        "unifiedProfile": [
            "enabled:false"
        ],
        "unifiedIdentity": [
            "enabled:true"
        ]
    }
}'
```

>[!TIP]
>
>No es necesario realizar ninguna configuración adicional si el esquema asociado con el conjunto de datos de identidad no tiene campos obligatorios.

## Estructura de carga útil entrante

A continuación se muestra un ejemplo de una estructura de carga útil entrante que establece nuevos vínculos de identidad.

### Carga útil con configuración de identidad

```shell
{
  "header": {
    "flowId": "923e2ac3-3869-46ec-9e6f-7012c4e23f69",
    "imsOrgId": "{ORG_ID}",
    "datasetId": "621fc19ab33d941949af16c8",
    "operations": {
        "data": "create" (default)/"merge"/"delete",
        "identity": "create",
        "identityDatasetId": "621fc19ab33d941949af16d9"
    }
  }
... //The raw data attributes are included here as the key/value pairs of the "body" property.
}
```

| Parámetro | Descripción |
| --- | --- |
| `flowId` | ID único para identificar un flujo de datos. Este ID de flujo de datos debe corresponder a la conexión de origen creada con [!DNL Amazon Kinesis], [!DNL Azure Event Hubs], o [!DNL HTTP API]. Este flujo de datos también debe tener un [!DNL Profile]Conjunto de datos habilitado para como conjunto de datos de destino. **Nota**: el ID del [!DNL Profile]El conjunto de datos de Target habilitado para también se usa como `datasetId` parámetro. |
| `imsOrgId` | El ID que corresponde a su organización. |
| `datasetId` | El ID del [!DNL Profile]Conjunto de datos de destino habilitado para el flujo de datos. **Nota**: Es el mismo ID que el [!DNL Profile]Se ha encontrado un ID de conjunto de datos de destino habilitado en el flujo de datos. |
| `operations` | Este parámetro describe las acciones que [!DNL Data Prep] tomará en función de la solicitud entrante. |
| `operations.data` | Define las acciones que se deben realizar en [!DNL Profile Service]. |
| `operations.identity` | Define las operaciones permitidas en los datos por [!DNL Identity Service]. |
| `operations.identityDatasetId` | (Opcional) ID del conjunto de datos de identidad que solo es necesario si se deben vincular nuevas identidades. |

#### Operaciones compatibles

Las siguientes operaciones son compatibles con [!DNL Profile Service]:

| Operaciones | Descripción |
| --- | --- | 
| `create` | La operación predeterminada. Esto genera un método de creación de entidad XDM para [!DNL Profile Service]. |
| `merge` | Esto genera un método de actualización de entidad XDM para [!DNL Profile Service]. |
| `delete` | Esto genera un método de eliminación de entidad XDM para [!DNL Profile Service] y elimina permanentemente los datos del [!DNL Profile Store]. |

Las siguientes operaciones son compatibles con [!DNL Identity Service]:

| Operaciones | Descripciones |
| --- | --- |
| `create` | La única operación permitida para este parámetro. If `create` se pasa como valor para `operations.identity`, entonces [!DNL Data Prep] genera una solicitud de creación de entidad XDM para [!DNL Identity Service]. Si la identidad ya existe, se ignora la identidad. **Nota:** If `operations.identity` se establece en `create`y, a continuación, el `identityDatasetId` también se debe especificar. El mensaje de creación de entidad XDM generado internamente por [!DNL Data Prep] se generará el componente para este id del conjunto de datos. |

### Carga útil sin configuración de identidad

Si no es necesario vincular nuevas identidades, puede omitir la variable `identity` y `identityDatasetId` parámetros en las operaciones. Al hacerlo, los datos solo se envían a [!DNL Profile Service] y omite el [!DNL Identity Service]. Consulte la carga útil siguiente para ver un ejemplo:

```shell
{
  "header": {
    "flowId": "923e2ac3-3869-46ec-9e6f-7012c4e23f69",
    "imsOrgId": "{ORG_ID}",
    "datasetId": "621fc19ab33d941949af16c8",
    "operations": {
        "data": "create"/"merge"/"delete",
    }
  }
... //The raw data attributes are included here as the key/value pairs of the "body" property.
}
```

## Transferir identidades principales de forma dinámica

Para las actualizaciones de XDM, el esquema debe estar habilitado para [!DNL Profile] y contienen una identidad principal. Puede especificar la identidad principal de un esquema XDM de dos formas:

* Designar un campo estático como identidad principal en el esquema XDM;
* Designe uno de los campos de identidad como identidad principal a través del grupo de campos mapa de identidad en el esquema XDM.

### Designar un campo estático como campo de identidad principal en el esquema XDM

En el ejemplo siguiente, `state`, `homePhone.number` y otros atributos se actualizan con sus respectivos valores dados en la variable [!DNL Profile] con la identidad principal de `sampleEmail@gmail.com`. A continuación, la transmisión genera un mensaje de actualización de entidad XDM [!DNL Data Prep] componente. [!DNL Profile Service] a continuación, confirma ese mensaje de actualización de XDM para actualizar el registro de perfil.

>[!NOTE]
>
>En este ejemplo, las identidades no se vincularán porque no hay operaciones definidas para la identidad.

```shell
curl -X POST 'https://dcs.adobedc.net/collection/9aba816d350a69c4abbd283eb5818ec3583275ffce4880ffc482be5a9d810c4b' \
  -H 'Content-Type: application/json' \
  -H 'x-adobe-flow-id: d5262d48-0f47-4949-be6d-795f06933527' \
  -d '{
    "header": {
        "flowId" : "d5262d48-0f47-4949-be6d-795f06933527",
        "imsOrgId": "{ORG_ID}",
        "datasetId": "62259f817f62d71947929a7b",
        "operations": {
         "data": "create"
     }
    },
    {
        "body": {
        "homeAddress": {
            "country": "US",
            "state": "GA",
            "region": "va7"
        },
        "homePhone": {
            "number": "123.456.799"
        },
        "identityMap": {
            "Email": [{
                "id": "sampleEmail@gmail.com",
                "primary": true
            }]
        },
      "personalEmail": {
            "address": "sampleEmail@gmail.com",
            "primary": true
       },
      "personID": "346576345",
      "_id": "346576345",
      "timestamp": "2021-05-05T17:51:45.1880+02",
      "workEmail": "sampleWorkEmail@gmail.com"
  }
}'
```

### Designe uno de los campos de identidad como identidad principal a través del grupo de campos de mapa de identidad en el esquema XDM

En este ejemplo, el encabezado contiene `operations` con el atributo `identity` y `identityDatasetId` propiedades. Esto permite combinar los datos con [!DNL Profile Service] y también para que las identidades se pasen a [!DNL Identity Service].

```shell
curl -X POST 'https://dcs.adobedc.net/collection/9aba816d350a69c4abbd283eb5818ec3583275ffce4880ffc482be5a9d810c4b' \
  -H 'Content-Type: application/json' \
  -H 'x-adobe-flow-id: d5262d48-0f47-4949-be6d-795f06933527' \
  -d '{
    "header": {
        "flowId" : "d5262d48-0f47-4949-be6d-795f06933527",
        "imsOrgId": "{ORG_ID}",
        "datasetId": "62259f817f62d71947929a7b",
        "operations": {          
            "data": "merge",
            "identity": "create",
            "identityDatasetId": "6254a93b851ecd194b64af9e"
      }
    },
    {        
       "body": {
        "homeAddress": {
            "country": "US",
            "state": "GA",
            "region": "va7"
        },
        "homePhone": {
            "number": "123.456.799"
        },
        "identityMap": {
            "Email": [{
                "id": "sampleEmail@gmail.com",
                "primary": true
            }]
        },
      "personalEmail": {
            "address": "sampleEmail@gmail.com",
            "primary": true
       },
      "personID": "346576345",
      "_id": "346576345",
      "timestamp": "2021-05-05T17:51:45.1880+02",
      "workEmail": "sampleWorkEmail@gmail.com"
  }
 }'
```

## Limitaciones conocidas y consideraciones clave

A continuación se describe una lista de limitaciones conocidas a tener en cuenta al transmitir actualizaciones con [!DNL Data Prep]:

* El método de actualizaciones de flujo continuo solo debe usarse al enviar actualizaciones de fila parciales a [!DNL Profile Service]. Las actualizaciones parciales de filas son **no** consumido por el lago de datos.
* El método de actualizaciones de streaming no admite la actualización, el reemplazo y la eliminación de identidades. Si no existen, se crean nuevas identidades. Por lo tanto, `identity` La operación siempre debe configurarse para crear. Si ya existe una identidad, la operación no es operativa.
* Actualmente, el método de actualizaciones de streaming no es compatible [SDK web de Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=es) y [SDK de Adobe Experience Platform Mobile](https://aep-sdks.gitbook.io/docs/).

## Pasos siguientes

Al leer este documento, ahora debería comprender cómo transmitir las actualizaciones en [!DNL Data Prep] para enviar actualizaciones parciales de fila a [!DNL Profile Service] datos, al tiempo que se crean y vinculan identidades con una sola solicitud de API. Para obtener más información sobre otros [!DNL Data Prep] funciones, lea la [[!DNL Data Prep] descripción general](./home.md). Para aprender a utilizar conjuntos de asignaciones dentro de [!DNL Data Prep] API, lea la [[!DNL Data Prep] guía para desarrolladores](./api/overview.md).
