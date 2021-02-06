---
keywords: Experience Platform;inicio;temas populares;servicio de catálogo;api de catálogo;apéndice
solution: Experience Platform
title: Apéndice de la API del servicio de catálogo
topic: developer guide
description: Este documento contiene información adicional para ayudarle a trabajar con la API de catálogo en Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: b395535cbe7e4030606ee2808eb173998f5c32e0
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 1%

---


# [!DNL Catalog Service] Apéndice de la guía de API

Este documento contiene información adicional para ayudarle a trabajar con la API [!DNL Catalog].

## Objetos interrelacionados de vista {#view-interrelated-objects}

Algunos objetos [!DNL Catalog] pueden interrelacionarse con otros objetos [!DNL Catalog]. Los campos con el prefijo `@` en las cargas de respuesta indican objetos relacionados. Los valores de estos campos toman la forma de un URI, que puede utilizarse en una solicitud de GET independiente para recuperar los objetos relacionados que representan.

El conjunto de datos de ejemplo devuelto en el documento el [buscar un conjunto de datos específico](look-up-object.md) contiene un campo `files` con el siguiente valor URI: `"@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"`. El contenido del campo `files` se puede ver usando este URI como ruta para una nueva solicitud de GET.

**Formato API**

```http
GET {OBJECT_URI}
```

| Parámetro | Descripción |
| --- | --- |
| `{OBJECT_URI}` | URI proporcionado por el campo de objeto interrelacionado (excluido el símbolo `@`). |

**Solicitud**

La siguiente solicitud utiliza el URI proporcionado por la propiedad `files` del conjunto de datos de ejemplo para recuperar una lista de los archivos asociados al conjunto de datos.

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

El extremo raíz de la API [!DNL Catalog] permite realizar varias solicitudes dentro de una sola llamada. La carga útil de la solicitud contiene una matriz de objetos que representan lo que normalmente serían solicitudes individuales, que luego se ejecutan en orden.

Si estas solicitudes son modificaciones o adiciones a [!DNL Catalog] y cualquiera de los cambios falla, todos los cambios se revertirán.

**Formato API**

```http
POST /
```

**Solicitud**

La siguiente solicitud crea un nuevo conjunto de datos y, a continuación, crea vistas relacionadas para dicho conjunto de datos. En este ejemplo se muestra el uso del lenguaje de plantilla para acceder a los valores devueltos en llamadas anteriores para su uso en llamadas posteriores.

Por ejemplo, si desea hacer referencia a un valor devuelto por una subsolicitud anterior, puede crear una referencia en el formato: `<<{REQUEST_ID}.{ATTRIBUTE_NAME}>>` (donde `{REQUEST_ID}` es el ID proporcionado por el usuario para la subsolicitud, como se muestra a continuación). Puede hacer referencia a cualquier atributo disponible en el cuerpo del objeto de respuesta de una subsolicitud anterior mediante estas plantillas.

>[!NOTE]
>
>Cuando una subsolicitud ejecutada devuelve sólo la referencia a un objeto (como es el valor predeterminado para la mayoría de las solicitudes de POST y PUT en la API de catálogo), esta referencia se asigna al valor `id` y se puede utilizar como `<<{OBJECT_ID}.id>>`.

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
        "dataSetId": "<<firstObjectId.id>>"
      }
    }
  ]'
```

| Propiedad | Descripción |
| --- | --- |
| `id` | ID proporcionado por el usuario que se adjunta al objeto de respuesta para que pueda hacer coincidir las solicitudes con las respuestas. [!DNL Catalog] no almacena este valor y simplemente lo devuelve en la respuesta con fines de referencia. |
| `resource` | La ruta del recurso en relación con la raíz de la API [!DNL Catalog]. El protocolo y el dominio no deben formar parte de este valor y deben tener el prefijo &quot;/&quot;. <br/><br/> Cuando utilice PATCH o DELETE como subsolicitud  `method`, incluya la ID del objeto en la ruta de acceso del recurso. No debe confundirse con el `id` proporcionado por el usuario, la ruta de recursos utiliza el ID del propio objeto [!DNL Catalog] (por ejemplo, `resource: "/dataSets/1234567890"`). |
| `method` | Nombre del método (GET, PUT, POST, PATCH o DELETE) relacionado con la acción que se realiza en la solicitud. |
| `body` | El documento JSON que normalmente se pasaría como carga útil en una solicitud de POST, PUT o PATCH. Esta propiedad no es necesaria para solicitudes de GET o DELETE. |

**Respuesta**

Una respuesta correcta devuelve una matriz de objetos que contiene el `id` asignado a cada solicitud, el código de estado HTTP para la solicitud individual y la respuesta `body`. Dado que las tres solicitudes de muestra creaban nuevos objetos, la `body` de cada objeto es una matriz que contiene solamente la ID del objeto recién creado, como es el estándar con las respuestas de POST más exitosas en [!DNL Catalog].

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

Tenga cuidado al inspeccionar la respuesta a una solicitud múltiple, ya que deberá comprobar el código de cada subsolicitud individual y no basarse únicamente en el código de estado HTTP para la solicitud del POST principal.  Es posible que una sola subsolicitud devuelva un 404 (como una solicitud de GET en un recurso no válido) mientras que la solicitud global devuelve 200.

## Encabezados de solicitud adicionales

[!DNL Catalog] proporciona varias convenciones de encabezado para ayudarle a mantener la integridad de los datos durante las actualizaciones.

### Si-Coincidencia

Se recomienda utilizar el control de versiones de objetos para evitar el tipo de daños en los datos que se producen cuando varios usuarios guardan un objeto casi simultáneamente.

La práctica recomendada al actualizar un objeto consiste en realizar primero una llamada de API a la vista (GET) del objeto que se va a actualizar. El encabezado `E-Tag` que contiene la versión del objeto está contenido en la respuesta (y en cualquier llamada en la que la respuesta contenga un solo objeto). Si se añade la versión del objeto como un encabezado de solicitud denominado `If-Match` en las llamadas de actualización (PUT o PATCH), la actualización solo se realizará correctamente si la versión sigue siendo la misma, lo que ayudará a evitar conflictos de datos.

Si las versiones no coinciden (el objeto fue modificado por otro proceso desde que lo recuperó), recibirá el estado HTTP 412 (Error de condición previa) que indica que se ha denegado el acceso al recurso de destinatario.

### Pragma

En ocasiones, es posible que desee validar un objeto sin guardar la información. El uso del encabezado `Pragma` con un valor de `validate-only` le permite enviar solicitudes de POST o PUT únicamente con fines de validación, lo que evita que se mantengan los cambios en los datos.

## Compactación de datos

Compaction es un servicio [!DNL Experience Platform] que combina datos de archivos pequeños en archivos más grandes sin cambiar ningún dato. Por motivos de rendimiento, a veces resulta beneficioso combinar un conjunto de archivos pequeños en archivos más grandes para proporcionar un acceso más rápido a los datos cuando se realiza una consulta.

Cuando se compactan los archivos de un lote ingestado, su objeto [!DNL Catalog] asociado se actualiza para fines de supervisión.