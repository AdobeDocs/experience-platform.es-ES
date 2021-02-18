---
keywords: Experience Platform;perfil;segmento;segmentos;segmentación;interfaz de usuario;IU;personalización;panel de segmentos;panel
title: Panel de segmentos
description: 'Adobe Experience Platform proporciona un panel mediante el cual puede realizar vistas de información importante sobre los segmentos que ha creado su organización. '
topic: guide
type: Documentation
translation-type: tm+mt
source-git-commit: 2f2459c1c88c97a3ab322b08ee178463fbb4a592
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 1%

---


# (Beta) panel de segmentos {#segment-dashboard}

>[!IMPORTANT]
>
>La funcionalidad de panel descrita en este documento está actualmente en fase beta y no está disponible para todos los usuarios. La documentación y las funciones están sujetas a cambios.

La interfaz de usuario (IU) de Adobe Experience Platform proporciona un panel mediante el cual puede realizar vistas de información importante sobre los segmentos, tal como se captura durante una instantánea diaria. Esta guía describe cómo acceder y trabajar con el panel de segmentos en la interfaz de usuario y proporciona más información sobre las visualizaciones que se muestran en el panel.

Para obtener una descripción general de todas las funciones del servicio de segmentación de Adobe Experience Platform en la interfaz de usuario de la plataforma, visite la [Guía de la interfaz de usuario del servicio de segmentación](../../segmentation/ui/overview.md).

## Datos de panel de segmentos

El panel de segmentos muestra una instantánea de los datos de atributos (registros) que su organización tiene dentro del almacén de Perfiles en Experience Platform. La instantánea no incluye datos de eventos (series temporales).

Los datos de atributo de la instantánea muestran los datos exactamente como aparecen en el momento concreto en que se realizó la instantánea. En otras palabras, la instantánea no es una aproximación o muestra de los datos y el panel del segmento no se actualiza en tiempo real.

>[!NOTE]
>
>Los cambios o actualizaciones realizados en los datos desde que se realizó la instantánea no se reflejarán en el panel hasta que se realice la siguiente instantánea.

## Explorar el panel del segmento

Para desplazarse al panel de segmentos dentro de la interfaz de usuario de la plataforma, seleccione **[!UICONTROL Segmentos]** en el carril izquierdo y, a continuación, seleccione la ficha **[!UICONTROL Información general]** para mostrar el panel.

![](../images/segments/dashboard-overview.png)

### Seleccionar un segmento

El panel seleccionará automáticamente un segmento para mostrar, pero puede cambiar el segmento que se muestra mediante el menú desplegable. Para elegir un segmento diferente, seleccione la lista desplegable junto al nombre del segmento y, a continuación, seleccione el segmento que desee vista.

>[!NOTE]
>
>El menú desplegable muestra todos los segmentos que su organización ha creado hasta ahora. Esto puede significar que tendrá que desplazarse para poder realizar la vista de la lista completa de los segmentos disponibles.

![](../images/segments/change-segment.png)

### Widgets y métricas

El panel de segmentos está compuesto de utilidades, que son métricas de solo lectura que proporcionan información importante con respecto al segmento seleccionado. La fecha y hora &quot;última actualización&quot; de la utilidad muestran cuándo se realizó la última instantánea de los datos.

![](../images/segments/widget-timestamp.png)

## Widgets disponibles

Experience Platform proporciona varias utilidades que puede utilizar para visualizar distintas métricas relacionadas con el segmento. Seleccione el nombre de una utilidad a continuación para obtener más información:

* [[!UICONTROL Tamaño del segmento]](#segment-size)
* [[!UICONTROL Perfiles agregados con el tiempo]](#profiles-added-over-time)
* [[!UICONTROL Perfiles por Área de nombres]](#profiles-by-namespace)

### [!UICONTROL Tamaño del segmento] {#segment-size}

La utilidad **[!UICONTROL Tamaño del segmento]** muestra el número total de perfiles combinados dentro del segmento seleccionado en el momento en que se realizó la instantánea. Este número es el resultado de aplicar la directiva de combinación de segmentos a los datos de Perfil para combinar los fragmentos de perfil y formar un único perfil para cada individuo del segmento.

Para obtener más información sobre fragmentos y perfiles combinados, lea la [información general del Perfil del cliente en tiempo real](../../profile/home.md).

![](../images/segments/segment-size.png)

### [!UICONTROL Perfiles agregados con el tiempo] {#profiles-added-over-time}

La utilidad **[!UICONTROL Perfiles agregados a lo largo del tiempo]** proporciona información sobre el número total de perfiles en el segmento capturados durante la instantánea diaria, durante los últimos 30 días. Esta utilidad muestra cómo el tamaño del segmento puede haber cambiado durante un período de 30 días a medida que los nuevos perfiles cumplen los requisitos para el segmento o salen de él.

Para obtener más información sobre la evaluación de segmentos y cómo los perfiles califican y salen de los segmentos, consulte la [documentación del servicio de segmentación](../../segmentation/home.md).

![](../images/segments/profiles-added-over-time.png)

### [!UICONTROL Perfiles por Área de nombres] {#profiles-by-namespace}

La utilidad **[!UICONTROL Perfiles por Área de nombres]** muestra el desglose de Áreas de nombres en todos los perfiles combinados del segmento seleccionado. El número total de perfiles por Área de nombres de identidad ([!UICONTROL Área de nombres de ID] en la utilidad) puede ser mayor que el número total de perfiles en el segmento porque un perfil podría tener varias Áreas de nombres asociadas. Dicho de otro modo, sumar los valores mostrados para cada Área de nombres puede ser mayor que el total de perfiles en el segmento porque si un cliente interactúa con su marca en más de un canal, se pueden asociar varias Áreas de nombres con ese cliente individual.

Para obtener más información sobre Áreas de nombres de identidad, visite la [documentación del servicio de identidad de Adobe Experience Platform](../../identity-service/home.md).

![](../images/segments/profiles-by-namespace.png)

## Pasos siguientes

Al seguir este documento ahora debería poder localizar el panel del segmento y seleccionar un segmento para la vista. También debe comprender las métricas que se muestran en los widgets disponibles. Para obtener más información sobre cómo trabajar con segmentos en la interfaz de usuario del Experience Platform, consulte la [Guía de la interfaz de usuario del servicio de segmentación](../../segmentation/ui/overview.md).