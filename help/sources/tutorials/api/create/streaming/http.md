---
keywords: Experience Platform;inicio;temas populares;conexión de flujo continuo;crear conexión de flujo continuo;guía de api;tutorial;crear una conexión de flujo continuo;ingesta de flujo continuo;ingesta;
solution: Experience Platform
title: Creación de una conexión de flujo de API HTTP mediante la API
topic-legacy: tutorial
type: Tutorial
description: Este tutorial le ayudará a empezar a utilizar las API de ingesta de transmisión, que forman parte de las API del servicio de ingesta de datos de Adobe Experience Platform.
exl-id: 9f7fbda9-4cd3-4db5-92ff-6598702adc34
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1567'
ht-degree: 3%

---


# Creación de [!DNL HTTP API] conexión de flujo continuo mediante la API

El servicio de flujo se utiliza para recopilar y centralizar datos de clientes de diferentes fuentes dentro de Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde las que se pueden conectar todas las fuentes admitidas.

Este tutorial utiliza la variable [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) para ayudarle a crear una conexión de flujo continuo mediante la API de servicio de flujo.

## Primeros pasos

Esta guía requiere conocer los siguientes componentes de Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)]](../../../../../xdm/home.md): El marco normalizado por el cual [!DNL Platform] organiza los datos de experiencia.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil unificado y de cliente en tiempo real basado en datos agregados de varias fuentes.

Además, la creación de una conexión de flujo continuo requiere que tenga un esquema XDM de destino y un conjunto de datos. Para aprender a crearlos, lea el tutorial sobre [datos de registro de flujo continuo](../../../../../ingestion/tutorials/streaming-record-data.md) o el tutorial en [transmisión de datos de series temporales](../../../../../ingestion/tutorials/streaming-time-series-data.md).

Las secciones siguientes proporcionan información adicional que deberá conocer para realizar llamadas correctamente a las API de ingesta de transmisión.

### Leer llamadas de API de ejemplo

Esta guía proporciona ejemplos de llamadas a la API para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) en el [!DNL Experience Platform] guía de solución de problemas.

### Recopilar valores para encabezados necesarios

Para realizar llamadas a [!DNL Platform] API, primero debe completar la variable [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todos los [!DNL Experience Platform] Llamadas de API, como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Todos los recursos de [!DNL Experience Platform], incluidas las pertenecientes a [!DNL Flow Service], están aisladas para entornos limitados virtuales específicos. Todas las solicitudes a [!DNL Platform] Las API requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados en [!DNL Platform], consulte la [documentación general de entorno limitado](../../../../../sandboxes/home.md).

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

- Content-Type: application/json

## Creación de una conexión base

Una conexión base especifica el origen y contiene la información necesaria para hacer que el flujo sea compatible con las API de ingesta de flujo continuo. Al crear una conexión base, tiene la opción de crear una conexión no autenticada y autenticada.

### Conexión no autenticada

Las conexiones no autenticadas son la conexión de flujo estándar que puede crear cuando desee transmitir datos a Platform.

**Formato de API**

```http
POST /flowservice/connections
```

**Solicitud**

Para crear una conexión de flujo continuo, el ID de proveedor y el ID de especificación de conexión deben proporcionarse como parte de la solicitud del POST. El ID del proveedor es `521eee4d-8cbe-4906-bb48-fb6bd4450033` y el ID de especificación de conexión es `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`.

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "Sample streaming connection",
     "description": "Sample description",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Sample connection",
             "dataType": "xdm",
             "name": "Sample connection"
         }
     }
 }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `auth.params.sourceId` | El ID de la conexión de flujo continuo que desea crear. |
| `auth.params.dataType` | Tipo de datos de la conexión de flujo continuo. Este valor debe ser `xdm`. |
| `auth.params.name` | Nombre de la conexión de flujo continuo que desea crear. |
| `connectionSpec.id` | Especificación de conexión `id` para conexiones de flujo continuo. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 201 con detalles de la conexión recién creada, incluido su identificador único (`id`).

```json
{
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `id` | La variable `id` de la conexión recién creada. Esto se denominará `{CONNECTION_ID}`. |
| `etag` | Identificador asignado a la conexión, que especifica la revisión de la conexión. |

### Conexión autenticada

Las conexiones autenticadas deben usarse cuando necesite diferenciar entre registros procedentes de fuentes de confianza y de las que no es de confianza. Los usuarios que deseen enviar información con Información de identificación personal (PII) deben crear una conexión autenticada al transmitir información a Platform.

**Formato de API**

```http
POST /flowservice/connections
```

**Solicitud**

Para crear una conexión de flujo continuo, el ID de proveedor y el ID de especificación de conexión deben proporcionarse como parte de la solicitud del POST. El ID del proveedor es `521eee4d-8cbe-4906-bb48-fb6bd4450033` y el ID de especificación de conexión es `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`.

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "Sample streaming connection",
     "description": "Sample description",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Sample connection",
             "dataType": "xdm",
             "name": "Sample connection",
             "authenticationRequired": true
         }
     }
 }
```


| Propiedad | Descripción |
| -------- | ----------- |
| `auth.params.sourceId` | El ID de la conexión de flujo continuo que desea crear. |
| `auth.params.dataType` | Tipo de datos de la conexión de flujo continuo. Este valor debe ser `xdm`. |
| `auth.params.name` | Nombre de la conexión de flujo continuo que desea crear. |
| `auth.params.authenticationRequired` | El parámetro que especifica que la conexión de flujo continuo creada |
| `connectionSpec.id` | Especificación de conexión `id` para conexiones de flujo continuo. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 201 con detalles de la conexión recién creada, incluido su identificador único (`id`).

```json
{
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `id` | La variable `id` de la conexión recién creada. Esto se denominará `{CONNECTION_ID}`. |
| `etag` | Identificador asignado a la conexión, que especifica la revisión de la conexión. |

## Obtener URL de extremo de flujo continuo

Con la conexión base creada, ahora puede recuperar la URL del extremo de flujo continuo.

**Formato de API**

```http
GET /flowservice/connections/{CONNECTION_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{CONNECTION_ID}` | La variable `id` de la conexión que ha creado anteriormente. |

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con información detallada sobre la conexión solicitada. La URL del extremo de flujo continuo se crea automáticamente con la conexión y se puede recuperar mediante la función `inletUrl` valor.

```json
{
    "items": [
        {
            "createdAt": 1583971856947,
            "updatedAt": 1583971856947,
            "createdBy": "{API_KEY}",
            "updatedBy": "{API_KEY}",
            "createdClient": "{USER_ID}",
            "updatedClient": "{USER_ID}",
            "id": "77a05521-91d6-451c-a055-2191d6851c34",
            "name": "Another new sample connection (Experience Event)",
            "description": "Sample description",
            "connectionSpec": {
                "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
                "version": "1.0"
            },
            "state": "enabled",
            "auth": {
                "specName": "Streaming Connection",
                "params": {
                    "sourceId": "Sample connection (ExperienceEvent)",
                    "inletUrl": "https://dcs.adobedc.net/collection/a868e1ce678a911ef1482b083329af3cafa4bafdc781285f25911eaae9e00eb2",
                    "inletId": "a868e1ce678a911ef1482b083329af3cafa4bafdc781285f25911eaae9e00eb2",
                    "dataType": "xdm",
                    "name": "Sample connection (ExperienceEvent)"
                }
            },
            "version": "\"56008aee-0000-0200-0000-5e697e150000\"",
            "etag": "\"56008aee-0000-0200-0000-5e697e150000\""
        }
    ]
}
```

## Crear una conexión de origen {#source}

Después de crear la conexión base, deberá crear una conexión de origen. Al crear una conexión de origen, necesitará la variable `id` de la conexión base creada.

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
    "name": "Sample source connection",
    "description": "Sample source connection description",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
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
    "id": "63070871-ec3f-4cb5-af47-cf7abb25e8bb",
    "etag": "\"28000b90-0000-0200-0000-6091b0150000\""
}
```

## Creación de un esquema XDM de destino {#target-schema}

Para que los datos de origen se utilicen en Platform, se debe crear un esquema de destino para estructurar los datos de origen según sus necesidades. A continuación, el esquema de destino se utiliza para crear un conjunto de datos de Platform en el que se contienen los datos de origen.

Se puede crear un esquema XDM de destino realizando una solicitud de POST al [API del Registro de esquemas](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

Para ver los pasos detallados sobre cómo crear un esquema XDM de destino, consulte el tutorial sobre [creación de un esquema con la API](../../../../../xdm/api/schemas.md).

### Creación de un conjunto de datos de destino {#target-dataset}

Se puede crear un conjunto de datos de destino realizando una solicitud de POST al [API del servicio de catálogo](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml), que proporciona el ID del esquema de destino dentro de la carga útil.

Para ver los pasos detallados sobre cómo crear un conjunto de datos de destinatario, consulte el tutorial en [creación de un conjunto de datos mediante la API](../../../../../catalog/api/create-dataset.md).

## Creación de una conexión de destino {#target}

Una conexión de destino representa la conexión con el destino en el que llegan los datos introducidos. Para crear una conexión de destino, debe proporcionar el ID de especificación de conexión fija asociado al lago de datos. Este ID de especificación de conexión es: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Ahora tiene los identificadores únicos, un esquema de destino, un conjunto de datos de destino y el ID de especificación de conexión al lago de datos. Con estos identificadores, puede crear una conexión de destino utilizando la variable [!DNL Flow Service] API para especificar el conjunto de datos que contendrá los datos de origen entrantes.

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
    "name": "Sample target connection",
    "description": "Sample target connection description",
    "connectionSpec": {
        "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
        "version": "1.0"
    },
    "data": {
        "format": "parquet_xdm"
    },
    "params": {
        "dataSetId": "{DATASET_ID}"
    }
}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 201 con detalles de la conexión de destino recién creada, incluido su identificador único (`id`).

```json
{
    "id": "98a2a72e-a80f-49ae-aaa3-4783cc9404c2",
    "etag": "\"0500b73f-0000-0200-0000-6091b0b90000\""
}
```

## Creación de una asignación {#mapping}

Para que los datos de origen se introduzcan en un conjunto de datos de destino, primero deben asignarse al esquema de destino al que se adhiera el conjunto de datos de destino.

Para crear un conjunto de asignaciones, realice una solicitud de POST al `mappingSets` punto final del [[!DNL Data Prep] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-prep.yaml) al proporcionar el esquema XDM de destino `$id` y los detalles de los conjuntos de asignación que desea crear.

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
        "xdmSchema": "_{TENANT_ID}.schemas.e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
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
| `xdmSchema` | La variable `$id` del esquema XDM de destino. |

**Respuesta**

Una respuesta correcta devuelve detalles de la asignación recién creada, incluido su identificador único (`id`). Este ID es necesario en un paso posterior para crear un flujo de datos.

```json
{
    "id": "380b032b445a46008e77585e046efe5e",
    "version": 0,
    "createdDate": 1604960750613,
    "modifiedDate": 1604960750613,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## Crear un flujo de datos

Con las conexiones de origen y destino creadas, ahora puede crear un flujo de datos. El flujo de datos es responsable de programar y recopilar datos de un origen. Puede crear un flujo de datos realizando una solicitud de POST al `/flows` punto final.

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
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "HTTP API streaming dataflow",
        "description": "HTTP API streaming dataflow",
        "flowSpec": {
            "id": "c1a19761-d2c7-4702-b9fa-fe91f0613e81",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "63070871-ec3f-4cb5-af47-cf7abb25e8bb"
        ],
        "targetConnectionIds": [
            "98a2a72e-a80f-49ae-aaa3-4783cc9404c2"
        ],
        "transformations": [
            {
            "name": "Mapping",
            "params": {
                "mappingId": "380b032b445a46008e77585e046efe5e",
                "mappingVersion": 0
            }
            }
        ]
    }'
```

| Propiedad | Descripción |
| --- | --- |
| `flowSpec.id` | El ID de especificación de flujo para [!DNL HTTP API]. Este ID es: `c1a19761-d2c7-4702-b9fa-fe91f0613e81`. |
| `sourceConnectionIds` | La variable [ID de conexión de origen](#source) recuperado en un paso anterior. |
| `targetConnectionIds` | La variable [ID de conexión de target](#target) recuperado en un paso anterior. |
| `transformations.params.mappingId` | La variable [ID de asignación](#mapping) recuperado en un paso anterior. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 201 con detalles del flujo de datos recién creado, incluido su identificador único (`id`).

```json
{
    "id": "ab03bde0-86f2-45c7-b6a5-ad8374f7db1f",
    "etag": "\"1200c123-0000-0200-0000-6091b1730000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión HTTP de flujo continuo, que le permite utilizar el extremo de flujo continuo para introducir datos en Platform. Para obtener instrucciones para crear una conexión de flujo continuo en la interfaz de usuario, lea la [creación de un tutorial de conexión de flujo continuo](../../../ui/create/streaming/http.md).

Para aprender a transmitir datos a Platform, lea cualquiera de los tutoriales sobre [transmisión de datos de series temporales](../../../../../ingestion/tutorials/streaming-time-series-data.md) o el tutorial en [datos de registro de flujo continuo](../../../../../ingestion/tutorials/streaming-record-data.md).

## Apéndice

Esta sección proporciona información complementaria sobre la creación de conexiones de flujo continuo mediante la API.

### Envío de mensajes a una conexión de flujo continuo autenticada

Si una conexión de flujo continuo tiene habilitada la autenticación, el cliente deberá agregar la variable `Authorization` a su solicitud.

Si la variable `Authorization` no está presente o se envía un token de acceso no válido/caducado, se devolverá una respuesta HTTP 401 no autorizada, con una respuesta similar a la que se muestra a continuación:

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

### Publicar datos sin procesar para ingerirlos en Platform {#ingest-data}

Ahora que ha creado su flujo, puede enviar su mensaje JSON al extremo de flujo que creó anteriormente.

**Formato de API**

```http
POST /collection/{CONNECTION_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{CONNECTION_ID}` | La variable `id` de la conexión de flujo continuo recién creada. |

**Solicitud**

La solicitud de ejemplo ingesta datos sin procesar en el extremo de flujo que se creó anteriormente.

```shell
curl -X POST https://dcs.adobedc.net/collection/2301a1f761f6d7bf62c5312c535e1076bbc7f14d728e63cdfd37ecbb4344425b \
  -H 'Content-Type: application/json' \
  -H 'x-adobe-flow-id: 1f086c23-2ea8-4d06-886c-232ea8bd061d' \
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

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la información recién ingerida.

```json
{
    "inletId": "{CONNECTION_ID}",
    "xactionId": "1584479347507:2153:240",
    "receivedTimeMs": 1584479347507
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{CONNECTION_ID}` | El ID de la conexión de flujo continuo creada anteriormente. |
| `xactionId` | Identificador único generado en el servidor para el registro que acaba de enviar. Este ID ayuda a los Adobes a rastrear el ciclo vital de este registro a través de varios sistemas y con depuración. |
| `receivedTimeMs` | Marca de tiempo (época en milisegundos) que muestra la hora a la que se recibió la solicitud. |
