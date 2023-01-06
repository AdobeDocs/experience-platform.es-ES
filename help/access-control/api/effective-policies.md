---
keywords: Experience Platform;inicio;temas populares;políticas efectivas;api de control de acceso
solution: Experience Platform
title: Punto final de API de directivas efectivas
description: Obtenga información sobre cómo ver las políticas de acceso efectivas mediante la API de control de acceso para Adobe Experience Platform.
exl-id: 555d73db-115d-4f4c-8bd2-b91477799591
source-git-commit: 7b197f253aa5ce04a682040814cf749407154ebc
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 2%

---

# Punto final de directivas efectivas

Para ver las directivas de control de acceso efectivas para el usuario actual, realice una solicitud de POST al `/acl/effective-policies` en la variable [!DNL Access Control] API. Los permisos y tipos de recursos que desea recuperar deben proporcionarse en la carga útil de la solicitud en forma de matriz. Esto se muestra en el ejemplo de llamada de API que aparece a continuación.

**Formato de API**

```http
POST /acl/effective-policies
```

**Solicitud**

Las siguientes solicitudes recuperan información sobre el[!UICONTROL Administrar conjuntos de datos]&quot; permiso y acceso a &quot;[!UICONTROL esquemas]&quot; tipo de recurso para el usuario actual.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/access-control/acl/effective-policies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
    "/permissions/manage-datasets",
    "/resource-types/schemas"
  ]'
```

>[!NOTE]
>
>Para obtener una lista completa de los permisos y tipos de recursos que se pueden proporcionar en la matriz de carga útil, consulte la sección del apéndice en [permisos aceptados y tipos de recursos](#accepted-permissions-and-resource-types).

**Respuesta**

Una respuesta correcta devuelve información sobre los permisos y tipos de recursos proporcionados en la solicitud. La respuesta incluye los permisos activos que el usuario actual tiene para los tipos de recursos especificados en la solicitud. Si algún permiso incluido en la carga útil de la solicitud está activo para el usuario actual, la API devuelve el permiso con un riesgo (`*`) para indicar que el permiso está activo. Todos los permisos proporcionados en la solicitud que no estén activos para el usuario se omiten en la carga útil de respuesta.

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

Este documento abarcaba cómo realizar llamadas al [!DNL Access Control] para devolver información sobre permisos activos y directivas de acceso relacionadas para tipos de recursos. Para obtener más información sobre el control de acceso para [!DNL Experience Platform], consulte la [información general sobre el control de acceso](../home.md).

## Apéndice

Esta sección proporciona información complementaria para usar la variable [!DNL Access Control] API.

### Permisos aceptados y tipos de recursos

A continuación se muestra una lista de permisos y tipos de recursos que puede incluir en la carga útil de una solicitud de POST para `/acl/active-permissions` punto final.

**Permisos**

```plaintext
permissions/activate-destinations
permissions/evaluate-segments
permissions/execute-decisioning-activities
permissions/export-audience-for-segment
permissions/manage-datasets
permissions/manage-decisioning-activities
permissions/manage-decisioning-options
permissions/manage-destinations
permissions/manage-dsw
permissions/manage-dule-labels
permissions/manage-dule-policies
permissions/manage-identity-namespaces
permissions/manage-privacy-workflows
permissions/manage-profile-configs
permissions/manage-profiles
permissions/manage-queries
permissions/manage-schemas
permissions/manage-segments
permissions/manage-sources
permissions/reset-sandboxes
permissions/view-datasets
permissions/view-destinations
permissions/view-dule-labels
permissions/view-dule-policies
permissions/view-identity-namespaces
permissions/view-monitoring-dashboard
permissions/view-privacy-workflows
permissions/view-profile-configs
permissions/view-profiles
permissions/view-sandboxes
permissions/view-schemas
permissions/view-segments
permissions/view-sources
```

**Tipos de recursos**

```plaintext
resource-types/activation-associations
resource-types/activations
resource-types/activities
resource-types/analytics-source
resource-types/audience-manager-source
resource-types/bizible-source
resource-types/connection
resource-types/customer-attributes-source
resource-types/data-science-workspace
resource-types/dataset-preview
resource-types/datasets
resource-types/dule-label
resource-types/dule-policy
resource-types/enterprise-source
resource-types/identity-descriptor
resource-types/identity-namespaces
resource-types/launch-source
resource-types/marketing-action
resource-types/marketo-source
resource-types/monitoring
resource-types/offers
resource-types/placements
resource-types/privacy-consent
resource-types/privacy-content-delivery
resource-types/privacy-job
resource-types/profile-configs
resource-types/profile-datasets
resource-types/profiles
resource-types/query
resource-types/relationship-descriptor
resource-types/sandboxes
resource-types/schemas
resource-types/segment-jobs
resource-types/segments
resource-types/streaming-source
```
