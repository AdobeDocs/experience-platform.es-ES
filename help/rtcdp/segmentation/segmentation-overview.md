---
keywords: segmentación; segmentación rtcdp;segmentación de la plataforma de datos del cliente en tiempo real
title: Servicio de segmentación en Real-time Customer Data Platform
description: CDP en tiempo real se basa en Adobe Experience Platform y utiliza muchos de los servicios y funcionalidades del Experience Platform. Con el servicio de segmentación, puede proporcionar un marketing personalizado dividiendo a los clientes en grupos más pequeños con características similares.
exl-id: 140667c0-e288-40c4-8c45-c275e348b84a
source-git-commit: ad0d38cbd249642d582a807c5679065827f57717
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 0%

---

# [!DNL Segmentation Service] en [!DNL Real-time Customer Data Platform]

[!DNL Real-time Customer Data Platform] (CDP en tiempo real) le permite obtener datos de múltiples fuentes para ofrecer a sus clientes una experiencia coordinada y coherente. Se pueden realizar campañas de marketing personalizadas relevantes mediante la variable [!DNL Segmentation Service], parte de Adobe Experience Platform.

CDP en tiempo real se basa en Adobe Experience Platform y utiliza muchos de los [!DNL Experience Platform] servicios y funcionalidad. Al usar la variable [!DNL Segmentation Service], puede proporcionar marketing a medida dividiendo a los clientes en grupos más pequeños con características similares.

## Segmentación

La segmentación es el proceso de definir atributos o comportamientos específicos compartidos por un subconjunto de perfiles del almacén de perfiles para distinguir un grupo comercializable de personas de la base de clientes. Por ejemplo, en una campaña de correo electrónico llamada &quot;¿Olvidó comprar sus zapatillas?&quot;, puede que quiera una audiencia de todos los usuarios que buscaron zapatillas en los últimos 30 días, pero que no completaron una compra. Con distintos segmentos, puede centrarse en las distintas audiencias y ofrecer una experiencia de marketing más personalizada.

## [!DNL Segment Builder]

[!DNL Platform] le permite crear segmentos y acceder a ellos fácilmente, así como utilizar distintos componentes básicos para caracterizarlos aún más. Para obtener más información sobre cómo utilizar el Generador de segmentos, lea la [Guía del Generador de segmentos](./segment-builder-guide.md).

## Customer AI

Customer AI, incluido con Real-time Customer Data Platform, le ofrece la capacidad de generar predicciones de clientes a nivel individual con explicaciones.

Con la ayuda de factores influyentes, la Customer AI puede indicarle qué es lo más probable que haga un cliente y por qué. Además, puede beneficiarse de las predicciones y perspectivas de Customer AI para personalizar las experiencias de los clientes al ofrecer las ofertas y los mensajes más adecuados. Customer AI puede ayudarle con:

* Ofrecer modelos de propensión del cliente de alta precisión para lograr una segmentación y una segmentación más sólidas.
* Comprender los factores influyentes y la probabilidad detrás de ciertos comportamientos del cliente.
* Proporcionar opciones personalizables para casos de uso y datos únicos de su empresa.
* Mejora del perfil del cliente en tiempo real con puntuaciones de inclinación del cliente como la pérdida y la conversión.
* Mejora de los perfiles de los clientes con factores influyentes para las puntuaciones de tendencia.
* Creación de segmentos de clientes basados en factores influyentes y puntuaciones de tendencia.

La AI del cliente se encuentra en la variable **[!UICONTROL Servicios]** ficha **[!UICONTROL Servicios de Adobe]**.

![Ubicación de Customer AI](../assets/overview/rtcdp-customer-ai.png)

### Introducción a Customer AI

Para comenzar con Customer AI, debe seguir la [tutorial de preparación de datos](../../intelligent-services/data-preparation.md) y configure el esquema de entrada en función de su caso de uso. A continuación, tendrá que [configuración de una instancia de Customer AI](../../intelligent-services/customer-ai/user-guide/configure.md). Después de configurar una instancia, se genera un modelo en el que puede [ver sus perspectivas y puntuaciones](../../intelligent-services/customer-ai/user-guide/discover-insights.md). Con los datos generados a partir del modelo, puede crear segmentos para la activación controlada por datos.

Para obtener más información sobre Customer AI, comience por visitar la [Información general sobre Customer AI](../../intelligent-services/customer-ai/overview.md). Además, el siguiente vídeo muestra cómo la Customer AI enriquece los perfiles de los clientes con las tendencias basadas en AI y potencia la segmentación de clientes y los esfuerzos de determinación de objetivos.

>[!VIDEO](https://video.tv.adobe.com/v/40374/?quality=12&learn=on)


## Pasos siguientes

Después de leer esta descripción general, ahora debe comprender cómo utiliza CDP en tiempo real [!DNL Segmentation Service] para mejorar la personalización de las campañas de marketing. Para obtener más información sobre la variable [!DNL Segmentation Service], lea la [Documentación de segmentación](../../segmentation/home.md).
