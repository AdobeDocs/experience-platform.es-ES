---
title: Punto final de API de caducidad del conjunto de datos
description: El extremo /ttl de la API de higiene de datos le permite programar la caducidad de los conjuntos de datos en Adobe Experience Platform.
exl-id: fbabc2df-a79e-488c-b06b-cd72d6b9743b
source-git-commit: 566f1b6478cd0de0691cfb2301d5b86fbbfece52
workflow-type: tm+mt
source-wordcount: '1402'
ht-degree: 3%

---

# Extremo de caducidad del conjunto de datos

El `/ttl` Este extremo de la API de higiene de datos le permite programar fechas de caducidad para conjuntos de datos en Adobe Experience Platform.

La caducidad de un conjunto de datos es solo una operación de eliminación con retraso programado. El conjunto de datos no está protegido mientras tanto, por lo que puede eliminarse por otros medios antes de que caduque.

>[!NOTE]
>
>Aunque la caducidad se especifica como un instante de tiempo específico, puede haber hasta 24 horas de retraso después de la caducidad antes de que se inicie la eliminación real. Una vez iniciada la eliminación, pueden pasar hasta siete días antes de que se hayan eliminado todos los seguimientos del conjunto de datos de los sistemas de Platform.

En cualquier momento antes de que se inicie realmente la eliminación del conjunto de datos, puede cancelar la caducidad o modificar su hora de déclencheur. Después de cancelar la caducidad de un conjunto de datos, puede volver a abrirlo estableciendo una nueva caducidad.

Una vez iniciada la eliminación del conjunto de datos, su trabajo de caducidad se marcará como `executing`, y no puede modificarse más. El propio conjunto de datos puede recuperarse durante un máximo de siete días, pero solo a través de un proceso manual iniciado a través de una solicitud de servicio de Adobe. A medida que se ejecuta la solicitud, el lago de datos, el servicio de identidad y el perfil del cliente en tiempo real comienzan procesos independientes para eliminar el contenido del conjunto de datos de sus respectivos servicios. Una vez eliminados los datos de los tres servicios, la caducidad se marca como `executed`.

>[!WARNING]
>
>Si un conjunto de datos está configurado para caducar, debe cambiar manualmente los flujos de datos que puedan estar introduciendo datos en ese conjunto de datos para que los flujos de trabajo descendentes no se vean afectados negativamente.

## Introducción

El extremo utilizado en esta guía forma parte de la API de higiene de datos. Antes de continuar, consulte la [descripción general](./overview.md) para obtener vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios para realizar correctamente llamadas a cualquier API de Experience Platform.

## Enumerar caducidades del conjunto de datos {#list}

Puede enumerar todas las caducidades de los conjuntos de datos de su organización realizando una solicitud de GET.

**Formato de API**

```http
GET /ttl?{QUERY_PARAMETERS}
```

| Parámetro | Descripción |
| --- | --- |
| `{QUERY_PARAMETERS}` | Una lista de parámetros de consulta opcionales, con varios parámetros separados por `&` caracteres. Los parámetros comunes incluyen `size` y `page` para fines de paginación. Para obtener una lista completa de los parámetros de consulta admitidos, consulte la [sección del apéndice](#query-params). |

{style="table-layout:auto"}

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl?updatedToDate=2021-08-01&author=LIKE%Jane Doe%25 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta enumera las caducidades resultantes del conjunto de datos. El siguiente ejemplo se ha truncado para el espacio.

```json
{
  "totalRecords": 3,
  "ttlDetails": [
    {
      "status": "completed",
      "workorderId": "SDc17a9501345c4997878c1383c475a77b",
      "imsOrgId": "885737B25DC460C50A49411B@AdobeOrg",
      "datasetId": "f440ac301c414bf1b6ba419162866346",
      "expiry": "2021-07-07T13:14:15Z",
      "updatedAt": "2021-07-07T13:14:15Z",
      "updatedBy": "Jane Doe <jane.doe@example.com> d741b5b877bf47cf@AdobeId"
    },
    {
      "status": "pending",
      "workorderId": "SD8ef60b33dbed444fb81861cced5da10b",
      "imsOrgId": "885737B25DC460C50A49411B@AdobeOrg",
      "datasetId": "80f0d38820a74879a2c5be82e38b1a94",
      "expiry": "2099-02-02T00:00:00Z",
      "updatedAt": "2021-02-02T13:00:00Z",
      "updatedBy": "John Q. Public <jqp@example.com> 93220281bad34ed0@AdobeId"
    },
    {
      "status": "pending",
      "workorderId": "SD2140ad4eaf1f47a1b24c05cce53e303e",
      "imsOrgId": "885737B25DC460C50A49411B@AdobeOrg",
      "datasetId": "9e63f9b25896416ba811657678b4fcb7",
      "expiry": "2099-01-01T00:00:00Z",
      "updatedAt": "2021-01-01T13:00:00Z",
      "updatedBy": "Jane Doe <jane.doe@example.com> d741b5b877bf47cf@AdobeId"
    }
  ]
}
```

| Propiedad | Descripción |
| --- | --- |
| `totalRecords` | Recuento de caducidades del conjunto de datos que coincidieron con los parámetros de la llamada a la lista. |
| `ttlDetails` | Contiene los detalles de las caducidades devueltas del conjunto de datos. Para obtener más información sobre las propiedades de la caducidad de un conjunto de datos, consulte la sección de respuesta para realizar una [llamada de búsqueda](#lookup). |

{style="table-layout:auto"}

## Búsqueda de una caducidad del conjunto de datos {#lookup}

Puede buscar una caducidad del conjunto de datos mediante una solicitud de GET.

**Formato de API**

```http
GET /ttl/{DATASET_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{DATASET_ID}` | El ID del conjunto de datos cuya caducidad desea buscar. |

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
    "workorderId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
    "datasetId": "62759f2ede9e601b63a2ee14",
    "imsOrg": "{ORG_ID}",
    "status": "pending",
    "expiry": "2023-12-31T23:59:59Z",
    "updatedAt": "2022-05-11T15:12:40.393115Z",
    "updatedBy": "{USER_ID}",
    "displayName": "Example Dataset Expiration Request",
    "description": "A dataset expiration request that will execute at the end of 2023"
}
```

| Propiedad | Descripción |
| --- | --- |
| `workorderId` | ID de caducidad del conjunto de datos. |
| `datasetId` | El ID del conjunto de datos al que se aplica esta caducidad. |
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

## Crear o actualizar una caducidad del conjunto de datos {#create-or-update}

Puede crear o actualizar una fecha de caducidad para un conjunto de datos mediante una solicitud del PUT.

**Formato de API**

```http
PUT /ttl/{DATASET_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{DATASET_ID}` | El ID del conjunto de datos para el que desea programar una caducidad. |

**Solicitud**

La siguiente solicitud programa un conjunto de datos `5b020a27e7040801dedbf46e` para su eliminación a finales de 2022 (hora del meridiano de Greenwich). Si no se encuentra ninguna caducidad existente para el conjunto de datos, se crea una nueva caducidad. Si el conjunto de datos ya tiene una caducidad pendiente, esa caducidad se actualiza con el nuevo `expiry` valor.

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/ttl/5b020a27e7040801dedbf46e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "expiry": "2022-12-31T23:59:59Z",
        "displayName": "Example Expiration Request",
        "description": "Cleanup identities required by JIRA request 12345 across all datasets in the prod sandbox."
      }'
```

| Propiedad | Descripción |
| --- | --- |
| `expiry` | Una marca de tiempo ISO 8601 para cuándo se eliminará el conjunto de datos. |
| `displayName` | Un nombre para mostrar para la solicitud de caducidad. |
| `description` | Una descripción opcional para la solicitud de caducidad. |

{style="table-layout:auto"}

**Respuesta**

Una respuesta correcta devuelve los detalles de la caducidad del conjunto de datos, con el estado HTTP 200 (OK) si se actualizó una caducidad preexistente, o 201 (Created) si no había una caducidad preexistente.

```json
{
    "workorderId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
    "datasetId": "5b020a27e7040801dedbf46e",
    "imsOrg": "{ORG_ID}",
    "status": "pending",
    "expiry": "2032-12-31T23:59:59Z",
    "updatedAt": "2022-05-09T22:38:40.393115Z",
    "updatedBy": "{USER_ID}",
    "displayName": "Example Expiration Request",
    "description": "Cleanup identities required by JIRA request 12345 across all datasets in the prod sandbox."
}
```

| Propiedad | Descripción |
| --- | --- |
| `workorderId` | ID de caducidad del conjunto de datos. |
| `datasetId` | El ID del conjunto de datos al que se aplica esta caducidad. |
| `imsOrg` | ID de su organización. |
| `status` | El estado actual de caducidad del conjunto de datos. |
| `expiry` | La fecha y hora programadas en las que se eliminará el conjunto de datos. |
| `updatedAt` | Una marca de tiempo de la última vez que se actualizó la caducidad. |
| `updatedBy` | El usuario que actualizó la caducidad por última vez. |

{style="table-layout:auto"}

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
| `{EXPIRATION_ID}` | El `workorderId` de la caducidad del conjunto de datos que desea cancelar. |

{style="table-layout:auto"}

**Solicitud**

La siguiente solicitud cancela una caducidad del conjunto de datos con ID `SD5cfd7a11b25543a9bcd9ef647db3d8df`:

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/hygiene/ttl/SD5cfd7a11b25543a9bcd9ef647db3d8df \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 204 (sin contenido) y el de la caducidad `status` el atributo se establece en `cancelled`.

## Recuperar el historial de estado de caducidad de un conjunto de datos

Puede buscar el historial de estado de caducidad de un conjunto de datos específico mediante el parámetro de consulta `include=history` en una solicitud de consulta. El resultado incluye información sobre la creación de la caducidad del conjunto de datos, cualquier actualización que se haya aplicado y su cancelación o ejecución (si corresponde).

**Formato de API**

```http
GET /ttl/{DATASET_ID}?include=history
```

| Parámetro | Descripción |
| --- | --- |
| `{DATASET_ID}` | El ID del conjunto de datos cuyo historial de caducidad desea buscar. |

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
  "workorderId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
  "datasetId": "62759f2ede9e601b63a2ee14",
  "datasetName": "Example Dataset",
  "sandboxName": "prod",
  "displayName": "Expiration Request 123",
  "description": "Expiration Request 123 Description",
  "imsOrg": "{ORG_ID}",
  "status": "cancelled",
  "expiry": "2022-05-09T23:47:30.071186Z",
  "updatedAt": "2022-05-09T23:47:30.071186Z",
  "updatedBy": "{USER_ID}",
  "history": [
    {
      "status": "created",
      "expiry": "2032-12-31T23:59:59Z",
      "updatedAt": "2022-05-09T22:38:40.393115Z",
      "updatedBy": "{USER_ID}"
    },
    {
      "status": "updated",
      "expiry": "2032-12-31T23:59:59Z",
      "updatedAt": "2022-05-09T22:41:46.731002Z",
      "updatedBy": "{USER_ID}"
    },
    {
      "status": "cancelled",
      "expiry": "2022-05-09T23:47:30.071186Z",
      "updatedAt": "2022-05-09T23:47:30.071186Z",
      "updatedBy": "{USER_ID}"
    }
  ]
}
```

| Propiedad | Descripción |
| --- | --- |
| `workorderId` | ID de caducidad del conjunto de datos. |
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

| Parámetro | Descripción | Ejemplo |
| --- | --- | --- |
| `size` | Un entero entre 1 y 100 que indica el número máximo de caducidades que se van a devolver. Valor predeterminado 25. | `size=50` |
| `page` | Un entero que indica qué página de caducidades se va a devolver. | `page=3` |
| `orgId` | Coincide con las caducidades de los conjuntos de datos cuyo ID de organización coincide con el del parámetro. Este valor predeterminado es el de `x-gw-ims-org-id` y se omite a menos que la solicitud proporcione un token de servicio. | `orgId=885737B25DC460C50A49411B@AdobeOrg` |
| `status` | Una lista de estados separados por comas. Cuando se incluye, la respuesta coincide con las caducidades del conjunto de datos cuyo estado actual está entre los enumerados. | `status=pending,cancelled` |
| `author` | Coincide con caducidades cuya `created_by` coincide con la cadena de búsqueda. Si la cadena de búsqueda empieza por `LIKE` o `NOT LIKE`, el resto se trata como un patrón de búsqueda SQL. De lo contrario, toda la cadena de búsqueda se trata como una cadena literal que debe coincidir exactamente con todo el contenido de un `created_by` field. | `author=LIKE %john%` |
| `sandboxName` | Coincide con las caducidades del conjunto de datos cuyo nombre de zona protegida coincide exactamente con el argumento. El valor predeterminado es el nombre de la zona protegida en el `x-sandbox-name` encabezado. Uso `sandboxName=*` para incluir las caducidades del conjunto de datos de todas las zonas protegidas. | `sandboxName=dev1` |
| `datasetId` | Coincide con las caducidades que se aplican a un conjunto de datos específico. | `datasetId=62b3925ff20f8e1b990a7434` |
| `createdDate` | Coincide con las caducidades creadas en la ventana de 24 horas a partir de la hora indicada.<br><br>Tenga en cuenta que las fechas sin una hora (como `2021-12-07`) representan la fecha y hora al principio de ese día. Por lo tanto, `createdDate=2021-12-07` hace referencia a cualquier caducidad creada el 7 de diciembre de 2021, desde `00:00:00` mediante `23:59:59.999999999` (UTC). | `createdDate=2021-12-07` |
| `createdFromDate` | Coincide con las caducidades creadas en la hora indicada o posteriormente. | `createdFromDate=2021-12-07T00:00:00Z` |
| `createdToDate` | Coincide con las caducidades creadas en la hora indicada o antes. | `createdToDate=2021-12-07T23:59:59.999999999Z` |
| `updatedDate` / `updatedToDate` / `updatedFromDate` | Like `createdDate` / `createdFromDate` / `createdToDate`, pero coincide con la hora de actualización de una caducidad del conjunto de datos en lugar de la hora de creación.<br><br>Una caducidad se considera actualizada en cada edición, incluso cuando se crea, cancela o ejecuta. | `updatedDate=2022-01-01` |
| `cancelledDate` / `cancelledToDate` / `cancelledFromDate` | Coincide con las caducidades que se cancelaron en cualquier momento en el intervalo indicado. Esto se aplica incluso si la caducidad se volvió a abrir más tarde (estableciendo una nueva caducidad para el mismo conjunto de datos). | `updatedDate=2022-01-01` |
| `completedDate` / `completedToDate` / `completedFromDate` | Coincide con las caducidades completadas durante el intervalo especificado. | `completedToDate=2021-11-11-06:00` |
| `expiryDate` / `expiryToDate` / `expiryFromDate` | Coincide con las caducidades que se van a ejecutar o que ya se han ejecutado durante el intervalo especificado. | `expiryFromDate=2099-01-01&expiryToDate=2100-01-01` |

{style="table-layout:auto"}
