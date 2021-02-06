---
keywords: Experience Platform;inicio;temas populares;kafka;conector kafka;Kafka;
solution: Experience Platform
title: Conector Kafka
topic: overview
description: El conector de flujo para Adobe Experience Platform se basa en Apache Kafka Connect. Esta biblioteca se puede utilizar para transmitir eventos JSON de temas de Kafka en el centro de datos directamente al Experience Platform en tiempo real.
translation-type: tm+mt
source-git-commit: 089a4d517476b614521d1db4718966e3ebb13064
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# [!DNL Kafka] conector para Adobe Experience Platform

El conector de flujo para Adobe Experience Platform se basa en [!DNL Apache Kafka Connect]. Esta biblioteca se puede utilizar para transmitir eventos JSON de [!DNL Kafka] temas del centro de datos directamente a [!DNL Experience Platform] en tiempo real.

El conector de flujo es un conector de receptor (unidireccional) que envía datos de [!DNL Kafka] temas a un punto final registrado en [!DNL Experience Platform]. Para utilizar este conector, debe descargar la biblioteca, agregarla a la implementación [!DNL Kafka] existente y configurar los temas [!DNL Kafka] en la dirección URL HTTP de flujo de Adobe. Se requiere código adicional **no**. El conector admite las siguientes funciones:

- Recopilación autenticada de datos
- Agrupación de mensajes para reducir las llamadas de red y aumentar el rendimiento

Para obtener más información sobre el conector [!DNL Kafka], incluidas instrucciones sobre cómo configurar el conector, lea la [guía de introducción](https://github.com/adobe/experience-platform-streaming-connect). Para obtener un flujo de trabajo más detallado, lea la [guía para desarrolladores](https://www.adobe.com/go/kafka-connector-developer-guide).