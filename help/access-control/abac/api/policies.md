---
keywords: Experience Platform;inicio;temas populares;api;Control de acceso basado en atributos;control de acceso basado en atributos
solution: Experience Platform
title: Punto final de API de directivas de control de acceso
description: El extremo /policies de la API de control de acceso basado en atributos le permite administrar directivas mediante programación en Adobe Experience Platform.
role: Developer
exl-id: 07690f43-fdd9-4254-9324-84e6bd226743
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '1433'
ht-degree: 3%

---

# Extremo de directivas de control de acceso

>[!NOTE]
>
>Si se pasa un token de usuario, el usuario del token debe tener un rol de &quot;administrador de organización&quot; para la organización solicitada.

Las políticas de control de acceso son instrucciones que unen atributos para establecer acciones permisibles e inadmisibles. Estas directivas pueden ser locales o globales, y pueden anular otras directivas. El extremo `/policies` de la API de control de acceso basado en atributos le permite administrar directivas mediante programación, incluida información sobre las reglas que las rigen, así como las condiciones de los respectivos sujetos.

>[!IMPORTANT]
>
>Este extremo no se debe confundir con el extremo `/policies` de la [API del servicio de directivas](../../../data-governance/api/policies.md), que se usa para administrar directivas de uso de datos.

## Introducción

El extremo de API utilizado en esta guía forma parte de la API de control de acceso basada en atributos. Antes de continuar, revisa la [guía de introducción](./getting-started.md) para ver vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios para realizar correctamente llamadas a cualquier API de Experience Platform.

## Recuperación de una lista de directivas {#list}

Realice una solicitud de GET al extremo `/policies` para enumerar todas las directivas existentes en su organización.

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
| `createdBy` | El ID del usuario que creó la directiva. |
| `createdAt` | Hora a la que se creó la directiva. La propiedad `createdAt` se muestra en la marca de tiempo unix epoch. |
| `modifiedBy` | El ID del usuario que actualizó la directiva por última vez. |
| `modifiedAt` | Hora a la que se actualizó la directiva por última vez. La propiedad `modifiedAt` se muestra en la marca de tiempo unix epoch. |
| `name` | Nombre de la directiva. |
| `description` | (Opcional) Una propiedad que se puede agregar para proporcionar más información sobre una directiva en particular. |
| `status` | El estado actual de una directiva. Esta propiedad define si una directiva es actualmente `active` o `inactive`. |
| `subjectCondition` | Las condiciones aplicadas a un asunto. Un sujeto es un usuario con ciertos atributos que solicitan acceso a un recurso para realizar una acción. En este caso, `subjectCondition` son condiciones de tipo consulta aplicadas a los atributos del asunto. |
| `rules` | Conjunto de reglas que definen una directiva. Las reglas definen qué combinaciones de atributos están autorizadas para que el sujeto realice correctamente una acción en el recurso. |
| `rules.effect` | El efecto que se produce después de considerar los valores de `action`, `condition` y `resource`. Los valores posibles incluyen: `permit`, `deny` o `indeterminate`. |
| `rules.resource` | Recurso u objeto al que puede tener acceso o al que no puede tener acceso un sujeto.  Los recursos pueden ser archivos, aplicaciones, servidores o incluso API. |
| `rules.condition` | Las condiciones aplicadas a un recurso. Por ejemplo, si un recurso es un esquema, un esquema puede tener aplicadas ciertas etiquetas que contribuyen a determinar si una acción contra ese esquema es permisible o no. |
| `rules.action` | Acción que un sujeto puede realizar contra un recurso consultado. Los valores posibles incluyen: `read`, `create`, `edit` y `delete`. |

## Buscar detalles de directivas por identificador {#lookup}

Realice una solicitud de GET al extremo `/policies` mientras proporciona un ID de directiva en la ruta de solicitud para recuperar información sobre esa directiva individual.

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
  "policies": [
    {
      "id": "7019068e-a3a0-48ce-b56b-008109470592",
      "imsOrgId": "5555467B5D8013E50A494220@AdobeOrg",
      "createdBy": "example@AdobeID",
      "createdAt": 1652892767559,
      "modifiedBy": "example@AdobeID",
      "modifiedAt": 1652895736367,
      "name": "schema-field",
      "description": "schema-field",
      "status": "inactive",
      "subjectCondition": null,
      "rules": [
        {
          "effect": "Deny",
          "resource": "/orgs/5555467B5D8013E50A494220@AdobeOrg/sandboxes/xql/schemas/*/schema-fields/*",
          "condition": "{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}",
          "actions": [
            "com.adobe.action.read",
            "com.adobe.action.write",
            "com.adobe.action.view"
          ]
        },
        {
          "effect": "Permit",
          "resource": "/orgs/5555467B5D8013E50A494220@AdobeOrg/sandboxes/*/schemas/*/schema-fields/*",
          "condition": "{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}",
          "actions": [
            "com.adobe.action.delete"
          ]
        },
        {
          "effect": "Deny",
          "resource": "/orgs/5555467B5D8013E50A494220@AdobeOrg/sandboxes/delete-sandbox-adfengine-test-8/segments/*",
          "condition": "{\"!\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"custom/\",{\"var\":\"resource.labels\"}]}]}",
          "actions": [
            "com.adobe.action.write"
          ]
        }
      ],
      "etag": "\"0300593f-0000-0200-0000-62852ff80000\""
    }
  ]
}
```

| Propiedad | Descripción |
| --- | --- |
| `id` | El ID que corresponde a una directiva. Este identificador se genera automáticamente y se puede utilizar para buscar, actualizar y eliminar una directiva. |
| `imsOrgId` | Organización donde se puede acceder a la directiva consultada. |
| `createdBy` | El ID del usuario que creó la directiva. |
| `createdAt` | Hora a la que se creó la directiva. La propiedad `createdAt` se muestra en la marca de tiempo unix epoch. |
| `modifiedBy` | El ID del usuario que actualizó la directiva por última vez. |
| `modifiedAt` | Hora a la que se actualizó la directiva por última vez. La propiedad `modifiedAt` se muestra en la marca de tiempo unix epoch. |
| `name` | Nombre de la directiva. |
| `description` | (Opcional) Una propiedad que se puede agregar para proporcionar más información sobre una directiva en particular. |
| `status` | El estado actual de una directiva. Esta propiedad define si una directiva es actualmente `active` o `inactive`. |
| `subjectCondition` | Las condiciones aplicadas a un asunto. Un sujeto es un usuario con ciertos atributos que solicitan acceso a un recurso para realizar una acción. En este caso, `subjectCondition` son condiciones de tipo consulta aplicadas a los atributos del asunto. |
| `rules` | Conjunto de reglas que definen una directiva. Las reglas definen qué combinaciones de atributos están autorizadas para que el sujeto realice correctamente una acción en el recurso. |
| `rules.effect` | El efecto que se produce después de considerar los valores de `action`, `condition` y `resource`. Los valores posibles incluyen: `permit`, `deny` o `indeterminate`. |
| `rules.resource` | Recurso u objeto al que puede tener acceso o al que no puede tener acceso un sujeto.  Los recursos pueden ser archivos, aplicaciones, servidores o incluso API. |
| `rules.condition` | Las condiciones aplicadas a un recurso. Por ejemplo, si un recurso es un esquema, un esquema puede tener aplicadas ciertas etiquetas que contribuyen a determinar si una acción contra ese esquema es permisible o no. |
| `rules.action` | Acción que un sujeto puede realizar contra un recurso consultado. Los valores posibles incluyen: `read`, `create`, `edit` y `delete`. |


## Crear una directiva {#create}

Para crear una directiva nueva, realice una solicitud de POST al extremo `/policies`.

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
            "com.adobe.action.read"
          ]
        }
      ]
    }'
```

| Parámetro | Descripción |
| --- | --- |
| `name` | Nombre de la directiva. |
| `description` | (Opcional) Una propiedad que se puede agregar para proporcionar más información sobre una directiva en particular. |
| `imsOrgId` | La organización que contiene la directiva. |
| `rules` | Conjunto de reglas que definen una directiva. Las reglas definen qué combinaciones de atributos están autorizadas para que el sujeto realice correctamente una acción en el recurso. |
| `rules.effect` | El efecto que se produce después de considerar los valores de `action`, `condition` y `resource`. Los valores posibles incluyen: `permit`, `deny` o `indeterminate`. |
| `rules.resource` | Recurso u objeto al que puede tener acceso o al que no puede tener acceso un sujeto.  Los recursos pueden ser archivos, aplicaciones, servidores o incluso API. |
| `rules.condition` | Las condiciones aplicadas a un recurso. Por ejemplo, si un recurso es un esquema, un esquema puede tener aplicadas ciertas etiquetas que contribuyen a determinar si una acción contra ese esquema es permisible o no. |
| `rules.action` | Acción que un sujeto puede realizar contra un recurso consultado. Los valores posibles incluyen: `read`, `create`, `edit` y `delete`. |

**Respuesta**

Una solicitud correcta devuelve la política recién creada, incluido su ID de política único y las reglas asociadas.

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
                "com.adobe.action.read"
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
| `rules` | Conjunto de reglas que definen una directiva. Las reglas definen qué combinaciones de atributos están autorizadas para que el sujeto realice correctamente una acción en el recurso. |
| `rules.effect` | El efecto que se produce después de considerar los valores de `action`, `condition` y `resource`. Los valores posibles incluyen: `permit`, `deny` o `indeterminate`. |
| `rules.resource` | Recurso u objeto al que puede tener acceso o al que no puede tener acceso un sujeto.  Los recursos pueden ser archivos, aplicaciones, servidores o incluso API. |
| `rules.condition` | Las condiciones aplicadas a un recurso. Por ejemplo, si un recurso es un esquema, un esquema puede tener aplicadas ciertas etiquetas que contribuyen a determinar si una acción contra ese esquema es permisible o no. |
| `rules.action` | Acción que un sujeto puede realizar contra un recurso consultado. Los valores posibles incluyen: `read`, `create`, `edit` y `delete`. |


## Actualizar una directiva por ID de directiva {#put}

Para actualizar las reglas de una directiva individual, realice una solicitud de PUT al extremo `/policies` y proporcione el ID de la directiva que desea actualizar en la ruta de solicitud.

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
          "com.adobe.action.read"
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
                "com.adobe.action.read"
            ]
        }
    ],
    "_etag": null
}
```

## Actualizar propiedades de la directiva {#patch}

Para actualizar las propiedades de una directiva individual, realice una solicitud de PATCH al extremo `/policies` y proporcione el ID de la directiva que desea actualizar en la ruta de solicitud.

**Formato de API**

```http
PATCH /policies/{POLICY_ID}
```

| Parámetro | Descripción |
| --- | --- |
| {POLICY_ID} | El ID de la directiva que desea actualizar. |

**Solicitud**

La siguiente solicitud reemplaza el valor de `/description` en el id. de directiva `c3863937-5d40-448d-a7be-416e538f955e`.

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
| `op` | La llamada de operación utilizada para definir la acción necesaria para actualizar la función. Las operaciones incluyen: `add`, `replace` y `remove`. |
| `path` | Ruta del parámetro que se va a actualizar. |
| `value` | El nuevo valor con el que desea actualizar el parámetro. |

**Respuesta**

Una respuesta correcta devuelve el ID de directiva consultado con la descripción actualizada.

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
                "com.adobe.action.read"
            ]
        }
    ],
    "_etag": null
}
```

## Eliminar una política {#delete}

Para eliminar una directiva, realice una solicitud de DELETE al extremo `/policies` y proporcione el identificador de la directiva que desea eliminar.

**Formato de API**

```http
DELETE /policies/{POLICY_ID}
```

| Parámetro | Descripción |
| --- | --- |
| {POLICY_ID} | El ID de la directiva que desea eliminar. |

**Solicitud**

La siguiente solicitud elimina la directiva con el identificador `c3863937-5d40-448d-a7be-416e538f955e`.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/access-control/administration/policies/c3863937-5d40-448d-a7be-416e538f955e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 204 (sin contenido) y un cuerpo en blanco.

Para confirmar la eliminación, intente realizar una solicitud de búsqueda (GET) a la directiva. Recibirá el estado HTTP 404 (no encontrado) porque la directiva se ha eliminado de la administración.
