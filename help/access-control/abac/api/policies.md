---
keywords: Experience Platform;inicio;temas populares;api;Control de acceso basado en atributos;control de acceso basado en atributos
solution: Experience Platform
title: Punto final de API de directivas de control de acceso
description: El extremo /policy de la API de control de acceso basado en atributos permite administrar mediante programación las políticas en Adobe Experience Platform.
exl-id: 07690f43-fdd9-4254-9324-84e6bd226743
source-git-commit: 05e63064dc8eb3f070a383f508cc4a86d4f5e9cc
workflow-type: tm+mt
source-wordcount: '1443'
ht-degree: 3%

---

# Punto final de las directivas de control de acceso

>[!IMPORTANT]
>
>El control de acceso basado en atributos actualmente está disponible en una versión limitada para clientes de asistencia médica basados en EE. UU. Esta capacidad estará disponible para todos los clientes de Real-time Customer Data Platform una vez que se haya lanzado completamente.

Las políticas de control de acceso son instrucciones que unen atributos para establecer acciones permisibles e inadmisibles. Estas políticas pueden ser locales o globales y pueden anular otras políticas. La variable `/policies` en la API de control de acceso basada en atributos le permite administrar políticas mediante programación, incluida información sobre las reglas que las rigen, así como sus respectivas condiciones de asunto.

>[!IMPORTANT]
>
>Este punto final no debe confundirse con la variable `/policies` en la variable [API de administración de datos](../../../data-governance/api/policies.md), que se utiliza para administrar las políticas de uso de datos.

## Primeros pasos

El extremo de API utilizado en esta guía forma parte de la API de control de acceso basada en atributos. Antes de continuar, revise la [guía de introducción](./getting-started.md) para ver vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios para realizar llamadas correctamente a cualquier API de Experience Platform.

## Recuperar una lista de directivas {#list}

Realice una solicitud de GET a `/policies` para enumerar todas las directivas existentes en su organización.

**Formato de API**

```http
GET /policies
```

**Solicitud**

La siguiente solicitud recupera una lista de directivas existentes.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/policies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Respuesta**

Una respuesta correcta devuelve una lista de directivas existentes.

```json
{
  {
      "id": "7019068e-a3a0-48ce-b56b-008109470592",
      "imsOrgId": "{IMS_ORG}",
      "createdBy": "{CREATED_BY}",
      "createdAt": 1652892767559,
      "modifiedBy": "{MODIFIED_BY}",
      "modifiedAt": 1652895736367,
      "name": "schema-field",
      "description": "schema-field",
      "status": "inactive",
      "subjectCondition": null,
      "rules": [
          {
              "effect": "Deny",
              "resource": "/orgs/{IMS_ORG}/sandboxes/xql/schemas/*/schema-fields/*",
              "condition": "{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}",
              "actions": [
                  "com.adobe.action.read",
                  "com.adobe.action.write",
                  "com.adobe.action.view"
              ]
          },
          {
              "effect": "Permit",
              "resource": "/orgs/{IMS_ORG}/sandboxes/*/schemas/*/schema-fields/*",
              "condition": "{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}",
              "actions": [
                  "com.adobe.action.delete"
              ]
          },
          {
              "effect": "Deny",
              "resource": "/orgs/{IMS_ORG}/sandboxes/delete-sandbox-adfengine-test-8/segments/*",
              "condition": "{\"!\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"custom/\",{\"var\":\"resource.labels\"}]}]}",
              "actions": [
                  "com.adobe.action.write"
              ]
          }
      ],
      "_etag": "\"0300593f-0000-0200-0000-62852ff80000\""
  },
  {
      "id": "13138ef6-c007-495d-837f-0a248867e219",
      "imsOrgId": "{IMS_ORG}",
      "createdBy": "{CREATED_BY}",
      "createdAt": 1652859368555,
      "modifiedBy": "{MODIFIED_BY}",
      "modifiedAt": 1652890780206,
      "name": "Documentation-Copy",
      "description": "xyz",
      "status": "active",
      "subjectCondition": null,
      "rules": [
          {
              "effect": "Permit",
              "resource": "orgs/{IMS_ORG}/sandboxes/ro-sand/schemas/*/schema-fields/*",
              "condition": "{\"!\":[{\"or\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"and\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}]}]}",
              "actions": [
                  "com.adobe.action.read"
              ]
          },
          {
              "effect": "Deny",
              "resource": "orgs/{IMS_ORG}/sandboxes/*/segments/*",
              "condition": "{\"!\":[{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"custom/\",{\"var\":\"resource.labels\"}]}]}]}",
              "actions": [
                  "com.adobe.action.read"
              ]
          }
      ],
      "_etag": "\"0300d43c-0000-0200-0000-62851c9c0000\""
  },
}
```

| Propiedad | Descripción |
| --- | --- |
| `id` | El ID que corresponde a una directiva. Este identificador se genera automáticamente y se puede utilizar para buscar, actualizar y eliminar una directiva. |
| `imsOrgId` | Organización donde se puede acceder a la directiva consultada. |
| `createdBy` | ID del usuario que creó la directiva. |
| `createdAt` | Hora a la que se creó la directiva. La variable `createdAt` se muestra en la marca de tiempo unix epoch. |
| `modifiedBy` | El ID del usuario que actualizó la directiva por última vez. |
| `modifiedAt` | Hora a la que se actualizó la directiva por última vez. La variable `modifiedAt` se muestra en la marca de tiempo unix epoch. |
| `name` | Nombre de la directiva. |
| `description` | (Opcional) Una propiedad que se puede agregar para proporcionar más información sobre una política en particular. |
| `status` | Estado actual de una directiva. Esta propiedad define si una directiva está `active` o `inactive`. |
| `subjectCondition` | Condiciones aplicadas a un asunto. Un sujeto es un usuario con ciertos atributos que solicita acceso a un recurso para realizar una acción. En este caso, `subjectCondition` son condiciones de tipo consulta aplicadas a los atributos del sujeto. |
| `rules` | Conjunto de reglas que definen una política. Las reglas definen qué combinaciones de atributos están autorizadas para que el sujeto realice correctamente una acción en el recurso. |
| `rules.effect` | El efecto que se obtiene después de considerar los valores de `action`, `condition` y `resource`. Los valores posibles incluyen: `permit`, `deny`o `indeterminate`. |
| `rules.resource` | Recurso u objeto al que puede acceder o no un sujeto.  Los recursos pueden ser archivos, aplicaciones, servidores o incluso API. |
| `rules.condition` | Condiciones aplicadas a un recurso. Por ejemplo, si un recurso es un esquema, entonces un esquema puede tener ciertas etiquetas aplicadas que contribuyen a si una acción contra ese esquema es permisible o no. |
| `rules.action` | Acción que un sujeto puede realizar contra un recurso consultado. Los valores posibles incluyen: `read`, `create`, `edit`y `delete`. |

## Buscar detalles de directivas por ID {#lookup}

Realice una solicitud de GET a `/policies` al proporcionar un ID de directiva en la ruta de solicitud para recuperar información sobre esa directiva individual.

**Formato de API**

```http
GET /policies/{POLICY_ID}
```

| Parámetro | Descripción |
| --- | --- |
| {POLICY_ID} | El ID de la directiva que desea recuperar. |

**Solicitud**

La siguiente solicitud recupera información sobre una directiva individual.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/policies/13138ef6-c007-495d-837f-0a248867e219 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Respuesta**

Una solicitud correcta devuelve información sobre el ID de directiva consultado.

```json
{
    "id": "13138ef6-c007-495d-837f-0a248867e219",
    "imsOrgId": "{IMS_ORG}",
    "createdBy": "{CREATED_BY}",
    "createdAt": 1652859368555,
    "modifiedBy": "{MODIFIED_BY}",
    "modifiedAt": 1652890780206,
    "name": "Documentation-Copy",
    "description": "xyz",
    "status": "active",
    "subjectCondition": null,
    "rules": [
        {
            "effect": "Permit",
            "resource": "orgs/{IMS_ORG}/sandboxes/ro-sand/schemas/*/schema-fields/*",
            "condition": "{\"!\":[{\"or\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"and\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}]}]}",
            "actions": [
                "com.adobe.action.read"
            ]
        },
        {
            "effect": "Deny",
            "resource": "orgs/{IMS_ORG}/sandboxes/*/segments/*",
            "condition": "{\"!\":[{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"custom/\",{\"var\":\"resource.labels\"}]}]}]}",
            "actions": [
                "com.adobe.action.read"
            ]
        }
    ],
    "_etag": "\"0300d43c-0000-0200-0000-62851c9c0000\""
}
```

| Propiedad | Descripción |
| --- | --- |
| `id` | El ID que corresponde a una directiva. Este identificador se genera automáticamente y se puede utilizar para buscar, actualizar y eliminar una directiva. |
| `imsOrgId` | Organización donde se puede acceder a la directiva consultada. |
| `createdBy` | ID del usuario que creó la directiva. |
| `createdAt` | Hora a la que se creó la directiva. La variable `createdAt` se muestra en la marca de tiempo unix epoch. |
| `modifiedBy` | El ID del usuario que actualizó la directiva por última vez. |
| `modifiedAt` | Hora a la que se actualizó la directiva por última vez. La variable `modifiedAt` se muestra en la marca de tiempo unix epoch. |
| `name` | Nombre de la directiva. |
| `description` | (Opcional) Una propiedad que se puede agregar para proporcionar más información sobre una política en particular. |
| `status` | Estado actual de una directiva. Esta propiedad define si una directiva está `active` o `inactive`. |
| `subjectCondition` | Condiciones aplicadas a un asunto. Un sujeto es un usuario con ciertos atributos que solicita acceso a un recurso para realizar una acción. En este caso, `subjectCondition` son condiciones de tipo consulta aplicadas a los atributos del sujeto. |
| `rules` | Conjunto de reglas que definen una política. Las reglas definen qué combinaciones de atributos están autorizadas para que el sujeto realice correctamente una acción en el recurso. |
| `rules.effect` | El efecto que se obtiene después de considerar los valores de `action`, `condition` y `resource`. Los valores posibles incluyen: `permit`, `deny`o `indeterminate`. |
| `rules.resource` | Recurso u objeto al que puede acceder o no un sujeto.  Los recursos pueden ser archivos, aplicaciones, servidores o incluso API. |
| `rules.condition` | Condiciones aplicadas a un recurso. Por ejemplo, si un recurso es un esquema, entonces un esquema puede tener ciertas etiquetas aplicadas que contribuyen a si una acción contra ese esquema es permisible o no. |
| `rules.action` | Acción que un sujeto puede realizar contra un recurso consultado. Los valores posibles incluyen: `read`, `create`, `edit`y `delete`. |


## Crear una directiva {#create}

Para crear una directiva nueva, realice una solicitud de POST a la variable `/policies` punto final.

**Formato de API**

```http
POST /policies
```

**Solicitud**

La siguiente solicitud crea una nueva directiva denominada: `acme-integration-policy`.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/access-control/administration/policies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
      "name": "acme-integration-policy",
      "description": "Policy for ACME",
      "imsOrgId": "{IMS_ORG}",
      "rules": [
        {
          "effect": "Permit",
          "resource": "/orgs/{IMS_ORG}/sandboxes/*",
          "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
          "actions": [
            "read"
          ]
        }
      ]
    }'
```

| Parámetro | Descripción |
| --- | --- |
| `name` | Nombre de la directiva. |
| `description` | (Opcional) Una propiedad que se puede agregar para proporcionar más información sobre una política en particular. |
| `imsOrgId` | La organización que contiene la directiva. |
| `rules` | Conjunto de reglas que definen una política. Las reglas definen qué combinaciones de atributos están autorizadas para que el sujeto realice correctamente una acción en el recurso. |
| `rules.effect` | El efecto que se obtiene después de considerar los valores de `action`, `condition` y `resource`. Los valores posibles incluyen: `permit`, `deny`o `indeterminate`. |
| `rules.resource` | Recurso u objeto al que puede acceder o no un sujeto.  Los recursos pueden ser archivos, aplicaciones, servidores o incluso API. |
| `rules.condition` | Condiciones aplicadas a un recurso. Por ejemplo, si un recurso es un esquema, entonces un esquema puede tener ciertas etiquetas aplicadas que contribuyen a si una acción contra ese esquema es permisible o no. |
| `rules.action` | Acción que un sujeto puede realizar contra un recurso consultado. Los valores posibles incluyen: `read`, `create`, `edit`y `delete`. |

**Respuesta**

Una solicitud correcta devuelve la directiva recién creada, incluido su ID de directiva único y las reglas asociadas.

```json
{
    "id": "c3863937-5d40-448d-a7be-416e538f955e",
    "imsOrgId": "{IMS_ORG}",
    "createdBy": "{CREATED_BY}",
    "createdAt": 1652988384458,
    "modifiedBy": "{MODIFIED_BY}",
    "modifiedAt": 1652988384458,
    "name": "acme-integration-policy",
    "description": "Policy for ACME",
    "status": "active",
    "subjectCondition": null,
    "rules": [
        {
            "effect": "Permit",
            "resource": "/orgs/{IMS_ORG}/sandboxes/*",
            "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
            "actions": [
                "read"
            ]
        }
    ],
    "_etag": null
}
```

| Propiedad | Descripción |
| --- | --- |
| `id` | El ID que corresponde a una directiva. Este identificador se genera automáticamente y se puede utilizar para buscar, actualizar y eliminar una directiva. |
| `name` | Nombre de una directiva. |
| `rules` | Conjunto de reglas que definen una política. Las reglas definen qué combinaciones de atributos están autorizadas para que el sujeto realice correctamente una acción en el recurso. |
| `rules.effect` | El efecto que se obtiene después de considerar los valores de `action`, `condition` y `resource`. Los valores posibles incluyen: `permit`, `deny`o `indeterminate`. |
| `rules.resource` | Recurso u objeto al que puede acceder o no un sujeto.  Los recursos pueden ser archivos, aplicaciones, servidores o incluso API. |
| `rules.condition` | Condiciones aplicadas a un recurso. Por ejemplo, si un recurso es un esquema, entonces un esquema puede tener ciertas etiquetas aplicadas que contribuyen a si una acción contra ese esquema es permisible o no. |
| `rules.action` | Acción que un sujeto puede realizar contra un recurso consultado. Los valores posibles incluyen: `read`, `create`, `edit`y `delete`. |


## Actualizar una directiva por ID de directiva {#put}

Para actualizar las reglas de una directiva individual, realice una solicitud de PUT al `/policies` al proporcionar el ID de la directiva que desea actualizar en la ruta de solicitud.

**Formato de API**

```http
PUT /policies/{POLICY_ID}
```

| Parámetro | Descripción |
| --- | --- |
| {POLICY_ID} | El ID de la directiva que desea actualizar. |

**Solicitud**

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/access-control/administration/policies/8cf487d7-3642-4243-a8ea-213d72f694b9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
      "id": "8cf487d7-3642-4243-a8ea-213d72f694b9",
      "imsOrgId": "{IMS_ORG}",
      "name": "test-2",
      "rules": [
      {
        "effect": "Deny",
        "resource": "/orgs/{IMS_ORG}/sandboxes/*",
        "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
        "actions": [
          "read"
        ]
      }
    ]
  }'
```

**Respuesta**

Una respuesta correcta devuelve la directiva actualizada.

```json
{
    "id": "8cf487d7-3642-4243-a8ea-213d72f694b9",
    "imsOrgId": "{IMS_ORG}",
    "createdBy": "{CREATED_BY}",
    "createdAt": 1652988866647,
    "modifiedBy": "{MODIFIED_BY}",
    "modifiedAt": 1652989297287,
    "name": "test-2",
    "description": null,
    "status": "active",
    "subjectCondition": null,
    "rules": [
        {
            "effect": "Deny",
            "resource": "/orgs/{IMS_ORG}/sandboxes/*",
            "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
            "actions": [
                "read"
            ]
        }
    ],
    "_etag": null
}
```

## Actualizar propiedades de directiva {#patch}

Para actualizar las propiedades de una directiva individual, realice una solicitud de PATCH al `/policies` al proporcionar el ID de la directiva que desea actualizar en la ruta de solicitud.

**Formato de API**

```http
PATCH /policies/{POLICY_ID}
```

| Parámetro | Descripción |
| --- | --- |
| {POLICY_ID} | El ID de la directiva que desea actualizar. |

**Solicitud**

La siguiente solicitud reemplaza el valor de `/description` en ID de directiva `c3863937-5d40-448d-a7be-416e538f955e`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/access-control/administration/policies/c3863937-5d40-448d-a7be-416e538f955e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
    "operations": [
      {
        "op": "replace",
        "path": "/description",
        "value": "Pre-set policy to be applied for ACME"
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

Una respuesta correcta devuelve el ID de la directiva consultada con una descripción actualizada.

```json
{
    "id": "c3863937-5d40-448d-a7be-416e538f955e",
    "imsOrgId": "{IMS_ORG}",
    "createdBy": "acp_accessControlService",
    "createdAt": 1652988384458,
    "modifiedBy": "acp_accessControlService",
    "modifiedAt": 1652988384458,
    "name": "acme-integration-policy",
    "description": "Pre-set policy to be applied for ACME",
    "status": "active",
    "subjectCondition": null,
    "rules": [
        {
            "effect": "Permit",
            "resource": "/orgs/{IMS_ORG}/sandboxes/*",
            "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
            "actions": [
                "read"
            ]
        }
    ],
    "_etag": null
}
```

## Eliminar una directiva {#delete}

Para eliminar una directiva, realice una solicitud de DELETE al `/policies` al proporcionar el ID de la directiva que desea eliminar.

**Formato de API**

```http
DELETE /policies/{POLICY_ID}
```

| Parámetro | Descripción |
| --- | --- |
| {POLICY_ID} | El ID de la directiva que desea eliminar. |

**Solicitud**

La siguiente solicitud elimina la directiva con el ID de `c3863937-5d40-448d-a7be-416e538f955e`.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/access-control/administration/policies/c3863937-5d40-448d-a7be-416e538f955e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 204 (sin contenido) y un cuerpo en blanco.

Puede confirmar la eliminación intentando realizar una solicitud de búsqueda (GET) a la directiva. Recibirá un estado HTTP 404 (no encontrado) porque la directiva se ha eliminado de la administración.
