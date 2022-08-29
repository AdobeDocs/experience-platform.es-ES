---
keywords: Experience Platform;inicio;temas populares;orígenes;conectores;conectores de origen;sdk de fuentes;sdk;SDK
solution: Experience Platform
title: Crear un flujo de datos para los miembros de Mailchimp mediante la API de servicio de flujo
topic-legacy: tutorial
description: Obtenga información sobre cómo conectar Adobe Experience Platform a miembros de MailChimp mediante la API de servicio de flujo.
exl-id: 900d4073-129c-47ba-b7df-5294d25a7219
source-git-commit: 23a6f8ee23fb67290a5bcba2673a87ce74c9e1d3
workflow-type: tm+mt
source-wordcount: '2123'
ht-degree: 2%

---

# Crear un flujo de datos para [!DNL Mailchimp Members] uso de la API de servicio de flujo

El siguiente tutorial le guía por los pasos para crear una conexión de origen y un flujo de datos para [!DNL Mailchimp Members] datos a Platform mediante [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Requisitos previos

Antes de conectarse [!DNL Mailchimp] a Adobe Experience Platform mediante el código de actualización de OAuth 2, primero debe recuperar el token de acceso para [!DNL MailChimp.] Consulte la [[!DNL Mailchimp] Guía de OAuth 2](https://mailchimp.com/developer/marketing/guides/access-user-data-oauth-2/) para obtener instrucciones detalladas sobre cómo encontrar el token de acceso.

## Creación de una conexión base {#base-connection}

Una vez que haya recuperado su [!DNL Mailchimp] credenciales de autenticación, ahora puede iniciar el proceso de creación de flujo de datos para traer [!DNL Mailchimp Members] a Platform. El primer paso para crear un flujo de datos es crear una conexión base.

Una conexión base retiene información entre la fuente y la plataforma, incluidas las credenciales de autenticación de la fuente, el estado actual de la conexión y el ID de conexión base único. El ID de conexión base le permite explorar y navegar archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

[!DNL Mailchimp] admite autenticación básica y código de actualización de OAuth 2. Consulte los siguientes ejemplos para obtener instrucciones sobre cómo autenticarse con cualquiera de los tipos de autenticación.

### Cree un [!DNL Mailchimp] conexión base con autenticación básica

Para crear un [!DNL Mailchimp] conexión base usando autenticación básica, realice una solicitud de POST al `/connections` punto final de [!DNL Flow Service] API mientras proporciona credenciales para su `authorizationTestUrl`, `username`y `password`.

**Formato de API**

```https
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para [!DNL Mailchimp]:

```shell
curl -X POST \
'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "Mailchimp base connection with basic authentication",
      "description": "Mailchimp Members base connection with basic authentication",
      "connectionSpec": {
          "id": "2e8580db-6489-4726-96de-e33f5f60295f",
          "version": "1.0"
      },
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "authorizationTestUrl": "https://login.mailchimp.com/oauth2/metadata",
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
| `connectionSpec.id` | El ID de especificación de conexión de su origen. Esta ID se puede recuperar después de registrar y aprobar el origen mediante la variable [!DNL Flow Service] API. |
| `auth.specName` | El tipo de autenticación que utiliza para conectar el origen a Platform. |
| `auth.params.authorizationTestUrl` | (Opcional) La URL de prueba de autorización se utiliza para validar las credenciales al crear una conexión base. Si no se proporciona, las credenciales se comprueban automáticamente durante el paso de creación de la conexión de origen. |
| `auth.params.username` | El nombre de usuario que corresponde a su [!DNL Mailchimp] cuenta. Esto es necesario para la autenticación básica. |
| `auth.params.password` | La contraseña que corresponde a su [!DNL Mailchimp] cuenta. Esto es necesario para la autenticación básica. |

**Respuesta**

Una respuesta correcta devuelve la conexión base recién creada, incluido su identificador de conexión único (`id`). Este ID es necesario para explorar la estructura de archivos y el contenido de la fuente en el siguiente paso.

```json
{
    "id": "4cea039f-f1cc-4fa5-9136-db8dd4c7fbfa",
    "etag": "\"4000cff7-0000-0200-0000-6154bad60000\""
}
```

### Cree un [!DNL Mailchimp] conexión base con código de actualización de OAuth 2

Para crear un [!DNL Mailchimp] conexión base utilizando el código de actualización de OAuth 2, realice una solicitud de POST al `/connections` punto final al proporcionar credenciales para su `authorizationTestUrl`y `accessToken`.

**Formato de API**

```https
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para [!DNL Mailchimp]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "MailChimp base connection with OAuth 2 refresh code",
      "description": "MailChimp Members base connection with OAuth 2 refresh code",
      "connectionSpec": {
          "id": "2e8580db-6489-4726-96de-e33f5f60295f",
          "version": "1.0"
      },
      "auth": {
          "specName": "oAuth2RefreshCode",
          "params": {
              "authorizationTestUrl": "https://login.mailchimp.com/oauth2/metadata",
              "accessToken": "{ACCESS_TOKEN}"
          }
      }
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `name` | Nombre de la conexión base. Asegúrese de que el nombre de la conexión base sea descriptivo, ya que puede utilizarlo para buscar información sobre la conexión base. |
| `description` | (Opcional) Una propiedad que puede incluir para proporcionar más información sobre la conexión base. |
| `connectionSpec.id` | El ID de especificación de conexión de su origen. Este ID se puede recuperar después de registrar el origen mediante el [!DNL Flow Service] API. |
| `auth.specName` | El tipo de autenticación que utiliza para autenticar el origen en Platform. |
| `auth.params.authorizationTestUrl` | (Opcional) La URL de prueba de autorización se utiliza para validar las credenciales al crear una conexión base. Si no se proporciona, las credenciales se comprueban automáticamente durante el paso de creación de la conexión de origen. |
| `auth.params.accessToken` | Token de acceso correspondiente utilizado para autenticar el origen. Esto es necesario para la autenticación basada en OAuth. |

**Respuesta**

Una respuesta correcta devuelve la conexión base recién creada, incluido su identificador de conexión único (`id`). Este ID es necesario para explorar la estructura de archivos y el contenido de la fuente en el siguiente paso.

```json
{
    "id": "4cea039f-f1cc-4fa5-9136-db8dd4c7fbfa",
    "etag": "\"4000cff7-0000-0200-0000-6154bad60000\""
}
```

## Explorar la fuente {#explore}

Con el ID de conexión base que generó en el paso anterior, puede explorar archivos y directorios realizando solicitudes de GET.

>[!TIP]
>
>Para recuperar el tipo de formato aceptado para `{SOURCE_PARAMS}`, debe codificar todo el `list_id` en base64. Por ejemplo, `"list_id": "10c097ca71"` codificado en base64 equivale a `eyJsaXN0SWQiOiIxMGMwOTdjYTcxIn0=`.

**Formato de API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&sourceParams={SOURCE_PARAMS}
```

Al realizar solicitudes de GET para explorar la estructura de archivos y el contenido del origen, debe incluir los parámetros de consulta que se enumeran en la siguiente tabla:

| Parámetro | Descripción |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | El ID de conexión base generado en el paso anterior. |
| `{OBJECT_TYPE}` | Tipo de objeto que desea explorar. Para los orígenes REST, el valor predeterminado es `rest`. |
| `{OBJECT}` | El objeto que desea explorar. |
| `{FILE_TYPE}` | Este parámetro solo es necesario cuando se visualiza un directorio específico. Su valor representa la ruta del directorio que desea explorar. |
| `{PREVIEW}` | Valor booleano que define si el contenido de la conexión admite la vista previa. |
| `{SOURCE_PARAMS}` | Una cadena con codificación base64 de su `list_id`. |

**Solicitud**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/05c595e5-edc3-45c8-90bb-fcf556b57c4b/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyJsaXN0SWQiOiIxMGMwOTdjYTcxIn0=' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve la estructura del archivo consultado.

```json
{ 
"data": [
    {
        "list_id": "10c097ca71",
        "_links": [
            {
                "rel": "self",
                "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members",
                "method": "GET",
                "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/CollectionResponse.json",
                "schema": "https://us6.api.mailchimp.com/schema/3.0/Paths/Lists/Members/Collection.json"
            },
            {
                "rel": "parent",
                "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71",
                "method": "GET",
                "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Response.json"
            },
            {
                "rel": "create",
                "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members",
                "method": "POST",
                "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Response.json",
                "schema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/POST.json"
            }
        ],
        "members": [
            {
                "id": "cff65fb4c5f5828666ad846443720efd",
                "email_address": "kendallt2134@gmail.com",
                "unique_email_id": "72c758cbf1",
                "contact_id": "874a0d6e9ddb89d8b4a31e416ead2d6f",
                "full_name": "Kendall Roy",
                "web_id": 547094062,
                "email_type": "html",
                "status": "subscribed",
                "consents_to_one_to_one_messaging": true,
                "merge_fields": {
                    "FNAME": "Kendall",
                    "LNAME": "Roy",
                    "ADDRESS": {
                        "country": "US"
                    }
                },
                "stats": {
                    "avg_open_rate": 0,
                    "avg_click_rate": 0
                },
                "ip_opt": "103.43.112.97",
                "timestamp_opt": "2021-06-01T15:31:36+00:00",
                "member_rating": 2,
                "last_changed": "2021-06-01T15:31:36+00:00",
                "vip": false,
                "location": {
                    "latitude": 0,
                    "longitude": 0,
                    "gmtoff": 0,
                    "dstoff": 0
                },
                "source": "Admin Add",
                "tags_count": 0,
                "list_id": "10c097ca71",
                "_links": [
                        {
                            "rel": "self",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Response.json"
                        },
                        {
                            "rel": "parent",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/CollectionResponse.json",
                            "schema": "https://us6.api.mailchimp.com/schema/3.0/Paths/Lists/Members/Collection.json"
                        },
                        {
                            "rel": "update",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd",
                            "method": "PATCH",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Response.json",
                            "schema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/PATCH.json"
                        },
                        {
                            "rel": "upsert",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd",
                            "method": "PUT",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Response.json",
                            "schema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/PUT.json"
                        },
                        {
                            "rel": "delete",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd",
                            "method": "DELETE"
                        },
                        {
                            "rel": "activity",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd/activity",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Activity/Response.json"
                        },
                        {
                            "rel": "goals",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd/goals",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Goals/Response.json"
                        },
                        {
                            "rel": "notes",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd/notes",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Notes/CollectionResponse.json"
                        },
                        {
                            "rel": "events",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd/events",
                            "method": "POST",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Events/POST.json"
                        },
                        {
                            "rel": "delete_permanent",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd/actions/delete-permanent",
                            "method": "POST"
                        }
                    ]
                }
            ]  
        }
    ]
}
```

## Crear una conexión de origen {#source-connection}

Puede crear una conexión de origen realizando una solicitud de POST al [!DNL Flow Service] API. Una conexión de origen consiste en un ID de conexión, una ruta al archivo de datos de origen y un ID de especificación de conexión.

Para crear una conexión de origen, también debe definir un valor de enumeración para el atributo de formato de datos.

Utilice los siguientes valores de enumeración para orígenes basados en archivos:

| Formato de datos | Valor de enumeración |
| ----------- | ---------- |
| Delimitado | `delimited` |
| JSON | `json` |
| Parqué | `parquet` |

Para todos los orígenes basados en tablas, establezca el valor en `tabular`.

**Formato de API**

```https
POST /sourceConnections
```

**Solicitud**

La siguiente solicitud crea una conexión de origen para [!DNL Mailchimp]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "MailChimp source connection to ingest listId",
      "description": "MailChimp Members source connection to ingest listId",
      "baseConnectionId": "4cea039f-f1cc-4fa5-9136-db8dd4c7fbfa",
      "connectionSpec": {
          "id": "2e8580db-6489-4726-96de-e33f5f60295f",
          "version": "1.0"
      },
      "data": {
          "format": "json",
      },
      "params": {
          "listId": "10c097ca71"
      }
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `name` | Nombre de la conexión de origen. Asegúrese de que el nombre de la conexión de origen sea descriptivo, ya que puede utilizarlo para buscar información sobre la conexión de origen. |
| `description` | (Opcional) Una propiedad que puede incluir para proporcionar más información sobre la conexión de origen. |
| `baseConnectionId` | El ID de conexión base de [!DNL Mailchimp]. Este ID se generó en un paso anterior. |
| `connectionSpec.id` | El ID de especificación de conexión que corresponde a su origen. |
| `data.format` | El formato de la variable [!DNL Mailchimp] datos que desea ingerir. |
| `params.listId` | También conocido como ID de audiencia, la variable [!DNL Mailchimp] El ID de lista permite la transferencia de datos de audiencia a otras integraciones. |

**Respuesta**

Una respuesta correcta devuelve el identificador único (`id`) de la conexión de origen recién creada. Este ID es necesario en un paso posterior para crear un flujo de datos.

```json
{
    "id": "a51e4cf6-65ef-45f4-b4bf-4f03da5f01cc",
    "etag": "\"6b02b65d-0000-0200-0000-6154bfbe0000\""
}
```

## Creación de un esquema XDM de destino {#target-schema}

Para que los datos de origen se utilicen en Platform, se debe crear un esquema de destino para estructurar los datos de origen según sus necesidades. A continuación, el esquema de destino se utiliza para crear un conjunto de datos de Platform en el que se contienen los datos de origen.

Se puede crear un esquema XDM de destino realizando una solicitud de POST al [API del Registro de esquemas](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

Para ver los pasos detallados sobre cómo crear un esquema XDM de destino, consulte el tutorial sobre [creación de un esquema con la API](../../../../../xdm/api/schemas.md).

### Creación de un conjunto de datos de destino {#target-dataset}

Se puede crear un conjunto de datos de destino realizando una solicitud de POST al [API del servicio de catálogo](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml), que proporciona el ID del esquema de destino dentro de la carga útil.

Para ver los pasos detallados sobre cómo crear un conjunto de datos de destinatario, consulte el tutorial en [creación de un conjunto de datos mediante la API](../../../../../catalog/api/create-dataset.md).

## Creación de una conexión de destino {#target-connection}

Una conexión de destino representa la conexión con el destino en el que llegan los datos introducidos. Para crear una conexión de destino, debe proporcionar el ID de especificación de conexión fija que corresponda a la variable [!DNL Data Lake]. Este ID es: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Ahora tiene identificadores únicos, un esquema de destino, un conjunto de datos de destino y el ID de especificación de conexión al [!DNL Data Lake]. Con estos identificadores, puede crear una conexión de destino utilizando la variable [!DNL Flow Service] API para especificar el conjunto de datos que contendrá los datos de origen entrantes.

**Formato de API**

```https
POST /targetConnections
```

**Solicitud**

La siguiente solicitud crea una conexión de destino para [!DNL Mailchimp]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "MailChimp target connection",
      "description": "MailChimp Members target connection",
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      },
      "data": {
          "format": "parquet_xdm",
          "schema": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/570630b91eb9d5cf5db0436756abb110d02912917a67da2d",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "6155e3a9bd13651949515f14"
      }
  }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `name` | Nombre de la conexión de destino. Asegúrese de que el nombre de la conexión de destino sea descriptivo, ya que puede utilizarlo para buscar información sobre la conexión de destino. |
| `description` | (Opcional) Una propiedad que puede incluir para proporcionar más información sobre la conexión de destino. |
| `connectionSpec.id` | El ID de especificación de conexión correspondiente a [!DNL Data Lake]. Este ID fijo es: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | El formato de la variable [!DNL Mailchimp] datos que desea traer a Platform. |
| `params.dataSetId` | El ID del conjunto de datos de destino recuperado en un paso anterior. |


**Respuesta**

Una respuesta correcta devuelve el identificador único de la nueva conexión de destino (`id`). Este ID se requiere en pasos posteriores.

```json
{
    "id": "8db5fb4a-6ce8-4370-afc0-1765e39535a5",
    "etag": "\"960093ce-0000-0200-0000-6154da3e0000\""
}
```

## Creación de una asignación {#mapping}

Para que los datos de origen se introduzcan en un conjunto de datos de destino, primero deben asignarse al esquema de destino al que se adhiera el conjunto de datos de destino. Esto se consigue realizando una solicitud de POST al [[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/) con asignaciones de datos definidas dentro de la carga útil de la solicitud.

**Formato de API**

```http
POST /conversion/mappingSets
```

**Solicitud**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "version": 0,
      "xdmSchema": "_{TENANT_ID}.schemas.570630b91eb9d5cf5db0436756abb110d02912917a67da2d",
      "xdmVersion": "1.0",
      "mappings": [
      {
        "destinationXdmPath": "person.name.firstName",
        "sourceAttribute": "merge_fields.FNAME",
        "identity": false,
        "version": 0
      },
      {
        "destinationXdmPath": "person.name.lastName",
        "sourceAttribute": "merge_fields.LNAME",
        "identity": false,
        "version": 0
      }
    ]
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `xdmSchema` | El ID de la variable [esquema XDM de destino](#target-schema) generado en un paso anterior. |
| `mappings.destinationXdmPath` | Ruta XDM de destino a la que se asigna el atributo de origen. |
| `mappings.sourceAttribute` | El atributo de origen que debe asignarse a una ruta XDM de destino. |
| `mappings.identity` | Un valor booleano que designa si el conjunto de asignaciones se marcará para [!DNL Identity Service]. |

**Respuesta**

Una respuesta correcta devuelve detalles de la asignación recién creada, incluido su identificador único (`id`). Este valor es necesario en un paso posterior para crear un flujo de datos.

```json
{
    "id": "5a365b23962d4653b9d9be25832ee5b4",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## Crear un flujo {#flow}

El último paso hacia [!DNL Mailchimp] Los datos de Platform son para crear un flujo de datos. A partir de ahora, se han preparado los siguientes valores obligatorios:

* [ID de conexión de origen](#source-connection)
* [ID de conexión de Target](#target-connection)
* [ID de asignación](#mapping)

Un flujo de datos es responsable de programar y recopilar datos de un origen. Puede crear un flujo de datos realizando una solicitud de POST mientras proporciona los valores mencionados anteriormente dentro de la carga útil.

Para programar una ingesta, primero debe establecer el valor de la hora de inicio en hora de inicio en segundos. A continuación, debe establecer el valor de frecuencia en una de las cinco opciones: `once`, `minute`, `hour`, `day`o `week`. El valor de intervalo designa el periodo entre dos ingestas consecutivas y la creación de una ingesta única no requiere que se establezca un intervalo. Para las demás frecuencias, el valor del intervalo debe establecerse en igual o bueno que `15`.


**Formato de API**

```http
POST /flows
```

**Solicitud**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "MailChimp Members dataflow",
      "description": "MailChimp Members dataflow",
      "flowSpec": {
          "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "a51e4cf6-65ef-45f4-b4bf-4f03da5f01cc"
      ],
      "targetConnectionIds": [
          "8db5fb4a-6ce8-4370-afc0-1765e39535a5"
      ],
      "transformations": [
          {
              "name": "Mapping",
              "params": {
                  "mappingId": "5a365b23962d4653b9d9be25832ee5b4",
                  "mappingVersion": 0
              }
          }
      ],
      "scheduleParams": {
          "startTime": "1632809759",
          "frequency": "minute",
          "interval": 15
      }
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `name` | El nombre del flujo de datos. Asegúrese de que el nombre del flujo de datos sea descriptivo, ya que puede utilizarlo para buscar información en el flujo de datos. |
| `description` | (Opcional) Una propiedad que puede incluir para proporcionar más información sobre el flujo de datos. |
| `flowSpec.id` | ID de especificación de flujo necesario para crear un flujo de datos. Este ID fijo es: `6499120c-0b15-42dc-936e-847ea3c24d72`. |
| `flowSpec.version` | Versión correspondiente del ID de especificación de flujo. Este valor se establece de forma predeterminada en `1.0`. |
| `sourceConnectionIds` | La variable [ID de conexión de origen](#source-connection) generado en un paso anterior. |
| `targetConnectionIds` | La variable [ID de conexión de target](#target-connection) generado en un paso anterior. |
| `transformations` | Esta propiedad contiene las distintas transformaciones que deben aplicarse a los datos. Esta propiedad es necesaria al llevar datos que no sean compatibles con XDM a Platform. |
| `transformations.name` | El nombre asignado a la transformación. |
| `transformations.params.mappingId` | La variable [ID de asignación](#mapping) generado en un paso anterior. |
| `transformations.params.mappingVersion` | Versión correspondiente del ID de asignación. Este valor se establece de forma predeterminada en `0`. |
| `scheduleParams.startTime` | La hora de inicio designada para el momento en que comienza la primera ingesta de datos. |
| `scheduleParams.frequency` | Frecuencia con la que el flujo de datos recopilará datos. Los valores aceptables incluyen: `once`, `minute`, `hour`, `day`o `week`. |
| `scheduleParams.interval` | El intervalo designa el periodo entre dos ejecuciones de flujo consecutivas. El valor del intervalo debe ser un número entero distinto de cero. El intervalo no es necesario cuando la frecuencia está establecida como `once` y debe ser bueno o igual que `15` para otros valores de frecuencia. |

**Respuesta**

Una respuesta correcta devuelve el ID (`id`) del flujo de datos recién creado. Puede utilizar este ID para supervisar, actualizar o eliminar el flujo de datos.

```json
{
    "id": "209812ad-7bef-430c-b5b2-a648aae72094",
    "etag": "\"2e01f11d-0000-0200-0000-615649660000\""
}
```

## Apéndice

La siguiente sección proporciona información sobre los pasos que puede seguir para supervisar, actualizar y eliminar el flujo de datos.

### Monitorizar el flujo de datos

Una vez creado el flujo de datos, puede supervisar los datos que se están incorporando a través de él para ver información sobre ejecuciones de flujo, estado de finalización y errores. Para ver ejemplos completos de API, consulte la guía de [monitorización de los flujos de datos de fuentes mediante la API](../../monitor.md).

### Actualizar el flujo de datos

Actualice los detalles del flujo de datos, como su nombre y descripción, así como su programación de ejecución y los conjuntos de asignaciones asociados realizando una solicitud del PATCH al `/flows` punto final de [!DNL Flow Service] al proporcionar el ID de su flujo de datos. Al realizar una solicitud de PATCH, debe proporcionar la variable única de su flujo de datos `etag` en el `If-Match` encabezado. Para ver ejemplos completos de API, consulte la guía de [actualización de flujos de datos de fuentes mediante la API](../../update-dataflows.md).

### Actualizar la cuenta

Actualice el nombre, la descripción y las credenciales de la cuenta de origen realizando una solicitud de PATCH al [!DNL Flow Service] al proporcionar su ID de conexión base como parámetro de consulta. Al realizar una solicitud de PATCH, debe proporcionar la variable única de la cuenta de origen `etag` en el `If-Match` encabezado. Para ver ejemplos completos de API, consulte la guía de [actualizar la cuenta de origen mediante la API](../../update.md).

### Eliminar el flujo de datos

Elimine el flujo de datos realizando una solicitud de DELETE al [!DNL Flow Service] mientras proporciona el ID del flujo de datos que desea eliminar como parte del parámetro de consulta. Para ver ejemplos completos de API, consulte la guía de [eliminación de los flujos de datos mediante la API](../../delete-dataflows.md).

### Eliminar su cuenta

Elimine la cuenta realizando una solicitud de DELETE al [!DNL Flow Service] mientras proporciona el ID de conexión base de la cuenta que desea eliminar. Para ver ejemplos completos de API, consulte la guía de [eliminación de la cuenta de origen mediante la API](../../delete.md).