---
title: Crear una conexión base de Google Cloud Storage mediante la API de Flow Service
description: Obtenga información sobre cómo conectar Adobe Experience Platform a una cuenta de Google Cloud Storage mediante la API de Flow Service.
exl-id: 321d15eb-82c0-45a7-b257-1096c6db6b18
source-git-commit: 3636b785d82fa2e49f76825650e6159be119f8b4
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 1%

---

# Crear un [!DNL Google Cloud Storage] conexión base mediante el [!DNL Flow Service] API

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Este tutorial lo acompañará durante los pasos para crear una conexión base para [!DNL Google Cloud Storage] uso del [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Primeros pasos

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): [!DNL Experience Platform] permite la ingesta de datos desde varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Zonas protegidas](../../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente a una cuenta de Google Cloud Storage mediante [!DNL Flow Service] API.

### Recopilar credenciales necesarias

Para que [!DNL Flow Service] para conectarse con su [!DNL Google Cloud Storage] En su cuenta de, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `accessKeyId` | Una cadena alfanumérica de 61 caracteres utilizada para autenticar su [!DNL Google Cloud Storage] a Platform. |
| `secretAccessKey` | Una cadena de 40 caracteres codificada en base 64 que se utiliza para autenticar su [!DNL Google Cloud Storage] a Platform. |
| `bucketName` | El nombre de su [!DNL Google Cloud Storage] cubo. Debe especificar un nombre de bloque si desea proporcionar acceso a una subcarpeta específica del almacenamiento en la nube. |
| `folderPath` | La ruta a la carpeta a la que desea proporcionar acceso. |

Para obtener más información sobre estos valores, consulte la [Claves HMAC de Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) guía. Para obtener información sobre cómo generar su propio ID de clave de acceso y clave de acceso secreta, consulte la [[!DNL Google Cloud Storage] descripción general](../../../../connectors/cloud-storage/google-cloud-storage.md).

### Uso de API de Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../../../landing/api-guide.md).

## Crear una conexión base

Una conexión base retiene información entre el origen y Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el ID único de conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un ID de conexión base, realice una solicitud de POST al `/connections` extremo al proporcionar su [!DNL Google Cloud Storage] credenciales de autenticación como parte de los parámetros de solicitud.

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
| `auth.params.accessKeyId` | El ID de clave de acceso asociado con su [!DNL Google Cloud Storage] cuenta. |
| `auth.params.secretAccessKey` | La clave secreta de acceso asociada a su [!DNL Google Cloud Storage] cuenta. |
| `auth.params.bucketName` | El nombre de su [!DNL Google Cloud Storage] cubo. Debe especificar un nombre de bloque si desea proporcionar acceso a una subcarpeta específica del almacenamiento en la nube. |
| `auth.params.folderPath` | La ruta a la carpeta a la que desea proporcionar acceso. |
| `connectionSpec.id` | El [!DNL Google Cloud Storage] identificador de especificación de conexión: `32e8f412-cdf7-464c-9885-78184cb113fd` |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar los datos de almacenamiento en la nube en el siguiente tutorial.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Pasos siguientes

Al seguir este tutorial, ha creado un [!DNL Google Cloud Storage] Se obtuvo una conexión mediante API y un ID único como parte del cuerpo de respuesta. Puede usar este ID de conexión para lo siguiente [explore los almacenes en la nube mediante la API de Flow Service](../../explore/cloud-storage.md).
