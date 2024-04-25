---
title: Recopilación de datos interactiva
description: Descubra cómo la API de Adobe Experience Platform Edge Network Server realiza la recopilación de datos interactiva.
exl-id: 1b06e755-b6a9-42dd-96c1-98ad67e7d222
source-git-commit: f8434746c4a023ec895d23a59e04fca4baecfc36
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 5%

---

# Recopilación de datos interactiva

## Información general {#overview}

Los extremos de recopilación de datos interactivos reciben un único evento y se utilizan cuando el cliente espera que el servidor del Edge Network de Adobe Experience Platform devuelva una respuesta. Estos extremos también pueden devolver contenido de otros servicios de Edge Network, mientras realizan la recopilación de datos.

>[!IMPORTANT]
>
>El `/interact` El extremo está diseñado principalmente para que lo utilicen los SDK de Experience Platform. Este punto de conexión está sujeto a cambios adicionales y su comportamiento puede evolucionar sin previo aviso. Por ejemplo, en el futuro, se podrían añadir nuevos elementos a la carga útil de respuesta.

La respuesta del servidor incluye una o más `Handle` como se muestra a continuación.

## Ejemplo de llamada de API

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
| `dataStreamId` | `String` | Sí. | ID de flujo de datos. |
| `requestId` | `String` | No | Proporcione un ID aleatorio de cliente para correlacionar las solicitudes internas del servidor. Si no se proporciona ninguno, el Edge Network genera uno y lo devuelve en la respuesta. |

### Respuesta {#response}

Una respuesta correcta devuelve el estado HTTP. `200 OK`, con uno o más `Handle` según los servicios perimetrales en tiempo real habilitados en la configuración del conjunto de datos.

```json
{
   "requestId": "c85402f5-83a1-4fb3-abdd-f4c17bf6dd49",
   "handle": []
}
```
