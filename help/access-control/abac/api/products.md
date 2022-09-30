---
keywords: Experience Platform;inicio;temas populares;api;Control de acceso basado en atributos;control de acceso basado en atributos
solution: Experience Platform
title: Punto final de la API de productos
description: El extremo /products de la API de control de acceso basado en atributos le permite administrar productos mediante programación en Adobe Experience Platform.
exl-id: 44ee9a9d-7a13-4d59-a1a9-97764dbd3763
source-git-commit: 9e44e647e4647a323fa9d1af55266d6f32b5ccb9
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 4%

---

# Punto final del producto

La variable `/products` en la API de control de acceso basada en atributos le permite administrar mediante programación productos, así como categorías de permisos y conjuntos de permisos asociados con productos de su organización.

## Primeros pasos

El extremo de API utilizado en esta guía forma parte de la API de control de acceso basada en atributos. Antes de continuar, revise la [guía de introducción](./getting-started.md) para ver vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios para realizar llamadas correctamente a cualquier API de Experience Platform.

## Recuperar una lista de productos autorizados {#list}

Puede recuperar una lista de productos con derecho realizando una solicitud de GET al `/products` punto final.

**Formato de API**

```http
GET /products/
```

**Solicitud**

La siguiente solicitud recupera una lista de productos con derecho que pertenecen a su organización.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/products \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Respuesta**

Una respuesta correcta devuelve una lista de los productos con derecho que pertenecen a su organización.

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
| `name` | Nombre del producto consultado. |
| `serviceCode` | El código de servicio correspondiente del producto consultado. |

## Buscar categorías de permisos por ID de producto

Puede buscar categorías de permisos para un producto determinado realizando una solicitud de GET al `/products/{PRODUCT_ID}/categories` al especificar el ID del producto.

**Formato de API**

```http
GET /products/{PRODUCT_ID}/categories
```

| Parámetro | Descripción |
| --- | --- |
| {PRODUCT_ID} | El ID del producto asociado con las categorías de permisos que desea buscar. |

**Solicitud**

La siguiente solicitud recupera categorías de permisos asociadas con `{PRODUCT_ID}`.

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
| `category` | Categorías de permisos disponibles dentro del ID de producto consultado. |
| `name` | Nombre de la categoría de permisos. |

## Buscar conjuntos de permisos por ID de producto

Puede buscar conjuntos de permisos para un producto determinado realizando una solicitud de GET al `/products/{PRODUCT_ID}/permission-sets` al especificar el ID del producto.

**Formato de API**

```http
GET /products/{PRODUCT_ID}/permission-sets
```

| Parámetro | Descripción |
| --- | --- |
| {PRODUCT_ID} | El ID del producto asociado con los conjuntos de permisos que desea buscar. |

**Solicitud**

La siguiente solicitud recupera conjuntos de permisos asociados con `{PRODUCT_ID}`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/products/{PRODUCT_ID}/permission-sets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Respuesta**

Una respuesta correcta devuelve los conjuntos de permisos asociados con el ID de producto que ha consultado.

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
| `permission-sets` | Los conjuntos de permisos representan un grupo de permisos que un administrador puede aplicar a una función. Un administrador puede asignar conjuntos de permisos a una función, en lugar de asignar permisos individuales. Esto le permite crear funciones personalizadas a partir de una función predefinida que contenga un grupo de permisos. |
| `id` | El ID correspondiente del conjunto de permisos consultado. |
| `name` | El nombre correspondiente del conjunto de permisos consultado. |
| `category` | La categoría de permisos disponibles. |
| `permissions` | Los permisos incluyen la capacidad de ver o usar funciones de Platform, como la creación de entornos limitados, la definición de esquemas y la administración de conjuntos de datos. |
| `permissions.resource` | Recurso u objeto al que puede acceder o no un sujeto. Los recursos pueden ser archivos, aplicaciones, servidores o incluso API. |
| `permissions.actions` | Acción que un sujeto puede realizar contra un recurso consultado. Los valores posibles incluyen: `view`, `read`, `create`, `edit`y `delete` |
