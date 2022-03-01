---
keywords: Experience Platform;inicio;temas populares;orígenes;conectores;conectores de origen;sdk de fuentes;sdk;SDK
solution: Experience Platform
title: Creación de un flujo de datos para Mailchimp Campaign mediante la API de servicio de flujo
topic-legacy: tutorial
description: Obtenga información sobre cómo conectar Adobe Experience Platform a MailChimp Campaign mediante la API de servicio de flujo.
exl-id: fd4821c7-6fe1-4cad-8e13-3549dbe0ce98
source-git-commit: fd851dea5623522e4706c6beb8bd086d466773b5
workflow-type: tm+mt
source-wordcount: '2319'
ht-degree: 3%

---

# Crear un flujo de datos para [!DNL Mailchimp Campaign] uso de la API de servicio de flujo

El siguiente tutorial le guía por los pasos para crear una conexión de origen y un flujo de datos para [!DNL Mailchimp Campaign] datos a Platform mediante [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Requisitos previos

Antes de conectarse [!DNL Mailchimp] a Adobe Experience Platform mediante el código de actualización de OAuth 2, primero debe recuperar el token de acceso para [!DNL MailChimp.] Consulte la [[!DNL Mailchimp] Guía de OAuth 2](https://mailchimp.com/developer/marketing/guides/access-user-data-oauth-2/) para obtener instrucciones detalladas sobre cómo encontrar el token de acceso.

## Creación de una conexión base {#base-connection}

Una vez que haya recuperado su [!DNL Mailchimp] credenciales de autenticación, ahora puede iniciar el proceso de creación de flujo de datos para traer [!DNL Mailchimp Campaign] a Platform. El primer paso para crear un flujo de datos es crear una conexión base.

Una conexión base retiene información entre la fuente y la plataforma, incluidas las credenciales de autenticación de la fuente, el estado actual de la conexión y el ID de conexión base único. El ID de conexión base le permite explorar y navegar archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

[!DNL Mailchimp] admite autenticación básica y código de actualización de OAuth 2. Consulte los siguientes ejemplos para obtener instrucciones sobre cómo autenticarse con cualquiera de los tipos de autenticación.

### Cree un [!DNL Mailchimp] conexión base con autenticación básica

Para crear un [!DNL Mailchimp] conexión base usando autenticación básica, realice una solicitud de POST al `/connections` punto final de [!DNL Flow Service] API mientras proporciona credenciales para su `host`, `authorizationTestUrl`, `username`y `password`.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "Mailchimp base connection with basic authentication",
      "description": "Mailchimp Campaign base connection with basic authentication",
      "connectionSpec": {
          "id": "c8ce8c8c-37fb-4162-9fbf-c2f181e04a7a",
          "version": "1.0"
      },
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "host": "{HOST}",
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
| `auth.params.host` | La URL raíz utilizada para conectarse a [!DNL Mailchimp] API. El formato de la dirección URL raíz es `https://{DC}.api.mailchimp.com`, donde `{DC}` representa el centro de datos que corresponde a su cuenta. |
| `auth.params.authorizationTestUrl` | (Opcional) La URL de prueba de autorización se utiliza para validar las credenciales al crear una conexión base. Si no se proporciona, las credenciales se comprueban automáticamente durante el paso de creación de la conexión de origen. |
| `auth.params.username` | El nombre de usuario que corresponde a su [!DNL Mailchimp] cuenta. Esto es necesario para la autenticación básica. |
| `auth.params.password` | La contraseña que corresponde a su [!DNL Mailchimp] cuenta. Esto es necesario para la autenticación básica. |

**Respuesta**

Una respuesta correcta devuelve la conexión base recién creada, incluido su identificador de conexión único (`id`). Este ID es necesario para explorar la estructura de archivos y el contenido de la fuente en el siguiente paso.

```json
{
    "id": "9601747c-6874-4c02-bb00-5732a8c43086",
    "etag": "\"3702dabc-0000-0200-0000-615b5b5a0000\""
}
```

### Cree un [!DNL Mailchimp] conexión base con código de actualización de OAuth 2

Para crear un [!DNL Mailchimp] conexión base utilizando el código de actualización de OAuth 2, realice una solicitud de POST al `/connections` punto final al proporcionar credenciales para su `host`, `authorizationTestUrl`y `accessToken`.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "Mailchimp base connection with OAuth 2 refresh code",
      "description": "Mailchimp Campaign base connection with OAuth 2 refresh code",
      "connectionSpec": {
          "id": "c8ce8c8c-37fb-4162-9fbf-c2f181e04a7a",
          "version": "1.0"
      },
      "auth": {
          "specName": "oAuth2RefreshCode",
          "params": {
              "host": "{HOST}",
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
| `auth.params.host` | La URL raíz utilizada para conectarse a [!DNL Mailchimp] API. El formato de la dirección URL raíz es `https://{DC}.api.mailchimp.com`, donde `{DC}` representa el centro de datos que corresponde a su cuenta. |
| `auth.params.authorizationTestUrl` | (Opcional) La URL de prueba de autorización se utiliza para validar las credenciales al crear una conexión base. Si no se proporciona, las credenciales se comprueban automáticamente durante el paso de creación de la conexión de origen. |
| `auth.params.accessToken` | Token de acceso correspondiente utilizado para autenticar el origen. Esto es necesario para la autenticación basada en OAuth. |

**Respuesta**

Una respuesta correcta devuelve la conexión base recién creada, incluido su identificador de conexión único (`id`). Este ID es necesario para explorar la estructura de archivos y el contenido de la fuente en el siguiente paso.

```json
{
    "id": "9601747c-6874-4c02-bb00-5732a8c43086",
    "etag": "\"3702dabc-0000-0200-0000-615b5b5a0000\""
}
```

## Explorar la fuente {#explore}

Con el ID de conexión base que generó en el paso anterior, puede explorar archivos y directorios realizando solicitudes de GET. Al realizar solicitudes de GET para explorar la estructura de archivos y el contenido del origen, debe incluir los parámetros de consulta que se enumeran en la siguiente tabla:

| Parámetro | Descripción |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | El ID de conexión base generado en el paso anterior. |
| `{OBJECT_TYPE}` | Tipo de objeto que desea explorar. Para los orígenes REST, el valor predeterminado es `rest`. |
| `{OBJECT}` | El objeto que desea explorar. |
| `{FILE_TYPE}` | Este parámetro solo es necesario cuando se visualiza un directorio específico. Su valor representa la ruta del directorio que desea explorar. |
| `{PREVIEW}` | Valor booleano que define si el contenido de la conexión admite la vista previa. |
| `{SOURCE_PARAMS}` | Una cadena con codificación base64 de su `campaign_id`. |

>[!TIP]
>
>Para recuperar el tipo de formato aceptado para `{SOURCE_PARAMS}`, debe codificar todo el `campaignId` en base64. Por ejemplo, `{"campaignId": "c66a200cda"}` codificado en base64 equivale a `eyJjYW1wYWlnbklkIjoiYzY2YTIwMGNkYSJ9`.

**Formato de API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&objectType={OBJECT_TYPE}&fileType={FILE_TYPE}&preview={PREVIEW}&sourceParams={SOURCE_PARAMS}
```

**Solicitud**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/05c595e5-edc3-45c8-90bb-fcf556b57c4b/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyJjYW1wYWlnbklkIjoiYzY2YTIwMGNkYSJ9' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve la estructura del archivo consultado.

```json
{
    "data": [
        {
            "emails": [
                {
                    "campaign_id": "c66a200cda",
                    "list_id": "10c097ca71",
                    "list_is_active": true,
                    "email_id": "cff65fb4c5f5828666ad846443720efd",
                    "email_address": "kendall2134@gmail.com",
                    "_links": [
                        {
                            "rel": "parent",
                            "href": "https://us6.api.mailchimp.com/3.0/reports/c66a200cda/email-activity",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Reports/EmailActivity/CollectionResponse.json"
                        },
                        {
                            "rel": "self",
                            "href": "https://us6.api.mailchimp.com/3.0/reports/c66a200cda/email-activity/cff65fb4c5f5828666ad846443720efd",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Reports/EmailActivity/Response.json"
                        },
                        {
                            "rel": "member",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Response.json"
                        }
                    ]
                },
                {
                    "campaign_id": "c66a200cda",
                    "list_id": "10c097ca71",
                    "list_is_active": true,
                    "email_id": "a16b82774b211afaf60902d1afd8abc5",
                    "email_address": "logan9935890967@gmail.com",
                    "_links": [
                        {
                            "rel": "parent",
                            "href": "https://us6.api.mailchimp.com/3.0/reports/c66a200cda/email-activity",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Reports/EmailActivity/CollectionResponse.json"
                        },
                        {
                            "rel": "self",
                            "href": "https://us6.api.mailchimp.com/3.0/reports/c66a200cda/email-activity/a16b82774b211afaf60902d1afd8abc5",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Reports/EmailActivity/Response.json"
                        },
                        {
                            "rel": "member",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/a16b82774b211afaf60902d1afd8abc5",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Response.json"
                        }
                    ]
                },
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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "MailChimp source connection to ingest campaign ID",
      "description": "MailChimp Campaign source connection to ingest campaign ID",
      "baseConnectionId": "4cea039f-f1cc-4fa5-9136-db8dd4c7fbfa",
      "connectionSpec": {
          "id": "c8ce8c8c-37fb-4162-9fbf-c2f181e04a7a",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
          "campaignId": "c66a200cda"
      }
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `name` | Nombre de la conexión de origen. Asegúrese de que el nombre de la conexión de origen sea descriptivo, ya que puede utilizarlo para buscar información sobre la conexión de origen. |
| `description` | Un valor opcional que puede incluir para proporcionar más información sobre la conexión de origen. |
| `baseConnectionId` | El ID de conexión base de [!DNL Mailchimp]. Este ID se generó en un paso anterior. |
| `connectionSpec.id` | El ID de especificación de conexión que corresponde a su origen. |
| `data.format` | El formato de la variable [!DNL Mailchimp] datos que desea ingerir. |
| `params.campaignId` | La variable [!DNL Mailchimp] el ID de campaña identifica un [!DNL Mailchimp] campaign, que le permite enviar correos electrónicos a sus listas o audiencias. |

**Respuesta**

Una respuesta correcta devuelve el identificador único (`id`) de la conexión de origen recién creada. Este ID es necesario en un paso posterior para crear un flujo de datos.

```json
{
    "id": "d6557bf1-7347-415f-964c-9316bd4cbf56",
    "etag": "\"e205c206-0000-0200-0000-615b5c070000\""
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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "MailChimp target connection",
      "description": "MailChimp Campaign target connection",
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
| `description` | Un valor opcional que puede incluir para proporcionar más información sobre la conexión de destino. |
| `connectionSpec.id` | El ID de especificación de conexión correspondiente a [!DNL Data Lake]. Este ID fijo es: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | El formato de la variable [!DNL Mailchimp] datos que desea traer a Platform. |
| `params.dataSetId` | El ID del conjunto de datos de destino recuperado en un paso anterior. |


**Respuesta**

Una respuesta correcta devuelve el identificador único de la nueva conexión de destino (`id`). Este ID se requiere en pasos posteriores.

```json
{
    "id": "9463fe9c-027d-4347-a423-894fcd105647",
    "etag": "\"b902e822-0000-0200-0000-615b5c370000\""
}
```

>[!IMPORTANT]
>
>Actualmente, las funciones de preparación de datos no son compatibles con [!DNL Mailchimp Campaign].

<!--
## Create a mapping {#mapping}

In order for the source data to be ingested into a target dataset, it must first be mapped to the target schema that the target dataset adheres to. This is achieved by performing a POST request to Conversion Service with data mappings defined within the request payload.

**API format**

```http
POST /conversion/mappingSets
```

**Request**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
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

| Property | Description |
| --- | --- |
| `xdmSchema` | The ID of the [target XDM schema](#target-schema) generated in an earlier step. |
| `mappings.destinationXdmPath` | The destination XDM path where the source attribute is being mapped to. |
| `mappings.sourceAttribute` | The source attribute that needs to be mapped to a destination XDM path. |
| `mappings.identity` | A boolean value that designates whether the mapping set will be marked for [!DNL Identity Service]. |

**Response**

A successful response returns details of the newly created mapping including its unique identifier (`id`). This value is required in a later step to create a dataflow.

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

--->

## Crear un flujo {#flow}

El último paso hacia [!DNL Mailchimp] Los datos de Platform son para crear un flujo de datos. A partir de ahora, se han preparado los siguientes valores obligatorios:

* [ID de conexión de origen](#source-connection)
* [ID de conexión de Target](#target-connection)

Un flujo de datos es responsable de programar y recopilar datos de un origen. Puede crear un flujo de datos realizando una solicitud de POST mientras proporciona los valores mencionados anteriormente dentro de la carga útil.

Para programar una ingesta, primero debe establecer el valor de la hora de inicio en hora de inicio en segundos. A continuación, debe establecer el valor de frecuencia en una de las cinco opciones: `once`, `minute`, `hour`, `day`o `week`. El valor de intervalo designa el periodo entre dos ingestas consecutivas y la creación de una ingesta única (`once`) no requiere que se establezca un intervalo. Para las demás frecuencias, el valor del intervalo debe establecerse en igual o bueno que `15`.


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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "MailChimp Campaign dataflow",
      "description": "MailChimp Campaign dataflow",
      "flowSpec": {
          "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "d6557bf1-7347-415f-964c-9316bd4cbf56"
      ],
      "targetConnectionIds": [
          "9463fe9c-027d-4347-a423-894fcd105647"
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
| `scheduleParams.startTime` | La hora de inicio designada para el momento en que comienza la primera ingesta de datos. |
| `scheduleParams.frequency` | Frecuencia con la que el flujo de datos recopilará datos. Los valores aceptables incluyen: `once`, `minute`, `hour`, `day`o `week`. |
| `scheduleParams.interval` | El intervalo designa el periodo entre dos ejecuciones de flujo consecutivas. El valor del intervalo debe ser un número entero distinto de cero. El intervalo no es necesario cuando la frecuencia está establecida como `once` y debe ser bueno o igual que `15` para otros valores de frecuencia. |

**Respuesta**

Una respuesta correcta devuelve el ID (`id`) del flujo de datos recién creado. Puede utilizar este ID para supervisar, actualizar o eliminar el flujo de datos.

```json
{
    "id": "be2d5249-eeaf-4a74-bdbd-b7bf62f7b2da",
    "etag": "\"7e010621-0000-0200-0000-615b5c9b0000\""
}
```

## Monitorizar el flujo de datos

Una vez creado el flujo de datos, puede supervisar los datos que se están incorporando a través de él para ver información sobre ejecuciones de flujo, estado de finalización y errores.

**Formato de API**

```http
GET /runs?property=flowId=={FLOW_ID}
```

**Solicitud**

La siguiente solicitud recupera las especificaciones de un flujo de datos existente.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/runs?property=flowId==993f908f-3342-4d9c-9f3c-5aa9a189ca1a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve detalles sobre la ejecución del flujo, incluida información sobre la fecha de creación, las conexiones de origen y destino, así como el identificador único de la ejecución del flujo (`id`).

```json
{
    "items": [
        {
            "id": "209812ad-7bef-430c-b5b2-a648aae72094",
            "createdAt": 1633044829955,
            "updatedAt": 1633044838006,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "imsOrgId": "{IMS_ORG}",
            "name": "MailChimp Campaign dataflow",
            "description": "MailChimp Campaign dataflow",
            "flowSpec": {
                "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
                "version": "1.0"
            },
            "state": "enabled",
            "version": "\"7e01322c-0000-0200-0000-615b5d520000\"",
            "etag": "\"7e01322c-0000-0200-0000-615b5d520000\"",
            "sourceConnectionIds": [
                "d6557bf1-7347-415f-964c-9316bd4cbf56"
            ],
            "targetConnectionIds": [
                "9463fe9c-027d-4347-a423-894fcd105647"
            ],
            "inheritedAttributes": {
                "sourceConnections": [
                    {
                        "id": "d6557bf1-7347-415f-964c-9316bd4cbf56",
                        "connectionSpec": {
                            "id": "c8ce8c8c-37fb-4162-9fbf-c2f181e04a7a",
                            "version": "1.0"
                        },
                        "baseConnection": {
                            "id": "9601747c-6874-4c02-bb00-5732a8c43086",
                            "connectionSpec": {
                                "id": "c8ce8c8c-37fb-4162-9fbf-c2f181e04a7a",
                                "version": "1.0"
                            }
                        }
                    }
                ],
                "targetConnections": [
                    {
                        "id": "9463fe9c-027d-4347-a423-894fcd105647",
                        "connectionSpec": {
                            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
                            "version": "1.0"
                        }
                    }
                ]
            },
            "scheduleParams": {
                "startTime": "1633377385",
                "frequency": "minute",
                "interval": 15
            },
            "runs": "/flows/be2d5249-eeaf-4a74-bdbd-b7bf62f7b2da/runs",
            "lastOperation": {
                "started": 1633377421476,
                "updated": 0,
                "operation": "create"
            },
            "lastRunDetails": {
                "id": "84f95788-3e83-4ce0-8e45-c0a89117c6f1",
                "state": "failed",
                "startedAtUTC": 1633377445979,
                "completedAtUTC": 1633377487082
            }
        }
    ]
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `items` | Contiene una única carga útil de metadatos asociados a su ejecución de flujo específica. |
| `id` | Muestra el ID correspondiente al flujo de datos. |
| `state` | Muestra el estado actual del flujo de datos. |
| `inheritedAttributes` | Contiene los atributos que definen el flujo, como los ID para su conexión base, origen y destino correspondiente. |
| `scheduleParams` | Contiene información sobre el programa de ingesta de su flujo de datos, como su hora de inicio (en tiempo de época), frecuencia e intervalo. |
| `transformations` | Contiene información sobre las propiedades de transformación aplicadas al flujo de datos. |
| `runs` | Muestra el ID de ejecución correspondiente del flujo. Puede utilizar este ID para supervisar ejecuciones de flujo específicas. |

## Actualizar el flujo de datos

Para actualizar la programación, el nombre y la descripción de ejecución del flujo de datos, realice una solicitud de PATCH al [!DNL Flow Service] mientras proporciona su ID de flujo, versión y la nueva programación que desea utilizar.

>[!IMPORTANT]
>
>La variable `If-Match` es obligatorio cuando se realiza una solicitud de PATCH. El valor de este encabezado es la versión única de la conexión que desea actualizar.

**Formato de API**

```http
PATCH /flows/{FLOW_ID}
```

**Solicitud**

La siguiente solicitud actualiza la programación de la ejecución del flujo, así como el nombre y la descripción del flujo de datos.

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/flowservice/flows/209812ad-7bef-430c-b5b2-a648aae72094' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'If-Match: "2e01f11d-0000-0200-0000-615649660000"' \
  -d '[
          {
              "op": "replace",
              "path": "/scheduleParams/frequency",
              "value": "day"
          },
          {
              "op": "replace",
              "path": "/name",
              "value": "MailChimp Campaign Dataflow 2.0"
          },
          {
              "op": "replace",
              "path": "/description",
              "value": "MailChimp Campaign Dataflow Updated"
          }
      ]'
```

| Parámetro | Descripción |
| --------- | ----------- |
| `op` | La llamada de operación utilizada para definir la acción necesaria para actualizar el flujo de datos. Las operaciones incluyen: `add`, `replace`y `remove`. |
| `path` | Ruta del parámetro que se va a actualizar. |
| `value` | El nuevo valor con el que desea actualizar el parámetro. |

**Respuesta**

Una respuesta correcta devuelve su ID de flujo y una etiqueta actualizada. Puede comprobar la actualización realizando una solicitud de GET a la variable [!DNL Flow Service] al proporcionar su ID de flujo.

```json
{
    "id": "209812ad-7bef-430c-b5b2-a648aae72094",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Eliminar el flujo de datos

Con un ID de flujo existente, puede eliminar un flujo de datos realizando una solicitud de DELETE al [!DNL Flow Service] API.

**Formato de API**

```http
DELETE /flows/{FLOW_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{FLOW_ID}` | El único `id` para el flujo de datos que desea eliminar. |

**Solicitud**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/flowservice/flows/209812ad-7bef-430c-b5b2-a648aae72094' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 204 (sin contenido) y un cuerpo en blanco. Puede confirmar la eliminación intentando realizar una solicitud de búsqueda (GET) al flujo de datos. La API devolverá un error HTTP 404 (no encontrado), que indica que se ha eliminado el flujo de datos.

## Actualizar la conexión

Para actualizar el nombre, la descripción y las credenciales de la conexión, realice una solicitud de PATCH al [!DNL Flow Service] al proporcionar el ID de conexión base, la versión y la nueva información que desea utilizar.

>[!IMPORTANT]
>
>La variable `If-Match` es obligatorio cuando se realiza una solicitud de PATCH. El valor de este encabezado es la versión única de la conexión que desea actualizar.

**Formato de API**

```http
PATCH /connections/{BASE_CONNECTION_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | El único `id` para la conexión que desea actualizar. |

**Solicitud**

La siguiente solicitud proporciona un nuevo nombre y descripción, así como un nuevo conjunto de credenciales, para actualizar la conexión con.

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/flowservice/connections/4cea039f-f1cc-4fa5-9136-db8dd4c7fbfa' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'If-Match: 4000cff7-0000-0200-0000-6154bad60000' \
  -d '[
      {
          "op": "replace",
          "path": "/auth/params",
          "value": {
              "username": "mailchimp-member-activity-user",
              "password": "{NEW_PASSWORD}"
          }
      },
      {
          "op": "replace",
          "path": "/name",
          "value": "MailChimp Campaign Connection 2.0"
      },
      {
          "op": "add",
          "path": "/description",
          "value": "Updated MailChimp Campaign Connection"
      }
  ]'
```

| Parámetro | Descripción |
| --------- | ----------- |
| `op` | La llamada de operación utilizada para definir la acción necesaria para actualizar la conexión. Las operaciones incluyen: `add`, `replace`y `remove`. |
| `path` | Ruta del parámetro que se va a actualizar. |
| `value` | El nuevo valor con el que desea actualizar el parámetro. |

**Respuesta**

Una respuesta correcta devuelve su ID de conexión base y una etiqueta actualizada. Puede comprobar la actualización realizando una solicitud de GET a la variable [!DNL Flow Service] al proporcionar su ID de conexión.

```json
{
    "id": "4cea039f-f1cc-4fa5-9136-db8dd4c7fbfa",
    "etag": "\"3600e378-0000-0200-0000-5f40212f0000\""
}
```

## Eliminar la conexión

Una vez que tenga un ID de conexión base existente, realice una solicitud de DELETE al [!DNL Flow Service] API.

**Formato de API**

```http
DELETE /connections/{CONNECTION_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | El único `id` para la conexión base que desea eliminar. |

**Solicitud**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/flowservice/connections/4cea039f-f1cc-4fa5-9136-db8dd4c7fbfa' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 204 (sin contenido) y un cuerpo en blanco.

Puede confirmar la eliminación intentando realizar una solicitud de búsqueda (GET) a la conexión.
