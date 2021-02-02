---
keywords: Experience Platform;perfil;perfil del cliente en tiempo real;solución de problemas;API
title: Extremo de la API de trabajos del sistema de perfil
topic: guide
type: Documentation
description: Adobe Experience Platform le permite eliminar un conjunto de datos o lote del almacén de Perfiles para eliminar los datos de Perfil del cliente en tiempo real que ya no sean necesarios o que se hayan agregado por error. Esto requiere el uso de la API de Perfil para crear un trabajo del sistema de Perfil o eliminar una solicitud.
translation-type: tm+mt
source-git-commit: d2ace7cadb06f77bdf14b6a4ef83e879c4ca88fd
workflow-type: tm+mt
source-wordcount: '1321'
ht-degree: 2%

---


# Extremo de trabajos del sistema de perfil (Eliminar solicitudes)

Adobe Experience Platform le permite ingerir datos de varias fuentes y crear perfiles sólidos para clientes individuales. Los datos ingestados en [!DNL Platform] se almacenan en [!DNL Data Lake] y si los datasets se han habilitado para Perfil, esos datos también se almacenan en el almacén de datos [!DNL Real-time Customer Profile]. En ocasiones puede ser necesario eliminar un conjunto de datos o lote del almacén de Perfiles para eliminar datos que ya no son necesarios o que se agregaron por error. Esto requiere utilizar la API [!DNL Real-time Customer Profile] para crear un trabajo del sistema [!DNL Profile], o `delete request`, que también se puede modificar, supervisar o eliminar si es necesario.

>[!NOTE]
>
>Si está intentando eliminar conjuntos de datos o lotes de [!DNL Data Lake], visite la [información general del servicio de catálogo](../../catalog/home.md) para obtener más información.

## Primeros pasos

El extremo de API utilizado en esta guía forma parte de [[!DNL Real-time Customer Profile API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml). Antes de continuar, consulte la [guía de introducción](getting-started.md) para ver los vínculos a la documentación relacionada, una guía para leer las llamadas de la API de muestra en este documento e información importante sobre los encabezados necesarios para realizar llamadas exitosas a cualquier API de Experience Platform.

## Solicitudes de eliminación de vistas

Una solicitud de eliminación es un proceso asincrónico de larga duración, lo que significa que su organización puede estar ejecutando varias solicitudes de eliminación a la vez. Para realizar la vista de todas las solicitudes de eliminación que su organización está ejecutando actualmente, puede realizar una solicitud de GET al extremo `/system/jobs`.

También puede utilizar parámetros de consulta opcionales para filtrar la lista de solicitudes de eliminación devueltas en la respuesta. Para utilizar varios parámetros, separe cada parámetro con un símbolo de interrogación (`&`).

**Formato API**

```http
GET /system/jobs
GET /system/jobs?{QUERY_PARAMETERS}
```

| Parámetro | Descripción |
|---|---|
| `start` | Desplaza la página de resultados devueltos, según la hora de creación de la solicitud. Ejemplo: `start=4` |
| `limit` | Limite el número de resultados devueltos. Ejemplo: `limit=10` |
| `page` | Devolver una página específica de resultados, según la hora de creación de la solicitud. Ejemplo: `page=2` |
| `sort` | Ordene los resultados por un campo específico en orden ascendente (`asc`) o descendente (`desc`). El parámetro de ordenación no funciona cuando se devuelven varias páginas de resultados. Ejemplo: `sort=batchId:asc` |

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Respuesta**

La respuesta incluye una matriz &quot;secundarios&quot; con un objeto para cada solicitud de eliminación que contiene los detalles de esa solicitud.

```json
{
  "_page": {
    "count": 100,
    "next": "K1JJRDpFaWc5QUwyZFgtMEpBQUFBQUFBQUFBPT0jUlQ6MSNUUkM6MiNGUEM6QWdFQUFBQVFBQWZBQUg0Ly9yL25PcmpmZndEZUR3QT0="
  },
  "children": [
    {
      "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
      "imsOrgId": "{IMS_ORG}",
      "batchId": "8d075b5a178e48389126b9289dcfd0ac",
      "jobType": "DELETE",
      "status": "COMPLETED",
      "metrics": "{\"recordsProcessed\":5,\"timeTakenInSec\":1}",
      "createEpoch": 1559026134,
      "updateEpoch": 1559026137
    },
    {
      "id": "3f225e7e-ac8c-4904-b1d5-0ce79e03c2ec",
      "imsOrgId": "{IMS_ORG}",
      "dataSetId": "5c802d3cd83fc114b741c4b5",
      "jobType": "DELETE",
      "status": "PROCESSING",
      "metrics": "{\"recordsProcessed\":0,\"timeTakenInSec\":15}",
      "createEpoch": 1559025404,
      "updateEpoch": 1559025406
    }
  ]
}
```

| Propiedad | Descripción |
|---|---|
| `_page.count` | Número total de solicitudes. Esta respuesta se ha truncado para el espacio. |
| `_page.next` | Si existe una página adicional de resultados, vista la siguiente página de resultados reemplazando el valor de ID en una [solicitud de búsqueda](#view-a-specific-delete-request) por el valor `"next"` proporcionado. |
| `jobType` | Tipo de trabajo que se va a crear. En este caso, siempre devolverá `"DELETE"`. |
| `status` | Estado de la solicitud de eliminación. Los valores posibles son `"NEW"`, `"PROCESSING"`, `"COMPLETED"`, `"ERROR"`. |
| `metrics` | Un objeto que incluye el número de registros que se han procesado (`"recordsProcessed"`) y el tiempo en segundos que la solicitud se ha procesado o el tiempo que tardó en completarse (`"timeTakenInSec"`). |

## Crear una solicitud de eliminación {#create-a-delete-request}

El inicio de una nueva solicitud de eliminación se realiza mediante una solicitud de POST al extremo `/systems/jobs`, donde el ID del conjunto de datos o lote que se va a eliminar se proporciona en el cuerpo de la solicitud.

### Eliminar un conjunto de datos

Para eliminar un conjunto de datos del almacén de Perfiles, el ID del conjunto de datos debe incluirse en el cuerpo de la solicitud del POST. Esta acción eliminará TODOS los datos de un conjunto de datos determinado. [!DNL Experience Platform] le permite eliminar conjuntos de datos basados en esquemas de registros y series temporales.

**Formato API**

```http
POST /system/jobs
```

**Solicitud**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "dataSetId": "5c802d3cd83fc114b741c4b5"
      }'
```

| Propiedad | Descripción |
|---|---|
| `dataSetId` | **(Requerido)** El ID del conjunto de datos que desea eliminar. |

**Respuesta**

Una respuesta correcta devuelve los detalles de la solicitud de eliminación recién creada, incluido un ID único, generado por el sistema y de solo lectura para la solicitud. Se puede utilizar para buscar la solicitud y comprobar su estado. El `status` de la solicitud en el momento de la creación es `"NEW"` hasta que comienza el procesamiento. El `dataSetId` de la respuesta debe coincidir con el `dataSetId` enviado en la solicitud.

```json
{
    "id": "3f225e7e-ac8c-4904-b1d5-0ce79e03c2ec",
    "imsOrgId": "{IMS_ORG}",
    "dataSetId": "5c802d3cd83fc114b741c4b5",
    "jobType": "DELETE",
    "status": "NEW",
    "createEpoch": 1559025404,
    "updateEpoch": 1559025406
}
```

| Propiedad | Descripción |
|---|---|
| `id` | ID única, generada por el sistema y de solo lectura de la solicitud de eliminación. |
| `dataSetId` | ID del conjunto de datos, tal como se especifica en la solicitud del POST. |

### Eliminar un lote

Para eliminar un lote, el ID del lote debe incluirse en el cuerpo de la solicitud del POST. Tenga en cuenta que no puede eliminar lotes para conjuntos de datos en función de esquemas de registros. Solo se pueden eliminar los lotes de conjuntos de datos basados en esquemas de series temporales.

>[!NOTE]
>
> El motivo por el que no se pueden eliminar lotes para conjuntos de datos basados en esquemas de registros es porque los lotes de conjuntos de datos de tipo de registro sobrescriben los registros anteriores y, por lo tanto, no se pueden &quot;deshacer&quot; ni eliminar. La única manera de eliminar el impacto de los lotes erróneos para conjuntos de datos basados en esquemas de registros es volver a ingestar el lote con los datos correctos para sobrescribir los registros incorrectos.

Para obtener más información sobre el comportamiento de registros y series temporales, consulte la [sección sobre comportamientos de datos XDM](../../xdm/home.md#data-behaviors) en la [!DNL XDM System] información general.

**Formato API**

```http
POST /system/jobs
```

**Solicitud**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
       "batchId": "8d075b5a178e48389126b9289dcfd0ac"
      }'
```

| Propiedad | Descripción |
|---|---|
| `batchId` | **(Requerido)** El ID del lote que desea eliminar. |

**Respuesta**

Una respuesta correcta devuelve los detalles de la solicitud de eliminación recién creada, incluido un ID único, generado por el sistema y de solo lectura para la solicitud. Se puede utilizar para buscar la solicitud y comprobar su estado. El `"status"` de la solicitud en el momento de la creación es `"NEW"` hasta que comienza el procesamiento. El valor `"batchId"` de la respuesta debe coincidir con el valor `"batchId"` enviado en la solicitud.

```json
{
    "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "imsOrgId": "{IMS_ORG}",
    "batchId": "8d075b5a178e48389126b9289dcfd0ac",
    "jobType": "DELETE",
    "status": "NEW",
    "createEpoch": 1559026131,
    "updateEpoch": 1559026132
}
```

| Propiedad | Descripción |
|---|---|
| `id` | ID única, generada por el sistema y de solo lectura de la solicitud de eliminación. |
| `batchId` | ID del lote, tal como se especifica en la solicitud del POST. |

Si intenta iniciar una solicitud de eliminación para un lote de conjuntos de datos de registro, se producirá un error de 400 niveles, similar al siguiente:

```json
{
    "requestId": "bc4eb29f-63a8-4653-9133-71238884bb81",
    "errors": {
        "400": [
            {
                "code": "500",
                "message": "Batch can only be specified for EE type 'a294e36d382649dab2cc6ad64a41b674'"
            }
        ]
    }
}
```

## Vista de una solicitud de eliminación específica {#view-a-specific-delete-request}

Para realizar la vista de una solicitud de eliminación específica, incluyendo detalles como su estado, puede realizar una solicitud de búsqueda (GET) al extremo `/system/jobs` e incluir el ID de la solicitud de eliminación en la ruta.

**Formato API**

```http
GET /system/jobs/{DELETE_REQUEST_ID}
```

| Parámetro | Descripción |
|---|---|
| `{DELETE_REQUEST_ID}` | **(Requerido)** El ID de la solicitud de eliminación que desea vista. |

**Solicitud**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Respuesta**

La respuesta proporciona los detalles de la solicitud de eliminación, incluido su estado actualizado. El ID de la solicitud de eliminación en la respuesta (el valor `"id"`) debe coincidir con el ID enviado en la ruta de la solicitud.

```json
{
    "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "imsOrgId": "{IMS_ORG}",
    "batchId": "8d075b5a178e48389126b9289dcfd0ac",
    "jobType": "DELETE",
    "status": "COMPLETED",
    "metrics": "{\"recordsProcessed\":5,\"timeTakenInSec\":1}",
    "createEpoch": 1559026134,
    "updateEpoch": 1559026137
}
```

| Propiedades | Descripción |
|---|---|
| `jobType` | El tipo de trabajo que se está creando, en este caso siempre devolverá `"DELETE"`. |
| `status` | Estado de la solicitud de eliminación. Valores posibles: `"NEW"`, `"PROCESSING"`, `"COMPLETED"`, `"ERROR"`. |
| `metrics` | Una matriz que incluye el número de registros que se han procesado (`"recordsProcessed"`) y el tiempo en segundos que la solicitud se ha procesado o el tiempo que tardó en completarse (`"timeTakenInSec"`). |

Una vez que el estado de la solicitud de eliminación es `"COMPLETED"`, puede confirmar que los datos se han eliminado intentando acceder a los datos eliminados mediante la API de acceso a datos. Para obtener instrucciones sobre cómo utilizar la API de acceso a datos para acceder a conjuntos de datos y lotes, consulte la [documentación de acceso a datos](../../data-access/home.md).

## Eliminar una solicitud de eliminación

[!DNL Experience Platform] le permite eliminar una solicitud anterior, lo cual puede resultar útil por varios motivos, incluso si el trabajo de eliminación no se completó o se quedó atascado en la fase de procesamiento. Para eliminar una solicitud de eliminación, puede realizar una solicitud de DELETE al extremo `/system/jobs` e incluir el ID de la solicitud de eliminación que desea eliminar en la ruta de la solicitud.

**Formato API**

```http
DELETE /system/jobs/{DELETE_REQUEST_ID}
```

| Parámetro | Descripción |
|---|---|
| {DELETE_REQUEST_ID} | ID de la solicitud de eliminación que desea eliminar. |

**Solicitud**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Respuesta**

Una solicitud de eliminación correcta devuelve Estado HTTP 200 (Aceptar) y un cuerpo de respuesta vacío. Puede confirmar que la solicitud se eliminó realizando una solicitud de GET para realizar la vista de la solicitud de eliminación por su ID. Esto debe devolver un estado HTTP 404 (no encontrado), que indica que se eliminó la solicitud de eliminación.

## Pasos siguientes

Ahora que conoce los pasos involucrados en la eliminación de conjuntos de datos y lotes del [!DNL Profile Store] dentro de [!DNL Experience Platform], puede eliminar de forma segura los datos que se han agregado por error o que su organización ya no necesita. Tenga en cuenta que una solicitud de eliminación no se puede deshacer, por lo que solo debe eliminar datos que esté seguro de que no necesita ahora y que no los necesitará en el futuro.