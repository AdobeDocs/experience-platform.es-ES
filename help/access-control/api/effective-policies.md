---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Políticas eficaces de Vista
topic: developer guide
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53

---


# Políticas eficaces de Vista

Para vista de directivas efectivas para el usuario actual, realice una solicitud POST al extremo en la API de Control de acceso `/acl/effective-policies` . Los permisos y tipos de recursos que desea recuperar deben proporcionarse en la carga útil de la solicitud en forma de matriz. Esto se muestra en el ejemplo de llamada de API que se muestra a continuación.

**Formato API**

```http
POST /acl/effective-policies
```

**Solicitud**

Las siguientes solicitudes recuperan información sobre el permiso &quot;Administrar conjuntos de datos&quot; y el acceso al tipo de recurso &quot;esquemas&quot; del usuario actual.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/access-control/acl/effective-policies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
    "/permissions/manage-datasets",
    "/resource-types/schemas"
  ]'
```

>[!NOTE] Para obtener una lista completa de los permisos y tipos de recursos que se pueden proporcionar en la matriz de carga útil, consulte la sección del apéndice sobre los permisos y tipos [de recursos](#accepted-permissions-and-resource-types)aceptados.

**Respuesta**

Una respuesta correcta devuelve información sobre los permisos y tipos de recursos proporcionados en la solicitud. La respuesta incluye los permisos activos que tiene el usuario actual para los tipos de recursos especificados en la solicitud. Si algún permiso incluido en la carga útil de la solicitud está activo para el usuario actual, la API devuelve el permiso con un riesgo (`*`) para indicar que el permiso está activo. Los permisos proporcionados en la solicitud que no estén activos para el usuario se omiten de la carga útil de respuesta.

```json
{
    "policies": {
        "/resource-types/schemas": [
            "read",
            "write",
            "delete"
        ],
        "/permissions/manage-datasets": [
            "*"
        ]
    }
}
```

## Pasos siguientes

En este documento se explica cómo realizar llamadas a la API de Control de acceso para devolver información sobre permisos activos y políticas relacionadas para tipos de recursos. Para obtener más información sobre control de acceso para la plataforma de experiencias, consulte la descripción general [de](../home.md)control de acceso.

## Apéndice

Esta sección proporciona información adicional para utilizar la API de Control de acceso.

### Permisos y tipos de recursos aceptados

A continuación se muestra una lista de permisos y tipos de recursos que puede incluir en la carga útil de una solicitud POST al `/acl/active-permissions` extremo.

**Permisos**

```plaintext
"permissions/activate-destinations"
"permissions/export-audience-for-segments"
"permissions/manage-datasets"
"permissions/manage-destinations"
"permissions/manage-identity-namespaces"
"permissions/manage-profiles"
"permissions/manage-sandboxes"
"permissions/manage-schemas"
"permissions/reset-sandboxes"
"permissions/view-datasets"
"permissions/view-destinations"
"permissions/view-identity-namespaces"
"permissions/view-monitoring-dashboard"
"permissions/view-profiles"
"permissions/view-sandboxes"
"permissions/view-schemas"
```

**Tipos de recursos**

```plaintext
"resource-types/classes"
"resource-types/connections"
"resource-types/data-types"
"resource-types/dataset-data"
"resource-types/datasets"
"resource-types/destinations"
"resource-types/dule-labels"
"resource-types/identity-descriptors"
"resource-types/identity-namespaces"
"resource-types/mixins"
"resource-types/monitoring"
"resource-types/profile-configs
"resource-types/profile-datasets"
"resource-types/profiles"
"resource-types/relationship-descriptors"
"resource-types/reset-sandboxes"
"resource-types/sandboxes"
"resource-types/schemas"
"resource-types/segment-jobs"
"resource-types/segments"
```
