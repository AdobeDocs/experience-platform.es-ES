---
title: Información general sobre Adobe Experience Platform Web Software Development Kit (SDK)
description: Aprenda a utilizar el SDK web de Adobe Experience Platform para integrar las funcionalidades de Platform en su sitio web.
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 2bf9c7ada9fd223df92b5cc9b1415f20705c2042
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 1%

---

# SDK web de Adobe Experience Platform {#overview}

El SDK web de Adobe Experience Platform es una biblioteca JavaScript del lado del cliente que permite a los clientes de Adobe Experience Cloud interactuar con sus servicios a través del Edge Network de Adobe Experience Platform.

Puede implementar el SDK web de dos formas:

* La [extensión de etiqueta SDK web](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Consulte el tutorial sobre cómo [implementar Adobe Experience Cloud con el SDK web](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=es) para obtener más información.
* Implementación manual mediante la biblioteca [Web SDK JavaScript](install/library.md).

Esta guía incluye instrucciones para interactuar con soluciones de Experience Cloud mediante la biblioteca JavaScript del SDK web y la extensión de etiquetas.

## Edge Network Experience Platform {#edge-network}



El SDK web de Experience Platform forma parte del Edge Network de Adobe Experience Platform, que incluye:

* **[SDK web de Experience Platform](#overview)**: Una biblioteca JavaScript y una extensión de etiquetas para simplificar la implementación de la tecnología de Adobe.
* **[SDK móvil de Experience Platform](https://developer.adobe.com/client-sdks/home/)**: Una extensión del SDK móvil v5 para la nueva metodología de implementación.
* **[API de Edge Network](../server-api/overview.md)**: una API del lado del servidor para la recopilación de datos, personalización, publicidad y casos de uso de marketing. Puede usarlo en servidores, dispositivos IoT, descodificadores y otros dispositivos.

El Edge Network proporciona recopilación de datos de baja latencia, informática conectable y activación rápida de datos en todos los canales direccionables. Ofrece un único SDK consolidado para canales web, móviles y del lado del servidor, que envía datos a un dominio de Adobe común (`adobedc.net`) y recibe una única carga útil para la entrega de datos y experiencia.

En el lado del servidor, una puerta de enlace perimetral unificada y un marco de servicio de plataforma común simplifican la implementación de nuevas funcionalidades, a la vez que proporcionan las siguientes ventajas:

* Reducir el tiempo de respuesta del cliente al valor;
* Poner fin a la necesidad de integraciones puntuales;
* Mejora del rendimiento en comparación con las bibliotecas antiguas;
* Reducción de los costes de funcionamiento;
* Aumentar la velocidad de innovación;
* Creación de ventajas competitivas sostenidas para los clientes de Adobe.

Un sistema Edge consolidado le permite administrar campañas de publicidad, marketing y personalización en todos los canales. Reduce el coste total de propiedad y admite varios tipos de datos, lo que permite asignar el modelo de datos para utilizarlo con varios productos de Experience Cloud.

## Vídeo introductorio {#video}

Vea el siguiente vídeo para obtener información general sobre Adobe Experience Platform [!DNL Web SDK] y [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## Bibliotecas reemplazadas por el SDK web {#sdks}

El SDK web es una nueva biblioteca de código abierto creada desde cero para integrar las funcionalidades de las bibliotecas existentes. Soluciona problemas con el orden de activación de etiquetas, incoherencias de versiones y administración de dependencias, lo que ofrece una nueva forma de [código abierto](https://github.com/adobe/alloy) de implementar [!DNL Experience Cloud].

El SDK web reemplaza a:

* `Visitor.js`
* `AppMeasurement.js`
* `AT.js`
* `DIL.js`

También introduce un nuevo extremo que optimiza las solicitudes HTTP a las soluciones de Adobe. Anteriormente, se necesitaban varias llamadas para `Visitor.js`, `AT.js`, `DIL.js` y `AppMeasurement.js`. Ahora, una sola llamada puede recuperar un ID, obtener una experiencia de [!DNL Target], enviar datos a [!DNL Audience Manager] y pasar datos a Adobe Experience Platform.

Vea el siguiente vídeo para ver Adobe Experience Platform [!DNL Web SDK] y [!DNL Edge Network] en acción, usando una sola llamada para enviar datos a [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager] y [!DNL Target].

>[!VIDEO](https://video.tv.adobe.com/v/34148)

## Migración de bibliotecas existentes al SDK web {#migrating-to-web-sdk}

El Adobe ofrece una ruta de actualización optimizada para simplificar la migración de cualquiera de las [bibliotecas existentes](#sdks) al SDK web. Puede migrar cada página del sitio web de forma individual, sin necesidad de migrar todo el sitio a la vez. Puede utilizar el SDK web en algunas páginas mientras las bibliotecas existentes permanecen en otras, lo que permite una transición gradual.

### Migración de `AT.js` a consideraciones del SDK web {#considerations}

Antes de migrar páginas con `AT.js` al SDK web, habilite las siguientes opciones de configuración del SDK web para asegurarse de que el perfil del visitante se mantiene al navegar entre páginas.

* [&quot;idMigrationEnabled&quot;](/help/web-sdk/commands/configure/idmigrationenabled.md)
* [&quot;targetMigrationEnabled&quot;](/help/web-sdk/commands/configure/targetmigrationenabled.md)

>[!IMPORTANT]
>
>Las siguientes características de Target no se admiten al migrar de `at.js` al SDK web:
>
>* [Ofertas de redireccionamiento](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html?lang=es)
>* [Compatibilidad con CNAME y entre dominios](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/atjs-cookies.html)

Después de migrar de `AT.js` al SDK web, quite la opción `targetMigrationEnabled` de la configuración.
