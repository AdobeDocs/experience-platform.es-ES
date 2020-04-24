---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Recursos de Lista
topic: developer guide
translation-type: tm+mt
source-git-commit: 4b052cdd3aca9c771855b2dc2a97ca48c7b8ffb0

---


# Recursos de Lista

Puede realizar la vista de una lista de todos los recursos (esquemas, clases, mezclas o tipos de datos) dentro de un contenedor mediante una sola solicitud GET.

>[!NOTE] Al enumerar los recursos, el Registro de Esquemas limita los conjuntos de resultados a 300 elementos. Para devolver recursos más allá de este límite, debe utilizar parámetros [de](#paging)paginación. También se recomienda utilizar parámetros de consulta para [filtrar los resultados](#filtering) y reducir el número de recursos devueltos.
>
> Si desea anular por completo el límite de 300 elementos, debe utilizar el encabezado Aceptar `application/vnd.adobe.xdm-v2+json` para devolver todos los resultados en una sola solicitud.

**Formato API**

```http
GET /{CONTAINER_ID}/{RESOURCE_TYPE}
GET /{CONTAINER_ID}/{RESOURCE_TYPE}?{QUERY_PARAMS}
```

| Parámetro | Descripción |
| --- | --- |
| `{CONTAINER_ID}` | El contenedor donde se ubican los recursos (&quot;global&quot; o &quot;inquilino&quot;). |
| `{RESOURCE_TYPE}` | Tipo de recurso que se va a recuperar de la biblioteca de Esquemas. Los tipos válidos son `datatypes`, `mixins`, `schemas`y `classes`. |
| `{QUERY_PARAMS`} | Parámetros de consulta opcionales para filtrar los resultados. Consulte la sección sobre parámetros [de](#query) consulta para obtener más información. |

**Solicitud**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/classes&limit=2 \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

El formato de respuesta depende del encabezado Accept enviado en la solicitud. Los siguientes encabezados Accept están disponibles para enumerar los recursos:

| Aceptar encabezado | Descripción |
| ------- | ------------ |
| application/vnd.adobe.xed-id+json | Devuelve un breve resumen de cada recurso. Éste es el encabezado recomendado para enumerar los recursos. (Límite: 300) |
| application/vnd.adobe.xed+json | Devuelve el esquema JSON completo para cada recurso, con el original `$ref` y `allOf` incluido. (Límite: 300) |
| application/vnd.adobe.xdm-v2+json | Devuelve el esquema JSON completo para todos los resultados en una sola solicitud, anulando el límite de 300 elementos. |

**Respuesta**

La solicitud anterior utilizaba el encabezado `application/vnd.adobe.xed-id+json` Accept, por lo tanto la respuesta incluye solamente los atributos `title`, `$id`, `meta:altId`y `version` de cada recurso. Si se sustituye `full` en el encabezado Accept, se devuelven todos los atributos de cada recurso. Seleccione el encabezado Aceptar correspondiente en función de la información que necesite en la respuesta.

```JSON
{
  "results": [
    {
        "title": "XDM ExperienceEvent",
        "$id": "https://ns.adobe.com/xdm/context/experienceevent",
        "meta:altId": "_xdm.context.experienceevent",
        "version": "1"
    },
    {
        "title": "XDM Individual Profile",
        "$id": "https://ns.adobe.com/xdm/context/profile",
        "meta:altId": "_xdm.context.profile",
        "version": "1"
    }
  ]
}
```

## Uso de parámetros de consulta {#query}

El Registro de Esquemas admite el uso de parámetros de consulta para filtrar los resultados de la página al enumerar los recursos.

>[!NOTE] Cuando se combinan varios parámetros de consulta, deben separarse con signos ampersands (`&`).

### Paginación {#paging}

Los parámetros de consulta más comunes para la paginación incluyen:

| Parámetro | Descripción |
| --- | --- |
| `start` | Especifique dónde deben estar los resultados enumerados. Ejemplo: `start=2` obtendrá la lista de los resultados del tercer elemento devuelto en adelante. |
| `limit` | Limite el número de recursos devueltos. Ejemplo: `limit=5` devolverá una lista de cinco recursos. |
| `orderby` | Ordene los resultados por una propiedad específica. Ejemplo: `orderby=title` ordenará los resultados por título en orden ascendente (A-Z). Si se Añade un título `-` antes del título (`orderby=-title`), los elementos se ordenarán por título en orden descendente (Z-A). |

### Filtrar {#filtering}

Puede filtrar los resultados utilizando el `property` parámetro, que se utiliza para aplicar un operador específico a una propiedad JSON determinada dentro de los recursos recuperados. Los operadores admitidos son:

| Operador | Descripción | Ejemplo |
| --- | --- | --- |
| `==` | Filtros si la propiedad es igual al valor proporcionado. | `property=title==test` |
| `!=` | Filtros por si la propiedad no es igual al valor proporcionado. | `property=title!=test` |
| `<` | Filtros si la propiedad es menor que el valor proporcionado. | `property=version<5` |
| `>` | Filtros según si la propiedad es buena que el valor proporcionado. | `property=version>5` |
| `<=` | Filtros por si la propiedad es menor o igual que el valor proporcionado. | `property=version<=5` |
| `>=` | Filtros por si la propiedad es buena o igual al valor proporcionado. | `property=version>=5` |
| `~` | Filtros según si la propiedad coincide con una expresión regular proporcionada. | `property=title~test$` |
| (None) | Si se establece únicamente el nombre de la propiedad, solo se devuelven las entradas donde existe la propiedad. | `property=title` |

>[!TIP] Puede utilizar el `property` parámetro para filtrar mezclas según su clase compatible. Por ejemplo, `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` devuelve solo las mezclas compatibles con la clase de Perfil XDM Individual.
