---
title: Extremo de API de exportación de eventos de auditoría
description: Obtenga información sobre cómo exportar eventos de auditoría en Experience Platform mediante la API de consulta de auditoría.
role: Developer
feature: Audits, API
exl-id: 76c5de76-e391-4258-afd8-ddb2c8a9443f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 4%

---

# Exportar una lista de eventos de auditoría

Puede recuperar datos de eventos realizando una petición GET al extremo `/audit/export`, especificando los eventos que desea recuperar en la carga útil.

**Formato de API**

```http
GET /audit/export
```

| Parámetro | Descripción |
| --------- | ----------- |
| `timestamp` | Al filtrar por marca de tiempo, se recomienda utilizar un rango que utilice los operadores > y &lt; en lugar de un valor exacto. <br/>Ejemplo: `?property=timestamp<2020-02-08T02:46:48.610862Z&property=timestamp>2020-01-01T02:46:48.610862Z`. |
| `status` | El estado de la acción. Un estado puede ser cualquiera de los siguientes: </li><li>`Allow` </li><li>`Deny` </li><li>`Failure` </li><li>`Success` </li></ul><br/>Ejemplo: `?property=status==Deny`. |
| `action` | El tipo de acción que se registró para el evento. Una acción puede ser cualquiera de las siguientes: <ul><li>`Add` </li><li>`Create` </li><li>`Dataset activate` </li><li>`Dataset remove` </li><li>`Delete` </li><li>`Disable for profile` </li><li>`Enable` </li><li>`Enable for profile` </li><li>`Profile activate` </li><li>`Profile remove` </li><li>`Remove` </li><li>`Reset` </li><li>`Segment Activate` </li><li>`Segment remove` </li><li>`Update` </li></ul> Ejemplo: `?property=action==Create`. |
| `user` | El usuario que realizó el evento. |
| `assetType` | El tipo de recurso de Experience Platform en el que se realizó la acción. <br/>Ejemplo: `?property=assetType==<an asset type>`. |

**Solicitud**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/audit/events
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {TRACING_ID}' \
```

**Respuesta**

Los resultados se generan en un archivo CSV para su exportación. Una respuesta correcta devuelve HTTP 307 sin cuerpo de respuesta. Se ha proporcionado un vínculo al archivo de exportación en el encabezado de respuesta `Location`.
