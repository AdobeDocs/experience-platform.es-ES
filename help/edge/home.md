---
title: Ayuda del SDK web de Adobe Experience Platform
seo-title: Ayuda del SDK web de Adobe Experience Platform
description: Descubra qué es el SDK web de Adobe Experience Platform y cómo se puede utilizar.
seo-description: permita a los clientes de Adobe Experience Cloud interactuar con los distintos servicios de Experience Cloud.
translation-type: tm+mt
source-git-commit: f06c90d6248071894bd9929fbe1150e30c8e7385
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---


# ¿Qué es el SDK web de Adobe Experience Platform?

Adobe Experience Platform Web SDK es una biblioteca JavaScript del lado del cliente que permite a los clientes de Adobe Experience Cloud interactuar con los distintos servicios de Experience Cloud a través de Adobe Experience Platform Edge Network.

## SDK reemplazados por el SDK web de Adobe Experience Platform

El SDK web de la plataforma Adobe Experience sustituye a los siguientes SDK:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

Esto no es sólo un envoltorio en torno a las bibliotecas existentes. Es una reescritura completa. Su propósito es acabar con los desafíos con la activación de etiquetas en el orden correcto, la incoherencia con los desafíos de versiones de la biblioteca y una mejor administración de dependencias. Es una nueva forma de implementar Experience Cloud y es de código [abierto](https://github.com/adobe/alloy)

Además de una nueva biblioteca, existe un nuevo extremo que racionaliza las solicitudes HTTP a las soluciones de Adobe. Antes, Visitante.js enviaba una llamada de bloqueo al servicio de ID de visitante y, a continuación, AT.js enviaba una llamada a Adobe Destinatario, DIL.js enviaba una llamada a Adobe Audiencia Manager y, finalmente, AppMeasurement.js enviaba una llamada a Adobe Analytics. Esta nueva biblioteca y punto final puede recuperar un ID, recuperar una experiencia de Destinatario, enviar datos al Administrador de Audiencias y pasar los datos a Adobe Experience Platform en una sola llamada.

## Primeros pasos

Le recomendamos encarecidamente que [consulte nuestra guía](getting-started/quick-start-with-launch.md) de introducción para ver un tutorial rápido sobre cómo empezar a utilizar el lanzamiento.

Este producto evoluciona y crece constantemente para dar soporte a cada vez más casos de uso. Para mantenerse al día con las últimas novedades, descargamos nuestro tablero [de casos de uso](https://github.com/adobe/alloy/projects/5)admitidos. Mantenemos esto al día con los casos de uso que actualmente apoyamos y en los que estamos trabajando para permitirle tomar las mejores decisiones posibles.

* __Casos de uso aún no admitidos__ : son casos de uso que están en nuestro plan de trabajo para ser realizados en el futuro.
* __Casos de uso en curso__ : Estos son los casos de uso en los que el equipo está trabajando para su lanzamiento.
* __Casos__ de uso admitidos: Son los casos de uso que se admiten y funcionan en la actualidad.
* __Casos de uso que no vamos a apoyar__ - Estos son los casos de uso que hemos tomado la decisión de no apoyar.
