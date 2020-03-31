---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Apéndice de la guía del desarrollador del servicio de catálogo
topic: developer guide
translation-type: tm+mt
source-git-commit: 4b2524fcfda578d0debb89623bec6edb537db852

---


# Apéndice de la guía del desarrollador del servicio de catálogo

Este documento contiene información adicional para ayudarle a trabajar con la API de catálogo.

## Vista de objetos interrelacionados {#view-interrelated-objects}

Algunos objetos de catálogo pueden estar interrelacionados con otros objetos de catálogo. Los campos con el prefijo `@` en las cargas de respuesta indican objetos relacionados. Los valores de estos campos toman la forma de un URI, que puede utilizarse en una solicitud GET independiente para recuperar los objetos relacionados que representan.

El conjunto de datos de ejemplo devuelto en el documento al [buscar un conjunto de datos](look-up-object.md) específico contiene un `files` campo con el siguiente valor URI: `"@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"`. El contenido del `files` campo se puede ver usando este URI como ruta para una nueva solicitud GET.

**Formato API**

```http
GET {OBJECT_URI}
```

| Parámetro | Descripción |
| --- | --- |
| `{OBJECT_URI}` | URI proporcionado por el campo de objeto interrelacionado (excluido el `@` símbolo). |

**Solicitud**

La siguiente solicitud utiliza el URI, siempre que la propiedad `files` del conjunto de datos de ejemplo permita recuperar una lista de los archivos asociados al conjunto de datos.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una lista de objetos relacionados. En este ejemplo, se devuelve una lista de archivos de conjunto de datos.

```json
{
    "7d501090-0280-11ea-a6bb-f18323b7005c-1": {
        "id": "7d501090-0280-11ea-a6bb-f18323b7005c-1",
        "batchId": "7d501090-0280-11ea-a6bb-f18323b7005c",
        "dataSetViewId": "5ba9452f7de80400007fc52b",
        "imsOrg": "{IMS_ORG}",
        "createdUser": "{USER_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1573256315368,
        "updated": 1573256315368
    },
    "148ac690-0280-11ea-8d23-8571a35dce49-1": {
        "id": "148ac690-0280-11ea-8d23-8571a35dce49-1",
        "batchId": "148ac690-0280-11ea-8d23-8571a35dce49",
        "dataSetViewId": "5ba9452f7de80400007fc52b",
        "imsOrg": "{IMS_ORG}",
        "createdUser": "{USER_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1573255982433,
        "updated": 1573255982433
    },
    "64dd5e19-8ea4-4ddd-acd1-f43cccd8eddb-1": {
        "id": "64dd5e19-8ea4-4ddd-acd1-f43cccd8eddb-1",
        "batchId": "64dd5e19-8ea4-4ddd-acd1-f43cccd8eddb",
        "dataSetViewId": "5ba9452f7de80400007fc52b",
        "imsOrg": "{IMS_ORG}",
        "createdUser": "{USER_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1569499425037,
        "updated": 1569499425037
    }
}
```

## Realizar varias solicitudes en una sola llamada

El extremo raíz de la API de catálogo permite realizar varias solicitudes en una sola llamada. La carga útil de la solicitud contiene una matriz de objetos que representan lo que normalmente serían solicitudes individuales, que luego se ejecutan en orden.

Si estas solicitudes son modificaciones o adiciones al catálogo y se produce un error en cualquiera de los cambios, todos los cambios se revertirán.

**Formato API**

```http
POST /
```

**Solicitud**

La siguiente solicitud crea un nuevo conjunto de datos y, a continuación, crea vistas relacionadas para dicho conjunto de datos. En este ejemplo se muestra el uso del lenguaje de plantilla para acceder a los valores devueltos en llamadas anteriores para su uso en llamadas posteriores.

Por ejemplo, si desea hacer referencia a un valor devuelto por una subsolicitud anterior, puede crear una referencia en el formato: `<<{REQUEST_ID}.{ATTRIBUTE_NAME}>>` (donde `{REQUEST_ID}` es el ID proporcionado por el usuario para la subsolicitud, como se muestra a continuación). Puede hacer referencia a cualquier atributo disponible en el cuerpo del objeto de respuesta de una subsolicitud anterior mediante estas plantillas.

>[!NOTE] Cuando una subsolicitud ejecutada devuelve solamente la referencia a un objeto (como es el valor predeterminado para la mayoría de las solicitudes POST y PUT en la API del catálogo), esta referencia se asigna al valor `id` y se puede utilizar como `<<{OBJECT_ID}.id>>`.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
    {
      "id": "firstObjectId",
      "resource": "/dataSets",
      "method": "post",
      "body": {
        "type": "raw",
        "name": "First Dataset"
      }
    }, 
    {
      "id": "secondObjectId",
      "resource": "/datasetViews",
      "method": "post",
      "body": {
        "status": "enabled",
        "aspect": "production",
        "dataSetId": "<<firstObjectId.id>>"
      }
    }
  ]'
```

| Propiedad | Descripción |
| --- | --- |
| `id` | ID proporcionado por el usuario que se adjunta al objeto de respuesta para que pueda hacer coincidir las solicitudes con las respuestas. Catalog no almacena este valor y simplemente lo devuelve en la respuesta con fines de referencia. |
| `resource` | Ruta de recurso relativa a la raíz de la API de catálogo. El protocolo y el dominio no deben formar parte de este valor y deben tener el prefijo &quot;/&quot;. <br/><br/> Cuando utilice PATCH o DELETE como la subsolicitud `method`, incluya el ID del objeto en la ruta del recurso. No debe confundirse con el proporcionado por el usuario `id`, la ruta de acceso al recurso utiliza el ID del propio objeto Catalog (por ejemplo, `resource: "/dataSets/1234567890"`). |
| `method` | Nombre del método (GET, PUT, POST, PATCH o DELETE) relacionado con la acción que se realiza en la solicitud. |
| `body` | El documento JSON que normalmente se pasaría como carga útil en una solicitud POST, PUT o PATCH. Esta propiedad no es necesaria para solicitudes GET o DELETE. |

**Respuesta**

Una respuesta correcta devuelve una matriz de objetos que contiene el `id` que asignó a cada solicitud, el código de estado HTTP para la solicitud individual y la respuesta `body`. Dado que las tres solicitudes de muestra creaban nuevos objetos, el `body` de cada objeto es una matriz que contiene solamente el ID del objeto recién creado, como es el caso de las respuestas POST más correctas en Catalog.

```json
[
    {
        "id": "firstObjectId",
        "code": 200,
        "body": [
            "@/dataSets/5be230aef5b02914cd52dbfa"
        ]
    },
    {
        "id": "secondObjectId",
        "code": 200,
        "body": [
            "@/dataSetViews/5be230aef5b02914cd52dbfb"
        ]
    }
]
```

Tenga cuidado al inspeccionar la respuesta a una solicitud múltiple, ya que deberá verificar el código de cada subsolicitud individual y no basarse únicamente en el código de estado HTTP para la solicitud POST principal.  Es posible que una sola subsolicitud devuelva un 404 (como una solicitud GET en un recurso no válido) mientras que la solicitud global devuelve 200.

## Encabezados de solicitud adicionales

Catalog proporciona varias convenciones de encabezado para ayudarle a mantener la integridad de los datos durante las actualizaciones.

### Si-Coincidencia

Se recomienda utilizar el control de versiones de objetos para evitar el tipo de daños en los datos que se producen cuando varios usuarios guardan un objeto casi simultáneamente.

La práctica recomendada al actualizar un objeto consiste en realizar primero una llamada de API a la vista (GET) en el objeto que se va a actualizar. Incluido en la respuesta (y en cualquier llamada donde la respuesta contenga un solo objeto) es un `E-Tag` encabezado que contiene la versión del objeto. Si se Añade la versión del objeto como un encabezado de solicitud denominado `If-Match` en las llamadas de actualización (PUT o PATCH), la actualización solo se realizará correctamente si la versión sigue siendo la misma, lo que ayudará a evitar conflictos de datos.

Si las versiones no coinciden (el objeto fue modificado por otro proceso desde que lo recuperó), recibirá el estado HTTP 412 (Error de condición previa) que indica que se ha denegado el acceso al recurso de destinatario.

### Pragma

En ocasiones, es posible que desee validar un objeto sin guardar la información. El uso del `Pragma` encabezado con un valor de `validate-only` le permite enviar solicitudes POST o PUT únicamente con fines de validación, evitando que se mantengan los cambios en los datos.

## Compactación de datos

Compaction es un servicio de la plataforma de experiencias que combina datos de archivos pequeños en archivos más grandes sin cambiar ningún dato. Por motivos de rendimiento, a veces resulta beneficioso combinar un conjunto de archivos pequeños en archivos más grandes para proporcionar un acceso más rápido a los datos cuando se realiza una consulta.

Cuando se compactan los archivos de un lote ingestado, se actualiza el objeto Catalog asociado para fines de supervisión.