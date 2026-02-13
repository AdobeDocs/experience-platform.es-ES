---
keywords: Experience Platform;inicio;temas populares;ingesta de datos;ingesta de datos;transmisión;información general;transmisión de datos;latencia;transmisión de datos;
solution: Experience Platform
title: Resumen de ingesta de streaming
description: Obtenga información acerca de la ingesta de transmisión en Adobe Experience Platform.
exl-id: 851f15fd-7ac5-4a9f-934d-6b907057da87
source-git-commit: 568208c9b2cb774bbbeed74ae2d456c87e99bca9
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 3%

---

# Resumen de ingesta de streaming

La introducción por transmisión para Adobe Experience Platform proporciona a los usuarios un método para enviar datos desde dispositivos del cliente y del lado del servidor a Experience Platform en tiempo real.

## ¿Qué puede hacer con la ingesta de transmisión?

Adobe Experience Platform le permite impulsar experiencias coordinadas, coherentes y relevantes mediante la generación de un perfil del cliente en tiempo real para cada uno de sus clientes individuales. La introducción por transmisión juega un papel clave en la creación de estos perfiles, ya que permite entregar datos de perfil al lago de datos con la menor latencia posible.

El siguiente vídeo está diseñado para ayudarle a comprender la ingesta de transmisión y describe los conceptos anteriores.

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### Registros de perfil de flujo y [!DNL ExperienceEvents]

Con la ingesta por transmisión, los usuarios pueden transmitir los registros de perfil y [!DNL ExperienceEvents] a Experience Platform en segundos para ayudar a impulsar la personalización en tiempo real. Todos los datos enviados a las API de ingesta de transmisión persisten automáticamente en el lago de datos.

Lea [crear una guía de conexión de flujo continuo](../tutorials/create-streaming-connection.md) para obtener más información.

### Transmitir a conjuntos de datos

Una vez que esté seguro de que los datos están limpios, puede habilitar los conjuntos de datos para el Perfil del cliente en tiempo real y [!DNL Identity Service].

Para obtener más información sobre cómo habilitar un conjunto de datos para el perfil y [!DNL Identity Service], lea la [guía de configuración de un conjunto de datos](/help/profile/tutorials/dataset-configuration.md).

## ¿Cuál es la latencia esperada para la ingesta de transmisión en Experience Platform?

>[!IMPORTANT]
>
>Las protecciones para la ingesta de transmisión están enlazadas al derecho de uso de licencia total que corresponde a toda la organización. Además, el uso de datos en entornos limitados de desarrollo está limitado al 10 % del total de perfiles. Para obtener más información acerca del derecho de uso de licencias, lea la [guía de prácticas recomendadas de administración de datos](/help/landing/license-usage-and-guardrails/data-management-best-practices.md). Para obtener información sobre cómo establecer límites en el rendimiento de streaming, lee [Descripción general de la capacidad](../../landing/license-usage-and-guardrails/capacity.md).

| Destino | Latencia esperada |
| --------- | ---------------- |
| Perfil del cliente en tiempo real | <ul><li>&lt; 15 minutos en el percentil 95 para la ingesta de datos B2C.</li><li>&lt; 30 minutos en el percentil 95 para la ingesta de datos B2B.</li></ul> |
| Lago de datos | &lt; 60 minutos |

## Solicitud de guía por segundos (RPS) sobre la ingesta de transmisión

La tabla siguiente muestra instrucciones sobre los límites de solicitudes por segundos para la ingesta de transmisión.

| Límite de RPS | Notas |
| --- | --- |
| 1000 solicitudes por segundo | Pueden contener varios mensajes al usar el extremo `/collection/batch`. |
| 10000 mensajes individuales por segundo | Los mensajes se pueden agrupar en menos solicitudes reales cuando se usa el extremo `/collection/`. |

>[!IMPORTANT]
>
>El límite impuesto se convierte en **60 solicitudes por minuto** al utilizar la validación sincrónica, ya que está pensada para fines de depuración.

## Extensión de Adobe Experience Platform

Puede utilizar la extensión de Adobe Experience Platform para crear una nueva conexión de flujo continuo. La extensión [!DNL Experience Platform] proporciona acciones para enviar señalizaciones con formato [!DNL Experience Data Model] (XDM) para la ingesta en tiempo real a [!DNL Experience Platform]. Visite la documentación de [Experience Platform Extension](/help/tags/extensions/client/web-sdk/overview.md) para obtener más información.
