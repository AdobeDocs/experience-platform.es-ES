---
keywords: Experience Platform;home;popular topics;filter;Filter;filter data;Filter data;date range
solution: Experience Platform
title: Filtrar datos del catálogo mediante parámetros de consulta
topic: developer guide
description: La API de servicio de catálogo permite filtrar los datos de respuesta mediante el uso de parámetros de consulta de solicitud. Una de las prácticas recomendadas para Catalog es utilizar filtros en todas las llamadas de API, ya que reducen la carga en la API y ayudan a mejorar el rendimiento general.
translation-type: tm+mt
source-git-commit: 71678b10c9e137016ea404305b272508b9c8cabe
workflow-type: tm+mt
source-wordcount: '2077'
ht-degree: 1%

---


# Filtrar [!DNL Catalog] datos mediante parámetros de consulta

La [!DNL Catalog Service] API permite filtrar los datos de respuesta mediante el uso de parámetros de consulta de solicitud. Una de las prácticas recomendadas para [!DNL Catalog] esta función es utilizar filtros en todas las llamadas de API, ya que reducen la carga de la API y ayudan a mejorar el rendimiento general.

Este documento describe los métodos más comunes para filtrar [!DNL Catalog] objetos en la API. Se recomienda que haga referencia a este documento mientras lee la guía [para desarrolladores de](getting-started.md) catálogos para obtener más información sobre cómo interactuar con la [!DNL Catalog] API. Para obtener más información general sobre [!DNL Catalog Service], consulte la [[!DNL Catalog] información general](../home.md).

## Limitar objetos devueltos

El parámetro de `limit` consulta limita el número de objetos devueltos en una respuesta. [!DNL Catalog] las respuestas se medirán automáticamente según los límites configurados:

* Si no se especifica un `limit` parámetro, el número máximo de objetos por carga útil de respuesta es 20.
* Para consultas de conjuntos de datos, si `observableSchema` se solicita usando el parámetro de `properties` consulta, el número máximo de conjuntos de datos devueltos es 20.
* El límite global para todas las demás consultas del catálogo es de 100 objetos.
* Los parámetros `limit` no válidos (incluido `limit=0`) dan como resultado respuestas de error de 400 niveles que describen intervalos adecuados.
* Los límites o desplazamientos que se pasan como parámetros de consulta tienen prioridad sobre los que se pasan como encabezados.

**Formato API**

```http
GET /{OBJECT_TYPE}?limit={LIMIT}
```

| Parámetro | Descripción |
| --- | --- |
| `{OBJECT_TYPE}` | Tipo de [!DNL Catalog] objeto que se va a recuperar. Los objetos válidos son: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{LIMIT}` | Un entero que indica el número de objetos que se van a devolver, desde 1 hasta 100. |

**Solicitud**

La siguiente solicitud recupera una lista de conjuntos de datos mientras limita la respuesta a tres objetos.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?limit=3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una lista de conjuntos de datos, limitada al número indicado por el parámetro de `limit` consulta.

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset 1",
        "description": "Description of dataset.",
        "files": "@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"
    },
    "5bb276b03a14440000971552": {
        "name": "Sample Dataset 2",
        "description": "Description of dataset.",
        "files": "@/dataSets/5bb276b03a14440000971552/views/5bb276b01250b012f9acc75b/files"
    },
    "5bceaa4c26c115000039b24b": {
        "name": "Sample Dataset 3"
    }
}
```

## Limitar las propiedades mostradas

Incluso cuando se filtra el número de objetos devueltos mediante el `limit` parámetro, los objetos devueltos pueden contener con frecuencia más información de la que realmente se necesita. Para reducir aún más la carga en el sistema, se recomienda filtrar las respuestas para incluir solo las propiedades que necesite.

El `properties` parámetro filtros a los objetos de respuesta para que devuelvan sólo un conjunto de propiedades especificadas. El parámetro puede configurarse para devolver una o varias propiedades.

El `properties` parámetro solo acepta propiedades de objeto de nivel superior, lo que significa que para el siguiente objeto de muestra, se pueden aplicar filtros para `name`, `description`y `subItem`, pero NO para `sampleKey`.

```json
{
  "5ba9452f7de80400007fc52a": {
      "name": "Sample Dataset",
      "description": "Sample dataset containing important data",
      "subitem": {
          "sampleKey": "sampleValue"
      }
  }
}
```

**Formato API**

```http
GET /{OBJECT_TYPE}?properties={PROPERTY}
GET /{OBJECT_TYPE}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
GET /{OBJECT_TYPE}/{OBJECT_ID}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| Parámetro | Descripción |
| --- | --- |
| `{OBJECT_TYPE}` | Tipo de [!DNL Catalog] objeto que se va a recuperar. Los objetos válidos son: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY}` | Nombre de un atributo que se incluirá en el cuerpo de la respuesta. |
| `{OBJECT_ID}` | Identificador único de un [!DNL Catalog] objeto específico que se recupera. |

**Solicitud**

La siguiente solicitud recupera una lista de conjuntos de datos. La lista separada por comas de los nombres de propiedad que se proporciona bajo el `properties` parámetro indica las propiedades que se devolverán en la respuesta. También se incluye un `limit` parámetro, que limita el número de conjuntos de datos devueltos. Si la solicitud no incluye un `limit` parámetro, la respuesta contendrá un máximo de 20 objetos.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=4&properties=name,schemaRef' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una lista de [!DNL Catalog] objetos con solo las propiedades solicitadas mostradas.

```json
{
    "Dataset1": {
        "name": "Dataset 1",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/bc82c518380478b59a95c63e0f843121",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    },
    "Dataset2": {},
    "Dataset3": {
        "name": {},
    },
    "Dataset4": {
        "name": "Dataset 4",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/142afb78d8b368a5ba97a6cc8fc7e033",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    }
}
```

Según la respuesta anterior, se puede inferir lo siguiente:

* Si a un objeto le falta alguna propiedad solicitada, solo se mostrarán las propiedades solicitadas que incluye. (`Dataset1`)
* Si un objeto no incluye ninguna de las propiedades solicitadas, aparecerá como un objeto vacío. (`Dataset2`)
* Un conjunto de datos puede devolver una propiedad solicitada como un objeto vacío si contiene la propiedad pero no hay ningún valor. (`Dataset3`)
* De lo contrario, el conjunto de datos mostrará el valor completo de todas las propiedades solicitadas. (`Dataset4`)

## Índice inicial de desplazamiento de la lista de respuesta

El parámetro de `start` consulta desplaza la lista de respuesta hacia delante en un número especificado, mediante la numeración basada en cero. Por ejemplo, `start=2` desplazaría la respuesta al inicio en el tercer objeto de la lista.

Si el `start` parámetro no está emparejado con un `limit` parámetro, el número máximo de objetos devueltos es 20.

**Formato API**

```http
GET /{OBJECT_TYPE}?start={OFFSET}
```

| Parámetro | Descripción |
| --- | --- |
| `{OBJECT_TYPE}` | Tipo de objeto Catalog que se va a recuperar. Los objetos válidos son: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OFFSET}` | Un entero que indica el número de objetos por los que se va a desplazar la respuesta. |

**Solicitud**

La siguiente solicitud recupera una lista de conjuntos de datos, se desplaza al quinto objeto (`start=4`) y limita la respuesta a dos conjuntos de datos devueltos (`limit=2`).

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?start=4&limit=2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

La respuesta incluye un objeto JSON que contiene dos elementos de nivel superior (`limit=2`), uno para cada conjunto de datos y sus detalles (los detalles se han resumido en el ejemplo). La respuesta se cambia por cuatro (`start=4`), lo que significa que los conjuntos de datos mostrados son el número cinco y seis cronológicamente.

```json
{
    "Dataset5": {},
    "Dataset6": {}
}
```

## Filtrar por etiqueta

Algunos objetos Catalog admiten el uso de un `tags` atributo. Las etiquetas pueden adjuntar información a un objeto y luego utilizarse para recuperarlo. La elección de las etiquetas que se deben utilizar y la forma de aplicarlas depende de los procesos de la organización.

Existen algunas limitaciones que hay que tener en cuenta al usar etiquetas:

* Los únicos objetos Catalog que admiten etiquetas actualmente son conjuntos de datos, lotes y conexiones.
* Los nombres de las etiquetas son exclusivos de la organización de IMS.
* Los procesos de Adobe pueden aprovechar las etiquetas para determinados comportamientos. Los nombres de estas etiquetas llevan el prefijo &quot;adobe&quot; como estándar. Por lo tanto, debe evitar esta convención al declarar nombres de etiquetas.
* Los siguientes nombres de etiquetas están reservados para su uso en todas partes [!DNL Experience Platform]y, por lo tanto, no se pueden declarar como nombres de etiqueta para su organización:
   * `unifiedProfile`:: Este nombre de etiqueta está reservado para los conjuntos de datos que [[!DNL Real-time Customer Profile]](../../profile/home.md).
   * `unifiedIdentity`:: Este nombre de etiqueta está reservado para los conjuntos de datos que [[!DNL Identity Service]](../../identity-service/home.md).

A continuación se muestra un ejemplo de un conjunto de datos que contiene una `tags` propiedad. Las etiquetas de esa propiedad adoptan la forma de pares clave-valor, y cada valor de etiqueta aparece como una matriz que contiene una sola cadena:

```json
{
    "5be1f2ecc73c1714ceba66e2": {
        "imsOrg": "{IMS_ORG}",
        "tags": {
            "sampleTag": [
                "123456"
            ],
            "secondTag": [
                "sample_tag_value"
            ]
        },
        "name": "Sample Dataset",
        "description": "Same dataset containing sample data.",
        "dule": {
            "identity": [
                "I1"
            ]
        },
        "statsCache": {},
        "state": "DRAFT",
        "lastBatchId": "ca12b29612bf4052872edad59573703c",
        "lastBatchStatus": "success",
        "lastSuccessfulBatch": "ca12b29612bf4052872edad59573703c",
        "namespace": "{NAMESPACE}",
        "createdUser": "{CREATED_USER}",
        "createdClient": "{CREATED_CLIENT}",
        "updatedUser": "{UPDATED_USER}",
        "version": "1.0.0",
        "created": 1541534444286,
        "updated": 1541534444286
    }
}
```

**Formato API**

Los valores del `tags` parámetro toman la forma de pares clave-valor, utilizando el formato `{TAG_NAME}:{TAG_VALUE}`. Se pueden proporcionar varios pares clave-valor en forma de lista separada por comas. Cuando se proporcionan varias etiquetas, se asume una relación Y.

El parámetro admite caracteres comodín (`*`) para valores de etiqueta. Por ejemplo, una cadena de búsqueda `test*` devuelve cualquier objeto donde el valor de la etiqueta comience por &quot;test&quot;. Una cadena de búsqueda que consiste únicamente en un comodín puede utilizarse para filtrar objetos en función de si contienen o no una etiqueta específica, independientemente de su valor.

```http
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}
GET /{OBJECT_TYPE}?tags={TAG_NAME_1}:{TAG_VALUE_1},{TAG_NAME_2}:{TAG_VALUE_2}
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}*
GET /{OBJECT_TYPE}?tags={TAG_NAME}:*
```

| Parámetro | Descripción |
| --- | --- |
| `{OBJECT_TYPE}` | Tipo de [!DNL Catalog] objeto que se va a recuperar. Los objetos válidos son: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li></ul> |
| `{TAG_NAME}` | Nombre de la etiqueta por la que se va a filtrar. |
| `{TAG_VALUE}` | El valor de la etiqueta por la que se va a filtrar. Admite caracteres comodín (`*`). |

**Solicitud**

La siguiente solicitud recupera una lista de conjuntos de datos, filtrando por una etiqueta que tiene un valor específico Y la segunda etiqueta que está presente.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?tags=sampleTag:123456,secondTag:* \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una lista de conjuntos de datos que contienen `sampleTag` un valor de &quot;123456&quot;, Y `secondTag` con cualquier valor. A menos que también se especifique un límite, la respuesta contiene un máximo de 20 objetos.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{IMS_ORG}",
            "name": "Example Dataset 1",
            "created": 1533539550237,
            "updated": 1533539552416,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "tags": {
                "sampleTag": [
                    "123456"
                ],
                "secondTag": [
                    "Example tag value"
                ]
            },
            "dule": {},
            "statsCache": {}
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.0",
            "imsOrg": "{IMS_ORG}",
            "name": "Example Dataset 2",
            "created": 1533539550237,
            "updated": 1533539552416,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "tags": {
                "sampleTag": [
                    "123456"
                ],
                "secondTag": [
                    "A different tag value"
                ],
                "anotherTag": [
                    "2.0"
                ]
            },
            "dule": {},
            "statsCache": {}
    }
}
```

## Filtrar por intervalo de fechas

Algunos extremos de la [!DNL Catalog] API tienen parámetros de consulta que permiten consultas de rango, la mayoría de las veces en el caso de las fechas.

**Formato API**

```http
GET /batches?createdAfter={TIMESTAMP_1}&createdBefore={TIMESTAMP_2}
```

| Parámetro | Descripción |
| --- | --- |
| `{TIMESTAMP }` | Un entero de fecha y hora en hora de Unix Epoch. |

**Solicitud**

La siguiente solicitud recupera una lista de lotes creados durante el mes de abril de 2019.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/batches?createdAfter=1554076800000&createdBefore=1556668799000' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta contiene una lista de [!DNL Catalog] objetos que se encuentran dentro del intervalo de fechas especificado. A menos que también se especifique un límite, la respuesta contiene un máximo de 20 objetos.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{IMS_ORG}",
            "name": "Example Dataset 1",
            "created": 1554930967705,
            "updated": 1554931119718,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.0",
            "imsOrg": "{IMS_ORG}",
            "name": "Example Dataset 2",
            "created": 1554974386247,
            "updated": 1554974386268,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    }
}
```

## Ordenar por propiedad

El parámetro de `orderBy` consulta permite ordenar los datos de respuesta en función de un valor de propiedad especificado. Este parámetro requiere una &quot;dirección&quot; (`asc` para ascendente o `desc` descendente), seguida de dos puntos (`:`) y, a continuación, una propiedad para ordenar los resultados. Si no se especifica una dirección, la dirección predeterminada es ascendente.

En una lista separada por comas se pueden proporcionar varias propiedades de ordenación. Si la primera propiedad de ordenación produce varios objetos que contienen el mismo valor para esa propiedad, se utilizará la segunda propiedad de ordenación para ordenar los objetos coincidentes.

For example, consider the following query: `orderBy=name,desc:created`. Los resultados se ordenan en orden ascendente según la primera propiedad de clasificación, `name`. En los casos en que varios registros comparten la misma `name` propiedad, los registros coincidentes se ordenan por la segunda propiedad de ordenación, `created`. Si ningún registro devuelto comparte lo mismo `name`, la `created` propiedad no se tiene en cuenta en la ordenación.


**Formato API**

```http
GET /{OBJECT_TYPE}?orderBy=asc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy=desc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy={PROPERTY_NAME_1},desc:{PROPERTY_NAME_2}
```

| Parámetro | Descripción |
| --- | --- |
| `{OBJECT_TYPE}` | Tipo de objeto Catalog que se va a recuperar. Los objetos válidos son: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY_NAME}` | Nombre de una propiedad por la que se ordenarán los resultados. |

**Solicitud**

La siguiente solicitud recupera una lista de conjuntos de datos ordenados por su `name` propiedad. Si alguno de los conjuntos de datos comparte lo mismo `name`, esos conjuntos de datos se ordenarán a su vez por su `updated` propiedad en orden descendente.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?orderBy=name,desc:updated' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta contiene una lista de [!DNL Catalog] objetos ordenados según el `orderBy` parámetro. A menos que también se especifique un límite, la respuesta contiene un máximo de 20 objetos.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{IMS_ORG}",
            "name": "0405",
            "created": 1554930967705,
            "updated": 1554931119718,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.3",
            "imsOrg": "{IMS_ORG}",
            "name": "AAM Dataset",
            "created": 1554974386247,
            "updated": 1554974386268,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5cd3a129ec106214b722a939": {
            "version": "1.0.2",
            "imsOrg": "{IMS_ORG}",
            "name": "AAM Dataset",
            "created": 1554028394852,
            "updated": 1554130582960,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    }
}
```

## Filtrar por propiedad

[!DNL Catalog] proporciona dos métodos de filtrado por propiedad, que se describen en detalle en las secciones siguientes:

* [Uso de filtros](#using-simple-filters)simples: Filtre por si una propiedad específica coincide con un valor específico.
* [Uso del parámetro](#using-the-property-parameter)property: Utilice expresiones condicionales para filtrar según si existe una propiedad o si el valor de una propiedad coincide, se aproxima o se compara con otro valor especificado o con otra expresión regular.

### Uso de filtros simples {#using-simple-filters}

Los filtros simples le permiten filtrar las respuestas en función de valores de propiedad específicos. Un filtro simple toma la forma de `{PROPERTY_NAME}={VALUE}`.

Por ejemplo, la consulta `name=exampleName` devuelve sólo objetos cuya `name` propiedad contiene un valor de &quot;exampleName&quot;. Por el contrario, la consulta `name=!exampleName` devuelve sólo objetos cuya `name` propiedad **no sea** &quot;exampleName&quot;.

Además, los filtros simples admiten la capacidad de consulta de varios valores para una sola propiedad. Cuando se proporcionan varios valores, la respuesta devuelve objetos cuya propiedad coincide con **cualquiera** de los valores de la lista proporcionada. Puede invertir una consulta de varios valores añadiendo un `!` carácter como prefijo a la lista, devolviendo solo los objetos cuyo valor de propiedad **no esté** en la lista proporcionada (por ejemplo, `name=!exampleName,anotherName`).

**Formato API**

```http
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE_1},{VALUE_2},{VALUE_3}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE_1},{VALUE_2},{VALUE_3}
```

| Parámetro | Descripción |
| --- | --- |
| `{OBJECT_TYPE}` | Tipo de [!DNL Catalog] objeto que se va a recuperar. Los objetos válidos son: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY_NAME}` | Nombre de la propiedad cuyo valor desea filtrar. |
| `{VALUE}` | Un valor de propiedad que determina qué resultados se incluirán (o excluirán, según la consulta). |

**Solicitud**

La siguiente solicitud recupera una lista de conjuntos de datos, filtrados para incluir solo conjuntos de datos cuya `name` propiedad tiene un valor de &quot;exampleName&quot; u &quot;anotherName&quot;.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?name=exampleName,anotherName' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta contiene una lista de conjuntos de datos, excluyendo cualquier conjunto de datos cuyo `name` es &quot;exampleName&quot; u &quot;anotherName&quot;. A menos que también se especifique un límite, la respuesta contiene un máximo de 20 objetos.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{IMS_ORG}",
            "name": "exampleName",
            "created": 1554930967705,
            "updated": 1554931119718,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.3",
            "imsOrg": "{IMS_ORG}",
            "name": "anotherName",
            "created": 1554974386247,
            "updated": 1554974386268,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    }
}
```

### Uso del `property` parámetro {#using-the-property-parameter}

El parámetro de `property` consulta proporciona más flexibilidad para el filtrado basado en propiedades que filtros simples. Además del filtrado en función de si una propiedad tiene un valor específico, el `property` parámetro puede utilizar otros operadores de comparación (como &quot;más que&quot; (`>`) y &quot;menos que&quot; (`<`)), así como expresiones regulares para filtrar por valores de propiedad. También puede filtrar por si existe o no una propiedad, independientemente de su valor.

El `property` parámetro sólo acepta propiedades de objeto de nivel superior, lo que significa que para el siguiente objeto de ejemplo, puede filtrar por propiedad `name`, `description`y `subItem`, pero NO por `sampleKey`.

```json
{
  "5ba9452f7de80400007fc52a": {
      "name": "Sample Dataset",
      "description": "Sample dataset containing important data",
      "subitem": {
          "sampleKey": "sampleValue"
      }
  }
}
```

**Formato API**

```http
GET /{OBJECT_TYPE}?property={CONDITION}
```

| Parámetro | Descripción |
| --- | --- |
| `{OBJECT_TYPE}` | Tipo de [!DNL Catalog] objeto que se va a recuperar. Los objetos válidos son: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{CONDITION}` | Expresión condicional que indica para qué propiedad se va a realizar la consulta y cómo se va a evaluar su valor. A continuación se proporcionan ejemplos. |

El valor del `property` parámetro admite varios tipos diferentes de expresiones condicionales. La siguiente tabla describe la sintaxis básica de las expresiones admitidas:

| Símbolo(s) | Descripción | Ejemplo |
| --- | --- | --- |
| (Ninguna) | Al establecer el nombre de la propiedad sin operador, solo se devuelven los objetos donde existe la propiedad, independientemente de su valor. | `property=name` |
| ! | Al prefijar un &quot;`!`&quot; en el valor de un `property` parámetro, sólo se devuelven objetos en los que la propiedad **no existe** . | `property=!name` |
| ~ | Devuelve sólo objetos cuyos valores de propiedad (cadena) coinciden con una expresión normal proporcionada después del símbolo de virgulilla (`~`). | `property=name~^example` |
| == | Devuelve sólo objetos cuyos valores de propiedad coinciden exactamente con la cadena proporcionada después del símbolo doble-es (`==`). | `property=name==exampleName` |
| != | Devuelve únicamente objetos cuyos valores de propiedad **no coinciden con** la cadena proporcionada después del símbolo no-es (`!=`). | `property=name!=exampleName` |
| &lt; | Devuelve sólo objetos cuyos valores de propiedad sean inferiores (pero no iguales) a una cantidad declarada. | `property=version<1.0.0` |
| &lt;= | Devuelve sólo objetos cuyos valores de propiedad sean inferiores (o iguales a) una cantidad declarada. | `property=version<=1.0.0` |
| > | Devuelve sólo objetos cuyos valores de propiedad son buenos (pero no iguales a) una cantidad declarada. | `property=version>1.0.0` |
| >= | Devuelve sólo objetos cuyos valores de propiedad sean buenos (o iguales a) una cantidad declarada. | `property=version>=1.0.0` |

>[!NOTE]
>
>La `name` propiedad admite el uso de un comodín `*`, ya sea como la cadena de búsqueda completa o como parte de ella. Los comodines coinciden con caracteres vacíos, de modo que la cadena de búsqueda `te*st` coincidirá con el valor &quot;test&quot;. Los asteriscos se escapan duplicándolos (`**`). Un asterisco de doble en una cadena de búsqueda representa un asterisco único como cadena literal.

**Solicitud**

La siguiente solicitud devolverá cualquier conjunto de datos con un número de versión bueno a 1.0.3.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?property=version>1.0.3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta contiene una lista de conjuntos de datos cuyos números de versión son buenos a 1.0.3. A menos que también se especifique un límite, la respuesta contiene un máximo de 20 objetos.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.1.2",
            "imsOrg": "{IMS_ORG}",
            "name": "sampleDataset",
            "created": 1554930967705,
            "updated": 1554931119718,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.6",
            "imsOrg": "{IMS_ORG}",
            "name": "exampleDataset",
            "created": 1554974386247,
            "updated": 1554974386268,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5cd3a129ec106214b722a939": {
            "version": "1.0.4",
            "imsOrg": "{IMS_ORG}",
            "name": "anotherDataset",
            "created": 1554028394852,
            "updated": 1554130582960,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    }
}
```

## Combinar varios filtros

Con un símbolo (`&`), puede combinar varios filtros en una sola solicitud. Cuando se agregan condiciones adicionales a una solicitud, se asume una relación Y.

**Formato API**

```http
GET /{OBJECT_TYPE}?{FILTER_1}={VALUE}&{FILTER_2}={VALUE}&{FILTER_3}={VALUE}
```
