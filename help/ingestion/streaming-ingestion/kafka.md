---
keywords: Experience Platform;home;popular topics;kafka;kafka connector;Kafka;
solution: Experience Platform
title: Conector Kafka
topic: overview
translation-type: tm+mt
source-git-commit: c04fb056d4564e53f192e0734a700a13820f5ba7
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 0%

---


# [!DNL Kafka] conector para Adobe Experience Platform

El conector de flujo para Adobe Experience Platform se basa en [!DNL Apache Kafka Connect]. Esta biblioteca se puede utilizar para transmitir eventos JSON de [!DNL Kafka] temas del centro de datos directamente a [!DNL Experience Platform] en tiempo real.

El conector de flujo es un conector de receptor (unidireccional) que proporciona datos de [!DNL Kafka] temas a un punto final registrado en [!DNL Experience Platform]. Para utilizar este conector, debe descargar la biblioteca, agregarla a la implementación existente [!DNL Kafka] y configurar los [!DNL Kafka] temas en la URL HTTP de flujo de Adobe. El código adicional **no es** obligatorio. El conector admite las siguientes funciones:

- Recopilación autenticada de datos
- Agrupación de mensajes para reducir las llamadas de red y aumentar el rendimiento

Para obtener más información sobre el [!DNL Kafka] conector, incluidas instrucciones sobre cómo configurar el conector, lea la guía de [introducción](https://github.com/adobe/experience-platform-streaming-connect). Para obtener un flujo de trabajo más detallado, consulte la guía para [desarrolladores](https://github.com/adobe/experience-platform-streaming-connect/blob/master/DEVELOPER_GUIDE.md).