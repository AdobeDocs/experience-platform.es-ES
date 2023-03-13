---
keywords: Experience Platform;inicio;temas populares;api;Control de acceso basado en atributos;control de acceso basado en atributos
solution: Experience Platform
title: Extremo de API de productos
description: El extremo /products de la API de control de acceso basado en atributos le permite administrar productos mediante programación en Adobe Experience Platform.
exl-id: 44ee9a9d-7a13-4d59-a1a9-97764dbd3763
source-git-commit: 16d85a2a4ee8967fc701a3fe631c9daaba9c9d70
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 4%

---

# Extremo de productos

>[!NOTE]
>
>Si se pasa un token de usuario, el usuario del token debe tener un rol de &quot;administrador de organización&quot; para la organización solicitada.

El `/products` Este extremo de la API de control de acceso basado en atributos le permite administrar mediante programación productos, así como categorías de permisos y conjuntos de permisos asociados a productos de su organización.

## Primeros pasos

El extremo de API utilizado en esta guía forma parte de la API de control de acceso basada en atributos. Antes de continuar, consulte la [guía de introducción](./getting-started.md) para obtener vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios para realizar correctamente llamadas a cualquier API de Experience Platform.

## Recuperación de una lista de productos con derechos {#list}

Puede recuperar una lista de productos autorizados realizando una solicitud de GET a `/products` punto final.

**Formato de API**

```http
GET /products/
```

**Solicitud**

La siguiente solicitud recupera una lista de productos autorizados que pertenecen a su organización.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/products \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Respuesta**

Una respuesta correcta devuelve una lista de productos con derechos que pertenecen a su organización.

```json
{
  "products": [
    {
      "id": "{ID}",
      "name": "Adobe Experience Platform",
      "serviceCode": "{SERVICE_CODE}"
    }
  ]
}
```

| Propiedad | Descripción |
| --- | --- |
| `id` | El ID correspondiente del producto consultado. |
| `name` | El nombre del producto consultado. |
| `serviceCode` | El código de servicio correspondiente del producto consultado. |

## Búsqueda de categorías de permisos por ID de producto

Puede buscar las categorías de permisos de un producto determinado realizando una solicitud de GET a `/products/{PRODUCT_ID}/categories` al especificar su ID de producto.

**Formato de API**

```http
GET /products/{PRODUCT_ID}/categories
```

| Parámetro | Descripción |
| --- | --- |
| {PRODUCT_ID} | El ID del producto asociado con las categorías de permisos que desea buscar. |

**Solicitud**

La siguiente solicitud recupera las categorías de permisos asociadas con `{PRODUCT_ID}`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/products/{PRODUCT_ID}/categories \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Respuesta**

Una respuesta correcta devuelve las categorías de permisos asociadas con el ID de producto que ha consultado.

```json
{
  "categories": [
    {
        "name": "Profile Management"
    },
    {
        "name": "Data Ingestion"
    },
    {
        "name": "Sandbox Administration"
    },
    {
        "name": "Query Service"
    },
    {
        "name": "Data Management"
    },
    {
        "name": "Identity Management"
    },
    {
        "name": "Data Modeling"
    },
    {
        "name": "Data Science Workspace"
    },
    {
        "name": "Dashboards"
    },
    {
        "name": "Alerts"
    },
    {
        "name": "Data Governance"
    }
  ]
}
```

| Propiedad | Descripción |
| --- | --- |
| `category` | Las categorías de permisos disponibles dentro del ID de producto consultado. |
| `name` | Nombre de la categoría de permisos. |

## Búsqueda de conjuntos de permisos por ID de producto

Puede buscar conjuntos de permisos para un producto determinado realizando una solicitud de GET a `/products/{PRODUCT_ID}/permission-sets` al especificar su ID de producto.

**Formato de API**

```http
GET /products/{PRODUCT_ID}/permission-sets
```

| Parámetro | Descripción |
| --- | --- |
| {PRODUCT_ID} | El ID del producto asociado con los conjuntos de permisos que desea buscar. |

**Solicitud**

La siguiente solicitud recupera los conjuntos de permisos asociados a `{PRODUCT_ID}`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/products/{PRODUCT_ID}/permission-sets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Respuesta**

Una respuesta correcta devuelve los conjuntos de permisos asociados al ID de producto que ha consultado.

```json
{
  "permission-sets": [
      {
          "id": "manage-schemas",
          "name": "Manage Schemas",
          "category": "Data Modeling",
          "permissions": [
              {
                  "resource": "schemas",
                  "actions": [
                      "read",
                      "write",
                      "delete"
                  ]
              },
              {
                  "resource": "schema-fields",
                  "actions": [
                      "read",
                      "write",
                      "delete"
                  ]
              },
              {
                  "resource": "sandboxes",
                  "actions": [
                      "view"
                  ]
              }
          ]
      },
      {
          "id": "view-schemas",
          "name": "View Schemas",
          "category": "Data Modeling",
          "permissions": [
              {
                  "resource": "schemas",
                  "actions": [
                      "read"
                  ]
              },
              {
                  "resource": "schema-fields",
                  "actions": [
                      "read"
                  ]
              },
              {
                  "resource": "sandboxes",
                  "actions": [
                      "view"
                  ]
              }
          ]
      },
  ]
}
```

| Propiedad | Descripción |
| --- | --- |
| `permission-sets` | Los conjuntos de permisos representan un grupo de permisos que un administrador puede aplicar a una función. Un administrador puede asignar conjuntos de permisos a una función, en lugar de asignar permisos individuales. Esto le permite crear funciones personalizadas a partir de una función predefinida que contiene un grupo de permisos. |
| `id` | El ID correspondiente del conjunto de permisos consultado. |
| `name` | El nombre correspondiente del conjunto de permisos consultado. |
| `category` | La categoría de permisos disponible. |
| `permissions` | Los permisos incluyen la capacidad de ver o utilizar funciones de Platform, como crear entornos limitados, definir esquemas y administrar conjuntos de datos. |
| `permissions.resource` | Recurso u objeto al que puede tener acceso o al que no puede tener acceso un sujeto. Los recursos pueden ser archivos, aplicaciones, servidores o incluso API. |
| `permissions.actions` | Acción que un sujeto puede realizar contra un recurso consultado. Los valores posibles incluyen: `view`, `read`, `create`, `edit`, y `delete` |
