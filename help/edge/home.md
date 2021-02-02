---
title: Ayuda del SDK web de Adobe Experience Platform
seo-title: Ayuda del SDK web de Adobe Experience Platform
description: Descubra qué es el SDK web de Adobe Experience Platform y cómo se puede utilizar.
seo-description: Obtenga información sobre cómo permitir que los clientes de Adobe Experience Cloud interactúen con los distintos servicios del Experience Cloud.
keywords: SDK web de Adobe Experience Platform;SDK web de plataforma;SDK web;edge;Visitante.js;AppMeasurement.js;AT.js;DIL.js;sdk web;SDK;SDK web;Launch;launch
translation-type: tm+mt
source-git-commit: 2dbd92efbd992b70f4f750b09e9d2e0626e71315
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 1%

---


# ¿Qué es Adobe Experience Platform Web SDK?

Adobe Experience Platform Web SDK es una biblioteca JavaScript del lado del cliente que permite a los clientes de Adobe Experience Cloud interactuar con los distintos servicios de [!DNL Experience Cloud] a través de Adobe Experience Platform Edge Network. Además de la biblioteca JavaScript, existe una [extensión de Experience Platform Launch](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/aep-extension/overview.html) para ayudarle con las configuraciones del SDK web.

## Experience Edge

[!DNL Adobe Experience Platform Web SDK] forma parte de la colección que forma Experience Edge. Experience Edge consta de tres tecnologías:

* **[!DNL Adobe Experience Platform Web SDK]:** Un SDK y una  [!DNL Experience Platform Launch] extensión de JavaScript para simplificar considerablemente la implementación de  [!DNL Adobe] tecnologías
* **SDK de Adobe Experience Platform Mobile:** extensión del SDK para móviles v5 que permite a los clientes utilizar la nueva metodología de implementación
* **[!DNL Adobe Experience Platform Edge Network]:** Una red global de servidores distribuidos que permite una nueva metodología para implementar  [!DNL Adobe] productos

El [!DNL Adobe Experience Edge] es un nuevo entorno para la recopilación de datos de baja latencia, la informática conectable y la rápida activación de datos en todos los canales direccionables.

[!DNL Adobe Experience Edge] proporciona un único SDK consolidado para cada canal (JavaScript, Móvil, del lado del servidor), que envía datos a un dominio de Adobe común (`adobedc.net`) y recibe una única carga útil para el envío de datos y experiencias.

En el lado del servidor, un gateway Edge unificado y un entorno de servicios de plataforma común facilitan el complemento e implementación de nuevas capacidades en este entorno informático en tiempo real.  Esta arquitectura:

* Disminuye el tiempo de respuesta del cliente al valor
* Termina con la necesidad de integraciones &quot;puntuales&quot;
* Mejora el rendimiento en comparación con las bibliotecas antiguas
* Disminuye los costos
* Aumenta la velocidad de la innovación
* Crea ventajas competitivas sostenidas para los clientes de Adobe

Un único sistema de Edge consolidado permite a los clientes gestionar sus campañas de publicidad, marketing o personalización en todos los canales como una experiencia integrada.  Permite que [!DNL Adobe] proporcione servicios con un menor costo total de propiedad para los clientes.  También ayuda a aumentar la velocidad de la innovación de los productos al hacer que el borde en tiempo real sea conectable y permitir que [!DNL Adobe] y sus clientes añadan más rápidamente nuevas capacidades y lógica definida por el cliente a ese sistema en tiempo real.

## Información general del vídeo

El siguiente vídeo proporciona una visión general de Adobe Experience Platform [!DNL Web SDK] y Adobe Experience Platform [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## SDK reemplazados por Adobe Experience Platform Web SDK

El SDK web de Adobe Experience Platform sustituye a los siguientes SDK:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

Esto no es sólo un envoltorio en torno a las bibliotecas existentes. Es una reescritura completa. Su propósito es acabar con los desafíos, ya que las etiquetas deben activarse en el orden correcto, con incoherencias con los desafíos de versiones de las bibliotecas y con una mejor administración de las dependencias. Es una nueva manera de implementar el [!DNL Experience Cloud] y es [código abierto](https://github.com/adobe/alloy).

Además de una nueva biblioteca, existe un nuevo extremo que racionaliza las solicitudes HTTP a las soluciones de Adobe. Antes, Visitante.js enviaba una llamada de bloqueo al servicio de ID de visitante, luego AT.js enviaba una llamada a Adobe Target, DIL.js enviaba una llamada a Adobe Audience Manager y, finalmente, AppMeasurement.js enviaba una llamada a Adobe Analytics. Esta nueva biblioteca y punto final puede recuperar un ID, recuperar una experiencia [!DNL Target], enviar datos a [!DNL Audience Manager] y pasar los datos a Adobe Experience Platform en una sola llamada.

El siguiente vídeo muestra Adobe Experience Platform [!DNL Web SDK] y Adobe Experience Platform [!DNL Edge Network] en acción. El ejemplo de vídeo utiliza una sola llamada a Adobe que envía datos a [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager] y [!DNL Target].

>[!VIDEO](https://video.tv.adobe.com/v/34148?quality=12&learn=on)

Este producto evoluciona y crece constantemente para dar soporte a cada vez más casos de uso. Para mantenerse al día con las últimas novedades, consulte nuestra [placa de casos de uso admitida](https://github.com/adobe/alloy/projects/5). Mantenemos esto al día con los casos de uso que actualmente apoyamos y con los que estamos trabajando para permitirle tomar las mejores decisiones posibles.

* **Casos de uso aún no admitidos:** Estos son casos de uso que están en nuestra hoja de ruta para ser admitidos en el futuro.
* **Casos de uso en curso:** Estos son los casos de uso en los que el equipo está trabajando para su lanzamiento.
* **Casos de uso admitidos:** Son los casos de uso que se admiten y funcionan en la actualidad.
* **Casos de uso que no vamos a apoyar:** Estos son los casos de uso que hemos tomado la decisión de no apoyar.
