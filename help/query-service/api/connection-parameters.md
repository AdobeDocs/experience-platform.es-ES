---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;guía de API;parámetros de conexión;servicio de Consulta;
solution: Experience Platform
title: Guía para desarrolladores de consulta Service
topic: connection parameters
description: Puede recuperar los parámetros de conexión para utilizar el servicio interactivo haciendo una solicitud de GET al extremo /connection_parameters.
translation-type: tm+mt
source-git-commit: 648544bc60c0cee8ca8b167118391980b6c33d91
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 1%

---


# Parámetros de conexión

## Ejemplos de llamadas a API

Ahora que comprende qué encabezados usar, está listo para empezar a realizar llamadas a la API [!DNL Query Service]. Las siguientes secciones explican las distintas llamadas de API que puede realizar mediante la API [!DNL Query Service]. Cada llamada incluye el formato de API general, una solicitud de muestra que muestra los encabezados necesarios y una respuesta de ejemplo.

### Solicitar parámetros de conexión

Puede recuperar los parámetros de conexión realizando una solicitud de GET al extremo `/connection_parameters`. Para obtener más información acerca de los clientes que utilizan parámetros de conexión para conectarse mediante el servicio interactivo, lea la documentación sobre [clientes del servicio de Consulta](../clients/overview.md).

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
