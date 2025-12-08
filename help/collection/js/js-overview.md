---
title: Información general sobre la biblioteca JavaScript de Web SDK
description: Envíe datos al Edge Network de Adobe Experience Platform mediante JavaScript.
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 7f932e9868e84cf8abdaa6cf0b2da5bac837234d
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 0%

---

# Información general sobre la biblioteca JavaScript de Web SDK

**Adobe Experience Platform Web SDK** es una biblioteca JavaScript del lado del cliente que le permite enviar datos a Adobe Experience Platform Edge Network. Esta guía describe la ruta de implementación de la biblioteca Web SDK JavaScript (`alloy.js`), incluidos los conceptos básicos, la instalación, la configuración y los comandos. Para la extensión de etiquetas Web SDK en la interfaz de usuario de recopilación de datos, consulte la [extensión de etiquetas Web SDK](/help/tags/extensions/client/web-sdk/overview.md).

Web SDK envía datos de forma independiente de las soluciones (XDM) a Experience Platform Edge Network, que a su vez asigna los datos a formatos y destinos específicos de la solución y los envía en tiempo real.

## Experience Platform Edge Network {#edge-network}

Adobe Experience Platform Edge Network proporciona recopilación de datos de baja latencia, informática conectable y activación rápida de datos en todos los canales direccionables. Ofrece un único SDK consolidado para canales web, móviles y del lado del servidor, que envía datos a un dominio común de Adobe (`adobedc.net`) y recibe una única carga útil para la entrega de datos y experiencia.

En el lado del servidor, una puerta de enlace perimetral unificada y un marco de servicio de plataforma común simplifican la implementación de nuevas funcionalidades, a la vez que proporcionan las siguientes ventajas:

* Reducir el tiempo de respuesta del cliente al valor;
* Poner fin a la necesidad de integraciones puntuales;
* Mejora del rendimiento en comparación con las bibliotecas antiguas;
* Reducción de los costes de funcionamiento;
* Aumentar la velocidad de innovación;
* Creación de ventajas competitivas sostenidas para los clientes de Adobe.

Un sistema Edge consolidado le permite administrar campañas de publicidad, marketing y personalización en todos los canales. Reduce el coste total de propiedad y admite varios tipos de datos, lo que le permite asignar el modelo de datos para utilizarlo con varios productos de Experience Cloud.

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## Bibliotecas reemplazadas por Web SDK {#sdks}

Web SDK es una biblioteca de código abierto creada desde cero para integrar las funcionalidades de las bibliotecas existentes. Aborda los problemas con el orden de activación de etiquetas, las incoherencias de la versión y la administración de dependencias, lo que ofrece una forma de implementar muchos productos de Experience Cloud. Web SDK reemplaza la recopilación de datos para los siguientes servicios:

* Servicio de ID de visitante de Adobe Experience Platform (`Visitor.js`)
* Adobe Analytics (`AppMeasurement.js`)
* Adobe Target (`AT.js`)
* Adobe Audience Manager (`DIL.js`)
* Adobe Media Analytics
* Adobe Advertising

También introduce un nuevo extremo que optimiza las solicitudes HTTP a las soluciones de Adobe. Anteriormente, se necesitaban varias llamadas para cada biblioteca de recopilación de datos. Ahora, una sola llamada puede recuperar un ID, obtener una experiencia de [!DNL Target], enviar datos a [!DNL Audience Manager] y pasar datos a Adobe Experience Platform.

## Migración de bibliotecas existentes a Web SDK {#migrating-to-web-sdk}

Adobe ofrece una ruta de actualización optimizada para simplificar la migración de cualquiera de las bibliotecas existentes a Web SDK. Puede migrar cada página del sitio web de forma individual, sin necesidad de migrar todo el sitio a la vez. Puede utilizar Web SDK en algunas páginas mientras las bibliotecas existentes permanecen en otras, lo que permite una transición gradual.
