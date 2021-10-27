---
keywords: Experience Platform;inicio;temas populares;kafka;conector kafka;Kafka;
solution: Experience Platform
title: Conector Kafka
topic-legacy: overview
description: El conector de flujo para Adobe Experience Platform se basa en Apache Kafka Connect. Esta biblioteca se puede utilizar para transmitir eventos JSON de temas de Kafka en su centro de datos directamente al Experience Platform en tiempo real.
exl-id: 062963e5-c727-4c2c-97db-8a9a5a7d903c
source-git-commit: 5a3aa74ca7319235c10902422abc0e897ad823b8
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# [!DNL Kafka] conector para Adobe Experience Platform (obsoleto)

>[!IMPORTANT]
>
>El conector Kafka está en desuso. Para crear una conexión de flujo continuo y traer datos a Adobe Experience Platform, consulte el tutorial en [creación de una conexión de flujo continuo de API HTTP](../../sources/connectors/streaming/http.md)

El conector de flujo para Adobe Experience Platform se basa en [!DNL Apache Kafka Connect]. Esta biblioteca puede utilizarse para transmitir eventos JSON desde [!DNL Kafka] temas de su centro de datos directamente a [!DNL Experience Platform] en tiempo real.

El conector de flujo es un conector de disipador (unidireccional) que proporciona datos desde [!DNL Kafka] temas a un punto final registrado en [!DNL Experience Platform]. Para utilizar este conector, debe descargar la biblioteca y agregarla a la [!DNL Kafka] implementación y configure la variable [!DNL Kafka] temas a la URL HTTP de flujo de Adobe. El código adicional es **not** obligatorio. El conector admite las siguientes funciones:

- Recopilación autenticada de datos
- Agrupación de mensajes para reducir las llamadas de red y aumentar el rendimiento

Para obtener más información sobre [!DNL Kafka] conector, incluidas instrucciones sobre cómo configurar el conector, lea la [guía de introducción](https://github.com/adobe/experience-platform-streaming-connect). Para obtener un flujo de trabajo más detallado, lea la [guía para desarrolladores](https://www.adobe.com/go/kafka-connector-developer-guide).
