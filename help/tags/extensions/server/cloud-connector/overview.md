---
title: Información general sobre la extensión Cloud Connector
description: Obtenga información acerca de la extensión de reenvío de eventos de Cloud Connector en Adobe Experience Platform.
exl-id: f3713652-ac32-4171-8dda-127c8c235849
source-git-commit: c7344d0ac5b65c6abae6a040304f27dc7cd77cbb
workflow-type: tm+mt
source-wordcount: '1616'
ht-degree: 98%

---

# Información general sobre la extensión Cloud Connector

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

La extensión de Cloud Connector para reenvío de eventos permite crear solicitudes HTTP personalizadas para enviar datos a un destino o recuperar datos de un destino. La extensión de conector de nube es como tener Postman en Adobe Experience Platform Edge Network y se puede usar para enviar datos a un punto final que aún no tiene una extensión dedicada.

Utilice esta referencia para obtener información sobre las opciones disponibles al utilizar esta extensión para generar una regla.

## Tipo de acción de extensión de conector de nube

En esta sección se describe el tipo de acción Enviar datos disponible en la extensión de conector de nube de Adobe Experience Platform.

### Tipo de solicitud

Para seleccionar el tipo de solicitud que requiere el extremo, seleccione el tipo adecuado en la lista desplegable [!UICONTROL Tipo de solicitud].

| Método | Descripción |
|---|---|
| [GET](https://developer.mozilla.org/es-ES/docs/Web/HTTP/Methods/GET) | Solicita una representación del recurso especificado. Las solicitudes que utilicen GET solo deben recuperar datos. |
| [POST](https://developer.mozilla.org/es-ES/docs/Web/HTTP/Methods/POST) | Envía una entidad al recurso especificado, causando a menudo un cambio de estado o efectos secundarios en el servidor. |
| [PUT](https://developer.mozilla.org/es-ES/docs/Web/HTTP/Methods/PUT) | Reemplaza todas las representaciones actuales del recurso de target con la carga útil de la solicitud. |
| [PATCH](https://developer.mozilla.org/es-ES/docs/Web/HTTP/Methods/PATCH) | Aplica modificaciones parciales a un recurso. |
| [DELETE](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/DELETE) | Elimina el recurso especificado. |

### URL de extremo

En el campo de texto situado junto al menú desplegable Tipo de solicitud, introduzca la dirección URL del extremo al que va a enviar los datos.

### Parámetros de consulta, encabezados y configuración de cuerpo

Utilice cada una de estas fichas (Parámetros de Consulta, Encabezados y Elementos de datos de cuerpo) para controlar qué datos se envían a un extremo determinado.

#### Parámetros de consulta

Defina una clave y un valor para cada par clave-valor que desee enviar como parámetro de cadena de consulta. Para introducir manualmente un elemento de datos, utilice la tokenización del elemento de datos para el reenvío de eventos. Para hacer referencia al valor de un elemento de datos llamado &quot;siteSection&quot; como clave o valor, escriba `{{siteSection}}`. O bien, seleccione el elemento de datos creado anteriormente seleccionándolo en el menú desplegable.

Para agregar más parámetros de consulta, seleccione **[!UICONTROL Añadir otro]**.

#### Encabezados

Defina una clave y un valor para cada par clave-valor que desee enviar como encabezado. Para introducir manualmente un elemento de datos, utilice la tokenización del elemento de datos para el reenvío de eventos. Para hacer referencia al valor de un elemento de datos llamado &quot;pageName&quot; como clave o valor, escriba `{{pageName}}`. O bien, seleccione el elemento de datos creado anteriormente seleccionándolo en el menú desplegable.

Para agregar más encabezados, seleccione **[!UICONTROL Añadir otro]**.

En la siguiente tabla se hace una lista de los encabezados predefinidos. No está limitado a estos encabezados y puede agregar sus propios encabezados personalizados si es necesario, pero están disponibles para su comodidad.

>[!NOTE]
>
>Para obtener información más detallada sobre estos encabezados, visite [https://developer.mozilla.org/es-ES/docs/Web/HTTP/Headers](https://developer.mozilla.org/es-ES/docs/Web/HTTP/Headers).

| Encabezado | Descripción |
|---|---|
| [A-IM](https://developer.mozilla.org/es-ES/docs/Web/HTTP/Headers/Accept) |  |
| [Accept](https://developer.mozilla.org/es-ES/docs/Web/HTTP/Headers/Accept) |  |
| [Accept-Charset](https://developer.mozilla.org/es-ES/docs/Web/HTTP/Headers/Accept-Charset) |  |
| [Accept-Encoding](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept-Encoding) |  |
| [Accept-Language](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept-Language) |  |
| [Accept-Datetime](https://developer.mozilla.org/es-ES/docs/Web/HTTP/Headers/Accept) | Transmitido por un agente de usuario para indicar que desea acceder a un estado anterior de un recurso original. Con este fin, el encabezado `Accept-Datetime` se transmite en una petición HTTP emitida contra una TimeGate para un recurso original, y su valor indica la fecha y hora del estado anterior deseado del recurso original. |
| Access-Control-Request-Headers | Los exploradores los utilizan para emitir una [solicitud de verificación previa](https://developer.mozilla.org/es-ES/docs/Glossary/preflight_request), a fin de que el servidor sepa qué [encabezados HTTP](https://developer.mozilla.org/es-ES/docs/Web/HTTP/Headers) puede enviar el cliente cuando se realiza la solicitud real. |
| Access-Control-Request-Method | Los exploradores los utilizan al emitir una [solicitud de verificación previa](https://developer.mozilla.org/es-ES/docs/Glossary/preflight_request), para hacer saber al servidor qué [método HTTP](https://developer.mozilla.org/es-ES/docs/Web/HTTP/Methods) se utilizará cuando se realice la solicitud real. Este encabezado es necesario porque la solicitud de verificación previa siempre es [OPTION](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/OPTIONS) y no utiliza el mismo método que la solicitud real. |
| Autorización | Contiene las credenciales para autenticar un usuario-agente con un servidor. |
| [Cache-Control](https://developer.mozilla.org/es-ES/docs/Web/HTTP/Headers/Cache-Control) | Directivas para mecanismos de almacenamiento en caché tanto en solicitudes como en respuestas. |
| [Conexión](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Connection) | Controla si la conexión de red permanece abierta después de que finalice la transacción actual. |
| [Content-Length](https://developer.mozilla.org/es-ES/docs/Web/HTTP/Headers/Content-Length) | El tamaño del recurso, en número decimal de bytes. |
| [Content-Type](https://developer.mozilla.org/es-ES/docs/Web/HTTP/Headers/Content-Type) | Indica el tipo de medio del recurso. |
| Cookie | Contiene [cookies HTTP](https://developer.mozilla.org/es-ES/docs/Web/HTTP/Cookies) almacenadas previamente enviadas por el servidor con el encabezado [`Set-Cookie`](https://developer.mozilla.org/es-ES/docs/Web/HTTP/Headers/Set-Cookie). |
| Fecha | El encabezado HTTP general contiene la fecha y la hora en que se originó el mensaje. |
| [DNT](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/DNT) | Expresa la preferencia de seguimiento del usuario. |
| Esperar | Indica las expectativas que el servidor debe cumplir para gestionar correctamente la solicitud. |
| Reenviado | Contiene información de los [servidores proxy inversos](https://developer.mozilla.org/es-ES/docs/Web/HTTP/Proxy_servers_and_tunneling) que se alteran o pierden cuando un proxy está involucrado en la ruta de la solicitud. |
| De | Contiene una dirección de correo electrónico de Internet para un usuario humano que controla el agente de usuario solicitante. |
| Host | Especifica el host y el número de puerto del servidor al que se envía la solicitud. |
| Si-Coincidencia |  |
| Si-Modificado-Desde |  |
| [Si-Ninguno-Coincidencia](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/If-None-Match) |  |
| [Si-Intervalo](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/If-Range) |  |
| [Si-Nomodificado-Desde](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/If-Unmodified-Since) |  |
| [Máx-Avanza](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/If-Unmodified-Since) |  |
| [Origen](https://developer.mozilla.org/es-ES/docs/Web/HTTP/Headers/Origin) |  |
| [Pragma](https://developer.mozilla.org/es-ES/docs/Web/HTTP/Headers/Pragma) | Encabezado específico para la implementación que puede tener varios efectos en cualquier parte de la cadena de solicitud y respuesta. Se utiliza para la compatibilidad con versiones anteriores de las memorias caché HTTP/1.0 donde el encabezado Caché-Control aún no está presente. |  |
| [Autorización de proxy](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Proxy-Authorization) |
| [Intervalo](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Range) | Indica la parte de un documento que el servidor debe devolver. |  |
| [Remitente](https://developer.mozilla.org/es-ES/docs/Web/HTTP/Headers/Referer) | Dirección de la página web anterior desde la que se siguió un vínculo a la página solicitada actualmente. |  |
| TE | Especifica las codificaciones de transferencia que el agente de usuario está dispuesto a aceptar. (Podría llamarlo `Accept-Transfer-Encoding` de manera informal, lo cual sería más intuitivo). |
| Actualizar | El documento RFC relevante para el campo de encabezado [`Upgrade` es RFC 7230, sección 6.7](https://tools.ietf.org/html/rfc7230#section-6.7). El estándar establece reglas para actualizar o cambiar a un protocolo diferente en la conexión actual de cliente, servidor y protocolo de transporte. Por ejemplo, este estándar de encabezado permite a un cliente cambiar de HTTP 1.1 a HTTP 2.0, suponiendo que el servidor decida reconocer e implementar el campo de encabezado `Upgrade`. No se pide a ninguna de las partes que acepte los términos especificados en el campo de encabezado `Upgrade`. Se puede utilizar en encabezados de cliente y de servidor. Si se especifica el campo de encabezado `Upgrade`, el remitente DEBE enviar también el campo de encabezado `Connection` con la opción `upgrade` especificada. |  |
| [User-Agent](https://developer.mozilla.org/es-ES/docs/Web/HTTP/Headers/User-Agent) | Contiene una cadena característica que permite a los pares de protocolo de red identificar el tipo de aplicación, el sistema operativo, el proveedor de software o la versión de software del agente de usuario de software solicitante. |
| [Via](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Via) | Añadido por proxies, tanto los proxies hacia delante como los de atrás, y puede aparecer en los encabezados de solicitud y en los encabezados de respuesta. |
| [Advertencia](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Warning) | Información general de advertencia sobre posibles problemas. |
| X-CSRF-Token |  |
| X-Requested-With |  |

#### Cuerpo como JSON

Defina una clave y un valor para cada par clave-valor que desee enviar en el cuerpo de la solicitud. Para introducir manualmente un elemento de datos, utilice la tokenización del elemento de datos para el reenvío de eventos. Para hacer referencia al valor de un elemento de datos denominado &quot;appSection&quot; como clave o valor, introduzca `{{appSection}}`. O bien, seleccione el elemento de datos creado anteriormente seleccionándolo en el menú desplegable.

Para añadir pares clave-valor adicionales, seleccione **[!UICONTROL Añadir otro]**.

#### Cuerpo como sin procesar

Defina una clave y un valor para cada par clave-valor que desee enviar en el cuerpo de la solicitud. Para introducir manualmente un elemento de datos, utilice la tokenización del elemento de datos para el reenvío de eventos. Para hacer referencia al valor de un elemento de datos denominado &quot;appSection&quot; como clave o valor, introduzca `{{appSection}}`. O bien, seleccione el elemento de datos creado anteriormente seleccionándolo en el menú desplegable. Puede añadir uno o más elementos de datos.

### Avanzadas

Las acciones dentro de las reglas en el reenvío de eventos se ejecutan secuencialmente. Podría haber situaciones en las que desee recuperar datos de un origen externo que no esté presente en el evento entrante desde el cliente y, luego, tomar esta respuesta y transformar o enviar estos datos a un destino final en una acción posterior dentro de una sola regla. La sección avanzada Guardar la respuesta de solicitud lo habilita.

Para guardar el cuerpo de respuesta de un extremo, marque la casilla **[!UICONTROL Guardar la respuesta de solicitud]** y defina una clave de respuesta en el campo de texto.

Si definió la clave de respuesta como `productDetails`, haga referencia a estos datos en un elemento de datos y, a continuación, haga referencia a este elemento de datos en una acción posterior dentro de la misma regla. Para crear un elemento de datos que haga referencia a `productDetail`, cree un elemento de datos de tipo `path` e introduzca la siguiente ruta:

```Json
arc.ruleStash.[EXTENSION-NAME-HERE].responses.[RESPONSE-KEY-HERE] 

arc.ruleStash.adobe-cloud-connector.reponses.productDetails 
```
