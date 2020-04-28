---
title: Ayuda del SDK web de Adobe Experience Platform
seo-title: Ayuda del SDK web de Adobe Experience Platform
description: Descubra qué es el SDK web de Adobe Experience Platform y cómo se puede utilizar.
seo-description: permita a los clientes de Adobe Experience Cloud interactuar con los distintos servicios de Experience Cloud.
translation-type: tm+mt
source-git-commit: 5027ae2cd083631d7122346796ef93572c129d3f

---


# (Beta) ¿Qué es el SDK web de Adobe Experience Platform?

>[!IMPORTANT]
>
>El SDK web de la plataforma de experiencia de Adobe se encuentra en fase beta y no está disponible para todos los usuarios. La documentación y las funciones están sujetas a cambios.

Adobe Experience Platform Web SDK es una biblioteca JavaScript del lado del cliente que permite a los clientes de Adobe Experience Cloud interactuar con los distintos servicios de Experience Cloud a través de Adobe Experience Platform Edge Network.

## SDK reemplazados por el SDK web de Adobe Experience Platform

El SDK web de la plataforma Adobe Experience sustituye a los siguientes SDK:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

Esto no es sólo un envoltorio en torno a las bibliotecas existentes. Es una reescritura completa. Su propósito es acabar con los desafíos con la activación de etiquetas en el orden correcto, la incoherencia con los desafíos de versiones de la biblioteca y una mejor administración de dependencias. Es una nueva forma de implementar Experience Cloud.

Además de una nueva biblioteca, existe un nuevo extremo que racionaliza las solicitudes HTTP a las soluciones de Adobe. Antes, Visitante.js enviaba una llamada de bloqueo al servicio de ID de visitante y, a continuación, AT.js enviaba una llamada a Adobe Destinatario, DIL.js enviaba una llamada a Adobe Audiencia Manager y, finalmente, AppMeasurement.js enviaba una llamada a Adobe Analytics. Esta nueva biblioteca y punto final puede recuperar un ID, recuperar una experiencia de Destinatario, enviar datos al Administrador de Audiencias y pasar los datos a Adobe Experience Platform en una sola llamada.