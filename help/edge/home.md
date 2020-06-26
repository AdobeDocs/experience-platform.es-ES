---
title: Ayuda del SDK web de Adobe Experience Platform
seo-title: Ayuda del SDK web de Adobe Experience Platform
description: Descubra qué es el SDK de Adobe Experience Platform Web y cómo se puede utilizar.
seo-description: permite a los clientes de Adobe Experience Cloud interactuar con los distintos servicios del Experience Cloud.
translation-type: tm+mt
source-git-commit: 3f52def8318f57cfc6534e15415d172e768a8614
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---


# ¿Qué es el SDK web de Adobe Experience Platform?

Adobe Experience Platform Web SDK es una biblioteca JavaScript del lado del cliente que permite a los clientes de Adobe Experience Cloud interactuar con los distintos servicios del Experience Cloud a través de Adobe Experience Platform Edge Network.

## SDK reemplazados por SDK web de Adobe Experience Platform

El SDK web de Adobe Experience Platform sustituye a los siguientes SDK:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

Esto no es sólo un envoltorio en torno a las bibliotecas existentes. Es una reescritura completa. Su propósito es acabar con los desafíos, ya que las etiquetas deben activarse en el orden correcto, con incoherencias con los desafíos de versiones de las bibliotecas y con una mejor administración de las dependencias. Es una nueva forma de implementar el Experience Cloud y es de código [abierto](https://github.com/adobe/alloy).

Además de una nueva biblioteca, existe un nuevo extremo que racionaliza las solicitudes HTTP a las soluciones de Adobe. Antes, Visitante.js enviaba una llamada de bloqueo al servicio de ID de visitante, luego AT.js enviaba una llamada a Adobe Target, DIL.js enviaba una llamada a Adobe Audience Manager y, finalmente, AppMeasurement.js enviaba una llamada a Adobe Analytics. Esta nueva biblioteca y punto final puede recuperar un ID, recuperar una [!DNL Target] experiencia, enviar datos al Audience Manager y pasar los datos al Adobe Experience Platform en una sola llamada.

## Primeros pasos

Le recomendamos que [consulte nuestra guía](getting-started/quick-start-with-launch.md) de introducción para ver un tutorial rápido sobre cómo empezar a utilizar Adobe Launch.

Este producto evoluciona y crece constantemente para dar soporte a cada vez más casos de uso. Para mantenerse al día con las últimas novedades, eche un vistazo a nuestro panel de casos [de uso](https://github.com/adobe/alloy/projects/5)admitidos. Mantenemos esto al día con los casos de uso que actualmente apoyamos y con los que estamos trabajando para permitirle tomar las mejores decisiones posibles.

* __Casos de uso aún no admitidos__ : Son casos de uso que están en nuestro plan de trabajo y que se admitirán en el futuro.
* __Casos de uso en curso__ : Estos son los casos de uso en los que el equipo está trabajando para su lanzamiento.
* __Casos__ de uso admitidos: Son los casos de uso que se admiten y funcionan en la actualidad.
* __Casos de uso que no vamos a apoyar__ - Estos son los casos de uso que hemos tomado la decisión de no apoyar.
