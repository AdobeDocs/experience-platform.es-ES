---
title: Clasificación y filtrado de respuestas en la API de servicio de flujo
description: Este tutorial trata la sintaxis para ordenar y filtrar mediante parámetros de consulta en la API de servicio de flujo, incluidos algunos casos de uso avanzados.
source-git-commit: ccca81357bd7d7083abd3f395aa547c85ebf65fd
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 6%

---

# Clasificación y filtrado de respuestas en la API de servicio de flujo

Al realizar solicitudes de inclusión en listas (GET) en la [API de servicio de flujo](https://www.adobe.io/experience-platform-apis/references/flow-service/), puede utilizar parámetros de consulta para ordenar y filtrar respuestas. Esta guía proporciona una referencia sobre cómo utilizar estos parámetros para diferentes casos de uso.

## Clasificación

Puede ordenar las respuestas utilizando un parámetro de consulta `orderby`. Los siguientes recursos se pueden ordenar en la API:

* [Conexiones](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Connections)
* [Conexiones de origen](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Source-connections)
* [Conexiones de destino](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Target-connections)
* [Flujos](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Flows)
* [Ejecuciones](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Runs)

Para utilizar el parámetro, debe establecer su valor en la propiedad específica por la que desee ordenar (por ejemplo, `?orderby=name`). Puede anteponer el valor con un signo más (`+`) para el orden ascendente o un signo menos (`-`) para el orden descendente. Si no se proporciona ningún prefijo de orden, la lista se ordena en orden ascendente de forma predeterminada.

```http
GET /flows?orderby=name
GET /flows?orderby=-name
```

También puede combinar un parámetro de ordenación con un parámetro de filtrado utilizando un símbolo &quot;and&quot; (`&`).

```http
GET /flows?property=state==enabled&orderby=createdAt
```

## Filtro

Puede filtrar las respuestas utilizando un parámetro `property` con una expresión clave-valor. Por ejemplo, `?property=id==12345` solo devuelve recursos cuya propiedad `id` es exactamente igual a `12345`.

El filtrado se puede aplicar de forma genérica en cualquier propiedad de una entidad siempre que se conozca la ruta válida a dicha propiedad.

>[!NOTE]
>
>Si una propiedad está anidada dentro de un elemento de matriz, debe anexar corchetes (`[]`) a la matriz en la ruta. Consulte la sección sobre [filtrado en propiedades de matriz](#arrays) para ver ejemplos.

**Devuelven todas las conexiones de origen donde el nombre de tabla de origen sea  `lead`:**

```http
GET /sourceConnections?property=params.tableName==lead
```

**Devolver todos los flujos para un ID de segmento específico:**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a
```

### Combinación de filtros

En una consulta se pueden incluir varios filtros `property` siempre que estén separados por caracteres &quot;y&quot; (`&`). Se asume una relación AND al combinar filtros, lo que significa que una entidad debe satisfacer todos los filtros para que se incluya en la respuesta.

**Devolver todos los flujos habilitados para un ID de segmento:**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a&property=state==enabled
```

### Filtrado en propiedades de matriz {#arrays}

Puede filtrar en función de las propiedades de los elementos de las matrices añadiendo `[]` al nombre de la propiedad de matriz.

**Flujos de retorno asociados a conexiones de origen específicas:**

```http
GET /flows?property=sourceConnectionIds[]==9874984,6980696
```

**Flujos de retorno que tienen una transformación que contiene un ID de valor de selector específico:**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a
```

**Devolver conexiones de origen que tienen una columna con un  `name` valor específico:**

```http
GET /sourceConnections?property=params.columns[].name==firstName
```

**Busque el ID de ejecución de flujo para un destino filtrando el ID de segmento:**

```http
GET /runs?property=metrics.recordSummary.targetSummaries[].entitySummaries[].id==segment:068d6e2c-b546-4c73-bfb7-9a9d33375659
```

### `count`

Cualquier consulta de filtrado se puede anexar con el parámetro de consulta `count` con un valor de `true` para devolver el recuento de los resultados. La respuesta de API contiene una propiedad `count` cuyo valor representa el recuento del total de elementos filtrados. Los elementos filtrados reales no se devuelven en esta llamada.

**Devuelve el recuento de los flujos habilitados en el sistema:**

```http
GET /flows?property=state==enabled&count=true
```

La respuesta a la consulta anterior tendría el siguiente aspecto:

```json
{
  "count": 95
}
```

### Propiedades filtrables por recurso

Según la entidad del servicio de flujo que esté recuperando, se pueden utilizar distintas propiedades para el filtrado. Las tablas siguientes desglosan los campos de nivel raíz para cada recurso que normalmente se emplean en los casos de uso de filtrado.

**`connectionSpec`**

| Propiedad | Ejemplo |
| --- | --- |
| `id` | `/connectionSpecs?property=id==736873,9485095` |
| `name` | `/connectionSpecs?property=name==TestConn` |
| `providerId` | `/connectionSpecs?property=providerId==3897933` |
| `attributes.{ATTRIBUTE_NAME}` | `/connectionSpecs?property=attributes.sampleAttribute="abc"` |

{style=&quot;table-layout:auto&quot;}

**`flowSpec`**

| Propiedad | Ejemplo |
| --- | --- |
| `id` | `/flowSpecs?property=id==736873,9485095` |
| `name` | `/flowSpecs?property=name==TestConn` |
| `providerId` | `/flowSpecs?property=providerId==3897933` |

{style=&quot;table-layout:auto&quot;}

**`connection`**

| Propiedad | Ejemplo |
| --- | --- |
| `id` | `/connections?property=id==736873,9485095` |
| `name` | `/connections?property=name==TestConn` |
| `description` | `/connections?property=description==Test%20description` |
| `connectionSpec.id` | `/connections?property=connectionSpec.id==938903,849048` |
| `state` | `/connections?property=state==enabled` |

{style=&quot;table-layout:auto&quot;}

**`sourceConnection`**

| Propiedad | Ejemplo |
| --- | --- |
| `id` | `/sourceConnections?property=id==736873,9485095` |
| `connectionSpec.id` | `/sourceConnections?property=connectionSpec.id==938903,849048` |
| `baseConnectionId` | `/sourceConnections?property=baseConnectionId==983908,4908095` |

{style=&quot;table-layout:auto&quot;}

**`targetConnection`**

| Propiedad | Ejemplo |
| --- | --- |
| `id` | `/targetConnections?property=id==736873,9485095` |
| `connectionSpec.id` | `/targetConnections?property=connectionSpec.id==938903,849048` |
| `baseConnectionId` | `/targetConnections?property=baseConnectionId==983908,4908095` |

{style=&quot;table-layout:auto&quot;}

**`flow`**

| Propiedad | Ejemplo |
| --- | --- |
| `id` | `/flows?property=id==736873,9485095` |
| `name` | `/flows?property=name==TestFlow` |
| `description` | `/flows?property=description==Test%20description` |
| `flowSpec.id` | `/flows?property=flowSpec.id==938903,849048` |
| `state` | `/flows?property=state==enabled` |
| `sourceConnectionIds` | `/flows?property=sourceConnectionIds[]==9874984,6980696` |
| `targetConnectionIds` | `/flows?property=targetConnectionIds[]==598590,690666` |

{style=&quot;table-layout:auto&quot;}

**`run`**

| Propiedad | Ejemplo |
| --- | --- |
| `id` | `/runs?property=id==736873,9485095` |
| `flowId` | `/runs?property=flowId==8749844` |
| `state` | `/runs?property=state==inProgress` |

{style=&quot;table-layout:auto&quot;}

## Pasos siguientes

Esta guía explica cómo utilizar los parámetros de consulta `orderby` y `property` para ordenar y filtrar las respuestas en la API de servicio de flujo. Para obtener guías paso a paso sobre cómo utilizar la API para flujos de trabajo comunes en Platform, consulte los tutoriales de API contenidos en la documentación [sources](../../sources/home.md) y [destinos](../../destinations/home.md) .
