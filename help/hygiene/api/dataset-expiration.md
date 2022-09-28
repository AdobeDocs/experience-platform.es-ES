---
title: Punto final de la API de caducidad del conjunto de datos
description: El extremo /ttl de la API de higiene de datos permite programar programáticamente las caducidades de conjuntos de datos en Adobe Experience Platform.
exl-id: fbabc2df-a79e-488c-b06b-cd72d6b9743b
source-git-commit: c2ff0d5806e57f230b937e8754d40031fb4b2305
workflow-type: tm+mt
source-wordcount: '1450'
ht-degree: 5%

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
  https://platform.adobe.io/data/core/hygiene/ttl?updatedToDate=2021-08-01&author=LIKE%Jane Doe%25 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta enumera las caducidades del conjunto de datos resultante. El siguiente ejemplo se ha truncado para el espacio.

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
| `totalRecords` | Recuento de caducidades del conjunto de datos que coinciden con los parámetros de la llamada de lista. |
| `ttlDetails` | Contiene los detalles de las caducidades del conjunto de datos devuelto. Para obtener más información sobre las propiedades de una caducidad de conjunto de datos, consulte la sección de respuestas para realizar una [llamada de búsqueda](#lookup). |

{style=&quot;table-layout:auto&quot;}

## Buscar una caducidad del conjunto de datos {#lookup}

Puede buscar una caducidad de conjunto de datos mediante una solicitud de GET.

**Formato de API**

```http
GET /ttl/{DATASET_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{DATASET_ID}` | El ID del conjunto de datos cuya caducidad desea buscar. |

{style=&quot;table-layout:auto&quot;}

**Solicitud**

La siguiente solicitud busca los detalles de caducidad para el conjunto de datos `62759f2ede9e601b63a2ee14`:

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
| `workorderId` | El ID de la caducidad del conjunto de datos. |
| `datasetId` | El ID del conjunto de datos al que se aplica esta caducidad. |
| `imsOrg` | El ID de su organización. |
| `status` | Estado actual de la caducidad del conjunto de datos. |
| `expiry` | La fecha y hora programadas en que se eliminará el conjunto de datos. |
| `updatedAt` | Marca de fecha y hora de la última actualización de la caducidad. |
| `updatedBy` | El usuario que actualizó la caducidad por última vez. |
| `displayName` | El nombre para mostrar de la solicitud de caducidad. |
| `description` | Descripción de la solicitud de caducidad. |

{style=&quot;table-layout:auto&quot;}

### Etiquetas de caducidad del catálogo

Al usar la variable [API del catálogo](../../catalog/api/getting-started.md) para buscar detalles del conjunto de datos, si el conjunto de datos tiene una caducidad activa, se enumerará en `tags.adobe/hygiene/ttl`.

El siguiente JSON representa una respuesta truncada para los detalles de un conjunto de datos de Catálogo, que tiene un valor de caducidad de `32503680000000`. El valor de la etiqueta codifica la caducidad como un número entero de milisegundos desde el comienzo de Unix Epoch.

```json
{
  "63212313c308d51b997858ba": {
    "name": "TTL Test Dataset",
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

La siguiente solicitud programa un conjunto de datos `5b020a27e7040801dedbf46e` para su supresión a finales de 2022 (hora media de Greenwich). Si no se encuentra ninguna caducidad existente para el conjunto de datos, se crea una nueva caducidad. Si el conjunto de datos ya tiene una caducidad pendiente, esa caducidad se actualiza con el nuevo `expiry` valor.

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
| `expiry` | Una marca de tiempo ISO 8601 para saber cuándo se eliminará el conjunto de datos. |
| `displayName` | Un nombre para mostrar para la solicitud de caducidad. |
| `description` | Una descripción opcional para la solicitud de caducidad. |

{style=&quot;table-layout:auto&quot;}

**Respuesta**

Una respuesta correcta devuelve los detalles de la caducidad del conjunto de datos, con el estado HTTP 200 (OK) si se actualizó una caducidad preexistente o 201 (Creado) si no había ninguna caducidad preexistente.

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
| `workorderId` | El ID de la caducidad del conjunto de datos. |
| `datasetId` | El ID del conjunto de datos al que se aplica esta caducidad. |
| `imsOrg` | El ID de su organización. |
| `status` | Estado actual de la caducidad del conjunto de datos. |
| `expiry` | La fecha y hora programadas en que se eliminará el conjunto de datos. |
| `updatedAt` | Marca de fecha y hora de la última actualización de la caducidad. |
| `updatedBy` | El usuario que actualizó la caducidad por última vez. |

{style=&quot;table-layout:auto&quot;}

## Cancelar una caducidad del conjunto de datos {#delete}

Puede cancelar una caducidad del conjunto de datos realizando una solicitud del DELETE.

>[!NOTE]
>
>Solo caducan los conjuntos de datos que tienen un estado de `pending` se puede cancelar. Al intentar cancelar una caducidad que se ha ejecutado o que ya se ha cancelado, se devuelve un error HTTP 404.

**Formato de API**

```http
DELETE /ttl/{EXPIRATION_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{EXPIRATION_ID}` | La variable `workorderId` de la caducidad del conjunto de datos que desea cancelar. |

{style=&quot;table-layout:auto&quot;}

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

Una respuesta correcta devuelve el estado HTTP 204 (sin contenido) y el valor de `status` se configura como `cancelled`.

## Recuperar el historial de estado de caducidad de un conjunto de datos

Puede consultar el historial de estado de caducidad de un conjunto de datos específico mediante el parámetro de consulta `include=history` en una solicitud de consulta. El resultado incluye información sobre la creación de la caducidad del conjunto de datos, cualquier actualización que se haya aplicado y su cancelación o ejecución (si corresponde).

**Formato de API**

```http
GET /ttl/{DATASET_ID}?include=history
```

| Parámetro | Descripción |
| --- | --- |
| `{DATASET_ID}` | El ID del conjunto de datos cuyo historial de caducidad desea buscar. |

{style=&quot;table-layout:auto&quot;}

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

Una respuesta correcta devuelve los detalles de la caducidad del conjunto de datos, con un `history` matriz que proporciona los detalles `status`, `expiry`, `updatedAt`y `updatedBy` para cada una de sus actualizaciones registradas.

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
| `workorderId` | El ID de la caducidad del conjunto de datos. |
| `datasetId` | El ID del conjunto de datos al que se aplica esta caducidad. |
| `datasetName` | El nombre para mostrar del conjunto de datos al que se aplica esta caducidad. |
| `sandboxName` | Nombre del simulador de pruebas en el que se encuentra el conjunto de datos de destino. |
| `displayName` | El nombre para mostrar de la solicitud de caducidad. |
| `description` | Descripción de la solicitud de caducidad. |
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
| `orgId` | Coincide con caducidades de conjuntos de datos cuyo ID de organización coincide con el del parámetro . Este valor predeterminado es el de la variable `x-gw-ims-org-id` y se omite a menos que la solicitud proporcione un token de servicio. | `orgId=885737B25DC460C50A49411B@AdobeOrg` |
| `status` | Lista de estados separados por coma. Cuando se incluye, la respuesta coincide con las caducidades de los conjuntos de datos cuyo estado actual se encuentra entre las de la lista. | `status=pending,cancelled` |
| `author` | Coincide con caducidades cuyo `created_by` es una coincidencia para la cadena de búsqueda. Si la cadena de búsqueda comienza por `LIKE` o `NOT LIKE`, el resto se trata como un patrón de búsqueda SQL. De lo contrario, toda la cadena de búsqueda se trata como una cadena literal que debe coincidir exactamente con todo el contenido de un `created_by` campo . | `author=LIKE %john%` |
| `sandboxName` | Coincide con las caducidades de conjuntos de datos cuyo nombre de simulador de pruebas coincida exactamente con el argumento . El valor predeterminado es el nombre del simulador de pruebas en la solicitud `x-sandbox-name` encabezado. Uso `sandboxName=*` para incluir las caducidades de los conjuntos de datos de todos los entornos limitados. | `sandboxName=dev1` |
| `datasetId` | Coincide con las caducidades que se aplican a un conjunto de datos específico. | `datasetId=62b3925ff20f8e1b990a7434` |
| `createdDate` | Coincide con las caducidades creadas en la ventana de 24 horas a partir de la hora indicada.<br><br>Tenga en cuenta que las fechas sin hora (como `2021-12-07`) representan la fecha y hora al comienzo de ese día. Así, `createdDate=2021-12-07` hace referencia a cualquier caducidad creada el 7 de diciembre de 2021 a partir de `00:00:00` hasta `23:59:59.999999999` (UTC). | `createdDate=2021-12-07` |
| `createdFromDate` | Coincide con las caducidades creadas en la hora indicada o después de ella. | `createdFromDate=2021-12-07T00:00:00Z` |
| `createdToDate` | Coincide con las caducidades creadas en la hora indicada o antes de ella. | `createdToDate=2021-12-07T23:59:59.999999999Z` |
| `updatedDate` / `updatedToDate` / `updatedFromDate` | Like `createdDate` / `createdFromDate` / `createdToDate`, pero coincide con el tiempo de actualización de una caducidad del conjunto de datos en lugar del tiempo de creación.<br><br>Una caducidad se considera actualizada en cada edición, incluso cuando se crea, cancela o ejecuta. | `updatedDate=2022-01-01` |
| `cancelledDate` / `cancelledToDate` / `cancelledFromDate` | Coincide con las caducidades que se cancelaron en cualquier momento en el intervalo indicado. Esto se aplica incluso si la caducidad se volvió a abrir posteriormente (estableciendo una nueva caducidad para el mismo conjunto de datos). | `updatedDate=2022-01-01` |
| `completedDate` / `completedToDate` / `completedFromDate` | Coincide con las caducidades que se completaron durante el intervalo especificado. | `completedToDate=2021-11-11-06:00` |
| `expiryDate` / `expiryToDate` / `expiryFromDate` | Coincide con las caducidades que se deben ejecutar o que ya se han ejecutado durante el intervalo especificado. | `expiryFromDate=2099-01-01&expiryToDate=2100-01-01` |

{style=&quot;table-layout:auto&quot;}
