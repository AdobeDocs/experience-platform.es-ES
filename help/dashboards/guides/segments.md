---
keywords: Experience Platform;perfil;segmento;segmentos;segmentación;interfaz de usuario;IU;personalización;panel de segmentos;tablero
title: Tablero de segmentos
description: 'Adobe Experience Platform proporciona un tablero a través del cual puede ver información importante sobre los segmentos que su organización ha creado. '
type: Documentation
exl-id: de5e07bc-2c44-416e-99db-7607059117cb
source-git-commit: 36aaccddeb207e22a22d5124ec8592ac8dddf8bc
workflow-type: tm+mt
source-wordcount: '900'
ht-degree: 0%

---

# Panel de segmentos {#segment-dashboard}

La interfaz de usuario (IU) de Adobe Experience Platform proporciona un tablero a través del cual puede ver información importante sobre sus segmentos, tal como se captura durante una instantánea diaria. Esta guía describe cómo acceder y trabajar con el panel de segmentos en la interfaz de usuario y proporciona más información sobre las visualizaciones que se muestran en el panel.

Para obtener una descripción general de todas las funciones del servicio de segmentación de Adobe Experience Platform dentro de la interfaz de usuario de Platform, visite la [Guía de interfaz de usuario del servicio de segmentación](../../segmentation/ui/overview.md).

## Datos del tablero de segmentos

El panel de segmentos muestra una instantánea de los datos de atributo (registro) que su organización tiene dentro del Almacenamiento de perfiles en Experience Platform. La instantánea no incluye datos de ningún evento (serie temporal).

Los datos de atributo de la instantánea muestran los datos exactamente como aparecen en el momento concreto en que se tomó la instantánea. En otras palabras, la instantánea no es una aproximación o muestra de los datos y el panel de segmentos no se actualiza en tiempo real.

>[!NOTE]
>
>Los cambios o actualizaciones realizados en los datos desde que se tomó la instantánea no se reflejarán en el panel hasta que se tome la siguiente instantánea.

## Exploración del panel de segmentos

Para ir al tablero de segmentos dentro de la interfaz de usuario de Platform, seleccione **[!UICONTROL Segments]** en el carril izquierdo y, a continuación, seleccione la pestaña **[!UICONTROL Overview]** para mostrar el tablero.

![](../images/segments/dashboard-overview.png)

### Modificación del tablero [!UICONTROL Segments]

Puede modificar el aspecto del tablero [!UICONTROL Segments] seleccionando **[!UICONTROL Modify dashboard]**. Esto le permite mover, agregar y quitar utilidades del tablero, así como acceder a la [!UICONTROL biblioteca de utilidades] para explorar las utilidades disponibles y crear utilidades personalizadas para su organización.

Consulte la documentación [modificación de tableros](../modify.md) y [biblioteca de utilidades](../widget-library.md) para obtener más información.

## Seleccionar un segmento

El tablero selecciona automáticamente un segmento para mostrar, aunque puede cambiarlo con el menú desplegable o el selector de segmentos.

Para elegir un segmento diferente, seleccione la lista desplegable junto al nombre del segmento o utilice el selector de segmentos para abrir el cuadro de diálogo de selección de segmentos.

![](../images/segments/change-segment.png)

![](../images/segments/select-segment-dialog.png)

## Widgets y métricas

El tablero de segmentos está compuesto por utilidades, que son métricas de solo lectura que proporcionan información importante sobre el segmento seleccionado.

La fecha y hora de &quot;última actualización&quot; de un widget muestra cuándo se tomó la última instantánea de los datos. La fecha y la hora de la instantánea se proporcionan en UTC; no se encuentra en la zona horaria del usuario individual o de la organización de IMS.

![](../images/segments/widget-timestamp.png)

## Widgets disponibles

Experience Platform proporciona varias utilidades que puede utilizar para visualizar distintas métricas relacionadas con su segmento. Seleccione el nombre de una utilidad para obtener más información:

* [[!UICONTROL Tamaño de la audiencia]](#audience-size)
* [[!UICONTROL Tendencia del tamaño de la audiencia]](#audience-size-trend)
* [[!UICONTROL Superposición de identidad]](#identity-overlap)
* [[!UICONTROL Perfiles por identidad]](#profiles-by-identity)

### [!UICONTROL Tamaño de la audiencia] {#audience-size}

El widget **[!UICONTROL Audience size]** muestra el número total de perfiles combinados dentro del segmento seleccionado en el momento en que se tomó la instantánea. Este número es el resultado de aplicar la política de combinación de segmentos a los datos de perfil para combinar fragmentos de perfil y formar un único perfil para cada individuo en el segmento.

Para obtener más información sobre los fragmentos y los perfiles combinados, comience por leer la [información general del perfil del cliente en tiempo real](../../profile/home.md).

![](../images/segments/audience-size.png)

### [!UICONTROL Tendencia del tamaño de la audiencia] {#audience-size-trend}

La utilidad **[!UICONTROL Tendencia del tamaño de la audiencia]** proporciona información sobre la cantidad total de perfiles del segmento capturados durante la instantánea diaria, durante los últimos 30 días, 90 días o 12 meses. Este widget muestra cómo el tamaño del segmento puede haber cambiado con el tiempo a medida que nuevos perfiles cumplen los requisitos para el segmento o salen de él.

Para obtener más información sobre la evaluación de segmentos y cómo los perfiles cumplen los requisitos y salen de los segmentos, consulte la [Documentación del servicio de segmentación](../../segmentation/home.md).

![](../images/segments/audience-size-trend.png)

### [!UICONTROL Superposición de identidad] {#identity-overlap}

La utilidad **[!UICONTROL Identity overlap]** muestra un diagrama de Venn o un diagrama de conjunto, que muestra la superposición de perfiles en el segmento que contienen varias identidades.

Después de utilizar los menús desplegables del widget para seleccionar las identidades que desea comparar, aparecen círculos que muestran el tamaño relativo de cada identidad, y el número de perfiles que contienen ambas áreas de nombres se representa por el tamaño de la superposición entre los círculos.

Si un cliente interactúa con su marca en más de un canal, se asociarán varias identidades con ese cliente individual, por lo que es probable que su organización tenga varios perfiles que contengan fragmentos de más de una identidad.

Para obtener más información sobre las identidades, visite la [documentación del servicio de identidad de Adobe Experience Platform](../../identity-service/home.md).

![](../images/segments/identity-overlap.png)

### [!UICONTROL Perfiles por identidad] {#profiles-by-identity}

La utilidad **[!UICONTROL Profiles by identity]** muestra el desglose de identidades en todos los perfiles combinados del segmento seleccionado. El número total de perfiles por identidad puede ser mayor que el número total de perfiles en el segmento porque un perfil podría tener varias identidades asociadas a él. En otras palabras, sumar los valores mostrados para cada identidad puede totalizar más que el tamaño total de audiencia en el segmento porque si un cliente interactúa con su marca en más de un canal, se pueden asociar varias identidades con ese cliente individual.

Para obtener más información sobre las identidades, visite la [documentación del servicio de identidad de Adobe Experience Platform](../../identity-service/home.md).

![](../images/segments/profiles-by-identity.png)

## Pasos siguientes

Al seguir este documento, debería poder localizar el panel de segmentos y seleccionar un segmento para verlo. También debe comprender las métricas que se muestran en los widgets disponibles. Para obtener más información sobre el trabajo con segmentos en la interfaz de usuario del Experience Platform, consulte la [Guía de la interfaz de usuario del servicio de segmentación](../../segmentation/ui/overview.md).
