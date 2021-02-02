---
keywords: Experience Platform;inicio;temas populares;ingestión de datos;datos ingestados;transmisión;información general;transmisión de flujo continuo;latencia;transmisión de latencia;
solution: Experience Platform
title: Introducción a la ingestión de flujo continuo de Adobe Experience Platform
topic: overview
description: La ingestión de flujo continuo para Adobe Experience Platform proporciona a los usuarios un método para enviar datos desde dispositivos cliente y servidor al Experience Platform en tiempo real.
translation-type: tm+mt
source-git-commit: 2dbd92efbd992b70f4f750b09e9d2e0626e71315
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 3%

---


# Introducción a la ingesta de flujo continuo

La ingestión de flujo continuo para Adobe Experience Platform proporciona a los usuarios un método para enviar datos desde dispositivos cliente y servidor a [!DNL Experience Platform] en tiempo real.

## ¿Qué se puede hacer con la ingestión por streaming?

Adobe Experience Platform le permite dirigir experiencias coordinadas, coherentes y relevantes mediante la generación de un [!DNL Real-time Customer Profile] para cada uno de sus clientes individuales. La ingestión por flujo continuo juega un papel clave en la creación de estos perfiles al permitirle entregar [!DNL Profile] datos en [!DNL Data Lake] con la menor latencia posible.

El siguiente vídeo está diseñado para ayudarle a comprender mejor la transmisión por secuencias de ingestión y describe los conceptos anteriores.

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### Registros de perfil de flujo y [!DNL ExperienceEvents]

Con la ingestión de flujo continuo, los usuarios pueden transmitir registros de perfil y [!DNL ExperienceEvents] a [!DNL Platform] en segundos para ayudar a impulsar la personalización en tiempo real. Todos los datos enviados a las API de inserción de flujo continuo se mantienen automáticamente en [!DNL Data Lake].

Para obtener más información, lea la [guía de conexión de flujo](../tutorials/create-streaming-connection.md).

### Flujo a conjuntos de datos

Una vez que esté seguro de que los datos están limpios, puede habilitar los datasets para [!DNL Real-time Customer Profile] y [!DNL Identity Service].

Para obtener más información sobre cómo habilitar un conjunto de datos para [!DNL Profile] y [!DNL Identity Service], lea la [guía de configuración de un conjunto de datos](../../profile/tutorials/dataset-configuration.md).

## ¿Cuál es la latencia esperada para transmitir la ingestión en [!DNL Platform]?

| Destino | Latencia esperada |
| --------- | ---------------- |
| Perfil del cliente en tiempo real | &lt; 1=&quot;&quot; minute=&quot;&quot;> |
| Lago de datos | &lt; 60 minutos |

## Extensión de Adobe Experience Platform

Puede utilizar la extensión de Adobe Experience Platform para crear una nueva conexión de flujo continuo. La extensión [!DNL Experience Platform] proporciona acciones para enviar señalizaciones con formato [!DNL Experience Data Model] (XDM) para la ingestión en tiempo real a [!DNL Experience Platform]. Visite la documentación de [Experience Platform Extension](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/adobe-experience-platform-extension.html) para obtener más información.