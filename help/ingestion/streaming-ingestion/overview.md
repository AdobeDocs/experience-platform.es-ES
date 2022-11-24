---
keywords: Experience Platform;inicio;temas populares;consumo de datos;datos ingestados;flujo continuo;descripción general;ingesta de transmisión;latencia;latencia de transmisión por secuencias;
solution: Experience Platform
title: Información general sobre la ingesta de flujos
topic-legacy: overview
description: La introducción por transmisión para Adobe Experience Platform proporciona a los usuarios un método para enviar datos desde dispositivos de cliente y del lado del servidor al Experience Platform en tiempo real.
exl-id: 851f15fd-7ac5-4a9f-934d-6b907057da87
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 3%

---

# Información general sobre la ingesta de flujos

La introducción por transmisión para Adobe Experience Platform proporciona a los usuarios un método para enviar datos desde dispositivos del lado del cliente y del servidor a [!DNL Experience Platform] en tiempo real.

## ¿Qué se puede hacer con la transmisión por secuencias?

Adobe Experience Platform le permite impulsar experiencias coordinadas, coherentes y relevantes mediante la generación de un [!DNL Real-time Customer Profile] para cada uno de sus clientes individuales. La introducción por transmisión desempeña un papel clave en la creación de estos perfiles, ya que le permite entregar [!DNL Profile] en [!DNL Data Lake] con la menor latencia posible.

El siguiente vídeo está diseñado para ayudarle a comprender la ingesta de transmisión por secuencias y describe los conceptos anteriores.

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### Registros de perfil de flujo y [!DNL ExperienceEvents]

Con la ingesta de flujo continuo, los usuarios pueden transmitir registros de perfil y [!DNL ExperienceEvents] a [!DNL Platform] en segundos para facilitar la personalización en tiempo real. Todos los datos enviados a las API de ingesta de flujo continuo se mantienen automáticamente en el [!DNL Data Lake].

Lea el [crear una guía de conexión de flujo continuo](../tutorials/create-streaming-connection.md) para obtener más información.

### Transmitir a conjuntos de datos

Una vez que esté seguro de que sus datos están limpios, puede habilitar sus conjuntos de datos para [!DNL Real-time Customer Profile] y [!DNL Identity Service].

Para obtener más información sobre cómo habilitar un conjunto de datos para [!DNL Profile] y [!DNL Identity Service], lea la [configuración de una guía de conjuntos de datos](../../profile/tutorials/dataset-configuration.md).

## ¿Cuál es la latencia esperada para la transmisión por secuencias de ingesta en [!DNL Platform]?

| Destino | Latencia esperada |
| --------- | ---------------- |
| Perfil del cliente en tiempo real | &lt; 1 minuto |
| Lago de datos | &lt; 60 minutos |

## Guía de solicitud por segundos (RPS) sobre la ingesta de transmisión

La siguiente tabla muestra instrucciones sobre los límites de solicitudes por segundos para la ingesta de flujo continuo.

| Límite de RPS | Notas |
| --- | --- |
| 1000 solicitudes por segundo | Pueden contener varios mensajes al usar `/collection/batch` punto final. |
| 10000 mensajes individuales por segundo | Los mensajes se pueden agrupar en menos solicitudes reales al usar la variable `/collection/batch` punto final. |

>[!IMPORTANT]
>
>El límite forzado se convierte en **60 solicitudes por minuto** cuando se utiliza la validación sincrónica, ya que está pensado para fines de depuración.

## Extensión de Adobe Experience Platform

Puede utilizar la extensión de Adobe Experience Platform para crear una nueva conexión de flujo continuo. La variable [!DNL Experience Platform] extensión proporciona acciones para enviar señalizaciones con formato [!DNL Experience Data Model] (XDM) para la ingesta en tiempo real a [!DNL Experience Platform]. Visite la [Extensión de Experience Platform](../../tags/extensions/client/sdk/overview.md) documentación para obtener más información.
