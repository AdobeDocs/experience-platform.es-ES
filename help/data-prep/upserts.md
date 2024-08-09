---
keywords: Experience Platform;inicio;temas populares;preparación de datos;preparación de datos;streaming;upsert;streaming upsert
title: Envío De Actualizaciones Parciales De Fila Al Perfil Del Cliente En Tiempo Real Mediante La Preparación De Datos
description: Obtenga información sobre cómo enviar actualizaciones parciales de fila al perfil del cliente en tiempo real mediante la preparación de datos.
exl-id: f9f9e855-0f72-4555-a4c5-598818fc01c2
source-git-commit: d62a61f44b27c0be882b5f29bfad5e423af7a1ca
workflow-type: tm+mt
source-wordcount: '1360'
ht-degree: 0%

---

# Enviar actualizaciones parciales de fila a [!DNL Real-Time Customer Profile] mediante [!DNL Data Prep]

>[!IMPORTANT]
>
>* La ingesta de mensajes de actualización de entidad del modelo de datos de experiencia (XDM) (con operaciones de PATCH de JSON) para actualizaciones de perfil a través de la entrada DCS ha quedado obsoleta. Siga los pasos descritos en esta guía como alternativa.
>
>* También puede usar el origen de la API HTTP para [introducir datos sin procesar en la entrada del DCS](../sources/tutorials/api/create/streaming/http.md#sending-messages-to-an-authenticated-streaming-connection) y especificar las asignaciones de datos necesarias para transformar los datos en mensajes compatibles con XDM para las actualizaciones de perfil.
>
>* Al utilizar matrices en actualizaciones de flujo continuo, debe utilizar explícitamente `upsert_array_append` o `upsert_array_replace` para definir la intención clara de la operación. Puede recibir errores si faltan estas funciones.

Use actualizaciones de flujo continuo en [!DNL Data Prep] para enviar actualizaciones de fila parciales a los datos de [!DNL Real-Time Customer Profile], a la vez que crea y establece nuevos vínculos de identidad con una sola solicitud de API.

Al transmitir las actualizaciones, puede conservar el formato de los datos mientras los traduce a [!DNL Real-Time Customer Profile] solicitudes de PATCH durante la ingesta. En función de las entradas que proporcione, [!DNL Data Prep] le permite enviar una sola carga útil de API y traducir los datos tanto a [!DNL Real-Time Customer Profile] PATCH como a [!DNL Identity Service] solicitudes CREATE.

[!DNL Data Prep] usa parámetros de encabezado para distinguir entre inserciones y actualizaciones. Todas las filas que utilicen actualizaciones deben tener un encabezado. Puede utilizar actualizaciones con o sin descriptores de identidad. Si usa actualizaciones con identidades, debe seguir los pasos de configuración descritos en la sección de [configuración del conjunto de datos de identidad](#configure-the-identity-dataset). Si utiliza actualizaciones sin identidades, no necesita proporcionar configuraciones de identidad en la solicitud. Lea la sección sobre [actualizaciones de transmisión sin identidades](#payload-without-identity-configuration) para obtener más información.

>[!NOTE]
>
>Para aprovechar la funcionalidad de actualización, se recomienda desactivar las configuraciones compatibles con XDM durante la ingesta de datos y volver a asignar la carga útil entrante mediante [Asignador de preparación de datos](./ui/mapping.md).

Este documento proporciona información sobre cómo transmitir actualizaciones en [!DNL Data Prep].

## Introducción

Esta descripción general requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Data Prep]](./home.md): [!DNL Data Prep] permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el modelo de datos de experiencia (XDM).
* [[!DNL Identity Service]](../identity-service/home.md): obtenga una mejor vista de los clientes individuales y su comportamiento al unir identidades entre dispositivos y sistemas.
* [Perfil del cliente en tiempo real](../profile/home.md): Proporciona un perfil de cliente unificado en tiempo real basado en datos agregados de múltiples fuentes.
* [Fuentes](../sources/home.md): El Experience Platform permite la ingesta de datos de varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.

## Usar actualizaciones de flujo continuo en [!DNL Data Prep] {#streaming-upserts-in-data-prep}

>[!NOTE]
>
>Las siguientes fuentes admiten el uso de actualizaciones de flujo continuo:<ul><li>[[!DNL Amazon Kinesis]](../sources/connectors/cloud-storage/kinesis.md)</li><li>[[!DNL Azure Event Hubs]](../sources/connectors/cloud-storage/eventhub.md)</li><li>[[!DNL HTTP API]](../sources/connectors/streaming/http.md)</li></ul>

### Flujo de trabajo de alto nivel de actualizaciones de streaming

La transmisión de actualizaciones en [!DNL Data Prep] funciona de la siguiente manera:

* Primero debe crear y habilitar un conjunto de datos para el consumo de [!DNL Profile]. Consulte la guía sobre [habilitar un conjunto de datos para [!DNL Profile]](../catalog/datasets/enable-for-profile.md) para obtener más información.
* Si se deben vincular nuevas identidades, también debe crear un conjunto de datos adicional **con el mismo esquema** que el conjunto de datos [!DNL Profile].
* Una vez que se hayan preparado los conjuntos de datos, debe crear un flujo de datos para asignar la solicitud entrante al conjunto de datos [!DNL Profile];
* A continuación, debe actualizar la solicitud entrante para incluir los encabezados necesarios. Estos encabezados definen:
   * La operación de datos que se necesita realizar con [!DNL Profile]: `create`, `merge` y `delete`.
   * La operación de identidad opcional que se va a realizar con [!DNL Identity Service]: `create`.

### Configuración del conjunto de datos de identidad {#configure-the-identity-dataset}

Si se deben vincular nuevas identidades, debe crear y pasar un conjunto de datos adicional en la carga útil entrante. Al crear un conjunto de datos de identidad, debe asegurarse de que se cumplan los siguientes requisitos:

* El conjunto de datos de identidad debe tener su esquema asociado como el conjunto de datos [!DNL Profile]. Una discrepancia en los esquemas puede provocar un comportamiento incoherente del sistema.
* Sin embargo, debe asegurarse de que el conjunto de datos de identidad sea diferente del conjunto de datos [!DNL Profile]. Si los conjuntos de datos son los mismos, los datos se sobrescribirán en lugar de actualizarse.
* Aunque el conjunto de datos inicial debe estar habilitado para [!DNL Profile], el conjunto de datos de identidad **no debe estar habilitado** para [!DNL Profile]. De lo contrario, los datos también se sobrescribirán en lugar de actualizarse. Sin embargo, el conjunto de datos de identidad **debe estar habilitado** para [!DNL Identity Service].

#### Campos obligatorios en los esquemas asociados al conjunto de datos de identidad {#identity-dataset-required-fileds}

Si el esquema contiene campos obligatorios, la validación del conjunto de datos debe suprimirse para permitir que [!DNL Identity Service] solo reciba las identidades. Puede suprimir la validación aplicando el valor `disabled` al parámetro `acp_validationContext`. Consulte el ejemplo siguiente:

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
| `flowId` | ID único para identificar un flujo de datos. Este identificador de flujo de datos debe corresponder a la conexión de origen creada con [!DNL Amazon Kinesis], [!DNL Azure Event Hubs] o [!DNL HTTP API]. Este flujo de datos también debe tener un conjunto de datos habilitado para [!DNL Profile] como conjunto de datos de destino. **Nota**: El ID del conjunto de datos de destino habilitado para [!DNL Profile] también se usa como parámetro de `datasetId`. |
| `imsOrgId` | El ID que corresponde a su organización. |
| `datasetId` | El identificador del conjunto de datos de destino habilitado para [!DNL Profile] de su flujo de datos. **Nota**: Este es el mismo ID que el ID del conjunto de datos de destino habilitado para [!DNL Profile] que se encuentra en su flujo de datos. |
| `operations` | Este parámetro describe las acciones que [!DNL Data Prep] realizará en función de la solicitud entrante. |
| `operations.data` | Define las acciones que se deben realizar en [!DNL Real-Time Customer Profile]. |
| `operations.identity` | Define las operaciones permitidas en los datos por [!DNL Identity Service]. |
| `operations.identityDatasetId` | (Opcional) ID del conjunto de datos de identidad que solo es necesario si se deben vincular nuevas identidades. |

#### Operaciones compatibles

[!DNL Real-Time Customer Profile] admite las siguientes operaciones:

| Operaciones | Descripción |
| --- | --- | 
| `create` | La operación predeterminada. Esto genera un método de creación de entidad XDM para [!DNL Real-Time Customer Profile]. |
| `merge` | Esto genera un método de actualización de entidad XDM para [!DNL Real-Time Customer Profile]. |
| `delete` | Esto genera un método de eliminación de entidad XDM para [!DNL Real-Time Customer Profile] y elimina permanentemente los datos de [!DNL Profile store]. |

[!DNL Identity Service] admite las siguientes operaciones:

| Operaciones | Descripciones |
| --- | --- |
| `create` | La única operación permitida para este parámetro. Si `create` se pasa como un valor para `operations.identity`, entonces [!DNL Data Prep] genera una solicitud de creación de entidad XDM para [!DNL Identity Service]. Si la identidad ya existe, se ignora la identidad. **Nota:** Si `operations.identity` está establecido en `create`, también se debe especificar `identityDatasetId`. El mensaje de creación de entidad XDM generado internamente por el componente [!DNL Data Prep] se generará para este ID de conjunto de datos. |

### Carga útil sin configuración de identidad {#payload-without-identity-configuration}

Si no es necesario vincular nuevas identidades, puede omitir los parámetros `identity` y `identityDatasetId` en las operaciones. Al hacerlo, se envían datos solamente a [!DNL Real-Time Customer Profile] y se omite [!DNL Identity Service]. Consulte la carga útil siguiente para ver un ejemplo:

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

Para las actualizaciones de XDM, el esquema debe estar habilitado para [!DNL Profile] y contener una identidad principal. Puede especificar la identidad principal de un esquema XDM de dos formas:

* Designar un campo estático como identidad principal en el esquema XDM;
* Designe uno de los campos de identidad como identidad principal a través del grupo de campos mapa de identidad en el esquema XDM.

### Designar un campo estático como campo de identidad principal en el esquema XDM

En el ejemplo siguiente, `state`, `homePhone.number` y otros atributos se actualizan con sus respectivos valores dados en [!DNL Profile] con la identidad principal de `sampleEmail@gmail.com`. A continuación, el componente [!DNL Data Prep] de flujo continuo genera un mensaje de actualización de entidad XDM. [!DNL Real-Time Customer Profile] confirma ese mensaje de actualización de XDM para actualizar el registro de perfil.

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

En este ejemplo, el encabezado contiene el atributo `operations` con las propiedades `identity` y `identityDatasetId`. Esto permite combinar datos con [!DNL Real-Time Customer Profile] y también pasar identidades a [!DNL Identity Service].

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

A continuación se describe una lista de limitaciones conocidas que deben tenerse en cuenta al transmitir actualizaciones con [!DNL Data Prep]:

* El método de actualizaciones de flujo continuo solo se debe usar cuando se envíen actualizaciones de fila parciales a [!DNL Real-Time Customer Profile]. Las actualizaciones parciales de fila **no** son consumidas por el lago de datos.
* El método de actualizaciones de streaming no admite la actualización, el reemplazo y la eliminación de identidades. Si no existen, se crean nuevas identidades. Por lo tanto, la operación `identity` siempre debe configurarse para crear. Si ya existe una identidad, la operación no es operativa.
* Actualmente, el método de actualizaciones de streaming no admite [Adobe Experience Platform Web SDK](/help/web-sdk/home.md) ni [Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/documentation/).

## Pasos siguientes

Al leer este documento, debería haber comprendido cómo transmitir actualizaciones de filas en [!DNL Data Prep] para enviar actualizaciones de filas parciales a los datos de [!DNL Real-Time Customer Profile], a la vez que crea y vincula identidades con una sola solicitud de API. Para obtener más información sobre otras características de [!DNL Data Prep], lea la [[!DNL Data Prep] descripción general](./home.md). Para obtener información sobre cómo usar conjuntos de asignaciones en la API [!DNL Data Prep], lea la [[!DNL Data Prep] guía para desarrolladores](./api/overview.md).
