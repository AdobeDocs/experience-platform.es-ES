---
title: Crear una conexión base de Azure Blob mediante la API de Flow Service
description: Obtenga información sobre cómo conectar Adobe Experience Platform al blob de Azure mediante la API de Flow Service.
exl-id: 4ab8033f-697a-49b6-8d9c-1aadfef04a04
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 3%

---

# Crear una conexión base [!DNL Azure Blob] mediante la API [!DNL Flow Service]

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Este tutorial proporciona los pasos para crear una conexión base para [!DNL Azure Blob] (en adelante denominada &quot;[!DNL Blob]&quot;) mediante la [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Experience Platform.
* [Zonas protegidas](../../../../../sandboxes/home.md): Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Experience Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que necesitará conocer para crear correctamente una conexión de origen de [!DNL Blob] mediante la API [!DNL Flow Service].

### Recopilar credenciales necesarias

Para que [!DNL Flow Service] se conecte con su almacenamiento de [!DNL Blob], debe proporcionar valores para la siguiente propiedad de conexión:

>[!BEGINTABS]

>[!TAB Autenticación de cadena de conexión]

| Credencial | Descripción |
| --- | --- |
| `connectionString` | Cadena que contiene la información de autorización necesaria para autenticar [!DNL Blob] en Experience Platform. El patrón de cadena de conexión [!DNL Blob] es: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. Para obtener más información sobre las cadenas de conexión, consulte este documento de [!DNL Blob] en [configuración de cadenas de conexión](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. El id. de especificación de conexión para [!DNL Blob] es: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

>[!TAB Autenticación de URI de SAS]

| Credencial | Descripción |
| --- | --- |
| `sasUri` | URI de firma de acceso compartido que puede usar como tipo de autenticación alternativo para conectar su cuenta de [!DNL Blob]. El patrón de URI de SAS [!DNL Blob] es: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` Para obtener más información, consulte este documento de [!DNL Blob] sobre [URI de firma de acceso compartido](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |
| `container` | El nombre del contenedor al que desea designar el acceso. Al crear una nueva cuenta con el origen [!DNL Blob], puede proporcionar un nombre de contenedor para especificar el acceso del usuario a la subcarpeta que elija. |
| `folderPath` | La ruta a la carpeta a la que desea proporcionar acceso. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. El id. de especificación de conexión para [!DNL Blob] es: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

>[!ENDTABS]

### Uso de API de Experience Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Experience Platform, consulte la guía sobre [introducción a las API de Experience Platform](../../../../../landing/api-guide.md).

## Crear una conexión base

>[!TIP]
>
>Una vez creada, no se puede cambiar el tipo de autenticación de una conexión base de [!DNL Blob]. Para cambiar el tipo de autenticación, debe crear una nueva conexión base.

Una conexión base retiene información entre el origen y Experience Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el identificador único de la conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

El origen [!DNL Blob] admite la autenticación de cadena de conexión y firma de acceso compartido (SAS). Un URI de firma de acceso compartido (SAS) permite la autorización delegada segura en su cuenta de [!DNL Blob]. Puede utilizar SAS para crear credenciales de autenticación con distintos grados de acceso, ya que la autenticación basada en SAS le permite establecer permisos, fechas de inicio y caducidad, así como disposiciones para recursos específicos.

Durante este paso, también puede designar las subcarpetas a las que tendrá acceso su cuenta definiendo el nombre del contenedor y la ruta de acceso a la subcarpeta.

Para crear un identificador de conexión base, realice una petición POST al extremo `/connections` y proporcione sus credenciales de autenticación [!DNL Blob] como parte de los parámetros de solicitud.

**Formato de API**

```http
POST /connections
```

**Solicitud**

>[!BEGINTABS]

>[!TAB Cadena de conexión]

La siguiente solicitud crea una conexión base para [!DNL Blob] mediante la autenticación basada en cadena de conexión:

+++Solicitud

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
| `connectionSpec.id` | El id. de especificación de conexión de almacenamiento del blob es: `4c10e202-c428-4796-9208-5f1f5732b1cf` |

+++

+++Respuesta

Una respuesta correcta devuelve detalles de la conexión base recién creada, incluido su identificador único (`id`). Este ID es necesario en el siguiente paso para crear una conexión de origen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

+++

>[!TAB Autenticación de URI de SAS]

Para crear una conexión de [!DNL Blob] con el URI de firma de acceso compartido, realice una petición POST a la API [!DNL Flow Service] y proporcione los valores para [!DNL Blob] `sasUri`.

+++Solicitud

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
| `auth.params.connectionString` | URI de SAS necesario para tener acceso a los datos del almacenamiento de [!DNL Blob]. El patrón de URI de SAS [!DNL Blob] es: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>`. |
| `connectionSpec.id` | El id. de especificación de conexión de almacenamiento [!DNL Blob] es: `4c10e202-c428-4796-9208-5f1f5732b1cf` |

+++

+++Respuesta

Una respuesta correcta devuelve detalles de la conexión base recién creada, incluido su identificador único (`id`). Este ID es necesario en el siguiente paso para crear una conexión de origen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

+++

>[!ENDTABS]

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión de [!DNL Blob] mediante API y se ha obtenido un ID único como parte del cuerpo de respuesta. Puede usar este identificador de conexión para [explorar los almacenes en la nube mediante la API de Flow Service](../../explore/cloud-storage.md).
