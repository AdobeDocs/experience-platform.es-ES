---
keywords: activar destinos;activar datos
title: Información general de Activation
type: Tutorial
seo-title: Activation overview
description: Aprenda a activar los datos de audiencia que tiene en Adobe Experience Platform en varios tipos de destinos.
seo-description: Learn how to activate the audience data you have in Adobe Experience Platform to various types of destinations.
source-git-commit: f4721d3f114357b25517e4e66f1f626f82621c34
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 1%

---


# Información general de Activation

Adobe Experience Platform admite una amplia gama de destinos. El flujo de trabajo de activación de audiencia varía según el tipo de datos de audiencia que admiten y la frecuencia de exportación de datos.

## Métodos de activación {#activation-methods}

Después de [configurar los destinos](connect-destination.md), puede activar los segmentos de audiencia de varias formas:

### Activar audiencias desde el catálogo de destinos

Consulte las siguientes guías para obtener información detallada sobre la activación de audiencias en el destino desde el catálogo de destinos:

* [Activar datos de audiencia en destinos de exportación de segmentos de flujo continuo](activate-segment-streaming-destinations.md)
* [Activar datos de audiencia en destinos de exportación de perfil de flujo continuo](activate-streaming-profile-destinations.md)
* [Activar datos de audiencia en destinos de exportación de perfiles en lote](activate-batch-profile-destinations.md)

### Activar audiencias desde la página [!UICONTROL Browse]

Siga los pasos a continuación para activar los datos en los destinos desde la página **[!UICONTROL Browse]**.

1. Vaya a **[!UICONTROL Connections > Destinations]** y seleccione la pestaña **[!UICONTROL Browse]**.

   ![Ficha Examinar](../assets/ui/activation-overview/browse-tab.png)

1. Busque la conexión de destino que desea utilizar para activar los segmentos, seleccione los tres puntos en la columna [!UICONTROL Name] y, a continuación, seleccione **[!UICONTROL Activate segments]**.

   ![Botón Activar segmentos](../assets/ui/activation-overview/activate-segments.png)

1. Según el destino seleccionado, siga los pasos descritos en los artículos siguientes, empezando por el paso **[!UICONTROL Select segments]**, para finalizar el flujo de trabajo de activación:

   * [Activar datos de audiencia en destinos de exportación de segmentos de flujo continuo](activate-segment-streaming-destinations.md)
   * [Activar datos de audiencia en destinos de exportación de perfil de flujo continuo](activate-streaming-profile-destinations.md)
   * [Activar datos de audiencia en destinos de exportación de perfiles en lote](activate-batch-profile-destinations.md)

### Activar audiencias desde la página de detalles del segmento {#activate-segment-details}

Puede activar segmentos a destinos desde la página de detalles del segmento. Consulte [Detalles del segmento](../../segmentation/ui/overview.md#segment-details) para obtener más información.

Según el destino seleccionado, siga los pasos descritos en los artículos siguientes para finalizar el flujo de trabajo de activación:

* [Activar datos de audiencia en destinos de exportación de segmentos de flujo continuo](activate-segment-streaming-destinations.md)
* [Activar datos de audiencia en destinos de exportación de perfil de flujo continuo](activate-streaming-profile-destinations.md)
* [Activar datos de audiencia en destinos de exportación de perfiles en lote](activate-batch-profile-destinations.md)