---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
title: 'Trabajos del sistema de perfil: API de Perfil del cliente en tiempo real'
topic: guide
translation-type: tm+mt
source-git-commit: 59cf089a8bf7ce44e7a08b0bb1d4562f5d5104db
workflow-type: tm+mt
source-wordcount: '1425'
ht-degree: 2%

---


# Extremo de trabajos del sistema de perfil (Eliminar solicitudes)

Adobe Experience Platform le permite ingerir datos de varias fuentes y crear perfiles sólidos para clientes individuales. Los datos ingeridos en [!DNL Platform] se almacenan tanto en el almacén [!DNL Data Lake] como en el [!DNL Real-time Customer Profile] almacén de datos. Ocasionalmente puede ser necesario eliminar un conjunto de datos o lote del almacén de Perfiles para eliminar datos que ya no son necesarios o que se agregaron por error. Esto requiere usar la [!DNL Real-time Customer Profile] API para crear un trabajo [!DNL Profile] del sistema, también conocido como &quot;[!DNL delete request]&quot;, que también se puede modificar, supervisar o eliminar si es necesario.

>[!NOTE]
>
>Si está intentando eliminar conjuntos de datos o lotes del [!DNL Data Lake], consulte la información general [del servicio de](../../catalog/home.md) catálogos para obtener instrucciones.

## Primeros pasos

El punto final de API utilizado en esta guía forma parte de la [[!DNL Real-time Customer Perfil API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml). Antes de continuar, consulte la guía [de](getting-started.md) introducción para ver los vínculos a la documentación relacionada, una guía para leer las llamadas de la API de muestra en este documento e información importante sobre los encabezados necesarios para realizar llamadas con éxito a cualquier [!DNL Experience Platform] API.

## Solicitudes de eliminación de vistas

Una solicitud de eliminación es un proceso asincrónico de larga duración, lo que significa que su organización puede estar ejecutando varias solicitudes de eliminación a la vez. Para realizar la vista de todas las solicitudes de eliminación que su organización está ejecutando actualmente, puede realizar una solicitud de GET al `/system/jobs` extremo.

También puede utilizar parámetros de consulta opcionales para filtrar la lista de solicitudes de eliminación devueltas en la respuesta. Para utilizar varios parámetros, separe cada parámetro con un símbolo &amp;.

**Formato API**

```http
GET /system/jobs
GET /system/jobs?{QUERY_PARAMETERS}
```

| Parámetro | Descripción |
|---|---|
| `start` | Desplaza la página de resultados devueltos, según la hora de creación de la solicitud. Ejemplo: *`start=4`* |
| `limit` | Limite el número de resultados devueltos. Ejemplo: *`limit=10`* |
| `page` | Devolver una página específica de resultados, según la hora de creación de la solicitud. Ejemplo: ***`page=2`*** |
| `sort` | Ordenar los resultados por un campo específico en orden ascendente (*`asc`*) o descendente (**`desc`**). El parámetro de ordenación no funciona cuando se devuelven varias páginas de resultados. Ejemplo: `sort=batchId:asc` |

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
| `_page.next` | Si existe una página adicional de resultados, reemplace el valor de ID en una solicitud [de](#view-a-specific-delete-request) búsqueda por el valor proporcionado para la vista de la siguiente página de resultados por el `"next"` . |
| `jobType` | Tipo de trabajo que se va a crear. En este caso, siempre regresará `"DELETE"`. |
| `status` | Estado de la solicitud de eliminación. Los valores posibles son `"NEW"`, `"PROCESSING"`, `"COMPLETED"`, `"ERROR"`. |
| `metrics` | Objeto que incluye el número de registros que se han procesado (`"recordsProcessed"`) y el tiempo en segundos que la solicitud se ha procesado o el tiempo que tardó en completarse (`"timeTakenInSec"`). |

## Crear una solicitud de eliminación {#create-a-delete-request}

El inicio de una nueva solicitud de eliminación se realiza mediante una solicitud de POST al extremo, donde el ID del conjunto de datos o lote que se va a eliminar se proporciona en el cuerpo de la solicitud. `/systems/jobs`

### Eliminar un conjunto de datos

Para eliminar un conjunto de datos, el ID del conjunto de datos debe incluirse en el cuerpo de la solicitud del POST. Esta acción eliminará TODOS los datos de un conjunto de datos determinado. [!DNL Experience Platform] le permite eliminar conjuntos de datos basados en esquemas de registros y series temporales.

>[!CAUTION]
>
> Al intentar eliminar un conjunto de datos [!DNL Profile]habilitado mediante la [!DNL Experience Platform] interfaz de usuario, el conjunto de datos se desactiva para la ingestión, pero no se elimina hasta que se crea una solicitud de eliminación mediante la API. Para obtener más información, consulte el [apéndice](#appendix) de este documento.

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

Una respuesta correcta devuelve los detalles de la solicitud de eliminación recién creada, incluido un ID único, generado por el sistema y de solo lectura para la solicitud. Se puede utilizar para buscar la solicitud y comprobar su estado. La solicitud **`status`** en el momento de la creación es *`"NEW"`* hasta que comienza el procesamiento. El **`dataSetId`** contenido de la respuesta debe coincidir con el ***`dataSetId`*** enviado en la solicitud.

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

Para obtener más información sobre el comportamiento de registros y series temporales, consulte la [sección sobre comportamientos](../../xdm/home.md#data-behaviors) de datos XDM en la [!DNL XDM System] información general.

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

Una respuesta correcta devuelve los detalles de la solicitud de eliminación recién creada, incluido un ID único, generado por el sistema y de solo lectura para la solicitud. Se puede utilizar para buscar la solicitud y comprobar su estado. La solicitud `"status"` en el momento de la creación es `"NEW"` hasta que comienza el procesamiento. El `"batchId"` contenido de la respuesta debe coincidir con el `"batchId"` enviado en la solicitud.

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

Para realizar la vista de una solicitud de eliminación específica, incluyendo detalles como su estado, puede realizar una solicitud de búsqueda (GET) al extremo e incluir el ID de la solicitud de eliminación en la ruta de acceso. `/system/jobs`

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

La respuesta proporciona los detalles de la solicitud de eliminación, incluido su estado actualizado. El ID de la solicitud de eliminación en la respuesta debe coincidir con el ID enviado en la ruta de la solicitud.

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
| `jobType` | El tipo de trabajo que se está creando, en este caso siempre volverá `"DELETE"`. |
| `status` | Estado de la solicitud de eliminación. Possible values: `"NEW"`, `"PROCESSING"`, `"COMPLETED"`, `"ERROR"`. |
| `metrics` | Matriz que incluye el número de registros que se han procesado (`"recordsProcessed"`) y el tiempo en segundos que la solicitud se ha estado procesando o el tiempo que tardó en completarse (`"timeTakenInSec"`). |

Una vez que el estado de la solicitud de eliminación `"COMPLETED"` puede confirmar que los datos se han eliminado intentando acceder a los datos eliminados mediante la API de acceso a datos. Para obtener instrucciones sobre cómo utilizar la API de acceso a datos para acceder a conjuntos de datos y lotes, consulte la documentación [de acceso a](../../data-access/home.md)datos.

## Eliminar una solicitud de eliminación

[!DNL Experience Platform] le permite eliminar una solicitud anterior, lo cual puede resultar útil por varios motivos, incluso si el trabajo de eliminación no se completó o se quedó atascado en la fase de procesamiento. Para eliminar una solicitud de eliminación, puede realizar una solicitud de DELETE al extremo e incluir el ID de la solicitud de eliminación que desea eliminar en la ruta de la solicitud. `/system/jobs`

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

Ahora que conoce los pasos necesarios para eliminar conjuntos de datos y lotes desde el [!DNL Profile Store] interior [!DNL Experience Platform], puede eliminar de forma segura los datos que se han agregado por error o que su organización ya no necesita. Tenga en cuenta que una solicitud de eliminación no se puede deshacer, por lo que solo debe eliminar datos que esté seguro de que no necesita ahora y que no los necesitará en el futuro.

## Apéndice {#appendix}

La siguiente información complementa el acto de eliminar un conjunto de datos del [!DNL Profile Store].

### Eliminación de un conjunto de datos mediante la [!DNL Experience Platform] IU

Al utilizar la interfaz de usuario para eliminar un conjunto de datos que se ha habilitado para [!DNL Experience Platform] , se abre un cuadro de diálogo en el que se pregunta: &quot;¿Realmente desea eliminar este conjunto de datos del [!DNL Profile][!DNL Experience Data Lake]? Utilice la API &#39;p[!DNL rofile systems jobs]&#39; para eliminar este conjunto de datos del [!DNL Profile Service].&quot;

Al hacer clic en **[!UICONTROL Eliminar]** en la interfaz de usuario, se deshabilita el conjunto de datos para su inserción, pero NO se elimina automáticamente el conjunto de datos en el servidor. Para eliminar permanentemente el conjunto de datos, se debe crear una solicitud de eliminación manualmente siguiendo los pasos de esta guía para [crear una solicitud](#create-a-delete-request)de eliminación.

La siguiente imagen muestra la advertencia al intentar eliminar un conjunto de datos [!DNL Profile]habilitado mediante la interfaz de usuario.

![](../images/delete-profile-dataset.png)

Para obtener más información sobre cómo trabajar con conjuntos de datos, lea la información general [de los](../../catalog/datasets/overview.md)conjuntos de datos.