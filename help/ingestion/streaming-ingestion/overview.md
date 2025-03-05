---
keywords: Experience Platform;inicio;temas populares;ingesta de datos;ingesta de datos;transmisión;información general;transmisión de datos;latencia;transmisión de datos;
solution: Experience Platform
title: Resumen de ingesta de streaming
description: La introducción por transmisión para Adobe Experience Platform proporciona a los usuarios un método para enviar datos desde dispositivos del cliente y del lado del servidor a Experience Platform en tiempo real.
exl-id: 851f15fd-7ac5-4a9f-934d-6b907057da87
source-git-commit: 9b2d0c8fad1ed328725129664be94cf1800f6631
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 2%

---

# Resumen de ingesta de streaming

La transmisión por secuencias de ingesta para Adobe Experience Platform proporciona a los usuarios un método para enviar datos desde dispositivos del cliente y del lado del servidor a [!DNL Experience Platform] en tiempo real.

## ¿Qué puede hacer con la ingesta de transmisión?

Adobe Experience Platform le permite impulsar experiencias coordinadas, coherentes y relevantes generando un [!DNL Real-Time Customer Profile] para cada uno de sus clientes individuales. La transmisión por secuencias de ingesta desempeña un papel clave en la creación de estos perfiles al permitirle entregar los datos de [!DNL Profile] en [!DNL Data Lake] con la menor latencia posible.

El siguiente vídeo está diseñado para ayudarle a comprender la ingesta de transmisión y describe los conceptos anteriores.

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### Registros de perfil de flujo y [!DNL ExperienceEvents]

Con la ingesta por transmisión, los usuarios pueden transmitir registros de perfil y de [!DNL ExperienceEvents] a [!DNL Platform] en segundos para ayudar a impulsar la personalización en tiempo real. Todos los datos enviados a las API de ingesta de transmisión se mantienen automáticamente en [!DNL Data Lake].

Lea [crear una guía de conexión de flujo continuo](../tutorials/create-streaming-connection.md) para obtener más información.

### Transmitir a conjuntos de datos

Una vez que sepa que los datos están limpios, puede habilitar los conjuntos de datos para [!DNL Real-Time Customer Profile] y [!DNL Identity Service].

Para obtener más información sobre cómo habilitar un conjunto de datos para [!DNL Profile] y [!DNL Identity Service], lea la guía [configurar un conjunto de datos](../../profile/tutorials/dataset-configuration.md).

## ¿Cuál es la latencia esperada para la ingesta de transmisión en Experience Platform?

>[!IMPORTANT]
>
>Las protecciones para la ingesta de transmisión se calculan en el nivel de organización y no en el de zona protegida. Esto significa que el uso de datos por zona protegida está enlazado al derecho de uso de licencias total que corresponde con toda la organización. Además, el uso de datos en entornos limitados de desarrollo está limitado al 10 % del total de perfiles. Para obtener más información acerca del derecho de uso de licencias, lea la [guía de prácticas recomendadas de administración de datos](../../landing/license-usage-and-guardrails/data-management-best-practices.md).

| Destino | Latencia esperada |
| --------- | ---------------- |
| Perfil del cliente en tiempo real | &lt; 15 minutos en el percentil 95 |
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

Puede utilizar la extensión de Adobe Experience Platform para crear una nueva conexión de flujo continuo. La extensión [!DNL Experience Platform] proporciona acciones para enviar señalizaciones con formato [!DNL Experience Data Model] (XDM) para la ingesta en tiempo real a [!DNL Experience Platform]. Visite la documentación de [Experience Platform Extension](../../tags/extensions/client/web-sdk/overview.md) para obtener más información.
