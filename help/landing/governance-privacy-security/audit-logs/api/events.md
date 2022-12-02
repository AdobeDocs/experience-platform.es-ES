---
title: Punto final de API de eventos de auditoría
description: Obtenga información sobre cómo recuperar eventos de auditoría en Experience Platform mediante la API de consulta de auditoría.
source-git-commit: 2abd3ea6f1affa7d83a3ae6ee368fa4b5b890d94
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 10%

---

# Extremo de eventos de auditoría

Los registros de auditoría se utilizan para proporcionar detalles de la actividad del usuario para varios servicios y capacidades. Cada acción registrada contiene metadatos que indican el tipo de acción, la fecha y la hora, el ID de correo electrónico del usuario que realizó la acción y los atributos adicionales relevantes de ese tipo de acción. La variable `/audit/events` en la variable [!DNL Audit Query] La API de le permite recuperar mediante programación datos de evento para la actividad de su organización en [!DNL Platform].

## Primeros pasos

El extremo de API utilizado en esta guía forma parte de la variable [[!DNL Audit Query] API](https://developer.adobe.com/experience-platform-apis/references/audit-query/). Antes de continuar, revise la [guía de introducción](./getting-started.md) para ver vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios para realizar llamadas correctamente a cualquier [!DNL Experience Platform] API.

## Enumerar eventos de auditoría

Puede recuperar los datos de eventos realizando una solicitud de GET al `/audit/events` , especificando los eventos que desea recuperar en la carga útil.

**Formato de API**

```http
GET /audit/events
```

La variable [!DNL Audit Query] La API de admite el uso de parámetros de consulta en la página y filtrar los resultados al enumerar eventos.

| Parámetro | Descripción |
| --- | --- |
| `limit` | Número máximo de registros que se van a devolver en la respuesta. El valor predeterminado `limit` es 50. |
| `start` | Un puntero al primer elemento de los resultados de búsqueda devueltos. Para acceder a la siguiente página de resultados, este parámetro debe incrementarse en la misma cantidad indicada por limit. Ejemplo: Para acceder a la siguiente página de resultados para una solicitud con límite=50, utilice el parámetro start=50, start=100 para la página después de eso, etc. |
| `queryId` | Al realizar una consulta al extremo /audit/events , la respuesta incluye una propiedad de cadena queryId . Para realizar la misma consulta en una llamada separada, puede incluir el valor Id como un solo parámetro de consulta en lugar de configurar manualmente los parámetros de búsqueda de nuevo. |

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
     "customerAuditLogList": [
       {
         "userEmail": "{USER_ID}",
         "userIpAddresses": [ ],
         "eventType": "Core",
         "id": "32b72208-3035-4bc6-b434-39e34401a864",
         "version": "1.0",
         "imsOrgId": "{ORGANIZATION_ID}",
         "sandboxName": "prod",
         "region": "VA7",
         "requestId": "5NphpgUQdQnjTWOcS9DSMs2wD1EUMlYG",
         "authId": "96715f98-d100-4575-8491-ebbcea654eb9",
         "permissionResource": "Sandbox",
         "permissionType": "RESET",
         "assetType": "Sandbox",
         "assetId": "prod",
         "assetName": "prod",
         "action": "Reset",
         "status": "Allow",
         "failureCode": "",
         "timestamp": "2021-08-04T21:58:09.745+0000"
       },
       {
         "userEmail": "{USER_ID}",
         "userIpAddresses": [ ],
         "eventType": "Core",
         "id": "a178736a-8fa1-47da-bac5-b0d9e741e414",
         "version": "1.0",
         "imsOrgId": "{ORGANIZATION_ID}",
         "sandboxName": "prod",
         "region": "VA7",
         "requestId": "7AlGIAhWvaEzYWHLzvuf26AAFAkqSyKg",
         "authId": "60fc1077-4aef-4e1f-a5ff-f64183e060f4",
         "permissionResource": "Sandbox",
         "permissionType": "RESET",
         "assetType": "Sandbox",
         "assetId": "prod",
         "assetName": "prod",
         "action": "Reset",
         "status": "Allow",
         "failureCode": "",
         "timestamp": "2021-08-04T21:28:00.301+0000"
       },
       {
         "userEmail": "{USER_ID}",
         "userIpAddresses": [ ],
         "eventType": "Core",
         "id": "ccfe8c77-9b93-481d-a561-0b2edf3b77dc",
         "version": "1.0",
         "imsOrgId": "{ORGANIZATION_ID}",
         "sandboxName": "prod",
         "region": "VA7",
         "requestId": "hArqS4CAa8wfRPnKuxV4yaA82atxwzYu",
         "authId": "80b7d887-9338-4cd5-9d79-2483b03f0160",
         "permissionResource": "Sandbox",
         "permissionType": "RESET",
         "assetType": "Sandbox",
         "assetId": "prod",
         "assetName": "prod",
         "action": "Reset",
         "status": "Allow",
         "failureCode": "",
         "timestamp": "2021-08-04T20:58:07.750+0000"
       }
     ]    
   },
   "_links": {
     "self": {
       "href": "https://platform-int.adobe.io/data/foundation/audit/events?limit=10&start=0&property=type%253D%253Dcore"
     },
     "next": {
       "href": "https://platform-int.adobe.io/data/foundation/audit/events?queryId=cXVlcnlJZD0xYjA4MDM4MV81ZWNkXzRjNTZfYTM2N18zYWExOWI5YzNhNTlfMTYyODExNDY5MTg1NSZ0b3RhbEVsZW1lbnRzPTI2&start=10&limit=10"
     },
     "page": {
       "href": "https://platform-int.adobe.io/data/foundation/audit/events?queryId=cXVlcnlJZD0xYjA4MDM4MV81ZWNkXzRjNTZfYTM2N18zYWExOWI5YzNhNTlfMTYyODExNDY5MTg1NSZ0b3RhbEVsZW1lbnRzPTI2&limit=10{&start}",
       "templated": true
     }
  },
  "page": {
    "size": 10,
    "totalElements": 3,
    "totalPages": 1,
    "number": 1
  },
  "queryId": "cXVlcnlJZD0xYjA4MDM4MV81ZWNkXzRjNTZfYTM2N18zYWExOWI5YzNhNTlfMTYyODExNDY5MTg1NSZ0b3RhbEVsZW1lbnRzPTI2"
}
```

| Propiedad | Descripción |
| --- | --- |
| `customerAuditLogList` | Matriz cuyos objetos representan cada uno de los eventos especificados en la solicitud. Cada objeto contiene información sobre la configuración del filtro y los datos de evento devueltos. |
| `userEmail` | El correo electrónico del usuario que realizó el evento. |
| `eventType` | Tipo de evento. Los tipos de eventos incluyen `Core` y `Enhanced`. |
| `imsOrgId` | ID de la organización en la que se celebró el evento. |
| `permissionResource` | El producto o la capacidad que proporcionó el permiso realizan la acción. Un recurso puede ser cualquiera de los siguientes: <ul><li>`Activation` </li><li>`ActivationAssociation` </li><li>`AnalyticSource` </li><li>`AudienceManagerSource` </li><li>`BizibleSource` </li><li>`CustomerAttributeSource` </li><li>`Dataset` </li><li>`EnterpriseSource` </li><li>`LaunchSource` </li><li>`MarketoSource` </li><li>`ProductProfile` </li><li>`ProfileConfig` </li><li>`Sandbox` </li><li>`Schema` </li><li>`Segment` </li><li>`StreamingSource` </li></ul> |
| `permissionType` | El tipo de permiso asociado a la acción. |
| `assetType` | Tipo de recurso de Platform en el que se realizó la acción. |
| `assetId` | Identificador único del recurso de Platform en el que se realizó la acción. |
| `assetName` | Nombre del recurso de Platform en el que se realizó la acción. |
| `action` | Tipo de acción que se registró para el evento. Una acción puede ser cualquiera de las siguientes: <ul><li>`Add` </li><li>`Create` </li><li>`Dataset activate` </li><li>`Dataset remove` </li><li>`Delete` </li><li>`Disable for profile` </li><li>`Enable` </li><li>`Enable for profile` </li><li>`Profile activate` </li><li>`Profile remove` </li><li>`remove` </li><li>`reset` </li><li>`segment activate` </li><li>`segment remove` </li><li>`update` </li></ul> |
| `status` | Estado de la acción. Un estado puede ser cualquiera de los siguientes: </li><li>`Allow` </li><li>`Deny` </li><li>`Failure` </li><li>`Success` </li></ul> |

{style=&quot;table-layout:auto&quot;}
