---
title: Administración de estado del cliente
description: Descubra cómo administra el Edge Network de Adobe Experience Platform el estado del cliente
seo-description: Learn how the Adobe Experience Platform Edge Network  manages client state
keywords: cliente;estado;administración;edge;red;puerta de enlace;api
exl-id: 798ecc52-1af1-4480-a2a3-3198a83538f8
source-git-commit: 85b428b3997d53cbf48e4f112e5c09c0f40f7ee1
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 1%

---

# Administración de estado del cliente

El Edge Network en sí no tiene estado (no mantiene su propia sesión). Sin embargo, hay ciertos casos de uso que requieren persistencia de estado del lado del cliente, como:

* Identificación coherente del dispositivo (consulte [identificación del visitante](visitor-identification.md))
* Recopilación y aplicación del consentimiento del usuario
* Mantener ID de sesión de personalización

El Edge Network utiliza un protocolo de administración de estado, delegando el aspecto de almacenamiento a su cliente/SDK, e incluye entradas de estado en sus respuestas. En los exploradores, las entradas se almacenan como cookies.

La responsabilidad del cliente es almacenarlas e incluirlas en todas las solicitudes posteriores. El cliente también debe encargarse de la caducidad adecuada de las entradas, tal como indica la puerta de enlace. Cuando las entradas se almacenan como cookies, el explorador hace todo este trabajo automáticamente.

Aunque las entradas de estado siempre tienen un valor `String` sin formato (visible para el llamador/SDK), no debe consumir ni manipular los valores de ninguna manera. La estructura o el formato del valor, o incluso el propio nombre, pueden cambiar en cualquier momento, lo que podría provocar un comportamiento inesperado para los clientes que utilizan el estado internamente. El estado está diseñado para que siempre lo consuma la propia puerta de enlace u otros servicios perimetrales.

## Mantener el estado del cliente como metadatos

El estado devuelto por [!DNL Edge Network] en el cuerpo de respuesta es un objeto `Handle` con el tipo `state:store`.

```json
{
   "requestId":"421036b3-a7ff-480b-a9ab-30adba6eb4f0",
   "handle":[
      {
         "payload":[
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_consent_check",
               "value":"1",
               "maxAge":7200,
               "attrs":{
                  "SameSite":"None"
               }
            },
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_identity",
               "value":"CiY1NDc1ODIxNzIzODk5MDY5MzQzMTIzNjQ1NTczNzExNjE4OTA1MFINCLGOvszNLhABGAEgBKABsY6-zM0uqAGHz-z2y82cul3wAbGOvszNLg==",
               "maxAge":34128000,
               "attrs":{
                  "SameSite":"None"
               }
            },
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_consent",
               "value":"general=in",
               "maxAge":15552000,
               "attrs":{
                  "SameSite":"None"
               }
            }
         ],
         "type":"state:store"
      }
   ]
}
```

| Atributo | Tipo | Descripción |
| --- | --- | --- |
| `key` | Cadena | **Requerido**. El nombre de la entrada. |
| `value` | Cadena | *Opcional*. El valor de entrada. |
| `maxAge` | Entero | *Opcional* El tiempo (en segundos) hasta que caduque la entrada. Si faltan, las entradas solo deben almacenarse para la sesión actual. |
| `attrs` | `Map<String, String>` | *Opcional*. Una lista opcional de atributos de entrada. Para todas las conexiones seguras con un encabezado HTTP de referente seguro, el atributo `SameSite` se establece en `None`. |


Para admitir el etiquetado múltiple (es decir, varias instancias del SDK en la misma propiedad, que podrían hacer referencia a diferentes organizaciones), todas las entradas de estado llevan automáticamente el prefijo `kndctr_` y el ID de organización seguro para la URL.

Cuando el SDK de cliente recibe un identificador `state:store` en la respuesta, debe hacer lo siguiente:

* Almacenar entradas del lado del cliente, respetando la hora de caducidad proporcionada por la puerta de enlace.
* Cárguelos desde el almacén de clientes e incluya todas las entradas que no hayan caducado en las solicitudes posteriores.

Este es un ejemplo de una solicitud que pasa en el estado almacenado del lado del cliente:

```json
{
   "meta":{
      "state":{
         "entries":[
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_consent_check",
               "value":"1"
            },
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_personalization_sessionId",
               "value":"0a88f43e-044b-41a6-a4f3-6c2848bbc672"
            }
         ]
      }
   }
}
```

## Mantener el estado de cliente en las cookies del explorador

Al trabajar con clientes del explorador, el Edge Network puede mantener automáticamente las entradas como cookies del explorador. Esto permite la compatibilidad con el almacenamiento de estado transparente, ya que los exploradores respetan el protocolo de administración de estado de forma predeterminada.

Casi todas las entradas se materializan como cookies de origen cuando se habilitan y admiten (consulte la nota siguiente), pero la puerta de enlace también podría almacenar algunas cookies de terceros cuando se utiliza el dominio de terceros `adobedc.demdex.net`.

Dado que las entradas siempre están enlazadas a un ámbito específico (dispositivo/aplicación) por su definición, el Edge Network solo escribirá el subconjunto compatible con el contexto de solicitud actual. Las entradas no escritas son
devuelto dentro de un identificador `state:store`.

Como regla general, las entradas con ámbito de aplicación siempre se escriben como cookies de origen, mientras que las entradas con ámbito de dispositivo se escriben como cookies de terceros. La decisión es completamente transparente para quien llama, la puerta de enlace decide qué entradas se pueden escribir, según el contexto de la llamada.

El autor de la llamada debe habilitar explícitamente la compatibilidad para almacenar el estado del cliente como cookies, a través del indicador `meta.state.cookiesEnabled`:

```json
{
   "meta":{
      "state":{
         "cookiesEnabled":true,
         "domain":"foo.com"
      }
   }
}
```

| Atributo | Tipo | Descripción |
| --- | --- | --- |
| `cookiesEnabled` | Booleano | Cuando se establece, se habilita la compatibilidad con cookies. El valor predeterminado es `false`. |
| `domain` | Cadena | Requerido cuando `cookiesEnabled: true`. Dominio de nivel superior en el que se deben escribir las cookies. El Edge Network utilizará este valor para decidir si el estado se puede mantener como cookies. |

Incluso si la compatibilidad con cookies está habilitada a través del indicador `cookiesEnabled`, el Edge Network de Adobe Experience Platform solo escribirá las entradas de estado si el dominio de nivel superior de la solicitud coincide con el `domain` especificado por el llamador. Cuando hay una discrepancia, las entradas se devuelven en un identificador `state:store`.

Las cookies de origen no se pueden escribir (aunque la compatibilidad esté habilitada) en los siguientes casos:

* La solicitud se envía en el dominio de terceros `adobedc.demdex.net`.
* La solicitud proviene de un dominio `CNAME` de origen, distinto del especificado por el llamador en `meta.state.domain`.

## Seguridad de cookies

Todas las cookies tienen [Secure flag](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies#restrict_access_to_cookies) habilitado siempre que sea posible.

Todas las cookies seguras tienen el atributo [SameSite](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie/SameSite) establecido en `None`, lo que significa que las cookies se envían en todos los contextos, tanto de origen como de origen cruzado.

* Para las cookies de origen (`kndcrt_*`), el indicador `Secure` solo se establece cuando el contexto de la solicitud es seguro (HTTPS) y cuando el referente ([Encabezado HTTP del referente](https://developer.mozilla.org/es-ES/docs/Web/HTTP/Headers/Referer)) también es HTTPS. Si el referente no es seguro (HTTP), se omite el indicador `Secure` para permitir que el SDK web lo lea. No se puede leer una cookie segura desde un contexto no seguro.
* Para la cookie de terceros (demdex), el indicador `Secure` siempre está establecido, ya que todas las solicitudes son HTTPS, por lo que el contexto de la solicitud es seguro y esta cookie nunca se lee desde JavaScript.

El indicador `Secure` no está presente en la [representación de metadatos de las cookies](#state-as-metadata). Solo se incluye el atributo `SameSite`. En este caso, es responsabilidad del cliente establecer correctamente el indicador `Secure` siempre que el atributo `SameSite` esté presente. Las cookies con `SameSite=None` también deben especificar el atributo `Secure`, ya que requieren un contexto seguro (HTTPS).
