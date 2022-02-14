---
keywords: personalización; target; destino; personalización de destinos; configurar destinos de personalización; la misma página; página siguiente;
title: Configurar destinos de personalización para la personalización de la misma página y de la página siguiente
type: Tutorial
seo-title: Configure personalization destinations for same-page and next-page personalization.
description: Obtenga información sobre cómo configurar destinos de personalización para la personalización de la misma página y de la página siguiente.
seo-description: Configure personalization destinations for same-page and next-page personalization.
exl-id: 7d7b6869-bd59-4766-a044-f449396f6524
source-git-commit: 69db8dbc315f97a0133bcc761ebf850d587dd7d1
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---

# Configurar destinos de personalización para la personalización de la misma página y de la página siguiente

Uso de Adobe Experience Platform [segmentación de arista](../../segmentation/ui/edge-segmentation.md) para permitir a los clientes crear y segmentar segmentos de audiencia a gran escala, en tiempo real.

Esta capacidad le ayuda a configurar casos de uso de personalización de la misma página y de la siguiente página.

Este artículo proporciona instrucciones paso a paso sobre cómo configurar los destinos de Experience Platform y personalización para estos casos de uso.

Además, vea el siguiente vídeo para obtener información general sobre el proceso de configuración de extremo a extremo.

>[!VIDEO](https://video.tv.adobe.com/v/340091/)

## Paso 1: Configuración de un conjunto de datos en la interfaz de usuario de la recopilación de datos {#configure-datastream}

El primer paso para configurar el destino de personalización es configurar un conjunto de datos para el SDK web del Experience Platform. Esto se realiza en la interfaz de usuario de la recopilación de datos.

Al configurar el conjunto de datos, en **[!UICONTROL Adobe Experience Platform]** asegúrese de que ambas **[!UICONTROL Segmentación de Edge]** y **[!UICONTROL Destinos de personalización]** están seleccionados.

![Configuración del almacén de datos](../assets/ui/configure-personalization-destinations/datastream-config.png)

Para obtener más información sobre cómo configurar un conjunto de datos, siga las instrucciones descritas en la sección [Documentación del SDK web de plataforma](../../edge/fundamentals/datastreams.md).

## Paso 2: Configurar el destino personalizado {#configure-destination}

Una vez configurado el conjunto de datos, puede empezar a configurar el destino de personalización.

Siga las [tutorial de creación de conexión de destino](../ui/connect-destination.md) para obtener instrucciones detalladas sobre cómo crear una nueva conexión de destino.

Según el destino que esté configurando, consulte los siguientes artículos para conocer los requisitos previos específicos de destino y la información relacionada:

* [Conexión Adobe Target](../catalog/personalization/adobe-target-connection.md)
* [Conexión personalizada personalizada](../catalog/personalization/custom-personalization.md)

## Paso 3: Cree un [!DNL Active-On-Edge] combinar directiva {#create-merge-policy}

Después de crear la conexión de destino, debe crear una [!DNL Active-On-Edge] directiva de combinación.

Siga las instrucciones indicadas en [creación de una directiva de combinación](../../profile/merge-policies/ui-guide.md#create-a-merge-policy)y asegúrese de habilitar la variable **[!UICONTROL Política de combinación activa/perimetral]** alternar.

## Paso 4: Crear un nuevo segmento en Platform {#create-segment}

Una vez creado el [!DNL Active-On-Edge] política de combinación, debe crear un nuevo segmento en Platform.

Siga las [generador de segmentos](../../segmentation/ui/segment-builder.md) guía para crear el nuevo segmento y asegúrese de [asignarlo](../../segmentation/ui/segment-builder.md#merge-policies) el [!DNL Active-On-Edge] política de combinación que ha creado en el paso 3.

## Paso 5: Activar el segmento en el destino

El último paso del proceso de configuración es activar el segmento que ha creado en el paso 4 al destino que ha creado en el paso 2.

Para ello, siga esta [tutorial de activación](../ui/activate-profile-request-destinations.md).

## Validación de la configuración {#validate-configuration}

Después de seguir correctamente los pasos anteriores, debería ver los nuevos segmentos en su destino de personalización.
