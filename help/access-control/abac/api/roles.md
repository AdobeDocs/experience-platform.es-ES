---
keywords: Experience Platform;inicio;temas populares;api;Control de acceso basado en atributos;control de acceso basado en atributos
solution: Experience Platform
title: Extremo de API de roles
description: El extremo /roles de la API de control de acceso basado en atributos le permite administrar los roles mediante programación en Adobe Experience Platform.
role: Developer
exl-id: 049f7a18-7d06-437b-8ce9-25d7090ba782
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1670'
ht-degree: 7%

---

# Extremo de roles

>[!NOTE]
>
>Si se pasa un token de usuario, el usuario del token debe tener un rol de &quot;administrador de organización&quot; para la organización solicitada.

Las funciones definen el acceso que un administrador, un especialista o un usuario final tiene a los recursos de su organización. En un entorno de control de acceso basado en funciones, el aprovisionamiento de acceso de los usuarios se agrupa a través de responsabilidades y necesidades comunes. Una función tiene un conjunto determinado de permisos y a los miembros de su organización se les puede asignar una o más funciones, según el ámbito de vista o acceso de escritura que necesiten.

El extremo `/roles` de la API de control de acceso basado en atributos le permite administrar mediante programación los roles de su organización.

## Introducción

El extremo de API utilizado en esta guía forma parte de la API de control de acceso basada en atributos. Antes de continuar, revisa la [guía de introducción](./getting-started.md) para ver vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios para realizar correctamente llamadas a cualquier API de Experience Platform.

## Recuperación de una lista de funciones {#list}

Puede enumerar todos los roles existentes que pertenecen a su organización realizando una petición GET al extremo `/roles`.

**Formato de API**

```http
GET /roles/
```

**Solicitud**

La siguiente solicitud recupera una lista de funciones que pertenecen a su organización.

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
| `name` | El nombre de su función. |
| `description` | La propiedad description proporciona información adicional sobre la función. |
| `roleType` | El tipo designado de la función. Los valores posibles para el tipo de rol son: `user-defined` y `system-defined`. |
| `permissionSets` | Los conjuntos de permisos representan un grupo de permisos que un administrador puede aplicar a una función. Un administrador puede asignar conjuntos de permisos a una función, en lugar de asignar permisos individuales. Esto le permite crear funciones personalizadas a partir de una función predefinida que contiene un grupo de permisos. |
| `sandboxes` | Esta propiedad muestra los entornos limitados de su organización que se han aprovisionado para una función concreta. |
| `subjectAttributes` | Atributos que indican la correlación entre un asunto y los recursos de Experience Platform a los que tienen acceso. |
| `subjectAttributes.labels` | Muestra las etiquetas de uso de datos aplicadas a la función consultada. |

## Búsqueda de un rol {#lookup}

Puede buscar un rol individual realizando una petición GET que incluya el(la) `roleId` correspondiente en la ruta de solicitud.

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

Una respuesta correcta devuelve detalles del ID de rol consultado, incluida información sobre su tipo de rol, conjuntos de permisos y atributos de asunto.

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
| `name` | El nombre de su función. |
| `description` | La propiedad description proporciona información adicional sobre la función. |
| `roleType` | El tipo designado de la función. Los valores posibles para el tipo de rol son: `user-defined` y `system-defined`. |
| `permissionSets` | Los conjuntos de permisos representan un grupo de permisos que un administrador puede aplicar a una función. Un administrador puede asignar conjuntos de permisos a una función, en lugar de asignar permisos individuales. Esto le permite crear funciones personalizadas a partir de una función predefinida que contiene un grupo de permisos. |
| `sandboxes` | Esta propiedad muestra los entornos limitados de su organización que se han aprovisionado para una función concreta. |
| `subjectAttributes` | Atributos que indican la correlación entre un asunto y los recursos de Experience Platform a los que tienen acceso. |
| `subjectAttributes.labels` | Muestra las etiquetas de uso de datos aplicadas a la función consultada. |

## Búsqueda de asuntos por ID de función

También puede recuperar sujetos realizando una petición GET al extremo `/roles` mientras proporciona un {ROLE_ID}.

**Formato de API**

```http
GET /roles/{ROLE_ID}/subjects
```

| Parámetro | Descripción |
| --- | --- |
| {ROLE_ID} | El ID de la función asociada a los asuntos que desea buscar. |

**Solicitud**

La siguiente solicitud recupera los asuntos asociados con `3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809/subjects \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Respuesta**

Una respuesta correcta devuelve los asuntos asociados con el ID de rol consultado, incluidos el ID de asunto y el tipo de asunto correspondientes.

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
| `roleId` | El ID de rol asociado con el asunto consultado. |
| `subjectType` | El tipo del asunto consultado. |
| `subjectId` | El ID que corresponde al asunto consultado. |

## Crear una función {#create}

Para crear una función nueva, realice una petición POST al extremo `/roles` y proporcione valores para el nombre, la descripción y el tipo de función de la función.

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
| `name` | El nombre de su función. Asegúrese de que el nombre de la función sea descriptivo, ya que puede utilizarlo para buscar información sobre la función. |
| `description` | (Opcional) Un valor descriptivo que puede incluir para proporcionar más información sobre la función. |
| `roleType` | El tipo designado de la función. Los valores posibles para el tipo de rol son: `user-defined` y `system-defined`. |

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
| `name` | El nombre de su función. |
| `description` | La propiedad description proporciona información adicional sobre la función. |
| `roleType` | El tipo designado de la función. Los valores posibles para el tipo de rol son: `user-defined` y `system-defined`. |
| `permissionSets` | Los conjuntos de permisos representan un grupo de permisos que un administrador puede aplicar a una función. Un administrador puede asignar conjuntos de permisos a una función, en lugar de asignar permisos individuales. Esto le permite crear funciones personalizadas a partir de una función predefinida que contiene un grupo de permisos. |
| `sandboxes` | Esta propiedad muestra los entornos limitados de su organización que se han aprovisionado para una función concreta. |
| `subjectAttributes` | Atributos que indican la correlación entre un asunto y los recursos de Experience Platform a los que tienen acceso. |
| `subjectAttributes.labels` | Muestra las etiquetas de uso de datos aplicadas a la función consultada. |

## Actualizar un rol {#patch}

Puede actualizar las propiedades de un rol realizando una petición PATCH al extremo `/roles` y proporcionando al mismo tiempo el ID de rol y los valores correspondientes para las operaciones que desee aplicar.

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
| `op` | La llamada de operación utilizada para definir la acción necesaria para actualizar la función. Las operaciones incluyen: `add`, `replace` y `remove`. |
| `path` | Ruta del parámetro que se va a actualizar. |
| `value` | El nuevo valor con el que desea actualizar el parámetro. |

**Respuesta**

Una respuesta correcta devuelve la función actualizada, incluidos los nuevos valores de las propiedades que eligió actualizar.

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
| `name` | El nombre de su función. |
| `description` | La propiedad description proporciona información adicional sobre la función. |
| `roleType` | El tipo designado de la función. Los valores posibles para el tipo de rol son: `user-defined` y `system-defined`. |
| `permissionSets` | Los conjuntos de permisos representan un grupo de permisos que un administrador puede aplicar a una función. Un administrador puede asignar conjuntos de permisos a una función, en lugar de asignar permisos individuales. Esto le permite crear funciones personalizadas a partir de una función predefinida que contiene un grupo de permisos. |
| `sandboxes` | Esta propiedad muestra los entornos limitados de su organización que se han aprovisionado para una función concreta. |
| `subjectAttributes` | Atributos que indican la correlación entre un asunto y los recursos de Experience Platform a los que tienen acceso. |
| `subjectAttributes.labels` | Muestra las etiquetas de uso de datos aplicadas a la función consultada. |

## Actualizar un rol por identificador de rol {#put}

Puede actualizar un rol realizando una petición PUT al extremo `/roles` y especificando el identificador de rol que corresponde al rol que desea actualizar.

**Formato de API**

```http
PUT /roles/{ROLE_ID}
```

**Solicitud**

La siguiente solicitud actualiza el nombre, la descripción y el tipo de rol para el identificador de rol: `3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809`.

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
| `description` | La descripción actualizada de un rol. |
| `roleType` | El tipo designado de la función. Los valores posibles para el tipo de rol son: `user-defined` y `system-defined`. |

**Respuesta**

Una respuesta correcta devuelve la función actualizada, incluidos los nuevos valores para su nombre, descripción y tipo de función.

```json
{
  "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
  "name": "Administrator role for ACME",
  "description": "New administrator role for ACME",
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
| `name` | El nombre de su función. |
| `description` | La propiedad description proporciona información adicional sobre la función. |
| `roleType` | El tipo designado de la función. Los valores posibles para el tipo de rol son: `user-defined` y `system-defined`. |
| `permissionSets` | Los conjuntos de permisos representan un grupo de permisos que un administrador puede aplicar a una función. Un administrador puede asignar conjuntos de permisos a una función, en lugar de asignar permisos individuales. Esto le permite crear funciones personalizadas a partir de una función predefinida que contiene un grupo de permisos. |
| `sandboxes` | Esta propiedad muestra los entornos limitados de su organización que se han aprovisionado para una función concreta. |
| `subjectAttributes` | Atributos que indican la correlación entre un asunto y los recursos de Experience Platform a los que tienen acceso. |
| `subjectAttributes.labels` | Muestra las etiquetas de uso de datos aplicadas a la función consultada. |

## Actualizar asunto por ID de rol

Para actualizar los asuntos asociados a un rol, realice una petición PATCH al extremo `/roles` y proporcione el identificador de rol de los asuntos que desea actualizar.

**Formato de API**

```http
PATCH /roles/{ROLE_ID}/subjects
```

| Parámetro | Descripción |
| --- | --- |
| {ROLE_ID} | El ID de la función asociada con los asuntos que desea actualizar. |

**Solicitud**

La siguiente solicitud actualiza los temas asociados con `{ROLE_ID}`.

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/access-control/administration/roles/<ROLE_ID>/subjects' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--data-raw '[
    {
        "op": "add",
        "path": "/user",
        "value": "{USER ID}"
    }
]' 
```

| Operaciones | Descripción |
| --- | --- |
| `op` | La llamada de operación utilizada para definir la acción necesaria para actualizar la función. Las operaciones incluyen: `add`, `replace` y `remove`. |
| `path` | Ruta del parámetro que se va a actualizar. |
| `value` | El nuevo valor con el que desea actualizar el parámetro. |

**Respuesta**

Una respuesta correcta devuelve la función actualizada, incluidos los nuevos valores de los temas.

```json
{
  "subjects": [
    [
      {
        "subjectId": "03Z07HFQCCUF3TUHAX274206@AdobeID",
        "subjectType": "user"
      }
    ]
  ],
  "_page": {
    "limit": 1,
    "count": 1
  },
  "_links": {
    "self": {
      "href": "https://platform.adobe.io:443/data/foundation/access-control/administration/roles/{ROLE_ID}/subjects",
      "templated": true
    },
    "page": {
      "href": "https://platform.adobe.io:443/data/foundation/access-control/administration/roles/{ROLE_ID}/subjects?limit={limit}&start={start}&orderBy={orderBy}&property={property}",
      "templated": true
    }
  }
}
```

## Eliminar un rol {#delete}

Para eliminar un rol, realice una petición DELETE al extremo `/roles` mientras especifica el identificador del rol que desea eliminar.

**Formato de API**

```http
DELETE /roles/{ROLE_ID}
```

| Parámetro | Descripción |
| --- | --- |
| {ROLE_ID} | El identificador de la función que desea eliminar. |

**Solicitud**

La siguiente solicitud elimina el rol con el identificador `{ROLE_ID}`.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/{ROLE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 204 (sin contenido) y un cuerpo en blanco.

Para confirmar la eliminación, intente realizar una solicitud de búsqueda (GET) al rol. Recibirá el estado HTTP 404 (no encontrado) porque la función se ha eliminado de la administración.

## Añadir una credencial de API {#apicredential}

Para agregar una credencial de API, realice una solicitud de PATCH al extremo `/roles` y proporcione el identificador de rol de los sujetos.

**Formato de API**

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/access-control/administration/roles/<ROLE_ID>/subjects' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--data-raw '[
    {
        "op": "add",
        "path": "/api-integration",
        "value": "{TECHNICAL ACCOUNT ID}"
    }
]'   
```

| Operaciones | Descripción |
| --- | --- |
| `op` | La llamada de operación utilizada para definir la acción necesaria para actualizar la función. Las operaciones incluyen: `add`, `replace` y `remove`. |
| `path` | Ruta del parámetro que se va a agregar. |
| `value` | El valor con el que desea agregar el parámetro. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 204 (sin contenido) y un cuerpo en blanco.
