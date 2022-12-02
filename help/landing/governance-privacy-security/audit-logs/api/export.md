---
title: Punto final de API de exportación de eventos de auditoría
description: Obtenga información sobre cómo exportar eventos de auditoría en Experience Platform mediante la API de consulta de auditoría.
source-git-commit: 5b3459711f41430977f9d7b06f8b35801739207c
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 3%

---

# Exportación de una lista de eventos de auditoría

Puede recuperar los datos de eventos realizando una solicitud de GET al `/audit/export` , especificando los eventos que desea recuperar en la carga útil.

**Formato de API**

```http
GET /audit/export
```

| Parámetro | Descripción |
| --------- | ----------- |
| `timestamp` | Al filtrar por marca de tiempo, se recomienda utilizar un intervalo con operadores > y &lt; en lugar de un valor exacto. <br/>Ejemplo: ?property=timestamp&lt;2020-02-08T02:46:48.610862Z&amp;property=timestamp>2020-01-01T02:46:48,610862Z. |
| `status` | Estado de la acción. Un estado puede ser cualquiera de los siguientes: </li><li>`Allow` </li><li>`Deny` </li><li>`Failure` </li><li>`Success` </li></ul> |
| `action` | Tipo de acción que se registró para el evento. Una acción puede ser cualquiera de las siguientes: <ul><li>`Add` </li><li>`Create` </li><li>`Dataset activate` </li><li>`Dataset remove` </li><li>`Delete` </li><li>`Disable for profile` </li><li>`Enable` </li><li>`Enable for profile` </li><li>`Profile activate` </li><li>`Profile remove` </li><li>`remove` </li><li>`reset` </li><li>`segment activate` </li><li>`segment remove` </li><li>`update` </li></ul> |
| `user` | El usuario que realizó el evento. |
| `assetType` | Tipo de recurso de Platform en el que se realizó la acción. |

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

Los resultados se generan en un archivo CSV para su exportación. Una respuesta correcta devuelve HTTP 307 sin cuerpo de respuesta. En la sección `Location` encabezado de respuesta.
