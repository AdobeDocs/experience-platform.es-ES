---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Conector Kafka
topic: overview
translation-type: tm+mt
source-git-commit: f80b2e1d787d1f8d9fe8ac306422aa7744a69cd3

---


# Conector Kafka para la plataforma Adobe Experience

El conector de flujo de Adobe Experience Platform se basa en Apache Kafka Connect. Esta biblioteca se puede utilizar para transmitir eventos JSON de temas de Kafka en su centro de datos directamente a la plataforma de experiencias en tiempo real.

El conector de flujo es un conector de receptor (unidireccional) que proporciona datos de temas de Kafka a un punto final registrado en la plataforma de experiencia. Para utilizar este conector, debe descargar la biblioteca, agregarla a la implementación de Kafka existente y configurar los temas de Kafka en la URL HTTP de flujo de Adobe. El código adicional **no es** obligatorio. El conector admite las siguientes funciones:

- Recopilación autenticada de datos
- Agrupación de mensajes para reducir las llamadas de red y aumentar el rendimiento

Para obtener más información sobre el conector Kafka, incluidas instrucciones sobre cómo configurar el conector, lea la guía de [introducción](https://github.com/adobe/experience-platform-streaming-connect). Para obtener un flujo de trabajo más detallado, consulte la guía para [desarrolladores](https://github.com/adobe/experience-platform-streaming-connect/blob/master/DEVELOPER_GUIDE.md).