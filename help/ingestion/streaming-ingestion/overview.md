---
keywords: Experience Platform;inicio;temas populares;consumo de datos;datos ingestados;flujo continuo;descripción general;ingesta de flujo;latencia;latencia de flujo continuo;
solution: Experience Platform
title: Información general sobre la ingesta de flujos
topic: overview
description: La introducción por transmisión para Adobe Experience Platform proporciona a los usuarios un método para enviar datos desde dispositivos de cliente y del lado del servidor a Experience Platform en tiempo real.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 3%

---


# Información general sobre la ingesta de flujos

La introducción por transmisión para Adobe Experience Platform proporciona a los usuarios un método para enviar datos desde dispositivos de cliente y del lado del servidor a [!DNL Experience Platform] en tiempo real.

## ¿Qué se puede hacer con la transmisión por secuencias?

Adobe Experience Platform le permite impulsar experiencias coordinadas, coherentes y relevantes generando un [!DNL Real-time Customer Profile] para cada uno de sus clientes individuales. La introducción por transmisión desempeña un papel clave en la creación de estos perfiles, ya que permite enviar datos [!DNL Profile] a [!DNL Data Lake] con la menor latencia posible.

El siguiente vídeo está diseñado para ayudarle a comprender la ingesta de transmisión por secuencias y describe los conceptos anteriores.

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### Registros de perfil de flujo y [!DNL ExperienceEvents]

Con la ingesta de flujo continuo, los usuarios pueden transmitir registros de perfil y [!DNL ExperienceEvents] a [!DNL Platform] en segundos para ayudar a impulsar la personalización en tiempo real. Todos los datos enviados a las API de ingesta de transmisión se mantienen automáticamente en el [!DNL Data Lake].

Lea la [guía de creación de conexión de flujo continuo](../tutorials/create-streaming-connection.md) para obtener más información.

### Transmitir a conjuntos de datos

Una vez que esté seguro de que sus datos están limpios, puede habilitar sus conjuntos de datos para [!DNL Real-time Customer Profile] y [!DNL Identity Service].

Para obtener más información sobre cómo habilitar un conjunto de datos para [!DNL Profile] y [!DNL Identity Service], lea la [configuración de una guía de conjunto de datos](../../profile/tutorials/dataset-configuration.md).

## ¿Cuál es la latencia esperada para la transmisión por secuencias en [!DNL Platform]?

| Destino | Latencia esperada |
| --------- | ---------------- |
| Perfil del cliente en tiempo real | &lt; 1=&quot;&quot; minute=&quot;&quot;> |
| Lago de datos | &lt; 60 minutos |

## Extensión de Adobe Experience Platform

Puede utilizar la extensión de Adobe Experience Platform para crear una nueva conexión de flujo continuo. La extensión [!DNL Experience Platform] proporciona acciones para enviar señalizaciones con formato [!DNL Experience Data Model] (XDM) para la ingesta en tiempo real a [!DNL Experience Platform]. Visite la documentación de [Experience Platform Extension](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/adobe-experience-platform-extension.html) para obtener más información.