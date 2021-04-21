---
keywords: Experience Platform;perfil;perfil del cliente en tiempo real;interfaz de usuario;IU;personalización;panel de perfiles;panel
title: Panel de destinos
description: Adobe Experience Platform proporciona un tablero en el que puede ver información importante sobre los destinos activos de su organización.
topic-legacy: guide
type: Documentation
exl-id: 6a34a796-24a1-450a-af39-60113928873e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 1%

---

# (Beta) [!UICONTROL Destinations] tablero

>[!IMPORTANT]
>
>La funcionalidad de tablero descrita en este documento está actualmente en fase beta y no está disponible para todos los usuarios. La documentación y las funciones están sujetas a cambios.

La interfaz de usuario (IU) de Adobe Experience Platform proporciona un tablero en el que puede ver información importante sobre los destinos activos de su organización, tal como se captura durante una instantánea diaria. Esta guía describe cómo acceder y trabajar con el panel de destinos en la interfaz de usuario y proporciona más información sobre las métricas que se muestran en el panel.

Para obtener una descripción general de los destinos, así como un catálogo de todos los destinos disponibles dentro de Experience Platform, visite la [información general de destinos](../../destinations/home.md).

## [!UICONTROL Destinations] datos de tablero  {#destinations-dashboard-data}

El tablero [!UICONTROL Destinations] muestra una instantánea de los destinos que su organización ha habilitado en Experience Profile. Los datos de la instantánea muestran los datos exactamente como aparecen en el momento concreto en que se tomó la instantánea. En otras palabras, la instantánea no es una aproximación o muestra de los datos y el panel de destinos no se actualiza en tiempo real.

>[!NOTE]
>
>Los cambios o actualizaciones realizados en los datos desde que se tomó la instantánea no se reflejarán en el panel hasta que se tome la siguiente instantánea.

## Exploración del panel de destinos

Para ir al panel de destinos dentro de la interfaz de usuario de Platform, seleccione **[!UICONTROL Destinations]** en el carril izquierdo y, a continuación, seleccione la pestaña **[!UICONTROL Overview]** para mostrar el panel.

![](../images/destinations/dashboard-overview.png)

## Widgets disponibles

Experience Platform proporciona varias utilidades que puede utilizar para visualizar distintas métricas relacionadas con los destinos. Seleccione el nombre de una utilidad para obtener más información:

* [[!UICONTROL Most used destinations]](#most-used-destinations)
* [[!UICONTROL Recently created destinations]](#recently-created-destinations)
* [[!UICONTROL Recently activated segments]](#recently-activated-segments)

### [!UICONTROL Most used destinations] {#most-used-destinations}

La utilidad **[!UICONTROL Most used destinations]** muestra los destinos principales de la organización por número de segmentos asignados, desde la última instantánea. Esta clasificación proporciona una perspectiva sobre los destinos que se utilizan, al tiempo que muestra los que pueden estar infrautilizados.

Por ejemplo, si configuró un destino ayer pero no le ha asignado ningún segmento, podría ver que el destino está infrautilizado.

El número de segmentos asignados que se muestra en la columna de recuento de segmentos es preciso a partir de la última instantánea diaria. La asignación de un nuevo segmento al destino no actualizará el recuento hasta que se tome la siguiente instantánea.

Si se selecciona el nombre de un destino en la lista que se muestra en la utilidad, se le dirigirá a los detalles de destino vinculados desde la pestaña **[!UICONTROL Browse]** . También puede seleccionar **[!UICONTROL View All]** para desplazarse a la pestaña **[!UICONTROL Browse]** y luego seleccionar el nombre de un destino para ver sus detalles.

![](../images/destinations/most-used-destinations.png)

### [!UICONTROL Recently created destinations] {#recently-created-destinations}

La utilidad **[!UICONTROL Recently created destinations]** permite ver una lista de los destinos configurados más recientemente en la organización.

La fecha creada mostrada es precisa para la última instantánea diaria. En otras palabras, si crea un nuevo destino, no aparecerá en la lista hasta que se haya tomado la siguiente instantánea.

Si se selecciona el nombre de un destino en la lista que se muestra en la utilidad, se le dirigirá a los detalles de destino vinculados desde la pestaña **[!UICONTROL Browse]** . También puede seleccionar **[!UICONTROL View All]** para desplazarse a la pestaña **[!UICONTROL Browse]** y luego seleccionar el nombre de un destino para ver sus detalles.

Para obtener más información sobre cómo configurar tipos de destinos específicos, visite la [documentación de destinos](../../destinations/home.md).

![](../images/destinations/recently-created-destinations.png)

### [!UICONTROL Recently activated segments] {#recently-activated-segments}

El widget **[!UICONTROL Recently activated segments]** proporciona una lista de los segmentos que se han asignado más recientemente a un destino. Esta lista proporciona una instantánea de los segmentos y destinos que se utilizan activamente en el sistema y puede ayudar a solucionar cualquier problema relacionado con las asignaciones erróneas.

La fecha actualizada que se muestra muestra muestra la última vez que se activó el segmento en el destino y es precisa para la última instantánea diaria. En otras palabras, si activa un segmento en el destino, la fecha de actualización no cambiará hasta que se tome la siguiente instantánea.

Si selecciona el nombre de un segmento en la lista que se muestra en la utilidad, obtendrá los detalles del segmento. También puede seleccionar **[!UICONTROL View All]** para ir a la pestaña de exploración de segmentos y, a continuación, seleccionar el nombre de un segmento para ver sus detalles.

Para obtener más información sobre cómo trabajar con segmentos en el Experience Platform, comience por leer la [información general del Servicio de segmentación](../../segmentation/home.md).

![](../images/destinations/recently-activated-segments.png)

## Pasos siguientes

Al seguir este documento, debería poder localizar el panel de destinos y comprender las métricas que se muestran en los widgets disponibles. Para obtener más información sobre cómo trabajar con destinos en Experience Platform, consulte la [documentación de destinos](../../destinations/home.md).
