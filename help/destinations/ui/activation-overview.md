---
keywords: activar destinos;activar datos
title: Información general de Activation
type: Tutorial
seo-title: Activation overview
description: Aprenda a activar los datos de audiencia que tiene en Adobe Experience Platform en varios tipos de destinos.
seo-description: Learn how to activate the audience data you have in Adobe Experience Platform to various types of destinations.
exl-id: 987af401-2d93-45b4-a8f9-191e6058e4da
source-git-commit: 5240e0db96a5072ab02a4c8b52e9c2d3dd4d6aa0
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 1%

---

# Información general de Activation

>[!IMPORTANT]
> 
>Para activar los datos, necesita la variable **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Adobe Experience Platform admite una amplia gama de destinos. El flujo de trabajo de activación de audiencia varía según el tipo de datos de audiencia que admiten y la frecuencia de exportación de datos.

## Métodos de activación {#activation-methods}

Tras [configurar el destino](connect-destination.md), puede activar los segmentos de audiencia de varias formas:

### Activar audiencias desde el catálogo de destinos

Consulte las siguientes guías para obtener información detallada sobre la activación de audiencias en el destino desde el catálogo de destinos:

* [Activar datos de audiencia en destinos de exportación de segmentos de flujo continuo](activate-segment-streaming-destinations.md)
* [Activar datos de audiencia en destinos de exportación de perfil de flujo continuo](activate-streaming-profile-destinations.md)
* [Activar datos de audiencia en destinos de exportación de perfiles en lote](activate-batch-profile-destinations.md)

### Activar audiencias desde el [!UICONTROL Examinar] página

Siga los pasos a continuación para activar los datos en los destinos desde la variable **[!UICONTROL Examinar]** página.

1. Vaya a **[!UICONTROL Conexiones > Destinos]** y seleccione **[!UICONTROL Examinar]** pestaña .

   ![Ficha Examinar](../assets/ui/activation-overview/browse-tab.png)

1. Busque la conexión de destino que desea utilizar para activar los segmentos, seleccione los tres puntos en la [!UICONTROL Nombre] y, a continuación, seleccione **[!UICONTROL Activar segmentos]**.

   ![Botón Activar segmentos](../assets/ui/activation-overview/activate-segments.png)

1. En función del destino seleccionado, siga los pasos descritos en los artículos siguientes, empezando por el **[!UICONTROL Seleccionar segmentos]** para finalizar el flujo de trabajo de activación:

   * [Activar datos de audiencia en destinos de exportación de segmentos de flujo continuo](activate-segment-streaming-destinations.md)
   * [Activar datos de audiencia en destinos de exportación de perfil de flujo continuo](activate-streaming-profile-destinations.md)
   * [Activar datos de audiencia en destinos de exportación de perfiles en lote](activate-batch-profile-destinations.md)

### Activar audiencias desde la página de detalles del segmento {#activate-segment-details}

Puede activar segmentos a destinos desde la página de detalles del segmento. Consulte [Detalles del segmento](../../segmentation/ui/overview.md#segment-details) para obtener más información.

Según el destino seleccionado, siga los pasos descritos en los artículos siguientes para finalizar el flujo de trabajo de activación:

* [Activar datos de audiencia en destinos de exportación de segmentos de flujo continuo](activate-segment-streaming-destinations.md)
* [Activar datos de audiencia en destinos de exportación de perfil de flujo continuo](activate-streaming-profile-destinations.md)
* [Activar datos de audiencia en destinos de exportación de perfiles en lote](activate-batch-profile-destinations.md)
