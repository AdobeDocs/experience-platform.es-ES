---
keywords: Experience Platform;inicio;temas populares;conjunto de datos;Conjunto de datos;crear un conjunto de datos;crear conjunto de datos
solution: Experience Platform
title: Crear un conjunto de datos mediante API
description: Este documento proporciona pasos generales para crear un conjunto de datos mediante las API de Adobe Experience Platform y rellenar el conjunto de datos con un archivo.
exl-id: 3a5f48cf-ad05-4b9e-be1d-ff213a26a477
source-git-commit: e2f16f532b98e6948ffd7f331e630137b3972f0f
workflow-type: tm+mt
source-wordcount: '1302'
ht-degree: 7%

---

# Creación de un conjunto de datos mediante API

Este documento proporciona pasos generales para crear un conjunto de datos mediante las API de Adobe Experience Platform y rellenar el conjunto de datos con un archivo.

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Ingesta por lotes](../../ingestion/batch-ingestion/overview.md): [!DNL Experience Platform] le permite ingerir datos como archivos por lotes.
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola instancia de [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que necesitará conocer para realizar llamadas correctamente a las API de [!DNL Platform].

### Lectura de llamadas de API de muestra

Este tutorial proporciona llamadas de API de ejemplo para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de la API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de ejemplo, consulte la sección sobre [cómo leer las llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas de [!DNL Experience Platform].

### Recopilación de valores para los encabezados obligatorios

Para poder realizar llamadas a las API de [!DNL Platform], primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados obligatorios en todas las llamadas de API de [!DNL Experience Platform], como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todos los recursos de [!DNL Experience Platform] están aislados en zonas protegidas virtuales específicas. Todas las solicitudes a las API de [!DNL Platform] requieren un encabezado que especifique el nombre de la zona protegida en la que se realizará la operación:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre las zonas protegidas en [!DNL Platform], consulte la [documentación de información general sobre las zonas protegidas](../../sandboxes/home.md).

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado `Content-Type: application/json` adicional. Para solicitudes JSON+PATCH, `Content-Type` debe ser `application/json-patch+json`.

## Tutorial

Para crear un conjunto de datos, primero debe definirse un esquema. Un esquema es un conjunto de reglas que ayudan a representar los datos. Además de describir la estructura de los datos, los esquemas proporcionan restricciones y expectativas que se pueden aplicar y utilizar para validar los datos a medida que se mueven entre sistemas.

Estas definiciones estándar permiten que los datos se interpreten de forma coherente, independientemente del origen, y eliminan la necesidad de traducción entre aplicaciones. Para obtener más información acerca de la composición de esquemas, consulte la guía sobre los [conceptos básicos de la composición de esquemas](../../xdm/schema/composition.md)

## Búsqueda de un esquema de conjunto de datos

Este tutorial comienza donde termina el [tutorial de API del Registro de esquemas](../../xdm/tutorials/create-schema-api.md), utilizando el esquema Miembros de fidelización creado durante ese tutorial.

Si no ha completado el tutorial [!DNL Schema Registry], comience allí y continúe con este tutorial del conjunto de datos solo una vez que haya compuesto el esquema necesario.

La siguiente llamada se puede utilizar para ver el esquema de miembros socio que creó durante el tutorial de API [!DNL Schema Registry]:

**Formato de API**

```HTTP
GET /tenant/schemas/{schema meta:altId or URL encoded $id URI}
```

**Solicitud**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

El formato del objeto response depende del encabezado Accept que se envíe en la solicitud. Las propiedades individuales de esta respuesta se han minimizado para el espacio.

```JSON
{
    "type": "object",
    "title": "Loyalty Members",
    "description": "Information for all members of the loyalty program",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/{TENANT_ID}/mixins/bb118e507bb848fd85df68fedea70c62"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:immutableTags": [
        "union"
    ],
    "meta:altId": "_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9",
    "meta:xdmType": "object",
    "properties": {
        "repositoryCreatedBy": {},
        "repositoryLastModifiedBy": {},
        "createdByBatchID": {},
        "modifiedByBatchID": {},
        "_repo": {},
        "identityMap": {},
        "_id": {},
        "timeSeriesEvents": {},
        "person": {},
        "homeAddress": {},
        "personalEmail": {},
        "homePhone": {},
        "mobilePhone": {},
        "faxPhone": {},
        "_{TENANT_ID}": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "loyalty": {
                    "title": "Loyalty",
                    "description": "Loyalty Info",
                    "type": "object",
                    "meta:xdmType": "object",
                    "meta:referencedFrom": "https://ns.adobe.com/{TENANT_ID}/datatypes/49b594dabe6bec545c8a6d1a0991a4dd",
                    "properties": {
                        "loyaltyId": {
                            "title": "Loyalty Identifier",
                            "type": "string",
                            "description": "Loyalty Identifier.",
                            "meta:xdmType": "string"
                        },
                        "loyaltyLevel": {
                            "title": "Loyalty Level",
                            "type": "string",
                            "meta:xdmType": "string"
                        },
                        "loyaltyPoints": {
                            "title": "Loyalty Points",
                            "type": "integer",
                            "description": "Loyalty points total.",
                            "meta:xdmType": "int"
                        },
                        "memberSince": {
                            "title": "Member Since",
                            "type": "string",
                            "format": "date-time",
                            "description": "Date the member joined the Loyalty Program.",
                            "meta:xdmType": "date-time"
                        }
                    }
                }
            }
        }
    },
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "version": "1.4",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1551836845496,
        "repo:lastModifiedDate": 1551843052271,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

## Crear un conjunto de datos

Con el esquema Miembros socio, ahora puede crear un conjunto de datos que haga referencia al esquema.

**Formato de API**

```HTTP
POST /dataSets
```

**Solicitud**

```SHELL
curl -X POST \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?requestDataSource=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name":"LoyaltyMembersDataset",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/719c4e19184402c27595e65b931a142b",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    }
}'
```

| Propiedad | Descripción |
| --- | --- |
| `schemaRef.id` | Valor de URI `$id` para el esquema XDM en el que se basará el conjunto de datos. |
| `schemaRef.contentType` | Indica el formato y la versión del esquema. Consulte la sección sobre [versiones de esquema](../../xdm/api/getting-started.md#versioning) en la guía de API de XDM para obtener más información. |

>[!NOTE]
>
>Este tutorial usa el formato de archivo [Apache Parquet](https://parquet.apache.org/docs/) para todos sus ejemplos. Encontrará un ejemplo que utiliza el formato de archivo JSON en la [guía para desarrolladores de ingesta por lotes](../../ingestion/batch-ingestion/api-overview.md)

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 201 (Creado) y un objeto de respuesta que consta de una matriz que contiene el ID del conjunto de datos recién creado con el formato `"@/datasets/{DATASET_ID}"`. El ID del conjunto de datos es una cadena generada por el sistema de solo lectura que se utiliza para hacer referencia al conjunto de datos en las llamadas a la API.

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```

## Crear un lote

Para poder agregar datos a un conjunto de datos, debe crear un lote vinculado al conjunto de datos. El lote se utilizará para la carga.

**Formato de API**

```HTTP
POST /batches
```

**Solicitud**

El cuerpo de la solicitud incluye un campo &quot;datasetId&quot;, cuyo valor es el `{DATASET_ID}` generado en el paso anterior.

```SHELL
curl -X POST 'https://platform.adobe.io/data/foundation/import/batches' \
  -H 'accept: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'content-type: application/json' \
  -d '{
        "datasetId":"5c8c3c555033b814b69f947f"
      }'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 201 (Creado) y un objeto de respuesta. El objeto response consiste en una matriz que contiene el identificador del lote recién creado con el formato `"@/batches/{BATCH_ID}"`. El ID de lote es una cadena generada por el sistema de solo lectura que se utiliza para hacer referencia al lote en las llamadas API.

```JSON
{
    "id": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "imsOrg": "{ORG_ID}",
    "updated": 1552694873602,
    "status": "loading",
    "created": 1552694873602,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "5c8c3c555033b814b69f947f"
        }
    ],
    "version": "1.0.0",
    "tags": {
        "acp_producer": [
            "{CREATED_CLIENT}"
        ],
        "acp_stagePath": [
            "{CREATED_CLIENT}/stage/5d01230fc78a4e4f8c0c6b387b4b8d1c"
        ],
        "use_plan_b_batch_status": [
            "false"
        ]
    },
    "createdUser": "{CREATED_BY}",
    "updatedUser": "{CREATED_BY}",
    "externalId": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "createdClient": "{CREATED_CLIENT}",
    "inputFormat": {
        "format": "parquet"
    }
}
```

## Cargar archivos en un lote

Después de crear correctamente un nuevo lote para cargar, ahora puede cargar archivos en el conjunto de datos específico. Es importante recordar que, al definir el conjunto de datos, especificó el formato de archivo como Parquet. Por lo tanto, los archivos que cargue deben tener ese formato.

>[!NOTE]
>
>El archivo de carga de datos más grande admitido es de 512 MB. Si el archivo de datos es más grande que este, debe dividirse en fragmentos que no superen los 512 MB para cargarse de uno en uno. Puede cargar cada archivo en el mismo lote repitiendo este paso para cada archivo, utilizando el mismo ID de lote. No hay límite en el número de archivos que se pueden cargar como parte de un lote.

**Formato de API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parámetro | Descripción |
| --- | --- |
| `{BATCH_ID}` | El `id` del lote que está cargando. |
| `{DATASET_ID}` | El `id` del conjunto de datos en el que se mantendrá el lote. |
| `{FILE_NAME}` | Nombre del archivo que está cargando. |

**Solicitud**

```SHELL
curl -X PUT 'https://platform.adobe.io/data/foundation/import/batches/5d01230fc78a4e4f8c0c6b387b4b8d1c/datasets/5c8c3c555033b814b69f947f/files/loyaltyData.parquet' \
  -H 'content-type: application/octet-stream' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  --data-binary '@{FILE_PATH_AND_NAME}.parquet'
```

**Respuesta**

Un archivo cargado correctamente devuelve un cuerpo de respuesta en blanco y el estado HTTP 200 (OK).

## Finalización de lote de señal

Después de cargar todos los archivos de datos en el lote, puede indicar al lote que finalice. La finalización de la señal hace que el servicio cree [!DNL Catalog] `DataSetFile` entradas para los archivos cargados y las asocie al lote generado anteriormente. El lote [!DNL Catalog] se ha marcado correctamente, lo cual déclencheur cualquier flujo descendente que pueda funcionar con los datos ahora disponibles.

**Formato de API**

```HTTP
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Parámetro | Descripción |
| --- | --- |
| `{BATCH_ID}` | El `id` del lote que está marcando como completado. |

**Solicitud**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/5d01230fc78a4e4f8c0c6b387b4b8d1c?action=COMPLETE" \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**Respuesta**

Un lote completado correctamente devuelve un cuerpo de respuesta en blanco y el estado HTTP 200 (OK).

## Monitorización de la ingesta

Según el tamaño de los datos, los lotes tardan distintos periodos en ingerirse. Puede monitorizar el estado de un lote adjuntando el ID de un lote a una solicitud `GET /batches`.

**Formato de API**

```HTTP
GET /batches/{BATCH_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{BATCH_ID}` | El `id` del lote que desea supervisar. |

**Solicitud**

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/batches?batch=5d01230fc78a4e4f8c0c6b387b4b8d1c' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**Respuesta**

Una respuesta positiva devuelve un objeto con su atributo `status` que contiene el valor de `success`:

```JSON
{
    "5b7129a879323401ef2a6486": {
        "imsOrg": "{ORG_ID}",
        "created": 1534142888068,
        "createdClient": "{CREATED_CLIENT}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1534142955152,
        "replay": {},
        "status": "success",
        "errors": [],
        "version": "1.0.3",
        "availableDates": {},
        "relatedObjects": [
            {
                "type": "batch",
                "id": "29285e08378f4a41827e7e70fb7cb8f0"
            }
        ],
        "metrics": {
            "startTime": 1534142943819,
            "endTime": 1534142951760,
            "recordsRead": 108,
            "recordsWritten": 108
        }
    }
}
```

Una respuesta negativa devuelve un objeto con el valor `"failed"` en su atributo `"status"` e incluye todos los mensajes de error relevantes:

```JSON
{
    "5b96ce65badcf701e51f075d": {
        "imsOrg": "{ORG_ID}",
        "status": "failed",
        "relatedObjects": [
            {
                "type": "batch",
                "id": "29285e08378f4a41827e7e70fb7cb8f0"
            }
        ],
        "replay": {},
        "availableDates": {},
        "metrics": {
            "startTime": 1536610322329,
            "endTime": 1536610438083,
            "recordsRead": 4004,
            "recordsWritten": 4004,
            "failureReason": "Job aborted due to stage failure: Task 0 in stage 1.0 failed 4 times,:"
        },
        "errors": [
            {
                "code": "0070000017",
                "description": "Unknown error occurred."
            },
            {
                "code": "unknown",
                "description": "Job aborted."
            }
        ],
        "created": 1536609893629,
        "createdClient": "{CREATED_CLIENT}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1536610442814,
        "version": "1.0.5"
    }
}
```

>[!NOTE]
>
>Un intervalo de sondeo recomendado es de dos minutos.

## Leer datos del conjunto de datos

Con el ID de lote, puede utilizar la API de acceso a datos para leer y comprobar todos los archivos cargados en el lote. La respuesta devuelve una matriz que contiene una lista de ID de archivo, cada uno de los cuales hace referencia a un archivo del lote.

También puede utilizar la API de acceso a datos para devolver el nombre, el tamaño en bytes y un vínculo para descargar el archivo o la carpeta.

Encontrará los pasos detallados para trabajar con la API de acceso a datos en la [Guía para desarrolladores de acceso a datos](../../data-access/home.md).

## Actualizar el esquema del conjunto de datos

Puede agregar campos e introducir datos adicionales en conjuntos de datos que ha creado. Para ello, primero debe actualizar el esquema añadiendo propiedades adicionales que definan los nuevos datos. Esto se puede hacer utilizando operaciones de PATCH o PUT para actualizar el esquema existente.

Para obtener más información sobre la actualización de esquemas, consulte [Schema Registry API Developer Guide](../../xdm/api/getting-started.md).

Una vez actualizado el esquema, puede volver a seguir los pasos de este tutorial para introducir nuevos datos que se ajusten al esquema revisado.

Es importante recordar que la evolución del esquema es puramente aditiva, lo que significa que no puede introducir un cambio radical en un esquema una vez que se ha guardado en el Registro y se ha utilizado para la ingesta de datos. Para obtener más información acerca de las prácticas recomendadas para crear esquemas para usarlos con Adobe Experience Platform, consulte la guía sobre los [conceptos básicos de la composición de esquemas](../../xdm/schema/composition.md).
