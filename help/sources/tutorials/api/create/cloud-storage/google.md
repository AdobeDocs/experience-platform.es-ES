---
title: Crear una conexión base de Google Cloud Storage mediante la API de Flow Service
description: Obtenga información sobre cómo conectar Adobe Experience Platform a una cuenta de Google Cloud Storage mediante la API de Flow Service.
exl-id: 321d15eb-82c0-45a7-b257-1096c6db6b18
source-git-commit: 3636b785d82fa2e49f76825650e6159be119f8b4
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 4%

---

# Crear una conexión base [!DNL Google Cloud Storage] mediante la API [!DNL Flow Service]

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Este tutorial lo guiará para crear una conexión base para [!DNL Google Cloud Storage] mediante la [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): [!DNL Experience Platform] permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de [!DNL Platform].
* [Zonas protegidas](../../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola instancia de [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que necesitará conocer para conectarse correctamente a una cuenta de Google Cloud Storage mediante la API [!DNL Flow Service].

### Recopilar credenciales necesarias

Para que [!DNL Flow Service] se conecte con su cuenta de [!DNL Google Cloud Storage], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `accessKeyId` | Cadena alfanumérica de 61 caracteres usada para autenticar su cuenta de [!DNL Google Cloud Storage] en Platform. |
| `secretAccessKey` | Cadena de 40 caracteres codificada en base 64 que se usa para autenticar la cuenta de [!DNL Google Cloud Storage] en Platform. |
| `bucketName` | Nombre de su cubo de [!DNL Google Cloud Storage]. Debe especificar un nombre de bloque si desea proporcionar acceso a una subcarpeta específica del almacenamiento en la nube. |
| `folderPath` | La ruta a la carpeta a la que desea proporcionar acceso. |

Para obtener más información sobre estos valores, consulte la guía [Claves HMAC de Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview). Para ver los pasos sobre cómo generar tu propio identificador de clave de acceso y clave de acceso secreta, consulta la [[!DNL Google Cloud Storage] descripción general](../../../../connectors/cloud-storage/google-cloud-storage.md).

### Uso de API de Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía sobre [introducción a las API de Platform](../../../../../landing/api-guide.md).

## Crear una conexión base

Una conexión base retiene información entre el origen y Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el ID único de conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un identificador de conexión base, realice una solicitud de POST al extremo `/connections` y proporcione las credenciales de autenticación [!DNL Google Cloud Storage] como parte de los parámetros de solicitud.

>[!TIP]
>
>Durante este paso, también puede designar las subcarpetas a las que tendrá acceso su cuenta definiendo el nombre del contenedor y la ruta a la subcarpeta.

**Formato de API**

```http
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para [!DNL Google Cloud Storage]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Google Cloud Storage connection",
      "description": "Connector for Google Cloud Storage",
      "auth": {
          "specName": "Basic Authentication for google-cloud",
          "params": {
              "accessKeyId": "accessKeyId",
              "secretAccessKey": "secretAccessKey",
              "bucketName": "acme-google-cloud-bucket",
              "folderPath": "/acme/customers/sales"
          }
      },
      "connectionSpec": {
          "id": "32e8f412-cdf7-464c-9885-78184cb113fd",
          "version": "1.0"
      }
  }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `auth.params.accessKeyId` | Identificador de clave de acceso asociado con su cuenta de [!DNL Google Cloud Storage]. |
| `auth.params.secretAccessKey` | La clave secreta de acceso asociada a su cuenta de [!DNL Google Cloud Storage]. |
| `auth.params.bucketName` | Nombre de su cubo de [!DNL Google Cloud Storage]. Debe especificar un nombre de bloque si desea proporcionar acceso a una subcarpeta específica del almacenamiento en la nube. |
| `auth.params.folderPath` | La ruta a la carpeta a la que desea proporcionar acceso. |
| `connectionSpec.id` | Id. de especificación de conexión [!DNL Google Cloud Storage]: `32e8f412-cdf7-464c-9885-78184cb113fd` |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar los datos de almacenamiento en la nube en el siguiente tutorial.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión de [!DNL Google Cloud Storage] mediante API y se ha obtenido un ID único como parte del cuerpo de respuesta. Puede usar este identificador de conexión para [explorar los almacenes en la nube mediante la API de Flow Service](../../explore/cloud-storage.md).
