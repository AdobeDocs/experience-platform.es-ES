---
keywords: Experience Platform;inicio;temas populares;kafka;conector kafka;Kafka;
solution: Experience Platform
title: Conector Kafka
topic-legacy: overview
description: El conector de flujo para Adobe Experience Platform se basa en Apache Kafka Connect. Esta biblioteca se puede utilizar para transmitir eventos JSON de temas de Kafka en su centro de datos directamente al Experience Platform en tiempo real.
exl-id: 062963e5-c727-4c2c-97db-8a9a5a7d903c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# [!DNL Kafka] conector para Adobe Experience Platform

El conector de flujo para Adobe Experience Platform se basa en [!DNL Apache Kafka Connect]. Esta biblioteca se puede utilizar para transmitir eventos JSON desde [!DNL Kafka] temas en su centro de datos directamente a [!DNL Experience Platform] en tiempo real.

El conector de flujo es un conector de disipador (unidireccional) que envía datos de los temas [!DNL Kafka] a un punto final registrado en [!DNL Experience Platform]. Para utilizar este conector, debe descargar la biblioteca, agregarla a la implementación [!DNL Kafka] existente y configurar los temas [!DNL Kafka] en la URL HTTP de flujo de Adobe. Se requiere código adicional **no**. El conector admite las siguientes funciones:

- Recopilación autenticada de datos
- Agrupación de mensajes para reducir las llamadas de red y aumentar el rendimiento

Para obtener más información sobre el conector [!DNL Kafka], incluidas instrucciones sobre cómo configurar el conector, lea la [guía de introducción](https://github.com/adobe/experience-platform-streaming-connect). Para obtener un flujo de trabajo más detallado, consulte la [guía para desarrolladores](https://www.adobe.com/go/kafka-connector-developer-guide).
