---
keywords: Experience Platform;segmentación;servicio de segmentación;solución de problemas;API;seg;segmento;búsqueda;búsqueda;búsqueda de segmentos;
title: Punto final de la API de búsqueda de segmentos
description: En la API del servicio de segmentación de Adobe Experience Platform, la búsqueda de segmentos se utiliza para buscar campos contenidos en varias fuentes de datos y devolverlos en tiempo casi real. Esta guía proporciona información para ayudarle a comprender mejor la búsqueda de segmentos e incluye ejemplos de llamadas API para realizar acciones básicas con la API.
exl-id: bcafbed7-e4ae-49c0-a8ba-7845d8ad663b
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1201'
ht-degree: 2%

---

# Punto final de búsqueda de segmentos

La búsqueda de segmentos se utiliza para buscar campos contenidos en varias fuentes de datos y devolverlos casi en tiempo real.

Esta guía proporciona información para ayudarle a comprender mejor la búsqueda de segmentos e incluye ejemplos de llamadas API para realizar acciones básicas con la API.

## Primeros pasos

Los extremos utilizados en esta guía forman parte del [!DNL Adobe Experience Platform Segmentation Service] API. Antes de continuar, revise la [guía de introducción](./getting-started.md) para obtener información importante que debe conocer para realizar correctamente llamadas a la API, incluidos los encabezados necesarios y cómo leer llamadas de API de ejemplo.

Además de los encabezados requeridos descritos en la sección Introducción , todas las solicitudes al extremo Búsqueda de segmentos requieren el siguiente encabezado adicional:

- x-ups-search-version: &quot;1.0&quot;

### Buscar en varias áreas de nombres

Este extremo de búsqueda se puede usar para buscar en varias áreas de nombres, devolviendo una lista de resultados de recuento de búsqueda. Se pueden usar varios parámetros, separados por el símbolo &amp;.

**Formato de API**

```http
GET /search/namespaces?schema.name={SCHEMA}
GET /search/namespaces?schema.name={SCHEMA}&s={SEARCH_TERM}
```

| Parámetros | Descripción |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **(Obligatorio)** Donde {SCHEMA} representa el valor de clase de esquema asociado con los objetos de búsqueda. Actualmente, solo `_xdm.context.segmentdefinition` es compatible. |
| `s={SEARCH_TERM}` | *(Opcional)* Donde {SEARCH_TERM} representa una consulta que se ajusta a la implementación de Microsoft de [Sintaxis de búsqueda de Lucene](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). Si no se especifica ningún término de búsqueda, entonces todos los registros asociados con `schema.name` se devuelve. Puede encontrar una explicación más detallada en la [apéndice](#appendix) de este documento. |

**Solicitud**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/namespaces?schema.name=_xdm.context.segmentdefinition \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-ups-search-version: 1.0' 
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con la siguiente información.

```json
{
  "namespaces": [
    {
      "namespace": "AAMTraits",
      "displayName": "AAMTraits",
      "count": 45
    },
    {
      "namespace": "AAMSegments",
      "displayName": "AAMSegment",
      "count": 10
    },
    {
      "namespace": "SegmentsAISegments",
      "displayName": "SegmentSAISegment",
      "count": 3
    }
  ],
  "totalCount": 3,
  "status": {
    "message": "Success"
  }
}
```

### Buscar entidades individuales

Este extremo de búsqueda se puede usar para recuperar una lista de todos los objetos indexados de texto completo dentro del espacio de nombres especificado. Se pueden usar varios parámetros, separados por el símbolo &amp;.

**Formato de API**

```http
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}&s={SEARCH_TERM}
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}&entityId={ENTITY_ID}
```

| Parámetros | Descripción |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **(Obligatorio)** Donde {SCHEMA} contiene el valor de clase de esquema asociado con los objetos de búsqueda. Actualmente, solo `_xdm.context.segmentdefinition` es compatible. |
| `namespace={NAMESPACE}` | **(Obligatorio)** Donde {NAMESPACE} contiene el espacio de nombres en el que desea buscar. |
| `s={SEARCH_TERM}` | *(Opcional)* Donde {SEARCH_TERM} contiene una consulta que se ajusta a la implementación de Microsoft de [Sintaxis de búsqueda de Lucene](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). Si no se especifica ningún término de búsqueda, entonces todos los registros asociados con `schema.name` se devuelve. Puede encontrar una explicación más detallada en la [apéndice](#appendix) de este documento. |
| `entityId={ENTITY_ID}` | *(Opcional)* Limita la búsqueda a dentro de la carpeta designada, especificada con {ENTITY_ID}. |
| `limit={LIMIT}` | *(Opcional)* Donde {LIMIT} representa el número de resultados de búsqueda que se van a devolver. El valor predeterminado es 50. |
| `page={PAGE}` | *(Opcional)* Donde {PAGE} representa el número de página utilizado para paginar los resultados de la consulta buscada. Tenga en cuenta que el número de página empieza en **0**. |


**Solicitud**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/entities?schema.name=_xdm.context.segmentdefinition&namespace=AAMSegments \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-ups-search-version: 1.0' 
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con resultados que coinciden con la consulta de búsqueda.

```json
{
  "entities": [
    {
       "id": "1012667",
       "base64EncodedSourceId": "RFVGamdydHpEdy01ZTE1ZGJlZGE4YjAxMzE4YWExZWY1MzM1",
       "sourceId": "DUFjgrtzDw-5e15dbeda8b01318aa1ef533",
       "isFolder": true,
       "parentFolderId": "974139",
       "name": "aam-47995 verification (100)"
    },
    {
       "id": "14653311",
       "base64EncodedSourceId": "REVGamduLVgzdy01ZTE2ZjRhNjc1ZDZhMDE4YThhZDM3NmY1",
       "sourceId": "DEFjgn-X3w-5e16f4a675d6a018a8ad376f",
       "isFolder": false,
       "parentFolderId": "324050",
       "name": "AAM - Heavy equipment",
       "description": "AAM - Acme Equipment"
    }
 
 ],
  "page": {
    "totalCount": 2,
    "totalPages": 1,
    "pageOffset": 0,
    "pageSize": 10
  },
  "status": {
    "message": "Success"
  }
}
```

### Obtener información estructural sobre un objeto de búsqueda

Este extremo de búsqueda se puede usar para obtener la información estructural sobre el objeto de búsqueda solicitado.

**Formato de API**

```http
GET /search/taxonomy?schema.name={SCHEMA}&namespace={NAMESPACE}&entityId={ENTITY_ID}
```

| Parámetros | Descripción |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **(Obligatorio)** Donde {SCHEMA} contiene el valor de clase de esquema asociado con los objetos de búsqueda. Actualmente, solo `_xdm.context.segmentdefinition` es compatible. |
| `namespace={NAMESPACE}` | **(Obligatorio)** Donde {NAMESPACE} contiene el espacio de nombres en el que desea buscar. |
| `entityId={ENTITY_ID}` | **(Obligatorio)** El ID del objeto de búsqueda del que desea obtener la información estructural, especificado con {ENTITY_ID}. |

**Solicitud**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/taxonomy?schema.name=_xdm.context.segmentdefinition&namespace=AAMSegments&entityId=porsche11037 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-ups-search-version: 1.0' 
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con información estructural detallada sobre el objeto de búsqueda solicitado.

```json
{
    "taxonomy": [
        {
            "id": "0",
            "base64EncodedSourceId": "RFVGZ01BLTVlNjgzMGZjMzk3YjQ1MThhYWExYTA4Zg2",
            "name": "AAMTraits for Cars",
            "parentFolderId": "root"
        },
        {
            "id": "150561",
            "base64EncodedSourceId": "RFVGamdpRk1BZy01ZTY4MzBmYzM5N2I0NTE4YWFhMWEwOGY1",
            "name": "Fast Cars",
            "parentFolderId": "carTraits"
        },
        {
            "id": "porsche11037",
            "base64EncodedSourceId": "REFGZ01CLTVlNjczMGZjMzk3YjQ1MThhZGIxYTA4Zg==",
            "name": "Porsche",
            "parentFolderId": "redCarsFolderId"
        }
    ],
    "status": {
        "message": "Success"
    }
}
```

## Pasos siguientes

Después de leer esta guía, ahora puede comprender mejor cómo funciona la búsqueda de segmentos.

## Apéndice {#appendix}

Las secciones siguientes proporcionan información adicional sobre cómo funcionan los términos de búsqueda. Las consultas de búsqueda se escriben de la siguiente manera: `s={FieldName}:{SearchExpression}`. Por ejemplo, para buscar un segmento denominado AAM o [!DNL Platform], utilizaría la siguiente consulta de búsqueda: `s=segmentName:AAM%20OR%20Platform`.

> !![NOTE] Para prácticas recomendadas, la expresión de búsqueda debe tener codificación HTML, como en el ejemplo mostrado arriba.

### Campos de búsqueda {#search-fields}

La tabla siguiente enumera los campos que se pueden buscar dentro del parámetro de consulta de búsqueda.

| Nombre del campo | Descripción |
| ---------- | ----------- |
| folderId | La carpeta o carpetas que tienen el ID de la carpeta de la búsqueda especificada. |
| folderLocation | La ubicación o ubicaciones que tienen la ubicación de la carpeta de la búsqueda especificada. |
| parentFolderId | El segmento o la carpeta que tienen el ID de la carpeta principal de la búsqueda especificada. |
| segmentId | El segmento coincide con el ID de segmento de la búsqueda especificada. |
| segmentName | El segmento coincide con el nombre del segmento de la búsqueda especificada. |
| segmentDescription | El segmento coincide con la descripción del segmento de la búsqueda especificada. |

### Expresión de búsqueda {#search-expression}

En la tabla siguiente se detallan los aspectos específicos del funcionamiento de las consultas de búsqueda al utilizar la API de búsqueda de segmentos.

>!![NOTE] Los siguientes ejemplos se muestran en un formato codificado no HTML para una mejor claridad. Para prácticas recomendadas, el HTML codifica la expresión de búsqueda.

| Ejemplo de expresión de búsqueda | Descripción |
| ------------------------- | ----------- |
| foo | Busque cualquier palabra. Esto devolverá resultados si la palabra &quot;foo&quot; se encuentra en cualquiera de los campos en los que se puede buscar. |
| foo AND bar | Una búsqueda booleana. Esto devolverá resultados si **both** las palabras &quot;foo&quot; y &quot;bar&quot; se encuentran en cualquiera de los campos en los que se pueden buscar. |
| barra de foo | Una búsqueda booleana. Esto devolverá resultados si **o** la palabra &quot;foo&quot; o la palabra &quot;bar&quot; se encuentran en cualquiera de los campos en los que se puede buscar. |
| foo NOT bar | Una búsqueda booleana. Esto devolverá resultados si se encuentra la palabra &quot;foo&quot;, pero la palabra &quot;bar&quot; no se encuentra en ninguno de los campos en los que se puede buscar. |
| nombre: foo AND bar | Una búsqueda booleana. Esto devolverá resultados si **both** las palabras &quot;foo&quot; y &quot;bar&quot; se encuentran en el campo &quot;name&quot;. |
| run* | Una búsqueda comodín. El uso de un asterisco (*) coincide con 0 o más caracteres, lo que significa que devolverá resultados si el contenido de cualquiera de los campos en los que se puede buscar contiene una palabra que empieza por &quot;ejecutar&quot;. Por ejemplo, esto devolverá resultados si aparecen las palabras &quot;se ejecuta&quot;, &quot;se ejecuta&quot;, &quot;se ejecuta&quot; o &quot;se ejecuta&quot;. |
| cam? | Una búsqueda comodín. Uso de un signo de interrogación (?) coincide exactamente con un carácter, lo que significa que devolverá resultados si el contenido de cualquiera de los campos en los que se puede buscar comienza con &quot;cam&quot; y una letra adicional. Por ejemplo, esto devolverá resultados si aparecen las palabras &quot;camp&quot; o &quot;cams&quot;, pero no devolverá resultados si aparecen las palabras &quot;cámara&quot; o &quot;fogata&quot;. |
| &quot;paraguas azul&quot; | Una búsqueda de frases. Esto devolverá resultados si el contenido de cualquiera de los campos en los que se puede buscar contiene la frase completa &quot;paraguas azul&quot;. |
| blue\~ | Una búsqueda difusa. De forma opcional, puede colocar un número entre 0 y 2 después de la virgulilla (~) para especificar la distancia de edición. Por ejemplo, &quot;blue\~1&quot; devolvería &quot;blue&quot;, &quot;blues&quot; o &quot;glue&quot;. La búsqueda difusa puede **only** se aplicará a los términos, no a las frases. Sin embargo, puede añadir tildes al final de cada palabra de una frase. Por lo tanto, por ejemplo, &quot;camping\~ in\~ the\~ verano\~&quot; coincidiría con &quot;camping in the Summer&quot;. |
| &quot;aeropuerto del hotel&quot;\~5 | Búsqueda por proximidad. Este tipo de búsqueda se utiliza para encontrar términos que estén próximos entre sí en un documento. Por ejemplo, la frase `"hotel airport"~5` encontrará los términos &quot;hotel&quot; y &quot;aeropuerto&quot; dentro de 5 palabras entre ellos en un documento. |
| `/a[0-9]+b$/` | Búsqueda de expresiones regulares. Este tipo de búsqueda encuentra una coincidencia basada en el contenido entre las barras diagonales &quot;/&quot;, como se documenta en la clase RegExp. Por ejemplo, para buscar documentos que contengan &quot;motel&quot; o &quot;hotel&quot;, especifique `/[mh]otel/`. Las búsquedas de expresiones regulares se comparan con las palabras simples. |

Para obtener documentación más detallada sobre la sintaxis de la consulta, lea la [Documentación de sintaxis de consulta de Lucene](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax).
