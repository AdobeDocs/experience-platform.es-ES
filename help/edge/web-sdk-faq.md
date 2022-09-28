---
title: Preguntas frecuentes sobre el SDK web de Adobe Experience Platform
description: Obtenga respuestas a las preguntas más frecuentes sobre el SDK web de Adobe Experience Platform.
exl-id: 6ddb4b4d-c9b8-471a-bd2e-135dc4202876
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '1934'
ht-degree: 2%

---

# Preguntas frecuentes

Esta guía proporciona respuestas a preguntas que se plantean a menudo sobre el SDK web de Adobe Experience Platform.

## ¿Qué es el SDK web de Adobe Experience Platform?

Adobe Experience Platform Web SDK es una biblioteca JavaScript del lado del cliente que permite a los clientes de Adobe Experience Cloud interactuar con los distintos servicios del Experience Cloud.

Envía datos de forma independiente (XDM) a Adobe Experience Platform Edge Network, que después asigna los datos a formatos y destinos específicos de la solución y los envía en tiempo real.

**Más información**
[Presentación del Adobe Summit](https://www.adobe.com/summit/2020/with-alloy-js-never-tag-for-an-evar-or-mbox-again.html)

## ¿En qué se diferencian el SDK web de Adobe Experience Platform y las soluciones anteriores?

### Antes del SDK de Adobe Experience Platform

Actualmente, debe implementar diferentes bibliotecas JavaScript basadas en cada solución individual.

* Cada solución tiene su propia biblioteca, esquema y dominio de JavaScript.
* Ninguna de estas bibliotecas se creó para trabajar entre sí.
* Los casos de uso entre soluciones y Adobe Experience Platform requieren que estas bibliotecas dispares sean interdependientes, lo que provoca fricciones en la implementación.

Aunque las etiquetas de Platform facilitan lo más posible la implementación y la administración de estas bibliotecas, sigue habiendo problemas con:

* Tamaño de la biblioteca (demasiado código de Adobe en una página)
* Rendimiento (los sitios tardan demasiado en cargarse)
* Varias llamadas a un solo caso de uso
* Esperando el retorno de ECID antes de las llamadas de personalización (causa retraso)
* Recopilación de datos fracturada (¿qué es una evar?)
* Confusión de esquemas entre soluciones (A4T)
* Muchas otras cosas menos óptimas

Además, actualmente no hay ninguna biblioteca JavaScript que envíe datos directamente a Adobe Experience Platform.

### Con el SDK web de Adobe Experience Platform

El nuevo SDK web envía datos de las siguientes soluciones a un único destino (Adobe Experience Platform Edge Network) y se resuelve en los casos de uso de las soluciones más comunes mencionados.

* Adobe Analytics
* Adobe Audience Manager
* Adobe Target
* ID de visitante
* Adobe Experience Platform

A finales de este año vendrán otras soluciones.

El SDK web de Adobe Experience Platform también puede enviar datos directamente a Adobe Experience Platform. Estos datos se encuentran en XDM y se asignan al esquema de soluciones del lado del servidor.

## ¿Cuál es el valor de este nuevo SDK web?

**Rendimiento:** El SDK web es más pequeño que el uso de todas las bibliotecas de Adobe actuales y proporciona cargas de página mucho más rápidas.

**Simplicidad:** La combinación de XDM, SDK web, etiquetas, Experience Edge, soluciones de Adobe Experience Cloud y Adobe Experience Platform crea una historia de recopilación de datos fácil de entender y de seguir.

* **XDM:** El esquema independiente de la solución que utiliza para enviar datos a Adobe. Ya no se etiquetan eVars ni mboxes.
* **SDK web de Adobe Experience Platform:** Facilita el envío y la recepción de datos en Adobe Experience Platform Edge Network.
* **Etiquetas:** Simplifica la implementación y configuración del SDK web (y de cualquier otra etiqueta de JavaScript) en un sitio.
* **Experience Edge:** Enrute fácilmente los datos a Adobe Experience Platform y a las soluciones en el formato que necesiten.
* **Soluciones de Adobe Experience Platform y Adobe:** Habilite su propuesta de valor.

**Control:** Como todos los datos utilizan un único flujo de datos conectado, lógicamente puede seguir y controlar el aspecto de los datos en cada milisegundo de su recorrido, desde y hacia las aplicaciones.

**Moderno y listo para el futuro:** El SDK web y su conexión con la red Experience Edge han permitido a Adobe modernizar de forma significativa el modo en que el Adobe trata la recopilación de datos, la personalización, el consentimiento y el futuro de las cookies de terceros. (Habilita un dominio de origen, administrado por Adobe).

**Tiempo para el valor:** Adobe ha trabajado duro (y seguirá) para facilitar lo más posible la implementación del SDK web mediante etiquetas y la asignación de datos del lado del cliente a XDM. Una vez finalizado ese trabajo, todas las demás soluciones de Adobe y servicios de Adobe Experience Platform se pueden activar o desactivar en el servidor. Por ejemplo, si está usando esto para Adobe Analytics y desea activar Target o el Experience Platform, simplemente puede activar un botón de alternancia en la configuración del almacén de datos y encender esos casos de uso.

## ¿Qué es Alloy?

Alloy es el nombre del código para el SDK web de Adobe Experience Platform. Se utiliza dentro del código fuente y del nombre de archivo del SDK, aunque el SDK web de Adobe Experience Platform es el nombre oficial.

## ¿Los clientes necesitan comprar Adobe Experience Platform para usar la variable [!DNL Web SDK]?

No. Cualquier cliente de Adobe Digital Experience puede utilizar el SDK web de Adobe Experience Platform de forma gratuita. Los clientes que deseen utilizar la variable [!DNL Web SDK] tendrá que configurar los permisos adecuados para crear esquemas, conjuntos de datos, áreas de nombres de identidad y conjuntos de datos en la interfaz de usuario de la recopilación de datos o del Experience Platform.

Para obtener más información sobre la configuración de estos permisos, consulte nuestra documentación sobre [administración de permisos de recopilación de datos](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html?lang=en).

## ¿Quién debe utilizar el SDK web?

El SDK web de Adobe Experience Platform se ha desarrollado para las siguientes personas:

* Usuarios de Adobe Experience Platform
   * Si necesita enviar datos directamente desde un dispositivo a Adobe Experience Platform, esta es la forma oficialmente recomendada.
   * El Adobe es consciente de que el uso del conector Adobe Analytics es más rápido si el cliente ya tiene Adobe Analytics, pero no es la estrategia a largo plazo para la recopilación de datos.

* Clientes de soluciones de Adobe Experience Cloud
   * Los nuevos clientes de Adobe Analytics, Adobe Audience Manager y Adobe Target deben comenzar con el nuevo SDK web y no utilizar bibliotecas heredadas.
   * Los clientes existentes que deseen obtener la implementación más optimizada posible deben utilizar el nuevo SDK web.


## ¿Cómo puedo obtener acceso para empezar a utilizar el SDK web de Adobe Experience Platform?

El SDK web está disponible actualmente para el público en general y se puede utilizar para enviar datos a productos de Adobe Experience Cloud. La capacidad de enviar datos a soluciones de terceros está a punto de llegar. El SDK es gratuito, está alojado por Adobe de forma gratuita y se puede descargar para que pueda alojarlo en sus propios servidores, si lo desea, de forma gratuita. El SDK web de Platform requiere acceso a las configuraciones del almacén de datos y al generador de esquemas Adobe Experience Platform XDM, para que los servidores de Adobe puedan gestionar correctamente los datos entrantes procedentes del SDK. Si desea obtener acceso, póngase en contacto con el administrador de éxito del cliente (CSM) para iniciar el proceso de solicitud.

## ¿Qué casos de uso admite actualmente el SDK web?

El SDK web está evolucionando rápidamente. Se están trabajando más casos de uso. Puede encontrar la variable [lista de casos de uso admitidos actualmente aquí.](https://github.com/adobe/alloy/projects/5)

## ¿Los clientes actuales tienen que volver a etiquetar sus sitios?

Depende. El SDK web de Adobe Experience Platform se puede implementar en dos estilos diferentes. Un futuro documento de migración proporcionará detalles adicionales.

* **Otra etiqueta:** Si el sitio ya está etiquetado para soluciones y no puede volver a etiquetar, pero desea enviar datos a Adobe Experience Platform Edge Network para casos de uso de Experience Platform o para las próximas funciones de reenvío de eventos (consulte a continuación), puede agregar la variable `alloy.js` en el sitio, donde funciona como &quot;otra etiqueta&quot;.

* **La única etiqueta:** Si desea utilizar el SDK web para una solución de Experience Cloud, debe utilizarlo para _all_ de las soluciones de esa página. Por ejemplo, si el sitio ya está etiquetado para Adobe Analytics y desea utilizarlo para Target, debe utilizarlo para ambos, así como para cualquier otro en el futuro.

En otras palabras, si decide utilizar el SDK web de Adobe Experience Platform para casos de uso que no sean de solución, puede etiquetar el sitio con `alloy.js` y sigue como si fuera una nueva solución. Si desea usarlo para Adobe Analytics, Target o Audience Manager, o para casos de uso de aplicaciones, es posible que tenga que eliminar cualquiera del código heredado de su página.

## ¿Puedo migrar los ECID cuando empiezo a usar Alloy para que los visitantes de mi sitio web no empiecen a aparecer como nuevos visitantes?

Sí, el SDK web de Adobe Experience Platform proporciona una función de migración de identidad. Siga las instrucciones para la migración de ID en la [Documentación de identidad del SDK web de plataforma](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#id-migration) para obtener más información.

## ¿En qué se diferencia el SDK web de las etiquetas?

* **Etiquetas en el Experience Platform** administre el código del dispositivo. Utilícelos para implementar el código con mayor facilidad. Son libres y poderosos.

* **SDK web de Adobe Experience Platform** es el nombre oficial del nuevo código que se implementaría mediante etiquetas para casos de uso de Adobe. También es libre y poderoso.

* **`alloy.js`** es el nombre de archivo del código del SDK web de Adobe Experience Platform.

## ¿Tengo que utilizar etiquetas para implementar el SDK web?

No. Puede descargar el `alloy.js` presente usted mismo.

Sin embargo:

* El SDK web de Adobe Experience Platform requiere un ID de almacén de datos para que la red perimetral pueda identificar el flujo y determinar qué hacer con los datos. Este ID se crea dentro de Experience Platform. Esto no significa que tenga que usar la interfaz de usuario para crear propiedades o implementar el código JavaScript, pero sí que debe utilizar etiquetas para crear un ID de configuración.

* Las etiquetas no son solo la mejor etiqueta disponible y el administrador de SDK, sino que también facilita la implementación `alloy.js` y asignar datos a esquemas XDM. Si decide no utilizar etiquetas, deberá administrar la implementación `alloy.js`, eventos y asignación de los datos en XDM antes de enviarlos. Esto es un _many_ proceso más difícil que el uso de etiquetas.

* Se recomienda utilizar etiquetas para implementar `alloy.js`, aunque sea la única etiqueta para la que la utilice.

## ¿Qué es el reenvío de eventos?

Si utiliza nuestros SDK y envía XDM a Experience Edge, estas nuevas funciones de reenvío de eventos le permiten instalar nuevas extensiones del lado del servidor y asignar esos datos a cualquier cosa (y enviarlos a cualquier lugar) desde nuestra red perimetral. Considérela como &quot;recopilación de datos como servicio&quot;. Estará disponible por un coste, así como como como parte de Adobe Experience Platform.

## ¿Qué es un CNAME o un dominio de origen y por qué importa?

Más información sobre un CNAME está disponible en la sección [documentación de Adobe](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/cname.html?lang=es)

## ¿El SDK web de Adobe Experience Platform utiliza cookies? En caso afirmativo, ¿qué cookies utiliza?

Sí, actualmente el SDK web utiliza entre 1 y 4 cookies, dependiendo de la implementación. A continuación se muestra una lista de las 4 cookies que podría ver con el SDK web y la forma en que se utilizan:

**kndct_orgid_identity:** La cookie de identidad se utiliza para almacenar el ECID, así como alguna otra información relacionada con el ECID.

**kndctr_orgid_permission:** Esta cookie almacena la preferencia de consentimiento del usuario para el sitio web.

**kndctr_orgid_cluster:** Esta cookie almacena la región de Experience Edge que sirve las solicitudes del usuario actual. La región se utiliza en la ruta URL para que Experience Edge pueda enrutar la solicitud a la región correcta. Esta cookie dura 30 minutos, de modo que si un usuario se conecta con una dirección IP diferente, la solicitud se puede enrutar a la región más cercana.

Al utilizar el SDK web, la red perimetral establece una o más de las cookies anteriores. La red perimetral establece todas las cookies con la variable `secure` y `sameSite="none"` atributos.

Si actualmente tiene secciones seguras y no seguras en el sitio web, esto podría interferir con la identificación del usuario. Cuando un usuario navega de una sección segura del sitio a una sección no segura, la red perimetral genera un `ECID` con la solicitud.

## ¿Con qué exploradores es compatible el SDK web de Adobe Experience Platform?

El SDK web de Adobe Experience Platform está diseñado para funcionar de forma óptima en las últimas versiones de Google Chrome, Safari, Firefox, Internet Explorer 11 y Microsoft Edge Chromium. Es posible que tenga problemas al utilizar ciertas funciones en versiones anteriores de los navegadores.

## ¿Dónde puedo obtener más información sobre el SDK web de Adobe Experience Platform?

* [Documentación](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=es)
* [Código fuente](https://github.com/adobe/alloy)
