---
title: Ayuda del SDK web de Adobe Experience Platform
seo-title: Ayuda del SDK web de Adobe Experience Platform
description: Descubra qué es el SDK web de Adobe Experience Platform y cómo se puede utilizar.
seo-description: permitir a los clientes de Adobe Experience Cloud interactuar con los distintos servicios de Experience Cloud
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (Beta) ¿Qué es el SDK web de Adobe Experience Platform?

>[!IMPORTANT]
>
>El SDK web de la plataforma de experiencia de Adobe se encuentra en fase beta y no está disponible para todos los usuarios. La documentación y la funcionalidad están sujetas a cambios.

Adobe Experience Platform Web SDK es una biblioteca JavaScript del lado del cliente que permite a los clientes de Adobe Experience Cloud interactuar con los distintos servicios de Experience Cloud.

## SDK reemplazados por el SDK web de Adobe Experience Platform

El SDK web de la plataforma Adobe Experience sustituye a los siguientes SDK:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

Esto no es sólo un envoltorio en torno a las bibliotecas existentes. Es una reescritura completa. Su propósito es acabar con los desafíos con la activación de etiquetas en el orden correcto, la incoherencia con los desafíos de versiones de la biblioteca y una mejor administración de dependencias. Es una nueva forma de implementar Experience Cloud.

Además de una nueva biblioteca, existe un nuevo extremo que racionaliza las solicitudes HTTP a las soluciones de Adobe. Antes, Visitor.js enviaba una llamada de bloqueo al servicio de ID de visitante y, a continuación, AT.js enviaba una llamada a Adobe Target, DIL.js enviaba una llamada a Adobe Audience Manager y, finalmente, AppMeasurement.js enviaba una llamada a Adobe Analytics. Esta nueva biblioteca y punto final puede recuperar un ID, recuperar una experiencia de Target, enviar datos a Audience Manager y pasar los datos a Adobe Experience Platform en una sola llamada.