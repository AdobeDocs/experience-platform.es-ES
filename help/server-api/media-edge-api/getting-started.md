---
solution: Experience Platform
title: Introducción a las API de Media Edge
description: Introducción a las API de Media Edge
source-git-commit: 3d0f2823dcf63f25c3136230af453118c83cdc7e
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 5%

---


# Introducción a la API de Media Edge

Esta guía proporciona instrucciones para realizar interacciones iniciales correctas con el servicio de API de Media Edge. Esto incluye el inicio de una sesión de contenido y el seguimiento de eventos que se envían a una solución de Adobe Experience Platform como Customer Journey Analytics (CJA). El servicio de API de Media Edge se inicia con el punto de conexión de inicio de sesión. Una vez iniciada la sesión, se puede realizar el seguimiento de uno o más de los siguientes eventos:

* `play`
* `ping`
* `bitrateChange`
* `bufferStart`
* `pauseStart`
* `adBreakStart`
* `adStart`
* `adComplete`
* `adSkip`
* `adBreakComplete`
* `chapterStart`
* `chapterComplete`
* `chapterSkip`
* `error`
* `sessionEnd`
* `sessionComplete`
* `statesUpdate`

Cada evento tiene su propio punto final. Todos los extremos de la API de Media Edge son métodos de POST, con cuerpos de solicitud JSON para datos de evento. Para obtener más información sobre los extremos, parámetros y ejemplos de la API de Media Edge, consulte la [Archivo Swagger de Media Edge](swagger.md).

Esta guía muestra cómo realizar un seguimiento de los siguientes eventos después de iniciar la sesión:

* [Inicio del búfer](#buffer-start-event-request)
* [Play](#play-event-request)
* [Sesión completa](#session-complete-event-request)

## Implementación de la API {#implement-api}

Aparte de pequeñas diferencias en el modelo y las rutas denominadas, la API de Media Edge tiene la misma implementación que la variable [API de Media Collection](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-overview.html?lang=en). Los detalles de implementación de Media Collection siguen siendo válidos para la API de Media Edge, tal como se describe en la siguiente documentación:

* [Configuración del tipo de solicitud HTTP en el reproductor](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-impl/mc-api-sed-pings.html?lang=en)
* [Envío de eventos ping](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-impl/mc-api-sed-pings.html?lang=en)
* [Condiciones de tiempo de espera](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-impl/mc-api-timeout.html?lang=en)
* [Control del orden de los eventos](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-impl/mc-api-ctrl-order.html?lang=en)

## Autorización {#authorization}

Actualmente, las API de Media Edge no requieren encabezados de autorización en sus solicitudes.


## Inicio de la sesión {#start-session}

Para iniciar la sesión de contenido en el servidor, utilice el punto final de Inicio de sesión. Una respuesta correcta incluye una `sessionId`, que es un parámetro obligatorio para solicitudes de eventos posteriores.

Antes de realizar la solicitud de inicio de sesión, necesitará lo siguiente:

* El `datastreamId`: un parámetro requerido para la solicitud de inicio de sesión de POST. Para recuperar un `datastreamId`, consulte [Configuración de una secuencia de datos](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html?lang=es).

* Un objeto JSON para la carga útil de la solicitud que contiene los datos mínimos requeridos (como se muestra en la solicitud de ejemplo siguiente).

Una vez que tenga esta información, proporcione el `datastreamId` en la siguiente llamada:

**POST**  `https://edge.adobedc.net/ee-pre-prd/va/v1/sessionStart?configId={datastream ID} \`

### Solicitud de ejemplo

El siguiente ejemplo muestra una solicitud cURL de inicio de sesión:

```
curl -i --request POST '{uri}/ee/va/v1/sessionStart?configId={dataStreamId}' \
--header 'Content-Type: application/json' \
--data-raw '{
  "events": [
    {
      "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
          "sessionDetails": {
            "name": "Media Analytics API Sample",
            "playerName": "sample-html5-api-player",
            "contentType": "VOD",
            "length": 60,
            "channel": "sample-channel",
            "appVersion": "va-api-1.0.0"
          },
          "playhead": 0
        }
      }
    }
  ]
}'
```

En la solicitud de ejemplo anterior, la variable `eventType` el valor contiene el prefijo `media.` según el [Modelo de datos de experiencia (XDM)](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=es) para especificar dominios.

Además, la asignación de tipos de datos para `eventType` en el ejemplo anterior son las siguientes:

| eventType | datatypes |
| -------- | ------ |
| media.SessionStart | [sessionDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/sessiondetails.schema.md) |
| media.chapterStart | [chapterDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/chapterdetails.schema.md) |
| media.adBreakStart | [advertisingPodDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/advertisingpoddetails.schema.md) |
| media.adStart | [advertisingDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/advertisingdetails.schema.md) |
| media.error | [errorDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/errordetails.schema.md) |
| media.statesUpdate | [statesStart](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/mediadetails.schema.md#xdmstatesstart): matriz[playerStateData], [statesEnd](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/mediadetails.schema.md#xdmstatesend): matriz[playerStateData] |
| media.sessionStart, media.chapterStart, media.adStart | [customMetadata](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/mediadetails.schema.md#xdmcustommetadata) |
| todo | [qoeDataDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/qoedatadetails.schema.md) |

### Respuesta de ejemplo

El siguiente ejemplo muestra una respuesta correcta para la solicitud de inicio de sesión:

```
HTTP/2 200
x-request-id: 99603f5c-95cf-49ad-9afb-0ba6c5867fd7
x-rate-limit-remaining: 599
vary: Origin
date: Tue, 07 Mar 2023 14:37:58 GMT
x-konductor: 23.3.2:367bc7dc
x-adobe-edge: IRL1;6
server: jag
content-type: application/json;charset=utf-8
strict-transport-security: max-age=31536000; includeSubDomains
cache-control: no-cache, no-store, max-age=0, no-transform
x-xss-protection: 1; mode=block
x-content-type-options: nosniff

{
    "requestId": "df14bca1-ba0f-4574-ae80-a4e24a960c00",
    "handle": [
        {
            "payload": [
                {
                    "sessionId": "af8bb22766e458fa0eef98c48ea42c9e351c463318230e851a19946862020333"
                }
            ],
            "type": "media-analytics:new-session",
            "eventIndex": 0
        },
        {
            "payload": [
                {
                    "key": "kndctr_6D9FE18C5536A5E90A4C98A6_AdobeOrg_cluster",
                    "value": "irl1",
                    "maxAge": 1800
                },
                {
                    "key": "kndctr_6D9FE18C5536A5E90A4C98A6_AdobeOrg_identity",
                    "value": "CiY1MTkxMDM4OTc1MzkwMTY4NTQ1NjAxNDg4OTgzODU5MTAzMDcyMVIPCKKt8KnsMBgBKgRJUkwx8AGirfCp7DA=",
                    "maxAge": 34128000
                }
            ],
            "type": "state:store"
        }
    ]
}
```

En la respuesta de ejemplo anterior, la variable `sessionId` se muestra como `af8bb22766e458fa0eef98c48ea42c9e351c463318230e851a19946862020333`. Utilizará este ID en solicitudes de eventos posteriores como parámetro obligatorio.

Para obtener más información sobre los parámetros y ejemplos de extremo de inicio de sesión, consulte la [Media Edge Swagger](swagger.md) archivo.

Para obtener más información sobre los parámetros de datos de medios XDM, consulte [Esquema de información de detalles de medios](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/mediadetails.schema.md#xdmplayhead).


## Solicitud de evento de inicio de búfer {#buffer-start}

El evento Inicio del búfer indica cuándo se inicia el almacenamiento en búfer en el reproductor de contenido. La reanudación del búfer no es un evento en el servicio API, sino que se deduce cuando se envía un evento de reproducción después del inicio del búfer. Para realizar una solicitud de evento de Inicio del búfer, utilice su `sessionId` en la carga útil de una llamada al siguiente extremo:

**POST**  `https://edge.adobedc.net/ee-pre-prd/va/v1/bufferStart \`

### Solicitud de ejemplo

El siguiente ejemplo muestra una solicitud cURL de inicio de búfer:

```
curl -X 'POST' \
  'https://edge.adobedc.net/ee-pre-prd/va/v1/bufferStart' \
  -H 'accept: */*' \
  -H 'Content-Type: application/json' \
  -d '{
  "events": [
    {
      "xdm": {
        "eventType": "media.bufferStart",
        "mediaCollection": {
          "sessionID": "af8bb22766e458fa0eef98c48ea42c9e351c463318230e851a19946862020333",
          "playhead": 25
        },
        "timestamp": "2022-03-04T13:39:00+00:00"
      }
    }
  ]
}'
```

En la solicitud de ejemplo anterior, lo mismo `sessionId` que se devuelve en la llamada anterior se utiliza como parámetro requerido en la solicitud de inicio del búfer.

La respuesta correcta indica un estado de 200 y no incluye ningún contenido.

Para obtener más información sobre los parámetros y ejemplos del extremo de Inicio del búfer, consulte la [Media Edge Swagger](swagger.md) archivo.


## Reproducir solicitud de evento {#play-event}

El evento de reproducción se envía cuando el reproductor de contenido cambia su estado a &quot;reproduciendo&quot; desde otro estado, como &quot;almacenamiento en búfer&quot;, &quot;en pausa&quot; o &quot;error&quot;. Para realizar una solicitud de evento de reproducción, utilice su `sessionId` en la carga útil de una llamada al siguiente extremo:

**POST**  `https://edge.adobedc.net/ee-pre-prd/va/v1/play \`

### Solicitud de ejemplo

El siguiente ejemplo muestra una solicitud de Play cURL:

```
curl -X 'POST' \
  'https://edge.adobedc.net/ee-pre-prd/va/v1/play' \
  -H 'accept: */*' \
  -H 'Content-Type: application/json' \
  -d '{
  "events": [
    {
      "xdm": {
        "eventType": "media.play",
        "mediaCollection": {
          "sessionID": "af8bb22766e458fa0eef98c48ea42c9e351c463318230e851a19946862020333",
          "playhead": 25
        },
        "timestamp": "2022-03-04T13:39:00+00:00"
      }
    }
  ]
}'
```

La respuesta correcta indica un estado de 200 y no incluye ningún contenido.

Para obtener más información sobre los parámetros y ejemplos del punto de conexión de reproducción, consulte la [Media Edge Swagger](swagger.md) archivo.

## Solicitud de evento de sesión completa {#session-complete}

El evento de Finalización de sesión se envía cuando se llega al final del contenido principal. Para realizar una solicitud de evento de Finalización de sesión, utilice su `sessionId` en la carga útil de una llamada al siguiente extremo:

**POST**  `https://edge.adobedc.net/ee-pre-prd/va/v1/sessionComplete \`

### Solicitud de ejemplo

El siguiente ejemplo muestra una solicitud cURL de finalización de sesión:

```
curl -X 'POST' \
  'https://edge.adobedc.net/ee-pre-prd/va/v1/sessionComplete' \
  -H 'accept: */*' \
  -H 'Content-Type: application/json' \
  -d '{
  "events": [
    {
      "xdm": {
        "eventType": "media.sessionComplete",
        "mediaCollection": {
          "sessionID": "af8bb22766e458fa0eef98c48ea42c9e351c463318230e851a19946862020333",
          "playhead": 25
        },
        "timestamp": "2022-03-04T13:39:00+00:00"
      }
    }
  ]
}'
```

La respuesta correcta indica un estado de 200 y no incluye ningún contenido.

Para obtener más información sobre los parámetros y ejemplos de extremo de finalización de sesión, consulte la [Media Edge Swagger](swagger.md) archivo.

## Códigos de respuesta

La siguiente tabla muestra los posibles códigos de respuesta resultantes de las solicitudes de API de Media Edge:

| Estado | Descripción |
| ---------- | --------- |
| 200 | La sesión se ha creado correctamente |
| 207 | Problema con uno de los servicios que se conectan a Experience Edge Network (consulte más información en el [guía de solución de problemas](troubleshooting.md)) |
| de 400 niveles | Solicitud incorrecta |
| de 500 niveles | Error del servidor |

## Más ayuda sobre esta función

* [Guía de solución de problemas de Media Edge](troubleshooting.md)
* [Información general de API de Media Edge](overview.md)


