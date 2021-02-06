---
keywords: Experience Platform;inicio;temas populares;políticas efectivas;API de control de acceso
solution: Experience Platform
title: Extremo de la API de directivas efectivas
topic: developer guide
description: Control de acceso en Adobe Experience Platform le permite administrar funciones y permisos para diversas funciones de la plataforma mediante Adobe Admin Console. Este documento sirve como guía para la vista de políticas eficaces mediante la API de control de acceso para Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 1%

---


# Extremo de directivas efectivo

Para vista de políticas efectivas para el usuario actual, realice una solicitud de POST al extremo `/acl/effective-policies` en la API [!DNL Access Control]. Los permisos y tipos de recursos que desea recuperar deben proporcionarse en la carga útil de la solicitud en forma de matriz. Esto se muestra en el ejemplo de llamada de API que se muestra a continuación.

**Formato API**

```http
POST /acl/effective-policies
```

**Solicitud**

Las siguientes solicitudes recuperan información sobre el permiso &quot;[!UICONTROL Administrar conjuntos de datos]&quot; y el acceso al tipo de recurso &quot;[!UICONTROL esquemas]&quot; para el usuario actual.

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
>Para obtener una lista completa de los permisos y tipos de recursos que se pueden proporcionar en la matriz de carga útil, consulte la sección del apéndice sobre [permisos y tipos de recursos aceptados](#accepted-permissions-and-resource-types).

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

Este documento explicaba cómo realizar llamadas a la API [!DNL Access Control] para devolver información sobre permisos activos y políticas relacionadas para tipos de recursos. Para obtener más información sobre control de acceso para [!DNL Experience Platform], consulte la [información general del control de acceso](../home.md).

## Apéndice

Esta sección proporciona información adicional para utilizar la API [!DNL Access Control].

### Permisos y tipos de recursos aceptados

A continuación se muestra una lista de permisos y tipos de recursos que puede incluir en la carga útil de una solicitud de POST al extremo `/acl/active-permissions`.

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
