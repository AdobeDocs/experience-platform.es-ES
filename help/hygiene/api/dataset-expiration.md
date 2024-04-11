---
title: Punto final de API de caducidad del conjunto de datos
description: El extremo /ttl de la API de higiene de datos le permite programar la caducidad de los conjuntos de datos en Adobe Experience Platform.
role: Developer
exl-id: fbabc2df-a79e-488c-b06b-cd72d6b9743b
source-git-commit: 0c6e6d23be42b53eaf1fca365745e6502197c329
workflow-type: tm+mt
source-wordcount: '2141'
ht-degree: 2%

---

# Extremo de caducidad del conjunto de datos

El `/ttl` Este extremo de la API de higiene de datos le permite programar fechas de caducidad para conjuntos de datos en Adobe Experience Platform.

La caducidad de un conjunto de datos es solo una operación de eliminación con retraso programado. El conjunto de datos no está protegido mientras tanto, por lo que puede eliminarse por otros medios antes de que caduque.

>[!NOTE]
>
>Aunque la caducidad se especifica como un instante de tiempo específico, puede haber hasta 24 horas de retraso después de la caducidad antes de que se inicie la eliminación real. Una vez iniciada la eliminación, pueden pasar hasta siete días antes de que se hayan eliminado todos los seguimientos del conjunto de datos de los sistemas de Platform.

En cualquier momento antes de que se inicie realmente la eliminación del conjunto de datos, puede cancelar la caducidad o modificar su hora de déclencheur. Después de cancelar la caducidad de un conjunto de datos, puede volver a abrirlo estableciendo una nueva caducidad.

Una vez iniciada la eliminación del conjunto de datos, su trabajo de caducidad se marcará como `executing`, y no puede modificarse más. El propio conjunto de datos puede recuperarse durante un máximo de siete días, pero solo a través de un proceso manual iniciado a través de una solicitud de servicio de Adobe. A medida que se ejecuta la solicitud, el lago de datos, el servicio de identidad y el perfil del cliente en tiempo real comienzan procesos independientes para eliminar el contenido del conjunto de datos de sus respectivos servicios. Una vez eliminados los datos de los tres servicios, la caducidad se marca como `completed`.

>[!WARNING]
>
>Si un conjunto de datos está configurado para caducar, debe cambiar manualmente los flujos de datos que puedan estar introduciendo datos en ese conjunto de datos para que los flujos de trabajo descendentes no se vean afectados negativamente.

## Introducción

El extremo utilizado en esta guía forma parte de la API de higiene de datos. Antes de continuar, consulte la [Guía de API](./overview.md) para obtener información sobre los encabezados necesarios para operaciones de CRUD, mensajes de error, colecciones de Postman y cómo leer llamadas de API de ejemplo.

>[!IMPORTANT]
>
>Al realizar llamadas a la API de higiene de datos, debe utilizar el -H `x-sandbox-name: {SANDBOX_NAME}` encabezado.

## Enumerar caducidades del conjunto de datos {#list}

Puede enumerar todas las caducidades de los conjuntos de datos de su organización realizando una solicitud de GET. Los parámetros de consulta se pueden utilizar para filtrar la respuesta y obtener los resultados adecuados.

**Formato de API**

```http
GET /ttl?{QUERY_PARAMETERS}
```

| Parámetro | Descripción |
| --- | --- |
| `{QUERY_PARAMETERS}` | Una lista de parámetros de consulta opcionales, con varios parámetros separados por `&` caracteres. Los parámetros comunes incluyen `limit` y `page` para fines de paginación. Para obtener una lista completa de los parámetros de consulta admitidos, consulte la [sección del apéndice](#query-params). |

{style="table-layout:auto"}

**Solicitud**

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
>El `ttlId` en la respuesta también se denomina la `{DATASET_EXPIRATION_ID}`. Ambos hacen referencia al identificador único para la caducidad del conjunto de datos.

```json
{
  "results": [
    {
      "ttlId": "SD-b16c8b48-a15a-45c8-9215-587ea89369bf",
      "datasetId": "629bd9125b31471b2da7645c",
      "datasetName": "Sample Acme dataset",
      "sandboxName": "hygiene-beta",
      "imsOrg": "A2A5*EF06164773A8A49418C@AdobeOrg",
      "status": "pending",
      "expiry": "2050-01-01T00:00:00Z",
      "updatedAt": "2023-06-09T16:52:44.136028Z",
      "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e"
    }
  ],
  "current_page": 0,
  "total_pages": 1,
  "total_count": 1
}
```

| Propiedad | Descripción |
| --- | --- |
| `total_count` | Recuento de caducidades del conjunto de datos que coincidieron con los parámetros de la llamada a la lista. |
| `results` | Contiene los detalles de las caducidades devueltas del conjunto de datos. Para obtener más información sobre las propiedades de la caducidad de un conjunto de datos, consulte la sección de respuesta para realizar una [llamada de búsqueda](#lookup). |

{style="table-layout:auto"}

## Búsqueda de una caducidad del conjunto de datos {#lookup}

Para buscar la caducidad de un conjunto de datos, realice una solicitud de GET con el `{DATASET_ID}` o el `{DATASET_EXPIRATION_ID}`.

>[!IMPORTANT]
>
>El `{DATASET_EXPIRATION_ID}` se denomina la variable `ttlId` en la respuesta. Ambos hacen referencia al identificador único para la caducidad del conjunto de datos.

**Formato de API**

```http
GET /ttl/{DATASET_ID}?include=history
GET /ttl/{DATASET_EXPIRATION_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{DATASET_ID}` | El ID del conjunto de datos cuya caducidad desea buscar. |
| `{DATASET_EXPIRATION_ID}` | ID de caducidad del conjunto de datos. |

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
    "imsOrg": "A2A5*EF06164773A8A49418C@AdobeOrg",
    "status": "pending",
    "expiry": "2024-12-31T23:59:59Z",
    "updatedAt": "2024-05-11T15:12:40.393115Z",
    "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e",
    "displayName": "Delete Acme Data before 2025",
    "description": "The Acme information in this dataset is licensed for our use through the end of 2024."
}
```

| Propiedad | Descripción |
| --- | --- |
| `ttlId` | ID de caducidad del conjunto de datos. |
| `datasetId` | El ID del conjunto de datos al que se aplica esta caducidad. |
| `datasetName` | El nombre para mostrar del conjunto de datos al que se aplica esta caducidad. |
| `sandboxName` | El nombre de la zona protegida en la que se encuentra el conjunto de datos de destinatario. |
| `imsOrg` | ID de su organización. |
| `status` | El estado actual de caducidad del conjunto de datos. |
| `expiry` | La fecha y hora programadas en las que se eliminará el conjunto de datos. |
| `updatedAt` | Una marca de tiempo de la última vez que se actualizó la caducidad. |
| `updatedBy` | El usuario que actualizó la caducidad por última vez. |
| `displayName` | El nombre para mostrar de la solicitud de caducidad. |
| `description` | Una descripción para la solicitud de caducidad. |

{style="table-layout:auto"}

### Etiquetas de caducidad del catálogo

Al usar el [API de catálogo](../../catalog/api/getting-started.md) para buscar los detalles del conjunto de datos, si este tiene una caducidad activa, se enumerará en `tags.adobe/hygiene/ttl`.

El siguiente JSON representa una respuesta truncada para los detalles de un conjunto de datos del catálogo, que tiene un valor de caducidad de `32503680000000`. El valor de la etiqueta codifica la caducidad como un número entero de milisegundos desde el comienzo de la época Unix.

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

Para garantizar que los datos se eliminen del sistema después de un periodo especificado, programe una caducidad para un conjunto de datos específico proporcionando el ID del conjunto de datos y la fecha y hora de caducidad en formato ISO 8601.

Para crear una caducidad del conjunto de datos, realice una solicitud de POST como se muestra a continuación y proporcione los valores mencionados a continuación dentro de la carga útil.

**Formato de API**

```http
POST /ttl
```

**Solicitud**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/hygiene/ttl \
  -H `Authorization: Bearer {ACCESS_TOKEN}`
  -H `x-gw-ims-org-id: {ORG_ID}`
  -H `x-api-key: {API_KEY}`
  -H `Accept: application/json`
  -d {
      "datasetId": "5b020a27e7040801dedbf46e",
      "expiry": "2030-12-31T23:59:59Z"
      "displayName": "Delete Acme Data before 2025",
      "description": "The Acme information in this dataset is licensed for our use through the end of 2024."
      }
```

| Propiedad | Descripción |
| --- | --- |
| `datasetId` | **Requerido** El ID del conjunto de datos de destinatario para el que desea programar una caducidad. |
| `expiry` | **Requerido** Una fecha y hora en formato ISO 8601. Si la cadena no tiene un desplazamiento explícito de zona horaria, se asume que la zona horaria es UTC. La duración de los datos dentro del sistema se establece según el valor de caducidad proporcionado.<br>Nota:<ul><li>La solicitud fallará si ya existe una caducidad del conjunto de datos para él.</li><li>Esta fecha y hora deben ser al menos **24 horas en el futuro**.</li></ul> |
| `displayName` | Un nombre para mostrar opcional para la solicitud de caducidad del conjunto de datos. |
| `description` | Una descripción opcional para la solicitud de caducidad. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 201 (Creado) y el nuevo estado de caducidad del conjunto de datos.

```json
{
  "ttlId":       "SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f",
  "datasetId":   "5b020a27e7040801dedbf46e",
  "datasetName": "Acme licensed data",
  "sandboxName": "prod",
  "imsOrg":      "{ORG_ID}",
  "status":      "pending",
  "expiry":      "2030-12-31T23:59:59Z",
  "updatedAt":   "2021-08-19T11:14:16Z",
  "updatedBy":   "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e",
  "displayName": "Delete Acme Data before 2031",
  "description": "The Acme information in this dataset is licensed for our use through the end of 2030."
}
```

| Propiedad | Descripción |
| --- | --- |
| `ttlId` | ID de caducidad del conjunto de datos. |
| `datasetId` | El ID del conjunto de datos al que se aplica esta caducidad. |
| `datasetName` | El nombre para mostrar del conjunto de datos al que se aplica esta caducidad. |
| `sandboxName` | El nombre de la zona protegida en la que se encuentra el conjunto de datos de destinatario. |
| `imsOrg` | ID de su organización. |
| `status` | El estado actual de caducidad del conjunto de datos. |
| `expiry` | La fecha y hora programadas en las que se eliminará el conjunto de datos. |
| `updatedAt` | Una marca de tiempo de la última vez que se actualizó la caducidad. |
| `updatedBy` | El usuario que actualizó la caducidad por última vez. |
| `displayName` | Un nombre para mostrar para la solicitud de caducidad. |
| `description` | Descripción de la solicitud de caducidad. |

Se produce un estado HTTP 400 (Solicitud incorrecta) si ya existe una caducidad del conjunto de datos para el conjunto de datos. Una respuesta incorrecta devolverá un estado HTTP 404 (no encontrado) si no existe dicha caducidad del conjunto de datos (o si no tiene acceso al conjunto de datos).

## Actualizar la caducidad de un conjunto de datos {#update}

Para actualizar una fecha de caducidad para un conjunto de datos, utilice una solicitud del PUT y la variable `ttlId`. Puede actualizar el `displayName`, `description`, y/o `expiry` información.

>[!NOTE]
>
>Si cambia la fecha y hora de caducidad, debe ser al menos 24 horas en el futuro. Este retraso obligatorio le ofrece la oportunidad de cancelar o volver a programar la caducidad y evitar la pérdida accidental de datos.

**Formato de API**

```http
PUT /ttl/{DATASET_EXPIRATION_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{DATASET_EXPIRATION_ID}` | El ID de la caducidad del conjunto de datos que desea cambiar. Nota: Esto se conoce como `ttlId` en la respuesta. |

**Solicitud**

La siguiente solicitud vuelve a programar la caducidad de un conjunto de datos `SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f` a finales de 2024 (hora del meridiano de Greenwich). Si se encuentra la caducidad del conjunto de datos existente, esa caducidad se actualiza con el nuevo `expiry` valor.

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/ttl/SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "expiry": "2024-12-31T23:59:59Z",
        "displayName": "Delete Acme Data before 2025",
        "description": "The Acme information in this dataset is licensed for our use through the end of 2024."
      }'
```

| Propiedad | Descripción |
| --- | --- |
| `expiry` | **Requerido** Una fecha y hora en formato ISO 8601. Si la cadena no tiene un desplazamiento explícito de zona horaria, se asume que la zona horaria es UTC. La duración de los datos dentro del sistema se establece según el valor de caducidad proporcionado. Cualquier marca de tiempo de caducidad anterior para el mismo conjunto de datos se reemplazará por el nuevo valor de caducidad que haya proporcionado. Esta fecha y hora deben ser al menos **24 horas en el futuro**. |
| `displayName` | Un nombre para mostrar para la solicitud de caducidad. |
| `description` | Una descripción opcional para la solicitud de caducidad. |

{style="table-layout:auto"}

**Respuesta**

Una respuesta correcta devuelve el nuevo estado de caducidad del conjunto de datos y un estado HTTP 200 (OK) si se actualizó una caducidad preexistente.

```json
{
    "ttlId": "SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f",
    "datasetId": "5b020a27e7040801dedbf46e",
    "imsOrg": "A2A5*EF06164773A8A49418C@AdobeOrg",
    "status": "pending",
    "expiry": "2024-12-31T23:59:59Z",
    "updatedAt": "2022-05-09T22:38:40.393115Z",
    "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e",
    "displayName": "Delete Acme Data before 2025",
    "description": "The Acme information in this dataset is licensed for our use through the end of 2024."
}
```

| Propiedad | Descripción |
| --- | --- |
| `ttlId` | ID de caducidad del conjunto de datos. |
| `datasetId` | El ID del conjunto de datos al que se aplica esta caducidad. |
| `imsOrg` | ID de su organización. |
| `status` | El estado actual de caducidad del conjunto de datos. |
| `expiry` | La fecha y hora programadas en las que se eliminará el conjunto de datos. |
| `updatedAt` | Una marca de tiempo de la última vez que se actualizó la caducidad. |
| `updatedBy` | El usuario que actualizó la caducidad por última vez. |

{style="table-layout:auto"}

Una respuesta incorrecta devolverá un estado HTTP 404 (no encontrado) si no existe dicha caducidad del conjunto de datos.

## Cancelar una caducidad del conjunto de datos {#delete}

Puede cancelar la caducidad de un conjunto de datos realizando una solicitud al DELETE.

>[!NOTE]
>
>Solo caducidades de conjuntos de datos que tengan el estado de `pending` se puede cancelar. Si se intenta cancelar una caducidad que se ha ejecutado o que ya se ha cancelado, se devuelve un error HTTP 404.

**Formato de API**

```http
DELETE /ttl/{EXPIRATION_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{EXPIRATION_ID}` | El `ttlId` de la caducidad del conjunto de datos que desea cancelar. |

{style="table-layout:auto"}

**Solicitud**

La siguiente solicitud cancela una caducidad del conjunto de datos con ID `SD-b16c8b48-a15a-45c8-9215-587ea89369bf`:

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/hygiene/ttl/SD-b16c8b48-a15a-45c8-9215-587ea89369bf \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 204 (sin contenido) y el de la caducidad `status` el atributo se establece en `cancelled`.

## Recuperar el historial de estado de caducidad de un conjunto de datos {#retrieve-expiration-history}

Para buscar el historial de estado de caducidad de un conjunto de datos específico, utilice el `{DATASET_ID}` y `include=history` parámetro de consulta en una solicitud de búsqueda. El resultado incluye información sobre la creación de la caducidad del conjunto de datos, cualquier actualización que se haya aplicado y su cancelación o ejecución (si corresponde). También puede utilizar la variable `{DATASET_EXPIRATION_ID}` para recuperar el historial de estado de caducidad del conjunto de datos.

**Formato de API**

```http
GET /ttl/{DATASET_ID}?include=history
GET /ttl/{DATASET_EXPIRATION_ID}?include=history
```

| Parámetro | Descripción |
| --- | --- |
| `{DATASET_ID}` | El ID del conjunto de datos cuyo historial de caducidad desea buscar. |
| `{DATASET_EXPIRATION_ID}` | ID de caducidad del conjunto de datos. Nota: Esto se conoce como `ttlId` en la respuesta. |

{style="table-layout:auto"}

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl/62759f2ede9e601b63a2ee14?include=history \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve los detalles de la caducidad del conjunto de datos, con un `history` matriz que proporciona los detalles de su `status`, `expiry`, `updatedAt`, y `updatedBy` atributos para cada una de sus actualizaciones registradas.

```json
{
  "ttlId": "SD-b16c8b48-a15a-45c8-9215-587ea89369bf",
  "datasetId": "62759f2ede9e601b63a2ee14",
  "datasetName": "Example Dataset",
  "sandboxName": "prod",
  "displayName": "Expiration Request 123",
  "description": "Expiration Request 123 Description",
  "imsOrg": "0FCC747E56F59C747F000101@AdobeOrg",
  "status": "cancelled",
  "expiry": "2022-05-09T23:47:30.071186Z",
  "updatedAt": "2022-05-09T23:47:30.071186Z",
  "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e",
  "history": [
    {
      "status": "created",
      "expiry": "2032-12-31T23:59:59Z",
      "updatedAt": "2022-05-09T22:38:40.393115Z",
      "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e"
    },
    {
      "status": "updated",
      "expiry": "2032-12-31T23:59:59Z",
      "updatedAt": "2022-05-09T22:41:46.731002Z",
      "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e"
    },
    {
      "status": "cancelled",
      "expiry": "2022-05-09T23:47:30.071186Z",
      "updatedAt": "2022-05-09T23:47:30.071186Z",
      "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e"
    }
  ]
}
```

| Propiedad | Descripción |
| --- | --- |
| `ttlId` | ID de caducidad del conjunto de datos. |
| `datasetId` | El ID del conjunto de datos al que se aplica esta caducidad. |
| `datasetName` | El nombre para mostrar del conjunto de datos al que se aplica esta caducidad. |
| `sandboxName` | El nombre de la zona protegida en la que se encuentra el conjunto de datos de destinatario. |
| `displayName` | El nombre para mostrar de la solicitud de caducidad. |
| `description` | Una descripción para la solicitud de caducidad. |
| `imsOrg` | ID de su organización. |
| `history` | Enumera el historial de actualizaciones para la caducidad como una matriz de objetos, cada uno de los cuales contiene el `status`, `expiry`, `updatedAt`, y `updatedBy` atributos para la caducidad en el momento de la actualización. |

{style="table-layout:auto"}

## Apéndice

### Parámetros de consulta aceptados {#query-params}

En la tabla siguiente se describen los parámetros de consulta disponibles cuando [enumerar caducidades del conjunto de datos](#list):

>[!NOTE]
>
>El `description`, `displayName`, y `datasetName` todos los parámetros contienen la capacidad de buscar por valores LIKE. Esto significa que puede encontrar caducidades de conjuntos de datos programados llamados: &quot;Name123&quot;, &quot;Name183&quot;, &quot;DisplayName1234&quot; buscando la cadena &quot;Name1&quot;.

| Parámetro | Descripción | Ejemplo |
| --- | --- | --- |
| `author` | Coincide con caducidades cuya `created_by` coincide con la cadena de búsqueda. Si la cadena de búsqueda empieza por `LIKE` o `NOT LIKE`, el resto se trata como un patrón de búsqueda SQL. De lo contrario, toda la cadena de búsqueda se trata como una cadena literal que debe coincidir exactamente con todo el contenido de un `created_by` field. | `author=LIKE %john%`, `author=John Q. Public` |
| `cancelledDate` / `cancelledToDate` / `cancelledFromDate` | Coincide con las caducidades que se cancelaron en cualquier momento en el intervalo indicado. Esto se aplica incluso si la caducidad se volvió a abrir más tarde (estableciendo una nueva caducidad para el mismo conjunto de datos). | `updatedDate=2022-01-01` |
| `completedDate` / `completedToDate` / `completedFromDate` | Coincide con las caducidades completadas durante el intervalo especificado. | `completedToDate=2021-11-11-06:00` |
| `createdDate` | Coincide con las caducidades creadas en la ventana de 24 horas a partir de la hora indicada.<br><br>Tenga en cuenta que las fechas sin una hora (como `2021-12-07`) representan la fecha y hora al principio de ese día. Por lo tanto, `createdDate=2021-12-07` hace referencia a cualquier caducidad creada el 7 de diciembre de 2021, desde `00:00:00` mediante `23:59:59.999999999` (UTC). | `createdDate=2021-12-07` |
| `createdFromDate` | Coincide con las caducidades creadas en la hora indicada o posteriormente. | `createdFromDate=2021-12-07T00:00:00Z` |
| `createdToDate` | Coincide con las caducidades creadas en la hora indicada o antes. | `createdToDate=2021-12-07T23:59:59.999999999Z` |
| `datasetId` | Coincide con las caducidades que se aplican a un conjunto de datos específico. | `datasetId=62b3925ff20f8e1b990a7434` |
| `datasetName` | Coincide con las caducidades cuyo nombre de conjunto de datos contiene la cadena de búsqueda proporcionada. La coincidencia distingue entre mayúsculas y minúsculas. | `datasetName=Acme` |
| `description` |   | `description=Handle expiration of Acme information through the end of 2024.` |
| `displayName` | Coincide con las caducidades cuyo nombre para mostrar contiene la cadena de búsqueda proporcionada. La coincidencia distingue entre mayúsculas y minúsculas. | `displayName=License Expiry` |
| `executedDate` / `executedFromDate` / `executedToDate` | Filtra los resultados en función de una fecha de ejecución exacta, una fecha de finalización para la ejecución o una fecha de inicio para la ejecución. Se utilizan para recuperar datos o registros asociados a la ejecución de una operación en una fecha específica, antes de una fecha determinada o después de una fecha determinada. | `executedDate=2023-02-05T19:34:40.383615Z` |
| `expiryDate` / `expiryToDate` / `expiryFromDate` | Coincide con las caducidades que se van a ejecutar o que ya se han ejecutado durante el intervalo especificado. | `expiryFromDate=2099-01-01&expiryToDate=2100-01-01` |
| `limit` | Un entero entre 1 y 100 que indica el número máximo de caducidades que se van a devolver. Valor predeterminado 25. | `limit=50` |
| `orderBy` | El `orderBy` parámetro de consulta especifica el orden de clasificación de los resultados devueltos por la API. Utilícelo para organizar los datos en función de uno o varios campos, ya sea en orden ascendente (ASC) o descendente (DESC). Utilice el prefijo + o - para indicar ASC y DESC, respectivamente. Se aceptan los siguientes valores: `displayName`, `description`, `datasetName`, `id`, `updatedBy`, `updatedAt`, `expiry`, `status`. | `-datasetName` |
| `orgId` | Coincide con las caducidades de los conjuntos de datos cuyo ID de organización coincide con el del parámetro. Este valor predeterminado es el de `x-gw-ims-org-id` y se omite a menos que la solicitud proporcione un token de servicio. | `orgId=885737B25DC460C50A49411B@AdobeOrg` |
| `page` | Un entero que indica qué página de caducidades se va a devolver. | `page=3` |
| `sandboxName` | Coincide con las caducidades del conjunto de datos cuyo nombre de zona protegida coincide exactamente con el argumento. El valor predeterminado es el nombre de la zona protegida en el `x-sandbox-name` encabezado. Uso `sandboxName=*` para incluir las caducidades del conjunto de datos de todas las zonas protegidas. | `sandboxName=dev1` |
| `search` | Coincide con caducidades en las que la cadena especificada coincide exactamente con el ID de caducidad o **contenido** en cualquiera de estos campos:<br><ul><li>autor</li><li>nombre para mostrar</li><li>descripción</li><li>nombre para mostrar</li><li>nombre del conjunto de datos</li></ul> | `search=TESTING` |
| `status` | Una lista de estados separados por comas. Cuando se incluye, la respuesta coincide con las caducidades del conjunto de datos cuyo estado actual está entre los enumerados. | `status=pending,cancelled` |
| `ttlId` | Coincide la solicitud de caducidad con el ID determinado. | `ttlID=SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f` |
| `updatedDate` / `updatedToDate` / `updatedFromDate` | Like `createdDate` / `createdFromDate` / `createdToDate`, pero coincide con la hora de actualización de una caducidad del conjunto de datos en lugar de la hora de creación.<br><br>Una caducidad se considera actualizada en cada edición, incluso cuando se crea, cancela o ejecuta. | `updatedDate=2022-01-01` |

{style="table-layout:auto"}

