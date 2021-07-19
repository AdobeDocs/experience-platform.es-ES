---
title: Información general del SDK web de Adobe Experience Platform
description: Aprenda a utilizar el SDK web de Adobe Experience Platform para integrar las funcionalidades de Platform en su sitio web.
keywords: SDK web de Adobe Experience Platform;SDK web de plataforma;SDK web;edge;Visitor.js;AppMeasurement.js;AT.js;DIL.js;sdk web;SDK;SDK web;Launch;iniciar
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 1%

---

# Información general del SDK web de Adobe Experience Platform

El SDK web de Adobe Experience Platform es una biblioteca JavaScript del lado del cliente que permite a los clientes de Adobe Experience Cloud interactuar con los distintos servicios de [!DNL Experience Cloud] a través de la red perimetral de Adobe Experience Platform. Además de la biblioteca JavaScript, existe una [extensión de Experience Platform Launch](../tags/extensions/web/sdk/overview.md) que le ayudará con las configuraciones del SDK web.

## Experience Edge

[!DNL Adobe Experience Platform Web SDK] forma parte de la colección que conforma Experience Edge. Experience Edge consta de tres tecnologías:

* **[!DNL Adobe Experience Platform Web SDK]:** Un SDK y una  [!DNL Experience Platform Launch] extensión de JavaScript para simplificar considerablemente la implementación de  [!DNL Adobe] tecnologías
* **SDK de Adobe Experience Platform Mobile:** Una extensión del SDK móvil v5 para permitir a los clientes utilizar la nueva metodología de implementación
* **[!DNL Adobe Experience Platform Edge Network]:** Una red distribuida global de servidores que permiten una nueva metodología de implementación de  [!DNL Adobe] productos

El [!DNL Adobe Experience Edge] es un nuevo marco para la recopilación de datos de baja latencia, la computación conectable y la activación rápida de datos en todos los canales a los que se puede dirigir.

[!DNL Adobe Experience Edge] proporciona un único SDK consolidado para cada canal (JavaScript, móvil, del lado del servidor), que envía datos a un dominio de Adobe común (`adobedc.net`) y recibe una única carga útil para el envío de datos y experiencias.

En el lado del servidor, una puerta de enlace perimetral unificada y un marco de servicios de plataforma común facilitan la incorporación e implementación de nuevas capacidades en este entorno informático en tiempo real.  Esta arquitectura:

* Reduce el tiempo de respuesta del cliente
* Finaliza la necesidad de integraciones &quot;puntuales&quot;
* Mejora el rendimiento en comparación con las bibliotecas antiguas
* Disminuye costes
* Aumenta la velocidad de la innovación
* Crea ventajas competitivas sostenidas para los clientes de Adobe

Un solo sistema Edge consolidado permite a los clientes administrar sus campañas de publicidad, marketing o personalización en todos los canales como una experiencia integrada.  Permite que [!DNL Adobe] proporcione servicios con un menor costo total de propiedad para los clientes.  También ayuda a aumentar la velocidad de innovación del producto al hacer que el borde en tiempo real sea conectable y permitir que [!DNL Adobe] y sus clientes añadan más rápidamente nuevas funciones y lógica definida por el cliente a ese sistema en tiempo real.

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

Además de una nueva biblioteca, existe un nuevo punto final que optimiza las solicitudes HTTP para las soluciones de Adobe. Antes, Visitor.js enviaba una llamada de bloqueo al servicio de ID de visitante, luego AT.js enviaba una llamada a Adobe Target, DIL.js enviaba una llamada a Adobe Audience Manager y, finalmente, AppMeasurement.js enviaba una llamada a Adobe Analytics. Esta nueva biblioteca y punto final pueden recuperar un ID, recuperar una experiencia [!DNL Target], enviar datos a [!DNL Audience Manager] y pasar los datos a Adobe Experience Platform en una sola llamada.

El siguiente vídeo muestra Adobe Experience Platform [!DNL Web SDK] y Adobe Experience Platform [!DNL Edge Network] en acción. El ejemplo de vídeo utiliza una sola llamada al Adobe que envía datos a [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager] y [!DNL Target].

>[!VIDEO](https://video.tv.adobe.com/v/34148?quality=12&learn=on)

Este producto evoluciona constantemente y crece para dar soporte a cada vez más casos de uso. Para mantenerse al día con las últimas novedades, consulte la [página de casos de uso admitidos](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/supported-use-cases.html). Esta página enumera los casos de uso que admitimos actualmente, con vínculos a más información cuando está disponible.

* **Casos de uso aún no compatibles:** Estos son casos de uso que están en nuestra hoja de ruta para ser compatibles en el futuro.
* **Casos de uso en curso:** estos son los casos de uso en los que el equipo está trabajando para su lanzamiento.
* **Casos de uso compatibles:** estos son los casos de uso compatibles y que funcionan actualmente.
* **Casos de uso que no vamos a apoyar:** estos son los casos de uso que hemos tomado la decisión de no apoyar.
