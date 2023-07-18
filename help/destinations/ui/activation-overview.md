---
keywords: activar destinos;activar datos
title: Información general de Activation
type: Tutorial
description: Obtenga información sobre cómo activar las audiencias que tiene en Adobe Experience Platform en varios tipos de destinos.
exl-id: 987af401-2d93-45b4-a8f9-191e6058e4da
source-git-commit: 771801b52b7df7029e1c6e7496dcfb563463d06e
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 1%

---

# Información general de Activation

>[!IMPORTANT]
> 
>Para activar los datos, necesita el **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Adobe Experience Platform admite una amplia gama de destinos. El flujo de trabajo de activación de audiencia varía según el destino, el tipo de datos de audiencia que admite y la frecuencia de exportación de datos.

## Métodos de activación {#activation-methods}

Después de usted [configuración del destino](connect-destination.md)Además, las audiencias se pueden activar de varias formas:

### Activar audiencias desde el catálogo de destinos

Consulte las siguientes guías para obtener información detallada sobre la activación de audiencias en el destino desde el catálogo de destinos:

* [Activar datos de audiencia en destinos de exportación de audiencia de flujo continuo](activate-segment-streaming-destinations.md)
* [Activación de datos de audiencia en destinos de exportación de perfil de flujo continuo](activate-streaming-profile-destinations.md)
* [Activar datos de audiencia en destinos de exportación de perfiles por lotes](activate-batch-profile-destinations.md)

### Activar audiencias desde el [!UICONTROL Examinar] página

Siga los pasos a continuación para activar los datos en sus destinos desde el **[!UICONTROL Examinar]** página.

1. Ir a **[!UICONTROL Conexiones > Destinos]** y seleccione la opción **[!UICONTROL Examinar]** pestaña.

   ![Ficha Examinar](../assets/ui/activation-overview/browse-tab.png)

1. Busque la conexión de destino que desee utilizar para activar los segmentos, seleccione los tres puntos en la [!UICONTROL Nombre] y, a continuación, seleccione **[!UICONTROL Activar audiencias]**.

   ![Botón Activar audiencias](../assets/ui/activation-overview/activate-segments.png)

1. Según el destino seleccionado, siga los pasos descritos en los artículos siguientes, empezando por **[!UICONTROL Seleccionar segmentos]** para finalizar el flujo de trabajo de activación:

   * [Activar datos de audiencia en destinos de exportación de audiencia de flujo continuo](activate-segment-streaming-destinations.md)
   * [Activación de datos de audiencia en destinos de exportación de perfil de flujo continuo](activate-streaming-profile-destinations.md)
   * [Activar datos de audiencia en destinos de exportación de perfiles por lotes](activate-batch-profile-destinations.md)

### Activar audiencias desde la página de detalles de audiencia {#activate-audience-details}

Puede activar audiencias en destinos desde la página de detalles de audiencia. Consulte [Detalles de audiencia](../../segmentation/ui/overview.md#audience-details) para obtener más información.

Según el destino seleccionado, siga los pasos descritos en los artículos siguientes para finalizar el flujo de trabajo de activación:

* [Activar datos de audiencia en destinos de exportación de audiencia de flujo continuo](activate-segment-streaming-destinations.md)
* [Activación de datos de audiencia en destinos de exportación de perfil de flujo continuo](activate-streaming-profile-destinations.md)
* [Activar datos de audiencia en destinos de exportación de perfiles por lotes](activate-batch-profile-destinations.md)
