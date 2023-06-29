---
keywords: Experience Platform;inicio;temas populares;ingesta de datos;ingesta de datos;flujo continuo;información general;flujo continuo;ingesta;latencia;flujo continuo;
solution: Experience Platform
title: Resumen de ingesta de streaming
description: La introducción por transmisión para Adobe Experience Platform proporciona a los usuarios un método para enviar datos desde dispositivos del cliente y del lado del servidor al Experience Platform en tiempo real.
exl-id: 851f15fd-7ac5-4a9f-934d-6b907057da87
source-git-commit: 12bd4c6c1993afc438b75a3e5163ebe2fe8a8dd0
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 4%

---

# Información general sobre la ingesta de flujo continuo

La introducción por transmisión para Adobe Experience Platform proporciona a los usuarios un método para enviar datos desde dispositivos del cliente y del lado del servidor a [!DNL Experience Platform] en tiempo real.

## ¿Qué puede hacer con la ingesta de transmisión?

Adobe Experience Platform le permite impulsar experiencias coordinadas, coherentes y relevantes mediante la generación de una [!DNL Real-Time Customer Profile] para cada uno de sus clientes individuales. La introducción por transmisión juega un papel clave en la creación de estos perfiles al permitirle entregar [!DNL Profile] datos en la [!DNL Data Lake] con la menor latencia posible.

El siguiente vídeo está diseñado para ayudarle a comprender la ingesta de transmisión y describe los conceptos anteriores.

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### Transmitir registros de perfil y [!DNL ExperienceEvents]

Con la ingesta de transmisión, los usuarios pueden transmitir registros de perfil y [!DNL ExperienceEvents] hasta [!DNL Platform] en segundos para impulsar la personalización en tiempo real. Todos los datos enviados a las API de ingesta de transmisión persisten automáticamente en [!DNL Data Lake].

Lea el [crear una guía de conexión de flujo continuo](../tutorials/create-streaming-connection.md) para obtener más información.

### Transmitir a conjuntos de datos

Una vez que esté seguro de que los datos están limpios, puede habilitar los conjuntos de datos para [!DNL Real-Time Customer Profile] y [!DNL Identity Service].

Para obtener más información sobre la activación de un conjunto de datos para [!DNL Profile] y [!DNL Identity Service], lea la [configuración de una guía de conjuntos de datos](../../profile/tutorials/dataset-configuration.md).

## ¿Cuál es la latencia esperada para la transmisión de la ingesta en [!DNL Platform]?

| Destino | Latencia esperada |
| --------- | ---------------- |
| Perfil del cliente en tiempo real | &lt; 1 minuto |
| Lago de datos | &lt; 60 minutos |

## Solicitud de guía por segundos (RPS) sobre la ingesta de transmisión

La tabla siguiente muestra instrucciones sobre los límites de solicitudes por segundos para la ingesta de transmisión.

| Límite de RPS | Notas |
| --- | --- |
| 1000 solicitudes por segundo | Pueden contener varios mensajes al utilizar `/collection/batch` punto final. |
| 10000 mensajes individuales por segundo | Los mensajes se pueden agrupar en menos solicitudes reales cuando se utiliza el `/collection/batch` punto final. |

>[!IMPORTANT]
>
>El límite impuesto se convierte en **60 solicitudes por minuto** cuando se utiliza la validación sincrónica, ya que está pensada para fines de depuración.

## Extensión de Adobe Experience Platform

Puede utilizar la extensión de Adobe Experience Platform para crear una nueva conexión de flujo continuo. El [!DNL Experience Platform] La extensión de proporciona acciones para enviar señalizaciones con formato [!DNL Experience Data Model] (XDM) para la ingesta en tiempo real en [!DNL Experience Platform]. Visite la [Extensión de Experience Platform](../../tags/extensions/client/web-sdk/overview.md) para obtener más información.
