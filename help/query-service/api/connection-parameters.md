---
keywords: Experience Platform;home;popular topics;query service;api guide;connection parameters;Query service;
solution: Experience Platform
title: Guía para desarrolladores de consulta Service
topic: connection parameters
description: Puede recuperar los parámetros de conexión para utilizar el servicio interactivo haciendo una solicitud de GET al extremo /connection_parameters.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 1%

---


# Parámetros de conexión

## Ejemplos de llamadas a API

Ahora que comprende qué encabezados usar, está listo para empezar a realizar llamadas a la [!DNL Query Service] API. Las siguientes secciones explican las distintas llamadas de API que puede realizar con la [!DNL Query Service] API. Cada llamada incluye el formato de API general, una solicitud de muestra que muestra los encabezados necesarios y una respuesta de ejemplo.

### Solicitar parámetros de conexión para el servicio interactivo

Puede recuperar los parámetros de conexión para utilizar el servicio [](../creating-queries/writing-queries.md) interactivo haciendo una solicitud de GET al `/connection_parameters` extremo. Para obtener más información sobre los clientes que utilizan parámetros de conexión para conectarse mediante el servicio interactivo, lea la documentación sobre los clientes [del servicio de](../clients/overview.md)Consulta.

**Formato API**

```http
GET /connection_parameters
```

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/connection_parameters
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con los parámetros de conexión.

```json
{
    "username": "{USERNAME}",
    "dbName": "prod:all",
    "host": "{HOSTNAME}",
    "version": 1,
    "port": 80,
    "token": "{TOKEN}",
    "compressedToken": "{COMPRESSED_TOKEN}",
    "websocketHost": "{WEBSOCKET_HOSTNAME}"
}
```
