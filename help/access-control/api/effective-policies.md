---
keywords: Experience Platform;home;popular topics;effective policies;access control api
solution: Experience Platform
title: Políticas eficaces de vista
topic: developer guide
description: Control de acceso en Adobe Experience Platform le permite administrar funciones y permisos para diversas funciones de la plataforma mediante Adobe Admin Console. Este documento sirve como guía para la vista de políticas eficaces mediante la API de control de acceso para Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 14f99c23cd82894fee5eb5c4093b3c50b95c52e8
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 1%

---


# Políticas eficaces de vista

Para vista de directivas efectivas para el usuario actual, realice una solicitud de POST al extremo en la `/acl/effective-policies` API [!DNL Access Control] . Los permisos y tipos de recursos que desea recuperar deben proporcionarse en la carga útil de la solicitud en forma de matriz. Esto se muestra en el ejemplo de llamada de API que se muestra a continuación.

**Formato API**

```http
POST /acl/effective-policies
```

**Solicitud**

Las siguientes solicitudes recuperan información sobre el permiso &quot;[!UICONTROL Administrar conjuntos]de datos&quot; y el acceso al tipo de recurso &quot;[!UICONTROL esquemas]&quot; para el usuario actual.

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

>[!NOTE]
>
>Para obtener una lista completa de los permisos y tipos de recursos que se pueden proporcionar en la matriz de carga útil, consulte la sección del apéndice sobre los permisos y tipos [de recursos](#accepted-permissions-and-resource-types)aceptados.

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

Este documento explicaba cómo realizar llamadas a la [!DNL Access Control] API para devolver información sobre permisos activos y políticas relacionadas para tipos de recursos. Para obtener más información sobre control de acceso para [!DNL Experience Platform], consulte la descripción general [del](../home.md)control de acceso.

## Apéndice

Esta sección proporciona información adicional para utilizar la [!DNL Access Control] API.

### Permisos y tipos de recursos aceptados

A continuación se muestra una lista de permisos y tipos de recursos que se pueden incluir en la carga útil de una solicitud de POST al `/acl/active-permissions` extremo.

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
