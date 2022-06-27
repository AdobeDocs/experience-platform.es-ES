---
title: Recopilación de datos interactiva
description: Descubra cómo la API de servidor de red perimetral de Adobe Experience Platform realiza la recopilación de datos interactiva.
exl-id: 1b06e755-b6a9-42dd-96c1-98ad67e7d222
source-git-commit: f52603f7e65ac553e00a2b632857561cd07ae441
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 7%

---

# Recopilación de datos interactiva

## Información general {#overview}

Los extremos de recopilación de datos interactivos reciben un solo evento y se utilizan cuando el cliente espera que el servidor Adobe Experience Platform Edge Network devuelva una respuesta. Estos extremos también pueden devolver contenido de otros servicios de Experience Edge al realizar la recopilación de datos.

La respuesta del servidor incluye una o más `Handle` como se muestra a continuación.

## Ejemplo de llamada a la API

### Formato de API {#format}

```http
POST /ee/v2/interact
```

### Solicitud {#request}

```shell
curl -X POST "https://server.adobedc.net/ee/v2/interact?dataStreamId={DATASTREAM_ID}" 
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {ORG_ID}" 
-H "x-api-key: {API_KEY}" 
-H "Content-Type: application/json" 
-d '{
   "event": {
      "xdm": {
         "identityMap": {
            "Email_LC_SHA256": [
               {
                  "id": "0c7e6a405862e402eb76a70f8a26fc732d07c32931e9fae9ab1582911d2e8a3b",
                  "primary": true
               }
            ]
         },
         "eventType": "web.webpagedetails.pageViews",
         "web": {
            "webPageDetails": {
               "URL": "https://alloystore.dev/",
               "name": "home-demo-Home Page"
            }
         },
         "timestamp": "2021-08-09T14:09:20.859Z"
      },
      "data": {
         "prop1": "custom value"
      }
   }
}'
```

| Parámetro | Tipo | Requerido | Descripción |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | Sí. | ID de almacén de datos. |
| `requestId` | `String` | No | Proporcione un ID aleatorio de cliente para correlacionar solicitudes de servidor internas. Si no se proporciona ninguno, la red perimetral generará uno y lo devolverá en la respuesta. |

### Respuesta {#response}

Una respuesta correcta devuelve el estado HTTP `200 OK`, con uno o más `Handle` objetos, según los servicios Edge en tiempo real habilitados en la configuración del conjunto de datos.

```json
{
   "requestId": "c85402f5-83a1-4fb3-abdd-f4c17bf6dd49",
   "handle": []
}
```
