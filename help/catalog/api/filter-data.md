---
keywords: Experience Platform;inicio;temas populares;filtrar;filtrar;filtrar datos;filtrar datos;intervalo de fechas
solution: Experience Platform
title: Filtrar datos del catálogo mediante parámetros de consulta
description: La API del servicio de catálogo permite filtrar los datos de respuesta mediante el uso de parámetros de consulta de solicitud. Una de las prácticas recomendadas para Catálogo es utilizar filtros en todas las llamadas a la API, ya que reducen la carga en la API y ayudan a mejorar el rendimiento general.
exl-id: 0cdb5a7e-527b-46be-9ad8-5337c8dc72b7
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '2120'
ht-degree: 2%

---

# Filtro [!DNL Catalog] datos mediante parámetros de consulta

La variable [!DNL Catalog Service] La API permite filtrar los datos de respuesta mediante el uso de parámetros de consulta de solicitud. Parte de las prácticas recomendadas para [!DNL Catalog] es utilizar filtros en todas las llamadas a la API, ya que reducen la carga en la API y ayudan a mejorar el rendimiento general.

Este documento describe los métodos más comunes de filtrado [!DNL Catalog] en la API. Se recomienda hacer referencia a este documento mientras se lee el [Guía para desarrolladores del catálogo](getting-started.md) para obtener más información sobre cómo interactuar con [!DNL Catalog] API. Para obtener información más general, consulte [!DNL Catalog Service], consulte la [[!DNL Catalog] información general](../home.md).

## Limitar objetos devueltos

La variable `limit` El parámetro query limita el número de objetos devueltos en una respuesta. [!DNL Catalog] las respuestas se miden automáticamente según los límites configurados:

* Si `limit` no se ha especificado, el número máximo de objetos por carga útil de respuesta es 20.
* Para consultas de conjuntos de datos, si `observableSchema` se solicita utilizando la variable `properties` parámetro de consulta, el número máximo de conjuntos de datos devueltos es 20.
* El límite global para todas las demás consultas de Catálogo es de 100 objetos.
* No válido `limit` parámetros (incluidos `limit=0`) dan como resultado respuestas de error de 400 niveles que describen los intervalos adecuados.
* Los límites o desplazamientos que se pasan como parámetros de consulta tienen prioridad sobre los que se pasan como encabezados.

**Formato de API**

```http
GET /{OBJECT_TYPE}?limit={LIMIT}
```

| Parámetro | Descripción |
| --- | --- |
| `{OBJECT_TYPE}` | El tipo de [!DNL Catalog] objeto que se va a recuperar. Los objetos válidos son: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{LIMIT}` | Un entero que indica el número de objetos que se van a devolver, que va del 1 al 100. |

**Solicitud**

La siguiente solicitud recupera una lista de conjuntos de datos mientras limita la respuesta a tres objetos.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?limit=3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una lista de conjuntos de datos, limitada al número indicado por la variable `limit` parámetro de consulta.

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

Incluso cuando se filtra el número de objetos devueltos mediante la variable `limit` , los propios objetos devueltos suelen contener más información de la que necesita. Para reducir aún más la carga en el sistema, se recomienda filtrar las respuestas para incluir solo las propiedades que necesite.

La variable `properties` filtros de parámetros de respuesta para devolver solo un conjunto de propiedades especificadas. El parámetro se puede configurar para que devuelva una o varias propiedades.

La variable `properties` solo acepta propiedades de objeto de nivel superior, lo que significa que para el siguiente objeto de ejemplo, puede aplicar filtros para `name`, `description`y `subItem`, pero NO para `sampleKey`.

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

**Formato de API**

```http
GET /{OBJECT_TYPE}?properties={PROPERTY}
GET /{OBJECT_TYPE}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
GET /{OBJECT_TYPE}/{OBJECT_ID}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| Parámetro | Descripción |
| --- | --- |
| `{OBJECT_TYPE}` | El tipo de [!DNL Catalog] objeto que se va a recuperar. Los objetos válidos son: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY}` | Nombre de un atributo que se va a incluir en el cuerpo de la respuesta. |
| `{OBJECT_ID}` | El identificador único de un [!DNL Catalog] objeto que se está recuperando. |

**Solicitud**

La siguiente solicitud recupera una lista de conjuntos de datos. Lista de nombres de propiedades separados por comas que se proporciona en la sección `properties` indica las propiedades que se van a devolver en la respuesta. A `limit` también se incluye, lo que limita el número de conjuntos de datos devueltos. Si la solicitud no incluía un `limit` , la respuesta contendría un máximo de 20 objetos.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=4&properties=name,schemaRef' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

En función de la respuesta anterior, se puede inferir lo siguiente:

* Si a un objeto le faltan propiedades solicitadas, solo se mostrarán las propiedades solicitadas que incluye. (`Dataset1`)
* Si un objeto no incluye ninguna de las propiedades solicitadas, aparecerá como objeto vacío. (`Dataset2`)
* Un conjunto de datos puede devolver una propiedad solicitada como un objeto vacío si contiene la propiedad pero no hay ningún valor. (`Dataset3`)
* De lo contrario, el conjunto de datos mostrará el valor completo de todas las propiedades solicitadas. (`Dataset4`)

>[!NOTE]
>
>En el `schemaRef` para cada conjunto de datos, el número de versión indica la última versión secundaria del esquema. Consulte la sección sobre [versiones de esquema](../../xdm/api/getting-started.md#versioning) en la guía de la API XDM para obtener más información.

## Índice inicial de desplazamiento de la lista de respuestas

La variable `start` El parámetro query desplaza la lista de respuestas hacia delante por un número especificado, utilizando la numeración basada en cero. Por ejemplo, `start=2` desplazaría la respuesta para que comience en el tercer objeto de la lista.

Si la variable `start` no está emparejado con un `limit` , el número máximo de objetos devueltos es 20.

**Formato de API**

```http
GET /{OBJECT_TYPE}?start={OFFSET}
```

| Parámetro | Descripción |
| --- | --- |
| `{OBJECT_TYPE}` | Tipo de objeto de catálogo que se va a recuperar. Los objetos válidos son: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OFFSET}` | Un entero que indica el número de objetos por los que se va a desplazar la respuesta. |

**Solicitud**

La siguiente solicitud recupera una lista de conjuntos de datos, lo que se contrasta con el quinto objeto (`start=4`) y limitando la respuesta a dos conjuntos de datos devueltos (`limit=2`).

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?start=4&limit=2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

La respuesta incluye un objeto JSON que contiene dos elementos de nivel superior (`limit=2`), uno para cada conjunto de datos y sus detalles (los detalles se han resumido en el ejemplo). La respuesta se cambia por cuatro (`start=4`), lo que significa que los conjuntos de datos mostrados son los números cinco y seis cronológicamente.

```json
{
    "Dataset5": {},
    "Dataset6": {}
}
```

## Filtrar por etiqueta

Algunos objetos Catálogo admiten el uso de un `tags` atributo. Las etiquetas pueden adjuntar información a un objeto y luego utilizarse más adelante para recuperarlo. La elección de las etiquetas que se deben utilizar y cómo aplicarlas depende de los procesos de organización.

Hay algunas limitaciones que hay que tener en cuenta al utilizar etiquetas:

* Los únicos objetos de catálogo que admiten etiquetas actualmente son conjuntos de datos, lotes y conexiones.
* Los nombres de las etiquetas son exclusivos de su organización.
* Los procesos de Adobe pueden aprovechar las etiquetas para ciertos comportamientos. A los nombres de estas etiquetas se les agregará el prefijo &quot;adobe&quot; como estándar. Por lo tanto, debe evitar esta convención al declarar nombres de etiquetas.
* Los siguientes nombres de etiquetas están reservados para su uso en [!DNL Experience Platform]y, por lo tanto, no se pueden declarar como nombre de etiqueta para su organización:
   * `unifiedProfile`: Este nombre de etiqueta está reservado para los conjuntos de datos que ingerirá [[!DNL Real-Time Customer Profile]](../../profile/home.md).
   * `unifiedIdentity`: Este nombre de etiqueta está reservado para los conjuntos de datos que ingerirá [[!DNL Identity Service]](../../identity-service/home.md).

A continuación se muestra un ejemplo de un conjunto de datos que contiene un `tags` propiedad. Las etiquetas de esa propiedad toman la forma de pares clave-valor, y cada valor de etiqueta aparece como una matriz que contiene una sola cadena:

```json
{
    "5be1f2ecc73c1714ceba66e2": {
        "imsOrg": "{ORG_ID}",
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

**Formato de API**

Valores de la variable `tags` toma la forma de pares clave-valor, utilizando el formato `{TAG_NAME}:{TAG_VALUE}`. Se pueden proporcionar varios pares de clave-valor en forma de lista separada por comas. Cuando se proporcionan varias etiquetas, se asume una relación AND.

El parámetro admite caracteres comodín (`*`) para valores de etiqueta. Por ejemplo, una cadena de búsqueda de `test*` devuelve cualquier objeto donde el valor de la etiqueta comience por &quot;test&quot;. Una cadena de búsqueda que consiste únicamente en un comodín puede utilizarse para filtrar objetos en función de si contienen o no una etiqueta específica, independientemente de su valor.

```http
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}
GET /{OBJECT_TYPE}?tags={TAG_NAME_1}:{TAG_VALUE_1},{TAG_NAME_2}:{TAG_VALUE_2}
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}*
GET /{OBJECT_TYPE}?tags={TAG_NAME}:*
```

| Parámetro | Descripción |
| --- | --- |
| `{OBJECT_TYPE}` | El tipo de [!DNL Catalog] objeto que se va a recuperar. Los objetos válidos son: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li></ul> |
| `{TAG_NAME}` | Nombre de la etiqueta por la que se va a filtrar. |
| `{TAG_VALUE}` | El valor de la etiqueta por la que filtrar. Admite caracteres comodín (`*`). |

**Solicitud**

La siguiente solicitud recupera una lista de conjuntos de datos, filtrando por una etiqueta que tiene un valor específico Y la segunda etiqueta que está presente.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?tags=sampleTag:123456,secondTag:* \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una lista de conjuntos de datos que contienen `sampleTag` con un valor de &quot;123456&quot;, AND `secondTag` con cualquier valor. A menos que también se especifique un límite, la respuesta contiene un máximo de 20 objetos.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{ORG_ID}",
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
            "imsOrg": "{ORG_ID}",
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

Algunos extremos de la variable [!DNL Catalog] La API tiene parámetros de consulta que permiten consultas de rango, generalmente en el caso de fechas.

**Formato de API**

```http
GET /batches?createdAfter={TIMESTAMP_1}&createdBefore={TIMESTAMP_2}
```

| Parámetro | Descripción |
| --- | --- |
| `{TIMESTAMP }` | Un entero datetime en Unix Epoch. |

**Solicitud**

La siguiente solicitud recupera una lista de lotes creados durante el mes de abril de 2019.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/batches?createdAfter=1554076800000&createdBefore=1556668799000' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta contiene una lista de [!DNL Catalog] objetos que se encuentran dentro del intervalo de fechas especificado. A menos que también se especifique un límite, la respuesta contiene un máximo de 20 objetos.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{ORG_ID}",
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
            "imsOrg": "{ORG_ID}",
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

La variable `orderBy` el parámetro de consulta le permite ordenar los datos de respuesta en función de un valor de propiedad especificado. Este parámetro requiere una &quot;dirección&quot; (`asc` para ascendente o `desc` para descender), seguido de dos puntos (`:`) y, a continuación, una propiedad para ordenar los resultados por. Si no se especifica una dirección, la dirección predeterminada es ascendente.

Se pueden proporcionar varias propiedades de ordenación en una lista separada por comas. Si la primera propiedad de ordenación produce varios objetos que contienen el mismo valor para esa propiedad, se utilizará la segunda propiedad de ordenación para ordenar aún más los objetos coincidentes.

Por ejemplo, considere la siguiente consulta: `orderBy=name,desc:created`. Los resultados se ordenan en orden ascendente según la primera propiedad de clasificación, `name`. En casos en los que varios registros comparten lo mismo `name` , los registros coincidentes se ordenan por la segunda propiedad de clasificación, `created`. Si ningún registro devuelto comparte lo mismo `name`, el `created` no tiene en cuenta el orden.


**Formato de API**

```http
GET /{OBJECT_TYPE}?orderBy=asc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy=desc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy={PROPERTY_NAME_1},desc:{PROPERTY_NAME_2}
```

| Parámetro | Descripción |
| --- | --- |
| `{OBJECT_TYPE}` | Tipo de objeto de catálogo que se va a recuperar. Los objetos válidos son: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY_NAME}` | Nombre de una propiedad por la que ordenar los resultados. |

**Solicitud**

La siguiente solicitud recupera una lista de conjuntos de datos ordenados por sus `name` propiedad. Si algún conjunto de datos comparte lo mismo `name`, estos conjuntos de datos, a su vez, se ordenarán por sus `updated` en orden descendente.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?orderBy=name,desc:updated' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta contiene una lista de [!DNL Catalog] objetos que están ordenados según la variable `orderBy` parámetro. A menos que también se especifique un límite, la respuesta contiene un máximo de 20 objetos.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{ORG_ID}",
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
            "imsOrg": "{ORG_ID}",
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
            "imsOrg": "{ORG_ID}",
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

[!DNL Catalog] proporciona dos métodos de filtrado por propiedad, que se describen en las secciones siguientes:

* [Uso de filtros simples](#using-simple-filters): Filtre por si una propiedad específica coincide con un valor específico.
* [Uso del parámetro de propiedad](#using-the-property-parameter): Utilice expresiones condicionales para filtrar en función de si existe una propiedad o si el valor de una propiedad coincide, se aproxima o compara con otro valor especificado o expresión regular.

### Uso de filtros simples {#using-simple-filters}

Los filtros simples le permiten filtrar respuestas en función de valores de propiedad específicos. Un filtro simple adopta la forma de `{PROPERTY_NAME}={VALUE}`.

Por ejemplo, la consulta `name=exampleName` solo devuelve objetos cuyos `name` contiene un valor de &quot;exampleName&quot;. Por el contrario, la consulta `name=!exampleName` solo devuelve objetos cuyos `name` la propiedad es **not** &quot;exampleName&quot;.

Además, los filtros simples admiten la capacidad de realizar consultas de varios valores para una sola propiedad. Cuando se proporcionan varios valores, la respuesta devuelve objetos cuya propiedad coincide con **any** de los valores de la lista proporcionada. Puede invertir una consulta de varios valores marcando como prefijo una `!` carácter a la lista, devolviendo solo objetos cuyo valor de propiedad sea **not** en la lista proporcionada (por ejemplo, `name=!exampleName,anotherName`).

**Formato de API**

```http
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE_1},{VALUE_2},{VALUE_3}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE_1},{VALUE_2},{VALUE_3}
```

| Parámetro | Descripción |
| --- | --- |
| `{OBJECT_TYPE}` | El tipo de [!DNL Catalog] objeto que se va a recuperar. Los objetos válidos son: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY_NAME}` | Nombre de la propiedad cuyo valor desea filtrar. |
| `{VALUE}` | Un valor de propiedad que determina qué resultados se incluirán (o excluirán, según la consulta). |

**Solicitud**

La siguiente solicitud recupera una lista de conjuntos de datos, filtrados para incluir solo conjuntos de datos cuya `name` tiene el valor &quot;exampleName&quot; u &quot;otherName&quot;.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?name=exampleName,anotherName' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta contiene una lista de conjuntos de datos, excluyendo cualquier conjunto de datos cuyo `name` es &quot;exampleName&quot; u &quot;otherName&quot;. A menos que también se especifique un límite, la respuesta contiene un máximo de 20 objetos.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{ORG_ID}",
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
            "imsOrg": "{ORG_ID}",
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

### Al usar la variable `property` parameter {#using-the-property-parameter}

La variable `property` El parámetro query proporciona más flexibilidad para el filtrado basado en propiedades que los filtros simples. Además de filtrar en función de si una propiedad tiene un valor específico, la variable `property` puede utilizar otros operadores de comparación (como &quot;more-than&quot; (`>`) y &quot;menor que&quot; (`<`)), así como expresiones regulares para filtrar por valores de propiedad. También puede filtrar por si existe o no una propiedad, independientemente de su valor.

La variable `property` solo acepta propiedades de objeto de nivel superior, lo que significa que para el siguiente objeto de ejemplo, puede filtrar por propiedad para `name`, `description`y `subItem`, pero NO para `sampleKey`.

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

**Formato de API**

```http
GET /{OBJECT_TYPE}?property={CONDITION}
```

| Parámetro | Descripción |
| --- | --- |
| `{OBJECT_TYPE}` | El tipo de [!DNL Catalog] objeto que se va a recuperar. Los objetos válidos son: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{CONDITION}` | Expresión condicional que indica qué propiedad se va a consultar y cómo se va a evaluar su valor. A continuación se proporcionan ejemplos. |

El valor de la variable `property` admite varios tipos diferentes de expresiones condicionales. La siguiente tabla describe la sintaxis básica de las expresiones admitidas:

| Símbolo(s) | Descripción | Ejemplo |
| --- | --- | --- |
| (Ninguna) | Al establecer el nombre de la propiedad sin operador, solo se devuelven objetos donde exista la propiedad, independientemente de su valor. | `property=name` |
| ! | Prefijando un &quot;`!`&quot; al valor de un `property` El parámetro solo devuelve objetos en los que la propiedad **not** existe. | `property=!name` |
| ~ | Devuelve solo los objetos cuyos valores de propiedad (cadena) coinciden con una expresión regular proporcionada después de la tilde (`~`). | `property=name~^example` |
| == | Devuelve solo los objetos cuyos valores de propiedad coincidan exactamente con la cadena proporcionada después del símbolo doble igual (`==`). | `property=name==exampleName` |
| != | Devuelve solo objetos cuyos valores de propiedad **not** cadena de coincidencia proporcionada después del símbolo not-equals (`!=`). | `property=name!=exampleName` |
| &lt; | Devuelve solo los objetos cuyos valores de propiedad sean inferiores (pero no iguales) a una cantidad declarada. | `property=version<1.0.0` |
| &lt;= | Devuelve solo los objetos cuyos valores de propiedad sean inferiores (o iguales) a una cantidad declarada. | `property=version<=1.0.0` |
| > | Devuelve solo los objetos cuyos valores de propiedad sean buenos (pero no iguales a) una cantidad declarada. | `property=version>1.0.0` |
| >= | Devuelve solo los objetos cuyos valores de propiedad sean buenos (o iguales a) una cantidad declarada. | `property=version>=1.0.0` |

>[!NOTE]
>
>La variable `name` admite el uso de un comodín `*`, ya sea como cadena de búsqueda completa o como parte de ella. Los caracteres comodín coinciden con caracteres vacíos, por lo que la cadena de búsqueda `te*st` coincidirá con el valor &quot;test&quot;. Los Asteriscos se escapan duplicándolos (`**`). Un asterisco doble en una cadena de búsqueda representa un solo asterisco como una cadena literal.

**Solicitud**

La siguiente solicitud devolverá cualquier conjunto de datos con un número de versión bueno a la 1.0.3.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?property=version>1.0.3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta contiene una lista de conjuntos de datos cuyos números de versión son buenos a 1.0.3. A menos que también se especifique un límite, la respuesta contiene un máximo de 20 objetos.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.1.2",
            "imsOrg": "{ORG_ID}",
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
            "imsOrg": "{ORG_ID}",
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
            "imsOrg": "{ORG_ID}",
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

## Combinación de varios filtros

Uso de un símbolo &amp; (`&`), puede combinar varios filtros en una sola solicitud. Cuando se agregan condiciones adicionales a una solicitud, se asume una relación AND.

**Formato de API**

```http
GET /{OBJECT_TYPE}?{FILTER_1}={VALUE}&{FILTER_2}={VALUE}&{FILTER_3}={VALUE}
```
