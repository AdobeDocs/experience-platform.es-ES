---
keywords: Experience Platform;inicio;temas populares;servicio de consultas;guía de api;parámetros de conexión;servicio de consultas;
solution: Experience Platform
title: Punto final de API de parámetros de conexión
description: Puede recuperar los parámetros de conexión para mediante el servicio interactivo realizando una solicitud de GET al extremo /connection_parameters.
role: Developer
exl-id: 1667f4a5-e6e5-41e9-8f9d-6d2c63c7d7d6
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 3%

---

# Extremo de parámetros de conexión

## Llamada de API de ejemplo

La siguiente sección lo acompañará a través de la llamada de API que puede realizar mediante la API [!DNL Query Service]. La llamada incluye el formato de API general, una solicitud de ejemplo que muestra los encabezados necesarios y una respuesta de ejemplo.

### Solicitar parámetros de conexión

Puede recuperar los parámetros de conexión realizando una solicitud de GET al extremo `/connection_parameters`. Para obtener más información acerca de los clientes que usan parámetros de conexión para conectarse a través del servicio interactivo, lea la documentación sobre [clientes del servicio de consultas](../clients/overview.md).

**Formato de API**

```http
GET /connection_parameters
```

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/connection_parameters
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
