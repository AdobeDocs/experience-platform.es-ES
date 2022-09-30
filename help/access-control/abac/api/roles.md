---
keywords: Experience Platform;inicio;temas populares;api;Control de acceso basado en atributos;control de acceso basado en atributos
solution: Experience Platform
title: Punto final de la API de roles
description: El extremo /roles de la API de control de acceso basado en atributos le permite administrar roles mediante programación en Adobe Experience Platform.
exl-id: 049f7a18-7d06-437b-8ce9-25d7090ba782
source-git-commit: 9e44e647e4647a323fa9d1af55266d6f32b5ccb9
workflow-type: tm+mt
source-wordcount: '1583'
ht-degree: 4%

---

# Punto de conexión de roles

Las funciones definen el acceso que un administrador, un especialista o un usuario final tiene a los recursos de su organización. En un entorno de control de acceso basado en roles, el aprovisionamiento de acceso de los usuarios se agrupa a través de responsabilidades y necesidades comunes. Una función tiene un conjunto determinado de permisos y los miembros de su organización pueden asignarse a una o más funciones, según el ámbito de vista o acceso de escritura que necesiten.

La variable `/roles` en la API de control de acceso basada en atributos le permite administrar mediante programación las funciones de su organización.

## Primeros pasos

El extremo de API utilizado en esta guía forma parte de la API de control de acceso basada en atributos. Antes de continuar, revise la [guía de introducción](./getting-started.md) para ver vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios para realizar llamadas correctamente a cualquier API de Experience Platform.

## Recuperar una lista de funciones {#list}

Puede enumerar todas las funciones existentes que pertenezcan a su organización realizando una solicitud de GET al `/roles` punto final.

**Formato de API**

```http
GET /roles/
```

**Solicitud**

La siguiente solicitud recupera una lista de funciones pertenecientes a su organización.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/roles \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Respuesta**

Una respuesta correcta devuelve una lista de funciones de su organización, incluida información sobre su tipo de función, conjuntos de permisos y atributos de asunto respectivos.

```json
{
  "roles": [
    {
      "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
      "name": "Administrator Role",
      "description": "Role for administrator type of responsibilities and access",
      "roleType": "user-defined",
      "permissionSets": [
        "manage-datasets",
        "manage-schemas"
      ],
      "sandboxes": [
        "prod"
      ],
      "subjectAttributes": {
        "labels": [
          "core/S1"
        ]
      },
      "createdBy": "{CREATED_BY}",
      "createdAt": 1648153201825,
      "modifiedBy": "{MODIFIED_BY}",
      "modifiedAt": 1648153201825,
      "etag": null
    }
  ],
  "_page": {
    "limit": 1,
    "count": 1
  },
  "_links": {
    "next": {
      "href": "https://platform.adobe.io:443/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
      "templated": true
    },
    "page": {
      "href": "https://platform.adobe.io:443/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
      "templated": true
    },
    "subjects": {
      "href": "https://platform.adobe.io:443/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
      "templated": true
    }
  }
}
```

| Propiedad | Descripción |
| --- | --- |
| `id` | El ID que corresponde a la función. Este ID se genera automáticamente. |
| `name` | Nombre de su función. |
| `description` | La propiedad description proporciona información adicional sobre su función. |
| `roleType` | Tipo designado de la función. Los valores posibles para el tipo de función son: `user-defined` y `system-defined`. |
| `permissionSets` | Los conjuntos de permisos representan un grupo de permisos que un administrador puede aplicar a una función. Un administrador puede asignar conjuntos de permisos a una función, en lugar de asignar permisos individuales. Esto le permite crear funciones personalizadas a partir de una función predefinida que contenga un grupo de permisos. |
| `sandboxes` | Esta propiedad muestra los entornos limitados de su organización que están aprovisionados para una función en particular. |
| `subjectAttributes` | Atributos que indican la correlación entre un asunto y los recursos de Platform a los que tienen acceso. |
| `subjectAttributes.labels` | Muestra las etiquetas de uso de datos aplicadas a la función consultada. |

## Buscar una función {#lookup}

Puede buscar una función individual realizando una solicitud de GET que incluya la `roleId` en la ruta de solicitud.

**Formato de API**

```http
GET /roles/{ROLE_ID}
```

| Parámetro | Descripción |
| --- | --- |
| {ROLE_ID} | El ID de la función que desea buscar. |

**Solicitud**

La siguiente solicitud recupera información para `{ROLE_ID}`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Respuesta**

Una respuesta correcta devuelve detalles para el ID de función consultado, incluida información sobre su tipo de función, conjuntos de permisos y atributos del asunto.

```json
{
  "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
  "name": "Administrator Role",
  "description": "Role for administrator type of responsibilities and access",
  "roleType": "user-defined",
  "permissionSets": [
    "manage-datasets",
    "manage-schemas"
  ],
  "sandboxes": [
    "prod"
  ],
  "subjectAttributes": {
    "labels": [
      "core/S1"
    ]
  },
  "createdBy": "{CREATED_BY}",
  "createdAt": 1648153201825,
  "modifiedBy": "{MODIFIED_BY}",
  "modifiedAt": 1648153201825,
  "etag": null
}
```

| Propiedad | Descripción |
| --- | --- |
| `id` | El ID que corresponde a la función. Este ID se genera automáticamente. |
| `name` | Nombre de su función. |
| `description` | La propiedad description proporciona información adicional sobre su función. |
| `roleType` | Tipo designado de la función. Los valores posibles para el tipo de función son: `user-defined` y `system-defined`. |
| `permissionSets` | Los conjuntos de permisos representan un grupo de permisos que un administrador puede aplicar a una función. Un administrador puede asignar conjuntos de permisos a una función, en lugar de asignar permisos individuales. Esto le permite crear funciones personalizadas a partir de una función predefinida que contenga un grupo de permisos. |
| `sandboxes` | Esta propiedad muestra los entornos limitados de su organización que están aprovisionados para una función en particular. |
| `subjectAttributes` | Atributos que indican la correlación entre un asunto y los recursos de Platform a los que tienen acceso. |
| `subjectAttributes.labels` | Muestra las etiquetas de uso de datos aplicadas a la función consultada. |

## Buscar temas por ID de rol

También puede recuperar los sujetos realizando una solicitud de GET a la variable `/roles` al proporcionar un {ROLE_ID}.

**Formato de API**

```http
GET /roles/{ROLE_ID}/subjects
```

| Parámetro | Descripción |
| --- | --- |
| {ROLE_ID} | El ID de la función asociada a los temas que desea buscar. |

**Solicitud**

La siguiente solicitud recupera los sujetos asociados con `3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809/subjects \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Respuesta**

Una respuesta correcta devuelve los asuntos asociados con el ID de función consultado, incluido el ID de asunto y el tipo de asunto correspondientes.

```json
{
  "items": [
      {
          "roleId": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
          "subjectType": "user",
          "subjectId": "03Z07HFQCCUF3TUHAX274206@AdobeID"
      },
      {
          "roleId": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
          "subjectType": "user",
          "subjectId": "PIRJ7WE5T3QT9Z4TCLVH86DE@AdobeID"
      },
      {
          "roleId": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
          "subjectType": "user",
          "subjectId": "WHPWE00MC26SHZ7AKBFG403D@AdobeID"
      },
  ]
  "_page": {
    "limit": 0,
    "count": 0
  },
  "_links": {
      "self": {
          "href": "/roles/{ROLE_ID}/subjects",
          "templated": false,
          "type": null,
          "method": null
      },
      "page": {
          "href": "/roles/{ROLE_ID}/subjects?limit={limit}&start={start}&orderBy={orderBy}&property={property}",
          "templated": true,
          "type": null,
          "method": null
      }
  }
}
```

| Propiedad | Descripción |
| --- | --- |
| `roleId` | El ID de función asociado al asunto consultado. |
| `subjectType` | Tipo del asunto que se consulta. |
| `subjectId` | El ID que corresponde al asunto consultado. |

## Crear una función {#create}

Para crear una función nueva, realice una solicitud de POST al `/roles` al proporcionar valores para el nombre, la descripción y el tipo de rol de su rol.

**Formato de API**

```http
POST /roles/
```

**Solicitud**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/access-control/administration/roles \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
    "name": "Administrator Role",
    "description": "Role for administrator type of responsibilities and access",
    "roleType": "user-defined"
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `name` | Nombre de su función. Asegúrese de que el nombre de su función sea descriptivo, ya que puede utilizarlo para buscar información sobre su función. |
| `description` | (Opcional) Un valor descriptivo que puede incluir para proporcionar más información sobre su función. |
| `roleType` | Tipo designado de la función. Los valores posibles para el tipo de función son: `user-defined` y `system-defined`. |

**Respuesta**

Una respuesta correcta devuelve la función recién creada, con su ID de función correspondiente, así como información sobre su tipo de función, conjuntos de permisos y atributos de asunto.

```json
{
  "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
  "name": "Administrator Role",
  "description": "Role for administrator type of responsibilities and access",
  "roleType": "user-defined",
  "permissionSets": [
    "manage-datasets",
    "manage-schemas"
  ],
  "sandboxes": [
    "prod"
  ],
  "subjectAttributes": {
    "labels": [
      "core/S1"
    ]
  },
  "createdBy": "{CREATED_BY}",
  "createdAt": 1648153201825,
  "modifiedBy": "{MODIFIED_BY}",
  "modifiedAt": 1648153201825,
  "etag": null
}
```

| Propiedad | Descripción |
| --- | --- |
| `id` | El ID que corresponde a la función. Este ID se genera automáticamente. |
| `name` | Nombre de su función. |
| `description` | La propiedad description proporciona información adicional sobre su función. |
| `roleType` | Tipo designado de la función. Los valores posibles para el tipo de función son: `user-defined` y `system-defined`. |
| `permissionSets` | Los conjuntos de permisos representan un grupo de permisos que un administrador puede aplicar a una función. Un administrador puede asignar conjuntos de permisos a una función, en lugar de asignar permisos individuales. Esto le permite crear funciones personalizadas a partir de una función predefinida que contenga un grupo de permisos. |
| `sandboxes` | Esta propiedad muestra los entornos limitados de su organización que están aprovisionados para una función en particular. |
| `subjectAttributes` | Atributos que indican la correlación entre un asunto y los recursos de Platform a los que tienen acceso. |
| `subjectAttributes.labels` | Muestra las etiquetas de uso de datos aplicadas a la función consultada. |

## Actualizar una función {#patch}

Puede actualizar las propiedades de una función realizando una solicitud de PATCH al `/roles` al proporcionar el ID de rol y los valores correspondientes para las operaciones que desea aplicar.

**Formato de API**

```http
PATCH /roles/{ROLE_ID}
```

| Parámetro | Descripción |
| --- | --- |
| {ROLE_ID} | El ID de la función que desea actualizar. |

**Solicitud**

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/{ROLE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
    "operations": [
      {
        "op": "add",
        "path": "/description",
        "value": "Role with permission sets for admin type of access"
      }
    ]
  }'
```

| Operaciones | Descripción |
| --- | --- |
| `op` | La llamada de operación utilizada para definir la acción necesaria para actualizar la función. Las operaciones incluyen: `add`, `replace`y `remove`. |
| `path` | Ruta del parámetro que se va a actualizar. |
| `value` | El nuevo valor con el que desea actualizar el parámetro. |

**Respuesta**

Una respuesta correcta devuelve la función actualizada, incluidos los nuevos valores para las propiedades que eligió actualizar.

```json
{
  "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
  "name": "Administrator Role",
  "description": "Role with permission sets for admin type of access",
  "roleType": "user-defined",
  "permissionSets": [
    "manage-datasets",
    "manage-schemas"
  ],
  "sandboxes": [
    "prod"
  ],
  "subjectAttributes": {
    "labels": [
      "core/S1"
    ]
  },
  "createdBy": "{CREATED_BY}",
  "createdAt": 1648153201825,
  "modifiedBy": "{MODIFIED_BY}",
  "modifiedAt": 1648153201825,
  "etag": null
}
```

| Propiedad | Descripción |
| --- | --- |
| `id` | El ID que corresponde a la función. Este ID se genera automáticamente. |
| `name` | Nombre de su función. |
| `description` | La propiedad description proporciona información adicional sobre su función. |
| `roleType` | Tipo designado de la función. Los valores posibles para el tipo de función son: `user-defined` y `system-defined`. |
| `permissionSets` | Los conjuntos de permisos representan un grupo de permisos que un administrador puede aplicar a una función. Un administrador puede asignar conjuntos de permisos a una función, en lugar de asignar permisos individuales. Esto le permite crear funciones personalizadas a partir de una función predefinida que contenga un grupo de permisos. |
| `sandboxes` | Esta propiedad muestra los entornos limitados de su organización que están aprovisionados para una función en particular. |
| `subjectAttributes` | Atributos que indican la correlación entre un asunto y los recursos de Platform a los que tienen acceso. |
| `subjectAttributes.labels` | Muestra las etiquetas de uso de datos aplicadas a la función consultada. |

## Actualizar una función por ID de función {#put}

Puede actualizar una función realizando una solicitud de PUT al `/roles` y especificar el ID de función que corresponde a la función que desea actualizar.

**Formato de API**

```http
PUT /roles/{ROLE_ID}
```

**Solicitud**

La siguiente solicitud actualiza el nombre, la descripción y el tipo de función del ID de rol: `3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809`.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
    "name": "Administrator role for ACME",
    "description": "New administrator role for ACME",
    "roleType": "user-defined"
  }'
```

| Parámetro | Descripción |
| --- | --- |
| `name` | Nombre actualizado de una función. |
| `description` | La descripción actualizada de una función. |
| `roleType` | Tipo designado de la función. Los valores posibles para el tipo de función son: `user-defined` y `system-defined`. |

**Respuesta**

Si la función se ejecuta correctamente, se incluirán nuevos valores para su nombre, descripción y tipo de función.

```json
{
  "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
  "name": "Administrator Role",
  "description": "Role with permission sets for admin type of access",
  "roleType": "user-defined",
  "permissionSets": [
    "manage-datasets",
    "manage-schemas"
  ],
  "sandboxes": [
    "prod"
  ],
  "subjectAttributes": {
    "labels": [
      "core/S1"
    ]
  },
  "createdBy": "{CREATED_BY}",
  "createdAt": 1648153201825,
  "modifiedBy": "{MODIFIED_BY}",
  "modifiedAt": 1648153201825,
  "etag": null
}
```

| Propiedad | Descripción |
| --- | --- |
| `id` | El ID que corresponde a la función. Este ID se genera automáticamente. |
| `name` | Nombre de su función. |
| `description` | La propiedad description proporciona información adicional sobre su función. |
| `roleType` | Tipo designado de la función. Los valores posibles para el tipo de función son: `user-defined` y `system-defined`. |
| `permissionSets` | Los conjuntos de permisos representan un grupo de permisos que un administrador puede aplicar a una función. Un administrador puede asignar conjuntos de permisos a una función, en lugar de asignar permisos individuales. Esto le permite crear funciones personalizadas a partir de una función predefinida que contenga un grupo de permisos. |
| `sandboxes` | Esta propiedad muestra los entornos limitados de su organización que están aprovisionados para una función en particular. |
| `subjectAttributes` | Atributos que indican la correlación entre un asunto y los recursos de Platform a los que tienen acceso. |
| `subjectAttributes.labels` | Muestra las etiquetas de uso de datos aplicadas a la función consultada. |

## Actualizar asunto por ID de función

Para actualizar los temas asociados a una función, realice una solicitud de PATCH a la variable `/roles` al proporcionar el ID de función de los sujetos que desea actualizar.

**Formato de API**

```http
PATCH /roles/{ROLE_ID}
```

| Parámetro | Descripción |
| --- | --- |
| {ROLE_ID} | El ID de la función asociada a los temas que desea actualizar. |

**Solicitud**

La siguiente solicitud actualiza los temas asociados con `{ROLE_ID}`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/{ROLE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
    "operations": [
      {
        "op": "add",
        "path": "/subjects",
        "value": "New subjects"
      }
    ]
  }'
```

| Operaciones | Descripción |
| --- | --- |
| `op` | La llamada de operación utilizada para definir la acción necesaria para actualizar la función. Las operaciones incluyen: `add`, `replace`y `remove`. |
| `path` | Ruta del parámetro que se va a actualizar. |
| `value` | El nuevo valor con el que desea actualizar el parámetro. |

**Respuesta**

Una respuesta correcta devuelve los temas actualizados asociados con el ID de rol consultado.

```json
{
  "subjects": [
    {
      "subjectId": "string",
      "subjectType": "user"
    }
  ],
  "_page": {
    "limit": 0,
    "count": 0
  },
  "_links": {
    "next": {
      "href": "string",
      "templated": true
    },
    "page": {
      "href": "string",
      "templated": true
    }
  }
}
```

| Propiedad | Descripción |
| --- | --- |
| `subjectId` | El ID de un asunto. |
| `subjectType` | Tipo de asunto. |

## Eliminar una función {#delete}

Para eliminar una función, realice una solicitud de DELETE al `/roles` al especificar el ID de la función que desea eliminar.

**Formato de API**

```http
DELETE /roles/{ROLE_ID}
```

| Parámetro | Descripción |
| --- | --- |
| {ROLE_ID} | El ID de la función que desea eliminar. |

**Solicitud**

La siguiente solicitud elimina la función con el ID de `{ROLE_ID}`.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/{ROLE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 204 (sin contenido) y un cuerpo en blanco.

Puede confirmar la eliminación intentando realizar una solicitud de búsqueda (GET) al rol. Recibirá un estado HTTP 404 (no encontrado) porque la función se ha eliminado de la administración.
