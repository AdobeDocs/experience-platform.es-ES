---
keywords: Experience Platform;inicio;temas populares;servicio de catálogo;api de catálogo;apéndice
solution: Experience Platform
title: Apéndice de la API del servicio de catálogo
topic-legacy: developer guide
description: Este documento contiene información adicional para ayudarle a trabajar con la API del catálogo en Adobe Experience Platform.
exl-id: fafc8187-a95b-4592-9736-cfd9d32fd135
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 1%

---

# [!DNL Catalog Service] apéndice de la guía de API

Este documento contiene información adicional para ayudarle a trabajar con la variable [!DNL Catalog] API.

## Ver objetos interrelacionados {#view-interrelated-objects}

Algunas [!DNL Catalog] los objetos se pueden interrelacionar con otros [!DNL Catalog] objetos. Todos los campos con el prefijo `@` en las cargas útiles de respuesta denotan objetos relacionados. Los valores de estos campos toman la forma de un URI, que puede utilizarse en una solicitud de GET independiente para recuperar los objetos relacionados que representan.

El conjunto de datos de ejemplo devuelto en el documento en [búsqueda de un conjunto de datos específico](look-up-object.md) contiene un `files` campo con el siguiente valor URI: `"@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"`. El contenido del `files` se puede ver utilizando este URI como la ruta para una nueva solicitud de GET.

**Formato de API**

```http
GET {OBJECT_URI}
```

| Parámetro | Descripción |
| --- | --- |
| `{OBJECT_URI}` | El URI proporcionado por el campo de objeto interrelacionado (excluido el `@` símbolo). |

**Solicitud**

La siguiente solicitud utiliza el URI, siempre que el conjunto de datos de ejemplo `files` para recuperar una lista de los archivos asociados del conjunto de datos.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una lista de objetos relacionados. En este ejemplo, se devuelve una lista de archivos de conjuntos de datos.

```json
{
    "7d501090-0280-11ea-a6bb-f18323b7005c-1": {
        "id": "7d501090-0280-11ea-a6bb-f18323b7005c-1",
        "batchId": "7d501090-0280-11ea-a6bb-f18323b7005c",
        "dataSetViewId": "5ba9452f7de80400007fc52b",
        "imsOrg": "{ORG_ID}",
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
        "imsOrg": "{ORG_ID}",
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
        "imsOrg": "{ORG_ID}",
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

El extremo raíz de la variable [!DNL Catalog] La API permite realizar varias solicitudes dentro de una sola llamada. La carga útil de la solicitud contiene una matriz de objetos que representan lo que normalmente serían solicitudes individuales, que luego se ejecutan en orden.

Si estas solicitudes son modificaciones o adiciones a [!DNL Catalog] y cualquiera de los cambios falla, todos los cambios se revertirán.

**Formato de API**

```http
POST /
```

**Solicitud**

La siguiente solicitud crea un nuevo conjunto de datos y luego crea vistas relacionadas para ese conjunto de datos. Este ejemplo muestra el uso del lenguaje de plantilla para acceder a los valores devueltos en llamadas anteriores para su uso en llamadas posteriores.

Por ejemplo, si desea hacer referencia a un valor devuelto por una subsolicitud anterior, puede crear una referencia con el formato : `<<{REQUEST_ID}.{ATTRIBUTE_NAME}>>` (donde `{REQUEST_ID}` es el ID proporcionado por el usuario para la subsolicitud, como se muestra a continuación). Puede hacer referencia a cualquier atributo disponible en el cuerpo del objeto Response de una subsolicitud anterior utilizando estas plantillas.

>[!NOTE]
>
>Cuando una subsolicitud ejecutada devuelve solo la referencia a un objeto (como es el valor predeterminado para la mayoría de las solicitudes de POST y PUT de la API del catálogo), esta referencia se asocia al valor `id` y pueden utilizarse como  `<<{OBJECT_ID}.id>>`.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
        "dataSetId": "<<firstObjectId.id>>"
      }
    }
  ]'
```

| Propiedad | Descripción |
| --- | --- |
| `id` | ID proporcionado por el usuario que está adjunto al objeto Response para que pueda hacer coincidir las solicitudes con las respuestas. [!DNL Catalog] no almacena este valor y simplemente lo devuelve en la respuesta con fines de referencia. |
| `resource` | La ruta del recurso en relación con la raíz del [!DNL Catalog] API. El protocolo y el dominio no deben formar parte de este valor y debe añadirse el prefijo &quot;/&quot;. <br/><br/> Cuando se utiliza un PATCH o un DELETE como el de la subsolicitud `method`, incluya el ID de objeto en la ruta del recurso. No confundir con el `id`, la ruta del recurso utiliza el ID de la variable [!DNL Catalog] propio objeto (por ejemplo, `resource: "/dataSets/1234567890"`). |
| `method` | Nombre del método (GET, PUT, POST, PATCH o DELETE) relacionado con la acción que se está realizando en la solicitud. |
| `body` | El documento JSON que normalmente se pasaría como carga útil en una solicitud de POST, PUT o PATCH. Esta propiedad no es necesaria para solicitudes de GET o DELETE. |

**Respuesta**

Una respuesta correcta devuelve una matriz de objetos que contienen la variable `id` que asignó a cada solicitud, el código de estado HTTP para la solicitud individual y la respuesta `body`. Dado que las tres solicitudes de ejemplo creaban nuevos objetos, la variable `body` de cada objeto es una matriz que contiene únicamente el ID del objeto recién creado, como es el estándar con las respuestas del POST más exitosas en [!DNL Catalog].

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

Tenga cuidado al inspeccionar la respuesta a una solicitud múltiple, ya que tendrá que comprobar el código de cada subsolicitud individual y no depender únicamente del código de estado HTTP para la solicitud del POST principal.  Es posible que una sola subsolicitud devuelva un 404 (como una solicitud de GET en un recurso no válido) mientras que la solicitud general devuelve 200.

## Encabezados de solicitud adicionales

[!DNL Catalog] proporciona varias convenciones de encabezado para ayudarle a mantener la integridad de los datos durante las actualizaciones.

### Si-Coincidencia

Se recomienda utilizar el control de versiones de objetos para evitar el tipo de corrupción de datos que se produce cuando varios usuarios guardan un objeto casi simultáneamente.

Una práctica recomendada al actualizar un objeto consiste en realizar primero una llamada API para ver (GET) el objeto que se va a actualizar. Incluida en la respuesta (y cualquier llamada donde la respuesta contenga un solo objeto) es una `E-Tag` que contiene la versión del objeto. Adición de la versión del objeto como un encabezado de solicitud denominado `If-Match` en las llamadas de actualización (PUT o PATCH), la actualización solo se realizará correctamente si la versión sigue siendo la misma, lo que ayudará a evitar conflictos de datos.

Si las versiones no coinciden (el objeto fue modificado por otro proceso desde que lo recuperó), recibirá el estado HTTP 412 (Error de precondición) que indica que se ha denegado el acceso al recurso de destino.

### Pragma

En ocasiones, es posible que desee validar un objeto sin guardar la información. Al usar la variable `Pragma` encabezado con un valor de `validate-only` permite enviar solicitudes de POST o PUT únicamente con fines de validación, lo que evita que se mantengan los cambios en los datos.

## Compactación de datos

La compactación es una [!DNL Experience Platform] que combina datos de archivos pequeños en archivos más grandes sin cambiar ningún dato. Por motivos de rendimiento, a veces resulta beneficioso combinar un conjunto de archivos pequeños en archivos más grandes para proporcionar un acceso más rápido a los datos cuando se realizan consultas.

Cuando se compactan los archivos de un lote ingerido, su [!DNL Catalog] se actualiza para fines de monitorización.
