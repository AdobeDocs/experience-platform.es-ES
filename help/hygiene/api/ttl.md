---
title: Punto final de API de DataSet Time-to-Live (TTL)
description: El extremo /ttl de la API de higiene de datos le permite programar mediante programación TTL de conjuntos de datos en Adobe Experience Platform.
exl-id: fbabc2df-a79e-488c-b06b-cd72d6b9743b
source-git-commit: 7f1e4bdf54314cab1f69619bcbb34216da94b17e
workflow-type: tm+mt
source-wordcount: '1313'
ht-degree: 7%

---

# Extremo de tiempo de vida (TTL) del conjunto de datos

>[!IMPORTANT]
>
>Actualmente, las funciones de higiene de datos de Adobe Experience Platform solo están disponibles para las organizaciones que han adquirido el Escudo de la salud.

La variable `/ttl` en la API de higiene de datos le permite programar protocolos de tiempo de vida (TTL) para conjuntos de datos en Adobe Experience Platform.

Un TTL de conjunto de datos es solo una operación de eliminación con retraso. El conjunto de datos no está protegido entre tanto, por lo que se puede eliminar por otros medios antes de que se alcance su caducidad.

>[!NOTE]
>
>Aunque la caducidad se especifica como un instante específico en el tiempo, puede haber hasta 24 horas de retraso después de la caducidad antes de iniciar la eliminación real. Una vez iniciada la eliminación, puede tardar hasta siete días en que se hayan eliminado todos los seguimientos del conjunto de datos de los sistemas de Platform.

En cualquier momento antes de que se inicie realmente la eliminación del conjunto de datos, puede cancelar el TTL o modificar su tiempo de déclencheur. Después de cancelar un TTL, puede volver a abrirlo configurando una nueva caducidad.

Una vez iniciada la eliminación del conjunto de datos, su TTL se marcará como `executing`y no puede modificarse. El conjunto de datos en sí puede recuperarse durante un máximo de siete días, pero solo a través de un proceso manual iniciado mediante una solicitud de servicio de Adobe.

## Primeros pasos

El extremo utilizado en esta guía forma parte de la API de higiene de datos. Antes de continuar, revise la [información general](./overview.md) para ver vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios para realizar llamadas correctamente a cualquier API de Experience Platform.

## Enumerar TTL de conjuntos de datos {#list}

Puede enumerar todo el TTL de conjuntos de datos para su organización realizando una solicitud de GET.

**Formato de API**

```http
GET /ttl?{QUERY_PARAMETERS}
```

| Parámetro | Descripción |
| --- | --- |
| `{QUERY_PARAMETERS}` | Una lista de parámetros de consulta opcionales, con varios parámetros separados por `&` caracteres. Los parámetros comunes incluyen `size` y `page` para fines de paginación. Para obtener una lista completa de los parámetros de consulta admitidos, consulte la [apéndice, sección](#query-params). |

{style=&quot;table-layout:auto&quot;}

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl?page=1&size=50 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta enumera los TTL resultantes. El siguiente ejemplo se ha truncado para el espacio.

```json
{
  "results": [
    {
      "ttlId": "SDfba908e9fb2e427ab4275d20465631d7",
      "datasetId": "62799c3e1151781b63ccaa28",
      "imsOrg": "{ORG_ID}",
      "status": "cancelled",
      "expiry": "2022-05-09T22:57:05.531024Z",
      "updatedAt": "2022-05-09T22:57:05.531025Z",
      "updatedBy": "{USER_ID}"
    },
    {
      "ttlId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
      "datasetId": "62759f2ede9e601b63a2ee14",
      "imsOrg": "{ORG_ID}",
      "status": "pending",
      "expiry": "2032-12-31T23:59:59Z",
      "updatedAt": "2022-05-09T22:41:46.731002Z",
      "updatedBy": "{USER_ID}"
    }
  ],
  "current_page": 1,
  "total_pages": 36,
  "total_count": 886
}
```

| Propiedad | Descripción |
| --- | --- |
| `results` | Contiene los detalles de los TTL devueltos. Para obtener más información sobre las propiedades de una entidad TTL, consulte la sección de respuestas para realizar una [llamada de búsqueda](#lookup). |
| `current_page` | La página actual de los resultados enumerados. |
| `total_pages` | Número total de páginas en la respuesta. |
| `total_count` | Número total de entidades TTL en la respuesta. |

{style=&quot;table-layout:auto&quot;}

## Buscar un TTL {#lookup}

Puede buscar un TTL de conjunto de datos mediante una solicitud de GET.

**Formato de API**

```http
GET /ttl/{TTL_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{TTL_ID}` | El ID del TTL que desea buscar. |

{style=&quot;table-layout:auto&quot;}

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl/5b020a27e7040801dedbf46e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve los detalles del TTL.

```json
{
    "ttlId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
    "datasetId": "62759f2ede9e601b63a2ee14",
    "imsOrg": "{ORG_ID}",
    "status": "pending",
    "expiry": "2023-12-31T23:59:59Z",
    "updatedAt": "2022-05-11T15:12:40.393115Z",
    "updatedBy": "{USER_ID}"
}
```

| Propiedad | Descripción |
| --- | --- |
| `ttlId` | El ID del TTL del conjunto de datos. |
| `datasetId` | El ID del conjunto de datos al que se aplica este TTL. |
| `imsOrg` | El ID de su organización. |
| `status` | Estado actual del TTL. |
| `expiry` | La fecha y hora programadas en que se eliminará el conjunto de datos. |
| `updatedAt` | Marca de tiempo de la última actualización del TTL. |
| `updatedBy` | El usuario que actualizó el TTL por última vez. |

{style=&quot;table-layout:auto&quot;}

## Crear un TTL {#create}

Puede agregar un TTL para un conjunto de datos a través de una solicitud del POST.

**Formato de API**

```http
POST /ttl
```

**Solicitud**

La siguiente solicitud programa un conjunto de datos `5b020a27e7040801dedbf46e` para su supresión a finales de 2022 (hora media de Greenwich).

```shell
curl -X POST \
  https://platform.adobe.io/data/core/hygiene/ttl \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "datasetId": "5b020a27e7040801dedbf46e",
        "expiry": "2022-12-31T23:59:59Z"
      }'
```

| Propiedad | Descripción |
| --- | --- |
| `datasetId` | El ID del conjunto de datos para el que desea programar un TTL. |
| `expiry` | Una marca de tiempo ISO 8601 para saber cuándo se eliminará el conjunto de datos. |

{style=&quot;table-layout:auto&quot;}

**Respuesta**

Una respuesta correcta devuelve los detalles del TTL, con el estado HTTP 200 (OK) si se actualizó un TTL preexistente o 201 (Creado) si no había ningún TTL preexistente.

```json
{
    "ttlId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
    "datasetId": "5b020a27e7040801dedbf46e",
    "imsOrg": "{ORG_ID}",
    "status": "pending",
    "expiry": "2032-12-31T23:59:59Z",
    "updatedAt": "2022-05-09T22:38:40.393115Z",
    "updatedBy": "{USER_ID}"
}
```

| Propiedad | Descripción |
| --- | --- |
| `ttlId` | El ID del TTL del conjunto de datos. |
| `datasetId` | El ID del conjunto de datos al que se aplica este TTL. |
| `imsOrg` | El ID de su organización. |
| `status` | Estado actual del TTL. |
| `expiry` | La fecha y hora programadas en que se eliminará el conjunto de datos. |
| `updatedAt` | Marca de tiempo de la última actualización del TTL. |
| `updatedBy` | El usuario que actualizó el TTL por última vez. |

{style=&quot;table-layout:auto&quot;}

## Actualizar un TTL {#update}

Puede actualizar un TTL para un conjunto de datos mediante una solicitud de PUT.

**Formato de API**

```http
PUT /ttl/{TTL_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{TTL_ID}` | El ID del TTL que desea modificar. |

{style=&quot;table-layout:auto&quot;}

**Solicitud**

La siguiente solicitud actualiza el TTL para el conjunto de datos `5b020a27e7040801dedbf46e` así que caduca a finales de 2023 (hora del meridiano de Greenwich).

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/ttl/5b020a27e7040801dedbf46e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "expiry": "2023-12-31T23:59:59Z"
      }'
```

| Propiedad | Descripción |
| --- | --- |
| `expiry` | Una marca de tiempo ISO 8601 para saber cuándo se eliminará el conjunto de datos. |

{style=&quot;table-layout:auto&quot;}

**Respuesta**

Una respuesta correcta devuelve los detalles del TTL actualizado.

```json
{
    "ttlId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
    "datasetId": "62759f2ede9e601b63a2ee14",
    "imsOrg": "{ORG_ID}",
    "status": "pending",
    "expiry": "2023-12-31T23:59:59Z",
    "updatedAt": "2022-05-11T15:12:40.393115Z",
    "updatedBy": "{USER_ID}"
}
```

| Propiedad | Descripción |
| --- | --- |
| `ttlId` | El ID del TTL del conjunto de datos. |
| `datasetId` | El ID del conjunto de datos al que se aplica este TTL. |
| `imsOrg` | El ID de su organización. |
| `status` | Estado actual del TTL. |
| `expiry` | La fecha y hora programadas en que se eliminará el conjunto de datos. |
| `updatedAt` | Marca de tiempo de la última actualización del TTL. |
| `updatedBy` | El usuario que actualizó el TTL por última vez. |

{style=&quot;table-layout:auto&quot;}

## Cancelar un TTL {#delete}

Puede cancelar un TTL realizando una solicitud de DELETE.

**Formato de API**

```http
DELETE /ttl/{TTL_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{TTL_ID}` | El ID del TTL que desea cancelar. |

{style=&quot;table-layout:auto&quot;}

**Solicitud**

La siguiente solicitud actualiza el TTL para el conjunto de datos `5b020a27e7040801dedbf46e` así que caduca a finales de 2023 (hora del meridiano de Greenwich).

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/hygiene/ttl/5b020a27e7040801dedbf46e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve los detalles del TTL, con su `status` ahora se establece en `cancelled`.

```json
{
    "ttlId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
    "datasetId": "62759f2ede9e601b63a2ee14",
    "imsOrg": "{ORG_ID}",
    "status": "cancelled",
    "expiry": "2023-12-31T23:59:59Z",
    "updatedAt": "2022-05-09T23:47:30.071186Z",
    "updatedBy": "{USER_ID}"
}
```

| Propiedad | Descripción |
| --- | --- |
| `ttlId` | El ID del TTL del conjunto de datos. |
| `datasetId` | El ID del conjunto de datos al que se aplica este TTL. |
| `imsOrg` | El ID de su organización. |
| `status` | Estado actual del TTL. |
| `expiry` | La fecha y hora programadas en que se eliminará el conjunto de datos. |
| `updatedAt` | Marca de tiempo de la última actualización del TTL. |
| `updatedBy` | El usuario que actualizó el TTL por última vez. |

{style=&quot;table-layout:auto&quot;}

## Recuperar el historial de un TTL

Puede consultar el historial de un TTL específico utilizando el parámetro de consulta `include=history` en una solicitud de consulta. El resultado incluye información sobre la creación del TTL, cualquier actualización que se haya aplicado y su cancelación o ejecución (si corresponde).

**Formato de API**

```http
GET /ttl/{TTL_ID}?include=history
```

| Parámetro | Descripción |
| --- | --- |
| `{TTL_ID}` | El ID del TTL cuyo historial desea buscar. |

{style=&quot;table-layout:auto&quot;}

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl/5b020a27e7040801dedbf46e?include=history \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve los detalles del TTL, con una `history` matriz que proporciona los detalles `status`, `expiry`, `updatedAt`y `updatedBy` para cada una de sus actualizaciones registradas.

```json
{
  "ttlId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
  "datasetId": "62759f2ede9e601b63a2ee14",
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
| `ttlId` | El ID del TTL del conjunto de datos. |
| `datasetId` | El ID del conjunto de datos al que se aplica este TTL. |
| `imsOrg` | El ID de su organización. |
| `history` | Muestra el historial de actualizaciones para el TTL como una matriz de objetos, cada uno de los cuales contiene el `status`, `expiry`, `updatedAt`y `updatedBy` para el TTL en el momento de la actualización. |

{style=&quot;table-layout:auto&quot;}

## Apéndice

### Parámetros de consulta aceptados {#query-params}

La siguiente tabla describe los parámetros de consulta disponibles cuando [listar TTL de conjuntos de datos](#list):

| Parámetro | Descripción | Ejemplo |
| --- | --- | --- |
| `size` | Un entero entre 1 y 100 que indica el número máximo de TTL que se va a devolver. El valor predeterminado es 25. | `size=50` |
| `page` | Un entero que indica qué página de TTL devolver. | `page=3` |
| `status` | Lista de estados separados por coma. Cuando se incluye, la respuesta coincide con los TTL cuyo estado actual se encuentra entre los enumerados. | `status=pending,cancelled` |
| `author` | Coincide con los TTL cuyas `created_by` es una coincidencia para la cadena de búsqueda. Si la cadena de búsqueda comienza por `LIKE` o `NOT LIKE`, el resto se trata como un patrón de búsqueda SQL. De lo contrario, toda la cadena de búsqueda se trata como una cadena literal que debe coincidir exactamente con todo el contenido de un `created_by` campo . | `author=LIKE %john%` |
| `createdDate` | Coincide con los TTL creados en la ventana de 24 horas a partir de la hora indicada.<br><br>Tenga en cuenta que las fechas sin hora (como `2021-12-07`) representan la fecha y hora al comienzo de ese día. Así, `createdDate=2021-12-07` se refiere a cualquier TTL creado el 7 de diciembre de 2021 a partir de `00:00:00` hasta `23:59:59.999999999` (UTC). | `createdDate=2021-12-07` |
| `createdFromDate` | Coincide con los TTL creados en la hora indicada o después de ella. | `createdFromDate=2021-12-07T00:00:00Z` |
| `createdToDate` | Coincide con los TTL creados en el momento indicado o antes de hacerlo. | `createdToDate=2021-12-07T23:59:59.999999999Z` |
| `updatedDate` / `updatedToDate` / `updatedFromDate` | Like `createdDate` / `createdFromDate` / `createdToDate`, pero coincide con el tiempo de actualización de un TTL en lugar de con el tiempo de creación.<br><br>Un TTL se considera actualizado en cada edición, incluso cuando se crea, cancela o ejecuta. | `updatedDate=2022-01-01` |
| `cancelledDate` / `cancelledToDate` / `cancelledFromDate` | Coincide con los TTL que se cancelaron en cualquier momento en el intervalo indicado. Esto se aplica incluso si el TTL se reabrió posteriormente (estableciendo una nueva caducidad para el mismo conjunto de datos). | `updatedDate=2022-01-01` |
| `completedDate` / `completedToDate` / `completedFromDate` | Coincide con los TTL completados durante el intervalo especificado. | `completedToDate=2021-11-11-06:00` |
| `expiryDate` / `expiryToDate` / `expiryFromDate` | Coincide con los TTL que se van a ejecutar o que ya se han ejecutado durante el intervalo especificado. | `expiryFromDate=2099-01-01&expiryToDate=2100-01-01` |

{style=&quot;table-layout:auto&quot;}
