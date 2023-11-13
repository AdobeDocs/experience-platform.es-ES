---
keywords: Experience Platform;inicio;temas populares;REST genérico;REST genérico
solution: Experience Platform
title: Creación de una conexión base de API de REST genérica mediante la API de Flow Service
type: Tutorial
description: Aprenda a conectar la API genérica de REST a Adobe Experience Platform mediante la API de Flow Service.
exl-id: 6b414868-503e-49d5-8f4a-5b2fc003dab0
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '945'
ht-degree: 3%

---

# Cree una conexión base de API REST genérica utilizando [!DNL Flow Service] API

>[!NOTE]
>
>El [!DNL Generic REST API] el origen está en versión beta. Consulte la [Resumen de orígenes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores etiquetados como beta.

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Este tutorial lo acompañará durante los pasos para crear una conexión base para [!DNL Generic REST API] uso del [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos desde varias fuentes y, al mismo tiempo, le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Zonas protegidas](../../../../../sandboxes/home.md): El Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../../../landing/api-guide.md).

### Recopilar credenciales necesarias

Para que [!DNL Flow Service] para conectar con [!DNL Generic REST API], debe proporcionar credenciales válidas para el tipo de autenticación que elija. [!DNL Generic REST API] admite código de actualización OAuth 2 y autenticación básica. Consulte las siguientes tablas para obtener información sobre las credenciales de los dos tipos de autenticación admitidos.

#### Código de actualización de OAuth 2

| Credencial | Descripción |
| --- | --- |
| `host` | La URL de host de la fuente a la que realiza la solicitud. Este valor es obligatorio y no se puede omitir usando `requestParameterOverride`. |
| `authorizationTestUrl` | (Opcional) La dirección URL de prueba de autorización se utiliza para validar credenciales al crear una conexión base. Si no se proporcionan, las credenciales se comprueban automáticamente durante el paso de creación de la conexión de origen. |
| `clientId` | (Opcional) El ID de cliente asociado con su cuenta de usuario. |
| `clientSecret` | (Opcional) Secreto de cliente asociado a su cuenta de usuario. |
| `accessToken` | Credencial de autenticación principal utilizada para acceder a la aplicación. El token de acceso representa la autorización de la aplicación para acceder a determinados aspectos de los datos de un usuario. Este valor es obligatorio y no se puede omitir usando `requestParameterOverride`. |
| `refreshToken` | (Opcional) Un token que se usa para generar un nuevo token de acceso cuando el token de acceso ha caducado. |
| `expirationDate` | (Opcional) Un valor oculto que define la fecha de caducidad del token de acceso. |
| `accessTokenUrl` | (Opcional) Punto final de URL utilizado para recuperar el token de acceso. |
| `requestParameterOverride` | (Opcional) Una propiedad que le permite especificar qué parámetros de credencial se van a anular. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. Identificador de especificación de conexión para [!DNL Generic REST API] es: `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |

#### Autenticación básica

| Credencial | Descripción |
| --- | --- |
| `host` | La URL de host de la fuente a la que realiza la solicitud. |
| `username` | El nombre de usuario que corresponde con su cuenta de usuario. |
| `password` | La contraseña que corresponde a su cuenta de usuario. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. Identificador de especificación de conexión para [!DNL Generic REST API] es: `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |

## Cree una conexión base

Una conexión base retiene información entre el origen y Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el ID único de conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

[!DNL Generic REST API] admite autenticación básica y código de actualización de OAuth 2. Consulte los siguientes ejemplos para obtener instrucciones sobre cómo autenticarse con cualquiera de los tipos de autenticación.

### Crear un [!DNL Generic REST API] conexión base mediante el código de actualización de OAuth 2

Para crear un ID de conexión base con el código de actualización de OAuth 2, realice una solicitud de POST al `/connections` al proporcionar sus credenciales de OAuth 2.

**Formato de API**

```http
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para [!DNL Generic REST API]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Generic REST API base connection with OAuth 2 refresh code",
      "description": "Generic REST API base connection with OAuth 2 refresh code",
      "connectionSpec": {
          "id": "4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62",
          "version": "1.0"
      },
      "auth": {
          "specName": "oAuth2RefreshCode",
          "params": {
              "host": "{HOST}",
              "accessToken": "{ACCESS_TOKEN}"
          }
      }
  }'
```

| Propiedad | Descripción |
| --------- | ----------- |
| `name` | Nombre de la conexión base. Asegúrese de que el nombre de la conexión base sea descriptivo, ya que puede utilizarlo para buscar información sobre la conexión base. |
| `description` | (Opcional) Una propiedad que puede incluir para proporcionar más información sobre la conexión base. |
| `connectionSpec.id` | Identificador de especificación de conexión asociado con [!DNL Generic REST API]. Este ID fijo es: `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |
| `auth.specName` | El tipo de autenticación que utiliza para autenticar el origen en Platform. |
| `auth.params.host` | La URL raíz utilizada para conectarse a su [!DNL Generic REST API] origen. |
| `auth.params.accessToken` | El token de acceso correspondiente utilizado para autenticar el origen. Esto es necesario para la autenticación basada en OAuth. |

**Respuesta**

Una respuesta correcta devuelve la conexión recién creada, incluido su identificador de conexión único (`id`). Este ID es necesario para explorar los datos en el siguiente tutorial.

```json
{
  "id": "a5c6b647-e784-4b58-86b6-47e784ab580b",
  "etag": "\"7b01056a-0000-0200-0000-5e8a4f5b0000\""
}
```

### Crear un [!DNL Generic REST API] conexión base mediante autenticación básica

Para crear un [!DNL Generic REST API] conexión base mediante autenticación básica, realice una solicitud de POST al `/connections` punto final de [!DNL Flow Service] API mientras proporciona sus credenciales de autenticación básicas.

**Formato de API**

```https
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para [!DNL Generic REST API]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "Generic REST API base connection with basic authentication",
      "description": "Generic REST API base connection with basic authentication",
      "connectionSpec": {
          "id": "4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62",
          "version": "1.0"
      },
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "host": "{HOST}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      }
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `name` | Nombre de la conexión base. Asegúrese de que el nombre de la conexión base sea descriptivo, ya que puede utilizarlo para buscar información sobre la conexión base. |
| `description` | (Opcional) Una propiedad que puede incluir para proporcionar más información sobre la conexión base. |
| `connectionSpec.id` | Identificador de especificación de conexión asociado con [!DNL Generic REST API]. Este ID fijo es: `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |
| `auth.specName` | El tipo de autenticación que utiliza para conectar el origen a Platform. |
| `auth.params.host` | La URL raíz utilizada para conectarse a su [!DNL Generic REST API] origen. |
| `auth.params.username` | El nombre de usuario que corresponde con su [!DNL Generic REST API] origen. Esto es necesario para la autenticación básica. |
| `auth.params.password` | La contraseña que corresponde con su [!DNL Generic REST API] origen. Esto es necesario para la autenticación básica. |

**Respuesta**

Una respuesta correcta devuelve la conexión base recién creada, incluido su identificador de conexión único (`id`). Este ID es necesario para explorar la estructura de archivos y el contenido de origen en el siguiente paso.

```json
{
    "id": "9601747c-6874-4c02-bb00-5732a8c43086",
    "etag": "\"3702dabc-0000-0200-0000-615b5b5a0000\""
}
```

## Pasos siguientes

Al seguir este tutorial, ha creado un [!DNL Generic REST API] conexión base mediante el [!DNL Flow Service] API. Puede utilizar este ID de conexión base en los siguientes tutoriales:

* [Explorar la estructura y el contenido de las tablas de datos mediante [!DNL Flow Service] API](../../explore/tabular.md)
* [Cree un flujo de datos para llevar los datos de los protocolos a Platform mediante [!DNL Flow Service] API](../../collect/protocols.md)
