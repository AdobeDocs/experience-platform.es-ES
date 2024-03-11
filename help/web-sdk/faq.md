---
title: Preguntas frecuentes sobre Adobe Experience Platform Web SDK
description: Obtenga respuestas a las preguntas frecuentes sobre el SDK web de Adobe Experience Platform.
exl-id: 6ddb4b4d-c9b8-471a-bd2e-135dc4202876
source-git-commit: 58cd6300307881c3de7c52e07c401bf2ed908517
workflow-type: tm+mt
source-wordcount: '2268'
ht-degree: 2%

---


# Preguntas frecuentes

Esta guía proporciona respuestas a preguntas que se plantean a menudo sobre el SDK web de Adobe Experience Platform.

## ¿Qué es el SDK web de Adobe Experience Platform?

El SDK web de Adobe Experience Platform es una biblioteca JavaScript del lado del cliente que le permite interactuar con los distintos servicios de Adobe Experience Cloud.

El SDK web envía datos de forma independiente de la solución (XDM) a Experience Platform Edge Network, que a su vez asigna los datos a formatos y destinos específicos de la solución y los envía en tiempo real.

Consulte el siguiente vídeo para obtener más información sobre el SDK web: [Conozca Alloy.js y no vuelva a etiquetar para un eVar o Mbox](https://www.adobe.com/summit/2020/with-alloy-js-never-tag-for-an-evar-or-mbox-again.html).

## ¿En qué se diferencian el SDK web de Adobe Experience Platform de las soluciones anteriores?

### Antes del SDK web de Experience Platform

Actualmente, debe implementar diferentes bibliotecas de JavaScript en función de cada solución individual.

* Cada solución tiene su propia biblioteca JavaScript, esquema y dominio.
* Ninguna de estas bibliotecas se creó para funcionar entre sí.
* Los casos de uso entre soluciones y Adobe Experience Platform requieren que estas bibliotecas dispares sean interdependientes, lo que provoca fricciones en la implementación.

Aunque las etiquetas en Platform facilitan al máximo la implementación y administración de estas bibliotecas, aún hay problemas con:

* Tamaño de la biblioteca (demasiado código de Adobe en una página)
* Rendimiento (los sitios tardan demasiado en cargarse)
* Varias llamadas para un solo caso de uso
* Esperar el retorno de ECID antes de las llamadas de personalización (causa un retraso)
* Recopilación de datos fraccionada (¿qué es una evar?)
* Confusión de esquemas entre soluciones (A4T)
* Muchas otras cosas menos óptimas

Además, actualmente no hay ninguna biblioteca JavaScript que envíe datos directamente a Adobe Experience Platform.

### Con SDK web de Experience Platform

El nuevo SDK web envía datos para las siguientes soluciones a un único destino (red perimetral de Experience Platform) y resuelve los casos de uso de soluciones mencionados con más frecuencia.

* Adobe Analytics
* Adobe Audience Manager
* Adobe Target
* ID de visitante
* Adobe Experience Platform

A continuación se presentarán otras soluciones.

El SDK web de Adobe Experience Platform también puede enviar datos directamente a Adobe Experience Platform. Estos datos están en formato XDM y se asignan al esquema de soluciones del lado del servidor.

## ¿Cuál es el valor de este nuevo SDK web?

**Rendimiento:** El SDK web es más pequeño que todas las bibliotecas de Adobes actuales y proporciona cargas de página considerablemente más rápidas.

**Simplicidad:** La combinación de XDM, SDK web, etiquetas, red perimetral, soluciones de Adobe Experience Cloud y Adobe Experience Platform crea una historia de recopilación de datos fácil de entender y seguir.

* **XDM:** Esquema independiente de la solución que se utiliza para enviar datos al Adobe. Se acabaron las etiquetas para evars y mboxes.
* **SDK web:** Facilita el envío y la recepción de datos a Adobe Experience Platform Edge Network.
* **Etiquetas:** Simplifica la implementación y la configuración del SDK web (y otras etiquetas JavaScript) en un sitio.
* **Red perimetral:** Enrute fácilmente los datos a Adobe Experience Platform y a las soluciones en el formato que necesitan.
* **Soluciones de Adobe Experience Platform y Adobe:** Habilite su propuesta de valor.

**Control:** Como todos los datos utilizan un único flujo de datos conectado, puede seguir y controlar lógicamente el aspecto de los datos en cada milisegundo de su recorrido, desde y hacia aplicaciones.

**Moderno y listo para el futuro:** El SDK web y su conexión a la red perimetral han permitido a Adobe modernizar de forma significativa la forma en que Adobe gestiona la recopilación de datos, la personalización, el consentimiento y el futuro de las cookies de terceros. (Habilita un dominio de origen, administrado por Adobe).

**Tiempo de respuesta:** Adobe ha trabajado duro (y seguirá haciéndolo) para que sea lo más fácil posible implementar el SDK web mediante  y asignar datos del lado del cliente a XDM. Una vez finalizado ese trabajo, todas las demás soluciones de Adobe y servicios de Adobe Experience Platform se pueden activar o desactivar en el lado del servidor. Por ejemplo, si utiliza esto para Adobe Analytics y desea activar Target o Experience Platform, simplemente puede activar una opción en la configuración del flujo de datos y activar esos casos de uso.

## ¿Qué es [!DNL alloy.js]?

[!DNL alloy.js] es el nombre de la biblioteca JavaScript del SDK web. Se hace referencia a él dentro del código fuente y del nombre de archivo del SDK.

## ¿Necesitan los clientes comprar Adobe Experience Platform para utilizar? [!DNL Web SDK]?

No. Cualquier cliente de Adobe Digital Experience puede utilizar el SDK web de Adobe Experience Platform de forma gratuita. Clientes que desean utilizar el [!DNL Web SDK] Deberá configurar los permisos adecuados para crear esquemas, conjuntos de datos, áreas de nombres de identidad y flujos de datos en la IU de recopilación de datos o la IU del Experience Platform.

Para obtener más información sobre la configuración de estos permisos, consulte nuestra documentación sobre [administración de permisos de recopilación de datos](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html).

## ¿Quién debe utilizar el SDK web?

El SDK web de Adobe Experience Platform se ha desarrollado para los siguientes clientes:

* Usuarios de Adobe Experience Platform
   * Si necesita enviar datos directamente desde un dispositivo a Adobe Experience Platform, esta es la forma recomendada oficialmente.
   * Adobe es consciente de que el uso del conector de Adobe Analytics es más rápido si ya tiene Adobe Analytics, pero no es la estrategia a largo plazo para la recopilación de datos.

* clientes de la solución Adobe Experience Cloud
   * Los nuevos clientes de Adobe Analytics, Adobe Audience Manager y Adobe Target deben empezar con el nuevo SDK web y no utilizar bibliotecas heredadas.
   * Los clientes existentes que deseen obtener la implementación más optimizada posible deben utilizar el nuevo SDK web.

## ¿Cómo obtengo acceso al SDK web?

El SDK web está disponible actualmente para el público en general y se puede utilizar para enviar datos a productos de Adobe Experience Cloud. La capacidad de enviar datos a soluciones de terceros está disponible en un futuro próximo.

El SDK no supone ningún coste y se aloja en el Adobe de forma gratuita. Si es necesario, puede descargarlo y alojarlo en sus propios servidores sin coste alguno.

El SDK web requiere acceso a [configuraciones de secuencia de datos](../datastreams/overview.md) y el Experience Platform [Generador de esquemas XDM](../xdm/tutorials/create-schema-ui.md), para que los servidores de Adobe gestionen correctamente los datos de entrada procedentes del SDK. Si desea obtener acceso, póngase en contacto con el equipo de su cuenta de Adobe para iniciar el proceso de solicitud.

## ¿Qué casos de uso admite actualmente el SDK web?

El SDK web evoluciona rápidamente. Se están trabajando en más casos de uso. Puede encontrar el [lista de casos de uso admitidos actualmente aquí.](https://github.com/orgs/adobe/projects/18/views/1?filterQuery=)

## ¿Los clientes actuales tienen que volver a etiquetar sus sitios?

Depende. El SDK web de Adobe Experience Platform se puede implementar en dos estilos diferentes. Un documento de migración futuro proporcionará detalles adicionales.

* **Solo otra etiqueta:** Si el sitio ya está etiquetado para soluciones de y no puede volver a etiquetar, pero desea enviar datos a Adobe Experience Platform Edge Network para casos de uso de Experience Platform o las próximas funciones de reenvío de eventos (ver a continuación), puede agregar el `alloy.js` al sitio, donde funciona como &quot;solo otra etiqueta&quot;.

* **La única etiqueta:** Si desea utilizar el SDK web para una solución de Experience Cloud, debe utilizarlo para _todo_ de las soluciones de esa página. Por ejemplo: Si su sitio ya está etiquetado para Adobe Analytics y desea utilizarlo para Target, debe utilizarlo tanto para como para cualquier otro en el futuro.

En otras palabras, si decide utilizar el SDK web de Adobe Experience Platform para casos de uso que no sean de solución, puede etiquetar el sitio con `alloy.js` y seguir adelante como si fuera una nueva solución. Si desea utilizarlo para Adobe Analytics, Target o Audience Manager, o para casos de uso de aplicaciones, es posible que tenga que eliminar cualquiera del código heredado en su página.

## ¿Puedo migrar los ECID cuando empiece a utilizar el SDK web para que los visitantes del sitio web no empiecen a mostrarse como nuevos visitantes?

Sí, el SDK web de Adobe Experience Platform proporciona una función de migración de identidad. Siga las instrucciones de migración de ID en la [Documentación de identidad del SDK web de Platform](/help/web-sdk/identity/overview.md#id-migration) para obtener más información.

## ¿En qué se diferencia el SDK web de las etiquetas?

* **Etiquetas en el Experience Platform** administrar el código del dispositivo. Utilícelos para implementar el código con mayor facilidad. Son libres y poderosos.

* **SDK web de Adobe Experience Platform** es el nombre oficial del nuevo código que implementarían las etiquetas para los casos de uso de Adobe. También es libre y poderoso.

* **`alloy.js`** es el nombre de archivo del código SDK web de Adobe Experience Platform.

## ¿Tengo que utilizar etiquetas para implementar el SDK web?

No. Puede descargar el `alloy.js` preséntese usted mismo.

Sin embargo:

* El SDK web de Adobe Experience Platform requiere un elemento denominado ID de flujo de datos para que la red perimetral pueda identificar el flujo y determinar qué hacer con los datos. Este ID se crea en el Experience Platform. Esto no significa que tenga que utilizar la interfaz de usuario para crear propiedades o implementar el código JavaScript, pero sí necesita utilizar etiquetas para crear un ID de configuración.

* Las etiquetas no solo son el mejor administrador de etiquetas y SDK disponible, sino que su implementación es muy sencilla `alloy.js` y asigne datos a esquemas XDM. Si decide no utilizar etiquetas, deberá administrar la implementación `alloy.js`, eventos y asignación de datos en XDM antes de enviarlos. Este es un _mucho_ un proceso más difícil que el uso de etiquetas.

* Se recomienda utilizar etiquetas para implementar `alloy.js`, incluso si es la única etiqueta para la que la utiliza.

## ¿Qué es el reenvío de eventos?

Si utiliza nuestros SDK y envía XDM a la red perimetral, estas nuevas funciones y el reenvío de eventos le permiten instalar nuevas extensiones del lado del servidor y asignar esos datos a cualquier cosa (y enviarlos a cualquier lugar) desde nuestra red perimetral. Considérelo como &quot;recopilación de datos como un servicio&quot;. Esto estará disponible por un coste adicional y se incluirá como parte de Adobe Experience Platform.

## ¿Qué es un CNAME o dominio de origen y por qué importa?

Encontrará más información sobre un CNAME en la [documentación del Adobe](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/cname.html?lang=es)

## ¿Utiliza cookies el SDK web de Adobe Experience Platform? En caso afirmativo, ¿qué cookies utiliza?

Sí, actualmente el SDK web utiliza entre una y siete cookies en función de su implementación. A continuación se muestra una lista de las cookies que puede ver con el SDK web y la forma en que se utilizan:

| **Nombre** | **maxAge** | **Página descriptiva** | **Descripción** |
|---|---|---|---|
| **kndct_orgid_identity** | 34128000 | 395 días | La cookie de identidad almacena el ECID, así como otra información relacionada con el ECID. |
| **kndctr_orgid_permission_check** | 7200 | 2 horas | Esta cookie almacena la preferencia de consentimiento del usuario para el sitio web. |
| **kndctr_orgid_permission** | 15552000 | 180 días | Esta cookie basada en sesión indica al servidor que busque las preferencias de consentimiento del lado del servidor. |
| **kndctr_orgid_cluster** | 1800 | 30 minutos | Esta cookie almacena la región de red perimetral que atiende las solicitudes del usuario actual. La región se utiliza en la ruta URL para que la red perimetral pueda enrutar la solicitud a la región correcta. Esta cookie tiene una duración de 30 minutos, de modo que si un usuario se conecta con una dirección IP diferente, la solicitud se puede enrutar a la región más cercana. |
| **mbox** | 63072000 | 2 años | Esta cookie aparece cuando la configuración de migración de Target se establece en verdadera. Esto permitirá que el destinatario [Cookie de mbox](https://developer.adobe.com/target/implement/client-side/atjs/atjs-cookies/) que establecerá el SDK web. |
| **mboxEdgeCluster** | 1800 | 30 minutos | Esta cookie aparece cuando la configuración de migración de Target se establece en verdadera. Esta cookie permite al SDK web comunicar el clúster perimetral correcto a at.js para que los perfiles de Target puedan permanecer sincronizados a medida que los usuarios navegan por un sitio. |
| **AMCV_###@AdobeOrg** | 34128000 | 395 días | Esta cookie solo aparece cuando la migración de ID en el SDK web de Adobe Experience Platform está habilitada. Esta cookie es útil cuando se realiza la transición al SDK web mientras algunas partes del sitio aún utilizan visitor.js. Consulte [`idMigrationEnabled`](/help/web-sdk/commands/configure/idmigrationenabled.md) para obtener más información. |

Al utilizar el SDK web, la red perimetral establece una o más de las cookies anteriores. La red perimetral establece todas las cookies con el `secure` y `sameSite="none"` atributos.

Si actualmente tiene secciones seguras y no seguras en su sitio web, esto podría interferir con la identificación del usuario. Cuando un usuario navega de una sección segura del sitio a una sección no segura, la red perimetral genera un nuevo `ECID` con la solicitud.

## ¿Con qué exploradores es compatible el SDK web de Adobe Experience Platform?

El SDK web de Adobe Experience Platform está diseñado para funcionar de forma óptima en las últimas versiones de Google Chrome, Safari, Firefox, Internet Explorer 11 y Microsoft Edge Chromium. Es posible que tenga problemas al utilizar determinadas funciones en versiones anteriores de los exploradores.

## ¿Dónde puedo obtener más información acerca del SDK web de Adobe Experience Platform?

* [Documentación](/help/web-sdk/home.md)
* [Código fuente](https://github.com/adobe/alloy)

### Compatibilidad con Internet Explorer {#support-internet-explore}

Este SDK utiliza promesas, que son un método de comunicación de la finalización de tareas asincrónicas. El [Promesa](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) La implementación utilizada por el SDK es compatible de forma nativa con todos los navegadores de destino, excepto [!DNL Internet Explorer]. Para usar el SDK en [!DNL Internet Explorer], debe tener `window.Promise` [polillenado](https://remysharp.com/2010/10/08/what-is-a-polyfill).

Para determinar si ya tiene `window.Promise` polillenado:

1. Abra el sitio web en [!DNL Internet Explorer].
1. Abra la consola de depuración del explorador.
1. Tipo `window.Promise` en la consola y, a continuación, pulse Entrar.

Si algo distinto de `undefined` aparece, probablemente ya haya rellenado correctamente `window.Promise`. Otra forma de determinar si `window.Promise` es polyfill es cargando su sitio web después de haber completado las instrucciones de instalación anteriores. Si el SDK genera un error al mencionar algo sobre una promesa, es probable que no haya rellenado correctamente `window.Promise`.

Si ha determinado que debe rellenar políticamente `window.Promise`, incluya la siguiente etiqueta de script encima del código base proporcionado anteriormente:

```html
<script src="https://cdn.jsdelivr.net/npm/promise-polyfill@8/dist/polyfill.min.js"></script>
```

Esta etiqueta carga una secuencia de comandos que garantiza que `window.Promise` es una implementación de Promise válida.

>[!NOTE]
>
>Si decide cargar una implementación de Promise diferente, asegúrese de que admita `Promise.prototype.finally`.

### Compatibilidad con Internet Explorer

El SDK de Adobe Experience Platform utiliza promesas, que son un método de comunicación de la finalización de tareas asincrónicas. El [Promesa](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) La implementación utilizada por el SDK es compatible de forma nativa con todos los navegadores de destino, excepto [!DNL Internet Explorer]. Para usar el SDK en [!DNL Internet Explorer], debe tener `window.Promise` [polillenado](https://remysharp.com/2010/10/08/what-is-a-polyfill).

Una biblioteca que podría usar para polyfill promise es promise-polyfill. Consulte la [documentación de promise-polyfill](https://www.npmjs.com/package/promise-polyfill) para obtener más información sobre cómo instalar con NPM.

>[!NOTE]
>
>Si decide cargar una implementación de Promise diferente, asegúrese de que admita `Promise.prototype.finally`.