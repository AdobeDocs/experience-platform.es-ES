---
title: Recopilación de datos no interactiva
description: Descubra cómo la API de Adobe Experience Platform Edge Network Server realiza una recopilación de datos no interactiva
seo-description: Learn how the Adobe Experience Platform Edge Network Server API performs non-interactive data collection
keywords: recopilación de datos;recopilación;adobe experience platform edge network;api;recopilación de datos no interactiva
source-git-commit: 3bb73e5798d8fcdb6bb8bdcb796e8df6a1bd8805
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 5%

---


# Recopilación de datos no interactiva

## Información general {#overview}

Los extremos de recopilación de datos de eventos no interactivos se utilizan para enviar varios eventos a conjuntos de datos de Experience Platform u otras salidas.

Se recomienda enviar eventos en lote cuando los eventos del usuario final se ponen en cola localmente durante un breve periodo de tiempo (por ejemplo, cuando no hay conexión de red).

Los eventos de lote no deben pertenecer necesariamente al mismo usuario final, lo que significa que los eventos pueden contener identidades diferentes dentro de sus `identityMap` objeto.


<!-- However, when an `ECID` identity is sent via a cookie or metadata (in Edge Network accepted format), the Edge Network will read it and associate it with each event in the batch.

Each event should include the corresponding `XDM` content that needs to be collected.

>[!NOTE]
>
>[Experience Edge Identity Protocol](visitor-identification.md#experience-edge-identity-protocol) (`ECID` generation) is not applicable for data collection requests, meaning that events sent to this API should already have at least one identity associated to them. For server datastreams (calls to `server.adobedc.net`), the API requires that each event contains an identity **explicitly set as primary**. For device datastreams, the Edge Network will attempt to set the `ECID` as primary, when it is present, and no other primary identity is explicitly set.

-->

## Ejemplo de llamada de API no interactiva {#example}

### Formato de API {#api-format}

```http
POST /ee/v2/collect
```

### Solicitud {#request}

```shell
curl -X POST "https://server.adobedc.net/ee/v2/collect?dataStreamId={DATASTREAM_ID}" 
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {IMS_ORG_ID}" 
-H "x-api-key: {API_KEY}" 
-H "Content-Type: application/json" 
-d '{
   "events": [
      {
         "xdm": {
            "identityMap": {
               "FPID": [
                  {
                     "id": "79bf8e83-f708-414b-b1ed-5789ff33bf0b",
                     "primary": "true"
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
      },
      {
         "xdm": {
            "identityMap": {
               "FPID": [
                  {
                     "id": "871e8460-a329-4e96-a5b6-ff359fb0afb9",
                     "primary": "true"
                  }
               ]
            },
            "eventType": "web.webinteraction.linkClicks",
            "web": {
               "webInteraction": {
                  "linkClicks": {
                     "value": 1
                  }
               },
               "name": "My Custom Link",
               "URL": "https://myurl.com"
            },
            "timestamp": "2021-08-09T14:09:20.859Z"
         }
      }
   ]
}'
```

| Parámetro | Tipo | Requerido | Descripción |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | Sí | ID del conjunto de datos utilizado por el extremo de recopilación de datos. |
| `requestId` | `String` | No | Proporcione un ID de seguimiento de solicitud externo. Si no se proporciona ninguno, la red perimetral generará uno por usted y lo devolverá de nuevo en el cuerpo o los encabezados de respuesta. |
| `silent` | `Boolean` | No | Parámetro booleano opcional que indica si la red perimetral debe devolver un `204 No Content` con una carga útil vacía o no. Los errores críticos se notifican utilizando el código de estado HTTP y la carga útil correspondientes. |


### Respuesta {#response}

Una respuesta correcta devuelve uno de los siguientes estados y una `requestID` si no se ha proporcionado ninguno en la solicitud.

* `202 Accepted` cuando la solicitud se haya procesado correctamente;
* `204 No Content` cuando la solicitud se procesó correctamente y la variable `silent` se ha definido como `true`;
* `400 Bad Request` cuando la solicitud no se formó correctamente (por ejemplo, no se encontró la identidad primaria obligatoria).

```json
{
  "requestId": "f567a988-4b3c-45a6-9ed8-f283188a445e"
}
```
