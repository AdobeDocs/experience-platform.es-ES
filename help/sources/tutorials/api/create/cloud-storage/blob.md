---
title: Crear una conexión base de Azure Blob mediante la API de Flow Service
description: Obtenga información sobre cómo conectar Adobe Experience Platform al blob de Azure mediante la API de Flow Service.
exl-id: 4ab8033f-697a-49b6-8d9c-1aadfef04a04
source-git-commit: 922e9a26f1791056b251ead2ce2702dfbf732193
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 1%

---

# Crear un [!DNL Azure Blob] conexión base mediante el [!DNL Flow Service] API

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Este tutorial lo acompañará durante los pasos para crear una conexión base para [!DNL Azure Blob] (en lo sucesivo, &quot;[!DNL Blob]&quot;) utilizando el [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Primeros pasos

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos desde varias fuentes y, al mismo tiempo, le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Zonas protegidas](../../../../../sandboxes/home.md): El Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para crear correctamente una [!DNL Blob] conexión de origen mediante [!DNL Flow Service] API.

### Recopilar credenciales necesarias

Para que [!DNL Flow Service] para conectarse con su [!DNL Blob] almacenamiento, debe proporcionar valores para la siguiente propiedad de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `connectionString` | Cadena que contiene la información de autorización necesaria para la autenticación [!DNL Blob] al Experience Platform. El [!DNL Blob] el patrón de cadena de conexión es: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. Para obtener más información acerca de las cadenas de conexión, consulte esto [!DNL Blob] documento en [configurar cadenas de conexión](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |
| `sasUri` | El URI de firma de acceso compartido que puede utilizar como tipo de autenticación alternativo para conectar su [!DNL Blob] cuenta. El [!DNL Blob] El patrón de URI de SAS es: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` Para obtener más información, consulte [!DNL Blob] documento en [URI de firma de acceso compartido](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |
| `container` | El nombre del contenedor al que desea designar el acceso. Al crear una cuenta nueva con [!DNL Blob] origen, puede proporcionar un nombre de contenedor para especificar el acceso del usuario a la subcarpeta que elija. |
| `folderPath` | La ruta a la carpeta a la que desea proporcionar acceso. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. Identificador de especificación de conexión para [!DNL Blob] es: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

### Uso de API de Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../../../landing/api-guide.md).

## Crear una conexión base

Una conexión base retiene información entre el origen y Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el ID único de conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

El [!DNL Blob] El origen admite la autenticación de cadena de conexión y firma de acceso compartido (SAS). Un URI de firma de acceso compartido (SAS) permite la autorización delegada segura a su [!DNL Blob] cuenta. Puede utilizar SAS para crear credenciales de autenticación con distintos grados de acceso, ya que la autenticación basada en SAS le permite establecer permisos, fechas de inicio y caducidad, así como disposiciones para recursos específicos.

Durante este paso, también puede designar las subcarpetas a las que tendrá acceso su cuenta definiendo el nombre del contenedor y la ruta de acceso a la subcarpeta.

Para crear un ID de conexión base, realice una solicitud de POST al `/connections` extremo al proporcionar su [!DNL Blob] credenciales de autenticación como parte de los parámetros de solicitud.

**Formato de API**

```http
POST /connections
```

**Solicitud**

>[!BEGINTABS]

>[!TAB Cadena de conexión]

La siguiente solicitud crea una conexión base para [!DNL Blob] uso de la autenticación basada en cadenas de conexión:

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

| Propiedad | Descripción |
| -------- | ----------- |
| `auth.params.connectionString` | Cadena de conexión necesaria para acceder a los datos del almacenamiento del blob. El patrón de cadena de conexión de blob es: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |
| `connectionSpec.id` | El ID de especificación de la conexión de almacenamiento del blob es: `4c10e202-c428-4796-9208-5f1f5732b1cf` |

>[!TAB Autenticación de URI de SAS]

Para crear un [!DNL Blob] conexión de blob con el URI de firma de acceso compartido, realice una solicitud de POST al [!DNL Flow Service] API mientras proporciona valores para su [!DNL Blob] `sasUri`.

La siguiente solicitud crea una conexión base para [!DNL Blob] uso del URI de firma de acceso compartido:

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

| Propiedad | Descripción |
| -------- | ----------- |
| `auth.params.connectionString` | El URI de SAS necesario para acceder a los datos de su [!DNL Blob] almacenamiento. El [!DNL Blob] El patrón de URI de SAS es: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>`. |
| `connectionSpec.id` | El [!DNL Blob] ID de especificación de conexión de almacenamiento: `4c10e202-c428-4796-9208-5f1f5732b1cf` |

>[!ENDTABS]

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión base recién creada, incluido su identificador único (`id`). Este ID es necesario en el siguiente paso para crear una conexión de origen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

## Pasos siguientes

Al seguir este tutorial, ha creado un [!DNL Blob] Se obtuvo una conexión mediante API y un ID único como parte del cuerpo de respuesta. Puede usar este ID de conexión para lo siguiente [explore los almacenes en la nube mediante la API de Flow Service](../../explore/cloud-storage.md).
