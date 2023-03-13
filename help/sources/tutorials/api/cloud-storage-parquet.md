---
keywords: Experience Platform;inicio;temas populares;conexión de origen de datos
solution: Experience Platform
title: Ingesta de datos de Parquet desde un sistema de almacenamiento en la nube de terceros mediante la API de Flow Service
type: Tutorial
description: Este tutorial utiliza la API de Flow Service para guiarle por los pasos para introducir datos de Apache Parquet desde un sistema de almacenamiento en la nube de terceros.
exl-id: fb1b19d6-16bb-4a5f-9e81-f537bac95041
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1095'
ht-degree: 3%

---

# Ingesta de datos de Parquet desde un sistema de almacenamiento en la nube de terceros mediante el [!DNL Flow Service] API

[!DNL Flow Service] se utiliza para recopilar y centralizar datos de clientes de varias fuentes diferentes dentro de Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde las que se pueden conectar todas las fuentes de datos admitidas.

Este tutorial utiliza el [!DNL Flow Service] API para guiarle por los pasos para ingerir datos de Parquet de un sistema de almacenamiento en la nube de terceros.

## Primeros pasos

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

- [Fuentes](../../home.md): [!DNL Experience Platform] permite la ingesta de datos desde varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
- [Zonas protegidas](../../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para ingerir correctamente datos de Parquet de un almacenamiento en la nube de terceros mediante [!DNL Flow Service] API.

### Leer llamadas de API de muestra

Este tutorial proporciona llamadas de API de ejemplo para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) en el [!DNL Experience Platform] guía de solución de problemas.

### Recopilar valores para los encabezados obligatorios

Para realizar llamadas a [!DNL Platform] API, primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todas las [!DNL Experience Platform] Llamadas de API, como se muestra a continuación:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

Todos los recursos de [!DNL Experience Platform], incluidos los pertenecientes a [!DNL Flow Service], están aisladas para zonas protegidas virtuales específicas. Todas las solicitudes a [!DNL Platform] Las API requieren un encabezado que especifique el nombre de la zona protegida en la que se realizará la operación:

- `x-sandbox-name: {SANDBOX_NAME}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medios adicional:

- `Content-Type: application/json`

## Crear una conexión

Para introducir datos de Parquet utilizando [!DNL Platform] Las API requieren que posea una conexión válida para el origen de almacenamiento en la nube de terceros al que acceda. Si todavía no dispone de una conexión para el almacenamiento con el que desea trabajar, puede crearla mediante los siguientes tutoriales:

- [Amazon S3](./create/cloud-storage/s3.md)
- [Azure Blob](./create/cloud-storage/blob.md)
- [Azure Data Lake Storage Gen2](./create/cloud-storage/adls-gen2.md)
- [Tienda de Google Cloud](./create/cloud-storage/google.md)
- [SFTP](./create/cloud-storage/sftp.md)

Obtenga y almacene el identificador único (`$id`) de la conexión y continúe con el siguiente paso de este tutorial.

## Creación de un esquema de destino

Para que los datos de origen se utilicen en [!DNL Platform], también se debe crear un esquema de destino para estructurar los datos de origen según sus necesidades. A continuación, se utiliza el esquema de destino para crear una [!DNL Platform] conjunto de datos en el que se incluyen los datos de origen.

Si prefiere usar la interfaz de usuario de en [!DNL Experience Platform], el [Tutorial del Editor de esquemas](../../../xdm/tutorials/create-schema-ui.md) proporciona instrucciones paso a paso para realizar acciones similares en el Editor de esquemas.

**Formato de API**

```http
POST /schemaregistry/tenant/schemas
```

**Solicitud**

La siguiente solicitud de ejemplo crea un esquema XDM que amplía el XDM [!DNL Individual Profile] clase.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
    "type": "object",
    "title": "Sample Demo Profile XDM {{$guid}}",
    "description": "",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-work-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-subscriptions"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/identitymap"
        }
    ],
    "meta:containerId": "tenant",
    "meta:resourceType": "schemas",
    "meta:xdmType": "object",
    "meta:class": "https://ns.adobe.com/xdm/context/profile"
}'
```

**Respuesta**

Una respuesta correcta devuelve detalles del esquema recién creado, incluido su identificador único (`$id`). Este ID es necesario en el siguiente paso para crear una conexión de origen.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/e15530faf88aeb52d9ca5c5671a059f44f1a42ea7f5fdb80",
    "meta:altId": "_{TENANT_ID}.schemas.e15530faf88aeb52d9ca5c5671a059f44f1a42ea7f5fdb80",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Sample Demo Profile XDM 8d96a964-aad8-43c5-a73a-c8b9b1ccbfb1",
    "type": "object",
    "description": "",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-work-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-subscriptions",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/identitymap",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/context/profile-subscriptions",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/context/profile-work-details"
    ],
    "imsOrg": "{ORG_ID}",
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/context/profile-subscriptions",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/context/profile-work-details"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1584673864341,
        "repo:lastModifiedDate": 1584673864341,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{MODIFIED_USER_ID}",
        "eTag": "fa704f80da907c8f0f66f453ffcac3e52958687edbf55d71231dc5e1522193c4"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Crear una conexión de origen {#source}

Con un esquema XDM de destino creado, ahora se puede crear una conexión de origen mediante una solicitud del POST a [!DNL Flow Service] API. Una conexión de origen consiste en una conexión para la API, un formato de datos de origen y una referencia al esquema XDM de destino recuperado en el paso anterior.

**Formato de API**

```http
POST /sourceConnections
```

**Solicitud**

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Source Connection S3 {{$guid}}",
        "baseConnectionId": "5831c52c-c261-4945-b1c5-2cc261d945b2",
        "connectionSpec": {
            "id": "ecadc60c-7455-4d87-84dc-2a0e293d997b",
            "version": 1
        },
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/e15530faf88aeb52d9ca5c5671a059f44f1a42ea7f5fdb80",
                "id": "",
                "version": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "params": {
            "path": "partners-demo/samples",
            "recursive": "true"
        }
    }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `baseConnectionId` | La conexión para la API que representa su almacenamiento en la nube. |
| `data.schema.id` | El (`$id`) si el esquema xdm de destino recuperado en el paso anterior. |
| `params.path` | Ruta del archivo de origen. |

**Respuesta**

Una respuesta correcta devuelve el identificador único (`id`) de la conexión de origen recién creada. Almacene este valor tal como se requiere en pasos posteriores para crear una conexión de destino.

```json
{
    "id": "73bc8911-505a-4e46-bc89-11505a6e466f",
    "etag": "\"c4004435-0000-0200-0000-5e7437d90000\""
}
```

## Crear una conexión base de conjunto de datos

Para introducir datos externos en [!DNL Platform], un [!DNL Experience Platform] primero se debe adquirir la conexión base del conjunto de datos.

Para crear una conexión base del conjunto de datos, siga los pasos descritos en la sección [tutorial de conexión base del conjunto de datos](./create-dataset-base-connection.md).

Siga los pasos descritos en la guía para desarrolladores hasta que haya creado una conexión base de conjunto de datos. Obtenga y almacene el identificador único (`$id`) y continúe usándolo como ID de conexión base en el siguiente paso para crear una conexión de destino.

## Crear un conjunto de datos de destinatario

Se puede crear un conjunto de datos de destino realizando una solicitud de POST al [API del servicio de catálogo](https://www.adobe.io/experience-platform-apis/references/catalog/), proporcionando el ID del esquema de destinatario dentro de la carga útil.

**Formato de API**

```http
POST /catalog/dataSets
```

**Solicitud**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/catalog/dataSets?requestDataSource=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Leads Dataset {{$guid}}",
        "schemaRef": {
            "id": ""https://ns.adobe.com/{TENANT_ID}/schemas/e15530faf88aeb52d9ca5c5671a059f44f1a42ea7f5fdb80"",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        }
    }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `schemaRef.id` | El ID del esquema XDM de destino. |

**Respuesta**

Una respuesta correcta devuelve una matriz que contiene el ID del conjunto de datos recién creado con el formato `"@/datasets/{DATASET_ID}"`. El ID del conjunto de datos es una cadena generada por el sistema de solo lectura que se utiliza para hacer referencia al conjunto de datos en las llamadas a la API. Almacene el ID del conjunto de datos de destino tal como se requiere en pasos posteriores para crear una conexión de destino y un flujo de datos.

```json
[
    "@/dataSets/5e7439b1ad55a618ad4c5102"
]
```

## Creación de una conexión de destino {#target}

Ahora tiene los identificadores únicos para una conexión base de conjunto de datos, un esquema de destino y un conjunto de datos de destino. Con estos identificadores, puede crear una conexión de destino con el [!DNL Flow Service] API para especificar el conjunto de datos que contendrá los datos de origen entrantes.

**Formato de API**

```http
POST /targetConnections
```

**Solicitud**

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "baseConnectionId": "291257e3-c560-4e07-9257-e3c5606e07d1",
        "connectionSpec": {
            "id":"c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        },
        "name": "Target Connection {{$guid}}",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": ""https://ns.adobe.com/{TENANT_ID}/schemas/e15530faf88aeb52d9ca5c5671a059f44f1a42ea7f5fdb80"",
                "version": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "params": {
            "dataSetId": "5e7439b1ad55a618ad4c5102"
        }
    }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `baseConnectionId` | El ID de la conexión base del conjunto de datos. |
| `data.schema.id` | El `$id` del esquema XDM de destino. |
| `params.dataSetId` | El ID del conjunto de datos de destinatario. |
| `connectionSpec.id` | ID de especificación de conexión para su almacenamiento en la nube. |

**Respuesta**

Una respuesta correcta devuelve el identificador único ( ) de la nueva conexión de destino`id`). Almacene este valor tal como se requiere en pasos posteriores.

```json
{
    "id": "9b3abc95-f2e9-47c1-babc-95f2e927c1ec",
    "etag": "\"7501936b-0000-0200-0000-5e743bcc0000\""
}
```

## Creación de un flujo de datos

El último paso para la ingesta de datos de Parquet desde un almacenamiento en la nube de terceros es crear un flujo de datos. Por ahora, tiene preparados los siguientes valores obligatorios:

- [ID de conexión de origen](#source)
- [ID de conexión de destino](#target)

Un flujo de datos es responsable de programar y recopilar datos de una fuente. Puede crear un flujo de datos realizando una solicitud de POST mientras proporciona los valores mencionados anteriormente dentro de la carga útil.

**Formato de API**

```http
POST /flows
```

**Solicitud**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Demo Parquet Ingestion Flow {{$guid}}",
        "flowSpec": {
            "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "73bc8911-505a-4e46-bc89-11505a6e466f"
        ],
        "targetConnectionIds": [
            "9b3abc95-f2e9-47c1-babc-95f2e927c1ec"
        ],
        "scheduleParams": {
            "startTime": {{$timestamp}},
            "frequency": "minute",
            "interval": 1000,
            "backfill": true
        }
    }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `sourceConnectionIds` | Identificador de conexión de origen recuperado en un paso anterior. |
| `targetConnectionIds` | El ID de conexión de destino recuperado en un paso anterior. |

**Respuesta**

Una respuesta correcta devuelve el ID (`id`) del flujo de datos recién creado.

```json
{
    "id": "89ff50ef-b082-426e-bf50-efb082d26e78",
    "etag": "\"890070b8-0000-0200-0000-5e743c040000\""
}
```

## Pasos siguientes

Al seguir este tutorial, ha creado un conector de origen para recopilar datos de Parquet de su sistema de almacenamiento en la nube de terceros de forma programada. Ahora, los datos entrantes pueden utilizarse en el flujo descendente [!DNL Platform] servicios como [!DNL Real-Time Customer Profile] y [!DNL Data Science Workspace]. Consulte los siguientes documentos para obtener más información:

- [Resumen del perfil del cliente en tiempo real](../../../profile/home.md)
- [Resumen de Data Science Workspace](../../../data-science-workspace/home.md)
