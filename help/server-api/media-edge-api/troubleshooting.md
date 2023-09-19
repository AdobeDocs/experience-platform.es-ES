---
solution: Experience Platform
title: Introducción a las API de Media Edge
description: Guía de solución de problemas de las API de Media Edge
source-git-commit: 3272db15283d427eb4741708dffeb8141f61d5ff
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 0%

---


# Guía de solución de problemas de API de Media Edge

Esta guía proporciona instrucciones para solucionar problemas, gestionar errores y obtener respuestas correctas.

## Uso de ayudas de respuesta de error

Para ayudar a solucionar problemas de respuestas fallidas, los errores van acompañados de un cuerpo de respuesta que contiene un objeto de error. En este caso, el cuerpo de la respuesta contiene detalles del problema, tal como se define en [RFC 7807: Detalles del problema para API HTTP](https://datatracker.ietf.org/doc/html/rfc7807). Para mejorar la experiencia del usuario de la API, los detalles del problema son descriptivos (los detalles de las claves de matriz se muestran mediante JsonPath en el campo que falta o no es válido). También son acumulativos (todos los campos no válidos se incluirán en la misma solicitud).


## Validando inicios de sesión

La mayoría de los problemas con las solicitudes de Inicio de sesión provocan una respuesta de varios estados 207.
La carga útil es similar a [API de servidor](../error-handling.md)Errores no fatales de. Todos los errores de Media Analytics tienen el siguiente tipo:  `https://ns.adobe.com/aep/errors/va-edge-0XXX-XXX`. Los números mostrados en la respuesta corresponden al estado de error.

El siguiente ejemplo muestra un cuerpo de respuesta para una solicitud de inicio de sesión que carece de un campo obligatorio y tiene uno no válido.

```
{
    "requestId": "d4be4f91-a535-41e7-80c6-bdd031d3a365",
    "handle": [
        ...
    ],
    "errors": [
        {
            "type": "https://ns.adobe.com/aep/errors/va-edge-0400-400",
            "status": 400,
            "title": "Invalid request",
            "report": {
                "eventIndex": 0,
                "details": [
                    {
                        "name": "$.xdm.mediaCollection.sessionDetails.name",
                        "reason": "Missing required field"
                    },
                    {
                        "name": "$.xdm.timestamp",
                        "reason": "Field should respect ISO 8601 standard for presenting date and time with offset to UTC (e.g. 2022-05-19T19:31:02Z, 2022-05-19T21:31:02+02:00, 2022-05-19T21:31:02.234+02:00)"
                    }
                ]
            }
        }
    ]
}
```

En el ejemplo anterior, ambos problemas se registran por `name` y `reason` bajo `details`: se muestra la primera razón `missing required field` y el segundo describe el incumplimiento de la norma ISO 8601.


>[!NOTE]
>
> Para los errores que se producen en orden ascendente desde Media Analytics, Adobe recomienda que continúe procesando la sesión de medios generada.

## Validación de eventos

La mayoría de las solicitudes de evento no válidas generan una respuesta 400 de solicitud incorrecta. En estos casos, la carga útil es similar a los errores irrecuperables de la API del servidor.

Para solicitudes de evento, el servicio de API de Edge de medios incluye comprobaciones adicionales que no se capturan en el propio modelo XDM. Esto incluye la comprobación de que la ruta `eventType` coincide con la carga útil solicitada `eventType`.


El siguiente ejemplo muestra un `eventType` no coincide con un `adBreakStart` carga útil enviada a `ee/va/v1/chapterStart`:

```
{
    "type": "https://ns.adobe.com/aep/errors/va-edge-0400-400",
    "status": 400,
    "title": "Bad Request",
    "detail": "Invalid request. Please check your input and try again.",
    "report": {
        "details": "The payload eventType adBreakStart was different from the path eventType chapterStart"
    }
}
```

El siguiente ejemplo muestra una comprobación adicional de la API de Media Edge que busca una `chapterStart` llamada perdida `chapterDetails` información:

```
{
    "type": "https://ns.adobe.com/aep/errors/va-edge-0400-400",
    "status": 400,
    "title": "Bad Request",
    "detail": "Invalid request. Please check your input and try again.",
    "report": {
        "details": [
            {
                "name": "$.events[0].xdm.mediaCollection.chapterDetails",
                "reason": "Missing required field"
            }
        ]
    }
}
```

## Gestión de errores de 400 niveles y 500 niveles

En la tabla siguiente se proporcionan instrucciones para controlar los errores de respuesta de estado:


| Código de error | Descripción |
| ---------- | --------- |
| 4xx Solicitud incorrecta | La mayoría de los errores 4xx (p. ej. `400`, `403`, `404`) no debería volver a intentarlo el usuario. Si se vuelve a intentar la solicitud, la respuesta no se realizará correctamente. El usuario debe corregir el error antes de volver a intentar la solicitud. Los eventos que generan códigos de estado 4xx no se rastrean, lo que podría afectar a la precisión de los datos en las sesiones que recibieron respuestas 4xx. |
| 410 desaparecido | Indica que la sesión destinada al seguimiento ya no se calcula en el lado del servidor. El motivo más común es que la sesión dura más de 24 horas. Después de recibir una `410`, intente iniciar una nueva sesión y realice un seguimiento de la misma. |
| Demasiadas solicitudes | Este código de respuesta indica que el servidor limita la velocidad de las solicitudes. Siga las **Retry-After** instrucciones en el encabezado de respuesta con cuidado. Las respuestas que regresen deben llevar el código de respuesta HTTP con un código de error específico del dominio. |
| 500 Error interno del servidor | `500` los errores son errores genéricos y captaces. `500` los errores no se deben volver a intentar, excepto para `502`, `503` y `504`. |
| 502 Puerta de enlace incorrecta | Este código de error indica que el servidor, mientras actuaba como puerta de enlace, recibió una respuesta no válida de los servidores de flujo ascendente. Esto puede deberse a problemas de red entre servidores. El problema de red temporal puede resolverse solo, por lo que si vuelve a intentar la solicitud, puede resolverse. |
| 503 Servicio no disponible | Este código de error indica que el servicio no está disponible temporalmente. Esto puede ocurrir durante los períodos de mantenimiento. Destinatarios de `503` Los errores de pueden reintentar la solicitud, pero también deben seguir el **Retry-After** instrucciones de encabezado. |


## Poner eventos en cola cuando las respuestas de sesión son lentas

Después de iniciar una sesión de seguimiento de contenido, el reproductor de contenido puede activarse antes de recibir la respuesta de inicio de sesión (con el parámetro ID de sesión) del servidor. Si esto sucede, la aplicación debe poner en cola los eventos de seguimiento que lleguen entre la Solicitud de inicio de sesión y su respuesta. Cuando llega la respuesta de sesiones, primero debe procesar los eventos en cola y, a continuación, iniciar el procesamiento de eventos en directo.

Para obtener los mejores resultados, consulte el reproductor de referencia de su distribución para obtener instrucciones sobre cómo procesar eventos antes de recibir un ID de sesión.

El siguiente ejemplo muestra un método para procesar eventos antes de recibir un ID de sesión:


```
// For event payload format, see "Request body" sections of "Session Start Request", "Event Requests" respectively.  *
 
VideoPlayer.prototype._collectEvent = function(event) {
    var sessionID = event.events[0].xdm.mediaCollection.sessionID
    var eventType = event.events[0].xdm.eventType.substring("media.".length);
    // If we don't have a Session ID yet,
    // queue the event and return...
    if (sessionId === undefined) {
        console.log("[Player] Queueing event")
        _pendingEvents.push(event)
        return;
    }
 
    // If we DO have a Session ID, process the
    // tracking event...
    apiClient.request({
        "baseUrl": `${endpoint}`,
        "path": `ee/va/v1/${eventType}`,
        "method": `POST`,
        "data": `${event}`
    }).then((response) => {
        if (eventType === "sessionStart") {
            var newSessionID = response.json().handle.filter((h) => h.type === "media-analytics:new-session")[0].payload[0].sessionId;
            _processPendingEvents(newSessionID);
        }
        […]
    }
}
 
VideoPlayer.prototype._processPendingEvents function(sessionID) {
    _pendingEvents.forEach((event) => {
        event.events[0].xdm.mediaCollection.sessionID = sessionID;
        _collectEvent(event);
    });
    _pendingEvents = [];
}
```


