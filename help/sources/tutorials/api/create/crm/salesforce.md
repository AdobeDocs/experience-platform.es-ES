---
title: Creación de una conexión base de Salesforce mediante la API de Flow Service
description: Aprenda a conectar Adobe Experience Platform a una cuenta de Salesforce mediante la API de Flow Service.
exl-id: 43dd9ee5-4b87-4c8a-ac76-01b83c1226f6
source-git-commit: 5951b0f549c2fd2723945f8f4089d12f73b92e6c
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 3%

---

# Crear una conexión base [!DNL Salesforce] mediante la API [!DNL Flow Service]

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Este tutorial lo guiará para crear una conexión base para [!DNL Salesforce] mediante la [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): [!DNL Experience Platform] permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de [!DNL Platform].
* [Zonas protegidas](../../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola instancia de [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que necesitará conocer para conectar correctamente [!DNL Platform] a una cuenta de [!DNL Salesforce] mediante la API de [!DNL Flow Service].

### Recopilar credenciales necesarias

El origen [!DNL Salesforce] admite la autenticación básica y la credencial de cliente OAuth2.

>[!BEGINTABS]

>[!TAB Autenticación básica]

Para conectar su cuenta de [!DNL Salesforce] a [!DNL Flow Service] mediante autenticación básica, proporcione valores para las siguientes credenciales:

| Credencial | Descripción |
| --- | --- |
| `environmentUrl` | Dirección URL de la instancia de origen [!DNL Salesforce]. El formato de `environmentUrl` es `https://[domain].my.salesforce.com`. |
| `username` | Nombre de usuario para la cuenta de usuario [!DNL Salesforce]. |
| `password` | Contraseña de la cuenta de usuario [!DNL Salesforce]. |
| `securityToken` | Token de seguridad para la cuenta de usuario [!DNL Salesforce]. |
| `apiVersion` | (Opcional) La versión de la API de REST de la instancia [!DNL Salesforce] que está utilizando. El valor de la versión de la API debe tener formato decimal. Por ejemplo, si está usando la versión de API `52`, debe introducir el valor como `52.0`. Si este campo se deja en blanco, el Experience Platform utilizará automáticamente la última versión disponible. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. El id. de especificación de conexión para [!DNL Salesforce] es: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Para obtener más información sobre cómo empezar, visite [este documento de Salesforce](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm).

>[!TAB Credencial de cliente de OAuth 2]

Para conectar su cuenta de [!DNL Salesforce] a [!DNL Flow Service] mediante la credencial de cliente de OAuth 2, proporcione valores para las siguientes credenciales:

| Credencial | Descripción |
| --- | --- |
| `environmentUrl` | Dirección URL de la instancia de origen [!DNL Salesforce]. El formato de `environmentUrl` es `https://[domain].my.salesforce.com` |
| `clientId` | El ID de cliente se utiliza junto con el secreto de cliente como parte de la autenticación OAuth2. Juntos, el ID de cliente y el secreto de cliente permiten que su aplicación funcione en nombre de su cuenta al identificar su aplicación en [!DNL Salesforce]. |
| `clientSecret` | El secreto de cliente se utiliza junto con el ID de cliente como parte de la autenticación OAuth2. Juntos, el ID de cliente y el secreto de cliente permiten que su aplicación funcione en nombre de su cuenta al identificar su aplicación en [!DNL Salesforce]. |
| `apiVersion` | La versión de la API de REST de la instancia [!DNL Salesforce] que está utilizando. El valor de la versión de la API debe tener formato decimal. Por ejemplo, si está usando la versión de API `52`, debe introducir el valor como `52.0`. Si este campo se deja en blanco, el Experience Platform utilizará automáticamente la última versión disponible. Este valor es obligatorio para la autenticación de credenciales de cliente de OAuth2. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. El id. de especificación de conexión para [!DNL Salesforce] es: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Para obtener más información sobre el uso de OAuth para [!DNL Salesforce], lea la [[!DNL Salesforce] guía sobre flujos de autorización de OAuth](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&amp;type=5).

>[!ENDTABS]

### Uso de API de Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía sobre [introducción a las API de Platform](../../../../../landing/api-guide.md).

## Crear una conexión base

Una conexión base retiene información entre el origen y Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el ID único de conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un identificador de conexión base, realice una solicitud de POST al extremo `/connections` y proporcione las credenciales de autenticación [!DNL Salesforce] en el cuerpo de la solicitud.

**Formato de API**

```http
POST /connections
```

**Solicitud**

>[!BEGINTABS]

>[!TAB Autenticación básica]

La siguiente solicitud crea una conexión base para [!DNL Salesforce] mediante autenticación básica:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ACME Salesforce account",
      "description": "Salesforce account using basic authentication",
      "auth": {
          "specName": "Basic Authentication",
          "params":
            "environmentUrl": "https://acme-enterprise-3126.my.salesforce.com",
            "username": "acme-salesforce",
            "password": "xxxx",
            "securityToken": "xxxx"
        }
      },
      "connectionSpec": {
          "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
          "version": "1.0"
      }
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `auth.params.environmentUrl` | La URL de su instancia [!DNL Salesforce]. |
| `auth.params.username` | El nombre de usuario asociado con su cuenta de [!DNL Salesforce]. |
| `auth.params.password` | La contraseña asociada a su cuenta de [!DNL Salesforce]. |
| `auth.params.securityToken` | El token de seguridad asociado con su cuenta de [!DNL Salesforce]. |
| `connectionSpec.id` | Identificador de especificación de conexión [!DNL Salesforce]: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

>[!TAB Credencial de cliente de OAuth 2]

La siguiente solicitud crea una conexión base para [!DNL Salesforce] mediante la credencial de cliente de OAuth 2:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ACME Salesforce account",
      "description": "Salesforce account using OAuth 2",
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
          "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
          "version": "1.0"
      }
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `auth.params.environmentUrl` | La URL de su instancia [!DNL Salesforce]. |
| `auth.params.clientId` | Identificador de cliente asociado con su cuenta de [!DNL Salesforce]. |
| `auth.params.clientSecret` | El secreto de cliente asociado con su cuenta de [!DNL Salesforce]. |
| `auth.params.apiVersion` | La versión de la API de REST de la instancia [!DNL Salesforce] que está utilizando. |
| `connectionSpec.id` | Identificador de especificación de conexión [!DNL Salesforce]: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

>[!ENDTABS]

**Respuesta**

Una respuesta correcta devuelve la conexión base recién creada junto con su ID único.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión base [!DNL Salesforce] mediante la API [!DNL Flow Service]. Puede utilizar este ID de conexión base en los siguientes tutoriales:

* [Explore la estructura y el contenido de las tablas de datos mediante la API  [!DNL Flow Service] B](../../explore/tabular.md)
* [Cree un flujo de datos para llevar datos de CRM a Platform mediante la API  [!DNL Flow Service] ](../../collect/crm.md)
