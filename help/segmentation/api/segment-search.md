---
keywords: Experience Platform;segmentación;servicio de segmentación;solución de problemas;API;seg;segmento;Segmento;buscar;búsqueda de segmentos;
title: Extremo de la API de búsqueda de segmentos
topic: guide
description: En la API de servicio de segmentación de Adobe Experience Platform, la búsqueda de segmentos se utiliza para buscar los campos contenidos en varias fuentes de datos y devolverlos en tiempo casi real. Esta guía proporciona información para ayudarle a comprender mejor la búsqueda de segmentos e incluye ejemplos de llamadas de API para realizar acciones básicas mediante la API.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '1201'
ht-degree: 2%

---


# Extremo de búsqueda de segmentos

La búsqueda de segmentos se utiliza para buscar los campos contenidos en varias fuentes de datos y devolverlos en tiempo casi real.

Esta guía proporciona información para ayudarle a comprender mejor la búsqueda de segmentos e incluye ejemplos de llamadas de API para realizar acciones básicas mediante la API.

## Primeros pasos

Los extremos utilizados en esta guía forman parte de la API [!DNL Adobe Experience Platform Segmentation Service]. Antes de continuar, consulte la [guía de introducción](./getting-started.md) para obtener información importante que debe conocer a fin de realizar llamadas exitosas a la API, incluidos los encabezados requeridos y cómo leer llamadas de API de ejemplo.

Además de los encabezados requeridos descritos en la sección de introducción, todas las solicitudes al extremo de búsqueda de segmentos requieren el siguiente encabezado adicional:

- x-ups-search-version: &quot;1.0&quot;

### Buscar en varias Áreas de nombres

Este extremo de búsqueda se puede usar para buscar en varias Áreas de nombres, devolviendo una lista de los resultados del recuento de búsqueda. Se pueden utilizar varios parámetros, separados por signos ampersands (&amp;).

**Formato API**

```http
GET /search/namespaces?schema.name={SCHEMA}
GET /search/namespaces?schema.name={SCHEMA}&s={SEARCH_TERM}
```

| Parámetros | Descripción |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **(Requerido)** Donde {ESQUEMA} representa el valor de clase de esquema asociado a los objetos de búsqueda. Actualmente, solo se admite `_xdm.context.segmentdefinition`. |
| `s={SEARCH_TERM}` | *(Opcional)* Donde {SEARCH_TERM} representa una consulta que se ajusta a la implementación de Microsoft de la sintaxis [ de búsqueda de ](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)Lucene. Si no se especifica ningún término de búsqueda, se devolverán todos los registros asociados con `schema.name`. En el [apéndice](#appendix) de este documento figura una explicación más detallada. |

**Solicitud**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/namespaces?schema.name=_xdm.context.segmentdefinition \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Este extremo de búsqueda se puede utilizar para recuperar una lista de todos los objetos indexados de texto completo dentro de la Área de nombres especificada. Se pueden utilizar varios parámetros, separados por signos ampersands (&amp;).

**Formato API**

```http
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}&s={SEARCH_TERM}
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}&entityId={ENTITY_ID}
```

| Parámetros | Descripción |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **(Requerido)** Donde {ESQUEMA} contiene el valor de clase de esquema asociado a los objetos de búsqueda. Actualmente, solo se admite `_xdm.context.segmentdefinition`. |
| `namespace={NAMESPACE}` | **(Requerido)** Donde {ÁREA DE NOMBRES} contiene la Área de nombres en la que desea realizar la búsqueda. |
| `s={SEARCH_TERM}` | *(Opcional)* Donde {SEARCH_TERM} contiene una consulta que se ajusta a la implementación de Microsoft de la sintaxis [ de búsqueda de ](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)Lucene. Si no se especifica ningún término de búsqueda, se devolverán todos los registros asociados con `schema.name`. En el [apéndice](#appendix) de este documento figura una explicación más detallada. |
| `entityId={ENTITY_ID}` | *(Opcional)* Limita la búsqueda dentro de la carpeta designada, especificada con {ENTITY_ID}. |
| `limit={LIMIT}` | *(Opcional)* Donde {LIMIT} representa el número de resultados de búsqueda que se van a devolver. El valor predeterminado es 50. |
| `page={PAGE}` | *(Opcional)* Donde {PAGE} representa el número de página utilizado para paginar los resultados de la consulta buscada. Tenga en cuenta que el número de página inicio en **0**. |


**Solicitud**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/entities?schema.name=_xdm.context.segmentdefinition&namespace=AAMSegments \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Este extremo de búsqueda se puede utilizar para obtener la información estructural sobre el objeto de búsqueda solicitado.

**Formato API**

```http
GET /search/taxonomy?schema.name={SCHEMA}&namespace={NAMESPACE}&entityId={ENTITY_ID}
```

| Parámetros | Descripción |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **(Requerido)** Donde {ESQUEMA} contiene el valor de clase de esquema asociado a los objetos de búsqueda. Actualmente, solo se admite `_xdm.context.segmentdefinition`. |
| `namespace={NAMESPACE}` | **(Requerido)** Donde {ÁREA DE NOMBRES} contiene la Área de nombres en la que desea realizar la búsqueda. |
| `entityId={ENTITY_ID}` | **(Requerido)** El ID del objeto de búsqueda sobre el que desea obtener la información estructural, especificado con {ENTITY_ID}. |

**Solicitud**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/taxonomy?schema.name=_xdm.context.segmentdefinition&namespace=AAMSegments&entityId=porsche11037 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Después de leer esta guía, ahora podrá comprender mejor cómo funciona la búsqueda de segmentos.

## Apéndice {#appendix}

Las siguientes secciones proporcionan información adicional sobre cómo funcionan los términos de búsqueda. Las consultas de búsqueda se escriben de la siguiente manera: `s={FieldName}:{SearchExpression}`. Así, por ejemplo, para buscar un segmento denominado AAM o [!DNL Platform], debe utilizar la siguiente consulta de búsqueda: `s=segmentName:AAM%20OR%20Platform`.

> !![NOTE] Para prácticas recomendadas, la expresión de búsqueda debe estar codificada en HTML, como el ejemplo que se muestra arriba.

### Campos de búsqueda {#search-fields}

La siguiente tabla lista los campos que se pueden buscar dentro del parámetro de consulta de búsqueda.

| Nombre del campo | Descripción |
| ---------- | ----------- |
| folderId | Carpeta o carpetas que tienen el ID de carpeta de la búsqueda especificada. |
| folderLocation | Ubicación o ubicaciones que tienen la ubicación de la carpeta de la búsqueda especificada. |
| parentFolderId | Segmento o carpeta que tiene el ID de carpeta principal de la búsqueda especificada. |
| segmentId | El segmento coincide con la ID del segmento de la búsqueda especificada. |
| segmentName | El segmento coincide con el nombre del segmento de la búsqueda especificada. |
| segmentDescription | El segmento coincide con la descripción del segmento de la búsqueda especificada. |

### Buscar expresión {#search-expression}

La siguiente tabla lista los detalles específicos de cómo funcionan las consultas de búsqueda al utilizar la API de búsqueda de segmentos.

>!![NOTE] Los siguientes ejemplos se muestran en un formato no HTML codificado para una mejor claridad. Para prácticas recomendadas, HTML codifica la expresión de búsqueda.

| Ejemplo de expresión de búsqueda | Descripción |
| ------------------------- | ----------- |
| foo | Busque cualquier palabra. Esto devolverá resultados si se encuentra la palabra &quot;foo&quot; en cualquiera de los campos en los que se puede buscar. |
| barra de PUBLICACIÓN Y | Una búsqueda booleana. Esto devolverá resultados si **tanto** las palabras &quot;foo&quot; como &quot;bar&quot; se encuentran en cualquiera de los campos en los que se puede buscar. |
| barra de foo OR | Una búsqueda booleana. Esto devolverá resultados si **o** la palabra &quot;foo&quot; o la palabra &quot;bar&quot; se encuentran en cualquiera de los campos en los que se puede buscar. |
| Barra de foo NOT | Una búsqueda booleana. Esto devolverá resultados si se encuentra la palabra &quot;foo&quot; pero no se encuentra la palabra &quot;bar&quot; en ninguno de los campos en los que se puede buscar. |
| name: barra de PUBLICACIÓN Y | Una búsqueda booleana. Esto devolverá resultados si **tanto** las palabras &quot;foo&quot; como &quot;bar&quot; se encuentran en el campo &quot;name&quot;. |
| run* | Búsqueda comodín. El uso de un asterisco (*) coincide con 0 o más caracteres, lo que significa que devolverá resultados si el contenido de cualquiera de los campos en los que se puede realizar la búsqueda contiene una palabra que inicio con &quot;ejecutar&quot;. Por ejemplo, esto devolverá resultados si aparecen las palabras &quot;se ejecuta&quot;, &quot;se ejecuta&quot;, &quot;se ejecuta&quot; o &quot;se ejecuta&quot;. |
| cam? | Búsqueda comodín. Uso de un signo de interrogación (?) coincide exactamente con un carácter, lo que significa que devolverá resultados si el contenido de cualquiera de los campos en los que se pueden realizar búsquedas inicio con &quot;cam&quot; y una letra adicional. Por ejemplo, esto devolverá resultados si aparecen las palabras &quot;camp&quot; o &quot;cams&quot;, pero no devolverá resultados si aparecen las palabras &quot;cámara&quot; o &quot;fogata&quot;. |
| &quot;paraguas azul&quot; | Búsqueda de frase. Esto devolverá resultados si el contenido de cualquiera de los campos en los que se puede buscar contiene la frase completa &quot;paraguas azul&quot;. |
| blue\~ | Una búsqueda difusa. Si lo desea, puede colocar un número entre 0 y 2 después de la virgulilla (~) para especificar la distancia de edición. Por ejemplo, &quot;blue\~1&quot; devolverá &quot;blue&quot;, &quot;blues&quot; o &quot;glue&quot;. La búsqueda difusa puede **sólo** aplicarse a términos, no frases. Sin embargo, puede anexar tildes al final de cada palabra de una frase. Por lo tanto, &quot;acampar\~ en\~ el\~ verano\~&quot; coincidirá con &quot;acampar en verano&quot;. |
| &quot;aeropuerto del hotel&quot;\~5 | Búsqueda de proximidad. Este tipo de búsqueda se utiliza para encontrar términos que están próximos entre sí en un documento. Por ejemplo, la frase `"hotel airport"~5` encontrará los términos &quot;hotel&quot; y &quot;aeropuerto&quot; dentro de 5 palabras entre sí en un documento. |
| `/a[0-9]+b$/` | Una búsqueda de expresión normal. Este tipo de búsqueda encuentra una coincidencia basada en el contenido entre las barras diagonales &quot;/&quot;, como se documenta en la clase RegExp. Por ejemplo, para buscar documentos que contengan &quot;motel&quot; o &quot;hotel&quot;, especifique `/[mh]otel/`. Las búsquedas de expresiones regulares se comparan con las palabras únicas. |

Para obtener documentación más detallada sobre la sintaxis de la consulta, lea la [documentación sobre la sintaxis de la consulta de Lucene](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax).
