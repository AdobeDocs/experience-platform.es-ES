---
title: Extremo de API de eventos de auditoría
description: Obtenga información sobre cómo recuperar eventos de auditoría en Experience Platform mediante la API de consulta de auditoría.
role: Developer
feature: Audits, API
exl-id: c365b6d8-0432-41a5-9a07-44a995f69b7d
source-git-commit: dec895e3ea625fb86d1891bad713185d39c47c81
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 2%

---

# Extremo de eventos de auditoría

Los registros de auditoría se utilizan para proporcionar detalles de la actividad del usuario para varios servicios y funcionalidades. Cada acción registrada contiene metadatos que indican el tipo de acción, la fecha y la hora, el ID de correo electrónico del usuario que realizó la acción y los atributos adicionales relevantes de ese tipo de acción. El extremo `/audit/events` de la API [!DNL Audit Query] le permite recuperar mediante programación los datos de evento de la actividad de su organización en [!DNL Experience Platform].

## Introducción

El extremo de API utilizado en esta guía forma parte de la [[!DNL Audit Query] API](https://developer.adobe.com/experience-platform-apis/references/audit-query/). Antes de continuar, revisa la [guía de introducción](./getting-started.md) para ver vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios para realizar correctamente llamadas a cualquier API de [!DNL Experience Platform].

## Enumerar eventos de auditoría

Puede recuperar datos de eventos realizando una petición GET al extremo `/audit/events`, especificando los eventos que desea recuperar en la carga útil.

**Formato de API**

```http
GET /audit/events
```

La API [!DNL Audit Query] admite el uso de parámetros de consulta para paginar y filtrar los resultados al enumerar eventos.

| Parámetro | Descripción |
| --- | --- |
| `limit` | Número máximo de registros que se devolverán en la respuesta. El valor predeterminado `limit` es 50. |
| `start` | Un puntero al primer elemento para los resultados de búsqueda devueltos. Para acceder a la siguiente página de resultados, este parámetro debe incrementarse en la misma cantidad indicada por limit. Ejemplo: Para acceder a la siguiente página de resultados de una solicitud con límite=50, utilice el parámetro start=50, luego start=100 para la página siguiente, etc. |
| `queryId` | Al realizar una consulta al extremo /audit/events, la respuesta incluye una propiedad de cadena queryId. Para realizar la misma consulta en una llamada independiente, puede incluir el valor de ID como un único parámetro de consulta en lugar de volver a configurar manualmente los parámetros de búsqueda. |

**Solicitud**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/audit/events?limit=10
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {TRACING_ID}' \
```

**Respuesta**

Una respuesta correcta devuelve los puntos de datos resultantes para las métricas y filtros especificados en la solicitud.

```json
{
  "_embedded": {
    "events": [
      {
        "id": "6ecc125d-da03-4882-a944-88c707ddc3f7",
        "requestId": "5YGdpTX5PvRrdqCfrCT8p8lWphZPzxl8",
        "permissionResource": "Dataset",
        "permissionType": "WRITE",
        "assetType": "Dataset",
        "action": "Create",
        "status": "Allow",
        "failureCode": "",
        "timestamp": "2025-06-24T16:50:28.318+0000",
        "version": "1.0",
        "imsOrgId": "{ORGANIZATION_ID}",
        "region": "VA7",
        "authId": "e6b46821-e2b4-4729-952f-2e4afd713b31",
        "assetId": "685ad754fb1abe2b263df4b3",
        "assetName": "my-dataset",
        "sandboxName": "prod",
        "sandboxId": "{SANDBOX_ID}",
        "userEmail": "{USER_EMAIL}",
        "userIpAddresses": [
          "130.*.*.*",
          "10.*.*.*"
        ],
        "enhancedEvents": [
          {
            "id": "0ee91e42-ac46-4f35-a01a-f74a1569c404",
            "requestId": "5YGdpTX5PvRrdqCfrCT8p8lWphZPzxl8",
            "permissionResource": "Dataset",
            "permissionType": "Write",
            "assetType": "Dataset",
            "action": "Create",
            "status": "Success",
            "failureCode": "",
            "timestamp": "2025-06-24T16:50:28.883+0000",
            "assetId": "685ad754fb1abe2b263df4b3",
            "assetName": "my-dataset"
          }
        ]
      }
    ]
  },
  "_links": {
    "self": {
      "href": "https://platform.adobe.io/data/foundation/audit/events?property=user%253D%253Ddraghici%2540adobe.com"
    },
    "page": {
      "href": "https://platform.adobe.io/data/foundation/audit/events?queryId=b3JkZXJCeVJ1bGVzPSZwcm9wZXJ0eT11c2VyPT1kcmFnaGljaUBhZG9iZS5jb20mdGltZXN0YW1wSW5kZXg9MTc1MDc4MzgyODMxOCZ0b3RhbEVsZW1lbnRzPTE3&limit=50{&start}",
      "templated": true
    }
  },
  "page": {
    "size": 1,
    "totalElements": 1,
    "totalPages": 1,
    "number": 1
  },
  "queryId": "b3JkZXJCeVJ1bGVzPSZwcm9wZXJ0eT11c2VyPT1kcmFnaGljaUBhZG9iZS5jb20mdGltZXN0YW1wSW5kZXg9MTc1MDc4MzgyODMxOCZ0b3RhbEVsZW1lbnRzPTE3"
}
```

| Propiedad | Descripción |
| --- | --- |
| `events` | Una matriz cuyos objetos representen cada uno de los eventos especificados en la solicitud. Cada objeto contiene información sobre la configuración del filtro y los datos de evento devueltos. |
| `userEmail` | El correo electrónico del usuario que realizó el evento. |
| `eventType` | El tipo de evento. Los tipos de eventos incluyen `Core` y `Enhanced`. |
| `imsOrgId` | El ID de la organización en la que se produjo el evento. |
| `permissionResource` | El producto o la funcionalidad que proporcionó el permiso para realizar la acción. Un recurso puede ser cualquiera de los siguientes: <ul><li>`Activation` </li><li>`ActivationAssociation` </li><li>`AnalyticSource` </li><li>`AudienceManagerSource` </li><li>`BizibleSource` </li><li>`CustomerAttributeSource` </li><li>`Dataset` </li><li>`EnterpriseSource` </li><li>`LaunchSource` </li><li>`MarketoSource` </li><li>`ProductProfile` </li><li>`ProfileConfig` </li><li>`Sandbox` </li><li>`Schema` </li><li>`Segment` </li><li>`StreamingSource` </li></ul> |
| `permissionType` | Tipo de permiso relacionado con la acción. |
| `assetType` | El tipo de recurso de Experience Platform en el que se realizó la acción. |
| `assetId` | Identificador único del recurso de Experience Platform en el que se realizó la acción. |
| `assetName` | Nombre del recurso de Experience Platform en el que se realizó la acción. |
| `action` | El tipo de acción que se registró para el evento. Una acción puede ser cualquiera de las siguientes: <ul><li>`Add` </li><li>`Create` </li><li>`Dataset activate` </li><li>`Dataset remove` </li><li>`Delete` </li><li>`Disable for profile` </li><li>`Enable` </li><li>`Enable for profile` </li><li>`Profile activate` </li><li>`Profile remove` </li><li>`remove` </li><li>`reset` </li><li>`segment activate` </li><li>`segment remove` </li><li>`update` </li></ul> |
| `status` | El estado de la acción. Un estado puede ser cualquiera de los siguientes: </li><li>`Allow` </li><li>`Deny` </li><li>`Failure` </li><li>`Success` </li></ul> |

{style="table-layout:auto"}
