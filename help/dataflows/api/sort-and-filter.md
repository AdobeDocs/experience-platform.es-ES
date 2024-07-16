---
title: Clasificación y filtrado de respuestas en la API de Flow Service
description: Este tutorial cubre la sintaxis para ordenar y filtrar mediante parámetros de consulta en la API de Flow Service, incluidos algunos casos de uso avanzados.
exl-id: 029c3199-946e-4f89-ba7a-dac50cc40c09
source-git-commit: c7ff379b260edeef03f8b47f932ce9040eef3be2
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 2%

---

# Clasificación y filtrado de respuestas en la API de Flow Service

Al realizar solicitudes de listado (GET) en la [API de Flow Service](https://www.adobe.io/experience-platform-apis/references/flow-service/), puede usar parámetros de consulta para ordenar y filtrar las respuestas. Esta guía proporciona una referencia sobre cómo utilizar estos parámetros para diferentes casos de uso.

## Orden

Puede ordenar las respuestas mediante un parámetro de consulta `orderby`. Los siguientes recursos se pueden ordenar en la API:

* [Conexiones](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Connections)
* [Conexiones de Source](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Source-connections)
* [Conexiones de destino](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Target-connections)
* [Flujos](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Flows)
* [Ejecuciones](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Runs)

Para utilizar el parámetro, debe establecer su valor en la propiedad específica por la que desea ordenar (por ejemplo, `?orderby=name`). Puede anteponer el valor con un signo más (`+`) para el orden ascendente o un signo menos (`-`) para el orden descendente. Si no se proporciona ningún prefijo de orden, la lista se ordena en orden ascendente de forma predeterminada.

```http
GET /flows?orderby=name
GET /flows?orderby=-name
```

También puede combinar un parámetro de ordenación con un parámetro de filtrado mediante un símbolo &quot;and&quot; (`&`).

```http
GET /flows?property=state==enabled&orderby=createdAt
```

## Filtrado

Puede filtrar las respuestas utilizando un parámetro `property` con una expresión clave-valor. Por ejemplo, `?property=id==12345` solo devuelve recursos cuya propiedad `id` sea igual exactamente a `12345`.

El filtrado se puede aplicar genéricamente en cualquier propiedad de una entidad siempre y cuando se conozca la ruta válida a esa propiedad.

>[!NOTE]
>
>Si una propiedad está anidada en un elemento de matriz, debe agregar corchetes (`[]`) a la matriz en la ruta de acceso. Consulte la sección sobre [filtrado en propiedades de matriz](#arrays) para ver ejemplos.

**Devuelve todas las conexiones de origen donde el nombre de la tabla de origen es `lead`:**

```http
GET /sourceConnections?property=params.tableName==lead
```

**Devolver todos los flujos para un Id. de segmento específico:**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a
```

### Combinación de filtros

Se pueden incluir varios filtros `property` en una consulta siempre que estén separados por caracteres &quot;y&quot; (`&`). Se asume una relación AND al combinar filtros, lo que significa que una entidad debe satisfacer todos los filtros para que se incluya en la respuesta.

**Devuelve todos los flujos habilitados para un ID de segmento:**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a&property=state==enabled
```

### Filtrado en propiedades de matriz {#arrays}

Puede filtrar según las propiedades de los elementos de las matrices adjuntando `[]` al nombre de la propiedad de matriz.

**Devolver flujos asociados con conexiones de origen específicas:**

```http
GET /flows?property=sourceConnectionIds[]==9874984,6980696
```

**Devolver flujos que tienen una transformación que contiene un identificador de valor de selector específico:**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a
```

**Devolver conexiones de origen que tienen una columna con un valor `name` específico:**

```http
GET /sourceConnections?property=params.columns[].name==firstName
```

**Busque el identificador de ejecución de flujo para un destino filtrando el identificador de segmento:**

```http
GET /runs?property=metrics.recordSummary.targetSummaries[].entitySummaries[].id==segment:068d6e2c-b546-4c73-bfb7-9a9d33375659
```

### `count`

Cualquier consulta de filtrado se puede anexar con `count` parámetro de consulta con un valor de `true` para devolver el recuento de los resultados. La respuesta de la API contiene una propiedad `count` cuyo valor representa el recuento total de elementos filtrados. Los elementos filtrados reales no se devuelven en esta llamada.

**Devuelve el recuento de flujos habilitados en el sistema:**

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

Según la entidad de Flow Service que esté recuperando, se pueden utilizar distintas propiedades para el filtrado. En las tablas siguientes se desglosan los campos de nivel raíz de cada recurso que se emplean comúnmente en los casos de uso de filtrado.

**`connectionSpec`**

| Propiedad | Ejemplo |
| --- | --- |
| `id` | `/connectionSpecs?property=id==736873,9485095` |
| `name` | `/connectionSpecs?property=name==TestConn` |
| `providerId` | `/connectionSpecs?property=providerId==3897933` |
| `attributes.{ATTRIBUTE_NAME}` | `/connectionSpecs?property=attributes.sampleAttribute="abc"` |

{style="table-layout:auto"}

**`flowSpec`**

| Propiedad | Ejemplo |
| --- | --- |
| `id` | `/flowSpecs?property=id==736873,9485095` |
| `name` | `/flowSpecs?property=name==TestConn` |
| `providerId` | `/flowSpecs?property=providerId==3897933` |

{style="table-layout:auto"}

**`connection`**

| Propiedad | Ejemplo |
| --- | --- |
| `id` | `/connections?property=id==736873,9485095` |
| `name` | `/connections?property=name==TestConn` |
| `description` | `/connections?property=description==Test%20description` |
| `connectionSpec.id` | `/connections?property=connectionSpec.id==938903,849048` |
| `state` | `/connections?property=state==enabled` |

{style="table-layout:auto"}

**`sourceConnection`**

| Propiedad | Ejemplo |
| --- | --- |
| `id` | `/sourceConnections?property=id==736873,9485095` |
| `connectionSpec.id` | `/sourceConnections?property=connectionSpec.id==938903,849048` |
| `baseConnectionId` | `/sourceConnections?property=baseConnectionId==983908,4908095` |

{style="table-layout:auto"}

**`targetConnection`**

| Propiedad | Ejemplo |
| --- | --- |
| `id` | `/targetConnections?property=id==736873,9485095` |
| `connectionSpec.id` | `/targetConnections?property=connectionSpec.id==938903,849048` |
| `baseConnectionId` | `/targetConnections?property=baseConnectionId==983908,4908095` |

{style="table-layout:auto"}

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

{style="table-layout:auto"}

**`run`**

| Propiedad | Ejemplo |
| --- | --- |
| `id` | `/runs?property=id==736873,9485095` |
| `flowId` | `/runs?property=flowId==8749844` |
| `state` | `/runs?property=state==inProgress` |

{style="table-layout:auto"}

## Casos de uso {#use-cases}

Lea esta sección para ver algunos ejemplos específicos de cómo puede utilizar el filtrado y la ordenación para devolver información sobre determinados conectores o para ayudarle en los problemas de depuración. Adobe Si desea agregar algún caso de uso adicional, use las **[!UICONTROL Opciones de comentarios detalladas]** de la página para enviar una solicitud.

**Filtro para devolver conexiones a un destino determinado solamente**

Puede utilizar filtros para devolver conexiones solo a determinados destinos. En primer lugar, consulte el extremo `connectionSpecs` como se muestra a continuación:

```http
GET /connectionSpecs
```

A continuación, busque su `connectionSpec` deseado inspeccionando el parámetro `name`. Por ejemplo, busque Amazon Ads, Pega o SFTP, etc. en el parámetro `name`. El `id` correspondiente es el `connectionSpec` por el que puede buscar en la siguiente llamada de API.

Por ejemplo, filtre los destinos para que solo devuelvan las conexiones existentes a las conexiones de Amazon S3:

```http
GET /connections?property=connectionSpec.id==4890fc95-5a1f-4983-94bb-e060c08e3f81
```

**Filtro para devolver flujos de datos solo a destinos**

Al consultar el extremo `/flows`, en lugar de devolver todos los flujos de datos de origen y destino, puede utilizar un filtro para devolver únicamente los flujos de datos a los destinos. Para ello, use `isDestinationFlow` como parámetro de consulta, de esta manera:

```http
GET /flows?property=inheritedAttributes.properties.isDestinationFlow==true
```

**Filtro para devolver flujos de datos solo a un origen o destino determinado**

Puede filtrar los flujos de datos para devolver flujos de datos a un destino determinado o solo desde un origen determinado. Por ejemplo, filtre los destinos para que solo devuelvan las conexiones existentes a las conexiones de Amazon S3:

```http
GET /flows?property=inheritedAttributes.targetConnections[].connectionSpec.id==4890fc95-5a1f-4983-94bb-e060c08e3f81
```

**Filtro para obtener todas las ejecuciones de un flujo de datos durante un período de tiempo específico**

Puede filtrar las ejecuciones de flujo de datos de un flujo de datos para ver solo las ejecuciones en un intervalo de tiempo determinado, como se muestra a continuación:

```
GET /runs?property=flowId==<flow-id>&property=metrics.durationSummary.startedAtUTC>1593134665781&property=metrics.durationSummary.startedAtUTC<1653134665781
```

**Filtro para devolver solo flujos de datos con errores**

Para fines de depuración, puede filtrar y ver todas las ejecuciones de flujo de datos fallidas para un flujo de datos de origen o destino determinado, como se muestra a continuación:

```http
GET /runs?property=flowId==<flow-id>&property=metrics.statusSummary.status==Failed
```

## Pasos siguientes

En esta guía se explica cómo utilizar los parámetros de consulta `orderby` y `property` para ordenar y filtrar las respuestas en la API de Flow Service. Para obtener guías paso a paso sobre cómo utilizar la API para flujos de trabajo comunes en Platform, consulte los tutoriales de API contenidos en la documentación de [orígenes](../../sources/home.md) y [destinos](../../destinations/home.md).
