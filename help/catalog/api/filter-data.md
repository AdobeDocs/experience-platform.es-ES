---
keywords: Experience Platform;inicio;temas populares;filtrar;filtrar;filtrar datos;filtrar datos;filtrar datos;intervalo de fechas
solution: Experience Platform
title: Filtrado de datos de catálogo mediante parámetros de consulta
description: La API del servicio de catálogo permite filtrar los datos de respuesta mediante el uso de parámetros de consulta de solicitud. Parte de las prácticas recomendadas para Catálogo es utilizar filtros en todas las llamadas a la API, ya que reducen la carga en la API y ayudan a mejorar el rendimiento general.
exl-id: 0cdb5a7e-527b-46be-9ad8-5337c8dc72b7
source-git-commit: 75099d39fbdb9488105a9254bbbcca9b12349238
workflow-type: tm+mt
source-wordcount: '2117'
ht-degree: 2%

---

# Filtrar datos de [!DNL Catalog] mediante parámetros de consulta

La API [!DNL Catalog Service] permite filtrar los datos de respuesta mediante el uso de parámetros de consulta de solicitud. Parte de las prácticas recomendadas para [!DNL Catalog] es utilizar filtros en todas las llamadas a la API, ya que reducen la carga en la API y ayudan a mejorar el rendimiento general.

Este documento describe los métodos más comunes para filtrar objetos [!DNL Catalog] en la API. Se recomienda hacer referencia a este documento mientras se lee la [Guía para desarrolladores de catálogos](getting-started.md) para obtener más información acerca de cómo interactuar con la API [!DNL Catalog]. Para obtener más información general sobre [!DNL Catalog Service], vea la [[!DNL Catalog] descripción general](../home.md).

## Límite de objetos devueltos

El parámetro de consulta `limit` restringe el número de objetos devueltos en una respuesta. [!DNL Catalog] respuestas se miden automáticamente de acuerdo con los límites configurados:

* Si no se especifica un parámetro `limit`, el número máximo de objetos por carga de respuesta es 20.
* Para las consultas de conjuntos de datos, si se solicita `observableSchema` mediante el parámetro de consulta `properties`, el número máximo de conjuntos de datos devueltos es 20.
* El límite global para todas las demás consultas de catálogo es de 100 objetos.
* Los parámetros `limit` no válidos (incluido `limit=0`) dan como resultado respuestas de error de 400 niveles que describen los intervalos adecuados.
* Los límites o desplazamientos que se pasan como parámetros de consulta tienen prioridad sobre los que se pasan como encabezados.

**Formato de API**

```http
GET /{OBJECT_TYPE}?limit={LIMIT}
```

| Parámetro | Descripción |
| --- | --- |
| `{OBJECT_TYPE}` | Tipo de objeto [!DNL Catalog] que se va a recuperar. Los objetos válidos son: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{LIMIT}` | Un entero que indica el número de objetos que se van a devolver, entre 1 y 100. |

**Solicitud**

La siguiente solicitud recupera una lista de conjuntos de datos y limita la respuesta a tres objetos.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?limit=3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una lista de conjuntos de datos, limitados al número indicado por el parámetro de consulta `limit`.

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset 1",
        "description": "Description of dataset.",
        "files": "@/dataSetFiles?dataSetId=5ba9452f7de80400007fc52a"
    },
    "5bb276b03a14440000971552": {
        "name": "Sample Dataset 2",
        "description": "Description of dataset.",
        "files": "@/dataSetFiles?dataSetId=5bb276b03a14440000971552"
    },
    "5bceaa4c26c115000039b24b": {
        "name": "Sample Dataset 3"
    }
}
```

## Limitar propiedades mostradas

Incluso cuando se filtra el número de objetos devueltos mediante el parámetro `limit`, los propios objetos devueltos pueden contener con frecuencia más información de la que realmente necesita. Para reducir aún más la carga en el sistema, se recomienda filtrar las respuestas para incluir solo las propiedades que necesite.

El parámetro `properties` filtra los objetos de respuesta para devolver solamente un conjunto de propiedades especificadas. El parámetro se puede establecer para que devuelva una o varias propiedades.

El parámetro `properties` puede aceptar cualquier propiedad de objeto de nivel. `sampleKey` se puede extraer usando `?properties=subItem.sampleKey`.

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
| `{OBJECT_TYPE}` | Tipo de objeto [!DNL Catalog] que se va a recuperar. Los objetos válidos son: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{PROPERTY}` | Nombre de un atributo que se va a incluir en el cuerpo de la respuesta. |
| `{OBJECT_ID}` | El identificador único de un objeto [!DNL Catalog] específico que se está recuperando. |

**Solicitud**

La siguiente solicitud recupera una lista de conjuntos de datos. La lista separada por comas de los nombres de propiedad proporcionados en el parámetro `properties` indica las propiedades que se van a devolver en la respuesta. También se incluye un parámetro `limit`, que limita el número de conjuntos de datos devueltos. Si la solicitud no incluía un parámetro `limit`, la respuesta contendría un máximo de 20 objetos.

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

Sobre la base de la respuesta anterior, se puede inferir lo siguiente:

* Si a un objeto le faltan propiedades solicitadas, solo se mostrarán las propiedades solicitadas que sí incluye. (`Dataset1`)
* Si un objeto no incluye ninguna de las propiedades solicitadas, aparecerá como un objeto vacío. (`Dataset2`)
* Un conjunto de datos puede devolver una propiedad solicitada como un objeto vacío si contiene la propiedad pero no hay ningún valor. (`Dataset3`)
* De lo contrario, el conjunto de datos mostrará el valor completo de todas las propiedades solicitadas. (`Dataset4`)

>[!NOTE]
>
>En la propiedad `schemaRef` para cada conjunto de datos, el número de versión indica la última versión secundaria del esquema. Consulte la sección sobre [versiones de esquema](../../xdm/api/getting-started.md#versioning) en la guía de API de XDM para obtener más información.

## Desplazamiento del índice inicial de la lista de respuestas

El parámetro de consulta `start` desplaza la lista de respuestas un número especificado, utilizando la numeración basada en cero. Por ejemplo, `start=2` desplazaría la respuesta para comenzar en el tercer objeto de la lista.

Si el parámetro `start` no está emparejado con un parámetro `limit`, el número máximo de objetos devueltos es 20.

**Formato de API**

```http
GET /{OBJECT_TYPE}?start={OFFSET}
```

| Parámetro | Descripción |
| --- | --- |
| `{OBJECT_TYPE}` | Tipo de objeto Catalog que se va a recuperar. Los objetos válidos son: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OFFSET}` | Un entero que indica el número de objetos por los que se desplaza la respuesta. |

**Solicitud**

La siguiente solicitud recupera una lista de conjuntos de datos, desplazándose al quinto objeto (`start=4`) y limitando la respuesta a dos conjuntos de datos devueltos (`limit=2`).

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?start=4&limit=2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

La respuesta incluye un objeto JSON que contiene dos elementos de nivel superior (`limit=2`), uno para cada conjunto de datos y sus detalles (los detalles se han resumido en el ejemplo). La respuesta se desplaza en cuatro (`start=4`), lo que significa que los conjuntos de datos mostrados son el número cinco y seis cronológicamente.

```json
{
    "Dataset5": {},
    "Dataset6": {}
}
```

## Filtrar por etiqueta

Algunos objetos Catalog admiten el uso de un atributo `tags`. Las etiquetas pueden adjuntar información a un objeto y utilizarla más adelante para recuperarlo. La elección de las etiquetas que se van a utilizar y cómo aplicarlas depende de los procesos de organización.

Hay algunas limitaciones que se deben tener en cuenta al utilizar etiquetas:

* Los únicos objetos de catálogo que actualmente admiten etiquetas son conjuntos de datos, lotes y conexiones.
* Los nombres de las etiquetas son únicos para su organización.
* Los procesos de Adobe pueden aprovechar las etiquetas para determinados comportamientos. El prefijo de los nombres de estas etiquetas es &quot;adobe&quot; como estándar. Por lo tanto, debe evitar esta convención al declarar nombres de etiquetas.
* Los siguientes nombres de etiquetas están reservados para su uso en [!DNL Experience Platform] y, por lo tanto, no se pueden declarar como un nombre de etiqueta para su organización:
   * `unifiedProfile`: este nombre de etiqueta está reservado para conjuntos de datos que [[!DNL Real-Time Customer Profile]](../../profile/home.md) va a ingerir.
   * `unifiedIdentity`: este nombre de etiqueta está reservado para conjuntos de datos que [[!DNL Identity Service]](../../identity-service/home.md) va a ingerir.

A continuación se muestra un ejemplo de un conjunto de datos que contiene una propiedad `tags`. Las etiquetas dentro de esa propiedad toman la forma de pares clave-valor, y cada valor de etiqueta aparece como una matriz que contiene una sola cadena:

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

Los valores del parámetro `tags` toman la forma de pares clave-valor, con el formato `{TAG_NAME}:{TAG_VALUE}`. Se pueden proporcionar varios pares de clave-valor en forma de lista separada por comas. Cuando se proporcionan varias etiquetas, se asume una relación AND.

El parámetro admite caracteres comodín (`*`) para los valores de etiqueta. Por ejemplo, una cadena de búsqueda de `test*` devuelve cualquier objeto donde el valor de la etiqueta comience por &quot;test&quot;. Se puede utilizar una cadena de búsqueda formada únicamente por un comodín para filtrar objetos en función de si contienen o no una etiqueta específica, independientemente de su valor.

```http
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}
GET /{OBJECT_TYPE}?tags={TAG_NAME_1}:{TAG_VALUE_1},{TAG_NAME_2}:{TAG_VALUE_2}
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}*
GET /{OBJECT_TYPE}?tags={TAG_NAME}:*
```

| Parámetro | Descripción |
| --- | --- |
| `{OBJECT_TYPE}` | Tipo de objeto [!DNL Catalog] que se va a recuperar. Los objetos válidos son: <ul><li>`batches`</li><li>`dataSets`</li></ul> |
| `{TAG_NAME}` | Nombre de la etiqueta por la que filtrar. |
| `{TAG_VALUE}` | El valor de la etiqueta por el que filtrar. Admite caracteres comodín (`*`). |

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

Una respuesta correcta devuelve una lista de conjuntos de datos que contienen `sampleTag` con el valor &quot;123456&quot; Y `secondTag` con cualquier valor. A menos que también se especifique un límite, la respuesta contiene un máximo de 20 objetos.

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
    }
}
```

## Filtrar por intervalo de fechas

Algunos extremos de la API [!DNL Catalog] tienen parámetros de consulta que permiten consultas de intervalo, la mayoría de las veces en el caso de las fechas.

**Formato de API**

```http
GET /batches?createdAfter={TIMESTAMP_1}&createdBefore={TIMESTAMP_2}
```

| Parámetro | Descripción |
| --- | --- |
| `{TIMESTAMP }` | Un entero de fecha y hora en Tiempo Unix Epoch. |

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
    }
}
```

## Ordenar por propiedad

El parámetro de consulta `orderBy` le permite ordenar los datos de respuesta en función de un valor de propiedad especificado. Este parámetro requiere una &quot;dirección&quot; (`asc` para ascendente o `desc` para descendente), seguida de dos puntos (`:`) y, a continuación, una propiedad por la que ordenar los resultados. Si no se especifica una dirección, la dirección predeterminada es ascendente.

Se pueden proporcionar varias propiedades de ordenación en una lista separada por comas. Si la primera propiedad de ordenación produce varios objetos que contienen el mismo valor para esa propiedad, la segunda propiedad de ordenación se utiliza para ordenar aún más esos objetos coincidentes.

Por ejemplo, considere la siguiente consulta: `orderBy=name,desc:created`. Los resultados se ordenan en orden ascendente según la primera propiedad de ordenación, `name`. En los casos en que varios registros comparten la misma propiedad `name`, esos registros coincidentes se ordenan por la segunda propiedad de ordenación, `created`. Si ningún registro devuelto comparte el mismo(a) `name`, la propiedad `created` no se tiene en cuenta en la ordenación.


**Formato de API**

```http
GET /{OBJECT_TYPE}?orderBy=asc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy=desc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy={PROPERTY_NAME_1},desc:{PROPERTY_NAME_2}
```

| Parámetro | Descripción |
| --- | --- |
| `{OBJECT_TYPE}` | Tipo de objeto Catalog que se va a recuperar. Los objetos válidos son: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{PROPERTY_NAME}` | Nombre de una propiedad por la que ordenar los resultados. |

**Solicitud**

La siguiente solicitud recupera una lista de conjuntos de datos ordenados por su propiedad `name`. Si algún conjunto de datos comparte el mismo(a) `name`, esos conjuntos de datos a su vez se ordenarán por su propiedad `updated` en orden descendente.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?orderBy=name,desc:updated' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta contiene una lista de [!DNL Catalog] objetos que se ordenan según el parámetro `orderBy`. A menos que también se especifique un límite, la respuesta contiene un máximo de 20 objetos.

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
    }
}
```

## Filtrar por propiedad

[!DNL Catalog] proporciona dos métodos de filtrado por propiedad, que se describen con más detalle en las secciones siguientes:

* [Uso de filtros simples](#using-simple-filters): filtre por si una propiedad específica coincide con un valor específico.
* [Uso del parámetro de propiedad](#using-the-property-parameter): utilice expresiones condicionales para filtrar basándose en si existe una propiedad o si el valor de una propiedad coincide, se aproxima o se compara con otro valor especificado o expresión regular.

### Uso de filtros simples {#using-simple-filters}

Los filtros simples le permiten filtrar las respuestas en función de valores de propiedad específicos. Un filtro simple adopta la forma de `{PROPERTY_NAME}={VALUE}`.

Por ejemplo, la consulta `name=exampleName` devuelve únicamente objetos cuya propiedad `name` contiene el valor &quot;exampleName&quot;. Por el contrario, la consulta `name=!exampleName` devuelve solamente objetos cuya propiedad `name` sea **no** &quot;exampleName&quot;.

Además, los filtros simples admiten la capacidad de consultar varios valores para una sola propiedad. Cuando se proporcionan varios valores, la respuesta devuelve objetos cuya propiedad coincide con **cualquiera** de los valores de la lista proporcionada. Puede invertir una consulta de varios valores prefiriendo un carácter `!` a la lista y devolviendo únicamente objetos cuyo valor de propiedad sea **no** en la lista proporcionada (por ejemplo, `name=!exampleName,anotherName`).

**Formato de API**

```http
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE_1},{VALUE_2},{VALUE_3}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE_1},{VALUE_2},{VALUE_3}
```

| Parámetro | Descripción |
| --- | --- |
| `{OBJECT_TYPE}` | Tipo de objeto [!DNL Catalog] que se va a recuperar. Los objetos válidos son: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{PROPERTY_NAME}` | Nombre de la propiedad por cuyo valor desea filtrar. |
| `{VALUE}` | Valor de propiedad que determina qué resultados se incluyen (o excluyen, según la consulta). |

**Solicitud**

La siguiente solicitud recupera una lista de conjuntos de datos, filtrados para incluir solo conjuntos de datos cuya propiedad `name` tiene el valor &quot;exampleName&quot; u &quot;anotherName&quot;.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?name=exampleName,anotherName' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta contiene una lista de conjuntos de datos, que excluye cualquier conjunto de datos cuyo `name` sea &quot;exampleName&quot; u &quot;anotherName&quot;. A menos que también se especifique un límite, la respuesta contiene un máximo de 20 objetos.

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
    }
}
```

### Usando el parámetro `property` {#using-the-property-parameter}

El parámetro de consulta `property` proporciona más flexibilidad para el filtrado basado en propiedades que los filtros simples. Además del filtrado basado en si una propiedad tiene un valor específico, el parámetro `property` puede utilizar otros operadores de comparación (como &quot;más que&quot; (`>`) y &quot;menos que&quot; (`<`)), así como expresiones regulares para filtrar por valores de propiedad. También puede filtrar por si existe o no una propiedad, independientemente de su valor.

El parámetro `property` puede aceptar cualquier propiedad de objeto de nivel. `sampleKey` se puede usar para filtrar con `?properties=subItem.sampleKey`.

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
| `{OBJECT_TYPE}` | Tipo de objeto [!DNL Catalog] que se va a recuperar. Los objetos válidos son: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{CONDITION}` | Expresión condicional que indica qué propiedad se va a consultar y cómo se va a evaluar su valor. A continuación se proporcionan ejemplos. |

El valor del parámetro `property` admite varios tipos diferentes de expresiones condicionales. En la tabla siguiente se describe la sintaxis básica de las expresiones admitidas:

| Símbolo(s) | Descripción | Ejemplo |
| --- | --- | --- |
| (Ninguno) | Si se indica el nombre de la propiedad sin operador, solo se devuelven objetos donde exista la propiedad, independientemente de su valor. | `property=name` |
| ! | Si se antepone un &quot;`!`&quot; al valor de un parámetro `property`, solo se devuelven objetos en los que la propiedad **no existe**. | `property=!name` |
| ~ | Devuelve solo objetos cuyos valores de propiedad (cadena) coinciden con una expresión regular proporcionada después del símbolo de tilde (`~`). | `property=name~^example` |
| == | Devuelve únicamente objetos cuyos valores de propiedad coinciden exactamente con la cadena proporcionada después del símbolo doble igual (`==`). | `property=name==exampleName` |
| != | Devuelve solo objetos cuyos valores de propiedad **no** coinciden con la cadena proporcionada después del símbolo no igual a (`!=`). | `property=name!=exampleName` |
| &lt; | Devuelve solo los objetos cuyos valores de propiedad sean menores (pero no iguales) que una cantidad establecida. | `property=version<1.0.0` |
| &lt;= | Devuelve solo objetos cuyos valores de propiedad sean menores (o iguales) que una cantidad establecida. | `property=version<=1.0.0` |
| > | Devuelve solo objetos cuyos valores de propiedad sean mayores (pero no iguales) que una cantidad establecida. | `property=version>1.0.0` |
| >= | Devuelve solo objetos cuyos valores de propiedad sean mayores (o iguales) que una cantidad establecida. | `property=version>=1.0.0` |

>[!NOTE]
>
>La propiedad `name` admite el uso de un comodín `*`, ya sea como toda la cadena de búsqueda o como parte de ella. Los caracteres comodín coinciden con caracteres vacíos, de modo que la cadena de búsqueda `te*st` coincidirá con el valor &quot;test&quot;. Los asteriscos se evitan duplicándolos (`**`). Un doble asterisco en una cadena de búsqueda representa un solo asterisco como cadena literal.

**Solicitud**

La siguiente solicitud devolverá cualquier conjunto de datos con un número de versión mayor que 1.0.3.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?property=version>1.0.3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta contiene una lista de conjuntos de datos cuyos números de versión son superiores a 1.0.3. A menos que también se especifique un límite, la respuesta contiene un máximo de 20 objetos.

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
    }
}
```

## Combinación de varios filtros

Con un signo &amp; (`&`), puede combinar varios filtros en una única solicitud. Cuando se añaden condiciones adicionales a una solicitud, se asume una relación AND.

**Formato de API**

```http
GET /{OBJECT_TYPE}?{FILTER_1}={VALUE}&{FILTER_2}={VALUE}&{FILTER_3}={VALUE}
```
