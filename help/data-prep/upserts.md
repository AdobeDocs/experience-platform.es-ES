---
keywords: Experience Platform;inicio;temas populares;preparación de datos;preparación de datos;flujo continuo;actualización;flujo continuo
title: Enviar Actualizaciones Parciales De Fila Al Servicio De Perfil Mediante La Preparación De Datos
description: Este documento proporciona información sobre cómo enviar actualizaciones de fila parciales al servicio de perfil mediante la preparación de datos.
exl-id: f9f9e855-0f72-4555-a4c5-598818fc01c2
source-git-commit: cc3ecbd8544839246d54f72b894ad27e850c0c90
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 1%

---

# Enviar actualizaciones de fila parciales a [!DNL Profile Service] using [!DNL Data Prep]

Transmisión de fuentes en [!DNL Data Prep] permite enviar actualizaciones de fila parciales a [!DNL Profile Service] al mismo tiempo que crea y establece nuevos vínculos de identidad con una única solicitud de API.

Si transmite archivos push, puede conservar el formato de sus datos y traducir esos datos a [!DNL Profile Service] solicitudes del PATCH durante la ingesta. En función de las entradas que proporcione, [!DNL Data Prep] permite enviar una única carga útil de API y traducir los datos a ambos [!DNL Profile Service] PATCH y [!DNL Identity Service] CREE solicitudes.

Este documento proporciona información sobre cómo retransmitir [!DNL Data Prep].

## Primeros pasos

Esta descripción general requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Data Prep]](./home.md): [!DNL Data Prep] permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el modelo de datos de Experience (XDM).
* [[!DNL Identity Service]](../identity-service/home.md): Obtenga una mejor visión de los clientes individuales y su comportamiento al unir identidades entre dispositivos y sistemas.
* [Perfil del cliente en tiempo real](../profile/home.md): Proporciona un perfil de cliente unificado en tiempo real basado en datos agregados de varias fuentes.
* [Fuentes](../sources/home.md): Experience Platform permite la ingesta de datos de varias fuentes, al mismo tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.

## Use fuentes de flujo continuo en [!DNL Data Prep] {#streaming-upserts-in-data-prep}

>[!NOTE]
>
>Las siguientes fuentes admiten el uso de posters de flujo continuo:<ul><li>[[!DNL Amazon Kinesis]](../sources/connectors/cloud-storage/kinesis.md)</li><li>[[!DNL Azure Event Hubs]](../sources/connectors/cloud-storage/eventhub.md)</li><li>[[!DNL HTTP API]](../sources/connectors/streaming/http.md)</li></ul>

### La transmisión confirma el flujo de trabajo de alto nivel

Transmisión de fuentes en [!DNL Data Prep] funciona de la siguiente manera:

* Primero debe crear y habilitar un conjunto de datos para [!DNL Profile] consumo. Consulte la guía de [activación de un conjunto de datos para [!DNL Profile]](../catalog/datasets/enable-for-profile.md) para obtener más información;
* Si se deben vincular nuevas identidades, también se debe crear un conjunto de datos adicional **con el mismo esquema** como su [!DNL Profile] conjunto de datos;
* Una vez preparados los conjuntos de datos, debe crear un flujo de datos para asignar la solicitud entrante al [!DNL Profile] conjunto de datos;
* A continuación, debe actualizar la solicitud entrante para incluir los encabezados necesarios. Estos encabezados definen:
   * La operación de datos que debe realizarse con [!DNL Profile]: `create`, `merge`y `delete`;
   * La operación de identidad opcional que se va a realizar con [!DNL Identity Service]: `create`.

### Configuración del conjunto de datos de identidad

Si se deben vincular nuevas identidades, se debe crear y pasar un conjunto de datos adicional en la carga útil entrante. Al crear un conjunto de datos de identidad, debe asegurarse de que se cumplan los siguientes requisitos:

* El conjunto de datos de identidad debe tener su esquema asociado como [!DNL Profile] conjunto de datos. Una discordancia de esquemas puede conducir a un comportamiento incoherente del sistema;
* Sin embargo, debe asegurarse de que el conjunto de datos de identidad sea diferente del [!DNL Profile] conjunto de datos. Si los conjuntos de datos son iguales, entonces los datos se sobrescriben en lugar de actualizarse;
* Mientras que el conjunto de datos inicial debe estar habilitado para [!DNL Profile], el conjunto de datos de identidad **no debe** estar habilitado para [!DNL Profile]. De lo contrario, los datos también se sobrescribirán en lugar de actualizarse.

#### Campos requeridos en los esquemas asociados con el conjunto de datos de identidad {#identity-dataset-required-fileds}

Si el esquema contiene campos obligatorios, la validación del conjunto de datos debe suprimirse para habilitar [!DNL Identity Service] solo para recibir las identidades. Puede suprimir la validación aplicando la variable `disabled` a la variable `acp_validationContext` parámetro. Consulte el ejemplo siguiente:

```shell
curl -X POST 'https://platform.adobe.io/data/foundation/catalog/dataSets/62257bef7a75461948ebcaaa' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "tags":{
        "acp_validationContext": ["disabled"]
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
| `flowId` | ID exclusivo para identificar un flujo de datos. Este ID de flujo de datos debe corresponder a la conexión de origen creada con [!DNL Amazon Kinesis], [!DNL Azure Event Hubs]o [!DNL HTTP API]. Este flujo de datos también debería tener un [!DNL Profile]conjunto de datos habilitado como conjunto de datos de destino. **Nota**: El ID de la variable [!DNL Profile]El conjunto de datos de target habilitado también se usa como `datasetId` parámetro. |
| `imsOrgId` | El ID que corresponde a su organización. |
| `datasetId` | El ID de la variable [!DNL Profile]conjunto de datos de target habilitado para su flujo de datos. **Nota**: Es el mismo ID que la variable [!DNL Profile]El ID del conjunto de datos de target habilitado se encuentra en el flujo de datos. |
| `operations` | Este parámetro describe las acciones que [!DNL Data Prep] se basará en la solicitud entrante. |
| `operations.data` | Define las acciones que se deben realizar en [!DNL Profile Service]. |
| `operations.identity` | Define las operaciones permitidas en los datos por [!DNL Identity Service]. |
| `operations.identityDatasetId` | (Opcional) El ID del conjunto de datos de identidad que solo es necesario si se deben vincular nuevas identidades. |

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
| `create` | La única operación permitida para este parámetro. If `create` se pasa como un valor para `operations.identity`, luego [!DNL Data Prep] genera una solicitud de creación de entidad XDM para [!DNL Identity Service]. Si la identidad ya existe, se ignora la identidad. **Nota:** If `operations.identity` está configurado como `create`, luego la variable `identityDatasetId` también debe especificarse. La entidad XDM crea un mensaje generado internamente por [!DNL Data Prep] se generará para este id de conjunto de datos. |

### Carga útil sin configuración de identidad

Si no es necesario vincular nuevas identidades, puede omitir la variable `identity` y `identityDatasetId` en las operaciones. Si lo hace, solo envía datos a [!DNL Profile Service] y omite el [!DNL Identity Service]. Consulte la carga útil siguiente para ver un ejemplo:

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

## Pasar identidades principales de forma dinámica

Para las actualizaciones XDM, el esquema debe estar habilitado para [!DNL Profile] y contienen una identidad principal. Puede especificar la identidad principal de un esquema XDM de dos maneras:

* Designe un campo estático como la identidad principal en el esquema XDM;
* Designe uno de los campos de identidad como identidad principal a través del grupo de campos de mapa de identidad en el esquema XDM.

### Designar un campo estático como el campo de identidad principal en el esquema XDM

En el ejemplo siguiente, `state`, `homePhone.number` y otros atributos se añaden con sus respectivos valores dados en la variable [!DNL Profile] con la identidad principal de `sampleEmail@gmail.com`. El flujo continuo genera un mensaje de actualización de entidad XDM [!DNL Data Prep] componente. [!DNL Profile Service] a continuación, confirma que el mensaje de actualización de XDM confirma el registro de perfil.

>[!NOTE]
>
>En este ejemplo, las identidades no se vinculan entre sí, ya que no hay operaciones definidas para la identidad.

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

En este ejemplo, el encabezado contiene la variable `operations` con la variable `identity` y `identityDatasetId` propiedades. Esto permite combinar los datos con [!DNL Profile Service] y también para las identidades que deben pasarse a [!DNL Identity Service].

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

A continuación se describe una lista de limitaciones conocidas que se deben tener en cuenta a la hora de transmitir mensajes push con [!DNL Data Prep]:

* El método de actualización de flujo continuo solo debe usarse al enviar actualizaciones de fila parciales a [!DNL Profile Service]. Las actualizaciones de fila parciales son **not** consumido por el lago de datos.
* El método de actualización de flujo continuo no admite la actualización, sustitución y eliminación de identidades. Las identidades nuevas se crean si no existen. Por lo tanto, `identity` siempre debe estar configurado para crear. Si ya existe una identidad, la operación es una no-op.
* Actualmente, el método de actualización de flujo continuo solo admite atributos primitivos de un solo valor (como enteros, fechas, marcas de tiempo y cadenas) y objetos.
* El método de actualización de flujo continuo actualmente no es compatible [SDK web de Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=es) y [SDK de Adobe Experience Platform Mobile](https://aep-sdks.gitbook.io/docs/).

## Pasos siguientes

Al leer este documento, ahora debe comprender cómo se retransmiten las subidas [!DNL Data Prep] para enviar actualizaciones de fila parciales a su [!DNL Profile Service] , mientras que también crea y vincula identidades con una única solicitud de API. Para obtener más información sobre otros [!DNL Data Prep] características, lea la [[!DNL Data Prep] información general](./home.md). Para aprender a utilizar conjuntos de asignación dentro de la variable [!DNL Data Prep] API, lea la [[!DNL Data Prep] guía para desarrolladores](./api/overview.md).
