---
title: Extremo de etiquetas unificadas
description: Obtenga información sobre cómo crear, actualizar, administrar y eliminar etiquetas y categorías de etiquetas mediante las API de Adobe Experience Platform.
role: Developer
source-git-commit: ede314d0cbe50514090915fccf7ef3c2a5254b7a
workflow-type: tm+mt
source-wordcount: '1860'
ht-degree: 4%

---


# Extremo de etiquetas unificadas

>[!IMPORTANT]
>
>La dirección URL del extremo para este conjunto de extremos es `https://experience.adobe.io`.

Las etiquetas son una funcionalidad que permite administrar taxonomías de metadatos para clasificar objetos empresariales y facilitar así su detección y categorización. Posteriormente, puede organizar estas etiquetas en otros grupos añadiéndolas a las categorías de etiquetas.

Esta guía proporciona información para ayudarle a comprender mejor las etiquetas y las categorías de etiquetas, e incluye llamadas de API de ejemplo para realizar acciones básicas mediante la API.

## Introducción

Los extremos utilizados en esta guía forman parte de las API de Adobe Experience Platform. Antes de continuar, consulte la [guía de introducción](./getting-started.md) para obtener información importante que necesita conocer para realizar llamadas correctamente a la API de, incluidos los encabezados necesarios y cómo leer llamadas de API de ejemplo

### Glosario

El siguiente glosario resalta la diferencia entre una **etiqueta** y una **categoría de etiqueta**.

- **Etiqueta**: una etiqueta permite administrar la taxonomía de metadatos para objetos empresariales, lo que permite clasificar estos objetos para facilitar la detección y la categorización.
   - **Etiqueta sin categoría**: una etiqueta sin clasificar es una etiqueta que no pertenece a una categoría de etiqueta. De forma predeterminada, las etiquetas creadas no se clasificarán.
- **Categoría de etiqueta**: una categoría de etiqueta permite agrupar las etiquetas en conjuntos significativos, lo que le permite proporcionar más contexto al propósito de la etiqueta.

## Recuperación de una lista de categorías de etiquetas {#get-tag-categories}

Puede recuperar una lista de categorías de etiquetas que pertenezcan a su organización realizando una solicitud de GET a `/tagCategory` punto final.

**Formato de API**

```http
GET /tagCategory
GET /tagCategory?{QUERY_PARAMETERS}
```

Se pueden utilizar los siguientes parámetros de consulta opcionales al recuperar las categorías de etiquetas.

| Parámetro de consulta | Descripción | Ejemplo |
| --------------- | ----------- | ------- |
| `start` | Ubicación desde la que comienza la lista de resultados. Puede utilizarlo para indicar el índice inicial para la paginación de los resultados. | `start=a` |
| `limit` | Número máximo de categorías de etiquetas que desea recuperar por página. | `limit=20` |
| `property` | Atributo por el que se desea filtrar al recuperar las categorías de etiqueta. Los valores admitidos son: &lt;ul><li>`name`: nombre de la categoría de etiqueta.</li></ul> | `property=name==category` |
| `sortBy` | Orden por el que se ordenan las categorías de etiquetas. Los valores admitidos incluyen `name`, `createdAt`, y `modifiedAt`. | `sortBy=name` |
| `sortOrder` | Dirección por la que se ordenan las categorías de etiquetas. Los valores admitidos incluyen `asc` y `desc`. | `sortOrder=asc` |

**Solicitud**

+++Una solicitud de ejemplo para enumerar todas las categorías de etiquetas de su organización

```shell
curl -X GET https://experience.adobe.io/unifiedtags/tagCategory
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con una lista de todas las categorías de etiquetas de su organización.

+++Una respuesta de ejemplo que contiene una lista de todas las categorías de etiquetas de su organización.

```json
{
    "_page": {
        "count": 1,
        "limit": 10,
        "property": []
    },
    "tags": [
        {
            "id": "e2b7c656-067b-4413-a366-adde0401df50",
            "name": "Test Category",
            "description": "A sample description for the test tag category.",
            "org": "{ORG_ID}",
            "createdBy": "{USER_ID}",
            "createdAt": "1661752268000",
            "modifiedBy": "{USER_ID}",
            "modifiedAt": "1661752268000",
            "tagCount": 0
        }
    ]
}
```

+++

## Crear una nueva categoría de etiqueta {#create-tag-category}

>[!IMPORTANT]
>
>Solo el administrador del sistema y el administrador del producto pueden utilizar esta llamada de API.

Puede crear una nueva categoría de etiquetas realizando una solicitud de POST a `/tagCategory` punto final.

**Formato de API**

```http
POST /tagCategory
```

**Solicitud**

+++Solicitud de ejemplo para crear una nueva categoría de etiqueta.

```shell
curl -X POST https://experience.adobe.io/unifiedtags/tagCategory
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -d '{
    "name": "Sample Test Category",
    "description": "Sample test category"
 }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `name` | Nombre de la categoría de etiqueta que desea crear. |
| `description` | Descripción de la categoría de etiqueta que desea crear. |

+++

**Respuesta**

Una respuesta de ejemplo devuelve el estado HTTP 200 con detalles de la categoría de etiqueta recién creada.

+++Una respuesta de ejemplo que contiene detalles de la categoría de etiquetas recién creada.

```json
{
    "id": "e2b7c656-067b-4413-a366-adde0401df50",
    "name": "Sample Test Category",
    "description": "Sample test category",
    "org": "{ORG_ID}",
    "createdBy": "{USER_ID}",
    "createdAt": "1661752268000",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "1661752268000",
    "tagCount": 0
}
```

+++

## Recuperar una categoría de etiqueta específica {#get-tag-category}

Puede recuperar una categoría de etiquetas específica que pertenezca a su organización realizando una solicitud de GET a `/tagCategory` y especificando el ID de la categoría de etiqueta.

**Formato de API**

```http
GET /tagCategory/{TAG_CATEGORY_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{TAG_CATEGORY_ID}` | El ID de la categoría de etiqueta que está recuperando. |

**Solicitud**

+++Una solicitud de ejemplo para recuperar una categoría de etiqueta específica.

```shell
curl -X GET https://experience.adobe.io/unifiedtags/tagCategory/e2b7c656-067b-4413-a366-adde0401df50 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la categoría de etiqueta especificada.

+++Respuesta de ejemplo que contiene detalles de la categoría de etiqueta especificada.

```json
{
    "id": "e2b7c656-067b-4413-a366-adde0401df50",
    "name": "Test Category",
    "description": "A sample description for the test tag category.",
    "org": "{ORG_ID}",
    "createdBy": "{USER_ID}",
    "createdAt": "1661752268000",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "1661752268000",
    "tagCount": 0
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `id` | El ID de la categoría de etiqueta solicitada. |
| `name` | Nombre de la categoría de etiqueta solicitada. |
| `description` | La descripción de la categoría de etiqueta solicitada. |
| `createdBy` | El ID del usuario que creó la categoría de etiqueta. |
| `createdAt` | La marca de tiempo del momento en el que se creó la categoría de etiqueta. |
| `modifiedBy` | El ID del usuario que actualizó la categoría de etiqueta por última vez. |
| `modifiedAt` | La marca de tiempo de la última actualización de la categoría de etiqueta. |
| `tagCount` | El número de etiquetas que pertenecen a la categoría de etiqueta. |

+++

## Actualizar una categoría de etiqueta específica {#update-tag-category}

>[!IMPORTANT]
>
>Solo el administrador del sistema y el administrador del producto pueden utilizar esta llamada de API.

Puede actualizar los detalles de una categoría de etiquetas específica que pertenezca a su organización realizando una solicitud de PATCH a `/tagCategory` y especificando el ID de la categoría de etiqueta.

**Formato de API**

```http
PATCH /tagCategory/{TAG_CATEGORY_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{TAG_CATEGORY_ID}` | El ID de la categoría de etiqueta que está recuperando. |

**Solicitud**

+++Una solicitud de ejemplo para actualizar una categoría de etiqueta específica.

```shell
curl -X PATCH https://experience.adobe.io/unifiedtags/tagCategory/e2b7c656-067b-4413-a366-adde0401df50 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -d '[{
    "op": "replace",
    "path": "description",
    "value": "Updated sample description",
    "from": "Sample description"
 }]'
```

| Parámetro | Descripción |
| --------- | ----------- |
| `op` | Operación que se ha completado. Para actualizar una categoría de etiqueta específica, establezca este valor en `replace`. |
| `path` | La ruta del campo que se actualizará. Los valores admitidos incluyen `name` y `description`. |
| `value` | El valor actualizado del campo que desea actualizar. |
| `from` | El valor original del campo que desea actualizar. |

+++

**Respuesta**

Un estado HTTP de respuesta 200 correcto con información sobre la categoría de etiqueta recién actualizada.

+++Una respuesta de ejemplo que contiene detalles de la categoría de etiquetas recién actualizada.

```json
{
    "id": "e2b7c656-067b-4413-a366-adde0401df50",
    "name": "Test Category",
    "description": "Updated sample description",
    "org": "{ORG_ID}",
    "createdBy": "{USER_ID}",
    "createdAt": "1661752268000",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "1661752268000",
    "tagCount": 0
}
```

+++

## Eliminar una categoría de etiqueta específica {#delete-tag-category}

>[!IMPORTANT]
>
>Solo el administrador del sistema y el administrador del producto pueden utilizar esta llamada de API.

Puede eliminar una categoría de etiquetas específica que pertenezca a su organización realizando una solicitud de DELETE a `/tagCategory` y especificando el ID de la categoría de etiqueta.

**Formato de API**

```http
DELETE /tagCategory/{TAG_CATEGORY_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{TAG_CATEGORY_ID}` | El ID de la categoría de etiqueta que está recuperando. |

**Solicitud**

+++Solicitud de ejemplo para eliminar una categoría de etiqueta específica.

```shell
curl -X DELETE https://experience.adobe.io/unifiedtags/tagCategory/e2b7c656-067b-4413-a366-adde0401df50 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 junto con una respuesta vacía.

## Recuperación de una lista de etiquetas {#get-tags}

Puede recuperar una lista de etiquetas que pertenezcan a su organización realizando una solicitud de GET a `/tags` y el ID de la categoría de etiqueta.

**Formato de API**

```http
GET /tags
GET /tags?{QUERY_PARAMETERS}
```

Los siguientes parámetros de consulta opcionales se pueden utilizar al recuperar etiquetas.

| Parámetro de consulta | Descripción | Ejemplo |
| --------------- | ----------- | ------- |
| `start` | Ubicación desde la que comienza la lista de resultados. Puede utilizarlo para indicar el índice inicial para la paginación de los resultados. | `start=a` |
| `limit` | Número máximo de etiquetas que desea recuperar por página. | `limit=20` |
| `property` | Atributo por el que desea filtrar al recuperar etiquetas. Los valores admitidos son:<ul><li>`name`: nombre de la etiqueta.</li><li>`archived`: Si las etiquetas se archivan o no. Puede establecer este valor en `true` o `false`.</li><li>`tagCategoryId`: ID de la categoría de etiqueta a la que pertenece la etiqueta.</li></ul> | <ul><li>`property=name==TestTag`</li><li>`property=archived==false`</li><li>`property=tagCategoryId==e2b7c656-067b-4413-a366-adde0401df50`</li> |
| `sortBy` | Orden por el que se ordenan las etiquetas. Los valores admitidos incluyen `name`, `createdAt`, y `modifiedAt`. | `sortBy=name` |
| `sortOrder` | Dirección por la que se ordenan las categorías de etiquetas. Los valores admitidos incluyen `asc` y `desc`. | `sortOrder=asc` |


**Solicitud**

+++Solicitud de ejemplo para recuperar todas las etiquetas que pertenecen a una categoría de etiqueta específica.

```shell
curl -X GET https://experience.adobe.io/unifiedtags/tags?property=tagCategoryId=e2b7c656-067b-4413-a366-adde0401df50
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles de las etiquetas pertenecientes a esa categoría de etiqueta.

+++ Una respuesta de ejemplo que contiene detalles de las etiquetas solicitadas.

```json
{
    "_page": {
        "count": 166,
        "limit": 10,
        "next": "eyJjb21wb3NpdGVUb2tlbiI6IntcInRva2VuXCI6XCIrUklEOn52a0owQUp3WDRrVko1d0FBQUFBQUFBPT0jUlQ6MiNUUkM6MjAjUlREOnVDTmQyWlAvWjV6TGdvUGVGR1JHQk1KNVExVmR6Mnc9I0lTVjoyI0lFTzo2NTU2NyNRQ0Y6OCNGUEM6QWdFQ0J3TG1BQ1NmQnNBQ0JBb0FBQVFBQ0FBQUNJQVlnQWVBRElBTmdBWEFFTUJCUUVBQUFBQkFRQkdBSElBR2dBQ0FENEFId0FKUkRFQUNBZ2dBUUJnQUVBQUlIb0FaZ0FDQUJNQUFRVUFBUUFCQVFScUFBc0FTQUFBRUxvQU9nQWFBQmNBQVlBQUFHSUlCUUFDQU1vQUlnQWlBQk1DQUFRQUFnZ0FnQUM2QURZQTNnQWlBR1lBQWdCZUFBY0FCZ0JlQUM4QURBQUlBQWdBQVFBQ0FBRUZBQVFFQUFBRWdBQ0FBSjRCR2dBeUFCSUFPZ0F5QU13QVNRQ0FBQUVBdGdCRUFBR0FkZ0FuQUFDZ0NBQUFBQ0lCQUFDSkFnQUJBRUFDQUg0QUhnQWFBQllBVUFFQUNCQUFFQUFRQUF4QUFzUnJBQUlFQUFBYkxoQklIQVBBQUhnUUVBTEVxQUE4RkNBQVFtcUVBd0FBTWd3Y09BSFdIa1FBZ0JGT0FTNEN4QVE0QVwiLFwicmFuZ2VcIjp7XCJtaW5cIjpcIlwiLFwibWF4XCI6XCJGRlwifX0iLCJvcmRlckJ5SXRlbXMiOlt7Iml0ZW0iOjE2OTQ0ODg2MDMwMDB9XSwicmlkIjoidmtKMEFKd1g0a1hHV2dFQUFBQUFBQT09IiwiaW5jbHVzaXZlIjp0cnVlfQ==",
        "property": [
            "tagCategoryId=e2b7c656-067b-4413-a366-adde0401df50"
        ]
    },
    "tags": [
        {
            "archived": false,
            "createdAt": 1705624523000,
            "createdBy": "{USER_ID}",
            "id": "8af14b1e-f267-44ad-b94c-9ac70274e3d5",
            "modifiedAt": 1705624523000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705624481530",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705624523000,
            "createdBy": "{USER_ID}",
            "id": "8b907a2c-0f15-4d2c-9672-bf545d5e47ab",
            "modifiedAt": 1705624523000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705624489131",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705624523000,
            "createdBy": "{USER_ID}",
            "id": "e30bd956-afad-40a1-8f4a-7e4428855856",
            "modifiedAt": 1705624523000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705624494191",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705451722000,
            "createdBy": "{USER_ID}",
            "id": "3bf6a6ba-0b11-4d83-8f35-db6e5b9652d8",
            "modifiedAt": 1705451722000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705451701640",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705422929000,
            "createdBy": "{USER_ID}",
            "id": "0910dfc8-7924-473d-afc6-1aa68337b3b6",
            "modifiedAt": 1705422929000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705422890399",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705394126000,
            "createdBy": "{USER_ID}",
            "id": "b426085e-580b-4147-9921-8ba77ffa77a9",
            "modifiedAt": 1705394126000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705394104556",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": true,
            "createdAt": 1705392795000,
            "createdBy": "{USER_ID}",
            "id": "92961035-e72b-45a0-9625-781380017585",
            "modifiedAt": 1705392832000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705392794917",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705335274000,
            "createdBy": "{USER_ID}",
            "id": "436ce801-ef87-45fd-b34a-9ce938a447e1",
            "modifiedAt": 1705335274000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705335252944",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1694776514000,
            "createdBy": "{USER_ID}",
            "id": "1e6e9836-5e18-4340-a959-3206c9bc3a94",
            "modifiedAt": 1694776514000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1694776510734",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1694488609000,
            "createdBy": "{USER_ID}",
            "id": "b8400673-2f90-48e9-b73b-cdfbba5ab361",
            "modifiedAt": 1694488609000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1694488608301",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        }
    ]
}
```

+++

## Crear una etiqueta nueva {#create-tag}

>[!IMPORTANT]
>
>Solo el administrador del sistema y el administrador del producto pueden utilizar esta llamada de API para crear una nueva etiqueta en una categoría de etiqueta especificada.
>
>Si está creando una etiqueta sin clasificar, debe hacer lo siguiente **no** necesita permisos de administrador.

Puede crear una etiqueta nueva realizando una solicitud de POST a `/tags` punto final.

**Formato de API**

```http
POST /tags
```

**Solicitud**

+++Solicitud de ejemplo para crear una etiqueta nueva.

```shell
curl -X POST https://experience.adobe.io/unifiedtags/tags
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -d '{
    "name": "sampleTag"
 }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `name` | **Requerido**. El nombre de la etiqueta que desea crear. |
| `tagCategoryId` | *Opcional*. El ID de la categoría de etiqueta a la que desea que pertenezca la etiqueta. Si no se especifica, la etiqueta se creará como parte de la categoría Sin categoría. |

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 201 con detalles de la etiqueta recién creada.

+++Una respuesta de ejemplo que contiene detalles de la etiqueta recién creada.

```json
{
    "name": "sampleTag",
    "id": "2bd5ddd9-7284-4767-81d9-c75b122f2a6a",
    "org": "{ORG_ID}",
    "createdAt": "1661753717000",
    "createdBy": "{USER_ID}",
    "modifiedAt": "1661753717000",
    "modifiedBy": "{USER_ID}",
    "tagCategoryId": "Uncategorized-{ORG_ID}",
    "tagCategoryName": "Uncategorized",
    "archived": false
}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `name` | Nombre de la etiqueta recién creada. |
| `id` | El ID de la etiqueta recién creada. |
| `org` | El ID de la organización a la que pertenece la etiqueta. |
| `createdAt` | La marca de tiempo del momento en el que se creó la etiqueta. |
| `createdBy` | El ID del usuario que creó la etiqueta. |
| `modifiedAt` | La marca de tiempo de la última actualización de la etiqueta. |
| `modifiedBy` | El ID del usuario que actualizó la etiqueta por última vez. |
| `tagCategoryId` | El ID de la categoría de etiqueta a la que pertenece la etiqueta. |
| `tagCategoryName` | Nombre de la categoría de etiqueta a la que pertenece la etiqueta. |

+++

## Recuperación de una etiqueta específica {#get-tag}

Puede recuperar una etiqueta específica que pertenezca a su organización realizando una solicitud de GET a `/tags` y especificando el ID de la etiqueta que desea recuperar.

**Formato de API**

```http
GET /tags/{TAG_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{TAG_ID}` | El ID de la etiqueta que está recuperando. |

**Solicitud**

+++Una solicitud de ejemplo para recuperar una etiqueta específica.

```shell
curl -X GET https://experience.adobe.io/unifiedtags/tags/2bd5ddd9-7284-4767-81d9-c75b122f2a6a \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la etiqueta especificada.

+++Respuesta de ejemplo que contiene detalles de la etiqueta especificada.

```json
{
    "name": "sampleTag",
    "id": "2bd5ddd9-7284-4767-81d9-c75b122f2a6a",
    "org": "{ORG_ID}",
    "createdAt": "1661753717000",
    "createdBy": "{USER_ID}",
    "modifiedAt": "1661753717000",
    "modifiedBy": "{USER_ID}",
    "tagCategoryId": "Test Category-{ORG_ID}",
    "tagCategoryName": "Test Category",
    "archived": false
}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `name` | El nombre de la etiqueta que ha recuperado. |
| `id` | El ID de la etiqueta recuperada. |
| `org` | El ID de la organización a la que pertenece la etiqueta. |
| `createdAt` | La marca de tiempo del momento en el que se creó la etiqueta. |
| `createdBy` | El ID del usuario que creó la etiqueta. |
| `modifiedAt` | La marca de tiempo de la última actualización de la etiqueta. |
| `modifiedBy` | El ID del usuario que actualizó la etiqueta por última vez. |
| `tagCategoryId` | El ID de la categoría de etiqueta a la que pertenece la etiqueta. |
| `tagCategoryName` | Nombre de la categoría de etiqueta a la que pertenece la etiqueta. |
| `archived` | El estado de archivo de la etiqueta. Si se establece en `true`, significa que la etiqueta se archiva. |

+++

## Validar etiquetas {#validate-tags}

Puede validar si existen etiquetas realizando una solicitud de POST a `/tags/validate` punto final.

**Formato de API**

```http
POST /tags/validate
```

**Solicitud**

+++Solicitud de ejemplo para validar los ID de etiqueta proporcionados.

```shell
curl -X POST https://experience.adobe.io/unifiedtags/tags/validate
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -d '{
    "ids": [
        "2bd5ddd9-7284-4767-81d9-c75b122f2a6a","d113f40c-0097-4626-8d5f-6d5017694453", "invalid-tag"
    ],
    "entity": "{API_KEY}"
 }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `ids` | Matriz que contiene una lista de los ID de etiqueta que desea validar. |
| `entity` | La entidad que solicita la validación. Puede usar el complemento `{API_KEY}` valor de este parámetro. |

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con información sobre las etiquetas válidas y las no válidas.

+++Respuesta de ejemplo que muestra qué etiquetas son válidas y no válidas.

```json
{
    "invalidTags": [
        {
            "id": "invalid-tag"
        }
    ],
    "validTags": [
        {
            "id": "d113f40c-0097-4626-8d5f-6d5017694453"
        },
        {
            "id": "2bd5ddd9-7284-4767-81d9-c75b122f2a6a"
        }
    ]
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `invalidTags` | Matriz que contiene una lista de los ID de etiqueta no válidos. |
| `validTags` | Matriz que contiene una lista de los ID de etiqueta válidos. |

+++

## Actualizar una etiqueta específica {#update-tag}

Puede actualizar una etiqueta especificada realizando una solicitud de PATCH a `/tags` y proporciona el ID de la etiqueta que desea actualizar.

**Formato de API**

```http
PATCH /tags/{TAG_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{TAG_ID}` | El ID de la etiqueta que está actualizando. |

**Solicitud**

+++Una solicitud de ejemplo para actualizar una etiqueta específica.

```shell
curl -X GET https://experience.adobe.io/unifiedtags/tags/2bd5ddd9-7284-4767-81d9-c75b122f2a6a \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -d '[{
    "op": "replace",
    "path": "name",
    "value": "newSampleTag",
    "from": "sampleTag"
 }]'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `op` | La operación que debe realizarse. En este caso de uso, siempre se establece en `replace`. |
| `path` | La ruta del campo que se actualizará. Los valores admitidos incluyen `name`, `archived`, y `tagCategoryId`. |
| `value` | El valor actualizado del campo que desea actualizar. |
| `from` | El valor original del campo que desea actualizar. |

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la etiqueta recién actualizada.

+++Una respuesta de ejemplo que contiene detalles de la etiqueta actualizada.

```json
{
    "name": "newSampleTag",
    "id": "2bd5ddd9-7284-4767-81d9-c75b122f2a6a",
    "org": "{ORG_ID}",
    "createdAt": "1661753717000",
    "createdBy": "{USER_ID}",
    "modifiedAt": "1661753717000",
    "modifiedBy": "{USER_ID}",
    "tagCategoryId": "Test Category-{ORG_ID}",
    "tagCategoryName": "Test Category",
    "archived": false
}
```

+++

## Eliminar una etiqueta específica {#delete-tag}

>[!IMPORTANT]
>
>Solo el administrador del sistema y el administrador del producto pueden utilizar esta llamada de API.
>
>Además, la etiqueta **no puede** estar asociado a cualquier objeto comercial y **debe** se archivarán antes de poder eliminar la etiqueta. Puede archivar la etiqueta utilizando la variable [actualizar extremo de etiqueta](#update-tag).

Para borrar una etiqueta específica, cree una etiqueta de DELETE en la `/tags` y especificando el ID de la etiqueta que desea eliminar.

**Formato de API**

```http
DELETE /tags/{TAG_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{TAG_ID}` | El ID de la etiqueta que está eliminando. |

**Solicitud**

+++Solicitud de ejemplo para eliminar una etiqueta específica

```shell
curl -X DELETE https://experience.adobe.io/unifiedtags/tags/2bd5ddd9-7284-4767-81d9-c75b122f2a6a \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 junto con una respuesta vacía.

## Pasos siguientes

Después de leer esta guía, tiene una mejor comprensión de cómo crear, administrar y eliminar etiquetas y categorías de etiquetas mediante las API de Adobe Experience Platform. Para obtener más información sobre la administración de etiquetas mediante la IU, lea la [guía de administración de etiquetas](../ui/managing-tags.md). Para obtener más información sobre la administración de categorías de etiquetas mediante la IU, lea la [guía de categorías de etiquetas](../ui/tags-categories.md).
