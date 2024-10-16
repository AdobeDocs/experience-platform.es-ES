---
keywords: Experience Platform;perfil;perfil de cliente en tiempo real;resolución de problemas;API
title: Punto final de API de trabajos del sistema de perfiles
type: Documentation
description: Adobe Experience Platform permite eliminar un conjunto de datos o un lote del almacén de perfiles para eliminar los datos del perfil del cliente en tiempo real que ya no se necesitan o que se añadieron por error. Para ello, es necesario utilizar la API de perfil para crear un trabajo del sistema de perfiles o eliminar una solicitud.
role: Developer
exl-id: 75ddbf2f-9a54-424d-8569-d6737e9a590e
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '1327'
ht-degree: 3%

---

# Extremo de trabajos del sistema de perfil (solicitudes de eliminación)

Adobe Experience Platform le permite introducir datos de varias fuentes y crear perfiles sólidos para clientes individuales. Los datos ingeridos en [!DNL Platform] se almacenan en [!DNL Data Lake], y si los conjuntos de datos se han habilitado para el perfil, esos datos también se almacenan en el almacén de datos [!DNL Real-Time Customer Profile]. En ocasiones, puede ser necesario eliminar datos de perfil asociados con un conjunto de datos del almacén de perfiles para eliminar datos que ya no son necesarios o que se añadieron por error. Esto requiere el uso de la API [!DNL Real-Time Customer Profile] para crear un trabajo del sistema [!DNL Profile] o `delete request` que también se pueda modificar, supervisar o eliminar si es necesario.

>[!NOTE]
>
>Si está tratando de eliminar conjuntos de datos o lotes de [!DNL Data Lake], visite la [descripción general del servicio de catálogo](../../catalog/home.md) para obtener más información.

## Introducción

El extremo de API utilizado en esta guía forma parte de [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). Antes de continuar, revisa la [guía de introducción](getting-started.md) para ver vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios para realizar correctamente llamadas a cualquier API de Experience Platform.

## Ver solicitudes de eliminación

Una solicitud de eliminación es un proceso asincrónico de larga duración, lo que significa que su organización puede estar ejecutando varias solicitudes de eliminación a la vez. Para ver todas las solicitudes de eliminación que su organización está ejecutando actualmente, puede realizar una solicitud de GET al extremo `/system/jobs`.

También puede utilizar parámetros de consulta opcionales para filtrar la lista de solicitudes de eliminación devueltas en la respuesta. Para usar varios parámetros, separe cada parámetro con un signo &amp; (`&`).

**Formato de API**

```http
GET /system/jobs
GET /system/jobs?{QUERY_PARAMETERS}
```

| Parámetro | Descripción |
|---|---|
| `start` | Desplazar la página de resultados devuelta según la hora de creación de la solicitud. Ejemplo: `start=4` |
| `limit` | Limite el número de resultados devueltos. Ejemplo: `limit=10` |
| `page` | Devolver una página de resultados específica, según la hora de creación de la solicitud. Ejemplo: `page=2` |
| `sort` | Ordene los resultados por un campo específico en orden ascendente (`asc`) o descendente (`desc`). El parámetro sort no funciona cuando se devuelven varias páginas de resultados. Ejemplo: `sort=batchId:asc` |

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Respuesta**

La respuesta incluye una matriz &quot;children&quot; con un objeto para cada solicitud de eliminación que contiene los detalles de esa solicitud.

```json
{
  "_page": {
    "count": 100,
    "next": "K1JJRDpFaWc5QUwyZFgtMEpBQUFBQUFBQUFBPT0jUlQ6MSNUUkM6MiNGUEM6QWdFQUFBQVFBQWZBQUg0Ly9yL25PcmpmZndEZUR3QT0="
  },
  "children": [
    {
      "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
      "imsOrgId": "{ORG_ID}",
      "batchId": "8d075b5a178e48389126b9289dcfd0ac",
      "jobType": "DELETE",
      "status": "COMPLETED",
      "metrics": "{\"recordsProcessed\":5,\"timeTakenInSec\":1}",
      "createEpoch": 1559026134,
      "updateEpoch": 1559026137
    },
    {
      "id": "3f225e7e-ac8c-4904-b1d5-0ce79e03c2ec",
      "imsOrgId": "{ORG_ID}",
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
| `_page.next` | Si existe una página de resultados adicional, vea la siguiente página de resultados reemplazando el valor de ID en una [solicitud de consulta](#view-a-specific-delete-request) con el valor `"next"` proporcionado. |
| `jobType` | Tipo de trabajo que se está creando. En este caso, siempre devolverá `"DELETE"`. |
| `status` | El estado de la solicitud de eliminación. Los valores posibles son `"NEW"`, `"PROCESSING"`, `"COMPLETED"`, `"ERROR"`. |
| `metrics` | Un objeto que incluye el número de registros que se han procesado (`"recordsProcessed"`) y el tiempo en segundos que la solicitud se ha estado procesando, o cuánto tiempo tardó la solicitud en completarse (`"timeTakenInSec"`). |

## Crear una solicitud de eliminación {#create-a-delete-request}

El inicio de una nueva solicitud de eliminación se realiza mediante una solicitud de POST al extremo `/systems/jobs`, donde el identificador del conjunto de datos o del lote que se va a eliminar se proporciona en el cuerpo de la solicitud.

### Eliminar un conjunto de datos y los datos de perfil asociados

Para eliminar un conjunto de datos y todos los datos de perfil asociados con él del almacén de perfiles, el ID del conjunto de datos debe incluirse en el cuerpo de la solicitud del POST. Esta acción eliminará TODOS los datos de un conjunto de datos determinado. [!DNL Experience Platform] le permite eliminar conjuntos de datos basados en esquemas de registros y series temporales.

**Formato de API**

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "dataSetId": "5c802d3cd83fc114b741c4b5"
      }'
```

| Propiedad | Descripción |
|---|---|
| `dataSetId` | **(Obligatorio)** El ID del conjunto de datos que desea eliminar. |

**Respuesta**

Una respuesta correcta devuelve los detalles de la solicitud de eliminación recién creada, incluido un ID único, generado por el sistema y de solo lectura para la solicitud. Se puede utilizar para buscar la solicitud y comprobar su estado. `status` para la solicitud en el momento de la creación es `"NEW"` hasta que comience a procesarse. El `dataSetId` de la respuesta debe coincidir con el `dataSetId` enviado en la solicitud.

```json
{
    "id": "3f225e7e-ac8c-4904-b1d5-0ce79e03c2ec",
    "imsOrgId": "{ORG_ID}",
    "dataSetId": "5c802d3cd83fc114b741c4b5",
    "jobType": "DELETE",
    "status": "NEW",
    "createEpoch": 1559025404,
    "updateEpoch": 1559025406
}
```

| Propiedad | Descripción |
|---|---|
| `id` | El ID único, generado por el sistema y de solo lectura de la solicitud de eliminación. |
| `dataSetId` | El ID del conjunto de datos, tal como se especifica en la solicitud del POST. |

### Eliminar un lote

Para eliminar un lote, se debe incluir el ID del lote en el cuerpo de la solicitud del POST. Tenga en cuenta que no puede eliminar lotes para conjuntos de datos basados en esquemas de registros. Solo se pueden eliminar los lotes de conjuntos de datos basados en esquemas de series temporales.

>[!NOTE]
>
> El motivo por el que no se pueden eliminar lotes para conjuntos de datos basados en esquemas de registro es porque los lotes de conjuntos de datos de tipo de registro sobrescriben registros anteriores y, por lo tanto, no se pueden &quot;deshacer&quot; ni eliminar. La única manera de eliminar el impacto de los lotes erróneos para conjuntos de datos basados en esquemas de registro es volver a ingerir el lote con los datos correctos para sobrescribir los registros incorrectos.

Para obtener más información sobre el comportamiento de registros y series temporales, consulte la [sección sobre comportamientos de datos XDM](../../xdm/home.md#data-behaviors) en la descripción general de [!DNL XDM System].

**Formato de API**

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
       "batchId": "8d075b5a178e48389126b9289dcfd0ac"
      }'
```

| Propiedad | Descripción |
|---|---|
| `batchId` | **(Obligatorio)** El identificador del lote que desea eliminar. |

**Respuesta**

Una respuesta correcta devuelve los detalles de la solicitud de eliminación recién creada, incluido un ID único, generado por el sistema y de solo lectura para la solicitud. Se puede utilizar para buscar la solicitud y comprobar su estado. `"status"` para la solicitud en el momento de la creación es `"NEW"` hasta que comience a procesarse. El valor `"batchId"` de la respuesta debe coincidir con el valor `"batchId"` enviado en la solicitud.

```json
{
    "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "imsOrgId": "{ORG_ID}",
    "batchId": "8d075b5a178e48389126b9289dcfd0ac",
    "jobType": "DELETE",
    "status": "NEW",
    "createEpoch": 1559026131,
    "updateEpoch": 1559026132
}
```

| Propiedad | Descripción |
|---|---|
| `id` | El ID único, generado por el sistema y de solo lectura de la solicitud de eliminación. |
| `batchId` | El ID del lote, tal como se especifica en la solicitud del POST. |

Si intenta iniciar una solicitud de eliminación para un lote del conjunto de datos de Record, se producirá un error de nivel 400, similar al siguiente:

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

## Ver una solicitud de eliminación específica {#view-a-specific-delete-request}

Para ver una solicitud de eliminación específica, incluidos detalles como su estado, puede realizar una solicitud de búsqueda (GET) al extremo `/system/jobs` e incluir el ID de la solicitud de eliminación en la ruta.

**Formato de API**

```http
GET /system/jobs/{DELETE_REQUEST_ID}
```

| Parámetro | Descripción |
|---|---|
| `{DELETE_REQUEST_ID}` | **(Obligatorio)** El identificador de la solicitud de eliminación que desea ver. |

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Respuesta**

La respuesta proporciona los detalles de la solicitud de eliminación, incluido su estado actualizado. El identificador de la solicitud de eliminación en la respuesta (el valor `"id"`) debe coincidir con el identificador enviado en la ruta de solicitud.

```json
{
    "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "imsOrgId": "{ORG_ID}",
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
| `status` | El estado de la solicitud de eliminación. Valores posibles: `"NEW"`, `"PROCESSING"`, `"COMPLETED"`, `"ERROR"`. |
| `metrics` | Matriz que incluye el número de registros que se han procesado (`"recordsProcessed"`) y el tiempo en segundos que la solicitud se ha estado procesando, o el tiempo que tardó la solicitud en completarse (`"timeTakenInSec"`). |

Una vez que el estado de la solicitud de eliminación sea `"COMPLETED"`, puede confirmar que los datos se han eliminado intentando acceder a los datos eliminados mediante la API de acceso a datos. Para obtener instrucciones sobre cómo usar la API de acceso a datos para acceder a conjuntos de datos y lotes, consulte la [documentación de acceso a datos](../../data-access/home.md).

## Eliminar una solicitud de eliminación

[!DNL Experience Platform] le permite eliminar una solicitud anterior, lo que puede resultar útil por varios motivos, incluso si el trabajo de eliminación no se completó o se quedó atascado en la fase de procesamiento. Para quitar una solicitud de eliminación, puede realizar una solicitud de DELETE al extremo `/system/jobs` e incluir el identificador de la solicitud de eliminación que desea quitar en la ruta de acceso de la solicitud.

**Formato de API**

```http
DELETE /system/jobs/{DELETE_REQUEST_ID}
```

| Parámetro | Descripción |
|---|---|
| {DELETE_REQUEST_ID} | El ID de la solicitud de eliminación que desea eliminar. |

**Solicitud**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Respuesta**

Una solicitud de eliminación correcta devuelve el estado HTTP 200 (OK) y un cuerpo de respuesta vacío. Puede confirmar que la solicitud se eliminó realizando una solicitud de GET para ver la solicitud de eliminación por su ID. Esto debería devolver un estado HTTP 404 (no encontrado), que indica que se eliminó la solicitud de eliminación.

## Pasos siguientes

Ahora que conoce los pasos involucrados en la eliminación de conjuntos de datos y lotes de [!DNL Profile store] dentro de [!DNL Experience Platform], puede eliminar de manera segura los datos que se agregaron erróneamente o que su organización ya no necesita. Tenga en cuenta que una solicitud de eliminación no se puede deshacer, por lo tanto, solo debe eliminar datos que esté seguro de que no necesita ahora y que no necesitará en el futuro.
