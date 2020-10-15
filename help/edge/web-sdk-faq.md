---
title: Preguntas más frecuentes sobre el SDK web
seo-title: Preguntas más frecuentes sobre el SDK web de Adobe Experience Platform
description: Preguntas más frecuentes sobre el SDK web de Adobe Experience Platform
seo-description: Preguntas más frecuentes sobre el SDK web de Adobe Experience Platform
translation-type: tm+mt
source-git-commit: 5ef902ef7f7717121744f7f0074c0aa17e5a9e9a
workflow-type: tm+mt
source-wordcount: '1710'
ht-degree: 2%

---


# Preguntas frecuentes

Esta pregunta frecuente incluye preguntas que se plantean a menudo sobre el SDK web de Adobe.

## ¿Qué es Adobe Experience Platform Web SDK?

Adobe Experience Platform Web SDK es una biblioteca JavaScript del lado del cliente que permite a los clientes del Adobe Experience Cloud interactuar con los distintos servicios del Experience Cloud.

Envía datos de una manera no basada en soluciones (XDM) a Adobe Experience Platform Edge Network, que luego asigna los datos a formatos y destinos específicos de la solución y los envía en tiempo real.

**Más información** Presentación de la Cumbre de[Adobe](https://www.adobe.com/summit/2020/with-alloy-js-never-tag-for-an-evar-or-mbox-again.html)

## ¿En qué se diferencia Adobe Experience Platform Web SDK de las soluciones anteriores?

### Antes del SDK de Adobe Experience Platform

Actualmente, tiene que implementar diferentes bibliotecas de JavaScript en función de cada solución individual.

* Cada solución tiene su propia biblioteca, esquema y dominio de JavaScript.
* Ninguna de estas bibliotecas se construyó para trabajar entre sí.
* Los casos de uso entre soluciones y Adobe Experience Platform requieren que estas bibliotecas dispares sean interdependientes, lo que provoca fricciones en la implementación.

Aunque Adobe Experience Platform Launch facilita la implementación y la administración de estas bibliotecas, aún hay problemas con:

* Tamaño de la biblioteca (demasiado código de Adobe en una página)
* Rendimiento (los sitios tardan demasiado en cargarse)
* Varias llamadas para un solo caso de uso
* Esperando la devolución de ECID antes de las llamadas de personalización (causa retraso)
* Recopilación de datos fracturada (¿qué es una evar?)
* Confusión de esquemas entre soluciones (A4T)
* Muchas otras cosas menos óptimas

Además, actualmente no hay ninguna biblioteca JavaScript que envíe datos directamente a Adobe Experience Platform.

### Con Adobe Experience Platform Web SDK

El nuevo SDK web envía datos para las siguientes soluciones a un único destino (AEP Edge Network) y resuelve los casos de uso de la solución más comunes antes mencionados.

* Adobe Analytics
* Adobe Audience Manager
* Adobe Target
* ID de visitante
* Adobe Experience Platform

Otras soluciones seguirán este año.

El SDK web de Adobe Experience Platform también puede enviar datos directamente a Adobe Experience Platform. Estos datos están en XDM y están asignados al esquema de la solución del lado del servidor.

## ¿Cuál es el valor de este nuevo SDK web?

**Rendimiento:** El SDK web es más pequeño que el uso de todas las bibliotecas de Adobe actuales y proporciona cargas de página considerablemente más rápidas.

**Simplicidad:** La combinación de soluciones XDM, Web SDK, Experience Platform Launch, Experience Edge, Adobe Experience Cloud y Adobe Experience Platform crea un artículo de recopilación de datos fácil de entender y de seguir.

* **XDM:** El esquema que se utiliza para enviar datos a Adobe. No más etiquetas para evars o mboxes.
* **SDK web:** Facilita el envío y la recepción de datos a Adobe Experience Platform Edge Network.
* **Experience Platform Launch:** Simplifica la implementación y configuración del SDK web (y de cualquier otra etiqueta de JavaScript) en un sitio.
* **Experience Edge:** Envía fácilmente los datos a Adobe Experience Platform y las soluciones en el formato que necesitan.
* **Soluciones de Adobe Experience Platform y Adobe:** Habilite su propuesta de valor.

**Control:** Debido a que todos los datos están utilizando un flujo de datos único y conectado, lógicamente puede seguir y controlar el aspecto de los datos en cada milisegundo de su viaje, desde y hacia las aplicaciones.

**Moderno y listo para el futuro:** El SDK web y su conexión a la red Experience Edge han permitido al Adobe modernizar significativamente la forma en que Adobe se ocupa de la recopilación de datos, la personalización, el consentimiento y el futuro de las cookies de terceros. (Habilita un dominio de origen, administrado por Adobe).

**Tiempo de respuesta al valor:** Adobe ha trabajado duro (y continuará) para facilitar lo más posible la implementación del SDK web mediante Experience Platform Launch y asignar datos del lado del cliente a XDM.  Una vez finalizado ese trabajo, todas las demás soluciones de Adobe y servicios de Adobe Experience Platform se pueden activar o desactivar en el servidor. Por ejemplo, si está utilizando esto para Adobe Analytics y desea activar Destinatario o Experience Platform, puede simplemente voltear un conmutador en la configuración de Experience Edge y aclarar esos casos de uso.

## ¿Qué es `alloy.js`?

`Alloy.js` es el nombre de archivo del SDK web de Adobe Experience Platform. Adobe Experience Platform Web SDK es el nombre oficial, pero muchos desarrolladores lo llaman &quot;aleación&quot;.

## ¿Necesitan los clientes comprar Adobe Experience Platform para utilizar el SDK web?

No. Cualquier cliente de Adobe Digital Experience puede utilizarlo. Totalmente libre. Cualquier cliente que desee utilizar el SDK web tendrá acceso para crear esquemas y conjuntos de datos en la interfaz de usuario de Adobe Experience Platform.

## ¿Quién debe utilizar el SDK web?

El SDK web de Adobe Experience Platform se ha desarrollado para las siguientes personas:

* Usuarios de Adobe Experience Platform

   Si necesita enviar datos directamente desde un dispositivo a Adobe Experience Platform, esta es la forma oficialmente recomendada.

   Adobe es consciente de que el uso del conector Adobe Analytics es más rápido si el cliente ya tiene Adobe Analytics, pero no es la estrategia a largo plazo para la recopilación de datos.

* Clientes de soluciones de Adobe Experience Cloud

   Los nuevos clientes de Adobe Analytics, Adobe Audience Manager y Adobe Target deben inicio con el nuevo SDK web y no utilizar bibliotecas heredadas.

   Los clientes existentes que deseen obtener la implementación más optimizada posible deben utilizar el nuevo SDK web.


## ¿Cómo puedo obtener acceso a inicio mediante el SDK web de Adobe Experience Platform?

El SDK web está actualmente disponible para el público en general y puede utilizarse para enviar datos a productos de Adobe Experience Cloud. La capacidad de enviar datos a soluciones de terceros se aproxima en un futuro próximo. Si desea obtener acceso al SDK web, póngase en contacto con su administrador de software certificado (CSM) para obtener el inicio del proceso de solicitud.

## ¿Qué casos de uso admite actualmente el SDK web?

El SDK web está evolucionando rápidamente. Se están trabajando más casos de uso. Aquí puede encontrar la [lista de casos de uso actualmente admitidos.](https://github.com/adobe/alloy/projects/5)

## ¿Los clientes actuales tienen que volver a etiquetar sus sitios?

Depende. El SDK web de Adobe Experience Platform se puede implementar en dos estilos diferentes. Un futuro documento de migración proporcionará detalles adicionales.

* **Otra etiqueta:** Si el sitio ya está etiquetado para soluciones y no puede volver a etiquetarlo, pero desea enviar datos a Adobe Experience Platform Edge Network para casos de uso de Experience Platform o para las próximas funciones del lado del servidor de Experience Platform Launch (ver más abajo), puede agregar la `alloy.js` etiqueta al sitio, donde funciona como &quot;otra etiqueta&quot;.

* **La única etiqueta:** Si desea utilizar el SDK web para una solución Experience Cloud, debe utilizarlo para _todas_ las soluciones de esa página. Por ejemplo: si su sitio ya está etiquetado para Adobe Analytics y desea utilizarlo para el Destinatario, debe utilizarlo para ambos, así como para cualquier otro en el futuro.

En otras palabras, si decide utilizar el SDK web de Adobe Experience Platform para casos de uso que no son de solución, puede etiquetar el sitio con `alloy.js` y continuar como si fuera una nueva solución. Si desea utilizarla para Adobe Analytics, Destinatario o Audience Manager, o para casos de uso de la aplicación, es posible que tenga que eliminar cualquier código preexistente de la página.

## ¿Puedo migrar los ECID cuando inicio con Alloy para que los visitantes de mi sitio web no tengan inicios de aparecer como nuevos visitantes?

Sí, el SDK web de Adobe Experience Platform proporciona una función de migración de identidades. Siga las instrucciones de [este documento](https://docs.adobe.com/content/help/en/experience-platform/edge/fundamentals/identity.html#id-migration) para obtener más información.

## ¿En qué se diferencia el SDK web de Adobe Experience Platform Launch?

* **Experience Platform Launch** es el administrador de códigos del dispositivo. Utilícelo para implementar el código más fácilmente. Es libre y poderosa.

* **Adobe Experience Platform Web SDK** es el nombre oficial del nuevo código que implementaría el Experience Platform Launch en casos de uso de Adobe. También es libre y poderosa.

* **`alloy.js`** es el nombre de archivo del código del SDK web de Adobe Experience Platform.

## ¿Tengo que usar Adobe Experience Platform Launch para implementar el SDK web?

No. Puede descargar el `alloy.js` archivo usted mismo.

Sin embargo:

* El SDK web de Adobe Experience Platform requiere algo llamado ID de configuración de Experience Edge para que la red Edge pueda identificar el flujo y determinar qué hacer con los datos. Este ID se crea en Experience Platform Launch. Esto no significa que tenga que utilizar Experience Platform Launch para crear propiedades o implementar el código JavaScript, pero sí que debe utilizar Experience Platform Launch para crear un ID de configuración.

* Adobe Experience Platform Launch no solo es el mejor administrador de etiquetas y SDK disponible, sino que facilita la implementación `alloy.js` y asignación de datos a esquemas XDM. Si decide no utilizar Experience Platform Launch, deberá administrar la implementación, la `alloy.js`realización de eventos y la asignación de los datos en XDM antes de enviarlos. Este es un proceso _mucho_ más difícil que usar Experience Platform Launch.

* Se recomienda utilizar Experience Platform Launch para la implementación `alloy.js`, incluso si es la única etiqueta para la que se utiliza.

## ¿Qué es XDM y tengo que usar en el SDK web?

XDM es el formato de datos que se utiliza para enviar datos al Adobe Experience Platform y al SDK web. La documentación [del SDK](https://docs.adobe.com/content/help/en/experience-platform/edge/get-started/quick-start-with-launch.html#prepare-a-schema) web le explica cómo configurar fácilmente un esquema que puede personalizar según sus necesidades específicas.

## ¿Qué es &quot;Adobe Experience Platform Launch Server Side&quot;?

Más adelante en 2020, Experience Platform Launch lanzará funciones de reenvío de servidor. Si utiliza nuestros SDK y envía XDM a Experience Edge, estas nuevas funciones le permitirán instalar nuevas extensiones del lado del servidor y asignar esos datos a cualquier cosa (y enviarlos a cualquier parte) desde nuestra red Edge. Considérela como &quot;recopilación de datos como un servicio&quot;.  Esto estará disponible por un costo, así como como como se incluirá como parte del Adobe Experience Platform.

**Más información** Presentación de la Cumbre de[Adobe](https://adobe.bluejeans.com/playback/s/9LhauPOnRSUTYg6RMHAw4oJekhYfOQgdBLlNekVJdWevYktpxqX2IYyl5fz2Wxh9)

## ¿Qué es un CNAME o un dominio de origen y por qué es importante?

Encontrará más información sobre un CNAME en la documentación de [Adobe](https://docs.adobe.com/content/help/es-ES/id-service/using/reference/analytics-reference/cname.html)

## ¿Dónde puedo obtener más información sobre el SDK web de Adobe Experience Platform?

* [Documentación](https://docs.adobe.com/content/help/es-ES/experience-platform/edge/home.html)
* [Código de origen](https://github.com/adobe/alloy)
