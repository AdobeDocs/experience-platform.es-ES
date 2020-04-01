---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Recursos de Lista
topic: developer guide
translation-type: tm+mt
source-git-commit: 1541b027a4e572dc5e4e64de1117a269c58bafab

---


# Recursos de Lista

Puede realizar la vista de una lista de todos los recursos (esquemas, clases, mezclas o tipos de datos) dentro de un contenedor mediante una sola solicitud GET. Para ayudar a filtrar los resultados, el Registro de Esquemas admite el uso de parámetros de consulta al enumerar los recursos.

Los parámetros de consulta más comunes incluyen:

* `limit` - Limite el número de recursos devueltos. Ejemplo: `limit=5` devolverá una lista de cinco recursos.
* `orderby` - Ordenar los resultados por una propiedad específica. Ejemplo: `orderby=title` ordenará los resultados por título en orden ascendente (A-Z). Si se Añade un título `-` antes del título (`orderby=-title`), los elementos se ordenarán por título en orden descendente (Z-A).
* `property` - Filtre los resultados en cualquier atributo de nivel superior. Por ejemplo, `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` devuelve solo las mezclas compatibles con la clase de Perfil XDM Individual.

Cuando se combinan varios parámetros de consulta, deben separarse con signos ampersands (`&`).

**Formato API**

```http
GET /{CONTAINER_ID}/{RESOURCE_TYPE}
```

| Parámetro | Descripción |
| --- | --- |
| `{CONTAINER_ID}` | El contenedor donde se ubican los recursos (&quot;global&quot; o &quot;inquilino&quot;). |
| `{RESOURCE_TYPE}` | Tipo de recurso que se va a recuperar de la biblioteca de Esquemas. Los tipos válidos son `datatypes`, `mixins`, `schemas`y `classes`. |

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
| application/vnd.adobe.xed-id+json | Devuelve un breve resumen de cada recurso, generalmente el encabezado preferido para el listado |
| application/vnd.adobe.xed+json | Devuelve el esquema JSON completo para cada recurso, con el original `$ref` y `allOf` incluido |

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
