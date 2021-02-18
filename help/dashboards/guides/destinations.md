---
keywords: Experience Platform;perfil;perfil del cliente en tiempo real;interfaz de usuario;IU;personalización;panel de perfil;panel
title: Panel de destinos
description: Adobe Experience Platform proporciona un panel mediante el cual puede realizar vistas de información importante sobre los destinos activos de su organización.
topic: guide
type: Documentation
translation-type: tm+mt
source-git-commit: 2f2459c1c88c97a3ab322b08ee178463fbb4a592
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 1%

---


# (Beta) [!UICONTROL panel de destinos]

>[!IMPORTANT]
>
>La funcionalidad de panel descrita en este documento está actualmente en fase beta y no está disponible para todos los usuarios. La documentación y las funciones están sujetas a cambios.

La interfaz de usuario (IU) de Adobe Experience Platform proporciona un panel a través del cual puede realizar vistas de información importante sobre los destinos activos de la organización, tal como se captura durante una instantánea diaria. Esta guía describe cómo acceder al panel de destinos en la interfaz de usuario y cómo trabajar con él, y proporciona más información sobre las métricas que se muestran en el panel.

Para obtener una visión general de los destinos, así como un catálogo de todos los destinos disponibles en Experience Platform, visite [destinos overview](../../destinations/home.md).

##  DestinosDatos del tablero  {#destinations-dashboard-data}

El panel [!UICONTROL Destinations] muestra una instantánea de los destinos que su organización ha habilitado en Experience Perfil. Los datos de la instantánea muestran los datos exactamente como aparecen en el momento específico en que se realizó la instantánea. En otras palabras, la instantánea no es una aproximación o muestra de los datos y el panel de destinos no se actualiza en tiempo real.

>[!NOTE]
>
>Los cambios o actualizaciones realizados en los datos desde que se realizó la instantánea no se reflejarán en el panel hasta que se realice la siguiente instantánea.

## Exploración del panel de destinos

Para desplazarse al panel de destinos dentro de la interfaz de usuario de la plataforma, seleccione **[!UICONTROL Destinations]** en el carril izquierdo y, a continuación, seleccione la ficha **[!UICONTROL Overview]** para mostrar el panel.

![](../images/destinations/dashboard-overview.png)

## Widgets disponibles

Experience Platform proporciona varias utilidades que puede utilizar para visualizar distintas métricas relacionadas con los destinos. Seleccione el nombre de una utilidad a continuación para obtener más información:

* [[!UICONTROL Destinos más utilizados]](#most-used-destinations)
* [[!UICONTROL Destinos creados recientemente]](#recently-created-destinations)
* [[!UICONTROL Segmentos activados recientemente]](#recently-activated-segments)

### [!UICONTROL Destinos más utilizados] {#most-used-destinations}

La utilidad **[!UICONTROL Destinos más utilizados]** muestra los destinos principales de la organización por número de segmentos asignados, desde la última instantánea. Esta clasificación proporciona una visión detallada de los destinos que se utilizan, al tiempo que muestra también los que podrían estar infrautilizados.

Por ejemplo: si configuró un destino ayer pero no asignó ningún segmento a él, podría ver que el destino está infrautilizado en este momento.

El número de segmentos asignados que se muestra en la columna de recuento de segmentos es preciso a partir de la última instantánea diaria. La asignación de un nuevo segmento al destino no actualizará el recuento hasta que se realice la siguiente instantánea.

Si selecciona el nombre de un destino en la lista que se muestra en la utilidad, se le dirigirá a los detalles de destino como se vinculan desde la ficha **[!UICONTROL Examinar]**. También puede seleccionar **[!UICONTROL Vista de todo]** para navegar a la ficha **[!UICONTROL Examinar]** y luego seleccionar el nombre de un destino para vista de sus detalles.

![](../images/destinations/most-used-destinations.png)

### [!UICONTROL Destinos creados recientemente] {#recently-created-destinations}

La utilidad **[!UICONTROL Destinos creados recientemente]** permite ver una lista de los destinos configurados más recientemente en la organización.

La fecha de creación mostrada es exacta a la última instantánea diaria. En otras palabras, si crea un nuevo destino, no aparecerá en la lista hasta que se realice la siguiente instantánea.

Si selecciona el nombre de un destino en la lista que se muestra en la utilidad, se le dirigirá a los detalles de destino como se vinculan desde la ficha **[!UICONTROL Examinar]**. También puede seleccionar **[!UICONTROL Vista de todo]** para navegar a la ficha **[!UICONTROL Examinar]** y luego seleccionar el nombre de un destino para vista de sus detalles.

Para obtener más información sobre cómo configurar tipos específicos de destinos, visite la [documentación de destinos](../../destinations/home.md).

![](../images/destinations/recently-created-destinations.png)

### [!UICONTROL Segmentos activados recientemente] {#recently-activated-segments}

La utilidad **[!UICONTROL Segmentos activados recientemente]** proporciona una lista de los segmentos asignados más recientemente a un destino. Esta lista proporciona una instantánea de los segmentos y destinos que se utilizan activamente en el sistema y puede ayudar a solucionar cualquier error de asignación.

La fecha actualizada que se muestra muestra la última vez que se activó el segmento en el destino y es precisa para la última instantánea diaria. En otras palabras, si activa un segmento en el destino, la fecha de actualización no cambiará hasta que se realice la siguiente instantánea.

Si selecciona el nombre de un segmento desde la lista mostrada en la utilidad, se le dirigirá a los detalles del segmento. También puede seleccionar **[!UICONTROL Vista de todo]** para navegar hasta la ficha de exploración de segmentos y, a continuación, seleccionar el nombre de un segmento para vista de sus detalles.

Para obtener más información sobre cómo trabajar con segmentos en Experience Platform, lea la [información general del servicio de segmentación](../../segmentation/home.md).

![](../images/destinations/recently-activated-segments.png)

## Pasos siguientes

Al seguir este documento, ahora debe poder localizar el panel de destinos y comprender las métricas que se muestran en los widgets disponibles. Para obtener más información sobre cómo trabajar con destinos en Experience Platform, consulte la [documentación de destinos](../../destinations/home.md).