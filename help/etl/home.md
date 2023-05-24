---
keywords: Experience Platform;inicio;temas populares;ETL;etl;integraciones de etl;integraciones de ETL
solution: Experience Platform
title: Desarrollo de integraciones de ETL para Adobe Experience Platform
description: La guía de integración de ETL describe los pasos generales para crear conectores seguros de alto rendimiento para Experience Platform e ingerir datos en Platform.
exl-id: 7d29b61c-a061-46f8-a31f-f20e4d725655
source-git-commit: 76ef5638316a89aee1c6fb33370af943228b75e1
workflow-type: tm+mt
source-wordcount: '4081'
ht-degree: 1%

---

# Desarrollo de integraciones de ETL para Adobe Experience Platform

La guía de integración de ETL describe los pasos generales para crear conectores seguros de alto rendimiento para [!DNL Experience Platform] e ingesta de datos en [!DNL Platform].


- [[!DNL Catalog]](https://www.adobe.io/experience-platform-apis/references/catalog/)
- [[!DNL Data Access]](https://www.adobe.io/experience-platform-apis/references/data-access/)
- [[!DNL Batch Ingestion]](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/)
- [[!DNL Streaming Ingestion]](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/)
- [Autenticación y autorización para las API de Experience Platform](https://www.adobe.com/go/platform-api-authentication-en)
- [[!DNL Schema Registry]](https://www.adobe.io/experience-platform-apis/references/schema-registry/)

Esta guía también incluye llamadas de API de ejemplo para utilizar al diseñar un conector ETL, con vínculos a documentación que describe cada uno [!DNL Experience Platform] y el uso de su API, con más detalle.

Hay una integración de muestra disponible en [!DNL GitHub] a través de [Código de referencia de integración de ecosistemas ETL](https://github.com/adobe/acp-data-services-etl-reference) en el [!DNL Apache] Versión de licencia 2.0.

## Flujo de trabajo

El siguiente diagrama de flujo de trabajo proporciona información general de alto nivel sobre la integración de componentes de Adobe Experience Platform con una aplicación y un conector de ETL.

![](images/etl.png)

## Componentes de Adobe Experience Platform

Hay varios componentes de Experience Platform involucrados en las integraciones del conector ETL. La siguiente lista describe varios componentes y funcionalidades clave:

- **Adobe Identity Management System (IMS)** : proporciona el marco para la autenticación en los servicios de Adobe.
- **Organización IMS** - Una entidad corporativa que puede poseer o licenciar productos y servicios y permitir el acceso a sus miembros.
- **Usuario de IMS** - Miembros de una organización IMS. La relación entre la organización y el usuario es de muchos a muchos.
- **[!DNL Sandbox]** - Una partición virtual un solo [!DNL Platform] por ejemplo, para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.
- **Detección de datos** : Registra los metadatos de los datos ingeridos y transformados en [!DNL Experience Platform].
- **[!DNL Data Access]** : Proporciona a los usuarios una interfaz para acceder a sus datos en [!DNL Experience Platform].
- **[!DNL Data Ingestion]** : inserta los datos en [!DNL Experience Platform] con [!DNL Data Ingestion] API.
- **[!DNL Schema Registry]** : define y almacena un esquema que describe la estructura de datos que se va a utilizar en [!DNL Experience Platform].

## Introducción a [!DNL Experience Platform] API

Las secciones siguientes proporcionan información adicional que deberá conocer o tener disponible para poder realizar llamadas correctamente a [!DNL Experience Platform] API.

### Leer llamadas de API de muestra

Esta guía proporciona ejemplos de llamadas API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../landing/troubleshooting.md#how-do-i-format-an-api-request) en el [!DNL Experience Platform] guía de solución de problemas.

### Recopilar valores para los encabezados obligatorios

Para realizar llamadas a [!DNL Platform] API, primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todas las [!DNL Experience Platform] Llamadas de API, como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Todos los recursos de [!DNL Experience Platform] están aisladas para zonas protegidas virtuales específicas. Todas las solicitudes a [!DNL Platform] Las API requieren un encabezado que especifique el nombre de la zona protegida en la que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre las zonas protegidas en [!DNL Platform], consulte la [documentación general de zona protegida](../sandboxes/home.md).

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

- Content-Type: application/json

## Flujo de usuario general

Para empezar, un usuario de ETL inicia sesión en [!DNL Experience Platform] interfaz de usuario (IU) y crea conjuntos de datos para su ingesta mediante un conector estándar o un conector de servicio push.

En la interfaz de usuario de, el usuario crea el conjunto de datos de salida seleccionando un esquema del conjunto de datos. La elección del esquema depende del tipo de datos (registro o serie temporal) que se estén introduciendo en [!DNL Platform]. Al hacer clic en la pestaña Esquemas dentro de la interfaz de usuario, el usuario puede ver todos los esquemas disponibles, incluido el tipo de comportamiento que admite el esquema.

En la herramienta ETL, el usuario empezará a diseñar sus transformaciones de asignación después de configurar la conexión adecuada (con sus credenciales). Se supone que la herramienta ETL ya tiene [!DNL Experience Platform] conectores instalados (proceso no definido en esta guía de integración).

Se han proporcionado maquetas para una herramienta y un flujo de trabajo de ETL de muestra en la [Flujo de trabajo de ETL](./workflow.md). Aunque las herramientas de ETL pueden diferir en formato, la mayoría exponen una funcionalidad similar.

>[!NOTE]
>
>El conector ETL debe especificar un filtro de marca de hora que marque la fecha de ingesta de datos y el desplazamiento (es decir, Ventana para la que se van a leer los datos). La herramienta ETL debe admitir la toma de estos dos parámetros en esta u otra interfaz de usuario relevante. En Adobe Experience Platform, estos parámetros se asignarán a las fechas disponibles (si están presentes) o a las fechas capturadas presentes en el objeto por lotes del conjunto de datos.

### Ver la lista de conjuntos de datos

Utilizando el origen de los datos para la asignación, se puede obtener una lista de todos los conjuntos de datos disponibles utilizando [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/).

Puede emitir una sola solicitud de API para ver todos los conjuntos de datos disponibles (por ejemplo, `GET /dataSets`), siendo la práctica recomendada incluir parámetros de consulta que limiten el tamaño de la respuesta.

En los casos en los que se solicita información completa del conjunto de datos, la carga útil de respuesta puede alcanzar más de 3 GB de tamaño, lo que puede ralentizar el rendimiento general. Por lo tanto, si utiliza parámetros de consulta para filtrar solo la información necesaria, [!DNL Catalog] consultas más eficientes.

#### Filtrado de listas

Al filtrar las respuestas, puede utilizar varios filtros en una sola llamada separando los parámetros con un signo &amp; (`&`). Algunos parámetros de consulta aceptan listas de valores separadas por comas, como el filtro &quot;propiedades&quot; de la solicitud de ejemplo siguiente.

[!DNL Catalog] las respuestas se miden automáticamente según los límites configurados, pero el parámetro de consulta &quot;limit&quot; se puede utilizar para personalizar las restricciones y limitar el número de objetos devueltos. El preconfigurado [!DNL Catalog] los límites de respuesta son:

- Si no se especifica un parámetro limit, el número máximo de objetos por carga útil de respuesta es de 20.
- El límite global para todos los demás [!DNL Catalog] queries tiene 100 objetos.
- Para las consultas de conjuntos de datos, si observableSchema se solicita mediante el parámetro de consulta de propiedades, el número máximo de conjuntos de datos devueltos es 20.
- Parámetros de límite no válidos (incluidos `limit=0`) se encuentran con un error HTTP 400 que describe los intervalos adecuados.
- Si los límites o desplazamientos se pasan como parámetros de consulta, tienen prioridad sobre los que se pasan como encabezados.

Los parámetros de consulta se tratan de forma más detallada en la [Resumen del servicio de catálogo](../catalog/home.md).

**Formato de API**

```http
GET /catalog/dataSets
GET /catalog/dataSets?{filter1}={value1},{value2}&{filter2}={value3}
```

**Solicitud**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets?limit=3&properties=name,description,schemaRef" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

Consulte la [Resumen del servicio de catálogo](../catalog/home.md) para ver ejemplos detallados de cómo realizar llamadas a [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/).

**Respuesta**

La respuesta incluye tres (`limit=3`) conjuntos de datos que muestran el &quot;nombre&quot;, &quot;descripción&quot; y &quot;schemaRef&quot; tal como indica la variable `properties` parámetro de consulta.

```json
{
    "5b95b155419ec801e6eee780": {
        "name": "Store Transactions",
        "description": "Retails Store Transactions",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    },
    "5c351fa2f5fee300000fa9e8": {
        "name": "Loyalty Members",
        "description": "Loyalty Program Members",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    },
    "5c1823b19e6f400000993885": {
        "name": "Web Traffic",
        "description": "Retail Web Traffic",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/2025a705890c6d4a4a06b16f8cf6f4ca",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    }
}
```

### Ver esquema del conjunto de datos

La propiedad &quot;schemaRef&quot; de un conjunto de datos contiene un URI que hace referencia al esquema XDM en el que se basa el conjunto de datos. El esquema XDM (&quot;schemaRef&quot;) representa todos los campos potenciales que podría utilizar el conjunto de datos, no necesariamente los campos que se están utilizando (consulte &quot;observableSchema&quot; a continuación).

El esquema XDM es el esquema que se utiliza cuando se necesita presentar al usuario una lista de todos los campos disponibles en los que se puede escribir.

El primer valor &quot;schemaRef.id&quot; del objeto de respuesta anterior (`https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18`) es un URI que apunta a un esquema XDM específico en el [!DNL Schema Registry]. El esquema se puede recuperar realizando una solicitud de consulta (GET) a [!DNL Schema Registry] API.

>[!NOTE]
>
>La propiedad &quot;schemaRef&quot; reemplaza a la propiedad &quot;schema&quot;, que ya está en desuso. Si &quot;schemaRef&quot; está ausente del conjunto de datos o no contiene un valor, deberá comprobar la presencia de una propiedad &quot;schema&quot;. Esto se puede hacer reemplazando &quot;schemaRef&quot; por &quot;schema&quot; en `properties` parámetro de consulta en la llamada anterior. Encontrará más información sobre la propiedad &quot;schema&quot; en la [Propiedad &quot;schema&quot; del conjunto de datos](#dataset-schema-property-deprecated---eol-2019-05-30) que sigue.

**Formato de API**

```http
GET /schemaregistry/tenant/schemas/{url encoded schemaRef.id}
```

**Solicitud**

La solicitud utiliza la dirección URL codificada `id` URI del esquema (el valor del atributo &quot;schemaRef.id&quot;) y requiere un encabezado Aceptar.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F274f17bc5807ff307a046bab1489fb18 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
```

El formato de respuesta depende del tipo de encabezado Aceptar enviado en la solicitud. Las solicitudes de búsqueda también requieren un `version` se incluirá en el encabezado Aceptar. En la tabla siguiente se describen los encabezados Aceptar disponibles para las búsquedas:

| Accept | Descripción |
| ------ | ----------- |
| `application/vnd.adobe.xed-id+json` | Enumeración de solicitudes, títulos, ID y versiones (GET) |
| `application/vnd.adobe.xed-full+json; version={major version}` | $refs y allOf resueltos, tiene títulos y descripciones |
| `application/vnd.adobe.xed+json; version={major version}` | Raw con $ref y allOf, tiene títulos y descripciones |
| `application/vnd.adobe.xed-notext+json; version={major version}` | Sin procesar con $ref y allOf, sin títulos ni descripciones |
| `application/vnd.adobe.xed-full-notext+json; version={major version}` | $refs y allOf resueltos, sin títulos ni descripciones |
| `application/vnd.adobe.xed-full-desc+json; version={major version}` | $refs y allOf resueltos, descriptores incluidos |

>[!NOTE]
>
>`application/vnd.adobe.xed-id+json` y `application/vnd.adobe.xed-full+json; version={major version}` son los encabezados Aceptar más utilizados. `application/vnd.adobe.xed-id+json` es la opción preferida para enumerar recursos en [!DNL Schema Registry] ya que solo devuelve el &quot;título&quot;, &quot;id&quot; y &quot;versión&quot;. `application/vnd.adobe.xed-full+json; version={major version}` se prefiere para ver un recurso específico (por su &quot;id&quot;), ya que devuelve todos los campos (anidados en &quot;propiedades&quot;), así como títulos y descripciones.

**Respuesta**

El esquema JSON devuelto describe la estructura y la información de nivel de campo (&quot;tipo&quot;, &quot;formato&quot;, &quot;mínimo&quot;, &quot;máximo&quot;, etc.) de los datos, serializados como JSON. Si utiliza un formato de serialización distinto de JSON para la ingesta (como Parquet o Scala), la variable [Guía del Registro de esquemas](../xdm/tutorials/create-schema-api.md) contiene una tabla que muestra el tipo JSON deseado (&quot;meta:xdmType&quot;) y su representación correspondiente en otros formatos.

Junto con esta tabla, la variable [!DNL Schema Registry] Developer Guide contiene ejemplos detallados de todas las posibles llamadas que se pueden realizar utilizando [!DNL Schema Registry] API.

### Propiedad &quot;schema&quot; del conjunto de datos (OBSOLETO: EOL 2019-05-30)

Los conjuntos de datos pueden contener una propiedad &quot;schema&quot; que ya no se utiliza y que permanece disponible temporalmente para la compatibilidad con versiones anteriores. Por ejemplo, una solicitud de listado (GET) similar a la realizada anteriormente, donde &quot;schema&quot; se sustituyó por &quot;schemaRef&quot; en `properties` parámetro de consulta, puede devolver lo siguiente:

```json
{
  "5ba9452f7de80400007fc52a": {
    "name": "Sample Dataset 1",
    "description": "Description of Sample Dataset 1.",
    "schema": "@/xdms/context/person"
  }
}
```

Si se rellena la propiedad &quot;schema&quot; de un conjunto de datos, esto indica que el esquema está en desuso `/xdms` y, cuando sea compatible, el conector ETL debe utilizar el valor de la propiedad &quot;schema&quot; con el `/xdms` extremo (un extremo obsoleto en el [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/)) para recuperar el esquema heredado.

**Formato de API**

```http
GET /catalog/{"schema" property without the "@"}
```

**Solicitud**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/xdms/context/person?expansion=xdm" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

>[!NOTE]
>
>Un parámetro de consulta opcional, `expansion=xdm`, indica a la API que expanda completamente y en línea cualquier esquema al que se haga referencia. Puede que desee hacerlo cuando presente una lista de todos los campos potenciales al usuario.

**Respuesta**

Similar a los pasos de [ver esquema del conjunto de datos](#view-dataset-schema), la respuesta contiene un esquema JSON que describe la estructura y la información de nivel de campo de los datos, serializados como JSON.

>[!NOTE]
>
>Cuando el campo &quot;schema&quot; está vacío o ausente por completo, el conector debe leer el campo &quot;schemaRef&quot; y utilizar [API de Registro de esquemas](https://www.adobe.io/experience-platform-apis/references/schema-registry/) como se muestra en los pasos anteriores para [ver un esquema del conjunto de datos](#view-dataset-schema).

### La propiedad &quot;observableSchema&quot;

La propiedad &quot;observableSchema&quot; de un conjunto de datos tiene una estructura JSON que coincide con la del esquema XDM JSON. El &quot;observableSchema&quot; contiene los campos que estaban presentes en los archivos de entrada entrantes. Al escribir datos en [!DNL Experience Platform]Sin embargo, un usuario no es necesario para utilizar cada campo del esquema de destino. En su lugar, deben proporcionar solo los campos que se están utilizando.

El esquema observable es el esquema que se utiliza para leer los datos o presentar una lista de campos disponibles para leer o asignar.

```json
{
    "598d6e81b2745f000015edcb": {
        "observableSchema": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "name": {
                    "type": "string",
                },
                "age": {
                    "type": "string",
                }
            }
        }
    }
}
```

### Previsualización de datos

La aplicación ETL puede proporcionar una capacidad de previsualización de datos ([&quot;Figura 8&quot; en el flujo de trabajo de ETL](./workflow.md)). La API de acceso a datos proporciona varias opciones para obtener una vista previa de los datos.

Encontrará información adicional, incluidas instrucciones paso a paso para obtener una vista previa de los datos mediante la API de acceso a datos, en la [tutorial de acceso a datos](../data-access/tutorials/dataset-data.md).

### Obtener detalles del conjunto de datos mediante el parámetro de consulta &quot;properties&quot;

Como se muestra en los pasos anteriores a [ver una lista de conjuntos de datos](#view-list-of-datasets), puede solicitar &quot;files&quot; utilizando el parámetro de consulta &quot;properties&quot;.

Puede consultar el [Resumen del servicio de catálogo](../catalog/home.md) para obtener información detallada sobre la consulta de conjuntos de datos y filtros de respuesta disponibles.

**Formato de API**

```http
GET /catalog/dataSets?limit={value}&properties={value}
```

**Solicitud**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets?limit=1&properties=files" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

**Respuesta**

La respuesta incluirá un conjunto de datos (`limit=1`) mostrando la propiedad &quot;files&quot;.

```json
{
  "5bf479a6a8c862000050e3c7": {
    "files": "@/dataSets/5bf479a6a8c862000050e3c7/views/5bf479a654f52014cfffe7f1/files"
  }
}
```

### Enumerar archivos de conjuntos de datos mediante el atributo &quot;files&quot;

También puede utilizar una solicitud de GET para recuperar los detalles del archivo mediante el atributo &quot;files&quot;.

**Formato de API**

```http
GET /catalog/dataSets/{DATASET_ID}/views/{VIEW_ID}/files
```

**Solicitud**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets/5bf479a6a8c862000050e3c7/views/5bf479a654f52014cfffe7f1/files" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Respuesta**

La respuesta incluye el ID del archivo del conjunto de datos como propiedad de nivel superior, con detalles del archivo contenidos en el objeto ID del archivo del conjunto de datos.

```json
{
    "194e89b976494c9c8113b968c27c1472-1": {
        "batchId": "194e89b976494c9c8113b968c27c1472",
        "dataSetViewId": "5bf479a654f52014cfffe7f1",
        "imsOrg": "{ORG_ID}",
        "availableDates": {},
        "createdUser": "{USER_ID}",
        "createdClient": "{API_KEY}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1542749145828,
        "updated": 1542749145828
    },
    "14d5758c107443e1a83c714e56ca79d0-1": {
        "batchId": "14d5758c107443e1a83c714e56ca79d0",
        "dataSetViewId": "5bf479a654f52014cfffe7f1",
        "imsOrg": "{ORG_ID}",
        "availableDates": {},
        "createdUser": "{USER_ID}",
        "createdClient": "{API_KEY}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1542752699111,
        "updated": 1542752699111
    },
    "ea40946ac03140ec8ac4f25da360620a-1": {
        "batchId": "ea40946ac03140ec8ac4f25da360620a",
        "dataSetViewId": "5bf479a654f52014cfffe7f1",
        "imsOrg": "{ORG_ID}",
        "availableDates": {},
        "createdUser": "{USER_ID}",
        "createdClient": "{API_KEY}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1542756935535,
        "updated": 1542756935535
    }
}
```

### Buscar detalles del archivo

Los ID de archivo del conjunto de datos devueltos en la respuesta anterior se pueden utilizar en una solicitud de GET para obtener más detalles del archivo mediante la variable [!DNL Data Access] API.

El [información general de acceso a datos](../data-access/home.md) contiene detalles sobre cómo utilizar el [!DNL Data Access] API.

**Formato de API**

```http
GET /export/files/{DATASET_FILE_ID}
```

**Solicitud**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Respuesta**

```json
[
    {
    "name": "{FILE_NAME}.parquet",
    "length": 2576,
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1?path=samplefile.parquet"
            }
        }
    }
]
```

### Previsualizar datos de archivo

La propiedad &quot;href&quot; se puede utilizar para obtener datos de vista previa a través de la variable [[!DNL Data Access API]](../data-access/home.md).

**Formato de API**

```http
GET /export/files/{FILE_ID}?path={FILE_NAME}.{FILE_FORMAT}
```

**Solicitud**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1?path=samplefile.parquet" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

La respuesta a la solicitud anterior contiene una previsualización del contenido del archivo.

Más información sobre la [!DNL Data Access] La API de, incluidas las solicitudes y respuestas detalladas, está disponible en la [información general de acceso a datos](../data-access/home.md).

### Obtener &quot;fileDescription&quot; del conjunto de datos

El componente de destino como salida de datos transformados, el ingeniero de datos elegirá un conjunto de datos de salida ([&quot;Figura 12&quot; en el flujo de trabajo de ETL](workflow.md)). El esquema XDM está asociado con el conjunto de datos de salida. Los datos que se van a escribir se identificarán con el atributo &quot;fileDescription&quot; de la entidad del conjunto de datos desde las API de detección de datos. Esta información se puede recuperar mediante una ID de conjunto de datos (`{DATASET_ID}`). La propiedad &quot;fileDescription&quot; de la respuesta JSON proporcionará la información solicitada.

**Formato de API**

```shell
GET /catalog/dataSets/{DATASET_ID}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{DATASET_ID}` | El `id` del conjunto de datos al que está intentando acceder. |

**Solicitud**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets/59c93f3da7d0c00000798f68" \
-H "accept: application/json" \
-H "x-gw-ims-org-id: {ORG_ID}" \
-H "x-sandbox-name: {SANDBOX_NAME}" \
-H "Authorization: Bearer {ACCESS_TOKEN}" \
-H "x-api-key: {API_KEY}"
```

**Respuesta**

```JSON
{
  "59c93f3da7d0c00000798f68": {
    "version": "1.0.4",
    "fileDescription": {
        "persisted": false,
        "format": "parquet"
    }
  }
}
```

Los datos se escribirán en [!DNL Experience Platform] uso del [API de ingesta por lotes](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/).  La escritura de datos es un proceso asincrónico. Cuando se escriben datos en Adobe Experience Platform, se crea un lote y se marca como un éxito solo después de que se hayan escrito completamente los datos.

Datos en [!DNL Experience Platform] debe escribirse en forma de archivos de Parquet.

## Fase de ejecución

A medida que se inicia la ejecución, el conector (tal como se define en el componente de origen) leerá los datos de [!DNL Experience Platform] uso del [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/). El proceso de transformación leerá los datos durante un intervalo de tiempo determinado. Internamente, consultará lotes de conjuntos de datos de origen. Al realizar la consulta, se utilizan archivos de conjuntos de datos de lista y fecha de inicio parametrizados (móviles para datos de series temporales o datos incrementales) para esos lotes y se comienza a realizar solicitudes de datos para esos archivos de conjuntos de datos.

### Transformaciones de ejemplo

El [transformaciones de ETL de muestra](./transformations.md) Este documento contiene una serie de transformaciones de ejemplo, incluida la administración de identidades y las asignaciones de tipo de datos. Utilice estas transformaciones como referencia.

### Leer datos de [!DNL Experience Platform]

Uso del [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/)Además, puede recuperar todos los lotes entre una hora de inicio y una hora de finalización especificadas y ordenarlos por el orden en que se crearon.

**Solicitud**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?dataSet=DATASETID&createdAfter=START_TIMESTAMP&createdBefore=END_TIMESTAMP&sort=desc:created" \
  -H "Accept: application/json" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

Puede encontrar más información sobre el filtrado de lotes en la [Tutorial de acceso a datos](../data-access/tutorials/dataset-data.md).

### Obtener archivos de un lote

Una vez que tenga el ID del lote que está buscando (`{BATCH_ID}`), es posible recuperar una lista de archivos que pertenecen a un lote específico mediante el [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/).  Los detalles para hacerlo están disponibles en la [[!DNL Data Access] tutorial](../data-access/tutorials/dataset-data.md).

**Solicitud**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/files" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

### Acceso a archivos mediante el ID de archivo

Usar el ID único de un archivo (`{FILE_ID`), el [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) se puede utilizar para acceder a los detalles específicos del archivo, incluido su nombre, tamaño en bytes y un vínculo para descargarlo.

**Solicitud**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{FILE_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

La respuesta puede apuntar a un solo archivo o a un directorio. Los detalles de cada uno se encuentran en la [[!DNL Data Access] tutorial](../data-access/tutorials/dataset-data.md).

### Acceder al contenido del archivo

El [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) se puede utilizar para acceder al contenido de un archivo específico. Para recuperar el contenido, se realiza una solicitud de GET utilizando el valor devuelto para `_links.self.href` al acceder a un archivo mediante el ID de archivo.

**Solicitud**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{DATASET_FILE_ID}?path=filename1.csv" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

La respuesta a esta solicitud contiene el contenido del archivo. Para obtener más información, incluidos detalles sobre la paginación de respuestas, consulte la [Cómo consultar datos a través de la API de acceso a datos](../data-access/tutorials/dataset-data.md) tutorial.

### Validar registros para el cumplimiento de esquemas

Cuando se escriben datos, los usuarios pueden optar por validarlos según las reglas de validación definidas en el esquema XDM. Encontrará más información sobre la validación de esquemas en la [Código de referencia de la integración de ecosistemas ETL en [!DNL GitHub]](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md#validation).

Si utiliza la implementación de referencia que se encuentra en [[!DNL GitHub]](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md), puede activar la validación de esquemas en esta implementación mediante la propiedad del sistema `-DenableSchemaValidation=true`.

La validación se puede realizar para tipos XDM lógicos, utilizando atributos como `minLength` y `maxlength` para cadenas, `minimum` y `maximum` para números enteros y más. El [Guía para desarrolladores de API de Registro de esquemas](../xdm/api/getting-started.md) contiene una tabla que describe los tipos XDM y las propiedades que se pueden utilizar para la validación.

>[!NOTE]
>
>Los valores mínimos y máximos previstos para varios `integer` Los tipos son los valores MIN y MAX que puede admitir el tipo, pero estos valores se pueden restringir aún más a los mínimos y máximos que elija.

### Crear un lote

Una vez procesados los datos, la herramienta ETL volverá a escribir los datos en [!DNL Experience Platform] uso del [API de ingesta por lotes](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/). Para poder agregar datos a un conjunto de datos, deben vincularse a un lote que luego se cargará en un conjunto de datos específico.

**Solicitud**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -d '{
        "datasetId":"{DATASET_ID}"
      }'
```

Los detalles para crear un lote, incluidas las solicitudes y respuestas de ejemplo, se encuentran en la [Resumen de ingesta por lotes](../ingestion/batch-ingestion/overview.md).

### Escribir en conjunto de datos

Después de crear correctamente un nuevo lote, los archivos se pueden cargar a un conjunto de datos específico. Se pueden publicar varios archivos en un lote hasta que se promocione. Los archivos se pueden cargar mediante la API de carga de archivos pequeños; sin embargo, si los archivos son demasiado grandes y se supera el límite de la puerta de enlace, puede utilizar la API de carga de archivos grandes. Para obtener más información sobre el uso de Carga de archivos grandes y pequeños, consulte la [Resumen de ingesta por lotes](../ingestion/batch-ingestion/overview.md).

**Solicitud**

Datos en [!DNL Experience Platform] debe escribirse en forma de archivos de Parquet.

```shell
curl -X PUT "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/dataSets/{DATASET_ID}/files/{FILE_NAME}.parquet" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id:{ORG_ID}" \
  -H "Authorization:Bearer ACCESS_TOKEN" \
  -H "x-api-key: API_KEY" \
  -H "content-type: application/octet-stream" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

### Marcar carga por lotes como completada

Una vez cargados todos los archivos en el lote, se puede marcar el lote para su finalización. Al hacer esto, la variable [!DNL Catalog] Las entradas &quot;DataSetFile&quot; se crean para los archivos completados y asociados con el lote generado. El [!DNL Catalog] A continuación, el lote se marca como correcto, que déclencheur los flujos descendentes para introducir los datos disponibles.

Los datos aterrizarán primero en la ubicación de ensayo en Adobe Experience Platform y, a continuación, se moverán a la ubicación final después de la catalogación y validación. Los lotes se marcarán como correctos una vez que todos los datos se muevan a una ubicación permanente.

**Solicitud**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

Si se realiza correctamente, la respuesta devolverá el estado HTTP 200 OK y el cuerpo de la respuesta estará vacío.

La herramienta ETL se asegurará de anotar la marca de tiempo de los conjuntos de datos de origen a medida que se lean los datos.

En la siguiente ejecución de transformación, probablemente por programación o invocación de evento, el ETL empezará a solicitar los datos de la marca de tiempo guardada anteriormente y todos los datos a partir de ahora.

### Obtener el último estado del lote

Antes de ejecutar nuevas tareas en la herramienta ETL, debe asegurarse de que el último lote se haya completado correctamente. El [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) proporciona una opción específica del lote que proporciona los detalles de los lotes relevantes.

**Solicitud**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?limit=1&sort=desc:created" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Respuesta**

Se pueden programar nuevas tareas si el valor del &quot;estado&quot; del lote anterior es &quot;correcto&quot;, como se muestra a continuación:

```json
"{BATCH_ID}": {
    "imsOrg": "{ORG_ID}",
    "created": 1494349962314,
    "createdClient": "{API_KEY}",
    "createdUser": "CLIENT_USER_ID@AdobeID",
    "updatedUser": "CLIENT_USER_ID@AdobeID",
    "updated": 1494349963467,
    "status": "success",
    "errors": [],
    "version": "1.0.1",
    "availableDates": {}
}
```

### Obtener el último estado del lote por identificador

Se puede recuperar un estado de lote individual a través del [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) al emitir una solicitud de GET utilizando `{BATCH_ID}`. El `{BATCH_ID}` utilizado sería el mismo que el ID devuelto cuando se creó el lote.

**Solicitud**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID}" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Respuesta: correcta**

La siguiente respuesta muestra un &quot;éxito&quot;:

```json
"{BATCH_ID}": {
    "imsOrg": "{ORG_ID}",
    "created": 1494349962314,
    "createdClient": "{API_KEY}",
    "createdUser": "{CREATED_USER}",
    "updatedUser": "{UPDATED_USER}",
    "updated": 1494349962314,
    "status": "success",
    "errors": [],
    "version": "1.0.1",
    "availableDates": {}
}
```

**Respuesta: error**

En caso de error, los &quot;errores&quot; se pueden extraer de la respuesta y mostrarse en la herramienta ETL como mensajes de error.

```json
"{BATCH_ID}": {
    "imsOrg": "{ORG_ID}",
    "created": 1494349962314,
    "createdClient": "{API_KEY}",
    "createdUser": "{CREATED_USER}",
    "updatedUser": "{UPDATED_USER}",
    "updated": 1494349962314,
    "status": "failure",
    "errors": [
        {
            "code": "200",
            "description": "Error in validating schema for file: 'adl://dataLake.azuredatalakestore.net/connectors-dev/stage/BATCHID/dataSetId/contact.csv' with errorMessage=adl://dataLake.azuredatalakestore.net/connectors-dev/stage/BATCHID/dataSetId/contact.csv is not a Parquet file. expected magic number at tail [80, 65, 82, 49] but found [57, 98, 55, 10] and errorType=java.lang.RuntimeException",
            "rows": []
        }
    ],
    "version": "1.0.1",
    "availableDates": {}
}
```

## Datos y eventos incrementales o de instantánea frente a perfiles

Los datos se pueden representar en una matriz de dos por dos de la siguiente manera:

| Eventos incrementales | Perfiles incrementales |
|-------------------------------|----------------------|
| Eventos de instantánea (menos probable) | Perfiles de instantánea |

Los datos de evento suelen almacenarse cuando hay columnas de marca de tiempo indizadas en cada fila.

Los datos de perfil se utilizan normalmente cuando no hay una marca de tiempo en los datos y cada fila se puede identificar mediante una clave principal/compuesta.

En los datos incrementales es donde solo entran en el sistema los datos nuevos o actualizados y se anexan a los datos actuales en los conjuntos de datos.

Los datos de instantánea se obtienen cuando todos los datos llegan al sistema y reemplazan algunos o todos los datos anteriores de un conjunto de datos.

En el caso de eventos incrementales, la herramienta ETL debe utilizar las fechas disponibles o la fecha de creación de la entidad por lotes. En caso de servicio push, las fechas disponibles no estarán presentes, por lo que la herramienta utilizará la fecha de creación/actualización por lotes para marcar los incrementos. Es necesario procesar cada lote de eventos incrementales.

Para perfiles incrementales, la herramienta ETL utilizará las fechas creadas o actualizadas de la entidad de lote. Normalmente, es necesario procesar cada lote de datos de perfil incrementales.

Los eventos de instantáneas son muy poco probables debido al mero tamaño de los datos. Pero si esto fuera necesario, la herramienta ETL debe elegir solo el último lote para procesar.

Cuando se utilizan perfiles de instantánea, la herramienta ETL tendrá que elegir el último lote de los datos que llegaron al sistema. Pero si es necesario realizar un seguimiento de las versiones de los cambios, se requerirá que se procesen todos los lotes. El procesamiento de deduplicación dentro del proceso de ETL ayudará a controlar los costes de almacenamiento.

## Reproducción por lotes y reprocesamiento de datos

La reproducción por lotes y el reprocesamiento de datos pueden ser necesarios en casos en los que un cliente descubra que, durante los últimos &quot;n&quot; días, los datos que se están procesando ETL no se han producido como se esperaba o que los datos de origen en sí mismos pueden no haber sido correctos.

Para ello, los administradores de datos del cliente utilizarán el [!DNL Platform] IU para eliminar los lotes que contienen datos dañados. A continuación, es probable que se tenga que volver a ejecutar el ETL, rellenando así con los datos correctos. Si la fuente en sí tenía datos dañados, el ingeniero/administrador de datos deberá corregir los lotes de origen y volver a ingerir los datos (ya sea en Adobe Experience Platform o a través de conectores ETL).

En función del tipo de datos que se genere, será la elección del ingeniero de datos eliminar un solo lote o todos los lotes de determinados conjuntos de datos. Los datos se eliminarán o archivarán según lo establecido en [!DNL Experience Platform] directrices.

Es probable que la funcionalidad de ETL para purgar datos sea importante.

Una vez finalizada la depuración, los administradores del cliente deberán volver a configurar Adobe Experience Platform para reiniciar el procesamiento de los servicios principales desde el momento en que se eliminen los lotes.

## Procesamiento por lotes simultáneo

A criterio del cliente, los administradores/ingenieros de datos pueden decidir extraer, transformar y cargar datos de forma secuencial o simultánea según las características de un conjunto de datos determinado. Esto también se basará en el caso de uso al que se dirija el cliente con los datos transformados.

Por ejemplo, si el cliente persiste en un almacén de persistencia actualizable y la secuencia o el orden de los eventos es importante, es posible que tenga que procesar estrictamente los trabajos con transformaciones secuenciales de ETL.

En otros casos, los datos desordenados se pueden procesar mediante aplicaciones o procesos descendentes que ordenan internamente mediante una marca de tiempo especificada. En estos casos, las transformaciones paralelas de ETL pueden ser viables para mejorar los tiempos de procesamiento.

Para los lotes de origen, volverá a depender de las preferencias del cliente y las restricciones del consumidor. Si los datos de origen se pueden recoger en paralelo independientemente de la regencia/orden de una fila, el proceso de transformación puede crear lotes de proceso con un mayor grado de paralelismo (optimización basada en el procesamiento desordenado). Sin embargo, si la transformación debe respetar las marcas de tiempo o cambiar el orden de prioridad, el programador/invocación de la herramienta ETL o la API de acceso a datos deberá garantizar que los lotes no se procesen de forma desordenada siempre que sea posible.

## Aplazamiento

El aplazamiento es un proceso en el que los datos de entrada aún no están lo suficientemente completos para enviarse a procesos descendentes, pero que pueden utilizarse en el futuro. Los clientes determinarán su tolerancia individual con la limitación de datos para la confrontación futura en comparación con el coste de procesamiento para informar su decisión de dejar de lado los datos y volver a procesarlos en la siguiente ejecución de transformación, con la esperanza de que se puedan enriquecer, reconciliar o vincular en algún momento futuro dentro de la ventana de retención. Este ciclo está en curso hasta que la fila se procese lo suficiente o hasta que se considere demasiado antigua para seguir invirtiendo en. Cada iteración generará datos diferidos, que son un superconjunto de todos los datos diferidos de iteraciones anteriores.

Adobe Experience Platform no identifica datos diferidos actualmente, por lo que las implementaciones de cliente deben basarse en las configuraciones manuales de ETL y Conjunto de datos para crear otro conjunto de datos en [!DNL Platform] crear una copia simétrica del conjunto de datos de origen que se puede utilizar para mantener datos diferidos. En este caso, los datos diferidos serán similares a los datos de instantánea. En cada ejecución de la transformación de ETL, los datos de origen se unen con los datos diferidos y se envían para su procesamiento.

## Changelog

| Fecha | Acción | Descripción |
| ---- | ------ | ----------- |
| 2019-01-19 | Se ha eliminado la propiedad &quot;fields&quot; de los conjuntos de datos | Anteriormente, los conjuntos de datos incluían una propiedad &quot;fields&quot; que contenía una copia del esquema. Esta capacidad ya no debe utilizarse. Si se encuentra la propiedad &quot;fields&quot;, debe ignorarse y se debe utilizar &quot;observedSchema&quot; o &quot;schemaRef&quot; en su lugar. |
| 2019-03-15 | Propiedad &quot;schemaRef&quot; agregada a conjuntos de datos | La propiedad &quot;schemaRef&quot; de un conjunto de datos contiene un URI que hace referencia al esquema XDM en el que se basa el conjunto de datos y representa todos los campos potenciales que el conjunto de datos podría utilizar. |
| 2019-03-15 | Todos los identificadores de usuario final se asignan a la propiedad identityMap | El &quot;identityMap&quot; es una encapsulación de todos los identificadores únicos de un asunto, como ID de CRM, ECID o ID del programa de fidelidad. Este mapa lo utiliza [[!DNL Identity Service]](../identity-service/home.md) para resolver todas las identidades conocidas y anónimas de un sujeto, formando un único gráfico de identidades para cada usuario final. |
| 2019-05-30 | EOL y Quitar la propiedad &quot;schema&quot; de los conjuntos de datos | La propiedad &quot;schema&quot; del conjunto de datos proporcionó un vínculo de referencia al esquema con el obsoleto `/xdms` punto final en la [!DNL Catalog] API. Esto se ha sustituido por un &quot;schemaRef&quot; que proporciona el &quot;id&quot;, la &quot;versión&quot; y el &quot;contentType&quot; del esquema como se hace referencia en el nuevo [!DNL Schema Registry] API. |
