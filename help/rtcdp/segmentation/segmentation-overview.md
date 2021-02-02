---
keywords: segmentación; segmentación rtcdp;segmentación de la plataforma de datos del cliente en tiempo real
title: Descripción general del servicio de segmentación
seo-title: Servicio de segmentación en la plataforma de datos del cliente en tiempo real
description: CDP en tiempo real se basa en Adobe Experience Platform y utiliza muchos de los servicios y funcionalidades del Experience Platform. Con el servicio de segmentación, puede proporcionar marketing personalizado dividiendo a los clientes en grupos más pequeños con características similares.
translation-type: tm+mt
source-git-commit: 9f20f8bfeefb5bc427a72a11ac1f01816cdbc4b2
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 0%

---


# [!DNL Segmentation Service] in [!DNL Real-time Customer Data Platform]

[!DNL Real-time Customer Data Platform] (CDP en tiempo real) le permite traer datos de múltiples fuentes para impulsar una experiencia coordinada y consistente para sus clientes. La entrega de campañas de mercadotecnia personalizadas relevantes se puede lograr usando la [!DNL Segmentation Service] parte de Adobe Experience Platform.

CDP en tiempo real se construye sobre Adobe Experience Platform y utiliza muchos de los [!DNL Experience Platform] servicios y funcionalidades. Al utilizar [!DNL Segmentation Service], puede proporcionar mercadotecnia personalizada dividiendo a los clientes en grupos más pequeños con características similares.

## Segmentación

La segmentación es el proceso de definir atributos o comportamientos específicos compartidos por un subconjunto de perfiles de su almacén de perfiles para distinguir un grupo de personas comercializables de su base de clientes. Por ejemplo: en una campaña por correo electrónico llamada &quot;¿Olvidó comprar sus zapatillas?&quot;, puede que desee una audiencia de todos los usuarios que buscaron zapatos deportivos en los últimos 30 días, pero que no completaron una compra. Con diferentes segmentos, puede centrarse en sus distintas audiencias y ofrecer una experiencia de marketing más personalizada.

## [!DNL Segment Builder]

[!DNL Platform] le permite crear segmentos y acceder a ellos fácilmente, así como utilizar diferentes componentes básicos para seguir caracterizándolos. Para obtener más información sobre cómo utilizar el Generador de segmentos, lea la [guía del Generador de segmentos](./segment-builder-guide.md).

## AI del cliente

La API del cliente, incluida con la plataforma de datos del cliente en tiempo real, le proporciona la capacidad para generar predicciones del cliente a nivel individual con explicaciones.

Con la ayuda de factores influyentes, la información sobre el cliente puede indicarle qué es lo que probablemente hará un cliente y por qué. Además, puede beneficiarse de las predicciones y perspectivas de la API del cliente para personalizar las experiencias de los clientes al ofrecer las ofertas y los mensajes más adecuados. La API del cliente puede ayudarle con:

* Proporcionar modelos de propensión del cliente de alta precisión para una segmentación y un objetivo más sólidos.
* Comprender los factores influyentes y la probabilidad que hay detrás de ciertos comportamientos del cliente.
* Proporciona opciones personalizables para los casos de uso y los datos únicos de su compañía.
* Mejora del Perfil de los clientes en tiempo real con puntuaciones de tendencia de los clientes, como la conversión y la reproducción.
* Mejora de los perfiles de los clientes con factores influyentes para las puntuaciones de tendencia.
* Creación de segmentos de clientes en función de factores influyentes y puntuaciones de tendencia.

La API del cliente se encuentra en la ficha **[!UICONTROL Servicios]** en **[!UICONTROL Servicios de Adobe]**.

![Ubicación de AI del cliente](../assets/overview/rtcdp-customer-ai.png)

### Introducción a la API del cliente

Para comenzar con la API del cliente, debe seguir el [tutorial de preparación de datos](../../intelligent-services/data-preparation.md) y configurar el esquema de entrada en función del caso de uso. A continuación, deberá [configurar una instancia de AI de cliente](../../intelligent-services/customer-ai/user-guide/configure.md). Después de configurar una instancia, se genera un modelo en el que puede [vista de sus perspectivas y puntuaciones](../../intelligent-services/customer-ai/user-guide/discover-insights.md). Con los datos generados a partir del modelo, puede crear segmentos para la activación basada en datos.

Para obtener más información sobre la IA del cliente, visite la [información general de la API del cliente](../../intelligent-services/customer-ai/overview.md) para obtener inicio. Además, el siguiente vídeo muestra cómo la API del cliente enriquece los perfiles de los clientes con las propensidades basadas en AI y potencia la segmentación de clientes y los esfuerzos de determinación de objetivos.

>[!VIDEO](https://video.tv.adobe.com/v/40374/?quality=12&learn=on)


## Pasos siguientes

Después de leer esta descripción general, ahora debe comprender cómo CDP en tiempo real utiliza [!DNL Segmentation Service] para mejorar la personalización y personalización de las campañas de mercadotecnia. Para obtener más información acerca de [!DNL Segmentation Service], lea la [documentación de segmentación](../../segmentation/home.md).
