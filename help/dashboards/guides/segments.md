---
keywords: Experience Platform;perfil;segmento;segmentos;segmentación;interfaz de usuario;IU;personalización;panel de segmentos;tablero
title: Tablero de segmentos
description: 'Adobe Experience Platform proporciona un tablero a través del cual puede ver información importante sobre los segmentos que su organización ha creado. '
topic-legacy: guide
type: Documentation
exl-id: de5e07bc-2c44-416e-99db-7607059117cb
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 1%

---

# (Beta) Panel de segmentos {#segment-dashboard}

>[!IMPORTANT]
>
>La funcionalidad de tablero descrita en este documento está actualmente en fase beta y no está disponible para todos los usuarios. La documentación y las funciones están sujetas a cambios.

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

### Seleccionar un segmento

El tablero seleccionará automáticamente un segmento para mostrar, pero puede cambiar el segmento que se muestra mediante el menú desplegable. Para elegir un segmento diferente, seleccione la lista desplegable junto al nombre del segmento y, a continuación, seleccione el segmento que desee ver.

>[!NOTE]
>
>El menú desplegable muestra todos los segmentos que su organización ha creado hasta el momento. Esto puede significar que tendrá que desplazarse para ver la lista completa de segmentos disponibles.

![](../images/segments/change-segment.png)

### Widgets y métricas

El tablero de segmentos está compuesto por utilidades, que son métricas de solo lectura que proporcionan información importante sobre el segmento seleccionado. La fecha y hora de &quot;última actualización&quot; del widget muestran cuándo se realizó la última instantánea de los datos.

![](../images/segments/widget-timestamp.png)

## Widgets disponibles

Experience Platform proporciona varias utilidades que puede utilizar para visualizar distintas métricas relacionadas con su segmento. Seleccione el nombre de una utilidad para obtener más información:

* [[!UICONTROL Segment size]](#segment-size)
* [[!UICONTROL Profiles added over time]](#profiles-added-over-time)
* [[!UICONTROL Profiles by namespace]](#profiles-by-namespace)

### [!UICONTROL Segment size] {#segment-size}

La utilidad **[!UICONTROL Segment size]** muestra el número total de perfiles combinados dentro del segmento seleccionado en el momento en que se tomó la instantánea. Este número es el resultado de aplicar la política de combinación de segmentos a los datos de perfil para combinar fragmentos de perfil y formar un único perfil para cada individuo en el segmento.

Para obtener más información sobre los fragmentos y los perfiles combinados, comience por leer la [información general del perfil del cliente en tiempo real](../../profile/home.md).

![](../images/segments/segment-size.png)

### [!UICONTROL Profiles added over time] {#profiles-added-over-time}

La utilidad **[!UICONTROL Profiles added over time]** proporciona información sobre la cantidad total de perfiles del segmento capturados durante la instantánea diaria durante los últimos 30 días. Este widget muestra cómo el tamaño del segmento puede haber cambiado durante un periodo de 30 días a medida que nuevos perfiles cumplen los requisitos para el segmento o salen de él.

Para obtener más información sobre la evaluación de segmentos y cómo los perfiles cumplen los requisitos y salen de los segmentos, consulte la [Documentación del servicio de segmentación](../../segmentation/home.md).

![](../images/segments/profiles-added-over-time.png)

### [!UICONTROL Profiles by namespace] {#profiles-by-namespace}

La utilidad **[!UICONTROL Profiles by namespace]** muestra el desglose de áreas de nombres en todos los perfiles combinados del segmento seleccionado. El número total de perfiles por área de nombres de identidad ([!UICONTROL ID namespace] en la utilidad) puede ser mayor que el número total de perfiles en el segmento porque un perfil podría tener varias áreas de nombres asociadas. En otras palabras, sumar los valores mostrados para cada área de nombres puede totalizar más que los perfiles totales del segmento porque si un cliente interactúa con la marca en más de un canal, se pueden asociar varias áreas de nombres con ese cliente individual.

Para obtener más información sobre áreas de nombres de identidad, visite la [documentación del servicio de identidad de Adobe Experience Platform](../../identity-service/home.md).

![](../images/segments/profiles-by-namespace.png)

## Pasos siguientes

Al seguir este documento, debería poder localizar el panel de segmentos y seleccionar un segmento para verlo. También debe comprender las métricas que se muestran en los widgets disponibles. Para obtener más información sobre el trabajo con segmentos en la interfaz de usuario del Experience Platform, consulte la [Guía de la interfaz de usuario del servicio de segmentación](../../segmentation/ui/overview.md).
