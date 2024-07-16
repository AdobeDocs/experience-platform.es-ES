---
title: Creación de una conexión base de Google Ads mediante la API de Flow Service
description: Obtenga información sobre cómo conectar Adobe Experience Platform a Google Ads mediante la API de Flow Service.
exl-id: 4658e392-1bd9-4e74-aa05-96109f9b62a0
source-git-commit: ce3dabe4ab08a41e581b97b74b3abad352e3267c
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 3%

---

# Crear una conexión base de Google Ads usando la API [!DNL Flow Service]

>[!WARNING]
>
>El origen [!DNL Google Ads] no está disponible temporalmente. El Adobe está trabajando para resolver los problemas con esta fuente.

>[!NOTE]
>
>La fuente de Google Ads está en versión beta. Consulte [Resumen de fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre cómo usar fuentes etiquetadas como beta.

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Este tutorial lo guiará para crear una conexión base para Google Ads mediante la [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Primeros pasos

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): el Experience Platform permite la ingesta de datos de varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Experience Platform.
* [Zonas protegidas](../../../../../sandboxes/home.md): El Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Experience Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que necesitará conocer para conectarse correctamente a Google Ads mediante la API [!DNL Flow Service].

### Recopilar credenciales necesarias

Para que [!DNL Flow Service] se conecte con Google Ads, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `clientCustomerId` | El ID de cliente es el número de cuenta que corresponde a la cuenta de cliente de Google Ads que desea administrar con la API de Google Ads. Este identificador sigue la plantilla de `123-456-7890`. |
| `loginCustomerId` | El ID de cliente de inicio de sesión es el número de cuenta que corresponde a su cuenta de administrador de Google Ads y se utiliza para recuperar datos de informe de un cliente operativo específico. Para obtener más información sobre el identificador de cliente de inicio de sesión, lea la [Documentación de la API de Google Ads](https://developers.google.com/search-ads/reporting/concepts/login-customer-id). |
| `developerToken` | El token de desarrollador le permite acceder a la API de Google Ads. Puede utilizar el mismo token de desarrollador para realizar solicitudes en todas las cuentas de Google Ads. Recupere su token de desarrollador al [iniciar sesión en su cuenta de administrador](https://ads.google.com/home/tools/manager-accounts/) y luego navegar a la página [!DNL API Center]. |
| `refreshToken` | El token de actualización forma parte de la autenticación [!DNL OAuth2]. Este token le permite volver a generar los tokens de acceso una vez caducados. |
| `clientId` | El ID de cliente se usa junto con el secreto de cliente como parte de la autenticación [!DNL OAuth2]. En conjunto, el ID de cliente y el secreto de cliente permiten que la aplicación funcione en nombre de la cuenta al identificar la aplicación en Google. |
| `clientSecret` | El secreto de cliente se usa junto con el ID de cliente como parte de la autenticación [!DNL OAuth2]. En conjunto, el ID de cliente y el secreto de cliente permiten que la aplicación funcione en nombre de la cuenta al identificar la aplicación en Google. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. El identificador de especificación de conexión para Google Ads es: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

Lea el documento de información general de la API para [obtener más información sobre cómo empezar a usar Google Ads](https://developers.google.com/google-ads/api/docs/first-call/overview).

### Uso de API de Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía sobre [introducción a las API de Platform](../../../../../landing/api-guide.md).

## Crear una conexión base

Una conexión base retiene información entre el origen y Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el ID único de conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un identificador de conexión base, realice una solicitud de POST al extremo `/connections` y proporcione las credenciales de autenticación de Google Ads como parte de los parámetros de solicitud.

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
              "authenticationType": "{AUTHENTICATION_TYPE}"
              "clientId": "{CLIENT_ID}",
              "clientSecret": "{CLIENT_SECRET}",
              "refreshToken": "{REFRESH_TOKEN}"
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
| `auth.params.clientCustomerID` | El ID de cliente de su cuenta de Google Ads. |
| `auth.params.loginCustomerID` | El ID de cliente de inicio de sesión que corresponde a su cuenta de administrador de Google Ads. |
| `auth.params.developerToken` | El token de desarrollador de su cuenta de Google Ads. |
| `auth.params.refreshToken` | El token de actualización de su cuenta de Google Ads. |
| `auth.params.clientID` | El ID de cliente de su cuenta de Google Ads. |
| `auth.params.clientSecret` | Secreto de cliente de su cuenta de Google Ads. |
| `connectionSpec.id` | Id. de especificación de conexión de Google Ads: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión base recién creada, incluido su identificador único (`id`). Este ID es necesario en el siguiente paso para crear una conexión de origen.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión base de Google Ads utilizando la API [!DNL Flow Service]. Puede utilizar este ID de conexión base en los siguientes tutoriales:

* [Explore la estructura y el contenido de las tablas de datos mediante la API  [!DNL Flow Service] B](../../explore/tabular.md)
* [Cree un flujo de datos para llevar los datos de publicidad a Platform mediante la API  [!DNL Flow Service] B](../../collect/advertising.md)
