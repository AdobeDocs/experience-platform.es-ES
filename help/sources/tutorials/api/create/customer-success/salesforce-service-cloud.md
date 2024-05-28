---
title: Creación de una conexión de origen de Salesforce Cloud mediante la API de Flow Service
description: Obtenga información sobre cómo conectar Adobe Experience Platform a Salesforce Service Cloud mediante la API de Flow Service.
exl-id: ed133bca-8e88-4c85-ae52-c3269b6bf3c9
source-git-commit: 7930a869627130a5db34780e64b809cda0c1e5f4
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 3%

---

# Crear un [!DNL Salesforce Service Cloud] conexión de origen mediante [!DNL Flow Service] API

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Lea este tutorial para aprender a crear una conexión base para [!DNL Salesforce Service Cloud] uso del [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): el Experience Platform permite la ingesta de datos desde varias fuentes y, al mismo tiempo, le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Zonas protegidas](../../../../../sandboxes/home.md): el Experience Platform proporciona entornos limitados virtuales que dividen un solo [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente a [!DNL Salesforce Service Cloud] uso del [!DNL Flow Service] API.

### Recopilar credenciales necesarias

El [!DNL Salesforce Service Cloud] El origen de admite la autenticación básica y la credencial de cliente de OAuth2.

>[!BEGINTABS]

>[!TAB Autenticación básica]

Para conectar su [!DNL Salesforce Service Cloud] cuenta a [!DNL Flow Service] con la autenticación básica, proporcione valores para las siguientes credenciales:

| Credencial | Descripción |
| --- | --- |
| `environmentUrl` | La dirección URL del [!DNL Salesforce Service Cloud] instancia de origen. |
| `username` | El nombre de usuario de [!DNL Salesforce Service Cloud] cuenta de usuario. |
| `password` | La contraseña para el [!DNL Salesforce Service Cloud] cuenta de usuario. |
| `securityToken` | El token de seguridad para [!DNL Salesforce Service Cloud] cuenta de usuario. |
| `apiVersion` | (Opcional) La versión de la API de REST de [!DNL Salesforce Service Cloud] instancia de que está utilizando. El valor de la versión de la API debe tener formato decimal. Por ejemplo, si utiliza la versión de API `52`, entonces debe introducir el valor como `52.0`. Si este campo se deja en blanco, el Experience Platform utilizará automáticamente la última versión disponible. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. Identificador de especificación de conexión para [!DNL Salesforce Service Cloud] es: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Para obtener más información sobre cómo empezar, visite [este documento de Salesforce](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm).

>[!TAB Credencial de cliente de OAuth 2]

Para conectar su [!DNL Salesforce Service Cloud] cuenta a [!DNL Flow Service] Con la credencial de cliente de OAuth 2, proporcione valores para las siguientes credenciales:

| Credencial | Descripción |
| --- | --- |
| `environmentUrl` | La dirección URL del [!DNL Salesforce Service Cloud] instancia de origen. |
| `clientId` | El ID de cliente se utiliza junto con el secreto de cliente como parte de la autenticación OAuth2. Juntos, el ID de cliente y el secreto de cliente permiten que su aplicación funcione en nombre de su cuenta al identificar su aplicación para [!DNL Salesforce Service Cloud]. |
| `clientSecret` | El secreto de cliente se utiliza junto con el ID de cliente como parte de la autenticación OAuth2. Juntos, el ID de cliente y el secreto de cliente permiten que su aplicación funcione en nombre de su cuenta al identificar su aplicación para [!DNL Salesforce Service Cloud]. |
| `apiVersion` | La versión de la API de REST de [!DNL Salesforce Service Cloud] instancia de que está utilizando. El valor de la versión de la API debe tener formato decimal. Por ejemplo, si utiliza la versión de API `52`, entonces debe introducir el valor como `52.0`. Si este campo se deja en blanco, el Experience Platform utilizará automáticamente la última versión disponible. Este valor es obligatorio para la autenticación de credenciales de cliente de OAuth2. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. Identificador de especificación de conexión para [!DNL Salesforce Service Cloud] es: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Para obtener más información sobre el uso de OAuth para [!DNL Salesforce Service Cloud], lea la [[!DNL Salesforce Service Cloud] Guía de flujos de autorización de OAuth](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&amp;type=5).

>[!ENDTABS]

### Uso de API de Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../../../landing/api-guide.md).

## Crear una conexión base

Una conexión base retiene información entre el origen y Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el ID único de conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un ID de conexión base, realice una solicitud de POST al `/connections` extremo al proporcionar su [!DNL Salesforce Service Cloud] credenciales de autenticación como parte de los parámetros de solicitud.

**Formato de API**

```http
POST /connections
```

**Solicitud**

>[!BEGINTABS]

>[!TAB Autenticación básica]

La siguiente solicitud crea una conexión base para [!DNL Salesforce Service Cloud] uso de la autenticación básica:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Salesforce Service Cloud account for ACME data (basic auth)",
      "description": "Salesforce Service Cloud account for ACME data (basic auth)",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
            "environmentUrl": "https://acme-enterprise-3126.my.salesforce.com",
            "username": "acme-salesforce-service-cloud",
            "password": "xxxx",
            "securityToken": "xxxx"
        }
      },
      "connectionSpec": {
          "id": "cb66ab34-8619-49cb-96d1-39b37ede86ea",
          "version": "1.0"
      }
  }'
```

| Parámetro | Descripción |
| ---| --- |
| `auth.params.environmentUrl` | La URL de su [!DNL Salesforce Service Cloud] ejemplo. |
| `auth.params.username` | El nombre de usuario asociado con su [!DNL Salesforce Service Cloud] cuenta. |
| `auth.params.password` | La contraseña asociada a su [!DNL Salesforce Service Cloud] cuenta. |
| `auth.params.securityToken` | El token de seguridad asociado con su [!DNL Salesforce Service Cloud] cuenta. |
| `connectionSpec.id` | El [!DNL Salesforce Service Cloud] identificador de especificación de conexión: `cb66ab34-8619-49cb-96d1-39b37ede86ea` |

>[!TAB Credencial de cliente de OAuth2]

La siguiente solicitud crea una conexión base para [!DNL Salesforce Service Cloud] usar la credencial de cliente de OAuth 2:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Salesforce Service Cloud account for ACME data (OAuth2)",
      "description": "Salesforce Service Cloud account for ACME data (OAuth2)",
      "auth": {
          "specName": "OAuth2 Client Credential",
          "params":
            "environmentUrl": "https://acme-enterprise-3126.my.salesforce.com",
            "clientId": "xxxx",
            "clientSecret": "xxxx",
            "apiVersion": "60.0"
        }
      },
      "connectionSpec": {
          "id": "cb66ab34-8619-49cb-96d1-39b37ede86ea",
          "version": "1.0"
      }
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `auth.params.environmentUrl` | La URL de su [!DNL Salesforce Service Cloud] ejemplo. |
| `auth.params.clientId` | El ID de cliente asociado con su [!DNL Salesforce Service Cloud] cuenta. |
| `auth.params.clientSecret` | El secreto de cliente asociado con su [!DNL Salesforce Service Cloud] cuenta. |
| `auth.params.apiVersion` | La versión de la API de REST de [!DNL Salesforce Service Cloud] instancia de que está utilizando. |
| `connectionSpec.id` | El [!DNL Salesforce Service Cloud] identificador de especificación de conexión: `cb66ab34-8619-49cb-96d1-39b37ede86ea`. |

>[!ENDTABS]

**Respuesta**

Una respuesta correcta devuelve la conexión base recién creada junto con su ID único.

```json
{
    "id": "4267c2ab-2104-474f-a7c2-ab2104d74f86",
    "etag": "\"0200f1c5-0000-0200-0000-5e4352bf0000\""
}
```

## Pasos siguientes

Al seguir este tutorial, ha creado un [!DNL Salesforce Service Cloud] conexión base mediante el [!DNL Flow Service] API. Puede utilizar este ID de conexión base en los siguientes tutoriales:

* [Explorar la estructura y el contenido de las tablas de datos mediante [!DNL Flow Service] API](../../explore/tabular.md)
* [Cree un flujo de datos para llevar los datos de éxito de los clientes a Platform mediante [!DNL Flow Service] API](../../collect/customer-success.md)
