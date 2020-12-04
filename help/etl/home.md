---
keywords: Experience Platform;home;popular topics;ETL;etl;etl integrations;ETL integrations
solution: Experience Platform
title: Creación de integraciones de ETL
topic: overview
description: La guía de integración de ETL describe los pasos generales para crear conectores seguros y de alto rendimiento para el Experience Platform y la ingesta de datos en la plataforma.
translation-type: tm+mt
source-git-commit: a362b67cec1e760687abb0c22dc8c46f47e766b7
workflow-type: tm+mt
source-wordcount: '4117'
ht-degree: 0%

---


# Desarrollo de integraciones de ETL para Adobe Experience Platform

La guía de integración de ETL describe los pasos generales para crear conectores seguros de alto rendimiento [!DNL Experience Platform] e incorporar datos en [!DNL Platform].


- [[!DNL Catalog]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)
- [[!DNL Data Access]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml)
- [[!DNL Data Ingestion]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)
- [API de autenticación y autorización](../tutorials/authentication.md)
- [[!DNL Schema Registry]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)

Esta guía también incluye ejemplos de llamadas a API que se utilizarán al diseñar un conector ETL, con vínculos a documentación que describe cada servicio y el uso de su API, con más detalle. [!DNL Experience Platform]

Se encuentra disponible una integración de muestra en [!DNL GitHub] el Código [de referencia de la integración de los ecosistemas de](https://github.com/adobe/acp-data-services-etl-reference) ETL en la versión 2.0 de la [!DNL Apache] licencia.

## Flujo de trabajo

El siguiente diagrama de flujo de trabajo proporciona información general de alto nivel para la integración de componentes de Adobe Experience Platform con una aplicación y un conector de ETL.

![](images/etl.png)

## Componentes de Adobe Experience Platform

Hay varios componentes de Experience Platform involucrados en integraciones de conector ETL. La siguiente lista describe varios componentes y funcionalidades clave:

- **Sistema Identity Management de Adobe (IMS)** : proporciona un marco para la autenticación en servicios de Adobe.
- **Organización** de IMS: entidad corporativa que puede poseer o licenciar productos y servicios y permitir el acceso a sus miembros.
- **Usuario** de IMS: Miembros de una organización de IMS. La relación entre la organización y el usuario es entre muchos.
- **[!DNL Sandbox]** - Una partición virtual de una sola [!DNL Platform] instancia, para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.
- **Detección** de datos: registra los metadatos de datos ingeridos y transformados en [!DNL Experience Platform].
- **[!DNL Data Access]** - Proporciona a los usuarios una interfaz para acceder a sus datos en [!DNL Experience Platform].
- **[!DNL Data Ingestion]** - Inserta datos en [!DNL Experience Platform] con [!DNL Data Ingestion] las API.
- **[!DNL Schema Registry]** - Define y almacena esquemas que describen la estructura de los datos que se utilizarán en [!DNL Experience Platform].

## Getting started with [!DNL Experience Platform] APIs

Las siguientes secciones proporcionan información adicional que deberá conocer o tener disponible para realizar llamadas a [!DNL Experience Platform] las API de forma satisfactoria.

### Leer llamadas de API de muestra

Esta guía proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas](../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de ejemplo en la guía de solución de problemas [!DNL Experience Platform] .

### Recopilar valores para encabezados necesarios

Para realizar llamadas a [!DNL Platform] API, primero debe completar el tutorial [de](../tutorials/authentication.md)autenticación. Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas [!DNL Experience Platform] de API, como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de [!DNL Experience Platform] están aislados en entornos limitados virtuales específicos. Todas las solicitudes a [!DNL Platform] las API requieren un encabezado que especifique el nombre del entorno limitado en el que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados de [!DNL Platform], consulte la documentación [general del](../sandboxes/home.md)entorno limitado.

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

- Content-Type: application/json

## Flujo de usuario general

Para empezar, un usuario de ETL inicia sesión en la interfaz de usuario (IU) y crea conjuntos de datos para la ingestión mediante un conector estándar o un conector de servicio push. [!DNL Experience Platform]

En la interfaz de usuario, el usuario crea el conjunto de datos de salida seleccionando un esquema de conjunto de datos. La elección del esquema depende del tipo de datos (registro o serie temporal) en los que se ingesta [!DNL Platform]. Al hacer clic en la ficha Esquemas de la interfaz de usuario, el usuario podrá realizar la vista de todos los esquemas disponibles, incluido el tipo de comportamiento que admite el esquema.

En la herramienta ETL, el usuario tendrá el inicio de diseñar las transformaciones de asignación después de configurar la conexión adecuada (mediante sus credenciales). Se supone que la herramienta ETL ya tiene [!DNL Experience Platform] conectores instalados (proceso no definido en esta Guía de integración).

En el flujo de trabajo de [ETL se han proporcionado maquetas para una herramienta de ETL de muestra y un flujo de trabajo](./workflow.md). Aunque las herramientas de ETL pueden tener un formato diferente, la mayoría de ellas exponen una funcionalidad similar.

>[!NOTE]
>
>El conector ETL debe especificar un filtro de marca de hora que marque la fecha de ingesta de datos y desplazamiento (es decir, la ventana para la que se deben leer los datos). La herramienta ETL debe admitir la utilización de estos dos parámetros en esta u otra IU relevante. En Adobe Experience Platform, estos parámetros se asignarán a fechas disponibles (si están presentes) o a fechas capturadas presentes en el objeto por lotes del conjunto de datos.

### Lista de vista de conjuntos de datos

Al utilizar la fuente de datos para la asignación, se puede recuperar una lista de todos los conjuntos de datos disponibles mediante el [[!DNL Catalog API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml).

Puede emitir una sola solicitud de API para la vista de todos los conjuntos de datos disponibles (p. ej. `GET /dataSets`), con lo que se recomienda incluir parámetros de consulta que limiten el tamaño de la respuesta.

En los casos en los que se solicita información completa del conjunto de datos, la carga útil de respuesta puede superar los 3 GB de tamaño, lo que puede ralentizar el rendimiento general. Por lo tanto, el uso de parámetros de consulta para filtrar solo la información necesaria hará que [!DNL Catalog] las consultas sean más eficientes.

#### Filtro de lista

Al filtrar respuestas, puede utilizar varios filtros en una sola llamada separando parámetros con un símbolo (`&`). Algunos parámetros de consulta aceptan listas de valores separadas por comas, como el filtro &quot;propiedades&quot; en la solicitud de ejemplo siguiente.

[!DNL Catalog] las respuestas se medirán automáticamente según los límites configurados, pero el parámetro de consulta &quot;limit&quot; puede utilizarse para personalizar las restricciones y limitar el número de objetos devueltos. Los límites de respuesta preconfigurados [!DNL Catalog] son:

- Si no se especifica un parámetro de límite, el número máximo de objetos por carga útil de respuesta es 20.
- El límite global para todas las demás [!DNL Catalog] consultas es de 100 objetos.
- Para consultas de conjuntos de datos, si se solicita observableSchema utilizando el parámetro de consulta de propiedades, el número máximo de conjuntos de datos devueltos es 20.
- Los parámetros de límite no válidos (incluido `limit=0`) se encuentran con un error HTTP 400 que describe los intervalos adecuados.
- Si los límites o desplazamientos se pasan como parámetros de consulta, tienen prioridad sobre los que se pasan como encabezados.

Los parámetros de consulta se tratan con más detalle en la descripción general [del servicio de](../catalog/home.md)catálogos.

**Formato API**

```http
GET /catalog/dataSets
GET /catalog/dataSets?{filter1}={value1},{value2}&{filter2}={value3}
```

**Solicitud**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets?limit=3&properties=name,description,schemaRef" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

Consulte la información general [del servicio de](../catalog/home.md) catálogo para ver ejemplos detallados de cómo realizar llamadas al [[!DNL Catalog API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml).

**Respuesta**

La respuesta incluye tres (`limit=3`) conjuntos de datos que muestran el &quot;nombre&quot;, la &quot;descripción&quot; y el &quot;esquemaRef&quot;, como indica el parámetro de `properties` consulta.

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

### Esquema del conjunto de datos de vista

La propiedad &quot;schemaRef&quot; de un conjunto de datos contiene un URI que hace referencia al esquema XDM en el que se basa el conjunto de datos. El esquema XDM (&quot;schemaRef&quot;) representa todos los campos potenciales que podría utilizar el conjunto de datos, no necesariamente los campos que se utilizan (consulte &quot;observableSchema&quot; más adelante).

El esquema XDM es el esquema que se utiliza cuando se necesita presentar al usuario una lista de todos los campos disponibles en los que se puede escribir.

El primer valor &quot;schemaRef.id&quot; en el objeto de respuesta anterior (`https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18`) es un URI que señala a un esquema XDM específico en el [!DNL Schema Registry]. El esquema se puede recuperar realizando una solicitud de búsqueda (GET) a la [!DNL Schema Registry] API.

>[!NOTE]
>
>La propiedad &quot;schemaRef&quot; sustituye a la propiedad &quot;esquema&quot;, que ahora está en desuso. Si &quot;schemaRef&quot; está ausente del conjunto de datos o no contiene un valor, deberá comprobar la presencia de una propiedad &quot;esquema&quot;. Esto se puede hacer reemplazando &quot;schemaRef&quot; por &quot;esquema&quot; en el parámetro de `properties` consulta de la llamada anterior. Encontrará más detalles sobre la propiedad &quot;esquema&quot; en la sección Propiedad [&quot;esquema&quot; de](#dataset-schema-property-deprecated---eol-2019-05-30) Dataset que se muestra a continuación.

**Formato API**

```http
GET /schemaregistry/tenant/schemas/{url encoded schemaRef.id}
```

**Solicitud**

La solicitud utiliza el `id` URI con codificación URL del esquema (el valor del atributo &quot;schemaRef.id&quot;) y requiere un encabezado Accept.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F274f17bc5807ff307a046bab1489fb18 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
```

El formato de respuesta depende del tipo de encabezado Accept enviado en la solicitud. Las solicitudes de búsqueda también requieren que `version` se incluyan en el encabezado Accept. La tabla siguiente describe los encabezados de Aceptar disponibles para las búsquedas:

| Aceptar | Descripción |
| ------ | ----------- |
| `application/vnd.adobe.xed-id+json` | Solicitudes de lista (GET), títulos, ID y versiones |
| `application/vnd.adobe.xed-full+json; version={major version}` | $refs y allOf resueltos, tiene títulos y descripciones |
| `application/vnd.adobe.xed+json; version={major version}` | Sin formato con $ref y allOf, tiene títulos y descripciones |
| `application/vnd.adobe.xed-notext+json; version={major version}` | Sin formato con $ref y allOf, sin títulos ni descripciones |
| `application/vnd.adobe.xed-full-notext+json; version={major version}` | $refs y todoDe resuelto, sin títulos ni descripciones |
| `application/vnd.adobe.xed-full-desc+json; version={major version}` | $refs y todoDe resueltos, se incluyen los descriptores |

>[!NOTE]
>
>`application/vnd.adobe.xed-id+json` y `application/vnd.adobe.xed-full+json; version={major version}` son los encabezados Accept más utilizados. `application/vnd.adobe.xed-id+json` es preferible para enumerar los recursos en la lista [!DNL Schema Registry] ya que devuelve solamente el &quot;título&quot;, el &quot;ID&quot; y la &quot;versión&quot;. `application/vnd.adobe.xed-full+json; version={major version}` es preferible para ver un recurso específico (por su &quot;id&quot;), ya que devuelve todos los campos (anidados en &quot;propiedades&quot;), así como títulos y descripciones.

**Respuesta**

El esquema JSON que se devuelve describe la información de estructura y de campo (&quot;tipo&quot;, &quot;formato&quot;, &quot;mínimo&quot;, &quot;máximo&quot;, etc.) de los datos, serializados como JSON. Si se utiliza un formato de serialización distinto de JSON para la ingestión (como Parquet o Scala), la Guía [del Registro de](../xdm/tutorials/create-schema-api.md) Esquema contiene una tabla que muestra el tipo de JSON deseado (&quot;meta:xdmType&quot;) y su representación correspondiente en otros formatos.

Junto con esta tabla, la Guía del [!DNL Schema Registry] programador contiene ejemplos detallados de todas las llamadas posibles que se pueden realizar mediante la [!DNL Schema Registry] API.

### Propiedad &quot;esquema&quot; del conjunto de datos (DESUSADO - EOL 2019-05-30)

Los conjuntos de datos pueden contener una propiedad &quot;esquema&quot; que ya no se utiliza y que permanece disponible temporalmente para la compatibilidad con versiones anteriores. Por ejemplo, una solicitud de listado (GET) similar a la realizada anteriormente, donde &quot;esquema&quot; se sustituyó por &quot;schemaRef&quot; en el parámetro de `properties` consulta, podría devolver lo siguiente:

```json
{
  "5ba9452f7de80400007fc52a": {
    "name": "Sample Dataset 1",
    "description": "Description of Sample Dataset 1.",
    "schema": "@/xdms/context/person"
  }
}
```

Si se rellena la propiedad &quot;esquema&quot; de un conjunto de datos, esto indica que el esquema es un esquema `/xdms` obsoleto y, cuando se admite, el conector ETL debe utilizar el valor de la propiedad &quot;esquema&quot; con el `/xdms` punto final (un punto final obsoleto en el [[!DNL Catalog API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)) para recuperar el esquema heredado.

**Formato API**

```http
GET /catalog/{"schema" property without the "@"}
```

**Solicitud**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/xdms/context/person?expansion=xdm" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

>[!NOTE]
>
>Un parámetro de consulta opcional `expansion=xdm`, indica a la API que expanda y en línea completamente cualquier esquema al que se haga referencia. Puede que desee hacerlo al presentar una lista de todos los campos posibles al usuario.

**Respuesta**

De forma similar a los pasos para [ver el esquema](#view-dataset-schema)del conjunto de datos, la respuesta contiene un esquema JSON que describe la estructura y la información de campo de los datos, serializados como JSON.

>[!NOTE]
>
>Cuando el campo &quot;esquema&quot; está vacío o está ausente en su totalidad, el conector debe leer el campo &quot;schemaRef&quot; y utilizar la API [del Registro de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) Esquema, como se muestra en los pasos anteriores, para [vista de un esquema](#view-dataset-schema)de conjunto de datos.

### La propiedad &quot;observableSchema&quot;

La propiedad &quot;observableSchema&quot; de un conjunto de datos tiene una estructura JSON que coincide con la del esquema JSON XDM. &quot;observableSchema&quot; contiene los campos que estaban presentes en los archivos de entrada entrantes. Al escribir datos en [!DNL Experience Platform], no es necesario que el usuario utilice todos los campos del esquema de destinatario. En su lugar, deben proporcionar solamente los campos que se están utilizando.

El esquema observable es el esquema que se utiliza para leer los datos o presentar una lista de los campos disponibles para leer o asignar.

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

### Datos de previsualización

La aplicación ETL puede proporcionar la capacidad de previsualización de datos ([&quot;Figura 8&quot; en el flujo de trabajo](./workflow.md)de ETL). La API de acceso a datos ofrece varias opciones para la previsualización de datos.

En el tutorial sobre el acceso a los [datos se puede encontrar información adicional, incluida una guía paso a paso para obtener una vista previa de los datos mediante la API de acceso a los datos](../data-access/tutorials/dataset-data.md).

### Obtener detalles del conjunto de datos mediante el parámetro de consulta &quot;properties&quot;

Como se muestra en los pasos anteriores para [vista de una lista de conjuntos](#view-list-of-datasets)de datos, puede solicitar &quot;archivos&quot; utilizando el parámetro de consulta &quot;propiedades&quot;.

Puede consultar la información general [del servicio de](../catalog/home.md) catálogo para obtener información detallada sobre cómo consultar conjuntos de datos y filtros de respuesta disponibles.

**Formato API**

```http
GET /catalog/dataSets?limit={value}&properties={value}
```

**Solicitud**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets?limit=1&properties=files" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
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

### Archivos de conjunto de datos de lista mediante el atributo &quot;files&quot;

También puede utilizar una solicitud de GET para recuperar los detalles del archivo mediante el atributo &quot;files&quot;.

**Formato API**

```http
GET /catalog/dataSets/{DATASET_ID}/views/{VIEW_ID}/files
```

**Solicitud**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets/5bf479a6a8c862000050e3c7/views/5bf479a654f52014cfffe7f1/files" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

**Respuesta**

La respuesta incluye el ID del archivo de conjunto de datos como propiedad de nivel superior, con los detalles del archivo contenidos en el objeto ID del archivo de conjunto de datos.

```json
{
    "194e89b976494c9c8113b968c27c1472-1": {
        "batchId": "194e89b976494c9c8113b968c27c1472",
        "dataSetViewId": "5bf479a654f52014cfffe7f1",
        "imsOrg": "{IMS_ORG}",
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
        "imsOrg": "{IMS_ORG}",
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
        "imsOrg": "{IMS_ORG}",
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

Los ID de archivo de conjunto de datos devueltos en la respuesta anterior se pueden utilizar en una solicitud de GET para obtener más detalles de archivo mediante la [!DNL Data Access] API.

La descripción general [del acceso a](../data-access/home.md) datos contiene detalles sobre cómo utilizar la [!DNL Data Access] API.

**Formato API**

```http
GET /export/files/{DATASET_FILE_ID}
```

**Solicitud**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
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

### Datos del archivo de previsualización

La propiedad &quot;href&quot; se puede utilizar para recuperar datos de previsualización mediante el [[!DNL Data Access API]](../data-access/home.md).

**Formato API**

```http
GET /export/files/{FILE_ID}?path={FILE_NAME}.{FILE_FORMAT}
```

**Solicitud**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1?path=samplefile.parquet" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

La respuesta a la solicitud anterior contendrá una previsualización del contenido del archivo.

Encontrará más información sobre la [!DNL Data Access] API, incluidas solicitudes y respuestas detalladas, en la descripción general [del acceso a](../data-access/home.md)datos.

### Obtener &quot;fileDescription&quot; del conjunto de datos

El componente de destino como resultado de datos transformados, el ingeniero de datos elegirá un conjunto de datos de salida ([&quot;Figura 12&quot; en el flujo de trabajo](workflow.md)de ETL). El esquema XDM está asociado al conjunto de datos de salida. Los datos que se escribirán se identificarán mediante el atributo &quot;fileDescription&quot; de la entidad del conjunto de datos de las API de detección de datos. Esta información se puede recuperar con una ID de conjunto de datos (`{DATASET_ID}`). La propiedad &quot;fileDescription&quot; de la respuesta JSON proporcionará la información solicitada.

**Formato API**

```shell
GET /catalog/dataSets/{DATASET_ID}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{DATASET_ID}` | El `id` valor del conjunto de datos al que intenta acceder. |

**Solicitud**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets/59c93f3da7d0c00000798f68" \
-H "accept: application/json" \
-H "x-gw-ims-org-id: {IMS_ORG}" \
-H "x-sandbox-name: {SANDBOX_NAME}" \
-H "Authorization: Bearer {ACCESS_TOKEN}" \
-H "x-api-key : {API_KEY}"
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

Los datos se escribirán en [!DNL Experience Platform] mediante la API [de inserción](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)de datos.  La escritura de datos es un proceso asincrónico. Cuando los datos se escriben en Adobe Experience Platform, se crea un lote y se marca como un éxito solo después de que los datos se hayan escrito completamente.

Los datos [!DNL Experience Platform] deben escribirse en forma de ficheros de parqué.

## Fase de ejecución

Como inicio de ejecución, el conector (tal como se define en el componente de origen) leerá los datos de [!DNL Experience Platform] uso del [[!DNL Data Access API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml). El proceso de transformación leerá los datos para un intervalo de tiempo determinado. Internamente, consulta lotes de conjuntos de datos de origen. Durante la consulta, utilizará archivos parametrizados (móviles para datos de series temporales o datos incrementales) de fecha de inicio y conjuntos de datos de lista para esos lotes, y inicios que solicitarán datos para esos archivos de conjuntos de datos.

### Transformaciones de ejemplo

El documento de transformaciones [ETL de](./transformations.md) ejemplo contiene una serie de transformaciones de ejemplo, como el manejo de identidades y las asignaciones de tipo de datos. Utilice estas transformaciones como referencia.

### Leer datos de [!DNL Experience Platform]

Con el [[!DNL Catalog API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml), puede recuperar todos los lotes entre una hora de inicio y una hora de finalización especificadas y ordenarlos según el orden en que se crearon.

**Solicitud**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?dataSet=DATASETID&createdAfter=START_TIMESTAMP&createdBefore=END_TIMESTAMP&sort=desc:created" \
  -H "Accept: application/json" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

Los detalles sobre el filtrado de lotes se encuentran en el tutorial [Acceso a](../data-access/tutorials/dataset-data.md)datos.

### Obtener archivos de un lote

Una vez que tenga el ID del lote que busca (`{BATCH_ID}`), es posible recuperar una lista de archivos pertenecientes a un lote específico a través del [[!DNL Data Access API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml).  Los detalles para hacerlo están disponibles en el [[!DNL Data Access] tutorial](../data-access/tutorials/dataset-data.md).

**Solicitud**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/files" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

### Acceso a archivos mediante el ID de archivo

Utilizando el ID exclusivo de un archivo (`{FILE_ID`), el archivo [[!DNL Data Access API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) puede utilizarse para acceder a los detalles específicos del archivo, incluido su nombre, tamaño en bytes y un vínculo para descargarlo.

**Solicitud**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{FILE_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key : {API_KEY}"
```

La respuesta puede apuntar a un solo archivo o a un directorio. Encontrará detalles sobre cada uno en el [[!DNL Data Access] tutorial](../data-access/tutorials/dataset-data.md).

### Acceso al contenido del archivo

El [[!DNL Data Access API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) se puede utilizar para acceder al contenido de un archivo específico. Para recuperar el contenido, se realiza una solicitud de GET utilizando el valor devuelto para `_links.self.href` cuando se accede a un archivo con el ID de archivo.

**Solicitud**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{DATASET_FILE_ID}?path=filename1.csv" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

La respuesta a esta solicitud contiene el contenido del archivo. Para obtener más información, incluidos detalles sobre la paginación de respuestas, consulte el tutorial [Cómo Consulta de datos mediante API](../data-access/tutorials/dataset-data.md) de acceso a datos.

### Validación de registros para el cumplimiento de esquemas

Cuando se escriben los datos, los usuarios pueden optar por validar los datos según las reglas de validación definidas en el esquema XDM. Puede encontrar más información sobre la validación de esquemas en el [ETL Ecosystem Integration Reference Code on [!DNL GitHub]](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md#validation).

Si utiliza la implementación de referencia que se encuentra en [[!DNL GitHub]](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md), puede activar la validación de esquema en esta implementación mediante la propiedad del sistema `-DenableSchemaValidation=true`.

La validación se puede realizar para tipos XDM lógicos, utilizando atributos como `minLength` y `maxlength` para cadenas, `minimum` y `maximum` para enteros, entre otros. La guía [para desarrolladores de la API de registro de](../xdm/api/getting-started.md) Esquema contiene una tabla que describe los tipos XDM y las propiedades que se pueden utilizar para la validación.

>[!NOTE]
>
>Los valores mínimo y máximo proporcionados para varios `integer` tipos son los valores MIN y MAX que el tipo puede admitir, pero estos valores pueden estar restringidos a los mínimos y máximos que elija.

### Crear un lote

Una vez procesados los datos, la herramienta ETL volverá a escribir los datos [!DNL Experience Platform] mediante la API [de inserción de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)lotes. Antes de agregar datos a un conjunto de datos, debe vincularse a un lote que luego se cargará en un conjunto de datos específico.

**Solicitud**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -d '{
        "datasetId":"{DATASET_ID}"
      }'
```

Los detalles para crear un lote, incluidas las solicitudes de muestra y las respuestas, se encuentran en la información general [de la ingesta de](../ingestion/batch-ingestion/overview.md)lotes.

### Escribir en conjunto de datos

Después de crear correctamente un nuevo lote, los archivos se pueden cargar a un conjunto de datos específico. Se pueden registrar varios archivos en un lote hasta que se promocione. Los archivos se pueden cargar mediante la API de carga de archivos pequeños; sin embargo, si los archivos son demasiado grandes y se supera el límite de la puerta de enlace, puede utilizar la API de carga de archivos grande. Los detalles para el uso de Carga de archivos grande y pequeña se encuentran en la información general [de ingestión de](../ingestion/batch-ingestion/overview.md)lotes.

**Solicitud**

Los datos [!DNL Experience Platform] deben escribirse en forma de ficheros de parqué.

```shell
curl -X PUT "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/dataSets/{DATASET_ID}/files/{FILE_NAME}.parquet" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id:{IMS_ORG}" \
  -H "Authorization:Bearer ACCESS_TOKEN" \
  -H "x-api-key: API_KEY" \
  -H "content-type: application/octet-stream" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

### Marcar carga por lotes completada

Una vez cargados todos los archivos en el lote, se puede indicar la finalización del lote. Al hacer esto, se crean las entradas [!DNL Catalog] &quot;DataSetFile&quot; para los archivos completados y se asocian al lote de generación. A continuación, el [!DNL Catalog] lote se marca como correcto, lo que desencadena flujos descendentes para ingestar los datos disponibles.

Los datos primero aterrizarán en la ubicación de ensayo en Adobe Experience Platform y luego se moverán a la ubicación final después de catalogarlos y validarlos. Los lotes se marcarán como correctos una vez que todos los datos se muevan a una ubicación permanente.

**Solicitud**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

Si se realiza correctamente, la respuesta devolverá el estado HTTP 200 OK y el cuerpo de la respuesta estará vacío.

La herramienta ETL se asegurará de anotar la marca de tiempo de los conjuntos de datos de origen a medida que se leen los datos.

En la siguiente ejecución de transformación, probablemente mediante programación o invocación de evento, la ETL realizará inicios solicitando los datos de la marca de tiempo guardada anteriormente y todos los datos a partir de ahora.

### Obtener el estado del último lote

Antes de ejecutar nuevas tareas en la herramienta ETL, debe asegurarse de que el último lote se completó correctamente. El [[!DNL Catalog Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) proporciona una opción específica para cada lote que proporciona los detalles de los lotes relevantes.

**Solicitud**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?limit=1&sort=desc:created" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Respuesta**

Se pueden programar nuevas tareas si el valor de &quot;estado&quot; del lote anterior es &quot;éxito&quot;, como se muestra a continuación:

```json
"{BATCH_ID}": {
    "imsOrg": "{IMS_ORG}",
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

Se puede recuperar un estado de lote individual mediante el [[!DNL Catalog Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) envío de una solicitud de GET mediante el `{BATCH_ID}`. El valor `{BATCH_ID}` utilizado sería el mismo que el ID devuelto cuando se creó el lote.

**Solicitud**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID}" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Respuesta - Éxito**

La siguiente respuesta muestra un &quot;éxito&quot;:

```json
"{BATCH_ID}": {
    "imsOrg": "{IMS_ORG}",
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

En caso de error, los &quot;errores&quot; se pueden extraer de la respuesta y aparecer en la herramienta ETL como mensajes de error.

```json
"{BATCH_ID}": {
    "imsOrg": "{IMS_ORG}",
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

Los datos pueden representarse en dos matrices, como se indica a continuación:

| Eventos incrementales | Perfiles incrementales |
|-------------------------------|----------------------|
| Eventos de instantáneas (menos probable) | Perfiles de instantáneas |

Los datos de evento suelen aparecer cuando hay columnas de marcas de hora indizadas en cada fila.

Los datos de perfil suelen ser cuando no hay una marca de hora en los datos y cada fila se puede identificar mediante una clave principal o compuesta.

Los datos incrementales son aquellos en los que sólo los datos nuevos o actualizados entran en el sistema y se anexan a los datos actuales en los conjuntos de datos.

Los datos de las instantáneas se producen cuando todos los datos entran en el sistema y sustituyen algunos o todos los datos anteriores de un conjunto de datos.

En el caso de eventos incrementales, la herramienta ETL debe utilizar las fechas disponibles/crear la fecha de la entidad por lotes. En el caso de servicio push, las fechas disponibles no estarán presentes, por lo que la herramienta utilizará la fecha de creación o actualización por lotes para marcar los incrementos. Es necesario procesar todos los lotes de eventos incrementales.

Para los perfiles incrementales, la herramienta ETL utilizará las fechas creadas o actualizadas de la entidad por lotes. Normalmente, se requiere que se procesen todos los lotes de datos de perfil incremental.

Los eventos de instantáneas son muy poco probables debido al tamaño de los datos. Pero si esto fuera necesario, la herramienta ETL debe elegir sólo el último lote para el procesamiento.

Cuando se utilizan perfiles de instantánea, la herramienta ETL tendrá que elegir el último lote de datos que llegó al sistema. Pero si lo necesario es realizar un seguimiento de las versiones de los cambios, entonces todos los lotes deberán procesarse. El procesamiento de la desduplicación dentro del proceso de ETL ayudará a controlar los costos de almacenamiento.

## Reproducción por lotes y reprocesamiento de datos

Es posible que se requiera la reproducción por lotes y el reprocesamiento de datos en los casos en que un cliente descubra que durante los últimos &quot;n&quot; días, los datos que se están procesando no se han producido del modo esperado o los datos de origen en sí no han sido correctos.

Para ello, los administradores de datos del cliente utilizarán la interfaz de usuario [!DNL Platform] para eliminar los lotes que contienen datos dañados. Luego, es probable que se deba volver a ejecutar el ETL, con lo que se volverá a rellenar con los datos correctos. Si el origen en sí tenía datos dañados, el ingeniero o administrador de datos deberá corregir los lotes de origen y volver a ingestar los datos (ya sea en Adobe Experience Platform o mediante conectores ETL).

Según el tipo de datos que se generen, será la elección del ingeniero de datos eliminar un solo lote o todos los lotes de ciertos conjuntos de datos. Los datos se eliminarán o archivarán según [!DNL Experience Platform] las directrices.

Es probable que la funcionalidad de ETL para depurar datos sea importante.

Una vez finalizada la purga, los administradores del cliente tendrán que volver a configurar Adobe Experience Platform para reiniciar el procesamiento de los servicios principales desde el momento en que se eliminen los lotes.

## Procesamiento simultáneo por lotes

A discreción del cliente, los administradores/ingenieros de datos pueden decidir extraer, transformar y cargar datos de manera secuencial o simultánea, según las características de un conjunto de datos en particular. Esto también se basará en el caso de uso que el cliente está dirigiendo con los datos transformados.

Por ejemplo, si el cliente persiste en un almacén de persistencia actualizable y la secuencia o el orden de eventos es importante, es posible que el cliente tenga que procesar estrictamente los trabajos con transformaciones de ETL secuenciales.

En otros casos, los datos desordenados pueden ser procesados por aplicaciones/procesos que se ordenan internamente usando una marca de tiempo específica. En esos casos, las transformaciones de ETL paralelas pueden ser viables para mejorar los tiempos de procesamiento.

Para los lotes de origen, nuevamente dependerá de la preferencia del cliente y de la restricción del consumidor. Si los datos de origen se pueden recoger en paralelo sin tener en cuenta la regencia o el orden de una fila, el proceso de transformación puede crear lotes de proceso con un mayor grado de paralelismo (optimización basada en el procesamiento por orden). Pero si la transformación tiene que cumplir con las marcas de hora o cambiar el orden de prioridad, la API de acceso a datos o la invocación/Planificador de herramientas de ETL deberán asegurarse de que los lotes no se procesen desordenados cuando sea posible.

## Aplazamiento

El aplazamiento es un proceso en el que los datos de entrada aún no se han completado lo suficiente como para enviarse a procesos posteriores, pero pueden utilizarse en el futuro. Los clientes determinarán su tolerancia individual para la limitación de datos para la correspondencia futura en comparación con el costo del procesamiento para informar su decisión de dejar de lado los datos y volver a procesarlos en la próxima ejecución de transformación, con la esperanza de que se puedan enriquecer y reconciliar/unir en algún momento futuro dentro de la ventana de retención. Este ciclo continúa hasta que la fila se procesa lo suficiente o se considera que es demasiado antigua para continuar invirtiendo en él. Cada iteración generará datos diferidos, que es un superconjunto de todos los datos diferidos en iteraciones anteriores.

Adobe Experience Platform no identifica actualmente los datos diferidos, por lo que las implementaciones de cliente deben basarse en las configuraciones manuales de ETL y Dataset para crear otro conjunto de datos al [!DNL Platform] espejar el conjunto de datos de origen que se puede utilizar para mantener los datos diferidos. En este caso, los datos diferidos serán similares a los datos de instantáneas. En cada ejecución de la transformación ETL, los datos de origen se unirán con los datos diferidos y se enviarán para su procesamiento.

## Changelog

| Fecha | Acción | Descripción |
| ---- | ------ | ----------- |
| 2019-01-19 | Se ha eliminado la propiedad &quot;fields&quot; de los conjuntos de datos | Anteriormente, los conjuntos de datos incluían una propiedad &quot;fields&quot; que contenía una copia del esquema. Esta capacidad ya no debe usarse. Si se encuentra la propiedad &quot;fields&quot;, se debe ignorar y se debe utilizar &quot;seenSchema&quot; o &quot;schemaRef&quot; en su lugar. |
| 2019-03-15 | Se agregó la propiedad &quot;schemaRef&quot; a los conjuntos de datos | La propiedad &quot;schemaRef&quot; de un conjunto de datos contiene un URI que hace referencia al esquema XDM en el que se basa el conjunto de datos y representa todos los campos potenciales que podría utilizar el conjunto de datos. |
| 2019-03-15 | Todos los identificadores de usuario final se asignan a la propiedad &quot;identityMap&quot; | &quot;identityMap&quot; es una encapsulación de todos los identificadores únicos de un asunto, como ID de CRM, ECID o ID de programa de lealtad. Este mapa se utiliza para [[!DNL Identity Service]](../identity-service/home.md) resolver todas las identidades conocidas y anónimas de un sujeto, formando un único gráfico de identidad para cada usuario final. |
| 2019-05-30 | EOL y Eliminar la propiedad &quot;esquema&quot; de los conjuntos de datos | La propiedad &quot;esquema&quot; del conjunto de datos proporcionó un vínculo de referencia al esquema mediante el punto final `/xdms` desaprobado en la [!DNL Catalog] API. Esto se ha reemplazado por un &quot;schemaRef&quot; que proporciona la &quot;id&quot;, &quot;version&quot; y &quot;contentType&quot; del esquema como se hace referencia en la nueva [!DNL Schema Registry] API. |