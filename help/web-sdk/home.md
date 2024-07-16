---
title: Información general sobre Adobe Experience Platform Web Software Development Kit (SDK)
description: Aprenda a utilizar el SDK web de Adobe Experience Platform para integrar las funcionalidades de Platform en su sitio web.
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 58cd6300307881c3de7c52e07c401bf2ed908517
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 1%

---


# SDK web de Adobe Experience Platform {#overview}

>[!IMPORTANT]
>
>A finales de abril de 2024, el SDK web de Adobe Experience Platform eliminará la compatibilidad con todas las versiones de Internet Explorer.

El Kit de desarrollo de software web (SDK) de Adobe Experience Platform es una biblioteca JavaScript del lado del cliente que permite a los clientes de Adobe Experience Cloud interactuar con sus servicios a través del Edge Network de Adobe Experience Platform.

Adobe ofrece dos métodos para implementar el SDK web:

* La [extensión de etiqueta SDK web](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Consulte el tutorial sobre cómo [implementar Adobe Experience Cloud con el SDK web](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=es) para obtener más información.
* Implementación manual mediante la biblioteca JavaScript del SDK web.

Esta guía del usuario incluye instrucciones sobre cómo interactuar con las soluciones de Experience Cloud a través de la biblioteca JavaScript del SDK web y la extensión de etiquetas, cuando corresponda.

## Edge Network Experience Platform {#edge-network}

El SDK web de Experience Platform forma parte de una colección de herramientas que conforman el Edge Network de Adobe Experience Platform.

El Edge Network consta de los siguientes componentes:

* **[SDK web de Experience Platform](#overview):** Una biblioteca JavaScript y una extensión de etiquetas que le ayudarán a simplificar la implementación de tecnologías de Adobe.
* **[SDK móvil de Experience Platform](https://developer.adobe.com/client-sdks/home/):** Extensión del SDK móvil v5 que le permite utilizar la nueva metodología de implementación.
* **[API de servidor Edge Network](../server-api/overview.md):** Una API del lado del servidor que puede usar para varios casos de uso de recopilación de datos, personalización, publicidad y marketing. La API de servidor se puede utilizar en servidores, dispositivos de IoT, descodificadores y otros dispositivos.

El Edge Network es una plataforma para la recopilación de datos de baja latencia, la computación conectable y la activación rápida de datos en todos los canales direccionables. Proporciona un único SDK consolidado para cada canal (web, móvil, del lado del servidor), que envía datos a un dominio de Adobe común (`adobedc.net`) y recibe una sola carga útil para la entrega de datos y experiencia.

En el lado del servidor, una puerta de enlace perimetral unificada y un marco de servicio de plataforma común ayudan a facilitar la implementación de nuevas funciones en este entorno informático en tiempo real. Esta arquitectura:

* Reduce el tiempo de respuesta del cliente
* Finaliza la necesidad de integraciones puntuales
* Mejora el rendimiento en comparación con las bibliotecas antiguas
* Disminuye los costes
* Aumenta la velocidad de la innovación
* Crea ventajas competitivas sostenidas para los clientes de Adobe

Un único sistema Edge consolidado le permite administrar sus campañas de publicidad, marketing o personalización en todos los canales como una experiencia integrada. También permite al Adobe prestar servicios con un coste total de propiedad menor para los clientes. El sistema Edge está diseñado para dar cabida a la mayoría de los tipos de datos, lo que le permite asignar su propio modelo de datos para que lo incorporen varios productos de Experience Cloud.

## Vídeo introductorio {#video}

Vea el siguiente vídeo para obtener información general sobre Adobe Experience Platform [!DNL Web SDK] y [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## Bibliotecas reemplazadas por el SDK web {#sdks}

El SDK web no es solo un contenedor de las bibliotecas existentes. Es una nueva biblioteca, escrita desde cero para incorporar funcionalidades de bibliotecas existentes. Su propósito es poner fin a los desafíos: las etiquetas deben activarse en el orden correcto, la incoherencia con los desafíos de las versiones de la biblioteca y una mejor administración de la dependencia. Es una nueva forma de implementar [!DNL Experience Cloud] y es de [código abierto](https://github.com/adobe/alloy).

El SDK web reemplaza los siguientes SDK:

* `Visitor.js`
* `AppMeasurement.js`
* `AT.js`
* `DIL.js`

Además de una nueva biblioteca, hay un nuevo punto de conexión que optimiza las solicitudes HTTP a las soluciones de Adobe. Antes, `Visitor.js` enviaba una llamada de bloqueo al servicio de ID de visitante, después `AT.js` enviaba una llamada a Adobe Target, `DIL.js` enviaba una llamada a Adobe Audience Manager y, por último, `AppMeasurement.js` enviaba una llamada a Adobe Analytics. Esta nueva biblioteca y extremo pueden recuperar un identificador, obtener una experiencia de [!DNL Target], enviar datos a [!DNL Audience Manager] y pasar los datos a Adobe Experience Platform mediante una sola llamada.

El siguiente vídeo muestra a Adobe Experience Platform [!DNL Web SDK] y Adobe Experience Platform [!DNL Edge Network] en acción. El ejemplo de vídeo utiliza una sola llamada al Adobe que envía datos a [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager] y [!DNL Target].

>[!VIDEO](https://video.tv.adobe.com/v/34148)

## Migración de bibliotecas existentes al SDK web {#migrating-to-web-sdk}

Para simplificar la migración de cualquiera de las [bibliotecas existentes](#sdks) al SDK web, Adobe ofrece una ruta de actualización optimizada. Esta ruta le permite migrar cada página individual del sitio web al SDK web sin necesidad de migrar todo el sitio web a la vez. Puede utilizar el SDK web en una página determinada mientras las bibliotecas existentes residen en otras páginas. Una vez que esté listo, también puede migrar esas otras páginas.

### Migración de `AT.js` a consideraciones del SDK web {#considerations}

Antes de migrar páginas que usan `AT.js` al SDK web, asegúrese de habilitar las siguientes opciones de configuración del SDK web. Estas opciones garantizan que el perfil del visitante se mantenga mientras se navega de páginas con `AT.js` a páginas que utilizan el SDK web.

* [&quot;idMigrationEnabled&quot;](/help/web-sdk/commands/configure/idmigrationenabled.md)
* [&quot;targetMigrationEnabled&quot;](/help/web-sdk/commands/configure/targetmigrationenabled.md)


>[!IMPORTANT]
>
>Las siguientes funciones de Target no son compatibles al migrar de at.js a SDK web:
>
>* [Ofertas de redireccionamiento](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html?lang=es)
>* [Compatibilidad con CNAME y entre dominios](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/atjs-cookies.html)

Después de migrar de `AT.js` al SDK web, quite la opción `targetMigrationEnabled` de la configuración.
