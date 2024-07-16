---
keywords: Experience Platform;inicio;temas populares;kafka;conector kafka;Kafka;
solution: Experience Platform
title: Conector Kafka
description: El conector de flujo para Adobe Experience Platform se basa en Apache Kafka Connect. Esta biblioteca se puede utilizar para transmitir eventos JSON desde temas de Kafka en su centro de datos directamente al Experience Platform en tiempo real.
exl-id: 062963e5-c727-4c2c-97db-8a9a5a7d903c
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---

# Conector [!DNL Kafka] para Adobe Experience Platform

El conector de flujo para Adobe Experience Platform se basa en [!DNL Apache Kafka Connect]. Esta biblioteca se puede usar para transmitir eventos JSON de [!DNL Kafka] temas en su centro de datos directamente a [!DNL Experience Platform] en tiempo real.

El conector de flujo es un conector de receptor (unidireccional) que entrega datos de [!DNL Kafka] temas a un extremo registrado en [!DNL Experience Platform]. Para utilizar este conector, debe descargar la biblioteca, agregarla a la implementación existente de [!DNL Kafka] y configurar los temas de [!DNL Kafka] en la dirección URL HTTP de flujo de Adobe. Se requiere código adicional **no**. El conector admite las siguientes funciones:

- Recopilación autenticada de datos
- Lotes de mensajes para reducir las llamadas de red y aumentar el rendimiento

Para obtener más información sobre el conector [!DNL Kafka], incluidas las instrucciones sobre cómo configurarlo, lea la [guía de introducción](https://github.com/adobe/experience-platform-streaming-connect). Para ver un flujo de trabajo más detallado, lea la [guía para desarrolladores](https://www.adobe.com/go/kafka-connector-developer-guide).
