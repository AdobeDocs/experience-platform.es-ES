---
title: Control de errores
description: Obtenga información acerca de los posibles errores que puede encontrar al realizar solicitudes de API a la API del servidor de red perimetral de Adobe Experience Platform.
exl-id: f6b8435c-b163-4046-b5fb-50a13a897637
source-git-commit: f52603f7e65ac553e00a2b632857561cd07ae441
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 3%

---

# Control de errores

## Información general {#overview}

Los errores de API en la API del servidor de red perimetral de Adobe Experience Platform pueden tener varias causas, internas (red perimetral en sí) o externas (relacionadas con la entrada, la configuración o el flujo ascendente).

## Tipos de error {#error-types}

| Error | Tipo | Descripción | Código de estado |
| --- | --- | --- | --- |
| `RequestProcessingError` | Internas | Error de uso general emitido por Adobe Experience Platform Edge Network debido a circunstancias inesperadas. | `500` |
| `InputError` | Externo | Incluye errores causados por entradas mal formadas, así como errores de validación de entidades. | `4xx` |
| `ConfigurationError` | Externo | Errores de configuración del lado del servidor. | `422` |
| `UpstreamError` | Externo | Errores de comunicación con servicios ascendentes. | `207 Multi-Status` |

## Gravedad

Los errores de API del servidor también se pueden dividir por gravedad:

* **Errores graves** detendrá la canalización de despacho.
* **Errores no graves** podría indicar un procesamiento parcial, al tiempo que permite que continúe el procesamiento de la solicitud.
   * Cuando está presente, el código de estado general de la solicitud se cambia a `207 Multi-Status`.

| Error | Tipo | Observaciones |
| --- | --- | --- |
| `RequestProcessingError` | Grave | Puede ocurrir en cualquier momento durante el procesamiento de la solicitud. |
| `InputError` | Grave | Sucede al aceptar la solicitud, antes de enviarla en orden ascendente. |
| `ConfigurationError` | Grave | Sucede al aceptar la solicitud, antes de enviarla en orden ascendente. |
| `UpstreamError` | No Mortal | Errores de comunicación con servicios ascendentes. |

### Errores graves {#fatal-errors}

Los errores graves detienen el procesamiento de la solicitud y hacen que se devuelva un estado de respuesta distinto de 2xx. Consulte la [tipos de error](#error-types) para ver el código de estado esperado, correspondiente a cada tipo de error.

Los errores irán acompañados de un cuerpo de respuesta que contenga un objeto de error. En este caso, el cuerpo de la respuesta contiene un detalle del problema, tal como se define en [RFC 7807: Detalles del problema para API HTTP](https://tools.ietf.org/html/rfc7807).

El tipo de contenido devuelto es el `application/problem+json` tipo de medio. Cuando está presente, esta respuesta contiene detalles legibles por el equipo pertenecientes al error. Los detalles del problema incluyen un tipo de URI.

Todos los objetos de error tienen un `type`, `status`, `title`, `detail` y `report` propiedades de mensajes para que el cliente de API pueda saber cuál es el problema.

| Propiedad | Tipo | Descripción |
| -------- | ------ | ----------- |
| `type` | Cadena | Referencia de URI (RFC3986) que identifica el tipo de problema según el formato `https://ns.adobe.com/aep/errors/<ERROR-CODE>`. |
| `status` | Número | El código de estado HTTP generado por el servidor para esta ocurrencia del problema. |
| `title` | Cadena | Un breve resumen legible en lenguaje natural del tipo de problema. |
| `detail` | Cadena | Una descripción breve y legible en lenguaje natural del tipo de problema. |
| `report` | Objeto | Mapa de propiedades adicionales que ayudan en la depuración, como el ID de solicitud o el ID de organización. En algunos casos, puede contener datos específicos del error en cuestión, como una lista de errores de validación. |

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

### Errores no graves {#non-fatal-errors}

Los errores no mortales pueden desglosarse en:

* Errores: problemas que se produjeron durante el procesamiento de la solicitud, pero que no provocaron que se rechazara toda la solicitud (p. ej.,. un error ascendente no crítico).
* Advertencias: Mensajes de servicios ascendentes que podrían indicar que se ha producido un procesamiento parcial de la solicitud.

Cuando se encuentran errores no graves (excluidas las advertencias), la variable [!DNL Server API] cambiará el estado de respuesta a `207 Multi-Status`.

Las advertencias, por otro lado, son en su mayoría informativas, ya que generalmente representan una condición potencialmente transitoria, que no afectó la solicitud en su totalidad. Un ejemplo aquí es una lectura parcial del perfil en el motor de segmentación, en cuyo caso la precisión se ve afectada hasta cierto punto, pero la funcionalidad aún se ofrece.

Los errores no fatales se representan en la variable _Detalles del problema_ , pero están incrustados directamente en la respuesta estándar de la puerta de enlace de Edge, que es del tipo `application/json`.

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
| `4xx Bad Request` | Más `4xx` los errores, como 400, 403, 404, no se deben volver a intentar en nombre del cliente, excepto para `429`. Estos son errores de cliente y no se realizarán correctamente. El cliente debe corregir el error antes de volver a intentar la solicitud. |
| `429 Too Many Requests` | `429` El código de respuesta HTTP indica que Adobe Experience Platform Edge Network o un servicio ascendente limita la velocidad de las solicitudes. En este caso, en tal caso, el llamador debe respetar el `Retry-After` encabezado de respuesta. Las respuestas que regresen deben llevar el código de respuesta HTTP con un código de error específico del dominio. |
| `500 Internal Server Error` | `500` los errores son errores genéricos y captaces. `500` los errores no se deben volver a intentar, excepto para `502` y `503`. Los intermediarios deben responder con una `500` error y puede responder con un código/mensaje de error genérico o con un código/mensaje de error más específico del dominio. |
| `502 Bad Gateway` | Indica que Adobe Experience Platform Edge Network recibió una respuesta no válida de los servidores de flujo ascendente. Esto puede deberse a problemas de red entre servidores. El problema de red temporal puede resolverse y, por lo tanto, un reintento puede resolverlo, por lo que los destinatarios de `502` los errores pueden reintentar la solicitud después de un tiempo. |
| `503 Service Unavailable` | Este código de error indica que el servicio no está disponible temporalmente. Esto puede ocurrir durante los períodos de mantenimiento. Destinatarios de `503` Los errores de pueden reintentar la solicitud, pero deben respetar la `Retry-After` encabezado. |
| `504 Gateway Timeout` | Indica que se ha agotado el tiempo de espera de la solicitud de Adobe Experience Platform Edge Network a los servidores de flujo ascendente. Esto puede deberse a problemas de red entre servidores, problemas de DNS u otros problemas de red. Los problemas temporales de red pueden resolverse después de un tiempo y un reintento puede resolver el problema. |
