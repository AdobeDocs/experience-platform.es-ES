---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;guía de api;parámetros de conexión;servicio de consulta;
solution: Experience Platform
title: Punto final de API de parámetros de conexión
description: Puede recuperar los parámetros de conexión para utilizar el servicio interactivo realizando una solicitud de GET al extremo /connection_parameters.
exl-id: 1667f4a5-e6e5-41e9-8f9d-6d2c63c7d7d6
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 3%

---

# Extremo de parámetros de conexión

## Llamada de API de ejemplo

La siguiente sección lo acompaña durante la llamada a la API que puede realizar mediante la función [!DNL Query Service] API. La llamada incluye el formato de API general, una solicitud de ejemplo que muestra los encabezados necesarios y una respuesta de ejemplo.

### Solicitar parámetros de conexión

Puede recuperar los parámetros de conexión realizando una solicitud de GET al `/connection_parameters` punto final. Para obtener más información sobre los clientes que utilizan parámetros de conexión para conectarse mediante el servicio interactivo, lea la documentación de [Clientes del servicio de consultas](../clients/overview.md).

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
