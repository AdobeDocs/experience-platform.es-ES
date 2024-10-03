---
keywords: Experience Platform;inicio;temas populares;conexión de flujo continuo;crear conexión de flujo continuo;guía de api;tutorial;crear una conexión de flujo continuo;ingesta de flujo continuo;ingesta;
title: Creación de una conexión de flujo continuo de API HTTP mediante la API de Flow Service
description: Este tutorial proporciona pasos sobre cómo crear una conexión de flujo continuo utilizando el origen de API HTTP para los datos sin procesar y XDM mediante la API de Flow Service
exl-id: 9f7fbda9-4cd3-4db5-92ff-6598702adc34
source-git-commit: 6ea5eaf28f260f974d168db2bed9bc95fcfa52af
workflow-type: tm+mt
source-wordcount: '1646'
ht-degree: 4%

---


# Crear una conexión de flujo continuo de API HTTP mediante la API [!DNL Flow Service]

Flow Service se utiliza para recopilar y centralizar datos de clientes de diferentes fuentes dentro de Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde las que se pueden conectar todas las fuentes de datos admitidas.

Este tutorial usa la [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) para guiarle por los pasos para crear una conexión de flujo continuo usando la API [!DNL Flow Service].

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)]](../../../../../xdm/home.md): el marco estandarizado mediante el cual [!DNL Platform] organiza los datos de experiencia.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): proporciona un perfil de consumidor unificado en tiempo real en función de los datos agregados de varios orígenes.

Además, la creación de una conexión de flujo continuo requiere que tenga un esquema XDM de destino y un conjunto de datos. Para aprender a crearlos, lea el tutorial sobre [datos de registros de transmisión](../../../../../ingestion/tutorials/streaming-record-data.md) o el tutorial sobre [datos de series de tiempo de transmisión](../../../../../ingestion/tutorials/streaming-time-series-data.md).

### Uso de API de Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía sobre [introducción a las API de Platform](../../../../../landing/api-guide.md).

## Crear una conexión base

Una conexión base especifica el origen y contiene la información necesaria para que el flujo sea compatible con las API de ingesta de flujo continuo. Al crear una conexión base, tiene la opción de crear una conexión no autenticada y autenticada.

### Conexión no autenticada

Las conexiones no autenticadas son la conexión de flujo continuo estándar que puede crear cuando desea transmitir datos a Platform.

Para crear una conexión base no autenticada, realice una solicitud de POST al extremo `/connections` y proporcione un nombre para la conexión, el tipo de datos y el identificador de especificación de la conexión HTTP API. Este identificador es `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`.

**Formato de API**

```http
POST /flowservice/connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para la API HTTP.

>[!BEGINTABS]

>[!TAB XDM]

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
    "name": "ACME Streaming Connection XDM Data",
    "description": "ACME streaming connection for customer data",
    "connectionSpec": {
        "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
        "version": "1.0"
    },
    "auth": {
      "specName": "Streaming Connection",
      "params": {
        "dataType": "xdm"
      }
    }
  }'
```

>[!TAB Datos sin procesar]

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
    "name": "ACME Streaming Connection Raw Data",
    "description": "ACME streaming connection for customer data",
    "connectionSpec": {
        "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
        "version": "1.0"
    },
    "auth": {
      "specName": "Streaming Connection",
      "params": {
        "dataType": "raw"
      }
    }
  }'
```

>[!ENDTABS]

| Propiedad | Descripción |
| --- | --- |
| `name` | Nombre de la conexión base. Asegúrese de que el nombre sea descriptivo, ya que puede utilizarlo para buscar información sobre la conexión base. |
| `description` | (Opcional) Una propiedad que puede incluir para proporcionar más información sobre la conexión base. |
| `connectionSpec.id` | ID de especificación de conexión que corresponde con la API HTTP. Este identificador es `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`. |
| `auth.params.dataType` | Tipo de datos de la conexión de flujo continuo. Los valores admitidos son: `xdm` y `raw`. |
| `auth.params.name` | Nombre de la conexión de flujo continuo que desea crear. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 201 con detalles de la conexión recién creada, incluido su identificador único (`id`).

```json
{
  "id": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
  "etag": "\"f50185ed-0000-0200-0000-637e8fad0000\""
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `id` | El `id` de su conexión base recién creada. |
| `etag` | Identificador asignado a la conexión, que especifica la versión de la conexión base. |

### Conexión autenticada

Las conexiones autenticadas deben utilizarse cuando necesite diferenciar entre registros procedentes de fuentes de confianza y no fiables. Los usuarios que deseen enviar información con Información de identificación personal (PII) deben crear una conexión autenticada al transmitir información a Platform.

Para crear una conexión base autenticada, debe incluir el parámetro `authenticationRequired` en la solicitud y especificar su valor como `true`. Durante este paso, también puede proporcionar un ID de origen para la conexión base autenticada. Este parámetro es opcional y utilizará el mismo valor que el atributo `name`, si no se proporciona.


**Formato de API**

```http
POST /flowservice/connections
```

**Solicitud**

La siguiente solicitud crea una conexión base autenticada para la API HTTP.

>[!BEGINTABS]

>[!TAB XDM]

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "ACME Streaming Connection XDM Data Authenticated",
     "description": "ACME streaming connection for customer data",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Authenticated XDM streaming connection",
             "dataType": "xdm",
             "name": "Authenticated XDM streaming connection",
             "authenticationRequired": true
         }
     }
 }
```

>[!TAB Datos sin procesar]

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "ACME Streaming Connection Raw Data Authenticated",
     "description": "ACME streaming connection for customer data",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Authenticated raw streaming connection",
             "dataType": "raw",
             "name": "Authenticated raw streaming connection",
             "authenticationRequired": true
         }
     }
 }
```

>[!ENDTABS]

| Propiedad | Descripción |
| -------- | ----------- |
| `auth.params.sourceId` | Identificador adicional que se puede utilizar al crear una conexión base autenticada. Este parámetro es opcional y utilizará el mismo valor que el atributo `name`, si no se proporciona. |
| `auth.params.authenticationRequired` | Este parámetro especifica si la conexión de flujo continuo requiere autenticación o no. Si `authenticationRequired` está establecido en `true`, se debe proporcionar autenticación para la conexión de flujo continuo. Si `authenticationRequired` está establecido en `false`, no se requiere autenticación. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 201 con detalles de la conexión recién creada, incluido su identificador único (`id`).

```json
{
  "id": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
  "etag": "\"f50185ed-0000-0200-0000-637e8fad0000\""
}
```

## Obtener URL del extremo de flujo continuo

Con la conexión base creada, ahora puede recuperar la dirección URL del extremo de flujo continuo.

**Formato de API**

```http
GET /flowservice/connections/{BASE_CONNECTION_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | El valor `id` de la conexión que creó anteriormente. |

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con información detallada sobre la conexión solicitada. La dirección URL del extremo de flujo continuo se crea automáticamente con la conexión y se puede recuperar con el valor `inletUrl`.

```json
{
  "items": [
    {
      "id": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
      "createdAt": 1669238699119,
      "updatedAt": 1669238699119,
      "createdBy": "acme@AdobeID",
      "updatedBy": "acme@AdobeID",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_ID}",
      "name": "ACME Streaming Connection XDM Data",
      "description": "ACME streaming connection for customer data",
      "connectionSpec": {
        "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
        "version": "1.0"
      },
      "state": "enabled",
      "auth": {
        "specName": "Streaming Connection",
        "params": {
          "sourceId": "ACME Streaming Connection XDM Data",
          "inletUrl": "https://dcs.adobedc.net/collection/667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec",
          "authenticationRequired": false,
          "inletId": "667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec",
          "dataType": "xdm",
          "name": "ACME Streaming Connection XDM Data"
        }
      },
      "version": "\"f50185ed-0000-0200-0000-637e8fad0000\"",
      "etag": "\"f50185ed-0000-0200-0000-637e8fad0000\""
    }
  ]
}
```

## Crear una conexión de origen {#source}

Para crear una conexión de origen, realice una solicitud de POST al extremo `/sourceConnections` y proporcione el identificador de conexión base.

**Formato de API**

```http
POST /flowservice/sourceConnections
```

**Solicitud**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "ACME Streaming Source Connection for Customer Data",
      "description": "A streaming source connection for ACME XDM Customer Data",
      "baseConnectionId": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
      "connectionSpec": {
          "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
          "version": "1.0"
      }
    }'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 201 con información detallada de la conexión de origen recién creada, incluido su identificador único (`id`).

```json
{
  "id": "34ece231-294d-416c-ad2a-5a5dfb2bc69f",
  "etag": "\"d505125b-0000-0200-0000-637eb7790000\""
}
```

## Creación de un esquema XDM de destino {#target-schema}

Para que los datos de origen se utilicen en Platform, se debe crear un esquema de destino para estructurar los datos de origen según sus necesidades. A continuación, el esquema de destino se utiliza para crear un conjunto de datos de Platform en el que se incluyen los datos de origen.

Se puede crear un esquema XDM de destino realizando una solicitud de POST a la [API de Registro de esquemas](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

Para ver los pasos detallados sobre cómo crear un esquema XDM de destino, consulte el tutorial de [creación de un esquema mediante la API](../../../../../xdm/api/schemas.md).

### Crear un conjunto de datos de destinatario {#target-dataset}

Se puede crear un conjunto de datos de destino realizando una solicitud de POST a la [API de servicio de catálogo](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml), que proporcione el ID del esquema de destino en la carga útil.

Para ver los pasos detallados sobre cómo crear un conjunto de datos de destino, consulte el tutorial de [creación de un conjunto de datos mediante la API](../../../../../catalog/api/create-dataset.md).

## Creación de una conexión de destino {#target}

Una conexión de destino representa la conexión con el destino donde aterrizan los datos introducidos. Para crear una conexión de destino, realice una solicitud de POST a `/targetConnections` mientras proporciona los ID para el conjunto de datos de destino y el esquema XDM de destino. Durante este paso, también debe proporcionar el ID de especificación de conexión del lago de datos. Este identificador es `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

**Formato de API**

```http
POST /flowservice/targetConnections
```

**Solicitud**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "ACME Streaming Target Connection",
      "description": "ACME Streaming Target Connection",
      "data": {
          "schema": {
              "id": "https://ns.adobe.com/{TENANT}/schemas/7f682c29f887512a897791e7161b90a1ae7ed3dd07a177b1",
              "version": "application/vnd.adobe.xed-full+json;version=1.0"
          }
      },
      "params": {
          "dataSetId": "637eb7fadc8a211b6312b65b"
      },
          "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      }
  }'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 201 con detalles de la conexión de destino recién creada, incluido su identificador único (`id`).

```json
{
  "id": "07f2f6ff-1da5-4704-916a-c615b873cba9",
  "etag": "\"340680f7-0000-0200-0000-637eb8730000\""
}
```

## Creación de una asignación {#mapping}

Para que los datos de origen se incorporen en un conjunto de datos de destino, primero deben asignarse al esquema de destino al que se adhiere el conjunto de datos de destino.

Para crear un conjunto de asignaciones, realice una solicitud de POST al extremo `mappingSets` de la [[!DNL Data Prep] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-prep.yaml) y proporcione el esquema XDM de destino `$id` y los detalles de los conjuntos de asignaciones que desee crear.

**Formato de API**

```http
POST /mappingSets
```

**Solicitud**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/mappingSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "version": 0,
      "xdmSchema": "https://ns.adobe.com/{TENANT}/schemas/7f682c29f887512a897791e7161b90a1ae7ed3dd07a177b1",
      "xdmVersion": "1.0",
      "mappings": [
          {
              "destinationXdmPath": "person.name.firstName",
              "sourceAttribute": "firstName",
              "identity": false,
              "version": 0
          },
          {
              "destinationXdmPath": "person.name.lastName",
              "sourceAttribute": "lastName",
              "identity": false,
              "version": 0
          }
      ]
  }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `xdmSchema` | El `$id` del esquema XDM de destino. |

**Respuesta**

Una respuesta correcta devuelve detalles de la asignación recién creada, incluido su identificador único (`id`). Este ID es necesario en un paso posterior para crear un flujo de datos.

```json
{
  "id": "79a623960d3f4969835c9e00dc90c8df",
  "version": 0,
  "createdDate": 1669249214031,
  "modifiedDate": 1669249214031,
  "createdBy": "acme@AdobeID",
  "modifiedBy": "acme@AdobeID"
}
```

## Creación de un flujo de datos

Con las conexiones de origen y destino creadas, ahora puede crear un flujo de datos. El flujo de datos es responsable de programar y recopilar datos de una fuente. Puede crear un flujo de datos realizando una solicitud de POST al extremo `/flows`.

**Formato de API**

```http
POST /flows
```

**Solicitud**

>[!BEGINTABS]

>[!TAB XDM]

La siguiente solicitud crea un flujo de datos de flujo continuo para los datos XDM.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "ACME Streaming Dataflow",
      "description": "ACME streaming dataflow for customer data",
      "flowSpec": {
        "id": "d8a6f005-7eaf-4153-983e-e8574508b877",
        "version": "1.0"
      },
      "sourceConnectionIds": [
        "34ece231-294d-416c-ad2a-5a5dfb2bc69f"
      ],
      "targetConnectionIds": [
        "07f2f6ff-1da5-4704-916a-c615b873cba9"
      ]
    }'
```

>[!TAB SIN PROCESAR]

Las siguientes solicitudes crean un flujo de datos de flujo continuo para los datos sin procesar.

Al crear un flujo de datos con transformaciones, el parámetro `name` no se puede cambiar. Este valor siempre debe establecerse en `Mapping`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "<name>",
      "description": "<description>",
      "flowSpec": {
        "id": "c1a19761-d2c7-4702-b9fa-fe91f0613e81",
        "version": "1.0"
      },
      "sourceConnectionIds": [
        "34ece231-294d-416c-ad2a-5a5dfb2bc69f"
      ],
      "targetConnectionIds": [
        "07f2f6ff-1da5-4704-916a-c615b873cba9"
      ],
      "transformations": [
        {
          "name": "Mapping",
          "params": {
            "mappingId": "79a623960d3f4969835c9e00dc90c8df",
            "mappingVersion": 0
          }
        }
      ]
    }'
```

>[!ENDTABS]

| Propiedad | Descripción |
| --- | --- |
| `name` | Nombre del flujo de datos. Asegúrese de que el nombre del flujo de datos sea descriptivo, ya que puede utilizarlo para buscar información en él. |
| `description` | (Opcional) Una propiedad que puede incluir para proporcionar más información sobre el flujo de datos. |
| `flowSpec.id` | Identificador de especificación de flujo para [!DNL HTTP API]. Para crear un flujo de datos con transformaciones, debe utilizar `c1a19761-d2c7-4702-b9fa-fe91f0613e81`. Para crear un flujo de datos sin transformaciones, use `d8a6f005-7eaf-4153-983e-e8574508b877`. |
| `sourceConnectionIds` | [Id. de conexión de origen](#source) recuperado en un paso anterior. |
| `targetConnectionIds` | [Id. de conexión de destino](#target) recuperado en un paso anterior. |
| `transformations.params.mappingId` | [ID de asignación](#mapping) recuperado en un paso anterior. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 201 con detalles del flujo de datos recién creado, incluido su identificador único (`id`).

```json
{
  "id": "f2ae0194-8bd8-4a40-a4d9-f07bdc3e6ce2",
  "etag": "\"dc0459ae-0000-0200-0000-637ebaec0000\""
}
```

## Publicar datos para ingerirlos en Platform {#ingest-data}

>[!NOTE]
>
>Debe añadir un retraso de al menos ~5 minutos entre la creación del flujo de datos y la ingesta de cualquier dato de flujo continuo. Esto permite que el flujo de datos esté completamente habilitado antes de que se incorpore cualquier dato.

Ahora que ha creado el flujo, puede enviar el mensaje JSON al extremo de flujo continuo creado anteriormente.

**Formato de API**

```http
POST /collection/{INLET_URL}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{INLET_URL}` | Su URL de extremo de flujo continuo. Puede recuperar esta dirección URL realizando una solicitud de GET al extremo `/connections` y proporcionando al mismo tiempo su ID de conexión base. |
| `{FLOW_ID}` | El ID del flujo de datos de streaming de la API HTTP. Este ID es necesario para los datos XDM y RAW. |

**Solicitud**

>[!BEGINTABS]

>[!TAB Enviar datos XDM]

```shell
curl -X POST https://dcs.adobedc.net/collection/667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec \
  -H 'Content-Type: application/json' \
  -d '{
        "header": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT}/schemas/7f682c29f887512a897791e7161b90a1ae7ed3dd07a177b1",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1.0"
          },
          "flowId": "f2ae0194-8bd8-4a40-a4d9-f07bdc3e6ce2",
          "datasetId": "604a18a3bae67d18db6d258c"
        },
        "body": {
          "xdmMeta": {
            "schemaRef": {
              "id": "https://ns.adobe.com/{TENANT}/schemas/7f682c29f887512a897791e7161b90a1ae7ed3dd07a177b1",
              "contentType": "application/vnd.adobe.xed-full-notext+json; version=1.0"
            }
          },
          "xdmEntity": {
            "_id": "http-source-connector-acme-01",
            "person": {
              "name": {
                "firstName": "suman",
                "lastName": "nolan"
              }
            },
            "workEmail": {
              "primary": true,
              "address": "suman@acme.com",
              "type": "work",
              "status": "active"
            }
          }
        }
      }'
```

>[!TAB Enviar datos sin procesar con ID de flujo como encabezado HTTP]

Al enviar datos sin procesar, puede especificar el ID de flujo como parámetro de consulta o como parte del encabezado HTTP. El siguiente ejemplo especifica el ID de flujo como un encabezado HTTP.

```shell
curl -X POST https://dcs.adobedc.net/collection/667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec \
  -H 'Content-Type: application/json' 
  -H 'x-adobe-flow-id=f2ae0194-8bd8-4a40-a4d9-f07bdc3e6ce2' \
  -d '{
      "name": "Johnson Smith",
      "location": {
          "city": "Seattle",
          "country": "United State of America",
          "address": "3692 Main Street"
      },
      "gender": "Male",
      "birthday": {
          "year": 1984,
          "month": 6,
          "day": 9
      }
  }'
```

>[!TAB Enviar datos sin procesar con ID de flujo como parámetro de consulta]

Al enviar datos sin procesar, puede especificar el ID de flujo como parámetro de consulta o como encabezado HTTP. El ejemplo siguiente especifica el ID de flujo como parámetro de consulta.

```shell
curl -X POST https://dcs.adobedc.net/collection/667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec?x-adobe-flow-id=f2ae0194-8bd8-4a40-a4d9-f07bdc3e6ce2 \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Johnson Smith",
      "location": {
          "city": "Seattle",
          "country": "United State of America",
          "address": "3692 Main Street"
      },
      "gender": "Male",
      "birthday": {
          "year": 1984,
          "month": 6,
          "day": 9
      }
  }'
```

>[!ENDTABS]

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la información recién introducida.

```json
{
    "inletId": "{BASE_CONNECTION_ID}",
    "xactionId": "1584479347507:2153:240",
    "receivedTimeMs": 1584479347507
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{BASE_CONNECTION_ID}` | El ID de la conexión de flujo continuo creada anteriormente. |
| `xactionId` | Identificador único generado del lado del servidor para el registro que acaba de enviar. Este ID ayuda al Adobe a rastrear el ciclo de vida de este registro a través de varios sistemas y con la depuración. |
| `receivedTimeMs` | Una marca de tiempo (epoch en milisegundos) que muestra a qué hora se recibió la solicitud. |


## Pasos siguientes

Al seguir este tutorial, ha creado una conexión HTTP de flujo continuo que le permite utilizar el extremo de flujo continuo para introducir datos en Platform. Para obtener instrucciones para crear una conexión de flujo continuo en la interfaz de usuario, lea el [tutorial sobre la creación de una conexión de flujo continuo](../../../ui/create/streaming/http.md).

Para aprender a transmitir datos a Platform, lea el tutorial sobre [transmisión de datos de series temporales](../../../../../ingestion/tutorials/streaming-time-series-data.md) o el tutorial sobre [transmisión de datos de registros](../../../../../ingestion/tutorials/streaming-record-data.md).

## Apéndice

Esta sección proporciona información complementaria sobre la creación de conexiones de flujo continuo mediante la API.

### Envío de mensajes a una conexión de flujo continuo autenticada

Si una conexión de flujo continuo tiene habilitada la autenticación, el cliente deberá agregar el encabezado `Authorization` a su solicitud.

Si el encabezado `Authorization` no está presente, o si se envía un token de acceso no válido o caducado, se devolverá una respuesta HTTP 401 no autorizada, con una respuesta similar a la siguiente:

**Respuesta**

```json
{
    "type": "https://ns.adobe.com/adobecloud/problem/data-collection-service-authorization",
    "status": "401",
    "title": "Authorization",
    "report": {
        "message": "[id] Ims service token is empty"
    }
}
```

