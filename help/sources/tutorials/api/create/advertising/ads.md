---
title: Conexión de Google Ads a Experience Platform mediante API
description: Obtenga información sobre cómo conectar Adobe Experience Platform a Google Ads mediante la API de Flow Service.
exl-id: 4658e392-1bd9-4e74-aa05-96109f9b62a0
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 1%

---

# Conectar [!DNL Google Ads] a Experience Platform mediante la API [!DNL Flow Service]

>[!NOTE]
>
>El origen [!DNL Google Ads] está en la versión beta. Consulte [Resumen de fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre cómo usar fuentes etiquetadas como beta.

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Lea este tutorial para aprender a conectar su cuenta de [!DNL Google Ads] a Adobe Experience Platform mediante la [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Experience Platform.
* [Zonas protegidas](../../../../../sandboxes/home.md): Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Experience Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que necesitará conocer para conectarse correctamente a [!DNL Google Ads] mediante la API [!DNL Flow Service].

### Uso de API de Experience Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Experience Platform, consulte la guía sobre [introducción a las API de Experience Platform](../../../../../landing/api-guide.md).

### Recopilar credenciales necesarias

Para obtener información sobre la autenticación, lea la [[!DNL Google Ads] descripción general del origen](../../../../connectors/advertising/ads.md).

## Crear una conexión base

Una conexión base retiene información entre el origen y Experience Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el identificador único de la conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un identificador de conexión base, realice una petición POST al extremo `/connections` y proporcione las credenciales de autenticación de Google Ads como parte de los parámetros de la solicitud.

**Formato de API**

```https
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para Google Ads:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "name": "Google Ads base connection",
      "description": "Google Ads base connection",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "clientCustomerID": "{CLIENT_CUSTOMER_ID}",
              "loginCustomerID": "{LOGIN_CUSTOMER_ID}",
              "developerToken": "{DEVELOPER_TOKEN}",
              "refreshToken": "{REFRESH_TOKEN}",
              "clientId": "{CLIENT_ID}",
              "clientSecret": "{CLIENT_SECRET}",
              "googleAdsApiVersion": "v17"

          }
      },
      "connectionSpec": {
          "id": "d771e9c1-4f26-40dc-8617-ce58c4b53702",
          "version": "1.0"
      }
  }'
```

| Propiedad | Descripción |
| --------- | ----------- |
| `auth.params.clientCustomerID` | Identificador de cliente de su cuenta de [!DNL Google Ads]. |
| `auth.params.loginCustomerID` | Identificador de cliente de inicio de sesión que corresponde con su cuenta de administrador [!DNL Google Ads]. |
| `auth.params.developerToken` | El token de desarrollador de su cuenta de [!DNL Google Ads]. |
| `auth.params.refreshToken` | El token de actualización de su cuenta de [!DNL Google Ads]. |
| `auth.params.clientID` | Identificador de cliente de su cuenta de [!DNL Google Ads]. |
| `auth.params.clientSecret` | Secreto de cliente de su cuenta de [!DNL Google Ads]. |
| `auth.params.googleAdsApiVersion` | Versión de la API [!DNL Google Ads] que está utilizando. La última versión compatible en Experience Platform es `v17`. |
| `connectionSpec.id` | Identificador de especificación de conexión [!DNL Google Ads]: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión base recién creada, incluido su identificador único (`id`). Este ID es necesario en el siguiente paso para crear una conexión de origen.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Creación de un flujo de datos para introducir datos publicitarios

Siguiendo este tutorial, ha creado una conexión base [!DNL Google Ads] mediante la API [!DNL Flow Service] y ha conectado su cuenta de [!DNL Google Ads] a Experience Platform. Puede utilizar este ID de conexión base en los siguientes tutoriales:

* [Explore la estructura y el contenido de las tablas de datos mediante la API  [!DNL Flow Service] B](../../explore/tabular.md)
* [Cree un flujo de datos para llevar los datos de publicidad a Experience Platform mediante la API  [!DNL Flow Service] ](../../collect/advertising.md)
