---
keywords: Experience Platform;inicio;temas populares;ETL;etl;integraciones de etl;integraciones de ETL
solution: Experience Platform
title: Desarrollo de integraciones de ETL para Adobe Experience Platform
description: La guía de integración de ETL describe los pasos generales para crear conectores seguros y de alto rendimiento para el Experience Platform y la ingesta de datos en Platform.
exl-id: 7d29b61c-a061-46f8-a31f-f20e4d725655
source-git-commit: 76ef5638316a89aee1c6fb33370af943228b75e1
workflow-type: tm+mt
source-wordcount: '4081'
ht-degree: 1%

---

# Desarrollo de integraciones de ETL para Adobe Experience Platform

La guía de integración de ETL describe los pasos generales para crear conectores seguros y de alto rendimiento para [!DNL Experience Platform] e ingesta de datos en [!DNL Platform].


- [[!DNL Catalog]](https://www.adobe.io/experience-platform-apis/references/catalog/)
- [[!DNL Data Access]](https://www.adobe.io/experience-platform-apis/references/data-access/)
- [[!DNL Batch Ingestion]](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/)
- [[!DNL Streaming Ingestion]](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/)
- [Autenticación y autorización para API de Experience Platform](https://www.adobe.com/go/platform-api-authentication-en)
- [[!DNL Schema Registry]](https://www.adobe.io/experience-platform-apis/references/schema-registry/)

Esta guía también incluye ejemplos de llamadas a la API para utilizar al diseñar un conector de ETL, con vínculos a documentación que describe cada [!DNL Experience Platform] y uso de su API, en más detalle.

Una integración de muestra está disponible en [!DNL GitHub] a través de la variable [Código de referencia de la integración del ecosistema ETL](https://github.com/adobe/acp-data-services-etl-reference) en el [!DNL Apache] Versión de licencia 2.0.

## Flujo de trabajo

El siguiente diagrama de flujo de trabajo proporciona una descripción general de alto nivel para la integración de componentes de Adobe Experience Platform con una aplicación y un conector de ETL.

![](images/etl.png)

## Componentes de Adobe Experience Platform

Hay varios componentes de Experience Platform involucrados en las integraciones de conectores de ETL. La siguiente lista describe varios componentes y funcionalidades clave:

- **Sistema Identity Management de Adobe (IMS)** : proporciona un marco para la autenticación en los servicios de Adobe.
- **Organización IMS** - Una entidad corporativa que puede poseer o licenciar productos y servicios y permitir el acceso a sus miembros.
- **Usuario IMS** - Miembros de una organización IMS. La relación entre Organización y Usuario es de varios a muchos.
- **[!DNL Sandbox]** - Una partición virtual [!DNL Platform] por ejemplo, para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.
- **Detección de datos** - Registra los metadatos de datos introducidos y transformados en [!DNL Experience Platform].
- **[!DNL Data Access]** : proporciona a los usuarios una interfaz para acceder a sus datos en [!DNL Experience Platform].
- **[!DNL Data Ingestion]** - Inserta datos en [!DNL Experience Platform] con [!DNL Data Ingestion] API.
- **[!DNL Schema Registry]** - Define y almacena un esquema que describe la estructura de datos a utilizar en [!DNL Experience Platform].

## Introducción a [!DNL Experience Platform] API

Las secciones siguientes proporcionan información adicional que debe conocer o tener disponible para realizar llamadas a [!DNL Experience Platform] API.

### Leer llamadas de API de ejemplo

Esta guía proporciona ejemplos de llamadas a la API para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../landing/troubleshooting.md#how-do-i-format-an-api-request) en el [!DNL Experience Platform] guía de solución de problemas.

### Recopilar valores para encabezados necesarios

Para realizar llamadas a [!DNL Platform] API, primero debe completar la variable [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todos los [!DNL Experience Platform] Llamadas de API, como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Todos los recursos de [!DNL Experience Platform] están aisladas para entornos limitados virtuales específicos. Todas las solicitudes a [!DNL Platform] Las API requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados en [!DNL Platform], consulte la [documentación general de entorno limitado](../sandboxes/home.md).

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

- Content-Type: application/json

## Flujo de usuario general

Para empezar, un usuario de ETL inicia sesión en el [!DNL Experience Platform] interfaz de usuario (IU) y crea conjuntos de datos para la ingesta mediante un conector estándar o un conector de servicio push.

En la interfaz de usuario, el usuario crea el conjunto de datos de salida seleccionando un esquema de conjunto de datos. La elección del esquema depende del tipo de datos (registro o serie temporal) que se incorporen en [!DNL Platform]. Al hacer clic en la pestaña Esquemas de la interfaz de usuario, el usuario podrá ver todos los esquemas disponibles, incluido el tipo de comportamiento que admite el esquema.

En la herramienta ETL, el usuario empezará a diseñar sus transformaciones de asignación después de configurar la conexión adecuada (con sus credenciales). Se supone que la herramienta ETL ya tiene [!DNL Experience Platform] conectores instalados (proceso no definido en esta Guía de integración).

Se han proporcionado en la sección [Flujo de trabajo de ETL](./workflow.md). Aunque las herramientas de ETL pueden tener un formato diferente, la mayoría exponen funcionalidades similares.

>[!NOTE]
>
>El conector ETL debe especificar un filtro de marca de hora que marque la fecha de entrada de datos y desplazamiento (es decir, la ventana para la que se deben leer los datos). La herramienta ETL debe admitir la toma de estos dos parámetros en esta u otra interfaz de usuario relevante. En Adobe Experience Platform, estos parámetros se asignarán a fechas disponibles (si están presentes) o a fechas capturadas presentes en el objeto por lotes del conjunto de datos.

### Ver lista de conjuntos de datos

Si se utiliza el origen de los datos para la asignación, se puede obtener una lista de todos los conjuntos de datos disponibles mediante la variable [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/).

Puede enviar una única solicitud de API para ver todos los conjuntos de datos disponibles (p. ej. `GET /dataSets`), siendo recomendable incluir parámetros de consulta que limiten el tamaño de la respuesta.

En los casos en los que se solicita información completa del conjunto de datos, la carga útil de respuesta puede superar los 3 GB de tamaño, lo que puede ralentizar el rendimiento general. Por lo tanto, el uso de parámetros de consulta para filtrar solo la información necesaria hará que [!DNL Catalog] consulta más eficaz.

#### Filtrado de listas

Al filtrar respuestas, puede utilizar varios filtros en una sola llamada separando parámetros con un signo &amp; (`&`). Algunos parámetros de consulta aceptan listas de valores separados por comas, como el filtro &quot;propiedades&quot; en la solicitud de ejemplo siguiente.

[!DNL Catalog] las respuestas se miden automáticamente según los límites configurados, sin embargo, el parámetro de consulta &quot;limit&quot; puede utilizarse para personalizar las restricciones y limitar el número de objetos devueltos. El [!DNL Catalog] los límites de respuesta son:

- Si no se especifica un parámetro de límite, el número máximo de objetos por carga útil de respuesta es de 20.
- El límite global para el resto [!DNL Catalog] las consultas son 100 objetos.
- Para consultas de conjuntos de datos, si observableSchema se solicita utilizando el parámetro de consulta de propiedades, el número máximo de conjuntos de datos devueltos es 20.
- Parámetros de límite no válidos (incluidos `limit=0`) se encuentran con un error HTTP 400 que describe los intervalos adecuados.
- Si los límites o desplazamientos se pasan como parámetros de consulta, tienen prioridad sobre los que se pasan como encabezados.

Los parámetros de consulta se tratan con más detalle en la sección [Información general del servicio de catálogo](../catalog/home.md).

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

Consulte la [Información general del servicio de catálogo](../catalog/home.md) para ver ejemplos detallados de cómo realizar llamadas a la variable [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/).

**Respuesta**

La respuesta incluye tres (`limit=3`) conjuntos de datos que muestran &quot;name&quot;, &quot;description&quot; y &quot;schemaRef&quot; como se indica en la `properties` parámetro de consulta.

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

La propiedad &quot;schemaRef&quot; de un conjunto de datos contiene una URI que hace referencia al esquema XDM en el que se basa el conjunto de datos. El esquema XDM (&quot;schemaRef&quot;) representa todos los campos potenciales que podría utilizar el conjunto de datos, no necesariamente los campos que se están utilizando (consulte &quot;observableSchema&quot; más adelante).

El esquema XDM es el esquema que se utiliza cuando se necesita presentar al usuario una lista de todos los campos disponibles en los que se puede escribir.

El primer valor &quot;schemaRef.id&quot; en el objeto de respuesta anterior (`https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18`) es un URI que señala a un esquema XDM específico en la variable [!DNL Schema Registry]. El esquema se puede recuperar realizando una solicitud de búsqueda (GET) al [!DNL Schema Registry] API.

>[!NOTE]
>
>La propiedad &quot;schemaRef&quot; reemplaza la propiedad ahora obsoleta &quot;schema&quot; . Si &quot;schemaRef&quot; está ausente del conjunto de datos o no contiene un valor, deberá comprobar la presencia de una propiedad &quot;schema&quot;. Esto se puede hacer reemplazando &quot;schemaRef&quot; por &quot;schema&quot; en la variable `properties` parámetro de consulta en la llamada anterior. Encontrará más información sobre la propiedad &quot;schema&quot; en la [Propiedad &quot;schema&quot; del conjunto de datos](#dataset-schema-property-deprecated---eol-2019-05-30) que sigue.

**Formato de API**

```http
GET /schemaregistry/tenant/schemas/{url encoded schemaRef.id}
```

**Solicitud**

La solicitud utiliza la dirección URL codificada `id` URI del esquema (el valor del atributo &quot;schemaRef.id&quot;) y requiere un encabezado Accept .

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F274f17bc5807ff307a046bab1489fb18 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
```

El formato de respuesta depende del tipo de encabezado Accept enviado en la solicitud. Las solicitudes de búsqueda también requieren un `version` se incluya en el encabezado Accept . La siguiente tabla describe los encabezados Accept disponibles para las búsquedas:

| Accept | Descripción |
| ------ | ----------- |
| `application/vnd.adobe.xed-id+json` | Enumerar solicitudes, títulos, id y versiones (GET) |
| `application/vnd.adobe.xed-full+json; version={major version}` | $refs y allOf resueltos, tiene títulos y descripciones |
| `application/vnd.adobe.xed+json; version={major version}` | Sin procesar con $ref y allOf, tiene títulos y descripciones |
| `application/vnd.adobe.xed-notext+json; version={major version}` | Sin procesar con $ref y todoOf, sin títulos ni descripciones |
| `application/vnd.adobe.xed-full-notext+json; version={major version}` | $refs y allOf resueltos, sin títulos ni descripciones |
| `application/vnd.adobe.xed-full-desc+json; version={major version}` | $refs y allOf resueltos, se incluyen los descriptores |

>[!NOTE]
>
>`application/vnd.adobe.xed-id+json` y `application/vnd.adobe.xed-full+json; version={major version}` son los encabezados Accept más utilizados. `application/vnd.adobe.xed-id+json` es preferible para listar recursos en la variable [!DNL Schema Registry] ya que solo devuelve &quot;title&quot;, &quot;id&quot; y &quot;version&quot;. `application/vnd.adobe.xed-full+json; version={major version}` es preferible para ver un recurso específico (por su &quot;id&quot;), ya que devuelve todos los campos (anidados en &quot;propiedades&quot;), así como los títulos y las descripciones.

**Respuesta**

El esquema JSON que se devuelve describe la información de nivel de estructura y campo (&quot;type&quot;, &quot;format&quot;, &quot;Minimum&quot;, &quot;maximum&quot;, etc.) de los datos, serializados como JSON. Si se utiliza un formato de serialización distinto de JSON para la ingesta (como Parquet o Scala), la variable [Guía del Registro de Esquemas](../xdm/tutorials/create-schema-api.md) contiene una tabla que muestra el tipo JSON deseado (&quot;meta:xdmType&quot;) y su representación correspondiente en otros formatos.

Junto con esta tabla, la variable [!DNL Schema Registry] La guía para desarrolladores contiene ejemplos detallados de todas las posibles llamadas que se pueden realizar mediante el [!DNL Schema Registry] API.

### Propiedad &quot;schema&quot; del conjunto de datos (OBSOLETO - EOL 2019-05-30)

Los conjuntos de datos pueden contener una propiedad &quot;schema&quot; que ahora está obsoleta y permanece disponible temporalmente para la compatibilidad con versiones anteriores. Por ejemplo, una solicitud de lista (GET) similar a la realizada anteriormente, donde &quot;schema&quot; se sustituyó por &quot;schemaRef&quot; en la variable `properties` , puede devolver lo siguiente:

```json
{
  "5ba9452f7de80400007fc52a": {
    "name": "Sample Dataset 1",
    "description": "Description of Sample Dataset 1.",
    "schema": "@/xdms/context/person"
  }
}
```

Si la propiedad &quot;schema&quot; de un conjunto de datos se rellena, esto indica que el esquema está en desuso `/xdms` y, cuando se admita, el conector ETL debe utilizar el valor de la propiedad &quot;schema&quot; con la variable `/xdms` punto final (un punto final obsoleto en la variable [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/)) para recuperar el esquema heredado.

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
>Un parámetro de consulta opcional, `expansion=xdm`, indica a la API que amplíe y en línea todos los esquemas a los que se hace referencia. Puede que desee hacerlo al presentar una lista de todos los campos posibles al usuario.

**Respuesta**

Similar a los pasos para [visualización del esquema del conjunto de datos](#view-dataset-schema), la respuesta contiene un esquema JSON que describe la estructura y la información a nivel de campo de los datos, serializados como JSON.

>[!NOTE]
>
>Cuando el campo &quot;schema&quot; está vacío o ausente por completo, el conector debe leer el campo &quot;schemaRef&quot; y utilizar la variable [API del Registro de esquemas](https://www.adobe.io/experience-platform-apis/references/schema-registry/) como se muestra en los pasos anteriores a [ver un esquema de conjunto de datos](#view-dataset-schema).

### La propiedad &quot;observableSchema&quot;

La propiedad &quot;observableSchema&quot; de un conjunto de datos tiene una estructura JSON que coincide con la del esquema XDM JSON. El &quot;observableSchema&quot; contiene los campos que estaban presentes en los archivos de entrada entrantes. Al escribir datos en [!DNL Experience Platform], no es necesario que un usuario utilice cada campo del esquema de destino. En su lugar, solo deben proporcionar los campos que se están utilizando.

El esquema observable es el esquema que se utiliza si se leen los datos o se presenta una lista de campos disponibles para leer o asignar.

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

La aplicación ETL puede proporcionar la capacidad de obtener una vista previa de los datos ([&quot;Figura 8&quot; en el flujo de trabajo de ETL](./workflow.md)). La API de acceso a datos ofrece varias opciones para obtener una vista previa de los datos.

Puede encontrar información adicional, incluidas instrucciones paso a paso para previsualizar datos mediante la API de acceso a datos, en la [tutorial de acceso a datos](../data-access/tutorials/dataset-data.md).

### Obtener detalles del conjunto de datos mediante el parámetro de consulta &quot;propiedades&quot;

Como se muestra en los pasos anteriores a [ver una lista de conjuntos de datos](#view-list-of-datasets), puede solicitar &quot;archivos&quot; utilizando el parámetro de consulta &quot;propiedades&quot;.

Puede consultar la [Información general del servicio de catálogo](../catalog/home.md) para obtener información detallada sobre la consulta de conjuntos de datos y filtros de respuesta disponibles.

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

La respuesta incluirá un conjunto de datos (`limit=1`) que muestra la propiedad &quot;files&quot;.

```json
{
  "5bf479a6a8c862000050e3c7": {
    "files": "@/dataSets/5bf479a6a8c862000050e3c7/views/5bf479a654f52014cfffe7f1/files"
  }
}
```

### Enumerar archivos de conjuntos de datos utilizando el atributo &quot;files&quot;

También puede utilizar una solicitud de GET para obtener detalles del archivo mediante el atributo &quot;files&quot;.

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

La respuesta incluye el ID del archivo del conjunto de datos como propiedad de nivel superior, con detalles del archivo incluidos en el objeto ID del archivo del conjunto de datos.

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

### Obtener detalles del archivo

Los ID de archivo del conjunto de datos devueltos en la respuesta anterior se pueden usar en una solicitud de GET para obtener más detalles del archivo a través del [!DNL Data Access] API.

La variable [información general sobre el acceso a los datos](../data-access/home.md) contiene detalles sobre cómo usar la variable [!DNL Data Access] API.

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

### Vista previa de datos de archivos

La propiedad &quot;href&quot; se puede usar para recuperar datos de vista previa a través del [[!DNL Data Access API]](../data-access/home.md).

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

La respuesta a la solicitud anterior contiene una vista previa del contenido del archivo.

Más información sobre [!DNL Data Access] La API, incluidas las solicitudes y respuestas detalladas, está disponible en la [información general sobre el acceso a los datos](../data-access/home.md).

### Obtener &quot;fileDescription&quot; del conjunto de datos

El componente de destino como salida de datos transformados, el ingeniero de datos elegirá un conjunto de datos de salida ([&quot;Figura 12&quot; en el flujo de trabajo de ETL](workflow.md)). El esquema XDM está asociado con el conjunto de datos de salida. Los datos que se escribirán se identificarán mediante el atributo &quot;fileDescription&quot; de la entidad del conjunto de datos de las API de detección de datos. Esta información se puede obtener mediante un ID de conjunto de datos (`{DATASET_ID}`). La propiedad &quot;fileDescription&quot; en la respuesta JSON proporcionará la información solicitada.

**Formato de API**

```shell
GET /catalog/dataSets/{DATASET_ID}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{DATASET_ID}` | La variable `id` del conjunto de datos al que está intentando acceder. |

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

Los datos se escribirán en [!DNL Experience Platform] usando la variable [API de ingesta de lotes](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/).  La escritura de datos es un proceso asincrónico. Cuando los datos se escriben en Adobe Experience Platform, un lote se crea y marca como un éxito solo después de que los datos se hayan escrito completamente.

Entrada de datos [!DNL Experience Platform] debe escribirse en forma de archivos de parquet.

## Fase de ejecución

A medida que comienza la ejecución, el conector (como se define en el componente de origen) lee los datos de [!DNL Experience Platform] usando la variable [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/). El proceso de transformación leerá los datos durante un intervalo de tiempo determinado. Internamente, consulta lotes de conjuntos de datos de origen. Durante la consulta, se utilizará un archivo parametrizado (móvil para datos de series temporales o datos incrementales) de fecha de inicio y de lista de archivos de conjuntos de datos para esos lotes, y se empezará a realizar solicitudes de datos para esos archivos de conjuntos de datos.

### Transformaciones de ejemplo

La variable [transformaciones de ETL de muestra](./transformations.md) documento contiene varias transformaciones de ejemplo, como el manejo de identidades y las asignaciones de tipo de datos. Utilice estas transformaciones como referencia.

### Leer datos de [!DNL Experience Platform]

Al usar la variable [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/), puede recuperar todos los lotes entre una hora de inicio y de finalización especificadas y ordenarlos según el orden en que se crearon.

**Solicitud**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?dataSet=DATASETID&createdAfter=START_TIMESTAMP&createdBefore=END_TIMESTAMP&sort=desc:created" \
  -H "Accept: application/json" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

Los detalles sobre los lotes de filtrado se encuentran en la [Tutorial de acceso a datos](../data-access/tutorials/dataset-data.md).

### Obtención de archivos de un lote

Una vez que tenga el ID del lote que está buscando (`{BATCH_ID}`), es posible recuperar una lista de archivos pertenecientes a un lote específico mediante el [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/).  Los detalles para ello están disponibles en la sección [[!DNL Data Access] tutorial](../data-access/tutorials/dataset-data.md).

**Solicitud**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/files" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

### Acceso a archivos mediante el ID de archivo

Uso del ID exclusivo de un archivo (`{FILE_ID`), el [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) se puede utilizar para acceder a los detalles específicos del archivo, incluido su nombre, tamaño en bytes y un vínculo para descargarlo.

**Solicitud**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{FILE_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

La respuesta puede apuntar a un solo archivo o a un directorio. Los detalles de cada uno se encuentran en la [[!DNL Data Access] tutorial](../data-access/tutorials/dataset-data.md).

### Acceso al contenido del archivo

La variable [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) para acceder al contenido de un archivo específico. Para recuperar el contenido, se realiza una solicitud de GET con el valor devuelto por `_links.self.href` al acceder a un archivo mediante el ID de archivo.

**Solicitud**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{DATASET_FILE_ID}?path=filename1.csv" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

La respuesta a esta solicitud contiene el contenido del archivo . Para obtener más información, incluidos los detalles sobre la paginación de respuestas, consulte la [Cómo consultar datos mediante la API de acceso a datos](../data-access/tutorials/dataset-data.md) tutorial.

### Validación de registros para la conformidad con esquemas

Cuando se escriben los datos, los usuarios pueden optar por validarlos de acuerdo con las reglas de validación definidas en el esquema XDM. Puede encontrar más información sobre la validación de esquemas en la [Código de referencia de integración de ecosistema de ETL en [!DNL GitHub]](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md#validation).

Si utiliza la implementación de referencia que se encuentra en [[!DNL GitHub]](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md), puede activar la validación de esquema en esta implementación mediante la propiedad system `-DenableSchemaValidation=true`.

La validación se puede realizar para tipos XDM lógicos, utilizando atributos como `minLength` y `maxlength` para cadenas, `minimum` y `maximum` para enteros, etc. La variable [Guía del desarrollador de API del Registro del Esquema](../xdm/api/getting-started.md) contiene una tabla que describe los tipos XDM y las propiedades que se pueden utilizar para la validación.

>[!NOTE]
>
>Los valores mínimo y máximo proporcionados para varios `integer` Los tipos son los valores MIN y MAX que el tipo puede admitir, pero estos valores se pueden restringir aún más a mínimos y máximos de su elección.

### Crear un lote

Una vez procesados los datos, la herramienta ETL vuelve a escribir los datos en [!DNL Experience Platform] usando la variable [API de ingesta de lotes](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/). Para poder agregar datos a un conjunto de datos, estos deben vincularse a un lote que luego se cargará en un conjunto de datos específico.

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

Los detalles para crear un lote, incluidas las solicitudes de muestra y las respuestas, se pueden encontrar en la [Información general sobre la ingesta de lotes](../ingestion/batch-ingestion/overview.md).

### Escribir en el conjunto de datos

Después de crear correctamente un nuevo lote, los archivos se pueden cargar en un conjunto de datos específico. Se pueden publicar varios archivos en un lote hasta que se promocione. Los archivos se pueden cargar mediante la API de carga de archivo pequeño; sin embargo, si los archivos son demasiado grandes y se supera el límite de la puerta de enlace, puede utilizar la API de carga de archivos grandes. Puede encontrar los detalles para utilizar la carga de archivos grande y pequeña en el [Información general sobre la ingesta de lotes](../ingestion/batch-ingestion/overview.md).

**Solicitud**

Entrada de datos [!DNL Experience Platform] debe escribirse en forma de archivos de parquet.

```shell
curl -X PUT "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/dataSets/{DATASET_ID}/files/{FILE_NAME}.parquet" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id:{ORG_ID}" \
  -H "Authorization:Bearer ACCESS_TOKEN" \
  -H "x-api-key: API_KEY" \
  -H "content-type: application/octet-stream" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

### Marcar la carga por lotes como completada

Una vez cargados todos los archivos en el lote, se puede indicar que el lote ha finalizado. Al hacer esto, la variable [!DNL Catalog] Las entradas &quot;DataSetFile&quot; se crean para los archivos completados y se asocian al lote generado. La variable [!DNL Catalog] a continuación, se marca como correcto, lo que déclencheur los flujos descendentes a la ingesta de los datos disponibles.

Los datos se dirigen primero a la ubicación de ensayo de Adobe Experience Platform y, después, se mueven a la ubicación final después de la catalogación y validación. Los lotes se marcarán como correctos una vez que todos los datos se hayan movido a una ubicación permanente.

**Solicitud**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

Si se realiza correctamente, la respuesta devolverá el estado HTTP 200 OK y el cuerpo de respuesta estará vacío.

La herramienta ETL se asegurará de anotar la marca de tiempo de los conjuntos de datos de origen a medida que se leen los datos.

En la siguiente ejecución de transformación, probablemente por programación o invocación de evento, ETL empezará a solicitar los datos de la marca de tiempo guardada anteriormente y todos los datos a partir de ahora.

### Obtener el estado del último lote

Antes de ejecutar nuevas tareas en la herramienta ETL, debe asegurarse de que el último lote se haya completado correctamente. La variable [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) proporciona una opción específica del lote que proporciona los detalles de los lotes relevantes.

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

Se pueden programar nuevas tareas si el valor anterior de &quot;estado&quot; del lote es &quot;éxito&quot;, como se muestra a continuación:

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

### Obtener el estado del último lote por ID

Se puede recuperar un estado de lote individual mediante la variable [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) al emitir una solicitud de GET utilizando `{BATCH_ID}`. La variable `{BATCH_ID}` se utilizaría igual que el ID devuelto cuando se creó el lote.

**Solicitud**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID}" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Respuesta: Correcto**

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

**Respuesta: Fallo**

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

## Eventos y datos incrementales frente a instantáneas frente a perfiles

Los datos se pueden representar en una matriz de dos por dos de la siguiente manera:

| Eventos incrementales | Perfiles incrementales |
|-------------------------------|----------------------|
| Eventos de instantánea (menos probable) | Perfiles de instantánea |

Los datos de evento suelen aparecer cuando hay columnas de marca de hora indexadas en cada fila.

Los datos de perfil suelen aparecer cuando no hay una marca de hora en los datos y cada fila se puede identificar con una clave principal/compuesta.

Los datos incrementales son aquellos en los que solo los datos nuevos o actualizados llegan al sistema y se anexan a los datos actuales en los conjuntos de datos.

Los datos de instantánea se producen cuando todos los datos entran en el sistema y sustituyen algunos o todos los datos anteriores de un conjunto de datos.

En el caso de eventos incrementales, la herramienta ETL debe utilizar las fechas disponibles/crear fecha de la entidad del lote. En caso de servicio push, las fechas disponibles no estarán presentes, por lo que la herramienta utilizará la fecha creada o actualizada por lotes para marcar los incrementos. Es necesario procesar cada lote de eventos incrementales.

Para perfiles incrementales, la herramienta ETL utilizará fechas creadas o actualizadas de la entidad por lotes. Normalmente, se requiere procesar cada lote de datos de perfil incrementales.

Los eventos de instantáneas son muy menos probables debido al tamaño de los datos. Pero si esto fuera necesario, la herramienta ETL debe seleccionar solo el último lote para el procesamiento.

Cuando se utilizan perfiles de instantánea, la herramienta ETL tendrá que elegir el último lote de datos que llegaron al sistema. Sin embargo, si el requisito es realizar un seguimiento de las versiones de los cambios, es necesario procesar todos los lotes. El procesamiento de deduplicación dentro del proceso de ETL ayudará a controlar los costos de almacenamiento.

## Reproducción por lotes y reprocesamiento de datos

Es posible que se requiera la reproducción por lotes y el reprocesamiento de datos en los casos en que un cliente descubra que durante los últimos &quot;n&quot; días, los datos que se están procesando con ETL no se han producido del modo esperado o puede que los datos de origen en sí no hayan sido correctos.

Para ello, los administradores de datos del cliente utilizarán la variable [!DNL Platform] IU para eliminar los lotes que contienen datos dañados. Entonces, es probable que se deba volver a ejecutar el ETL, lo que se rerellenará con los datos correctos. Si la fuente en sí tenía datos dañados, el ingeniero/administrador de datos deberá corregir los lotes de origen y volver a introducir los datos (ya sea en Adobe Experience Platform o a través de conectores ETL).

En función del tipo de datos que se generen, la elección del ingeniero de datos será eliminar un único lote o todos los lotes de ciertos conjuntos de datos. Los datos se eliminarán o archivarán según [!DNL Experience Platform] directrices.

Es probable que la funcionalidad de ETL para depurar datos sea importante.

Una vez finalizada la depuración, los administradores del cliente deberán reconfigurar Adobe Experience Platform para reiniciar el procesamiento de los servicios principales desde el momento en que se eliminen los lotes.

## Procesamiento por lotes simultáneo

A criterio del cliente, los administradores/ingenieros de datos pueden decidir extraer, transformar y cargar datos de manera secuencial o concurrente según las características de un conjunto de datos en particular. Esto también se basará en el caso de uso al que se dirige el cliente con los datos transformados.

Por ejemplo, si el cliente persiste en un almacén de persistencia actualizable y la secuencia o el orden de los eventos es importante, es posible que el cliente tenga que procesar estrictamente los trabajos con transformaciones de ETL secuenciales.

En otros casos, los datos desordenados se pueden procesar mediante aplicaciones o procesos descendentes que se ordenan internamente mediante una marca de tiempo especificada. En estos casos, las transformaciones de ETL paralelas pueden ser viables para mejorar los tiempos de procesamiento.

Para los lotes de origen, también dependerá de las preferencias del cliente y de la restricción del consumidor. Si los datos de origen se pueden recopilar en paralelo independientemente de la regencia o el orden de una fila, el proceso de transformación puede crear lotes de procesos con un mayor grado de paralelismo (optimización basada en el procesamiento por orden). Pero si la transformación tiene que cumplir con las marcas de tiempo o cambiar la orden de prioridad, la API de acceso a datos o el programador/invocación de herramientas de ETL tendrán que asegurarse de que los lotes no se procesen de forma desordenada siempre que sea posible.

## Aplazamiento

El aplazamiento es un proceso en el que los datos de entrada aún no están lo suficientemente completos para enviarse a procesos descendentes, pero pueden utilizarse en el futuro. Los clientes determinarán su tolerancia individual para la limitación de datos en caso de correspondencias futuras en comparación con el coste del procesamiento para informar su decisión de apartar datos y reprocesarlos en la siguiente ejecución de transformación, con la esperanza de que se puedan enriquecer y reconciliar/vincular en algún momento futuro dentro del período de retención. Este ciclo está en curso hasta que la fila se procese lo suficiente o se considere demasiado antigua para seguir invirtiendo en. Cada iteración genera datos diferidos, que son un superconjunto de todos los datos diferidos de iteraciones anteriores.

Adobe Experience Platform no identifica actualmente los datos diferidos, por lo que las implementaciones de cliente deben confiar en las configuraciones del manual ETL y Dataset para crear otro conjunto de datos en [!DNL Platform] reflejo del conjunto de datos de origen que se puede usar para mantener los datos diferidos. En este caso, los datos diferidos serán similares a los datos de instantáneas. En cada ejecución de la transformación ETL, los datos de origen se unen con los datos diferidos y se envían para su procesamiento.

## Cambio

| Fecha | Acción | Descripción |
| ---- | ------ | ----------- |
| 2019-01-19 | Se ha eliminado la propiedad &quot;fields&quot; de los conjuntos de datos | Anteriormente, los conjuntos de datos incluían una propiedad &quot;fields&quot; que contenía una copia del esquema. Esta capacidad ya no debe usarse. Si se encuentra la propiedad &quot;fields&quot;, se debe ignorar y usar en su lugar el &quot;observationSchema&quot; o &quot;schemaRef&quot;. |
| 2019-03-15 | Propiedad &quot;schemaRef&quot; agregada a conjuntos de datos | La propiedad &quot;schemaRef&quot; de un conjunto de datos contiene una URI que hace referencia al esquema XDM en el que se basa el conjunto de datos y representa todos los campos potenciales que podría utilizar el conjunto de datos. |
| 2019-03-15 | Todos los identificadores de usuario final se asignan a la propiedad &quot;identityMap&quot;. | &quot;identityMap&quot; es una encapsulación de todos los identificadores únicos de un asunto, como ID de CRM, ECID o ID de programa de fidelidad. Este mapa lo utiliza [[!DNL Identity Service]](../identity-service/home.md) para resolver todas las identidades conocidas y anónimas de un sujeto, formando un único gráfico de identidad para cada usuario final. |
| 2019-05-30 | EOL y Eliminar la propiedad &quot;schema&quot; de los conjuntos de datos | La propiedad &quot;schema&quot; del conjunto de datos proporcionó un vínculo de referencia al esquema mediante el desaprobada `/xdms` en la variable [!DNL Catalog] API. Esto se ha reemplazado por un &quot;schemaRef&quot; que proporciona el &quot;id&quot;, &quot;version&quot; y &quot;contentType&quot; del esquema como se hace referencia en el nuevo [!DNL Schema Registry] API. |
