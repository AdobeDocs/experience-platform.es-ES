---
keywords: Experience Platform;inicio;temas populares;conjunto de datos;Conjunto de datos;crear un conjunto de datos;crear conjunto de datos
solution: Experience Platform
title: Creación de un conjunto de datos mediante API
topic: datasets
description: Este documento proporciona pasos generales para crear un conjunto de datos con las API de Adobe Experience Platform y rellenar el conjunto de datos con un archivo.
translation-type: tm+mt
source-git-commit: 2940f030aa21d70cceeedc7806a148695f68739e
workflow-type: tm+mt
source-wordcount: '1268'
ht-degree: 1%

---


# Creación de un conjunto de datos mediante API

Este documento proporciona pasos generales para crear un conjunto de datos con las API de Adobe Experience Platform y rellenar el conjunto de datos con un archivo.

## Primeros pasos

Esta guía requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

* [Ingesta](../../ingestion/batch-ingestion/overview.md) por lotes:  [!DNL Experience Platform] permite ingestar datos como archivos por lotes.
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):: Marco normalizado por el cual se  [!DNL Experience Platform] organizan los datos de experiencia del cliente.
* [[!DNL Sandboxes]](../../sandboxes/home.md)::  [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola  [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las siguientes secciones proporcionan información adicional que deberá conocer para realizar llamadas exitosas a las API [!DNL Platform].

### Leer llamadas de API de muestra

Este tutorial proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener más información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas [!DNL Experience Platform].

### Recopilar valores para encabezados necesarios

Para realizar llamadas a [!DNL Platform] API, primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas [!DNL Experience Platform] API, como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos los recursos de [!DNL Experience Platform] están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API [!DNL Platform] requieren un encabezado que especifique el nombre del entorno limitado en el que se realizará la operación:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados en [!DNL Platform], consulte la [documentación general del entorno limitado](../../sandboxes/home.md).

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

* Content-Type: application/json

## Tutorial

Para crear un conjunto de datos, primero se debe definir un esquema. Un esquema es un conjunto de reglas que ayudan a representar los datos. Además de describir la estructura de los datos, los esquemas proporcionan restricciones y expectativas que se pueden aplicar y utilizar para validar los datos a medida que se mueven entre sistemas.

Estas definiciones estándar permiten interpretar los datos de manera coherente, independientemente del origen, y eliminan la necesidad de traducirlos entre las aplicaciones. Para obtener más información sobre la composición de esquemas, consulte la guía sobre los [conceptos básicos de la composición de esquemas](../../xdm/schema/composition.md)

## Buscar un esquema de conjunto de datos

Este tutorial comienza donde termina el [tutorial de API del Registro de Esquema](../../xdm/tutorials/create-schema-api.md), haciendo uso del esquema Miembros de lealtad creado durante ese tutorial.

Si no ha completado el tutorial [!DNL Schema Registry], inicio aquí y continúe con este tutorial de conjunto de datos sólo una vez que haya redactado el esquema necesario.

Se puede utilizar la siguiente llamada para vista del esquema Miembros de lealtad que creó durante el tutorial de API [!DNL Schema Registry]:

**Formato API**

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

El formato del objeto response depende del encabezado Accept enviado en la solicitud. Las propiedades individuales de esta respuesta se han minimizado para el espacio.

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
    "imsOrg": "{IMS_ORG}",
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

Con el esquema Miembros de lealtad en su lugar, ahora puede crear un conjunto de datos que haga referencia al esquema.

**Formato API**

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name":"LoyaltyMembersDataset",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/719c4e19184402c27595e65b931a142b",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    },
    "fileDescription": {
        "persisted": true,
        "containerFormat": "parquet",
        "format": "parquet"
    }
}'
```

>[!NOTE]
>
>Este tutorial utiliza el formato de archivo [Apache Parquet](https://parquet.apache.org/documentation/latest/) para todos sus ejemplos. Encontrará un ejemplo que utiliza el formato de archivo JSON en la [guía para desarrolladores de ingestión por lotes](../../ingestion/batch-ingestion/api-overview.md)

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 201 (Creado) y un objeto de respuesta que consta de una matriz que contiene el ID del conjunto de datos recién creado con el formato `"@/datasets/{DATASET_ID}"`. El ID del conjunto de datos es una cadena de sólo lectura generada por el sistema que se utiliza para hacer referencia al conjunto de datos en las llamadas de API.

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```

## Crear un lote

Para poder agregar datos a un conjunto de datos, debe crear un lote vinculado al conjunto de datos. El lote se utilizará para la carga.

**Formato API**

```HTTP
POST /batches
```

**Solicitud**

El cuerpo de la solicitud incluye un campo &quot;datasetId&quot;, cuyo valor es el `{DATASET_ID}` generado en el paso anterior.

```SHELL
curl -X POST 'https://platform.adobe.io/data/foundation/import/batches' \
  -H 'accept: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'content-type: application/json' \
  -d '{
        "datasetId":"5c8c3c555033b814b69f947f"
      }'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 201 (Creado) y un objeto de respuesta que contiene detalles del lote recién creado, incluida su `id`, una cadena de sólo lectura generada por el sistema.

```JSON
{
    "id": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "imsOrg": "{IMS_ORG}",
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

## Carga de archivos en un lote

Después de crear correctamente un nuevo lote para la carga, ahora puede cargar archivos en el conjunto de datos específico. Es importante recordar que cuando definió el conjunto de datos, especificó el formato de archivo como Parquet. Por lo tanto, los archivos que cargue deben tener ese formato.

>[!NOTE]
>
>El archivo de carga de datos más grande admitido es de 512 MB. Si el archivo de datos es más grande que este, debe dividirse en fragmentos de no más de 512 MB, que se cargarán de uno en uno. Puede cargar cada archivo del mismo lote repitiendo este paso para cada archivo, utilizando el mismo ID de lote. No hay límite en el número si se pueden cargar archivos como parte de un lote.

**Formato API**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Parámetro | Descripción |
| --- | --- |
| `{BATCH_ID}` | El `id` del lote al que está cargando. |
| `{DATASET_ID}` | El `id` del conjunto de datos en el que se mantendrá el lote. |
| `{FILE_NAME}` | Nombre del archivo que está cargando. |

**Solicitud**

```SHELL
curl -X PUT 'https://platform.adobe.io/data/foundation/import/batches/5d01230fc78a4e4f8c0c6b387b4b8d1c/datasets/5c8c3c555033b814b69f947f/files/loyaltyData.parquet' \
  -H 'content-type: application/octet-stream' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  --data-binary '@{FILE_PATH_AND_NAME}.parquet'
```

**Respuesta**

Un archivo cargado correctamente devuelve un cuerpo de respuesta en blanco y Estado HTTP 200 (Aceptar).

## Finalización del lote de señales

Después de cargar todos los archivos de datos en el lote, puede indicar que el lote se ha completado. La finalización de la señalización hace que el servicio cree [!DNL Catalog] `DataSetFile` entradas para los archivos cargados y los asocie con el lote generado anteriormente. El lote [!DNL Catalog] se marca correctamente, lo que déclencheur cualquier flujo descendente que luego pueda funcionar con los datos disponibles.

**Formato API**

```HTTP
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Parámetro | Descripción |
| --- | --- |
| `{BATCH_ID}` | El `id` del lote que está marcando como completado. |

**Solicitud**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/5d01230fc78a4e4f8c0c6b387b4b8d1c?action=COMPLETE" \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**Respuesta**

Un lote completado correctamente devuelve un cuerpo de respuesta en blanco y Estado HTTP 200 (Aceptar).

## Supervisión de la ingesta

Según el tamaño de los datos, los lotes tardan varios períodos en ingestar. Puede supervisar el estado de un lote adjuntando un parámetro de solicitud `batch` que contenga el ID del lote a una solicitud `GET /batches`. La API sondea el conjunto de datos para el estado del lote desde la ingestión hasta que `status` en la respuesta indica finalización (&quot;éxito&quot; o &quot;error&quot;).

**Formato API**

```HTTP
GET /batches?batch={BATCH_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{BATCH_ID}` | El `id` del lote que desea monitorear. |

**Solicitud**

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/batches?batch=5d01230fc78a4e4f8c0c6b387b4b8d1c' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**Respuesta**

Una respuesta positiva devuelve un objeto con su atributo `status` que contiene el valor de `success`:

```JSON
{
    "5b7129a879323401ef2a6486": {
        "imsOrg": "{IMS_ORG}",
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

Una respuesta negativa devuelve un objeto con el valor `"failed"` en su atributo `"status"` e incluye cualquier mensaje de error relevante:

```JSON
{
    "5b96ce65badcf701e51f075d": {
        "imsOrg": "{IMS_ORG}",
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

Encontrará pasos detallados para trabajar con la API de acceso a datos en la [guía para desarrolladores de acceso a datos](../../data-access/home.md).

## Actualizar el esquema del conjunto de datos

Puede agregar campos e ingerir datos adicionales en conjuntos de datos que haya creado. Para ello, primero debe actualizar el esquema agregando propiedades adicionales que definan los nuevos datos. Esto se puede hacer con operaciones de PATCH o PUT para actualizar el esquema existente.

Para obtener más información sobre la actualización de esquemas, consulte la [Guía del programador de API de registro de Esquema](../../xdm/api/getting-started.md).

Una vez actualizado el esquema, puede seguir los pasos de este tutorial para ingestar nuevos datos que se ajusten al esquema revisado.

Es importante recordar que la evolución del esquema es puramente aditiva, lo que significa que no se puede introducir un cambio de ruptura en un esquema una vez que se haya guardado en el Registro y se haya utilizado para la ingestión de datos. Para obtener más información sobre las prácticas recomendadas para la composición de esquemas para su uso con Adobe Experience Platform, consulte la guía sobre los [conceptos básicos de la composición de esquemas](../../xdm/schema/composition.md).