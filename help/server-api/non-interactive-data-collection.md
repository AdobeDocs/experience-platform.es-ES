---
title: Recopilación de datos no interactiva
description: Descubra cómo la API del servidor de red perimetral de Adobe Experience Platform realiza la recopilación de datos no interactiva.
exl-id: 1a704e8f-8900-4f56-a843-9550007088fe
source-git-commit: f52603f7e65ac553e00a2b632857561cd07ae441
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 5%

---

# Recopilación de datos no interactiva

## Información general {#overview}

Los extremos de recopilación de datos de evento no interactivos se utilizan para enviar varios eventos a conjuntos de datos de Experience Platform u otros medios.

Se recomienda enviar eventos por lotes cuando los eventos del usuario final se ponen en cola localmente durante un corto periodo de tiempo (por ejemplo, cuando no hay conexión de red).

Los eventos por lotes no deben pertenecer necesariamente al mismo usuario final, lo que significa que los eventos pueden contener identidades diferentes dentro de su `identityMap` objeto.

## Ejemplo de llamada de API no interactiva {#example}

### Formato de API {#api-format}

```http
POST /ee/v2/collect
```

### Solicitud {#request}

```shell
curl -X POST "https://server.adobedc.net/ee/v2/collect?dataStreamId={DATASTREAM_ID}" 
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {ORG_ID}" 
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
| `dataStreamId` | `String` | Sí | ID de la secuencia de datos utilizada por el extremo de recopilación de datos. |
| `requestId` | `String` | No | Proporcione un ID de seguimiento de solicitud externa. Si no se proporciona ninguno, la red perimetral generará uno para usted y lo devolverá de nuevo en el cuerpo de respuesta/encabezados. |
| `silent` | `Boolean` | No | Parámetro booleano opcional que indica si la red perimetral debe devolver un `204 No Content` respuesta con una carga útil vacía o no. Los errores críticos se registran utilizando el código de estado HTTP y la carga útil correspondientes. |


### Respuesta {#response}

Una respuesta correcta devuelve uno de los siguientes estados y un `requestID` si no se proporcionó ninguno en la solicitud.

* `202 Accepted` cuando la solicitud se haya procesado correctamente;
* `204 No Content` cuando la solicitud se haya procesado correctamente y la variable `silent` el parámetro se ha establecido en `true`;
* `400 Bad Request` cuando la solicitud no se formó correctamente (por ejemplo, no se encontró la identidad principal obligatoria).

```json
{
  "requestId": "f567a988-4b3c-45a6-9ed8-f283188a445e"
}
```
