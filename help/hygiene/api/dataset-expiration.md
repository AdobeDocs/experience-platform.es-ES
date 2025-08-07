---
title: Punto final de API de caducidad del conjunto de datos
description: El extremo /ttl de la API de higiene de datos le permite programar la caducidad de los conjuntos de datos en Adobe Experience Platform.
role: Developer
exl-id: fbabc2df-a79e-488c-b06b-cd72d6b9743b
source-git-commit: ca6d7d257085da65b3f08376f0bd32e51e293533
workflow-type: tm+mt
source-wordcount: '2331'
ht-degree: 2%

---

# Extremo de caducidad del conjunto de datos

Utilice el extremo `/ttl` en la API de higiene de datos para programar cuándo se deben eliminar los conjuntos de datos en Adobe Experience Platform.

Una caducidad del conjunto de datos es una operación de eliminación retrasada. El conjunto de datos no está protegido mientras tanto y puede eliminarse por otros medios antes de su caducidad programada.

>[!NOTE]
>
>Aunque la caducidad se especifica como un instante de tiempo específico, puede haber hasta 24 horas de retraso después de la caducidad antes de que se inicie la eliminación real. Una vez iniciada la eliminación, pueden pasar hasta siete días antes de que se hayan eliminado todos los seguimientos del conjunto de datos de los sistemas Experience Platform.

Antes de que comience la eliminación, puede cancelar la caducidad o cambiar su hora programada. Para volver a abrir una caducidad cancelada, establezca una nueva caducidad.

Una vez iniciada la eliminación, el trabajo de caducidad se marca como `executing` y ya no se puede modificar. El conjunto de datos puede recuperarse durante un máximo de siete días, pero solo a través de una solicitud de servicio manual de Adobe. Durante la eliminación, el lago de datos, el servicio de identidad y el perfil del cliente en tiempo real quitan cada uno el contenido del conjunto de datos por separado. Una vez completada la eliminación, la caducidad se marca como `completed`.

>[!WARNING]
>
>Si un conjunto de datos está configurado para caducar, debe cambiar manualmente los flujos de datos que puedan estar introduciendo datos en ese conjunto de datos para que los flujos de trabajo descendentes no se vean afectados negativamente.

La administración avanzada del ciclo de vida de datos admite eliminaciones de conjuntos de datos mediante el extremo de caducidad del conjunto de datos y eliminaciones de ID (datos de nivel de fila) mediante identidades principales a través del [extremo de orden de trabajo](./workorder.md). También puede administrar [caducidades de conjuntos de datos](../ui/dataset-expiration.md) y [eliminaciones de registros](../ui/record-delete.md) a través de la interfaz de usuario de Experience Platform. Consulte la documentación vinculada para obtener más información.

>[!NOTE]
>
>El ciclo de vida de datos no admite la eliminación por lotes.

## Introducción

El extremo utilizado en esta guía forma parte de la API de higiene de datos. Antes de continuar, revise la [guía de API](./overview.md) para obtener información sobre los encabezados necesarios para operaciones de CRUD, mensajes de error, colecciones de Postman y cómo leer llamadas de API de ejemplo.

>[!IMPORTANT]
>
>Al realizar llamadas a la API de higiene de datos, debe utilizar el encabezado -H `x-sandbox-name: {SANDBOX_NAME}`.

## Enumerar caducidades del conjunto de datos {#list}

Puede enumerar todas las caducidades de los conjuntos de datos configurados para su organización realizando una petición GET al extremo `/ttl`.

Filtre los resultados con parámetros de consulta para devolver solo las caducidades que cumplan los criterios. Cada resultado incluye detalles de estado y configuración para cada caducidad del conjunto de datos.

**Formato de API**

```http
GET /ttl?{QUERY_PARAMETERS}
```

| Parámetro | Descripción |
| --- | --- |
| `{QUERY_PARAMETERS}` | Una lista de parámetros de consulta opcionales, con varios parámetros separados por `&` caracteres. Los parámetros comunes incluyen `limit` y `page` para fines de paginación. Para obtener una lista completa de los parámetros de consulta admitidos, consulte la [sección del apéndice](#query-params) con una lista completa de los parámetros de consulta admitidos. Los parámetros más utilizados se incluyen a continuación, así como en el apéndice. |
| `author` | Filtre por el usuario que actualizó o creó recientemente la caducidad del conjunto de datos. Admite patrones de tipo SQL (por ejemplo, `LIKE %john%`). |
| `datasetId` | Filtrar las caducidades por un ID de conjunto de datos específico. |
| `datasetName` | Un filtro que no distingue entre mayúsculas y minúsculas para las coincidencias de nombres de conjuntos de datos. |
| `status` | Filtrar por una lista de estados separados por comas: `pending`, `executing`, `cancelled`, `completed`. |
| `expiryDate` | Filtre por caducidades con una fecha de caducidad específica. |
| `limit` | Estipule el número máximo de resultados que desea devolver (1-100, predeterminado: 25). |
| `page` | Pagine los resultados con un índice basado en cero (tamaño de página predeterminado: 50, máximo: 100). |

{style="table-layout:auto"}

**Solicitud**

La siguiente solicitud recupera todas las caducidades del conjunto de datos actualizadas antes del 1 de agosto de 2021 y actualizadas por última vez por un usuario cuyo nombre coincida con &quot;Jane Doe&quot;.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl?updatedToDate=2021-08-01&author=LIKE%20%25Jane%20Doe%25 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta enumera las caducidades resultantes del conjunto de datos. El siguiente ejemplo se ha truncado para el espacio.

>[!IMPORTANT]
>
>El `ttlId` de la respuesta también se conoce como `{DATASET_EXPIRATION_ID}`. Ambos hacen referencia al identificador único para la caducidad del conjunto de datos.

```json
{
  "results": [
    {
      "ttlId": "SD-c9f113f2-d751-44bc-bc20-9d5ca0b6ae15",
      "datasetId": "3e9f815ae1194c65b2a4c5ea",
      "datasetName": "Acme_Profile_Engagements",
      "sandboxName": "acme-beta",
      "displayName": "Engagement Data Retention Policy",
      "description": "Scheduled expiry for Acme marketing data",
      "imsOrg": "C9D8E7F6A5B41234567890AB@AcmeOrg",
      "status": "pending",
      "expiry": "2027-01-12T17:15:31.000Z",
      "updatedAt": "2026-12-15T12:40:20.000Z",
      "updatedBy": "t.lannister@acme.com <t.lannister@acme.com> 3E9F815AE1194C65B2A4C5EA@acme.com"
    }
  ],
  "current_page": 0,
  "total_pages": 1,
  "total_count": 1
}
```

| Propiedad | Descripción |
| --- | --- |
| `results` | Matriz de configuraciones de caducidad de conjuntos de datos. |
| `ttlId` | El identificador único de la configuración de caducidad del conjunto de datos. |
| `datasetId` | El identificador único del conjunto de datos asociado con esta configuración. |
| `datasetName` | Nombre del conjunto de datos. |
| `sandboxName` | La zona protegida en la que se configura la caducidad de este conjunto de datos. |
| `displayName` | Un nombre legible en lenguaje natural para la configuración de caducidad. |
| `description` | Una descripción de la configuración de caducidad. |
| `imsOrg` | Su identificador único de organización. |
| `status` | El estado actual de la caducidad. Uno de: `pending`, `executing`, `cancelled`, `completed`. |
| `expiry` | La fecha y hora de caducidad programadas (formato ISO 8601). |
| `updatedAt` | La marca de tiempo de la última actualización de esta configuración. |
| `updatedBy` | El identificador y el correo electrónico del usuario o servicio que actualizó la configuración por última vez. |
| `current_page` | Índice de la página de resultados actual (basado en cero). |
| `total_pages` | Número total de páginas de resultados disponibles. |
| `total_count` | Número total de registros de configuración de caducidad del conjunto de datos devueltos. |

{style="table-layout:auto"}

## Búsqueda de una caducidad del conjunto de datos {#lookup}

Recupere los detalles de una configuración de caducidad específica del conjunto de datos realizando una petición GET con el ID de caducidad del conjunto de datos o el ID del conjunto de datos como parámetro de ruta.

>[!IMPORTANT]
>
>Puede proporcionar una ID de caducidad del conjunto de datos (por ejemplo, `SD-xxxxxx-xxxx`) o una ID de conjunto de datos en la ruta. El `ttlId` en la respuesta es el identificador único para la caducidad del conjunto de datos.

**Formato de API**

```http
GET /ttl/{ID}
GET /ttl/{ID}?include=history
```

| Parámetro | Descripción |
| --- | --- |
| `{ID}` | El identificador único de la configuración de caducidad del conjunto de datos. Puede proporcionar una ID de caducidad del conjunto de datos o una ID de conjunto de datos. |
| `include` | (Opcional) Si se establece en `history`, la respuesta incluye una matriz `history` con eventos de cambio para la configuración. |

{style="table-layout:auto"}

**Solicitud**

La siguiente solicitud busca los detalles de caducidad del conjunto de datos `62759f2ede9e601b63a2ee14`:

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl/62759f2ede9e601b63a2ee14 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve los detalles de la caducidad del conjunto de datos.

```json
{
    "ttlId": "SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f",
    "datasetId": "62759f2ede9e601b63a2ee14",
    "datasetName": "XtVRwq9-38734",
    "sandboxName": "prod",
    "displayName": "Delete Acme Data before 2025",
    "description": "The Acme information in this dataset is licensed for our use through the end of 2024.",
    "imsOrg": "885737B25DC460C50A49411B@AdobeOrg",
    "status": "pending",
    "expiry": "2035-09-25T00:00:00Z",
    "updatedAt": "2025-05-01T19:00:55.000Z",
    "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e",
}
```

| Propiedad | Descripción |
| --- | --- |
| `ttlId` | El identificador único de la configuración de caducidad del conjunto de datos. |
| `datasetId` | El identificador único del conjunto de datos. |
| `datasetName` | Nombre del conjunto de datos. |
| `sandboxName` | La zona protegida en la que se configura la caducidad del conjunto de datos. |
| `displayName` | Un nombre en lenguaje natural para la configuración de caducidad del conjunto de datos. |
| `description` | Descripción de la configuración de caducidad del conjunto de datos. |
| `imsOrg` | El identificador único de organización asociado con esta configuración. |
| `status` | El estado actual de la configuración de caducidad del conjunto de datos.<br>Uno de: `pending`, `executing`, `cancelled`, `completed`. |
| `expiry` | La marca de tiempo de caducidad programada para el conjunto de datos (formato ISO 8601). |
| `updatedAt` | Marca de tiempo de la actualización más reciente. |
| `updatedBy` | El identificador y el correo electrónico del usuario o servicio que actualizó la caducidad del conjunto de datos por última vez. |

{style="table-layout:auto"}

### Etiquetas de caducidad del catálogo

Al usar la [API de catálogo](../../catalog/api/getting-started.md) para buscar detalles del conjunto de datos, si este tiene una caducidad activa, se enumerará en `tags.adobe/hygiene/ttl`.

El siguiente JSON muestra una respuesta de API de catálogo truncada para un conjunto de datos con un valor de caducidad de `32503680000000`. La etiqueta codifica la caducidad como el número de milisegundos desde la época de Unix.

```json
{
  "63212313c308d51b997858ba": {
    "name": "Test Dataset",
    "description": "A piecrust promise, made to be broken",
    "imsOrg": "0FCC747E56F59C747F000101@AdobeOrg",
    "sandboxId": "8dc51b90-d0f9-11e9-b164-ed6a398c8b35",
    "tags": {
      "adobe/hygiene/ttl": [ "32503680000000" ],
      ...
    },
    ...
  }
}
```

## Crear una caducidad del conjunto de datos {#create}

Cree una nueva configuración de caducidad del conjunto de datos para definir cuándo caducará un conjunto de datos y cuándo podrá eliminarse.\
Proporcione el ID del conjunto de datos, la fecha de caducidad o la fecha-hora (en formato ISO 8601), un nombre para mostrar y (opcionalmente) una descripción.

>[!NOTE]
>
>El valor de caducidad puede ser una fecha (AAAA-MM-DD) o una fecha y hora (AAAA-MM-DDTHH:MM:SSZ). Si proporciona solo una fecha, el sistema utiliza la medianoche UTC (00:00:00Z) de ese día. La caducidad debe ser de al menos 24 horas en el futuro.

Para crear una caducidad del conjunto de datos, envíe una petición POST como se muestra a continuación.

>[!TIP]
>
>Si recibe un error 404, asegúrese de que la solicitud no tenga barras diagonales adicionales. Una barra diagonal puede provocar el fallo de una petición POST.

**Formato de API**

```http
POST /ttl
```

**Solicitud**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/hygiene/ttl \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "datasetId": "3e9f815ae1194c65b2a4c5ea",
        "expiry": "2030-12-31",
        "displayName": "Expiry rule for Acme customers",
        "description": "Set expiration for Acme customer dataset"
      }'
```

| Propiedad | Descripción |
| --- | --- |
| `datasetId` | **Requerido.**: identificador único del conjunto de datos al que se aplicará la caducidad. |
| `expiry` | **Requerido.** La fecha y hora de caducidad en formato ISO 8601. Define la duración de los datos dentro del sistema. Si solo se proporciona una fecha, el valor predeterminado es medianoche UTC (00:00:00Z). La caducidad **debe ser al menos 24 horas en el futuro**. <br>**NOTA**:<ul><li>La solicitud fallará si ya existe una caducidad del conjunto de datos para él.</li></ul> |
| `displayName` | **Requerido.** Un nombre legible en lenguaje natural para la configuración de caducidad del conjunto de datos. |
| `description` | Una descripción opcional para la configuración de caducidad del conjunto de datos. |

**Respuesta**

Una respuesta correcta devuelve un estado HTTP 201 (Creado) y la nueva configuración de caducidad del conjunto de datos.

```json
{
  "ttlId": "SD-2aaf113e-3f17-4321-bf29-a2c51152b042",
  "datasetId": "3e9f815ae1194c65b2a4c5ea",
  "datasetName": "Acme_Customer_Data",
  "sandboxName": "acme-prod",
  "displayName": "Expiry rule for Acme customers",
  "description": "Set expiration for Acme customer dataset",
  "imsOrg": "{ORG_ID}",
  "status": "pending",
  "expiry": "2030-12-31T00:00:00Z",
  "updatedAt": "2025-01-02T10:35:45.000Z",
  "updatedBy": "s.stark@acme.com <s.stark@acme.com> 3E9F815AE1194C65B2A4C5EA@acme.com"
}
```

| Propiedad | Descripción |
| --- | --- |
| `ttlId` | El identificador único de la configuración de caducidad del conjunto de datos creada. |
| `datasetId` | El identificador único del conjunto de datos. |
| `datasetName` | Nombre del conjunto de datos. |
| `sandboxName` | La zona protegida en la que se configura la caducidad de este conjunto de datos. |
| `displayName` | El nombre para mostrar de la configuración de caducidad del conjunto de datos. |
| `description` | Descripción de la configuración de caducidad del conjunto de datos. |
| `imsOrg` | El identificador único de organización asociado con esta configuración. |
| `status` | El estado actual de la configuración de caducidad del conjunto de datos.<br>Uno de: `pending`, `executing`, `cancelled`, `completed`. |
| `expiry` | La marca de tiempo de caducidad programada para el conjunto de datos. |
| `updatedAt` | La marca de tiempo de la actualización más reciente. |
| `updatedBy` | El identificador y el correo electrónico del usuario o servicio que actualizó la configuración de caducidad del conjunto de datos por última vez. |

Se produce un estado HTTP 400 (Solicitud incorrecta) si ya existe una caducidad del conjunto de datos para el conjunto de datos. Se produce un estado HTTP 404 (no encontrado) si no existe el conjunto de datos o si no tiene acceso a él.

## Actualizar una configuración de caducidad del conjunto de datos {#update}

Para actualizar una configuración de caducidad de conjunto de datos existente, realice una petición PUT a `/ttl/DATASET_EXPIRATION_ID`. Solo puede actualizar los campos `displayName`, `description` y `expiry` de la configuración. Las actualizaciones solo se permiten cuando el estado de caducidad es `pending`.

>[!NOTE]
>
>El campo `expiry` acepta una fecha (AAAA-MM-DD) o fecha y hora (AAAA-MM-DDTHH:MM:SSZ). Si solo se proporciona una fecha, el sistema utiliza la medianoche UTC (00:00:00Z) de ese día. La caducidad **debe ser al menos 24 horas en el futuro**.

**Formato de API**

```http
PUT /ttl/{DATASET_EXPIRATION_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{DATASET_EXPIRATION_ID}` | El identificador único de la configuración de caducidad del conjunto de datos. **NOTA**: Esto se conoce como `ttlId` en la respuesta. |

**Solicitud**

La siguiente solicitud actualiza la caducidad, el nombre para mostrar y la descripción de la caducidad del conjunto de datos `SD-c1f902aa-57cb-412e-bb2b-c70b8e1a5f45`:

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/ttl/SD-c1f902aa-57cb-412e-bb2b-c70b8e1a5f45 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "displayName": "Customer Dataset Expiry Rule",
        "description": "Updated description for Acme customer dataset",
        "expiry": "2031-06-15"
      }'
```

| Propiedad | Descripción |
| --- | --- |
| `displayName` | (Opcional) Un nuevo nombre legible en lenguaje natural para la configuración de caducidad del conjunto de datos. |
| `description` | (Opcional) Una nueva descripción para la configuración de caducidad del conjunto de datos. |
| `expiry` | (Opcional) Una nueva fecha de caducidad o fecha y hora en formato ISO 8601. Si solo se proporciona una fecha, el valor predeterminado es medianoche UTC. La caducidad debe ser **al menos 24 horas en el futuro**. |

>[!NOTE]
>
>Al menos uno de estos campos debe proporcionarse en la solicitud.

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 (OK) y la configuración de caducidad del conjunto de datos actualizada.

```json
{
  "ttlId": "SD-c1f902aa-57cb-412e-bb2b-c70b8e1a5f45",
  "datasetId": "3e9f815ae1194c65b2a4c5ea",
  "datasetName": "Acme_Customer_Data",
  "sandboxName": "acme-prod",
  "displayName": "Customer Dataset Expiry Rule",
  "description": "Updated description for Acme customer dataset",
  "imsOrg": "C9D8E7F6A5B41234567890AB@AcmeOrg",
  "status": "pending",
  "expiry": "2031-06-15T00:00:00Z",
  "updatedAt": "2031-05-01T14:11:12.000Z",
  "updatedBy": "b.tarth@acme.com <b.tarth@acme.com> 3E9F815AE1194C65B2A4C5EA@acme.com"
}
```

| Propiedad | Descripción |
| --- | --- |
| `ttlId` | El identificador único de la configuración de caducidad actualizada del conjunto de datos. |
| `datasetId` | El identificador único del conjunto de datos. |
| `datasetName` | Nombre del conjunto de datos. |
| `sandboxName` | La zona protegida en la que se configura la caducidad de este conjunto de datos. |
| `displayName` | El nombre para mostrar de la configuración de caducidad del conjunto de datos. |
| `description` | Descripción de la configuración de caducidad del conjunto de datos. |
| `imsOrg` | El ID de organización asociado con esta configuración. |
| `status` | El estado actual de la configuración de caducidad del conjunto de datos.<br>Uno de: `pending`, `executing`, `cancelled`, `completed`. |
| `expiry` | La marca de tiempo de caducidad programada para el conjunto de datos. |
| `updatedAt` | La marca de tiempo de la actualización más reciente. |
| `updatedBy` | El identificador y el correo electrónico del usuario o servicio que actualizó la configuración de caducidad del conjunto de datos por última vez. |

{style="table-layout:auto"}

Una respuesta incorrecta devolverá un estado HTTP 404 (no encontrado) si no existe dicha caducidad del conjunto de datos.

## Cancelar una caducidad del conjunto de datos {#delete}

Cancele una configuración de caducidad del conjunto de datos pendiente realizando una petición DELETE a `/ttl/{ID}`.

>[!NOTE]
>
>Solo se pueden cancelar las caducidades del conjunto de datos en el estado `pending`. Si se intenta cancelar una caducidad que ya es `executing`, `completed` o `cancelled`, se devolverá HTTP 400 (Solicitud incorrecta).

**Formato de API**

```http
DELETE /ttl/{ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{ID}` | El identificador único de la configuración de caducidad del conjunto de datos. Puede proporcionar una ID de caducidad del conjunto de datos o una ID de conjunto de datos. |

{style="table-layout:auto"}

**Solicitud**

La siguiente solicitud cancela la caducidad de un conjunto de datos con el ID `SD-d4a7d918-283b-41fd-bfe1-4e730a613d21`:

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/hygiene/ttl/SD-d4a7d918-283b-41fd-bfe1-4e730a613d21 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 (OK) y la configuración de caducidad del conjunto de datos cancelada. Observe que el atributo `status` de la caducidad está establecido en `cancelled`.

```json
{
  "ttlId": "SD-d4a7d918-283b-41fd-bfe1-4e730a613d21",
  "datasetId": "5a9e2c68d3b24f03b55a91ce",
  "datasetName": "Acme_Customer_Data",
  "sandboxName": "acme-prod",
  "displayName": "Customer Dataset Expiry Rule",
  "description": "Cancelled expiry configuration for Acme customer dataset",
  "imsOrg": "C9D8E7F6A5B41234567890AB@AcmeOrg",
  "status": "cancelled",
  "expiry": "2032-02-28T00:00:00Z",
  "updatedAt": "2032-01-15T08:27:31.000Z",
  "updatedBy": "s.clegane@acme.com <s.clegane@acme.com> 5A9E2C68D3B24F03B55A91CE@acme.com"
}
```

| Propiedad | Descripción |
|---|---|
| `ttlId` | El identificador único de la configuración de caducidad del conjunto de datos eliminado. |
| `datasetId` | El identificador único del conjunto de datos. |
| `datasetName` | Nombre del conjunto de datos. |
| `sandboxName` | Zona protegida donde se configura la caducidad de este conjunto de datos. |
| `displayName` | El nombre para mostrar de la configuración de caducidad del conjunto de datos. |
| `description` | Descripción de la configuración de caducidad del conjunto de datos. |
| `imsOrg` | El identificador único de organización asociado con esta configuración. |
| `status` | El estado actual de la configuración de caducidad del conjunto de datos.<br>Uno de: `pending`, `executing`, `cancelled`, `completed`. |
| `expiry` | La marca de tiempo de caducidad programada para el conjunto de datos. |
| `updatedAt` | La marca de tiempo de la actualización más reciente. |
| `updatedBy` | El identificador y el correo electrónico del usuario o servicio que actualizó la configuración de caducidad del conjunto de datos por última vez. |

**Ejemplo 400 (Solicitud incorrecta) respuesta**

Se produce un error 400 al intentar cancelar un conjunto de datos que tiene una configuración de caducidad de `executing`, `completed` o `cancelled`.

```json
{
  "type": "http://ns.adobe.com/aep/errors/HYGN-3102-400",
  "title": "The requested dataset already has an existing expiration. Additional detail: A TTL already exists for datasetId=686e9ca25ef7462aefe72c93",
  "status": 400,
  "report": {
    "tenantInfo": {
      "sandboxName": "prod",
      "sandboxId": "not-applicable",
      "imsOrgId": "{IMS_ORG_ID}"
    },
    "additionalContext": {
      "Invoking Client ID": "acp_privacy_hygiene"
    }
  },
  "error-chain": [
    {
      "serviceId": "HYGN",
      "errorCode": "HYGN-3102-400",
      "invokingServiceId": "acp_privacy_hygiene",
      "unixTimeStampMs": 1754408150394
    }
  ]
}
```

>[!NOTE]
>
>Se produce un error 404 al intentar cancelar una caducidad del conjunto de datos que ya es `completed` o `cancelled`.

## Apéndice

### Parámetros de consulta aceptados {#query-params}

En la tabla siguiente se describen los parámetros de consulta disponibles al [enumerar caducidades del conjunto de datos](#list):

>[!NOTE]
>
>Los parámetros `description`, `displayName` y `datasetName` contienen la capacidad de búsqueda de valores LIKE. Esto significa que puede encontrar caducidades de conjuntos de datos programados llamados: &quot;Name123&quot;, &quot;Name183&quot;, &quot;DisplayName1234&quot; buscando la cadena &quot;Name1&quot;.

| Parámetro | Descripción | Ejemplo |
| --- | --- | --- |
| `author` | Utilice el parámetro de consulta `author` para encontrar a la persona que actualizó recientemente la caducidad del conjunto de datos. Si no se ha realizado ninguna actualización desde su creación, coincidirá con el creador original de la caducidad. Este parámetro coincide con las caducidades en las que el campo `created_by` corresponde a la cadena de búsqueda.<br>Si la cadena de búsqueda empieza por `LIKE` o `NOT LIKE`, el resto se trata como un patrón de búsqueda SQL. De lo contrario, toda la cadena de búsqueda se tratará como una cadena literal que debe coincidir exactamente con todo el contenido de un campo `created_by`. | `author=LIKE %john%`, `author=John Q. Public` |
| `datasetId` | Coincide con las caducidades que se aplican a un conjunto de datos específico. | `datasetId=62b3925ff20f8e1b990a7434` |
| `datasetName` | Coincide con las caducidades cuyo nombre de conjunto de datos contiene la cadena de búsqueda proporcionada. La coincidencia distingue entre mayúsculas y minúsculas. | `datasetName=Acme` |
| `description` |   | `description=Handle expiration of Acme information through the end of 2024.` |
| `displayName` | Coincide con las caducidades cuyo nombre para mostrar contiene la cadena de búsqueda proporcionada. La coincidencia distingue entre mayúsculas y minúsculas. | `displayName=License Expiry` |
| `executedDate` / `executedFromDate` / `executedToDate` | Filtra los resultados en función de una fecha de ejecución exacta, una fecha de finalización para la ejecución o una fecha de inicio para la ejecución. Se utilizan para recuperar datos o registros asociados a la ejecución de una operación en una fecha específica, antes de una fecha determinada o después de una fecha determinada. | `executedDate=2023-02-05T19:34:40.383615Z` |
| `expiryDate` | Coincide con las caducidades que se produjeron en la ventana de 24 horas de la fecha especificada. | `2024-01-01` |
| `expiryToDate` / `expiryFromDate` | Coincide con las caducidades que se van a ejecutar o que ya se han ejecutado durante el intervalo especificado. | `expiryFromDate=2099-01-01&expiryToDate=2100-01-01` |
| `limit` | Un entero entre 1 y 100 que indica el número máximo de caducidades que se van a devolver. Valor predeterminado 25. | `limit=50` |
| `orderBy` | El parámetro de consulta `orderBy` especifica el orden de clasificación de los resultados devueltos por la API. Utilícelo para organizar los datos en función de uno o varios campos, ya sea en orden ascendente (ASC) o descendente (DESC). Utilice el prefijo + o - para indicar ASC y DESC, respectivamente. Se aceptan los siguientes valores: `displayName`, `description`, `datasetName`, `id`, `updatedBy`, `updatedAt`, `expiry`, `status`. | `-datasetName` |
| `orgId` | Coincide con las caducidades de los conjuntos de datos cuyo ID de organización coincide con el del parámetro. Este valor toma como valor predeterminado el de los encabezados `x-gw-ims-org-id` y se omite a menos que la solicitud proporcione un token de servicio. | `orgId=885737B25DC460C50A49411B@AdobeOrg` |
| `page` | Un entero que indica qué página de caducidades se va a devolver. | `page=3` |
| `sandboxName` | Coincide con las caducidades del conjunto de datos cuyo nombre de zona protegida coincide exactamente con el argumento. El valor predeterminado es el nombre de la zona protegida en el encabezado `x-sandbox-name` de la solicitud. Use `sandboxName=*` para incluir las caducidades del conjunto de datos de todas las zonas protegidas. | `sandboxName=dev1` |
| `search` | Coincide con caducidades en las que la cadena especificada coincide exactamente con el identificador de caducidad o está **contenida** en cualquiera de estos campos:<br><ul><li>autor</li><li>nombre para mostrar</li><li>descripción</li><li>nombre para mostrar</li><li>nombre del conjunto de datos</li></ul> | `search=TESTING` |
| `status` | Una lista de estados separados por comas. Cuando se incluye, la respuesta coincide con las caducidades del conjunto de datos cuyo estado actual está entre los enumerados. | `status=pending,cancelled` |
| `ttlId` | Coincide la solicitud de caducidad con el ID determinado. | `ttlID=SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f` |
| `updatedDate` | Coincide con las caducidades actualizadas en la ventana de 24 horas de la fecha especificada. | `2024-01-01` |
| `updatedToDate` / `updatedFromDate` | Coincide con las caducidades actualizadas en la ventana de 24 horas a partir de la hora indicada.<br><br>Se considera que una caducidad está actualizada en cada edición, incluso cuando se crea, cancela o ejecuta. | `updatedDate=2022-01-01` |

{style="table-layout:auto"}

