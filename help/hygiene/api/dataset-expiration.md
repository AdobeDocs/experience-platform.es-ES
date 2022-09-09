---
title: Punto final de API de caducidad del conjunto de datos
description: El extremo /ttl de la API de higiene de datos permite programar programáticamente las caducidades de conjuntos de datos en Adobe Experience Platform.
exl-id: fbabc2df-a79e-488c-b06b-cd72d6b9743b
source-git-commit: 5a12c75a54f420b2ca831dbfe05105dfd856dc4d
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Extremo de caducidad del conjunto de datos

>[!IMPORTANT]
>
>Actualmente, las funciones de higiene de datos de Adobe Experience Platform solo están disponibles para las organizaciones que han adquirido el Escudo de la salud.

La variable `/ttl` en la API de higiene de datos le permite programar fechas de caducidad para conjuntos de datos en Adobe Experience Platform.

Una caducidad del conjunto de datos es solo una operación de eliminación con retraso. El conjunto de datos no está protegido entre tanto, por lo que se puede eliminar por otros medios antes de que se alcance su caducidad.

>[!NOTE]
>
>Aunque la caducidad se especifica como un instante específico en el tiempo, puede haber hasta 24 horas de retraso después de la caducidad antes de iniciar la eliminación real. Una vez iniciada la eliminación, puede tardar hasta siete días en que se hayan eliminado todos los seguimientos del conjunto de datos de los sistemas de Platform.

En cualquier momento antes de que se inicie realmente la eliminación del conjunto de datos, puede cancelar la caducidad o modificar su tiempo de déclencheur. Después de cancelar una caducidad del conjunto de datos, puede volver a abrirlo estableciendo una nueva caducidad.

Una vez iniciada la eliminación del conjunto de datos, su trabajo de caducidad se marcará como `executing`y no puede modificarse. El conjunto de datos en sí puede recuperarse durante un máximo de siete días, pero solo a través de un proceso manual iniciado mediante una solicitud de servicio de Adobe. A medida que se ejecuta la solicitud, el lago de datos, el servicio de identidad y el perfil del cliente en tiempo real comienzan procesos separados para eliminar el contenido del conjunto de datos de sus respectivos servicios. Una vez eliminados los datos de los tres servicios, la caducidad se marca como `executed`.

>[!WARNING]
>
>Si un conjunto de datos está configurado para caducar, debe cambiar manualmente cualquier flujo de datos que pueda estar introduciendo datos en ese conjunto de datos para que sus flujos de trabajo descendentes no se vean afectados negativamente.

## Primeros pasos

El extremo utilizado en esta guía forma parte de la API de higiene de datos. Antes de continuar, revise la [información general](./overview.md) para ver vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios para realizar llamadas correctamente a cualquier API de Experience Platform.

## Enumerar caducidades del conjunto de datos {#list}

Puede enumerar todas las caducidades de los conjuntos de datos de su organización realizando una solicitud de GET.

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

Una respuesta correcta enumera las caducidades del conjunto de datos resultante. El siguiente ejemplo se ha truncado para el espacio.

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
| `results` | Contiene los detalles de las caducidades del conjunto de datos devuelto. Para obtener más información sobre las propiedades de una caducidad de conjunto de datos, consulte la sección de respuestas para realizar una [llamada de búsqueda](#lookup). |
| `current_page` | La página actual de los resultados enumerados. |
| `total_pages` | Número total de páginas en la respuesta. |
| `total_count` | El número total de caducidades del conjunto de datos en la respuesta. |

{style=&quot;table-layout:auto&quot;}

## Buscar una caducidad del conjunto de datos {#lookup}

Puede buscar una caducidad de conjunto de datos mediante una solicitud de GET.

**Formato de API**

```http
GET /ttl/{TTL_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{TTL_ID}` | El ID de la caducidad del conjunto de datos que desea buscar. |

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

Una respuesta correcta devuelve los detalles de la caducidad del conjunto de datos.

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
| `ttlId` | El ID de la caducidad del conjunto de datos. |
| `datasetId` | El ID del conjunto de datos al que se aplica esta caducidad. |
| `imsOrg` | El ID de su organización. |
| `status` | Estado actual de la caducidad del conjunto de datos. |
| `expiry` | La fecha y hora programadas en que se eliminará el conjunto de datos. |
| `updatedAt` | Marca de fecha y hora de la última actualización de la caducidad. |
| `updatedBy` | El usuario que actualizó la caducidad por última vez. |

{style=&quot;table-layout:auto&quot;}

## Crear una caducidad para el conjunto de datos {#create}

Puede crear una fecha de caducidad para un conjunto de datos mediante una solicitud del POST.

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
| `datasetId` | El ID del conjunto de datos para el que desea programar una fecha de caducidad. |
| `expiry` | Una marca de tiempo ISO 8601 para saber cuándo se eliminará el conjunto de datos. |

{style=&quot;table-layout:auto&quot;}

**Respuesta**

Una respuesta correcta devuelve los detalles de la caducidad del conjunto de datos, con el estado HTTP 200 (OK) si se actualizó una caducidad preexistente o 201 (Creado) si no había ninguna caducidad preexistente.

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
| `ttlId` | El ID de la caducidad del conjunto de datos. |
| `datasetId` | El ID del conjunto de datos al que se aplica esta caducidad. |
| `imsOrg` | El ID de su organización. |
| `status` | Estado actual de la caducidad del conjunto de datos. |
| `expiry` | La fecha y hora programadas en que se eliminará el conjunto de datos. |
| `updatedAt` | Marca de fecha y hora de la última actualización de la caducidad. |
| `updatedBy` | El usuario que actualizó la caducidad por última vez. |

{style=&quot;table-layout:auto&quot;}

## Actualizar una caducidad del conjunto de datos {#update}

Puede actualizar una caducidad del conjunto de datos mediante una solicitud del PUT.

**Formato de API**

```http
PUT /ttl/{TTL_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{TTL_ID}` | El ID de la caducidad del conjunto de datos que desea modificar. |

{style=&quot;table-layout:auto&quot;}

**Solicitud**

La siguiente solicitud actualiza la caducidad del conjunto de datos `5b020a27e7040801dedbf46e` así que caduca a finales de 2023 (hora del meridiano de Greenwich).

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

Una respuesta correcta devuelve los detalles de la caducidad actualizada.

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
| `ttlId` | El ID de la caducidad del conjunto de datos. |
| `datasetId` | El ID del conjunto de datos al que se aplica esta caducidad. |
| `imsOrg` | El ID de su organización. |
| `status` | Estado actual de la caducidad del conjunto de datos. |
| `expiry` | La fecha y hora programadas en que se eliminará el conjunto de datos. |
| `updatedAt` | Marca de fecha y hora de la última actualización de la caducidad. |
| `updatedBy` | El usuario que actualizó la caducidad por última vez. |

{style=&quot;table-layout:auto&quot;}

## Cancelar una caducidad del conjunto de datos {#delete}

Puede cancelar una caducidad del conjunto de datos realizando una solicitud del DELETE.

**Formato de API**

```http
DELETE /ttl/{TTL_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{TTL_ID}` | El ID de la caducidad del conjunto de datos que desea cancelar. |

{style=&quot;table-layout:auto&quot;}

**Solicitud**

La siguiente solicitud actualiza la caducidad del conjunto de datos `5b020a27e7040801dedbf46e` así que caduca a finales de 2023 (hora del meridiano de Greenwich).

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/hygiene/ttl/5b020a27e7040801dedbf46e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve los detalles de la caducidad del conjunto de datos, con su `status` ahora se establece en `cancelled`.

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
| `ttlId` | El ID de la caducidad del conjunto de datos. |
| `datasetId` | El ID del conjunto de datos al que se aplica esta caducidad. |
| `imsOrg` | El ID de su organización. |
| `status` | Estado actual de la caducidad del conjunto de datos. |
| `expiry` | La fecha y hora programadas en que se eliminará el conjunto de datos. |
| `updatedAt` | Marca de fecha y hora de la última actualización de la caducidad. |
| `updatedBy` | El usuario que actualizó la caducidad por última vez. |

{style=&quot;table-layout:auto&quot;}

## Recuperar el historial de una caducidad del conjunto de datos

Puede consultar el historial de una caducidad específica del conjunto de datos utilizando el parámetro de consulta `include=history` en una solicitud de consulta. El resultado incluye información sobre la creación de la caducidad del conjunto de datos, cualquier actualización que se haya aplicado y su cancelación o ejecución (si corresponde).

**Formato de API**

```http
GET /ttl/{TTL_ID}?include=history
```

| Parámetro | Descripción |
| --- | --- |
| `{TTL_ID}` | El ID de la caducidad del conjunto de datos cuyo historial desea buscar. |

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

Una respuesta correcta devuelve los detalles de la caducidad del conjunto de datos, con un `history` matriz que proporciona los detalles `status`, `expiry`, `updatedAt`y `updatedBy` para cada una de sus actualizaciones registradas.

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
| `ttlId` | El ID de la caducidad del conjunto de datos. |
| `datasetId` | El ID del conjunto de datos al que se aplica esta caducidad. |
| `imsOrg` | El ID de su organización. |
| `history` | Muestra el historial de actualizaciones para la caducidad como una matriz de objetos, cada uno de los cuales contiene el `status`, `expiry`, `updatedAt`y `updatedBy` para la caducidad en el momento de la actualización. |

{style=&quot;table-layout:auto&quot;}

## Apéndice

### Parámetros de consulta aceptados {#query-params}

La siguiente tabla describe los parámetros de consulta disponibles cuando [lista de caducidades del conjunto de datos](#list):

| Parámetro | Descripción | Ejemplo |
| --- | --- | --- |
| `size` | Un entero entre 1 y 100 que indica el número máximo de caducidades que se van a devolver. El valor predeterminado es 25. | `size=50` |
| `page` | Un entero que indica qué página de caducidades devolver. | `page=3` |
| `status` | Lista de estados separados por coma. Cuando se incluye, la respuesta coincide con las caducidades de los conjuntos de datos cuyo estado actual se encuentra entre las de la lista. | `status=pending,cancelled` |
| `author` | Coincide con caducidades cuyo `created_by` es una coincidencia para la cadena de búsqueda. Si la cadena de búsqueda comienza por `LIKE` o `NOT LIKE`, el resto se trata como un patrón de búsqueda SQL. De lo contrario, toda la cadena de búsqueda se trata como una cadena literal que debe coincidir exactamente con todo el contenido de un `created_by` campo . | `author=LIKE %john%` |
| `createdDate` | Coincide con las caducidades creadas en la ventana de 24 horas a partir de la hora indicada.<br><br>Tenga en cuenta que las fechas sin hora (como `2021-12-07`) representan la fecha y hora al comienzo de ese día. Así, `createdDate=2021-12-07` hace referencia a cualquier caducidad creada el 7 de diciembre de 2021 a partir de `00:00:00` hasta `23:59:59.999999999` (UTC). | `createdDate=2021-12-07` |
| `createdFromDate` | Coincide con las caducidades creadas en la hora indicada o después de ella. | `createdFromDate=2021-12-07T00:00:00Z` |
| `createdToDate` | Coincide con las caducidades creadas en la hora indicada o antes de ella. | `createdToDate=2021-12-07T23:59:59.999999999Z` |
| `updatedDate` / `updatedToDate` / `updatedFromDate` | Like `createdDate` / `createdFromDate` / `createdToDate`, pero coincide con el tiempo de actualización de una caducidad del conjunto de datos en lugar del tiempo de creación.<br><br>Una caducidad se considera actualizada en cada edición, incluso cuando se crea, cancela o ejecuta. | `updatedDate=2022-01-01` |
| `cancelledDate` / `cancelledToDate` / `cancelledFromDate` | Coincide con las caducidades que se cancelaron en cualquier momento en el intervalo indicado. Esto se aplica incluso si la caducidad se volvió a abrir posteriormente (estableciendo una nueva caducidad para el mismo conjunto de datos). | `updatedDate=2022-01-01` |
| `completedDate` / `completedToDate` / `completedFromDate` | Coincide con las caducidades que se completaron durante el intervalo especificado. | `completedToDate=2021-11-11-06:00` |
| `expiryDate` / `expiryToDate` / `expiryFromDate` | Coincide con las caducidades que se deben ejecutar o que ya se han ejecutado durante el intervalo especificado. | `expiryFromDate=2099-01-01&expiryToDate=2100-01-01` |

{style=&quot;table-layout:auto&quot;}
