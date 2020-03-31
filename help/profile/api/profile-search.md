---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Guía para desarrolladores de API de Perfil para clientes en tiempo real
topic: guide
translation-type: tm+mt
source-git-commit: 95e002c60389ca7e4c1dcf32bbcf6f552cd55d95

---


# Búsqueda de Perfiles

La búsqueda por Perfil se utiliza para buscar e indexar los campos configurables contenidos en varias fuentes de datos y devolverlos en tiempo casi real.

Esta guía proporciona información para ayudarle a comprender mejor la búsqueda de Perfiles e incluye ejemplos de llamadas de API para realizar acciones básicas mediante la API.

## Primeros pasos

Los extremos de API que se utilizan en esta guía forman parte de la API de Perfil del cliente en tiempo real. Antes de continuar, consulte la guía [para desarrolladores de Perfil para clientes en tiempo](getting-started.md)real.

En particular, la sección [de](getting-started.md) introducción de la guía para desarrolladores de Perfil incluye vínculos a temas relacionados, una guía para leer las llamadas de API de muestra en este documento e información importante sobre los encabezados necesarios que son necesarios para realizar llamadas con éxito a cualquier API de plataforma de experiencia.

### Obtener resultados de búsqueda

El extremo de búsqueda se puede utilizar para obtener resultados de búsqueda en función de los valores del parámetro requerido y los parámetros de consulta opcionales adicionales `schema.name` y adicionales. Se pueden utilizar varios parámetros, separados por signos ampersands (&amp;).

**Formato API**

```http
GET /search?{QUERY_PARAMETERS}
```

| Parámetro | Descripción |
|---|---|
| `schema.name` | **Requerido.** Nombre de la clase de esquema que contiene el contenido que se va a buscar, escrito en formato de notación de puntos. Actualmente, solo `schema.name=_xdm.context.segmentdefinition` se admite. |
| `limit` | Número de resultados de búsqueda que se van a devolver. El valor predeterminado es 50. |
| `page` | Número de página utilizado para paginar los resultados de la consulta buscada. |
| `s` | consulta que se ajusta a la implementación de Microsoft de la sintaxis [de búsqueda de](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)Lucene. Si no se especifica ningún término de búsqueda, se devolverán todos los registros asociados con `schema.name` . Encontrará una explicación más detallada en la sección Parámetros [de](#search-parameters) búsqueda de este documento. |
| `namespace` | Identifica los datos reales para buscar en la clase de esquema especificada en el `schema.name` parámetro. |
| `organization.type` | Determina el contenido de la respuesta. El formato del contenido devuelto depende de los valores utilizados en `schema.name`. Por `_xdm.context.segmentdefinition`, los valores válidos son `hierarchy` o `hierarchyinfo`. |
| `organization.id` | **Necesario si`organization.type`se especifica.** Proporciona la jerarquía de la organización especificada cuando se utiliza con la jerarquía `organization.type` de jerarquía. |

**Solicitud**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search?schema.name=_xdm.context.segmentdefinition \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una matriz de objetos que cumplen los criterios de búsqueda. En este ejemplo, como el `schema.name` parámetro era `_xdm.context.segmentdefinition`, se devuelve una lista de definiciones de segmentos.

```json
{
  "aam-hierarchy": {
    "_xdm.context.segmentdefinition": [
      {
        "isFolder": true,
        "id": "100023",
        "name": "Segment Definition 1",
        "description": "Sample description.",
        "parentFolderId": "99970"
      },
      {
        "isFolder": false,
        "id": "1000028",
        "name": "Segment Definition 2",
        "description": "Sample description.",
        "parentFolderId": "103584"
      }
    ]
  },
  "page": {
    "totalCount": 2,
    "totalPages": 1,
    "pageOffset": "1",
    "pageSize": 2,
    "limit": 2
  }
}
```

### Creación de solicitudes de aprovisionamiento

Puede crear solicitudes de aprovisionamiento para habilitar la búsqueda de Perfiles en esquemas haciendo una solicitud POST al extremo del `/search/provisioning/component/init` .

**Solicitud**

>[!CAUTION]
>Esta solicitud POST no contiene una carga útil y, por lo tanto, no requiere un encabezado Content-Type. Además, no hay encabezado de Simulador para pruebas porque todos los datos se envían a un simulador para pruebas global.

```shell
curl -X POST \
    https://platform.adobe.io/data/core/ups/search/provisioning/component/init \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' 
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 201 (Creado) y el siguiente mensaje:

```plaintext
The request has been fulfilled and resulted in a new resource being created.
```

### Administrar solicitudes de configuración

El extremo de configuración puede utilizarse para configurar los índices, los indexadores y las conexiones de origen de datos correspondientes para una nueva organización de IMS. Se requieren dos propiedades para gestionar las solicitudes de configuración: `databaseName` y `containerName`.

`databaseName` representa el nombre de la base de datos de Perfil para la organización que se va a configurar.

`containerName` representa el nombre del contenedor rellenado por un conector de datos, que es lo que se lee durante la configuración. Existen dos valores para `containerName`, uno o ambos se pueden usar en la solicitud POST:
- `_xdm.content.segmentdefinition`
- `_experience.audiencemanager.segmentfolder`

### Crear una solicitud de configuración

La siguiente llamada de API genera el origen de datos, el indizador y el índice necesarios en función de los parámetros suministrados en la carga útil de la solicitud.

**Formato API**

```http
POST /search/configure
```

**Solicitud**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/search/configure \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "databaseName": {DATABASE_NAME},
    "containerName": "_xdm.context.segmentdefinition" "_experience.audiencemanager.segmentfolder"
  }'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 202 (Aceptado) y un mensaje de texto sin formato.

```plaintext
The request has been accepted for processing, but the processing has not been completed.
```

### Eliminar una solicitud de configuración

La siguiente llamada de API elimina las entradas de índice coincidentes y elimina el indizador y el origen de datos en función de los parámetros suministrados en la carga útil de la solicitud.

>[!NOTE]
>El índice en sí no se eliminará, ya que es un recurso compartido.

**Formato API**

```http
DELETE /search/configure
```

**Solicitud**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/search/configure \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "databaseName": {DATABASE_NAME},
    "containerName": "_xdm.context.segmentdefinition" "_experience.audiencemanager.segmentfolder"
  }'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 202 (Aceptado) y un mensaje de texto sin formato.

```plaintext
The request has been accepted for processing, but the processing has not been completed.
```

## Pasos siguientes

Después de leer esta guía, ahora podrá comprender mejor cómo funciona la búsqueda de Perfiles de clientes en tiempo real. Para obtener más información sobre el Perfil del cliente en tiempo real, lea la descripción general [del Perfil del cliente en tiempo](../home.md)real. Para obtener más información sobre la segmentación, lea la información general [sobre la](../../segmentation/home.md)segmentación.

## Apéndice {#appendix}

### Parámetros de búsqueda {#search-parameters}

La siguiente tabla lista los detalles específicos de cómo funciona el parámetro de búsqueda al utilizar la API de búsqueda.

| Consulta de búsqueda | Descripción |
|------------ | -----------|
| foo | Busque cualquier palabra. Esto devolverá resultados si se encuentra la palabra &quot;foo&quot; en cualquiera de los campos en los que se puede buscar. |
| barra de PUBLICACIÓN Y | Una búsqueda booleana. Esto devolverá resultados si **ambas** palabras, &quot;foo&quot; y &quot;bar&quot;, se encuentran en cualquiera de los campos en los que se puede buscar. |
| barra de foo OR | Una búsqueda booleana. Esto devolverá resultados si **se encuentra** la palabra &quot;foo&quot; o la palabra &quot;bar&quot; en cualquiera de los campos en los que se puede buscar. |
| Barra de foo NOT | Una búsqueda booleana. Esto devolverá resultados si se encuentra la palabra &quot;foo&quot; pero no se encuentra la palabra &quot;bar&quot; en ninguno de los campos en los que se puede buscar. |
| name: barra de PUBLICACIÓN Y | Una búsqueda booleana. Esto devolverá resultados si **ambas** palabras, &quot;foo&quot; y &quot;bar&quot;, se encuentran en el campo &quot;nombre&quot;. |
| run* | Búsqueda comodín. El uso de un asterisco (*) coincide con 0 o más caracteres, lo que significa que devolverá resultados si el contenido de cualquiera de los campos en los que se puede realizar la búsqueda contiene una palabra que inicio con &quot;ejecutar&quot;. Por ejemplo, esto devolverá resultados si aparecen las palabras &quot;se ejecuta&quot;, &quot;se ejecuta&quot;, &quot;se ejecuta&quot; o &quot;se ejecuta&quot;. |
| cam? | Búsqueda comodín. Uso de un signo de interrogación (?) coincide exactamente con un carácter, lo que significa que devolverá resultados si el contenido de cualquiera de los campos en los que se pueden realizar búsquedas inicio con &quot;cam&quot; y una letra adicional. Por ejemplo, esto devolverá resultados si aparecen las palabras &quot;camp&quot; o &quot;cams&quot;, pero no devolverá resultados si aparecen las palabras &quot;cámara&quot; o &quot;fogata&quot;. |
| &quot;paraguas azul&quot; | Búsqueda de frase. Esto devolverá resultados si el contenido de cualquiera de los campos en los que se puede buscar contiene la frase completa &quot;paraguas azul&quot;. |
| blue\~ | Una búsqueda difusa. Si lo desea, puede colocar un número entre 0 y 2 después de la virgulilla (~) para especificar la distancia de edición. Por ejemplo, &quot;blue\~1&quot; devolverá &quot;blue&quot;, &quot;blues&quot; o &quot;glue&quot;. La búsqueda difusa **sólo** se puede aplicar a términos, no frases. Sin embargo, puede anexar tildes al final de cada palabra de una frase. Por lo tanto, &quot;acampar\~ en\~ el\~ verano\~&quot; coincidirá con &quot;acampar en verano&quot;. |
| &quot;aeropuerto del hotel&quot;\~5 | Búsqueda de proximidad. Este tipo de búsqueda se utiliza para encontrar términos que están próximos entre sí en un documento. Por ejemplo, la frase `"hotel airport"~5` encontrará los términos &quot;hotel&quot; y &quot;aeropuerto&quot; dentro de 5 palabras entre sí en un documento. |
| `/a[0-9]+b$/` | Una búsqueda de expresión normal. Este tipo de búsqueda encuentra una coincidencia basada en el contenido entre las barras diagonales &quot;/&quot;, como se documenta en la clase RegExp. Por ejemplo, para buscar documentos que contengan &quot;motel&quot; o &quot;hotel&quot;, especifique `/[mh]otel/`. Las búsquedas de expresiones regulares se comparan con las palabras únicas. |

Para obtener documentación más detallada sobre la sintaxis de la consulta, consulte la documentación sobre la sintaxis de la consulta de [Lucene](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax).
