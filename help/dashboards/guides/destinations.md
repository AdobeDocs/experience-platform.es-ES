---
keywords: Experience Platform;perfil;perfil del cliente en tiempo real;interfaz de usuario;IU;personalización;panel de perfiles;panel
title: Panel de destinos
description: Adobe Experience Platform proporciona un tablero en el que puede ver información importante sobre los destinos activos de su organización.
type: Documentation
exl-id: 6a34a796-24a1-450a-af39-60113928873e
source-git-commit: 41ef7a6e6d3b0ee9afe762b19c8c286ceb361dbb
workflow-type: tm+mt
source-wordcount: '895'
ht-degree: 0%

---

#  Panel de destinos

La interfaz de usuario (IU) de Adobe Experience Platform proporciona un tablero en el que puede ver información importante sobre los destinos activos de su organización, tal como se captura durante una instantánea diaria. Esta guía describe cómo acceder y trabajar con el panel de destinos en la interfaz de usuario y proporciona más información sobre las métricas que se muestran en el panel.

Para obtener una descripción general de los destinos, así como un catálogo de todos los destinos disponibles dentro de Experience Platform, visite la [documentación de destinos](../../destinations/home.md).

##  Destinos, datos de tablero {#destinations-dashboard-data}

El tablero [!UICONTROL Destinations] muestra una instantánea de los destinos que su organización ha habilitado en Experience Profile. Los datos de la instantánea muestran los datos exactamente como aparecen en el momento concreto en que se tomó la instantánea. En otras palabras, la instantánea no es una aproximación o muestra de los datos y el panel de destinos no se actualiza en tiempo real.

>[!NOTE]
>
>Los cambios o actualizaciones realizados en los datos desde que se tomó la instantánea no se reflejarán en el panel hasta que se tome la siguiente instantánea.

## Exploración del panel de destinos

Para ir al panel de destinos dentro de la interfaz de usuario de Platform, seleccione **[!UICONTROL Destinations]** en el carril izquierdo y, a continuación, seleccione la pestaña **[!UICONTROL Overview]** para mostrar el panel.

>[!NOTE]
>
>Si su organización es nueva para Experience Platform y aún no tiene destinos activos, el panel [!UICONTROL Destinations] y la pestaña [!UICONTROL Overview] no están visibles. En su lugar, al seleccionar [!UICONTROL Destinations] en el panel de navegación izquierdo, se muestra la pestaña [!UICONTROL Catalog]. Para obtener más información sobre la pestaña [!UICONTROL Catalog], consulte la [[!UICONTROL Destinations] guía del espacio de trabajo](../../destinations/ui/destinations-workspace.md).

![](../images/destinations/dashboard-overview.png)

### Modificación del panel de destinos

Puede modificar el aspecto del panel de destinos seleccionando **[!UICONTROL Modificar tablero]**. Esto le permite mover, agregar y quitar utilidades del tablero, así como acceder a la **[!UICONTROL biblioteca de utilidades]** para explorar las utilidades disponibles y crear utilidades personalizadas para su organización.

Consulte la documentación [modificación de tableros](../customize/modify.md) y [descripción general de la biblioteca de utilidades](../customize/widget-library.md) para obtener más información.

## Widgets estándar

Adobe proporciona varios widgets estándar que puede utilizar para visualizar distintas métricas relacionadas con los destinos. También puede crear utilidades personalizadas para compartirlas con su organización mediante la [!UICONTROL biblioteca de utilidades]. Para obtener más información sobre la creación de utilidades personalizadas, comience leyendo la [descripción general de la biblioteca de utilidades](../customize/widget-library.md).

Para obtener más información sobre cada uno de los widgets estándar disponibles, seleccione el nombre de un widget en la siguiente lista:

* [[!UICONTROL Destinos más utilizados]](#most-used-destinations)
* [[!UICONTROL Destinos creados recientemente]](#recently-created-destinations)
* [[!UICONTROL Segmentos activados recientemente]](#recently-activated-segments)

### [!UICONTROL Destinos más utilizados] {#most-used-destinations}

El widget **[!UICONTROL Destinos más utilizados]** muestra los destinos principales de su organización por número de segmentos asignados, desde la última instantánea. Esta clasificación proporciona una perspectiva sobre los destinos que se utilizan, al tiempo que muestra los que pueden estar infrautilizados.

Por ejemplo, si configuró un destino ayer pero no le ha asignado ningún segmento, podría ver que el destino está infrautilizado.

El número de segmentos asignados que se muestra en la columna de recuento de segmentos es preciso a partir de la última instantánea diaria. La asignación de un nuevo segmento al destino no actualizará el recuento hasta que se tome la siguiente instantánea.

Si selecciona el nombre de un destino en la lista que se muestra en la utilidad, se le dirigirá a los detalles de destino vinculados desde la pestaña **[!UICONTROL Browse]**. También puede seleccionar **[!UICONTROL Ver todo]** para ir a la pestaña **[!UICONTROL Examinar]** y luego seleccionar el nombre de un destino para ver sus detalles.

![](../images/destinations/most-used-destinations.png)

### [!UICONTROL Destinos creados recientemente] {#recently-created-destinations}

La utilidad **[!UICONTROL Destinos creados recientemente]** permite ver una lista de los destinos configurados más recientemente en la organización.

La fecha creada mostrada es precisa para la última instantánea diaria. En otras palabras, si crea un nuevo destino, no aparecerá en la lista hasta que se haya tomado la siguiente instantánea.

Si selecciona el nombre de un destino en la lista que se muestra en la utilidad, se le dirigirá a los detalles de destino vinculados desde la pestaña **[!UICONTROL Browse]**. También puede seleccionar **[!UICONTROL Ver todo]** para ir a la pestaña **[!UICONTROL Examinar]** y luego seleccionar el nombre de un destino para ver sus detalles.

Para obtener más información sobre cómo configurar tipos de destinos específicos, visite la [documentación de destinos](../../destinations/home.md).

![](../images/destinations/recently-created-destinations.png)

### [!UICONTROL Segmentos activados recientemente] {#recently-activated-segments}

El widget **[!UICONTROL Segmentos activados recientemente]** proporciona una lista de los segmentos que se han asignado más recientemente a un destino. Esta lista proporciona una instantánea de los segmentos y destinos que se utilizan activamente en el sistema y puede ayudar a solucionar cualquier problema relacionado con las asignaciones erróneas.

La fecha actualizada que se muestra muestra muestra la última vez que se activó el segmento en el destino y es precisa para la última instantánea diaria. En otras palabras, si activa un segmento en el destino, la fecha de actualización no cambiará hasta que se tome la siguiente instantánea.

Si selecciona el nombre de un segmento en la lista que se muestra en la utilidad, obtendrá los detalles del segmento. También puede seleccionar **[!UICONTROL Ver todo]** para ir a la pestaña de exploración de segmentos y, a continuación, seleccionar el nombre de un segmento para ver sus detalles.

Para obtener más información sobre cómo trabajar con segmentos en el Experience Platform, comience por leer la [información general del Servicio de segmentación](../../segmentation/home.md).

![](../images/destinations/recently-activated-segments.png)

## Pasos siguientes

Al seguir este documento, debería poder localizar el panel de destinos y comprender las métricas que se muestran en los widgets disponibles. Para obtener más información sobre cómo trabajar con destinos en Experience Platform, consulte la [documentación de destinos](../../destinations/home.md).
