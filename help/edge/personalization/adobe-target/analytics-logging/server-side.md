---
title: Registro del lado del servidor para datos de A4T en el SDK web de Platform
description: Obtenga información sobre cómo habilitar el registro en el lado del servidor para Adobe Analytics for Target (A4T) mediante el SDK web de Experience Platform.
seo-title: Server-side logging for A4T data in Platform Web SDK
seo-description: Learn how to enable server-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: a4t;target;web;sdk;platform;registro;
exl-id: 26c25f58-e43c-4147-8595-69ea85af561f
source-git-commit: 38d54b2c793c9dcb1a45ec4acbb9016d1e927d23
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 1%

---

# Registro del lado del servidor para datos de A4T en el SDK web de Platform

El SDK web de Adobe Experience Platform le permite implementar la funcionalidad de Adobe Analytics for Target (A4T) en Platform Edge Network. Cuando el registro del lado del servidor está habilitado, todas las visitas de Analytics enviadas a través de la red perimetral se aumentan con detalles de Target en el lado del servidor, sin tener que pasar por el proceso de vinculación de visitas.

El registro del lado del servidor para Analytics está habilitado cuando Analytics está habilitado en la configuración del flujo de datos:

![Configuración del flujo de datos de Analytics habilitada](../assets/enable-analytics-datastream.png)

El diagrama siguiente muestra cómo fluyen los datos a través del sistema cuando el registro de Analytics en el lado del servidor está habilitado:

![Flujo de registro del lado del servidor](../assets/analytics-server-side-logging.png)

## Pasos siguientes

En esta guía se describe el registro en el lado del servidor para datos de A4T en el SDK web. Consulte la guía de [registro en el lado del cliente](./client-side.md) para obtener más información sobre cómo gestionar los datos de A4T en el lado del cliente.
