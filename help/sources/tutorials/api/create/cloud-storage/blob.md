---
keywords: Experience Platform;inicio;temas populares;Azure;azure blob;blob;Blob
solution: Experience Platform
title: Creación de una conexión de base de Azure Blob mediante la API de servicio de flujo
topic-legacy: overview
type: Tutorial
description: Obtenga información sobre cómo conectar Adobe Experience Platform a Azure Blob mediante la API de servicio de flujo.
exl-id: 4ab8033f-697a-49b6-8d9c-1aadfef04a04
source-git-commit: 0d891acd4e33eb7080da44e204672dc3601cf166
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 2%

---

# Cree un [!DNL Azure Blob] conexión base utilizando [!DNL Flow Service] API

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Este tutorial le guía por los pasos para crear una conexión base para [!DNL Azure Blob] (en lo sucesivo, &quot;el[!DNL Blob]&quot;) usando la variable [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Primeros pasos

Esta guía requiere conocer los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos de varias fuentes, al mismo tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que debe conocer para crear correctamente un [!DNL Blob] conexión de origen utilizando la variable [!DNL Flow Service] API.

### Recopilar las credenciales necesarias

Para [!DNL Flow Service] para conectarse con su [!DNL Blob] , debe proporcionar valores para la siguiente propiedad de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `connectionString` | Una cadena que contiene la información de autorización necesaria para autenticarse [!DNL Blob] al Experience Platform. La variable [!DNL Blob] el patrón de cadena de conexión es: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. Para obtener más información sobre cadenas de conexión, consulte esta [!DNL Blob] documento en [configuración de cadenas de conexión](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |
| `sasUri` | El URI de firma de acceso compartido que puede usar como tipo de autenticación alternativo para conectar su [!DNL Blob] cuenta. La variable [!DNL Blob] El patrón de URI SAS es: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` Para obtener más información, consulte [!DNL Blob] documento en [URI de firma de acceso compartido](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de un origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y de origen. El ID de especificación de conexión para [!DNL Blob] es: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

### Uso de las API de plataforma

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../../../landing/api-guide.md).

## Creación de una conexión base

Una conexión base retiene información entre la fuente y la plataforma, incluidas las credenciales de autenticación de la fuente, el estado actual de la conexión y el ID de conexión base único. El ID de conexión base le permite explorar y navegar archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un ID de conexión base, realice una solicitud de POST al `/connections` al proporcionar su [!DNL Blob] credenciales de autenticación como parte de los parámetros de solicitud.

### Cree un [!DNL Blob] conexión base mediante autenticación basada en cadenas de conexión

Para crear un [!DNL Blob] conexión base mediante autenticación basada en cadenas de conexión, realice una solicitud de POST al [!DNL Flow Service] API al proporcionar su [!DNL Blob] `connectionString`.

**Formato de API**

```http
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para [!DNL Blob] mediante autenticación basada en cadenas de conexión:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Blob connection using connectionString",
        "description": "Azure Blob connection using connectionString",
        "auth": {
            "specName": "ConnectionString",
            "params": {
                "connectionString": "DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}"
            }
        },
        "connectionSpec": {
            "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
            "version": "1.0"
        }
    }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `auth.params.connectionString` | La cadena de conexión necesaria para acceder a los datos del almacenamiento del blob. El patrón de la cadena de conexión Blob es: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |
| `connectionSpec.id` | El ID de especificación de la conexión de almacenamiento Blob es: `4c10e202-c428-4796-9208-5f1f5732b1cf` |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión base recién creada, incluido su identificador único (`id`). Este ID es necesario en el paso siguiente para crear una conexión de origen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

### Cree un [!DNL Blob] conexión base con URI de firma de acceso compartido

Un URI de firma de acceso compartido (SAS) permite una autorización delegada segura en su [!DNL Blob] cuenta. Puede utilizar SAS para crear credenciales de autenticación con distintos grados de acceso, ya que la autenticación basada en SAS permite establecer permisos, fechas de inicio y caducidad, así como disposiciones para recursos específicos.

Para crear un [!DNL Blob] conexión blob con URI de firma de acceso compartido, realice una solicitud de POST al [!DNL Flow Service] API al proporcionar valores para su [!DNL Blob] `sasUri`.

**Formato de API**

```http
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para [!DNL Blob] usando el URI de firma de acceso compartido:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Blob source connection using SAS URI",
        "description": "Azure Blob source connection using SAS URI",
        "auth": {
            "specName": "SAS URI Authentication",
            "params": {
                "sasUri": "https://{ACCOUNT_NAME}.blob.core.windows.net/?sv={STORAGE_VERSION}&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>"
            }
        },
        "connectionSpec": {
            "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
            "version": "1.0"
        }
    }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `auth.params.connectionString` | El URI de SAS necesario para acceder a los datos de su [!DNL Blob] almacenamiento. La variable [!DNL Blob] El patrón de URI SAS es: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>`. |
| `connectionSpec.id` | La variable [!DNL Blob] el ID de especificación de conexión de almacenamiento es: `4c10e202-c428-4796-9208-5f1f5732b1cf` |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión base recién creada, incluido su identificador único (`id`). Este ID es necesario en el paso siguiente para crear una conexión de origen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

## Pasos siguientes

Al seguir este tutorial, ha creado un [!DNL Blob] se obtuvo una conexión mediante API y un ID único como parte del cuerpo de respuesta. Puede utilizar este ID de conexión para [explorar las tiendas en la nube mediante la API de servicio de flujo](../../explore/cloud-storage.md).
