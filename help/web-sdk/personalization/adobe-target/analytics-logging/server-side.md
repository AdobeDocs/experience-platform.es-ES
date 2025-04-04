---
title: Registro del lado del servidor para datos de A4T en Experience Platform Web SDK
description: Obtenga información sobre cómo habilitar el registro en el lado del servidor para Adobe Analytics for Target (A4T) mediante Experience Platform Web SDK.
seo-title: Server-side logging for A4T data in Experience Platform Web SDK
seo-description: Learn how to enable server-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: a4t;target;web;sdk;platform;registro;
exl-id: 26c25f58-e43c-4147-8595-69ea85af561f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 1%

---

# Registro del lado del servidor para datos de A4T en Experience Platform Web SDK

Adobe Experience Platform Web SDK le permite implementar la funcionalidad de Adobe Analytics for Target (A4T) en Experience Platform Edge Network. Cuando el registro del lado del servidor está habilitado, todas las visitas de Analytics enviadas a través de Edge Network se aumentan con detalles de Target en el lado del servidor, sin tener que pasar por el proceso de vinculación de visitas.

El registro del lado del servidor para Analytics está habilitado cuando Analytics está habilitado en la configuración del flujo de datos:

![Configuración de secuencia de datos de Analytics habilitada](../assets/enable-analytics-datastream.png)

El diagrama siguiente muestra cómo fluyen los datos a través del sistema cuando el registro de Analytics en el lado del servidor está habilitado:

![Flujo de registro del lado del servidor](../assets/analytics-server-side-logging.png)

## Pasos siguientes

En esta guía se describe el registro en el lado del servidor para datos de A4T en Web SDK. Consulte la guía de [registro en el lado del cliente](./client-side.md) para obtener más información sobre cómo administrar los datos de A4T en el lado del cliente.
