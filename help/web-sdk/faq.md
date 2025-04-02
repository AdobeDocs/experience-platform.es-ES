---
title: Preguntas frecuentes sobre Adobe Experience Platform Web SDK
description: Obtenga respuestas a las preguntas frecuentes sobre Adobe Experience Platform Web SDK.
exl-id: 6ddb4b4d-c9b8-471a-bd2e-135dc4202876
source-git-commit: c26abeed890e06dce4e77133502b7031443bb4fa
workflow-type: tm+mt
source-wordcount: '2080'
ht-degree: 2%

---

# Preguntas frecuentes

Esta guía proporciona respuestas a preguntas que se plantean a menudo sobre Adobe Experience Platform Web SDK.

## ¿Qué es Adobe Experience Platform Web SDK?

Adobe Experience Platform Web SDK es una biblioteca JavaScript del lado del cliente que le permite interactuar con los distintos servicios de Adobe Experience Cloud.

Web SDK envía datos de forma independiente de las soluciones (XDM) a Experience Platform Edge Network, que a su vez asigna los datos a formatos y destinos específicos de la solución y los envía en tiempo real.

Vea el siguiente vídeo para obtener más información sobre Web SDK: [Conozca Alloy.js y no vuelva a etiquetar para un eVar o Mbox](https://www.adobe.com/summit/2020/with-alloy-js-never-tag-for-an-evar-or-mbox-again.html).

## ¿En qué se diferencian Adobe Experience Platform Web SDK y las soluciones anteriores?

### Antes de Experience Platform Web SDK

Actualmente, debe implementar diferentes bibliotecas de JavaScript basadas en cada solución individual.

* Cada solución tiene su propia biblioteca, esquema y dominio de JavaScript.
* Ninguna de estas bibliotecas se creó para funcionar entre sí.
* Los casos de uso entre soluciones y Adobe Experience Platform requieren que estas bibliotecas dispares sean interdependientes, lo que provoca fricciones en la implementación.

Aunque las etiquetas en Platform facilitan al máximo la implementación y administración de estas bibliotecas, aún hay problemas con:

* Tamaño de la biblioteca (demasiado código Adobe en una página)
* Rendimiento (los sitios tardan demasiado en cargarse)
* Varias llamadas para un solo caso de uso
* Esperar el retorno de ECID antes de las llamadas de personalización (causa un retraso)
* Recopilación de datos fraccionada (¿qué es una evar?)
* Confusión de esquemas entre soluciones (A4T)
* Muchas otras cosas menos óptimas

Además, actualmente no hay ninguna biblioteca de JavaScript que envíe datos directamente a Adobe Experience Platform.

### Con Experience Platform Web SDK

La nueva SDK web envía datos para las siguientes soluciones a un único destino (Experience Platform Edge Network) y resuelve los casos de uso de soluciones mencionados con más frecuencia.

* Adobe Analytics
* Adobe Audience Manager
* Adobe Target
* ID de visitante
* Adobe Experience Platform

A continuación se presentarán otras soluciones.

Adobe Experience Platform Web SDK también puede enviar datos directamente a Adobe Experience Platform. Estos datos están en formato XDM y se asignan al esquema de soluciones del lado del servidor.

## ¿Cuál es el valor de este nuevo Web SDK?

**Rendimiento:** El SDK web es más pequeño que todas las bibliotecas de Adobe actuales y proporciona cargas de página considerablemente más rápidas.

**Simplicidad:** La combinación de XDM, Web SDK, etiquetas, Edge Network, soluciones de Adobe Experience Cloud y Adobe Experience Platform crea una historia de recopilación de datos fácil de entender y seguir.

* **XDM:** esquema independiente de soluciones que usa para enviar datos a Adobe. Se acabaron las etiquetas para evars y mboxes.
* **Web SDK:** facilita el envío y la recepción de datos a Adobe Experience Platform Edge Network.
* **Etiquetas:** simplifica la implementación y configuración de Web SDK (y de cualquier otra etiqueta JavaScript) en un sitio.
* **Edge Network:** enrute fácilmente los datos a Adobe Experience Platform y a las soluciones en el formato que necesitan.
* **Soluciones de Adobe Experience Platform y Adobe:** Active su propuesta de valor.

**Control:** Como todos los datos utilizan una única secuencia de datos conectada, puede seguir y controlar lógicamente el aspecto de los datos en cada milisegundo de su recorrido, desde y hacia aplicaciones.

**Moderno y listo para el futuro:** El Web SDK y su conexión con Edge Network han permitido a Adobe modernizar de manera significativa la forma en que Adobe trata la recopilación de datos, la personalización, el consentimiento y el futuro de las cookies de terceros. (Habilita un dominio de origen, administrado por Adobe).

**Tiempo de obtención del valor:** Adobe ha trabajado duro (y seguirá haciéndolo) para que sea lo más fácil posible implementar Web SDK mediante etiquetas y asignar datos del lado del cliente a XDM. Una vez finalizado ese trabajo, todas las demás soluciones de Adobe y servicios de Adobe Experience Platform se pueden activar o desactivar en el lado del servidor. Por ejemplo, si utiliza esto para Adobe Analytics y desea activar Target o Experience Platform, simplemente puede activar una opción en la configuración del flujo de datos y activar esos casos de uso.

## ¿Qué es [!DNL alloy.js]?

[!DNL alloy.js] es el nombre de la biblioteca Web SDK JavaScript. Se hace referencia a él dentro del código fuente y del nombre de archivo de SDK.

## ¿Necesitan los clientes comprar Adobe Experience Platform para usar [!DNL Web SDK]?

No. Cualquier cliente de Adobe Digital Experience puede utilizar Adobe Experience Platform Web SDK de forma gratuita.

* Los clientes que *no* tengan acceso a Experience Platform o Real-time CDP y deseen usar [!DNL Web SDK] deberán configurar los permisos adecuados para crear esquemas y flujos de datos en la IU de recopilación de datos o la IU de Experience Platform.
* Los clientes que tengan acceso a Experience Platform o Real-time CDP y deseen utilizar [!DNL Web SDK] deberán configurar los permisos adecuados para crear esquemas, conjuntos de datos, áreas de nombres de identidad y flujos de datos en la IU de recopilación de datos o la IU de Experience Platform.

Para obtener más información sobre la configuración de estos permisos, consulte nuestra documentación sobre [administración de permisos de recopilación de datos](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html).

## ¿Quién debe utilizar Web SDK?

Adobe Experience Platform Web SDK se ha desarrollado para los siguientes clientes:

* Usuarios de Adobe Experience Platform
   * Si necesita enviar datos directamente desde un dispositivo a Adobe Experience Platform, esta es la forma recomendada oficialmente.
   * Adobe es consciente de que el uso del conector de Adobe Analytics es más rápido si ya tiene Adobe Analytics, pero no es la estrategia a largo plazo para la recopilación de datos.

* clientes de la solución Adobe Experience Cloud
   * Los nuevos clientes de Adobe Analytics, Adobe Audience Manager y Adobe Target deben empezar con el nuevo Web SDK y no utilizar bibliotecas heredadas.
   * Los clientes existentes que deseen obtener la implementación más optimizada posible deben utilizar el nuevo Web SDK.

## ¿Cómo obtengo acceso a Web SDK?

Web SDK está disponible actualmente para el público en general y se puede utilizar para enviar datos a productos de Adobe Experience Cloud. La capacidad de enviar datos a soluciones de terceros está disponible en un futuro próximo.

El SDK es gratuito y está alojado en Adobe de forma gratuita. Si es necesario, puede descargarlo y alojarlo en sus propios servidores sin coste alguno.

Web SDK requiere acceso a [configuraciones de secuencia de datos](../datastreams/overview.md) y al generador de esquemas XDM](../xdm/tutorials/create-schema-ui.md) de Experience Platform para que los servidores de Adobe puedan gestionar correctamente los datos entrantes procedentes de SDK. [ Si desea obtener acceso, póngase en contacto con el equipo de su cuenta de Adobe para iniciar el proceso de solicitud.

## ¿Qué casos de uso admite actualmente Web SDK?

Web SDK está evolucionando rápidamente. Se están trabajando en más casos de uso. Aquí puede encontrar la [lista de casos de uso actualmente admitidos.](https://github.com/orgs/adobe/projects/18/views/1?filterQuery=)

## ¿Los clientes actuales tienen que volver a etiquetar sus sitios?

Depende de ti. Adobe Experience Platform Web SDK se puede implementar en dos estilos diferentes. Un documento de migración futuro proporcionará detalles adicionales.

* **Solo otra etiqueta:** Si el sitio ya está etiquetado para soluciones y no puede volver a etiquetar, pero desea enviar datos a Adobe Experience Platform Edge Network para casos de uso de Experience Platform o las próximas funciones de reenvío de eventos (ver a continuación), puede agregar la etiqueta `alloy.js` al sitio, donde funciona como &quot;solo otra etiqueta&quot;.

* **Única etiqueta:** Si desea usar Web SDK para una solución de Experience Cloud, debe usarla para _todas_ las soluciones de esa página. Por ejemplo: Si su sitio ya está etiquetado para Adobe Analytics y desea utilizarlo para Target, debe utilizarlo tanto para como para cualquier otro en el futuro.

En otras palabras, si decide utilizar Adobe Experience Platform Web SDK para casos de uso que no sean de solución, puede etiquetar el sitio con `alloy.js` y continuar como si fuera una nueva solución. Si desea utilizarlo para Adobe Analytics, Target o Audience Manager, o para casos de uso de aplicaciones, es posible que tenga que eliminar cualquiera del código heredado en su página.

## ¿Puedo migrar los ECID cuando empiece a utilizar Web SDK para que los visitantes de mi sitio web no empiecen a mostrarse como nuevos visitantes?

Sí, Adobe Experience Platform Web SDK proporciona una función de migración de identidad. Siga las instrucciones para la migración de ID en [Documentación de identidad de Platform Web SDK](/help/web-sdk/identity/overview.md#id-migration) para obtener más información.

## ¿En qué se diferencia Web SDK de las etiquetas?

* **Las etiquetas de Experience Platform** administran el código del dispositivo. Utilícelos para implementar el código con mayor facilidad. Son libres y poderosos.

* **Adobe Experience Platform Web SDK** es el nombre oficial del nuevo código que implementarían las etiquetas para los casos de uso de Adobe. También es libre y poderoso.

* **`alloy.js`** es el nombre de archivo del código de Adobe Experience Platform Web SDK.

## ¿Tengo que utilizar etiquetas para implementar Web SDK?

No. Puede descargar el archivo de `alloy.js` usted mismo.

Sin embargo:

* Adobe Experience Platform Web SDK requiere algo llamado ID de flujo de datos para que la red perimetral pueda identificar el flujo y determinar qué hacer con los datos. Este ID se crea en Experience Platform. Esto no significa que tenga que utilizar la interfaz de usuario para crear propiedades o implementar el código JavaScript, pero sí necesita utilizar etiquetas para crear un ID de configuración.

* Las etiquetas no solo son las mejores etiquetas disponibles y el administrador de SDK, sino que también facilita la implementación de `alloy.js` y la asignación de datos a esquemas XDM. Si decide no utilizar etiquetas, deberá administrar la implementación de `alloy.js`, los eventos y la asignación de los datos en XDM antes de enviarlos. Este es un proceso _mucho_ más difícil que usar etiquetas.

* Se recomienda usar etiquetas para implementar `alloy.js`, incluso si es la única etiqueta para la que se usa.

## ¿Qué es el reenvío de eventos?

Si utiliza nuestros SDK y envía XDM a Edge Network, estas nuevas funciones y el reenvío de eventos le permiten instalar nuevas extensiones del lado del servidor y asignar esos datos a cualquier cosa (y enviarlos a cualquier lugar) desde nuestra red perimetral. Considérelo como &quot;recopilación de datos como un servicio&quot;. Esto estará disponible por un coste adicional y se incluirá como parte de Adobe Experience Platform.

## ¿Qué es un CNAME o dominio de origen y por qué importa?

Encontrará más información sobre un CNAME en [Documentación de Adobe](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/cname.html?lang=es)

## ¿Adobe Experience Platform Web SDK utiliza cookies? En caso afirmativo, ¿qué cookies utiliza?

Sí, actualmente Web SDK utiliza entre una y siete cookies en función de su implementación. A continuación se muestra una lista de las cookies que puede ver con Web SDK y la forma en que se utilizan:

| **Nombre** | **maxAge** | **Edad amistosa** | **Descripción** |
|---|---|---|---|
| **kndct_orgid_identity** | 34128000 | 395 días | La cookie de identidad almacena el ECID, así como otra información relacionada con el ECID. |
| **kndctr_orgid_permission_check** | 7200 | 2 horas | Esta cookie basada en sesión indica al servidor que busque las preferencias de consentimiento del lado del servidor. |
| **kndctr_orgid_permission** | 15552000 | 180 días | Esta cookie almacena la preferencia de consentimiento del usuario para el sitio web. |
| **kndctr_orgid_cluster** | 1800 | 30 minutos | Esta cookie almacena la región de Edge Network que sirve las solicitudes del usuario actual. La región se utiliza en la ruta URL para que Edge Network pueda enrutar la solicitud a la región correcta. Esta cookie tiene una duración de 30 minutos, de modo que si un usuario se conecta con una dirección IP diferente, la solicitud se puede enrutar a la región más cercana. |
| **mbox** | 63072000 | 2 años | Esta cookie aparece cuando la configuración de migración de Target se establece en verdadera. Esto permitirá que Web SDK establezca la [cookie de mbox](https://developer.adobe.com/target/implement/client-side/atjs/atjs-cookies/) de Target. |
| **mboxEdgeCluster** | 1800 | 30 minutos | Esta cookie aparece cuando la configuración de migración de Target se establece en verdadera. Esta cookie permite a Web SDK comunicar el clúster perimetral correcto a at.js para que los perfiles de Target puedan permanecer sincronizados a medida que los usuarios navegan por un sitio. |
| **AMCV_###@AdobeOrg** | 34128000 | 395 días | Esta cookie solo aparece cuando la migración de ID en Adobe Experience Platform Web SDK está habilitada. Esta cookie es útil cuando se realiza la transición a Web SDK mientras algunas partes del sitio siguen utilizando visitor.js. Consulte [`idMigrationEnabled`](/help/web-sdk/commands/configure/idmigrationenabled.md) para obtener más información. |

Al utilizar Web SDK, Edge Network establece una o más de las cookies anteriores. Edge Network establece todas las cookies con los atributos `secure` y `sameSite="none"`.

Si actualmente tiene secciones seguras y no seguras en su sitio web, esto podría interferir con la identificación del usuario. Cuando un usuario navega de una sección segura del sitio a una sección no segura, Edge Network genera un nuevo(a) `ECID` con la solicitud.

## ¿Con qué exploradores es compatible Adobe Experience Platform Web SDK?

Adobe Experience Platform Web SDK está diseñado para funcionar de forma óptima en las últimas versiones de Google Chrome, Safari, Firefox y Microsoft Edge Chromium. Es posible que tenga problemas al utilizar determinadas funciones en versiones anteriores de exploradores o exploradores obsoletos, como Internet Explorer.

## ¿Dónde puedo obtener más información sobre Adobe Experience Platform Web SDK?

* [Documentación](/help/web-sdk/home.md)
* [Código Source](https://github.com/adobe/alloy)
