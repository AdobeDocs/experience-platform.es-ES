---
title: Punto final de API de audiencias externas
description: Aprenda a utilizar la API de audiencias externas para crear, actualizar, activar y eliminar audiencias externas de Adobe Experience Platform.
hide: true
hidefromtoc: true
exl-id: eaa83933-d301-48cb-8a4d-dfeba059bae1
source-git-commit: 3acadf73b5c82d6f5f0f1eaec41387bec897558d
workflow-type: tm+mt
source-wordcount: '2405'
ht-degree: 4%

---

# Extremo de audiencias externas

Las audiencias externas permiten cargar datos de perfil de fuentes externas en Adobe Experience Platform. Puede usar el extremo `/external-audience` en la API del servicio de segmentación para introducir una audiencia externa en Experience Platform, ver detalles y actualizar las audiencias externas, así como eliminar las audiencias externas.

## Introducción

>[!IMPORTANT]
>
>Los extremos de esta guía llevan el prefijo `/core/ais`, a diferencia de `/core/ups`.

Para usar las API de Experience Platform, debe haber completado el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en las llamadas a la API de Experience Platform, como se muestra a continuación:

- Autorización: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Todos los recursos de [!DNL Experience Platform] están aislados en zonas protegidas virtuales específicas. Todas las solicitudes a las API de [!DNL Experience Platform] requieren un encabezado que especifica el nombre de la zona protegida en la que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre cómo trabajar con zonas protegidas en [!DNL Experience Platform], consulte la [documentación general sobre las zonas protegidas](../../sandboxes/home.md).

## Crear audiencia externa {#create-audience}

Puede crear una audiencia externa realizando una petición POST al extremo `/external-audience/`.

**Formato de API**

```http
POST /external-audience/
```

**Solicitud**

+++ Una solicitud de ejemplo para crear una audiencia externa.

```shell
curl -X POST https://platform.adobe.io/data/core/ais/external-audience/ \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "Sample external audience",
        "description": "A sample version of an external audience",
        "fields": [
            {
                "name": "ppid",
                "type": "string",
                "identityNs": "email"
            },
            {
                "name": "list_id",
                "type": "string",
                "labels": ["core/C2", "custom/deep"]
            },
            {
                "name": "delete",
                "type": "number"
            },
            {
                "name": "process_consent",
                "type": "string"
            }
        ],
        "sourceSpec": {
            "path": "activation/sample-source/example.csv",
            "type": "file",
            "sourceType": "Cloud Storage",
            "baseConnectionId": "1d1d4bc5-b527-46a3-9863-530246a61b2b"
        },
        "ttlInDays": "40",
        "labels": ["core/C1"],
        "audienceType": "people",
        "originName": "CUSTOM_UPLOAD"
    }'
```

| Propiedad | Tipo | Descripción |
| -------- | ---- | ----------- |
| `name` | Cadena | Nombre de la audiencia externa. |
| `description` | Cadena | Una descripción opcional para la audiencia externa. |
| `customAudienceId` | Cadena | Un identificador opcional para la audiencia externa. |
| `fields` | Matriz de objetos | La lista de campos y sus tipos de datos. Al crear la lista de campos, puede agregar los siguientes elementos: <ul><li>`name`: **Requerido** El nombre del campo que forma parte de la especificación de audiencia externa.</li><li>`type`: **Requerido** Tipo de datos que van al campo. Los valores admitidos son `string`, `number`, `long`, `integer`, `date` (`2025-05-13`), `datetime` (`2025-05-23T20:19:00+00:00`) y `boolean`.</li>`identityNs`: **Requerido para el campo de identidad** El área de nombres que usa el campo de identidad. Los valores admitidos incluyen todas las áreas de nombres válidas, como `ECID` o `email`.li><li>`labels`: *Opcional* Una matriz de etiquetas de control de acceso para el campo. Encontrará más información sobre las etiquetas de control de acceso disponibles en el [glosario de etiquetas de uso de datos](/help/data-governance/labels/reference.md). </li></ul> |
| `sourceSpec` | Objeto | Un objeto que contiene la información donde se encuentra la audiencia externa. Al usar este objeto, **debe** incluir la siguiente información: <ul><li>`path`: **Requerido**: La ubicación de la audiencia externa o la carpeta que contiene la audiencia externa dentro del origen.</li><li>`type`: **Requerido** El tipo de objeto que está recuperando del origen. Este valor puede ser `file` o `folder`.</li><li>`sourceType`: *Opcional* El tipo de origen desde el que está recuperando. Actualmente, el único valor admitido es `Cloud Storage`.</li><li>`cloudType`: *Opcional* El tipo de almacenamiento en la nube, basado en el tipo de origen. Los valores admitidos son `S3`, `DLZ`, `GCS` y `SFTP`.</li><li>`baseConnectionId`: el identificador de la conexión base y se proporciona desde el proveedor de origen. Este valor es **obligatorio** si se usa un valor `cloudType` de `S3`, `GCS` o `SFTP`. Para obtener más información, lea la [descripción general de conectores de origen](../../sources/home.md)li></ul> |
| `ttlInDays` | Entero | La caducidad de los datos de la audiencia externa en días. Este valor puede establecerse de 1 a 90. De forma predeterminada, la caducidad de los datos se establece en 30 días. |
| `audienceType` | Cadena | Tipo de audiencia de la audiencia externa. Actualmente, solo se admite `people`. |
| `originName` | Cadena | **Requerido**: el origen de la audiencia. Indica de dónde proviene la audiencia. Para audiencias externas, debe usar `CUSTOM_UPLOAD`. |
| `namespace` | Cadena | El área de nombres de la audiencia. De manera predeterminada, este valor está establecido en `CustomerAudienceUpload`. |
| `labels` | Matriz de cadenas | Las etiquetas de control de acceso que se aplican a la audiencia externa. Encontrará más información sobre las etiquetas de control de acceso disponibles en el [glosario de etiquetas de uso de datos](/help/data-governance/labels/reference.md). |
| `tags` | Matriz de cadenas | Las etiquetas que desee aplicar a la audiencia externa. Encontrará más información sobre las etiquetas en la [guía de administración de etiquetas](/help/administrative-tags/ui/managing-tags.md). |

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 202 con detalles de la audiencia externa recién creada.

+++ Una respuesta de ejemplo al crear una audiencia externa.

```json
{
    "operationId": "df8cd82f-a214-4b72-b549-d6ee23f1ff1a",
    "operationDetails": {
        "name": "Sample external audience",
        "description": "A sample version of an external audience",
        "fields": [
            {
                "name": "ppid",
                "type": "string",
                "identityNs": "Email"
            },
            {
                "name": "list_id",
                "type": "string",
                "labels": ["core/C2", "custom/deep"]
            },
            {
                "name": "delete",
                "type": "number"
            },
            {
                "name": "process_consent",
                "type": "string"
            }
        ],
        "sourceSpec": {
            "path": "activation/sample-source/example.csv",
            "type": "file",
            "sourceType": "Cloud Storage",
            "baseConnectionId": "1d1d4bc5-b527-46a3-9863-530246a61b2b"
            },
        "ttlInDays": 40,
        "labels": ["core/C1"],
        "audienceType": "people",
        "originName": "CUSTOM_UPLOAD"
    }   
}
```

| Propiedad | Tipo | Descripción |
| -------- | ---- | ----------- |
| `operationId` | Cadena | El ID de la operación. Posteriormente, puede utilizar este ID para recuperar el estado de creación de la audiencia. |
| `operationDetails` | Objeto | Un objeto que contiene los detalles de la solicitud enviada para crear la audiencia externa. |
| `name` | Cadena | Nombre de la audiencia externa. |
| `description` | Cadena | La descripción de la audiencia externa. |
| `fields` | Matriz de objetos | La lista de campos y sus tipos de datos. Esta matriz determina qué campos necesita en la audiencia externa. |
| `sourceSpec` | Objeto | Un objeto que contiene la información donde se encuentra la audiencia externa. |
| `ttlInDays` | Entero | La caducidad de los datos de la audiencia externa en días. Este valor puede establecerse de 1 a 90. De forma predeterminada, la caducidad de los datos se establece en 30 días. |
| `audienceType` | Cadena | Tipo de audiencia de la audiencia externa. |
| `originName` | Cadena | **Requerido**: el origen de la audiencia. Indica de dónde proviene la audiencia. |
| `namespace` | Cadena | El área de nombres de la audiencia. |
| `labels` | Matriz de cadenas | Las etiquetas de control de acceso que se aplican a la audiencia externa. Encontrará más información sobre las etiquetas de control de acceso disponibles en el [glosario de etiquetas de uso de datos](/help/data-governance/labels/reference.md). |


+++

## Recuperar estado de creación de audiencia {#retrieve-status}

Puede recuperar el estado del envío de audiencia externa realizando una petición GET al extremo `/external-audiences/operations` y proporcionando el ID de la operación que recibió de la respuesta Crear audiencia externa.

**Formato de API**

```http
GET /external-audiences/operations/{OPERATION_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{OPERATION_ID}` | El valor `id` de la operación que desea recuperar. |

**Solicitud**

+++ Una solicitud de muestra para recuperar el estado de funcionamiento de una audiencia externa.

```shell
curl -X GET https://platform.adobe.io/data/core/ais/external-audience/operations/df8cd82f-a214-4b72-b549-d6ee23f1ff1a \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles del estado de la tarea de la audiencia externa.

+++ Una respuesta de ejemplo al recuperar el estado de la tarea de una audiencia externa.

```json
{
    "operationId": "df8cd82f-a214-4b72-b549-d6ee23f1ff1a",
    "status": "SUCCESS",
    "operationDetails": {
        "name": "Sample external audience",
        "description": "A sample version of an external audience",
        "fields": [
            {
                "name": "ppid",
                "type": "string",
                "identityNs": "Email"
            },
            {
                "name": "list_id",
                "type": "string",
                "labels": ["core/C2", "custom/deep"]
            },
            {
                "name": "delete",
                "type": "number"
            },
            {
                "name": "process_consent",
                "type": "string"
            }
        ],
        "sourceSpec": {
            "path": "activation/sample-source/example.csv",
            "type": "file",
            "sourceType": "Cloud Storage",
            "baseConnectionId": "1d1d4bc5-b527-46a3-9863-530246a61b2b"
            },
        "ttlInDays": 40,
        "labels": ["core/C1"],
        "audienceType": "people",
        "originName": "CUSTOM_UPLOAD"
    },
    "audienceName": "Sample external audience",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "createdBy": "{USER_ID}",
    "createdAt": 1749324248,
    "updatedBy": "{USER_ID}",
    "updatedAt": 1749624273
}
```

| Propiedad | Tipo | Descripción |
| -------- | ---- | ----------- |
| `operationId` | Cadena | El ID de la operación que está recuperando. |
| `status` | Cadena | El estado de la operación. Puede ser uno de los siguientes valores: `SUCCESS`, `FAILED`, `PROCESSING`. |
| `operationDetails` | Objeto | Un objeto que contiene detalles de la audiencia. |
| `audienceId` | Cadena | El ID de la audiencia externa que envía la operación. |
| `createdBy` | Cadena | El ID del usuario que creó la audiencia externa. |
| `createdAt` | Marca de tiempo de época larga | La marca de tiempo, en segundos, cuando se envió la solicitud para crear la audiencia externa. |
| `updatedBy` | Cadena | El ID del usuario que actualizó la audiencia por última vez. |
| `updatedAt` | Marca de tiempo de época larga | La marca de tiempo, en segundos, de la última actualización de la audiencia. |

+++

## Actualización de una audiencia externa {#update-audience}

>[!NOTE]
>
>Para usar el siguiente punto de conexión, necesita tener `audienceId` de su audiencia externa. Puede obtener su `audienceId` desde una llamada correcta al extremo `GET /external-audiences/operations/{OPERATION_ID}`.

Puede actualizar los campos de la audiencia externa realizando una petición PATCH al extremo `/external-audience` y proporcionando el ID de la audiencia en la ruta de solicitud.

Al utilizar este punto de conexión, puede actualizar los siguientes campos:

- Descripción de público
- Etiquetas de control de acceso de nivel de campo
- Etiquetas de control de acceso de nivel de audiencia

Al actualizar el campo usando este extremo **se reemplaza** el contenido del campo que solicitó.

**Formato de API**

```http
PATCH /external-audience/{AUDIENCE_ID}
```

**Solicitud**

+++ Una solicitud de ejemplo para actualizar la descripción de la audiencia externa.

```shell
curl -X PATCH https://platform.adobe.io/data/core/ais/external-audience/60ccea95-1435-4180-97a5-58af4aa285ab\
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "description": "New sample description"
 }'
```

| Propiedad | Tipo | Descripción |
| -------- | ---- | ----------- |
| `description` | Cadena | La descripción actualizada para la audiencia externa. |

Además, puede actualizar los siguientes parámetros:

| Propiedad | Tipo | Descripción |
| -------- | ---- | ----------- |
| `labels` | Matriz | Una matriz que contiene la lista actualizada de etiquetas de acceso para la audiencia. Encontrará más información sobre las etiquetas de control de acceso disponibles en el [glosario de etiquetas de uso de datos](/help/data-governance/labels/reference.md). |
| `fields` | Matriz de objetos | Una matriz que contiene los campos y sus etiquetas asociadas para la audiencia externa. Solo se actualizan los campos que aparecen en la solicitud de PATCH. Encontrará más información sobre las etiquetas de control de acceso disponibles en el [glosario de etiquetas de uso de datos](/help/data-governance/labels/reference.md). |
| `ttlInDays` | Entero | La caducidad de los datos de la audiencia externa en días. Este valor puede establecerse de 1 a 90. |

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la audiencia externa actualizada.

+++ Una respuesta de ejemplo al actualizar la descripción de la audiencia externa.

```json
{
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceName": "Sample external audience",
    "description": "New sample description",
    "fields": [
        {
            "name": "ppid",
            "type": "string",
            "identityNs": "Email"
        },
        {
            "name": "list_id",
            "type": "string",
            "labels": ["core/C2", "custom/deep"]
        },
        {
            "name": "delete",
            "type": "number"
        },
        {
            "name": "process_consent",
            "type": "string"
        }
    ],
    "sourceSpec": {
        "path": "activation/sample-source/example.csv",
        "type": "file",
        "sourceType": "Cloud Storage",
        "baseConnectionId": "1d1d4bc5-b527-46a3-9863-530246a61b2b"
        },
    "ttlInDays": 40,
    "labels": ["core/C1"],
    "audienceType": "people",
    "originName": "CUSTOM_UPLOAD",
    "createdBy": "{USER_ID}",
    "createdAt": 1749324248,
    "updatedBy": "{USER_ID}",
    "updatedAt": 1749624273
}
```

+++

## Iniciar ingesta de audiencia {#start-audience-ingestion}

>[!IMPORTANT]
>
>**no** podrá iniciar una nueva ingesta para la audiencia externa si ya se está realizando una ingesta de audiencia anterior.

>[!NOTE]
>
>Para usar el siguiente punto de conexión, necesita tener `audienceId` de su audiencia externa. Puede obtener su `audienceId` desde una llamada correcta al extremo `GET /external-audiences/operations/{OPERATION_ID}`.

Puede iniciar una ingesta de audiencia realizando una petición POST al siguiente punto de conexión, proporcionando al mismo tiempo el ID de audiencia.

**Formato de API**

```http
POST /external-audience/{AUDIENCE_ID}/runs
```

**Solicitud**

La siguiente solicitud crea un déclencheur de ejecución de ingesta para la audiencia externa.

+++ Una solicitud de ejemplo para iniciar una ingesta de audiencia.

```shell
curl -X POST https://platform.adobe.io/data/core/ais/external-audience/60ccea95-1435-4180-97a5-58af4aa285ab/runs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "dataFilterStartTime": 764245635
 }' 
```

| Propiedad | Tipo | Descripción |
| -------- | ---- | ----------- |
| `dataFilterStartTime` | Marca de tiempo Epoch | **Requerido** Intervalo que especifica la hora de inicio en la que se ejecutará el flujo para seleccionar qué archivos se procesarán. |
| `dataFilterEndTime` | Marca de tiempo Epoch | Intervalo que especifica la hora de finalización en la que se ejecutará el flujo para seleccionar qué archivos se procesarán. |
| `differentialIngestion` | Booleano | Campo que determina si la ingesta será parcial, en función de la diferencia desde la última o total. De manera predeterminada, este valor es `true`. |

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles sobre la ejecución de la ingesta.

+++ Una respuesta de ejemplo al iniciar la ingesta de audiencia.

```json
{
    "audienceName": "Sample external audience",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "runId": "fb342311-725d-4b48-ab7d-c6105fbc2b8b",
    "differentialIngestion": true,
    "dataFilterStartTime": 764245635,
    "dataFilterEndTime": 4565657575,
    "createdAt": 4565657575,
    "createdBy:" "{USER_ID}"
}
```

| Propiedad | Tipo | Descripción |
| -------- | ---- | ----------- |
| `audienceName` | Cadena | El nombre de la audiencia para la que está iniciando una ejecución de ingesta. |
| `audienceId` | Cadena | El ID de la audiencia. |
| `runId` | Cadena | El ID de la ejecución de ingesta que inició. |
| `differentialIngestion` | Booleano | Campo que determina si la ingesta es parcial, en función de la diferencia desde la última ingesta o desde una ingesta de audiencia completa. |
| `dataFilterStartTime` | Marca de tiempo Epoch | El rango que especifica la hora de inicio en la que se ejecuta el flujo para seleccionar qué archivos se procesaron. |
| `dataFilterEndTime` | Marca de tiempo Epoch | Intervalo que especifica la hora de finalización en la que se ejecuta el flujo para seleccionar qué archivos se procesaron. |
| `createdAt` | Marca de tiempo de época larga | La marca de tiempo, en segundos, cuando se envió la solicitud para crear la audiencia externa. |
| `createdBy` | Cadena | El ID del usuario que creó la audiencia externa. |

+++

## Recuperar estado de ingesta de audiencia específico {#retrieve-ingestion-status}

>[!NOTE]
>
>Para usar el siguiente extremo, necesita tener `audienceId` de la audiencia externa y `runId` del identificador de ejecución de la ingesta. Puede obtener su `audienceId` desde una llamada correcta al extremo `GET /external-audiences/operations/{OPERATION_ID}` y su `runId` desde una llamada correcta anterior del extremo `POST /external-audience/{AUDIENCE_ID}/runs`.

Puede recuperar el estado de una ingesta de audiencia realizando una petición GET al siguiente extremo, proporcionando al mismo tiempo la audiencia y los ID de ejecución.

**Formato de API**

```http
GET /external-audience/{AUDIENCE_ID}/runs/{RUN_ID}
```

**Solicitud**

La siguiente solicitud recupera el estado de ingesta para la audiencia externa.

+++ Una solicitud de muestra para recuperar el estado de ingesta de la audiencia externa.

```shell
curl -X GET https://platform.adobe.io/data/core/ais/external-audience/60ccea95-1435-4180-97a5-58af4aa285ab/runs/fb342311-725d-4b48-ab7d-c6105fbc2b8b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la ingesta de audiencia externa.

+++ Una respuesta de ejemplo al recuperar la ingesta de la audiencia externa.

```json
{
    "audienceName": "Sample external audience",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "runId": "fb342311-725d-4b48-ab7d-c6105fbc2b8b",
    "status": "SUCCESS",
    "differentialIngestion": true,
    "dataFilterStartTime": 764245635,
    "dataFilterEndTime": 3456788568,
    "createdAt": 1749324248,
    "createdBy": "{USER_ID}",
    "details": [
        {
            "stage": "DATASET_INGEST",
            "status": "SUCCESS",
            "flowRunId": "{FLOW_RUN_ID}"
        },
        {
            "stage": "PROFILE_STORE_INGEST",
            "status": "SUCCESS",
            "flowRunId": "{FLOW_RUN_ID}"
        }
    ]
}
```

| Propiedad | Tipo | Descripción |
| -------- | ---- | ----------- |
| `audienceName` | Cadena | Nombre de la audiencia. |
| `audienceId` | Cadena | El ID de la audiencia. |
| `runId` | Cadena | El ID de la ejecución de ingesta. |
| `status` | Cadena | El estado de la ejecución de ingesta. Los estados posibles incluyen `SUCCESS` y `FAILED`. |
| `differentialIngestion` | Booleano | Campo que determina si la ingesta es parcial, en función de la diferencia desde la última ingesta o desde una ingesta de audiencia completa. |
| `dataFilterStartTime` | Marca de tiempo Epoch | El rango que especifica la hora de inicio en la que se ejecuta el flujo para seleccionar qué archivos se procesaron. |
| `dataFilterEndTime` | Marca de tiempo Epoch | Intervalo que especifica la hora de finalización en la que se ejecuta el flujo para seleccionar qué archivos se procesaron. |
| `createdAt` | Marca de tiempo de época larga | La marca de tiempo, en segundos, cuando se envió la solicitud para crear la audiencia externa. |
| `createdBy` | Cadena | El ID del usuario que creó la audiencia externa. |
| `details` | Matriz de objetos | Un objeto que contiene los detalles de la ejecución de ingesta. <ul><li>`stage`: fase de la ejecución de ingesta. Puede ser `DATASET_INGEST` o `PROFILE_STORE_INGEST`, que representan la ingesta del lago de datos y la ingesta de perfiles.</li><li>`status`: el estado de la ingesta en el escenario. Los estados posibles incluyen `SUCCESS` y `FAILED`.</li><li>`flowRunId`: ID de ejecución del flujo de ingesta de la fase.</li></ul> |

+++

## Enumerar ejecuciones de ingesta de audiencia {#list-ingestion-runs}

>[!NOTE]
>
>Para usar el siguiente punto de conexión, necesita tener `audienceId` de su audiencia externa. Puede obtener su `audienceId` desde una llamada correcta al extremo `GET /external-audiences/operations/{OPERATION_ID}`.

Puede recuperar todas las ejecuciones de ingesta para la audiencia externa seleccionada realizando una petición GET al siguiente punto de conexión mientras proporciona el ID de audiencia. Se pueden incluir varios parámetros, separados por el símbolo et (`&`).

**Formato de API**

El siguiente punto de conexión admite varios parámetros de consulta para filtrar los resultados. Aunque estos parámetros son opcionales, se recomienda encarecidamente su uso para ayudarle a enfocar los resultados.

```http
GET /external-audience/{AUDIENCE_ID}/runs
GET /external-audience/{AUDIENCE_ID}/runs?{QUERY_PARAMETERS}
```

**Parámetros de consulta**

+++ Una lista de parámetros de consulta disponibles.

| Parámetro | Descripción | Ejemplo |
| --------- | ----------- | ------- |
| `limit` | Número máximo de elementos devueltos en la respuesta. Este valor puede variar de 1 a 40. De forma predeterminada, el límite se establece en 20. | `limit=30` |
| `sortBy` | Orden en el que se ordenan los elementos devueltos. Puede ordenar por `name` o por `createdAt`. Además, puede agregar un signo `-` para ordenar por orden **descendente** en lugar de **ascendente**. De forma predeterminada, los elementos se ordenan por `createdAt` en orden descendente. | `sortBy=name` |
| `property` | Un filtro para determinar qué ejecuciones de ingesta de audiencia se muestran. Puede filtrar según las siguientes propiedades: <ul><li>`name`: le permite filtrar por nombre de audiencia. Si utiliza esta propiedad, puede realizar la comparación mediante `=`, `!=`, `=contains` o `!=contains`. </li><li>`createdAt`: le permite filtrar por el tiempo de ingesta. Si usa esta propiedad, puede realizar la comparación mediante `>=` o `<=`.</li><li>`status`: le permite filtrar por el estado de la ejecución de ingesta. Si utiliza esta propiedad, puede realizar la comparación mediante `=`, `!=`, `=contains` o `!=contains`. </li></ul> | `property=createdAt<1683669114845`<br/>`property=name=demo_audience`<br/>`property=status=SUCCESS` |

+++

**Solicitud**

La siguiente solicitud recupera todas las ejecuciones de ingesta para la audiencia externa.

+++ Se ejecuta una solicitud de ejemplo para obtener una lista de ejecuciones de ingesta de audiencias.

```shell
curl -X GET https://platform.adobe.io/data/core/ais/external-audience/60ccea95-1435-4180-97a5-58af4aa285ab/runs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con una lista de ejecuciones de ingesta para la audiencia externa especificada.

+++ Una respuesta de ejemplo al recuperar una lista de ejecuciones de ingesta de audiencia.

```json
{
    "runs": [
        {
            "audienceName": "Sample external audience",
            "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "runId": "fb342311-725d-4b48-ab7d-c6105fbc2b8b",
            "status": "SUCCESS",
            "differentialIngestion": true,
            "dataFilterStartTime": 764245635,
            "dataFilterEndTime": 3456788568,
            "createdAt": 1785678909,
            "createdBy": "{USER_NAME}"
        },
        {
            "audienceName": "Sample external audience 2",
            "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "runId": "406e38e4-fbd5-43e1-8d0c-01ccb3f9ad10",
            "status": "SUCCESS",
            "differentialIngestion": true,
            "dataFilterStartTime": 764245635,
            "dataFilterEndTime": 3456788568,
            "createdAt": 1749324248,
            "createdBy": "{USER_ID}"
        }
    ],
    "_page": {
        "limit": 20,
        "count": 2,
        "totalCount": 2
    }
}
```

| Propiedad | Tipo | Descripción |
| -------- | ---- | ----------- |
| `runs` | Objeto | Un objeto que contiene la lista de ejecuciones de ingesta que pertenece a la audiencia. Encontrará más información sobre este objeto en la [sección de recuperación del estado de ingesta](#retrieve-ingestion-status). |
| `_page` | Objeto | Objeto que contiene la información de paginación acerca de la lista de resultados. |

+++

## Eliminación de una audiencia externa {#delete-audience}

>[!NOTE]
>
>Para usar el siguiente punto de conexión, necesita tener `audienceId` de su audiencia externa. Puede obtener su `audienceId` desde una llamada correcta al extremo `GET /external-audiences/operations/{OPERATION_ID}`.

Puede eliminar una audiencia externa realizando una petición DELETE al siguiente extremo, siempre que proporcione el ID de audiencia.

**Formato de API**

```http
DELETE /external-audience/{AUDIENCE_ID}
```

**Solicitud**

La siguiente solicitud elimina la audiencia externa especificada.

+++ Una solicitud de ejemplo para eliminar la audiencia externa.

```shell
curl -X DELETE https://platform.adobe.io/data/core/ais/external-audience/60ccea95-1435-4180-97a5-58af4aa285ab/ \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 204 con un cuerpo de respuesta vacío.

## Pasos siguientes {#next-steps}

Después de leer esta guía, ahora tiene una mejor comprensión de cómo crear, administrar y eliminar audiencias externas mediante las API de Experience Platform. Para obtener información sobre cómo usar audiencias externas con la interfaz de usuario de Experience Platform, lea la [documentación de Audience Portal](../ui/audience-portal.md).

## Apéndice {#appendix}

En la siguiente sección se enumeran los códigos de error disponibles al utilizar la API de audiencias externas.

| Código de error de plataforma | Código de estado | Mensaje | Descripción |
| ------------------- | ----------- | ------- | ----------- |
| 100910-400 | 400 | `BAD_REQUEST` | Se ha producido una solicitud incorrecta debido a un error que se produjo al validar las solicitudes. |
| 100911-400 | 400 | `BAD_REQUEST` | Se ha proporcionado un token no válido. |
| 100920-401 | 401 | `UNAUTHORIZED` | Falta un encabezado. |
| 100921-401 | 401 | `UNAUTHORIZED` | Se ha proporcionado un `imsOrgId` no válido. |
| 100922-401 | 401 | `UNAUTHORIZED` | No tiene autorización para utilizar las API de audiencias externas. |
| 100940-404 | 404 | `NOT_FOUND` | No se ha encontrado la audiencia solicitada. |
| 100950-409 | 409 | `DUPLICATE_RESOURCE` | La audiencia ya existe. |
| 100960-422 | 422 | `UNPROCESSABLE_ENTITY` | La estructura de la solicitud es válida, pero no se puede procesar debido a errores lógicos o semánticos. |
| 100970-500 | 500 | `INTERNAL_SERVER_ERROR` | Se ha producido un error al procesar la solicitud en el sistema. |
| 100970-502 | 502 | `BAD_GATEWAY` | Hay problemas de dependencia descendente. |
