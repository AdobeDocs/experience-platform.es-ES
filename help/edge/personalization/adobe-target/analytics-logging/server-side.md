---
title: Registro del lado del servidor para datos de A4T en Platform Web SDK
description: Obtenga información sobre cómo habilitar el registro en el lado del servidor para Adobe Analytics for Target (A4T) mediante el SDK web de Experience Platform.
seo-title: Server-side logging for A4T data in Platform Web SDK
seo-description: Learn how to enable server-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: a4t;target;web;sdk;plataforma;registro;
source-git-commit: a2214465001f90d19d88c0622c154e7a4ae3bb03
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 1%

---

# Registro del lado del servidor para datos de A4T en Platform Web SDK

El SDK web de Adobe Experience Platform le permite implementar la funcionalidad Adobe Analytics for Target (A4T) en Platform Edge Network. Cuando el registro en el servidor está habilitado, todas las visitas de Analytics enviadas a través de la red perimetral se suman con los detalles de Target en el servidor, sin tener que pasar por el proceso de vinculación de visitas.

El registro del lado del servidor para Analytics se habilita cuando Analytics está habilitado en la configuración del conjunto de datos:

![Configuración del conjunto de datos de Analytics habilitada](../assets/enable-analytics-datastream.png)

El diagrama siguiente muestra cómo fluyen los datos a través del sistema cuando está habilitado el registro de Analytics en el servidor:

![Flujo de registro del lado del servidor](../assets/analytics-server-side-logging.png)

## Pasos siguientes

Esta guía abarcaba el registro en el lado del servidor de datos de A4T en el SDK web. Consulte la guía de [registro del lado del cliente](./client-side.md) para obtener más información sobre cómo gestionar los datos de A4T en el lado del cliente.
