---
title: Conectar Azure Blob Storage a Experience Platform mediante la API de Flow Service
description: Obtenga información sobre cómo conectar Adobe Experience Platform al blob de Azure mediante la API de Flow Service.
exl-id: 4ab8033f-697a-49b6-8d9c-1aadfef04a04
source-git-commit: 8e932a25026bef2b785cfddfb8b668b1dd47eb0d
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 3%

---

# Conectar [!DNL Azure Blob Storage] a Experience Platform mediante la API

Lea esta guía para aprender a conectar su cuenta de [!DNL Azure Blobg Storage] a Adobe Experience Platform mediante la [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Experience Platform.
* [Zonas protegidas](../../../../../sandboxes/home.md): Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Experience Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

### Uso de API de Experience Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Experience Platform, consulte la guía sobre [introducción a las API de Experience Platform](../../../../../landing/api-guide.md).

### Recopilar credenciales necesarias

Lea la [[!DNL Azure Blob Storage] descripción general](../../../../connectors/cloud-storage/blob.md#authentication) para obtener información sobre la autenticación.

## Conecte su cuenta de [!DNL Azure Blob Storage] a Experience Platform {#connect}

Lea los pasos siguientes para obtener información sobre cómo conectar su cuenta de [!DNL Azure Blob Storage] a Experience Platform.

### Crear una conexión base

>[!NOTE]
>
>Una vez creada, no se puede cambiar el tipo de autenticación de una conexión base de [!DNL Azure Blob Storage]. Para cambiar el tipo de autenticación, debe crear una nueva conexión base.

Una conexión base vincula el origen a Experience Platform y almacena los detalles de autenticación, el estado de la conexión y un ID único. Utilice este ID para examinar los archivos de origen e identificar elementos específicos que se van a introducir, incluidos sus tipos de datos y formatos.

Puede conectar su cuenta de [!DNL Azure Blob Storage] a Experience Platform mediante los siguientes tipos de autenticación:

* **Autenticación de clave de cuenta**: Utiliza la clave de acceso de la cuenta de almacenamiento para autenticarse y conectarse a su cuenta de [!DNL Azure Blob Storage].
* **Firma de acceso compartido (SAS)**: Utiliza un URI de SAS para proporcionar acceso delegado y limitado en el tiempo a los recursos de su cuenta de [!DNL Azure Blob Storage].
* **Autenticación basada en entidad de seguridad de servicio**: Utiliza una entidad de seguridad de servicio de Azure Active Directory (AAD) (ID de cliente y secreto) para autenticarse de forma segura en su cuenta de Azure Blob Storage.

**Formato de API**

```https
POST /connections
```

Para crear un identificador de conexión base, realice una petición POST al extremo `/connections` y proporcione sus credenciales de autenticación como parte de los parámetros de solicitud.

>[!BEGINTABS]

>[!TAB Autenticación de clave de cuenta]

Para usar la autenticación de clave de cuenta, proporcione valores para `connectionString`, `container` y `folderPath`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Azure Blob Storage connection using connectingString",
    "description": "Azure Blob Storage connection using connectionString",
    "auth": {
      "specName": "ConnectionString",
      "params": {
        "connectionString": "DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}",
        "container": "acme-blob-container",
        "folderPath": "/acme/customers/salesData"
      }
    },
    "connectionSpec": {
      "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
      "version": "1.0"
    }
  }'
```

| Parámetro | Descripción |
| --- | --- |
| `connectionString` | Cadena de conexión de su cuenta de [!DNL Azure Blob Storage]. El patrón de cadena de conexión es: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY};EndpointSuffix=core.windows.net`. |
| `container` | Nombre del contenedor [!DNL Azure Blob Storage] donde se almacenan los archivos de datos. |
| `folderPath` | Ruta de acceso dentro del contenedor especificado donde se encuentran los archivos. |
| `connectionSpec.id` | Id. de especificación de conexión del origen [!DNL Azure Blob Storage]. Este identificador se corrigió como: `4c10e202-c428-4796-9208-5f1f5732b1cf`. |

>[!TAB Firma de acceso compartido]

Para usar la firma de acceso compartido, proporcione valores para `sasUri`, `container` y `folderPath`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Azure Blob Storage source connection using SAS URI",
    "description": "Azure Blob Storage source connection using SAS URI",
    "auth": {
      "specName": "SAS URI Authentication",
      "params": {
        "sasUri": "https://{ACCOUNT_NAME}.blob.core.windows.net/?sv={STORAGE_VERSION}&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>",
        "container": "acme-blob-container",
        "folderPath": "/acme/customers/salesData"
      }
    },
    "connectionSpec": {
      "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
      "version": "1.0"
    }
  }'
```

| Parámetro | Descripción |
| --- | --- |
| `sasUri` | El URI de firma de acceso compartido que puede utilizar como tipo de autenticación alternativo para conectar su cuenta. El patrón de URI de SAS es: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv={STORAGE_VERSION}&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}`. |
| `container` | Nombre del contenedor [!DNL Azure Blob Storage] donde se almacenan los archivos de datos. |
| `folderPath` | Ruta de acceso dentro del contenedor especificado donde se encuentran los archivos. |
| `connectionSpec.id` | Id. de especificación de conexión del origen [!DNL Azure Blob Storage]. Este identificador se corrigió como: `4c10e202-c428-4796-9208-5f1f5732b1cf`. |

>[!TAB Autenticación basada en entidad de seguridad de servicio]

Para conectarse a través de la autenticación basada en la entidad de seguridad de servicio, proporcione valores para: `serviceEndpoint`, `servicePrincipalId`, `servicePrincipalKey`, `accountKind`, `tenant`, `container` y `folderPath`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Azure Blob Storage source connection using service principal based authentication",
    "description": "Azure Blob Storage source connection using service principal based authentication",
    "auth": {
      "specName": "Service Principal Based Authentication",
      "params": {
        "serviceEndpoint": "{SERVICE_ENDPOINT}",
        "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
        "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}",
        "accountKind": "{ACCOUNT_KIND}",
        "tenant": "{TENANT}",
        "container": "acme-blob-container",
        "folderPath": "/acme/customers/salesData"
      }
    },
    "connectionSpec": {
      "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
      "version": "1.0"
    }
  }'
```

| Parámetro | Descripción |
| --- | --- |
| `serviceEndpoint` | La dirección URL de extremo de su cuenta de [!DNL Azure Blob Storage]. Normalmente en el formato: `https://{ACCOUNT_NAME}.blob.core.windows.net`. |
| `servicePrincipalId` | Identificador de cliente/aplicación de la entidad de seguridad del servicio de Azure Active Directory (AAD) que se usa para la autenticación. |
| `servicePrincipalKey` | El secreto de cliente o la contraseña asociados con la entidad de seguridad del servicio de Azure. |
| `accountKind` | El tipo de su cuenta de [!DNL Azure Blob Storage]. Los valores comunes incluyen `Storage` (propósito general V1), `StorageV2` (propósito general V2), `BlobStorage` y `BlockBlobStorage`. |
| `tenant` | Identificador de inquilino de Azure Active Directory (AAD) donde está registrada la entidad de seguridad de servicio. |
| `container` | Nombre del contenedor [!DNL Azure Blob Storage] donde se almacenan los archivos de datos. |
| `folderPath` | Ruta de acceso dentro del contenedor especificado donde se encuentran los archivos. |
| `connectionSpec.id` | Id. de especificación de conexión del origen [!DNL Azure Blob Storage]. Este identificador se corrigió como: `4c10e202-c428-4796-9208-5f1f5732b1cf`. |

>[!ENDTABS]

Una respuesta correcta devuelve detalles de la conexión base recién creada, incluido su identificador único (`id`). Este ID es necesario en el siguiente paso para crear una conexión de origen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```



## Próximos pasos

Siguiendo este tutorial, ha creado una conexión de [!DNL Blob] mediante API y se ha obtenido un ID único como parte del cuerpo de respuesta. Puede usar este identificador de conexión para [explorar los almacenes en la nube mediante la API de Flow Service](../../explore/cloud-storage.md).
