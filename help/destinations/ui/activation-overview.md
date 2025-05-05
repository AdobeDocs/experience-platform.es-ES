---
keywords: activar destinos;activar datos
title: Información general de Activation
type: Tutorial
description: Obtenga información sobre cómo activar las audiencias que tiene en Adobe Experience Platform en varios tipos de destinos.
exl-id: 987af401-2d93-45b4-a8f9-191e6058e4da
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 1%

---

# Información general de Activation

>[!IMPORTANT]
> 
>* Para activar los datos, necesita los **[!UICONTROL permisos de control de acceso]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]**&#x200B;[para ](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[[!UICONTROL permiso de control de acceso]](/help/access-control/home.md#permissions) de&rbrack;** Ver gráfico de identidad&lbrack;. <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Adobe Experience Platform admite una amplia gama de destinos. El flujo de trabajo de activación de audiencia varía según el destino, el tipo de datos de audiencia que admite y la frecuencia de exportación de datos.

## Métodos de activación {#activation-methods}

Después de [configurar el destino](connect-destination.md), puede activar audiencias de varias maneras:

### Activar audiencias desde el catálogo de destinos

Consulte las siguientes guías para obtener información detallada sobre la activación de audiencias en el destino desde el catálogo de destinos:

* [Activar datos de audiencia en destinos de exportación de audiencia de flujo continuo](activate-segment-streaming-destinations.md)
* [Activación de datos de audiencia en destinos de exportación de perfil de flujo continuo](activate-streaming-profile-destinations.md)
* [Activar datos de audiencia en destinos de exportación de perfiles por lotes](activate-batch-profile-destinations.md)

### Activar audiencias desde la página [!UICONTROL Examinar]

Siga los pasos a continuación para activar los datos en sus destinos desde la página **[!UICONTROL Examinar]**.

1. Vaya a **[!UICONTROL Conexiones > Destinos]** y seleccione la pestaña **[!UICONTROL Examinar]**.

   ![Ficha Examinar](../assets/ui/activation-overview/browse-tab.png)

1. Busque la conexión de destino que desee usar para activar los segmentos, seleccione los tres puntos de la columna [!UICONTROL Nombre] y, a continuación, seleccione **[!UICONTROL Activar audiencias]**.

   ![Botón Activar audiencias](../assets/ui/activation-overview/activate-segments.png)

1. Según el destino seleccionado, siga los pasos descritos en los artículos siguientes, empezando por el paso **[!UICONTROL Seleccionar segmentos]** para finalizar el flujo de trabajo de activación:

   * [Activar datos de audiencia en destinos de exportación de audiencia de flujo continuo](activate-segment-streaming-destinations.md)
   * [Activación de datos de audiencia en destinos de exportación de perfil de flujo continuo](activate-streaming-profile-destinations.md)
   * [Activar datos de audiencia en destinos de exportación de perfiles por lotes](activate-batch-profile-destinations.md)

### Activar audiencias desde la página de detalles de audiencia {#activate-audience-details}

Puede activar audiencias en destinos desde la página de detalles de audiencia. Consulte [Detalles de audiencia](../../segmentation/ui/audience-portal.md#audience-details) para obtener más información.

Según el destino seleccionado, siga los pasos descritos en los artículos siguientes para finalizar el flujo de trabajo de activación:

* [Activar datos de audiencia en destinos de exportación de audiencia de flujo continuo](activate-segment-streaming-destinations.md)
* [Activación de datos de audiencia en destinos de exportación de perfil de flujo continuo](activate-streaming-profile-destinations.md)
* [Activar datos de audiencia en destinos de exportación de perfiles por lotes](activate-batch-profile-destinations.md)
