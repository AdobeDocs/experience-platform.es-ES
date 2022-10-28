---
title: Administración del estado del cliente
description: Descubra cómo Adobe Experience Platform Edge Network administra el estado del cliente
seo-description: Learn how the Adobe Experience Platform Edge Network  manages client state
keywords: cliente;estado;administración;edge;red;puerta de enlace;api
exl-id: 798ecc52-1af1-4480-a2a3-3198a83538f8
source-git-commit: 85b428b3997d53cbf48e4f112e5c09c0f40f7ee1
workflow-type: tm+mt
source-wordcount: '850'
ht-degree: 2%

---

# Administración del estado del cliente

La red perimetral en sí no tiene estado (no mantiene su propia sesión). Sin embargo, hay algunos casos de uso que requieren persistencia del estado del lado del cliente, como:

* Identificación coherente de dispositivos (consulte [identificación de visitantes](visitor-identification.md))
* Recopilar y hacer cumplir el consentimiento del usuario
* Mantener ID de sesión de personalización

La red perimetral utiliza un protocolo de administración de estado, delegando el aspecto de almacenamiento a su cliente/SDK, e incluye entradas de estado en sus respuestas. En el caso de los exploradores, las entradas se almacenan como cookies.

La responsabilidad del cliente es almacenarlas e incluirlas en todas las solicitudes posteriores. El cliente también debe encargarse de la caducidad adecuada de las entradas, tal como indica la puerta de enlace. Cuando las entradas se almacenaban como cookies, el explorador realiza todo esto automáticamente.

Aunque las entradas de estado siempre tienen un estado sin formato `String` (visible para el llamador/SDK), no debe consumir ni manipular los valores de ninguna manera. La estructura/formato del valor o incluso el propio nombre pueden cambiar en cualquier momento, lo que podría provocar un comportamiento inesperado para los clientes que utilizan el estado internamente. El estado está pensado para que siempre lo consuma la propia puerta de enlace u otros servicios Edge.

## Estado persistente del cliente como metadatos

El estado devuelto por la variable [!DNL Edge Network] en el cuerpo de respuesta es un `Handle` objeto con el tipo `state:store`.

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
| `maxAge` | Número entero | *Opcional* Tiempo (en segundos) hasta que caduca la entrada. Si faltan, las entradas solo deben almacenarse para la sesión actual. |
| `attrs` | `Map<String, String>` | *Opcional*. Una lista opcional de atributos de entrada. Para todas las conexiones seguras con un encabezado HTTP de referencia seguro, la variable `SameSite` se configura como `None`. |


Para admitir el etiquetado múltiple (es decir, varias instancias de SDK en la misma propiedad, que potencialmente hacen referencia a diferentes organizaciones), el prefijo de todas las entradas de estado se fija automáticamente en `kndctr_` y el ID de organización seguro para URL.

Cuando el SDK de cliente recibe un `state:store` gestione en la respuesta de , debe hacer lo siguiente:

* Almacene entradas del lado del cliente, respetando el tiempo de caducidad proporcionado por la puerta de enlace.
* Carguelos desde el almacén de cliente e incluya todas las entradas no caducadas en las solicitudes posteriores.

Este es un ejemplo de solicitud que pasa el estado almacenado del lado del cliente:

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

## Estado persistente del cliente en las cookies del explorador

Al trabajar con clientes del explorador, la red perimetral puede mantener automáticamente las entradas como cookies del explorador. Esto permite la compatibilidad con el almacenamiento de estado transparente, ya que los exploradores respetan el protocolo de administración de estado de forma predeterminada.

Casi todas las entradas se materializan como cookies de origen cuando están activadas y son compatibles (consulte la nota a continuación), pero la puerta de enlace también podría almacenar algunas cookies de terceros cuando `adobedc.demdex.net` se utiliza.

Como las entradas siempre están enlazadas a un ámbito específico (dispositivo/aplicación) por su definición, solo el subconjunto compatible con el contexto de solicitud actual será escrito por la red perimetral. Las entradas no escritas se devuelven dentro de un `state:store` control.

Como regla general, las entradas de ámbito de aplicación siempre se escriben como cookies de origen, mientras que las entradas de ámbito de dispositivo se escriben como cookies de terceros. La decisión es completamente transparente para el llamador, la puerta de enlace decide qué entradas se pueden escribir, dependiendo del contexto de la llamada.

El llamador debe habilitar explícitamente la compatibilidad para almacenar el estado del cliente como cookies, a través del `meta.state.cookiesEnabled` indicador:

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
| `cookiesEnabled` | Booleano | Cuando se configura, habilita la compatibilidad con cookies. El valor predeterminado es `false`. |
| `domain` | Cadena | Requerido cuando `cookiesEnabled: true`. Dominio de nivel superior en el que se deben escribir las cookies. La red perimetral utilizará este valor para decidir si el estado se puede mantener como cookies. |

Incluso si la compatibilidad con cookies está habilitada mediante la variable `cookiesEnabled` , la red perimetral de Adobe Experience Platform solo escribirá las entradas de estado si el dominio de nivel superior de la solicitud coincide con el `domain` especificado por el llamador. Cuando hay una discordancia, las entradas se devuelven en una `state:store` control.

Las cookies de origen no se pueden escribir (aunque la compatibilidad esté habilitada) en los siguientes casos:

* La solicitud llega a terceros `adobedc.demdex.net` dominio.
* La solicitud procede de un origen `CNAME` , distinto del especificado por el llamador en `meta.state.domain`.

## Seguridad de la cookie

Todas las cookies tienen la variable [Indicador seguro](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies#restrict_access_to_cookies) siempre que sea posible.

Todas las cookies seguras tienen la variable [Atributo SameSite](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie/SameSite) configure como `None`, lo que significa que las cookies se envían en todos los contextos, tanto de origen como de origen cruzado.

* Para las cookies de origen (`kndcrt_*`), el `Secure` el indicador solo se establece cuando el contexto de solicitud es seguro (HTTPS) y cuando el referente ([Encabezado HTTP del referente](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Referer)) también es HTTPS. Si el referente no es seguro (HTTP), la variable `Secure` se omite el indicador para permitir que el SDK web los lea. Una cookie segura no se puede leer desde un contexto no seguro.
* Para la cookie de terceros (demdex), la variable `Secure` siempre se establece, ya que todas las solicitudes son HTTPS, por lo que el contexto de la solicitud es seguro y esta cookie nunca se lee desde JavaScript.

La variable `Secure` el indicador no está presente en la variable [representación de metadatos de las cookies](#state-as-metadata). Solo el `SameSite` se incluye. En este caso, es responsabilidad del cliente configurar correctamente la variable `Secure` siempre que la variable `SameSite` está presente. Cookies con `SameSite=None` también debe especificar el `Secure` , ya que requieren un contexto seguro (HTTPS).
