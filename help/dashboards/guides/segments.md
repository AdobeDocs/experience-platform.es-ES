---
keywords: Experience Platform;perfil;segmento;segmentos;segmentación;interfaz de usuario;IU;personalización;panel de segmentos;tablero
title: Segments Dashboard
description: 'Adobe Experience Platform proporciona un tablero a través del cual puede ver información importante sobre los segmentos que su organización ha creado. '
type: Documentation
exl-id: de5e07bc-2c44-416e-99db-7607059117cb
source-git-commit: b4cd7bc0d8c038346aacdda7c4c9def12864065c
workflow-type: tm+mt
source-wordcount: '1232'
ht-degree: 0%

---

# Segments dashboard {#segment-dashboard}

La interfaz de usuario (IU) de Adobe Experience Platform proporciona un tablero a través del cual puede ver información importante sobre sus segmentos, tal como se captura durante una instantánea diaria. This guide outlines how to access and work with the segments dashboard in the UI and provides more information regarding the visualizations displayed in the dashboard.

For an overview of all of the Adobe Experience Platform Segmentation Service features within the Platform user interface, please visit the [Segmentation Service UI guide](../../segmentation/ui/overview.md).

## Datos del tablero de segmentos

The segment dashboard displays a snapshot of the attribute (record) data that your organization has within the Profile store in Experience Platform. La instantánea no incluye datos de ningún evento (serie temporal).

The attribute data in the snapshot shows the data exactly as it appears at the specific point in time when the snapshot was taken. In other words, the snapshot is not an approximation or sample of the data, and the segment dashboard is not updating in real-time.

>[!NOTE]
>
>Los cambios o actualizaciones realizados en los datos desde que se tomó la instantánea no se reflejarán en el panel hasta que se tome la siguiente instantánea.

## Exploración del panel de segmentos

Para ir a la [!UICONTROL Segmentos] tablero en la interfaz de usuario de Platform, seleccione **[!UICONTROL Segmentos]** en el carril izquierdo, seleccione la opción **[!UICONTROL Información general]** para mostrar el tablero.

>[!NOTE]
>
>If your organization is new to Platform and does not yet have active Profile datasets or merge policies created, the [!UICONTROL Segments] dashboard is not visible. En su lugar, la variable [!UICONTROL Información general] muestra vínculos y documentación para ayudarle a empezar con la segmentación.

![](../images/segments/dashboard-overview.png)

### Modificación de la variable [!UICONTROL Segmentos] tablero

You can modify the appearance of the [!UICONTROL Segments] dashboard by selecting **[!UICONTROL Modify dashboard]**. Esto le permite mover, agregar y quitar widgets del tablero, así como acceder al **[!UICONTROL Biblioteca de utilidades]** para explorar las utilidades disponibles y crear utilidades personalizadas para su organización.

Consulte la [modificación de tableros](../customize/modify.md) y [Información general de la biblioteca de utilidades](../customize/widget-library.md) documentación para obtener más información.

## Seleccionar un segmento

El tablero selecciona automáticamente un segmento para mostrar, aunque puede cambiarlo con el menú desplegable o el selector de segmentos.

Para elegir un segmento diferente, seleccione la lista desplegable junto al nombre del segmento o utilice el selector de segmentos para abrir el cuadro de diálogo de selección de segmentos.

![](../images/segments/change-segment.png)

![](../images/segments/select-segment-dialog.png)

## Widgets y métricas

El tablero de segmentos está compuesto por utilidades, que son métricas de solo lectura que proporcionan información importante sobre el segmento seleccionado.

La fecha y hora de &quot;última actualización&quot; de un widget muestra cuándo se tomó la última instantánea de los datos. The date and time of the snapshot are provided in UTC; it is not in the timezone of the individual user or IMS Organization.

![](../images/segments/widget-timestamp.png)

## Widgets estándar

Adobe proporciona varios widgets estándar que puede utilizar para visualizar distintas métricas relacionadas con los segmentos. También puede crear utilidades personalizadas para compartirlas con su organización mediante la [!UICONTROL Biblioteca de utilidades]. Para obtener más información sobre la creación de widgets personalizados, lea la [Información general de la biblioteca de utilidades](../customize/widget-library.md).

Para obtener más información sobre cada uno de los widgets estándar disponibles, seleccione el nombre de un widget en la siguiente lista:

* [[!UICONTROL Tamaño de la audiencia]](#audience-size)
* [[!UICONTROL Superposición de identidad]](#identity-overlap)
* [[!UICONTROL Perfiles por identidad]](#profiles-by-identity)
* [[!UICONTROL Orden de activación de la audiencia]](#audience-activation-order)
* [[!UICONTROL Tendencia del tamaño de la audiencia]](#audience-size-trend)
* [[!UICONTROL Audience size change trend]](#audience-size-change-trend)
* [[!UICONTROL Tendencia del tamaño de la audiencia por identidad]](#audience-size-trend-by-identity)

### [!UICONTROL Audience size] {#audience-size}

La variable **[!UICONTROL Tamaño de la audiencia]** muestra el número total de perfiles combinados dentro del segmento seleccionado en el momento en que se tomó la instantánea. Este número es el resultado de aplicar la política de combinación de segmentos a los datos de perfil para combinar fragmentos de perfil y formar un único perfil para cada individuo en el segmento.

For more information on fragments and merged profiles, please begin by reading the [Real-time Customer Profile overview](../../profile/home.md).

![](../images/segments/audience-size.png)

### [!UICONTROL Superposición de identidad] {#identity-overlap}

La variable **[!UICONTROL Superposición de identidad]** La utilidad muestra un diagrama de Venn o un diagrama de conjunto que muestra la superposición de perfiles en el segmento que contiene varias identidades.

After using the dropdown menus on the widget to select the identities that you wish to compare, circles appear displaying the relative size of each identity, with the number of profiles containing both namespaces being represented by the size of the overlap between the circles.

Si un cliente interactúa con su marca en más de un canal, se asociarán varias identidades con ese cliente individual, por lo que es probable que su organización tenga varios perfiles que contengan fragmentos de más de una identidad.

Para obtener más información sobre las identidades, visite [Documentación del servicio de identidad de Adobe Experience Platform](../../identity-service/home.md).

![](../images/segments/identity-overlap.png)

### [!UICONTROL Profiles by identity] {#profiles-by-identity}

The **[!UICONTROL Profiles by identity]** widget displays the breakdown of identities across all of the merged profiles in your selected segment. El número total de perfiles por identidad puede ser mayor que el número total de perfiles en el segmento porque un perfil podría tener varias identidades asociadas a él. In other words, adding together the values shown for each identity may total more than the total audience size in the segment because if a customer interacts with your brand on more than one channel, multiple identities may be associated with that individual customer.

Select **[!UICONTROL Subtítulos]** para abrir el cuadro de diálogo rótulos automáticos.

![The profiles by identity captions dialog.](../images/segments/profiles-by-identity.png)

Un modelo de aprendizaje automático genera automáticamente perspectivas de datos analizando la distribución general y las dimensiones clave de los datos.

To learn more about identities, please visit the [Adobe Experience Platform Identity Service documentation](../../identity-service/home.md).

### [!UICONTROL Audience activation order] {#audience-activation-order}

La variable [!UICONTROL Orden de activación de la audiencia] proporciona una tabla de tres columnas que enumera las [!UICONTROL nombre de destino], el [!UICONTROL platform]y la activación [!UICONTROL date] de la audiencia. The list is ordered from high to low according to recency and can accommodate up to 10 rows.

![El widget de orden de activación de audiencias.](../images/segments/audience-activation-order.png)

### [!UICONTROL Tendencia del tamaño de la audiencia] {#audience-size-trend}

La variable [!UICONTROL Tendencia del tamaño de la audiencia] proporciona una ilustración de gráfico de líneas para el número total de perfiles que cumplen los criterios de **any** definición de segmento durante un período de tiempo determinado. La tendencia del tamaño de la audiencia se puede visualizar en periodos de 30 días, 90 días y 12 meses. El periodo de tiempo se elige en un menú desplegable del widget. El tamaño de la audiencia se refleja en el eje y y en el tiempo en el eje x.

![El widget de tendencia del tamaño de la audiencia.](../images/segments/audience-size-trend.png)

### [!UICONTROL Audience size change trend] {#audience-size-change-trend}

Esta utilidad proporciona un gráfico de líneas con la diferencia en la cantidad total de perfiles que cumplen los requisitos para un segmento determinado entre las instantáneas diarias más recientes. The segment chosen for analysis is selected from the overview dropdown. El período de análisis de tendencias se puede visualizar a lo largo de 30 días, 90 días y 12 meses. El periodo de tiempo se elige en un menú desplegable del widget. El tamaño de la audiencia se refleja en el eje y y en el tiempo en el eje x.

![El widget de tendencia del cambio de tamaño de la audiencia.](../images/segments/audience-size-change-trend.png)

### [!UICONTROL Audience size trend by identity] {#audience-size-trend-by-identity}

Esta utilidad ilustra la tendencia del tamaño de la audiencia de un segmento concreto en función del tipo de identidad elegido en el menú desplegable de la utilidad. The segment used for analysis is selected from the overview dropdown. The period of trend analysis can be visualized over 30 days, 90 days, and 12 month periods. El periodo de tiempo se elige en un menú desplegable del widget.

![La tendencia del tamaño de la audiencia por widget de identidad.](../images/segments/audience-size-trend-by-identity.png)

## Pasos siguientes

Al seguir este documento, debería poder localizar el panel de segmentos y seleccionar un segmento para verlo. También debe comprender las métricas que se muestran en los widgets disponibles. Para obtener más información sobre el trabajo con segmentos en la interfaz de usuario del Experience Platform, consulte la [Guía de la interfaz de usuario del servicio de segmentación](../../segmentation/ui/overview.md).
