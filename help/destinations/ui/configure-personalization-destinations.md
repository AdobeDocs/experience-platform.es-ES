---
keywords: personalización; target; destino; destinos de personalización; configurar destinos de personalización; misma página; página siguiente;
title: Configurar destinos de personalización para la personalización de la misma página y de la página siguiente
type: Tutorial
description: Obtenga información sobre cómo configurar destinos de personalización para la personalización de la misma página y de la página siguiente.
exl-id: 7d7b6869-bd59-4766-a044-f449396f6524
source-git-commit: a6fe0f5a0c4f87ac265bf13cb8bba98252f147e0
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---

# Configurar destinos de personalización para la personalización de la misma página y de la página siguiente

## Información general {#overview}

>[!NOTE]
>
>Cuándo [configuración de la conexión de Adobe Target](../catalog/personalization/adobe-target-connection.md) sin usar un ID de flujo de datos, no se admiten los casos de uso descritos en este artículo.

Adobe Experience Platform utiliza [segmentación de borde](../../segmentation/ui/edge-segmentation.md) para permitir a los clientes crear y segmentar audiencias a gran escala, en tiempo real.

Esta capacidad le ayuda a configurar casos de uso de personalización de la misma página y de la siguiente.

Este artículo proporciona instrucciones paso a paso sobre cómo configurar Experience Platform y los destinos de personalización para estos casos de uso.

Además, vea el siguiente vídeo para obtener una descripción general del proceso de configuración de extremo a extremo.

>[!VIDEO](https://video.tv.adobe.com/v/340091/)

>[!NOTE]
>
>La interfaz de usuario del Experience Platform se actualiza con frecuencia y puede haber cambiado desde que se grabó este vídeo. Para obtener la información más actualizada, consulte los pasos de configuración descritos en las secciones siguientes.

## Paso 1: Configurar un flujo de datos en la IU de recopilación de datos {#configure-datastream}

El primer paso para configurar el destino de personalización es configurar una secuencia de datos para el SDK web de Experience Platform. Esto se realiza en la IU de recopilación de datos.

Al configurar la secuencia de datos, en **[!UICONTROL Adobe Experience Platform]** asegúrese de que ambas **[!UICONTROL Segmentación de Edge]** y **[!UICONTROL Destinos de personalización]** están seleccionados.

![Configuración de flujo de datos](../assets/ui/configure-personalization-destinations/datastream-config.png)

Para obtener más información sobre cómo configurar un conjunto de datos, siga las instrucciones que se describen en la [Documentación del SDK web de Platform](../../edge/datastreams/overview.md).

## Paso 2: Configuración del destino de personalización {#configure-destination}

Una vez configurada la secuencia de datos, puede empezar a configurar el destino de personalización.

Siga las [tutorial de creación de conexión de destino](../ui/connect-destination.md) para obtener instrucciones detalladas sobre cómo crear una nueva conexión de destino.

Según el destino que esté configurando, consulte los siguientes artículos para conocer los requisitos previos específicos del destino y la información relacionada:

* [Conexión de Adobe Target](../catalog/personalization/adobe-target-connection.md)
* [Conexión de personalización personalizada](../catalog/personalization/custom-personalization.md)

## Paso 3: Crear un [!DNL Active-On-Edge] política de combinación {#create-merge-policy}

Después de crear la conexión de destino, debe crear un [!DNL Active-On-Edge] política de combinación.

Siga las instrucciones de [creación de una política de combinación](../../profile/merge-policies/ui-guide.md#create-a-merge-policy)y asegúrese de habilitar la variable **[!UICONTROL Política de combinación activa en Edge]** alternar.

## Paso 4: Crear un nuevo segmento en Platform {#create-segment}

Después de crear el [!DNL Active-On-Edge] política de combinación, debe crear un nuevo segmento en Platform.

Siga las [generador de segmentos](../../segmentation/ui/segment-builder.md) para crear su nuevo segmento, y asegúrese de lo siguiente [asignarlo](../../segmentation/ui/segment-builder.md#merge-policies) el [!DNL Active-On-Edge] política de combinación creada en el paso 3.

## Paso 5: Activar el segmento en su destino

El último paso del proceso de configuración es activar el segmento que ha creado en el paso 4 en el destino que ha creado en el paso 2.

Para ello, siga este [tutorial de activación](../ui/activate-profile-request-destinations.md).

## Validación de la configuración {#validate-configuration}

Después de seguir correctamente los pasos anteriores, debería ver los nuevos segmentos en el destino de personalización.
