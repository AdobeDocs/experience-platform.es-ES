---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Introducción a la ingesta de flujo de Adobes Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: 3f1c3c77a0755a3e305da0fb8a234be0f0ee1863
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 3%

---


# Introducción a la ingesta de flujo continuo

La ingestión por flujo continuo para Adobe Experience Platform proporciona a los usuarios un método para enviar datos desde dispositivos cliente y servidor al Experience Platform en tiempo real.

## ¿Qué se puede hacer con la ingestión por streaming?

Adobe Experience Platform le permite impulsar experiencias coordinadas, coherentes y relevantes mediante la generación de un Perfil de cliente en tiempo real para cada uno de sus clientes individuales. La transmisión por secuencias de la ingestión desempeña un papel clave en la creación de estos perfiles, ya que le permite entregar datos de Perfil en el Data Lake con la menor latencia posible.

El siguiente vídeo está diseñado para ayudarle a comprender mejor la transmisión por secuencias de ingestión y describe los conceptos anteriores.

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### Registros de flujo de perfil y ExperienceEvents

Con la transmisión por flujo continuo, los usuarios pueden transmitir registros de perfiles y ExperienceEvents a Platform en segundos para ayudar a impulsar la personalización en tiempo real. Todos los datos enviados a las API de inserción de flujo continuo se conservan automáticamente en el lago de datos.

Para obtener más información, lea la guía [](../tutorials/create-streaming-connection.md) crear una conexión de flujo continuo.

### Flujo a conjuntos de datos

Una vez que esté seguro de que los datos están limpios, puede habilitar los conjuntos de datos para el servicio de Perfil e identidad del cliente en tiempo real.

Para obtener más información sobre cómo habilitar un conjunto de datos para Perfil y servicio de identidad, lea la [configuración de una guía](../../profile/tutorials/dataset-configuration.md)de conjuntos de datos.

## ¿Cuál es la latencia esperada para transmitir la ingestión en Platform?

| Destino | Latencia esperada |
| --------- | ---------------- |
| Perfil del cliente en tiempo real | &lt; 1 minuto |
| Lago de datos | &lt; 60 minutos |

## Extensión de Adobe Experience Platform

Puede utilizar la extensión de Adobe Experience Platform para crear una nueva conexión de flujo continuo. La extensión Experience Platform proporciona acciones para enviar señalizaciones formateadas en el Modelo de datos de experiencia (XDM) para la ingestión en tiempo real al Experience Platform. Visite la documentación de [Experience Platform Extension](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/adobe-experience-platform-extension.html) para obtener más información.