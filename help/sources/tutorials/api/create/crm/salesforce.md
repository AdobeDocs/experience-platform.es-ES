---
title: Conectar Salesforce A Experience Platform Mediante La API De Flow Service
description: Obtenga información sobre cómo conectar Adobe Experience Platform a una cuenta de Salesforce mediante la API de Flow Service.
exl-id: 43dd9ee5-4b87-4c8a-ac76-01b83c1226f6
source-git-commit: 01f655df8679383f57d60796be5274acd9b5df68
workflow-type: tm+mt
source-wordcount: '1077'
ht-degree: 3%

---

# Conectar [!DNL Salesforce] al Experience Platform mediante la API [!DNL Flow Service]

Lea esta guía para saber cómo conectar su cuenta de origen de [!DNL Salesforce] a Adobe Experience Platform mediante la [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Introducción 

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): [!DNL Experience Platform] permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de [!DNL Platform].
* [Zonas protegidas](../../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola instancia de [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

### Uso de API de Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía sobre [introducción a las API de Platform](../../../../../landing/api-guide.md).

## Conectar [!DNL Salesforce] al Experience Platform en [!DNL Azure] {#azure}

Lea los pasos siguientes para obtener información sobre cómo conectar su origen de [!DNL Salesforce] al Experience Platform en [!DNL Azure].

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

### Crear una conexión base para [!DNL Salesforce] en el Experience Platform de [!DNL Azure]

Una conexión base retiene información entre el origen y Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el ID único de conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear una conexión base y conectar su cuenta de [!DNL Salesforce] al Experience Platform en [!DNL Azure], realice una solicitud de POST al extremo de `/connections` y proporcione las credenciales de autenticación de [!DNL Salesforce] en el cuerpo de la solicitud.

**Formato de API**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB Autenticación básica]

+++Solicitud

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

+++

+++Respuesta

Una respuesta correcta devuelve la conexión base recién creada junto con su ID único.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

+++

>[!TAB Credencial de cliente de OAuth 2]

+++Solicitud

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

+++


+++Respuesta

Una respuesta correcta devuelve la conexión base recién creada junto con su ID único.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

+++

>[!ENDTABS]

## Conectar [!DNL Salesforce] al Experience Platform en Amazon Web Service (AWS) {#aws}

>[!AVAILABILITY]
>
>Esta sección se aplica a las implementaciones de Experience Platform que se ejecutan en Amazon Web Service (AWS). Un Experience Platform que se ejecuta en AWS está disponible actualmente para un número limitado de clientes. Para obtener más información acerca de la infraestructura de Experience Platform compatible, consulte la [descripción general de la nube múltiple de Experience Platform](../../../../../landing/multi-cloud.md).

Lea los pasos siguientes para obtener información sobre cómo conectar su origen de [!DNL Salesforce] al Experience Platform en AWS.

### Requisitos previos

Para obtener información sobre cómo configurar tu cuenta de [!DNL Salesforce] para poder conectarte a Experience Platform en AWS, lee la [[!DNL Salesforce] descripción general](../../../../connectors/crm/salesforce.md#aws).

### Crear una conexión base para [!DNL Salesforce] en el Experience Platform en AWS

Para crear una conexión base y conectar su cuenta de [!DNL Salesforce] a Experience Platform en AWS, realice una solicitud de POST al extremo de `/connections` y proporcione los valores apropiados para sus credenciales.

**Formato de API**

```http
POST /connections
```

**Solicitud**

+++Seleccionar para ver la solicitud

La siguiente solicitud crea una conexión base para el origen [!DNL Salesforce] en Experience Platform en AWS.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ACME Salesforce account on AWS",
      "description": "ACME Salesforce account on AWS",
      "auth": {
          "specName": "OAuth2 JWT Token Credential",
          "params":
            "jwtToken": "{JWT_TOKEN},
            "clientId": "xxxx",
            "clientSecret": "xxxx",
            "instanceUrl": "https://acme-enterprise-3126.my.salesforce.com"
        }
      },
      "connectionSpec": {
          "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
          "version": "1.0"
      }
  }'
```

Para obtener información sobre cómo recuperar su [!DNL Salesforce] `jwtToken`, lea la guía sobre [cómo configurar un origen de  [!DNL Salesforce] para conectarse al Experience Platform en AWS](../../../../connectors/crm/salesforce.md#aws).

+++

**Respuesta**

+++Seleccionar para ver la respuesta

Una respuesta correcta devuelve la conexión base recién creada junto con su ID único.

```json
{
    "id": "3e908d3f-c390-482b-9f44-43d3d4f2eb82",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

+++

### Compruebe el estado de la conexión

Para comprobar el estado de la conexión, realice una solicitud de GET al extremo `/connections` y proporcione el identificador de conexión base que se generó en el paso de creación.

**Formato de API**

```http
GET /connections
```

**Solicitud**

+++Seleccionar para ver la solicitud

La siguiente solicitud recupera información para el id. de conexión base: `3e908d3f-c390-482b-9f44-43d3d4f2eb82`.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/3e908d3f-c390-482b-9f44-43d3d4f2eb82' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
```

+++

**Respuesta**

>[!BEGINTABS]

>[!TAB Inicializando]

+++Seleccione para ver el ejemplo de respuesta

La siguiente respuesta muestra información para el id. de conexión base: `3e908d3f-c390-482b-9f44-43d3d4f2eb82` mientras se encuentra en el estado `initializing`.

```json
{
  "items": [
    {
      "id": "3e908d3f-c390-482b-9f44-43d3d4f2eb82",
      "createdAt": 1736506325115,
      "updatedAt": 1736506325717,
      "createdBy": "acme@techacct.adobe.com",
      "updatedBy": "acme@techacct.adobe.com",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_ID}",
      "name": "JWT Token Auth Authentication E2E-1736506322",
      "description": "Base Connection for salesforce E2E",
      "connectionSpec": {
        "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
        "version": "1.0"
      },
      "state": "initializing",
      "auth": {
        "specName": "OAuth2 JWT Token Credential",
        "params": {
          "jwtToken": "{JWT_TOKEN}",
          "clientId": "{CLIENT_ID}",
          "clientSecret": "{CLIENT_SECRET}",
          "instanceUrl": "https://acme-enterprise-3126.my.salesforce.com"
        }
      }
    }
  }
]
```

+++

>[!TAB Habilitado]

+++Seleccione para ver el ejemplo de respuesta

La siguiente respuesta muestra información para el id. de conexión base: `3e908d3f-c390-482b-9f44-43d3d4f2eb82` mientras se encuentra en el estado `enabled`.

```json
{
  "items": [
      {
        "id": "3e908d3f-c390-482b-9f44-43d3d4f2eb82",
        "createdAt": 1736506325115,
        "updatedAt": 1736506413299,
        "createdBy": "acme@techacct.adobe.com",
        "updatedBy": "acme@AdobeID",
        "createdClient": "{CREATED_CLIENT}",
        "updatedClient": "acme",
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "imsOrgId": "{ORG_ID}",
        "name": "JWT Token Auth Authentication E2E-1736506322",
        "description": "Base Connection for salesforce E2E",
        "connectionSpec": {
          "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
          "version": "1.0"
        },
        "state": "enabled",
        "auth": {
          "specName": "OAuth2 JWT Token Credential",
          "params": {
            "jwtToken": "{JWT_TOKEN}",
            "clientId": "{CLIENT_ID}",
            "clientSecret": "{CLIENT_SECRET}",
            "instanceUrl": "https://adb8-dev-ed.develop.my.salesforce.com",
            "orgId": "00DdL000001iPRxUAM"
          }
        },
        "version": "\"6d27f305-40be-41c3-97d4-a701827c34df\"",
        "etag": "\"6d27f305-40be-41c3-97d4-a701827c34df\""
    }
  ]
}
```

+++

>[!ENDTABS]

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión base [!DNL Salesforce] mediante la API [!DNL Flow Service]. Puede utilizar este ID de conexión base en los siguientes tutoriales:

* [Explore la estructura y el contenido de las tablas de datos mediante la API  [!DNL Flow Service] B](../../explore/tabular.md)
* [Cree un flujo de datos para llevar datos de CRM a Platform mediante la API  [!DNL Flow Service] ](../../collect/crm.md)
