---
title: Información general del SDK web de Adobe Experience Platform
description: Aprenda a utilizar el SDK web de Adobe Experience Platform para integrar las funcionalidades de Platform en su sitio web.
keywords: SDK web de Adobe Experience Platform;SDK web de plataforma;SDK web;edge;Visitor.js;AppMeasurement.js;AT.js;DIL.js;sdk web;SDK;SDK web;Launch;iniciar
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 1048f19e2395f63fac8c4218ed92a546b8071a93
workflow-type: tm+mt
source-wordcount: '703'
ht-degree: 1%

---

# Información general del SDK web de Adobe Experience Platform

El SDK web de Adobe Experience Platform es una biblioteca JavaScript del lado del cliente que permite a los clientes de Adobe Experience Cloud interactuar con los distintos servicios del [!DNL Experience Cloud] a través de Adobe Experience Platform Edge Network. Además de la biblioteca JavaScript, hay un [extensión de etiqueta](./extension/web-sdk-extension-configuration.md) para ayudarle con las configuraciones del SDK web.

**Para obtener una guía paso a paso sobre la configuración del SDK web con etiquetas y el envío de datos a las soluciones, consulte nuestra [Tutorial de implementación de Adobe Experience Cloud con SDK web](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=en)**

## Experience Edge

[!DNL Adobe Experience Platform Web SDK] forma parte de la colección que conforma Experience Edge. Experience Edge consta de tres tecnologías:

* **[!DNL Adobe Experience Platform Web SDK]:** Un SDK de JavaScript y la extensión de etiquetas para simplificar considerablemente la implementación [!DNL Adobe] tecnologías
* **SDK de Adobe Experience Platform Mobile:** Extensión del SDK móvil v5 para permitir a los clientes utilizar la nueva metodología de implementación
* **[!DNL Adobe Experience Platform Edge Network]:** Una red distribuida global de servidores que permiten una nueva metodología de implementación [!DNL Adobe] products

La variable [!DNL Adobe Experience Edge] es un nuevo marco para la recopilación de datos de baja latencia, la computación conectable y la activación rápida de datos en todos los canales a los que se puede dirigir.

[!DNL Adobe Experience Edge] proporciona un único SDK consolidado para cada canal (JavaScript, móvil, del lado del servidor), que envía datos a un dominio de Adobe común (`adobedc.net`) y recibe una única carga útil para el envío de datos y experiencias.

En el lado del servidor, una puerta de enlace perimetral unificada y un marco de servicios de plataforma común facilitan la incorporación e implementación de nuevas capacidades en este entorno informático en tiempo real.  Esta arquitectura:

* Reduce el tiempo de respuesta del cliente
* Finaliza la necesidad de integraciones &quot;puntuales&quot;
* Mejora el rendimiento en comparación con las bibliotecas antiguas
* Disminuye costes
* Aumenta la velocidad de la innovación
* Crea ventajas competitivas sostenidas para los clientes de Adobe

Un solo sistema Edge consolidado permite a los clientes administrar sus campañas de publicidad, marketing o personalización en todos los canales como una experiencia integrada.  Permite [!DNL Adobe] para ofrecer servicios con un menor coste total de propiedad para los clientes.  También ayuda a aumentar la velocidad de innovación de los productos al hacer que el borde en tiempo real sea conectable y permitir [!DNL Adobe] y sus clientes para agregar más rápidamente nuevas funciones y lógica definida por el cliente a ese sistema en tiempo real.

## Información general del vídeo

El siguiente vídeo ofrece información general sobre Adobe Experience Platform [!DNL Web SDK] y Adobe Experience Platform [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## SDK reemplazado por el SDK web de Adobe Experience Platform

El SDK web de Adobe Experience Platform sustituye a los siguientes SDK:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

Esto no es solamente un envoltorio alrededor de bibliotecas existentes. Es una reescritura completa. Su objetivo es acabar con los desafíos, ya que las etiquetas deben activarse en el orden correcto, con incoherencia con los desafíos de versiones de las bibliotecas y con una mejor administración de dependencias. Es una nueva forma de implementar el [!DNL Experience Cloud] y es [código abierto](https://github.com/adobe/alloy).

Además de una nueva biblioteca, existe un nuevo punto final que optimiza las solicitudes HTTP para las soluciones de Adobe. Antes, Visitor.js enviaba una llamada de bloqueo al servicio de ID de visitante, luego AT.js enviaba una llamada a Adobe Target, DIL.js enviaba una llamada a Adobe Audience Manager y, finalmente, AppMeasurement.js enviaba una llamada a Adobe Analytics. Esta nueva biblioteca y punto final puede recuperar un ID y obtener un [!DNL Target] experiencia, enviar datos a [!DNL Audience Manager]y pasar los datos a Adobe Experience Platform en una sola llamada.

El siguiente vídeo muestra Adobe Experience Platform [!DNL Web SDK] y Adobe Experience Platform [!DNL Edge Network] en acción. El ejemplo de vídeo utiliza una sola llamada al Adobe que envía datos a [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager]y [!DNL Target].

>[!VIDEO](https://video.tv.adobe.com/v/34148?quality=12&learn=on)

Este producto evoluciona constantemente y crece para dar soporte a cada vez más casos de uso. Para mantenerse al día con las últimas novedades, consulte la [página de casos de uso admitidos](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/supported-use-cases.html). Esta página enumera los casos de uso que admitimos actualmente, con vínculos a más información cuando está disponible.

* **Casos de uso aún no compatibles:** Estos son casos de uso que están en nuestra hoja de ruta para ser apoyados en el futuro.
* **Casos De Uso En Curso:** Estos son los casos de uso en los que el equipo está trabajando para su lanzamiento.
* **Casos de uso compatibles:** Estos son los casos de uso compatibles y que funcionan hoy en día.
* **Casos de uso que no admitiremos:** Estos son los casos de uso que hemos tomado la decisión de no apoyar.
