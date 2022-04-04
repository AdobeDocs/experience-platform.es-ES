---
title: Control de errores
description: Obtenga información sobre los posibles errores que podría encontrar al realizar solicitudes de API a la API de Adobe Experience Platform Edge Network Server.
seo-description: Learn about the possible errors you might encounter when performing API requests to the Adobe Experience Platform Edge Network Server API.
keywords: error;código;gestión;edge;red;puerta de enlace;api
exl-id: f6b8435c-b163-4046-b5fb-50a13a897637
source-git-commit: 422f859bef8faf292fd7e5fd8b6a8d31967421c1
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 3%

---

# Control de errores

## Información general {#overview}

Los errores de API en la API de Adobe Experience Platform Edge Network Server pueden tener una variedad de causas, internas (la propia red perimetral) o externas (relacionadas con la entrada, la configuración o el flujo ascendente).

## Tipos de error {#error-types}

| Error | Tipo | Descripción | Código de estado |
| --- | --- | --- | --- |
| `RequestProcessingError` | Internas | Error de propósito general emitido por Adobe Experience Platform Edge Network en circunstancias inesperadas. | `500` |
| `InputError` | Externo | Incluye errores causados por entradas mal formadas, así como errores de validación de entidades. | `4xx` |
| `ConfigurationError` | Externo | Errores de configuración del lado del servidor. | `422` |
| `UpstreamError` | Externo | Errores de comunicación con los servicios de subida. | `207 Multi-Status` |

## Gravedad

Los errores de API de servidor también se pueden dividir por gravedad:

* **Errores fatales** detendrá la canalización de envío.
* **Errores no mortales** podría indicar un procesamiento parcial, mientras que se permite que continúe el procesamiento de la solicitud.
   * Cuando está presente, el código de estado general de la solicitud se cambia a `207 Multi-Status`.

| Error | Tipo | Observaciones |
| --- | --- | --- |
| `RequestProcessingError` | Mortal | Puede ocurrir en cualquier momento durante el procesamiento de la solicitud. |
| `InputError` | Mortal | Sucede al aceptar la solicitud, antes de enviarla de subida. |
| `ConfigurationError` | Mortal | Sucede al aceptar la solicitud, antes de enviarla de subida. |
| `UpstreamError` | No mortal | Errores de comunicación con los servicios de subida. |

### Errores fatales {#fatal-errors}

Los errores fatales detienen el procesamiento de la solicitud y provocan que se devuelva un estado de respuesta que no sea de 2xx. Consulte la [tipos de error](#error-types) para ver el código de estado esperado, correspondiente a cada tipo de error.

Los errores irán acompañados de un cuerpo de respuesta que contenga un objeto de error. En este caso, el cuerpo de la respuesta contiene un detalle del problema, tal como se define en [RFC 7807 Detalles del problema para las API HTTP](https://tools.ietf.org/html/rfc7807).

El tipo de contenido devuelto es el `application/problem+json` tipo de medio. Cuando está presente, esta respuesta contiene detalles legibles por el equipo que pertenecen al error. Los detalles del problema incluyen un tipo de URI.

Todos los objetos de error tienen un valor `type`, `status`, `title`, `detail` y `report` para que el cliente de API pueda saber cuál es el problema.

| Propiedad | Tipo | Descripción |
| -------- | ------ | ----------- |
| `type` | Cadena | Una referencia URI (RFC3986) que identifica el tipo de problema, siguiendo el formato `https://ns.adobe.com/aep/errors/<ERROR-CODE>`. |
| `status` | Número | Código de estado HTTP generado por el servidor para esta incidencia del problema. |
| `title` | Cadena | Breve resumen legible por el usuario del tipo de problema. |
| `detail` | Cadena | Descripción breve y comprensible del tipo de problema. |
| `report` | Objeto | Mapa de propiedades adicionales que ayudan a depurar, como el ID de solicitud o el ID de organización. En algunos casos, puede contener datos específicos del error en cuestión, como una lista de errores de validación. |

```json
{
   "type":"https://ns.adobe.com/aep/errors/EXEG-0104-422",
   "status":422,
   "title":"Unprocessable entity",
   "detail":"Invalid request (report attached). Please check your input and try again.",
   "report":{
      "errors":[
         "Allowed Adobe version is 1.0 for standard 'Adobe' at index 0",
         "Allowed IAB version is 2.0 for standard 'IAB TCF' at index 1",
         "IAB consent string value must not be empty for standard 'IAB TCF' at index 1"
      ],
      "requestId":"0f8821e5-ed1a-4301-b445-5f336fb50ee8",
      "orgId":"53A16ACB5CC1D3760A495C99@AdobeOrg"
   }
}
```

### Errores no mortales {#non-fatal-errors}

Los errores no mortales pueden desglosarse en:

* Errores: Problemas que se produjeron durante el procesamiento de la solicitud, pero que no hicieron que se rechazara toda la solicitud (p. ej. un error ascendente no crítico).
* Advertencias: Mensajes de los servicios de subida que podrían indicar que se ha producido un procesamiento parcial de la solicitud.

Cuando se encuentran errores no mortales (excluidas las advertencias), la variable [!DNL Server API] cambiará el estado de la respuesta a `207 Multi-Status`.

Las advertencias, por otra parte, son en su mayoría informativas, ya que generalmente representan una condición potencialmente transitoria, que no afectó a la solicitud en su totalidad. Un ejemplo a continuación es una lectura parcial del perfil en el motor de segmentación, en cuyo caso la precisión se ve afectada hasta cierto punto, pero la funcionalidad sigue estando disponible.

Los errores no mortales se representan en la variable _Detalles del problema_ , pero están incrustados directamente en la respuesta estándar de Edge gateway, que es del tipo `application/json`.

```json
{
  "requestId": "72eaa048-207e-4dde-bf16-0cb2b21336d5",
  "handle": [
  ],
  "errors": [
    {
      "type": "https://ns.adobe.com/aep/errors/EXEG-0201-503",
      "status": 503,
      "title": "The 'com.adobe.experience.platform.ode' service is temporarily unable to serve this request. Please try again later."
    }
  ],
  "warnings": [
    {
      "type": "https://ns.adobe.com/aep/errors/EXEG-0204-200",
      "status": 200,
      "title": "A warning occurred while calling the 'com.adobe.audiencemanager' service for this request.",
      "report": {
        "cause": {
          "message": "Cannot read related customer for device id: ...",
          "code": 202
        }
      }
    }
  ]
}
```

## Gestión `4xx` y `5xx` Respuestas


| Código de error | Descripción |
|---|---|
| `4xx Bad Request` | Más `4xx` los errores, como 400, 403, 404, no se deben volver a intentar en nombre del cliente, excepto para `429`. Estos son errores de cliente y no se producirán correctamente. El cliente debe solucionar el error antes de volver a intentar la solicitud. |
| `429 Too Many Requests` | `429` El código de respuesta HTTP indica que la red perimetral de Adobe Experience Platform o un servicio ascendente limita la velocidad de las solicitudes. En este caso, el llamador debe respetar el `Retry-After` encabezado de respuesta. Cualquier respuesta que se devuelva debe llevar el código de respuesta HTTP con un código de error específico del dominio. |
| `500 Internal Server Error` | `500` los errores son genéricos, errores generales. `500` los errores no se deben volver a intentar, excepto para `502` y `503`. Los intermediarios deben responder con una `500` y puede responder con un código/mensaje de error genérico o con un código/mensaje de error más específico del dominio. |
| `502 Bad Gateway` | Indica que Adobe Experience Platform Edge Network recibió una respuesta no válida de los servidores de flujo ascendente. Esto puede deberse a problemas de red entre servidores. El problema de red temporal puede resolverse y, por lo tanto, un reintento puede resolver el problema, por lo que los destinatarios de `502` pueden volver a intentar realizar la solicitud después de un tiempo. |
| `503 Service Unavailable` | Este código de error indica que el servicio no está disponible temporalmente. Esto puede ocurrir durante los períodos de mantenimiento. Destinatarios de `503` los errores pueden volver a intentar la solicitud, pero deben respetar el `Retry-After` encabezado. |
| `504 Gateway Timeout` | Indica que se ha agotado el tiempo de espera de la solicitud de Adobe Experience Platform Edge Network a los servidores de flujo ascendente. Esto puede deberse a problemas de red entre servidores, problemas de DNS u otros problemas de red. Los problemas temporales de red pueden resolverse después de algún tiempo y un reintento puede resolver el problema. |
