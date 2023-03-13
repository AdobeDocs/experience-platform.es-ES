---
keywords: Experience Platform;perfil;segmento;segmentos;segmentación;interfaz de usuario;IU;personalización;tablero de segmentos;tablero
title: Guía del panel de segmentos
description: Adobe Experience Platform proporciona un tablero a través del cual puede ver información importante acerca de los segmentos que ha creado su organización.
type: Documentation
exl-id: de5e07bc-2c44-416e-99db-7607059117cb
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '2105'
ht-degree: 0%

---

# [!UICONTROL Segmentos] tablero {#segment-dashboard}

La interfaz de usuario (IU) de Adobe Experience Platform proporciona un tablero a través del cual puede ver información importante acerca de los segmentos, tal como se captura durante una instantánea diaria. Esta guía describe cómo acceder al panel de segmentos en la interfaz de usuario y trabajar con él, y proporciona más información sobre las visualizaciones que se muestran en el panel.

Para obtener una descripción general de todas las funciones del servicio de segmentación de Adobe Experience Platform dentro de la interfaz de usuario de Platform, visite la [Guía de IU del servicio de segmentación](../../segmentation/ui/overview.md).

## [!UICONTROL Segmentos] datos del panel

El panel de segmentos muestra una instantánea de los datos de atributo (registro) que su organización tiene en el almacén de perfiles en Experience Platform. La instantánea no incluye datos de evento (series temporales).

Los datos de atributos de la instantánea muestran los datos exactamente como aparecen en el momento específico en el que se tomó la instantánea. En otras palabras, la instantánea no es una aproximación o una muestra de los datos y el panel de segmentos no se actualiza en tiempo real.

>[!NOTE]
>
>Los cambios o actualizaciones realizados en los datos desde que se tomó la instantánea no se reflejarán en el tablero hasta que se tome la siguiente instantánea.

## Explore la [!UICONTROL Segmentos] tablero {#explore}

Para ir a [!UICONTROL Segmentos] en la IU de Platform, seleccione **[!UICONTROL Segmentos]** en el carril izquierdo, seleccione **[!UICONTROL Información general]** para mostrar el tablero.

>[!NOTE]
>
>Si su organización es nueva en Platform y aún no ha creado conjuntos de datos de perfil o políticas de combinación activos, la variable [!UICONTROL Segmentos] el panel no es visible. En su lugar, la variable [!UICONTROL Información general] La pestaña muestra vínculos y documentación para ayudarle a empezar con la segmentación.

![La pestaña Información general del panel Segmentos con Segmentos e Información general resaltados.](../images/segments/dashboard-overview.png)

### Modifique la [!UICONTROL Segmentos] tablero {#modify}

Puede modificar el aspecto del [!UICONTROL Segmentos] panel seleccionando **[!UICONTROL Modificar tablero]**. Esto le permite mover, añadir y quitar widgets del panel, así como acceder al **[!UICONTROL Biblioteca de widgets]** para explorar los widgets disponibles y crear widgets personalizados para su organización.

Consulte la [modificación de paneles](../customize/modify.md) y [Resumen de biblioteca de widgets](../customize/widget-library.md) para obtener más información.

### Añadir widgets {#add-widget}

Seleccionar **[!UICONTROL Añadir widget]** para desplazarse a la biblioteca de widgets y ver una lista de los widgets disponibles para agregarlos al tablero.

![Información general del panel Segmentos con el widget Agregar resaltado.](../images/segments/segments-overview-add-widget.png)

Desde la biblioteca de widgets, puede examinar la selección de widgets de segmento estándar y personalizados. Para obtener información sobre cómo añadir widgets, consulte la documentación de la biblioteca de widgets sobre cómo [añadir un widget](../customize/widget-library.md#add-widgets).

## Seleccione un segmento

El panel selecciona automáticamente un segmento para mostrar, aunque puede cambiarlo mediante el menú desplegable o el selector de segmentos.

Para elegir un segmento diferente, seleccione la lista desplegable junto al nombre del segmento o utilice el selector de segmentos para abrir el cuadro de diálogo de selección de segmentos.

>[!IMPORTANT]
>
>En la lista de segmentos seleccionables solo se muestran los segmentos con un recuento de perfiles superior a cero.

![Información general del panel Segmentos, con el menú desplegable de segmentos globales resaltado.](../images/segments/change-segment.png)

![El cuadro de diálogo Seleccionar segmento que muestra todos los segmentos disponibles.](../images/segments/select-segment-dialog.png)

## Widgets y métricas

El panel de segmentos está compuesto por widgets, que son métricas de solo lectura que proporcionan información importante sobre el segmento seleccionado.

La fecha y la hora de la instantánea más reciente se muestran en la parte superior de la [!UICONTROL Información general] junto al menú desplegable de segmentos. Todos los datos del widget son precisos a partir de esa fecha y hora. La marca de tiempo de la instantánea se proporciona en formato UTC; no se encuentra en la zona horaria del usuario u organización individual.

![La pestaña Información general de segmentos con una marca de tiempo de widget resaltada.](../images/segments/widget-timestamp.png)

## Widgets estándar {#standard-widgets}

Adobe proporciona varios widgets estándar que puede utilizar para visualizar diferentes métricas relacionadas con los segmentos. También puede crear widgets personalizados para compartirlos con su organización mediante el [!UICONTROL Biblioteca de widgets]. Para obtener más información sobre la creación de widgets personalizados, comience por leer el [Resumen de biblioteca de widgets](../customize/widget-library.md).

Para obtener más información sobre cada uno de los widgets estándar disponibles, seleccione el nombre de un widget en la siguiente lista:

* [[!UICONTROL Tamaño de la audiencia]](#audience-size)
* [[!UICONTROL Orden de activación de audiencia]](#audience-activation-order)
* [[!UICONTROL Tendencia de tamaño de audiencia]](#audience-size-trend)
* [[!UICONTROL Tendencia de cambio de tamaño de audiencia]](#audience-size-change-trend)
* [[!UICONTROL Tendencia del tamaño de la audiencia por identidad]](#audience-size-trend-by-identity)
* [[!UICONTROL Superposición de audiencias]](#audience-overlap)
* [[!UICONTROL Informe de superposición de audiencia]](#audience-overlap-report)
* [[!UICONTROL Superposición de identidad]](#identity-overlap)
* [[!UICONTROL Perfiles por identidad]](#profiles-by-identity)
* [[!UICONTROL Activaciones programadas]](#scheduled-activations)

### [!UICONTROL Tamaño de la audiencia] {#audience-size}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_audiencesize"
>title="Tamaño de la audiencia"
>abstract="Este widget muestra el número total de perfiles combinados dentro del segmento seleccionado. Este número depende de la política de combinación aplicada a los datos y es correcto en el momento de la instantánea más reciente."

El **[!UICONTROL Tamaño de audiencia]** widget muestra el número total de perfiles combinados dentro del segmento seleccionado en el momento en que se tomó la instantánea. Este número es el resultado de aplicar la política de combinación de segmentos a los datos del perfil para combinar fragmentos de perfil y formar un único perfil para cada individuo en el segmento.

Para obtener más información sobre fragmentos y perfiles combinados, consulte la [Resumen del perfil del cliente en tiempo real](../../profile/home.md).

![Información general del panel Segmentos con el widget de tamaño de audiencia resaltado.](../images/segments/audience-size.png)

### [!UICONTROL Tendencia de tamaño de audiencia] {#audience-size-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_audiencesizetrend"
>title="Tendencia de tamaño de audiencia"
>abstract="Este widget proporciona información sobre el número total de perfiles que cumplen los criterios de **cualquiera** definición del segmento, según se captura durante la captura diaria, durante los últimos 30 días, 90 días o 12 meses."

El **[!UICONTROL Tendencia de tamaño de audiencia]** El widget proporciona una ilustración de gráfico de líneas para el número total de perfiles que cumplen los criterios de **cualquiera** definición del segmento durante un periodo determinado. La tendencia del tamaño de la audiencia se puede visualizar en períodos de 30 días, 90 días y 12 meses. El período de tiempo se elige en un menú desplegable del widget. El tamaño de la audiencia se refleja en el eje y y el tiempo en el eje x.

Este widget también incluye el [!UICONTROL Subtítulos] función en la que un modelo de aprendizaje automático analiza los datos de gráficos y segmentos y genera automáticamente subtítulos para describir las tendencias clave y los eventos importantes. Seleccionar **[!UICONTROL Subtítulos]** para abrir el diálogo subtítulos automáticos.

![La Información general de segmentos muestra el widget de tendencia de tamaño de audiencia.](../images/segments/audience-size-trend-captions.png)

El cuadro de diálogo de subtítulos automáticos se abre para proporcionar información sobre los datos.

![Cuadro de diálogo de subtítulos automáticos para el widget de tendencia de tamaño de audiencia.](../images/segments/audience-size-trend-automatic-captions-dialog.png)

Para obtener más información sobre la evaluación de segmentos y cómo los perfiles cumplen los requisitos y salen de los segmentos, consulte la [Documentación del Servicio de segmentación](../../segmentation/home.md).

### [!UICONTROL Tendencia de cambio de tamaño de audiencia] {#audience-size-change-trend}

Este widget proporciona un gráfico de líneas que ilustra la diferencia en el número total de perfiles aptos para un segmento determinado entre las instantáneas diarias más recientes. El segmento elegido para el análisis se selecciona en la lista desplegable de información general. El periodo de análisis de tendencias se puede visualizar en periodos de 30 días, 90 días y 12 meses. El período de tiempo se elige en un menú desplegable del widget. El tamaño de la audiencia se refleja en el eje y y el tiempo en el eje x.

![El widget de tendencia Cambio de tamaño de audiencia.](../images/segments/audience-size-change-trend.png)

### [!UICONTROL Tendencia del tamaño de la audiencia por identidad] {#audience-size-trend-by-identity}

Este widget ilustra la tendencia del tamaño de la audiencia de un segmento en particular en función del tipo de identidad elegido en el menú desplegable del widget. El segmento utilizado para el análisis se selecciona en la lista desplegable de información general. El periodo de análisis de tendencias se puede visualizar en periodos de 30 días, 90 días y 12 meses. El período de tiempo se elige en un menú desplegable del widget.

![La tendencia del tamaño de la audiencia por widget de identidad.](../images/segments/audience-size-trend-by-identity.png)

### [!UICONTROL Orden de activación de audiencia] {#audience-activation-order}

El [!UICONTROL Orden de activación de audiencia] El widget proporciona una tabla de tres columnas que enumera las variables [!UICONTROL nombre de destino], el [!UICONTROL plataforma]y la activación [!UICONTROL fecha] de la audiencia. La lista se ordena de alta a baja según la actualización y puede alojar hasta 10 filas.

![El widget de orden de activación de Audiencia.](../images/segments/audience-activation-order.png)

### [!UICONTROL Superposición de audiencias] {#audience-overlap}

Este widget representa el número de perfiles de dos segmentos que cumplen los criterios de ambas definiciones de segmentos. Los segmentos utilizados para la comparación se seleccionan en los menús desplegables de widgets. El número total de perfiles contenidos dentro de la definición del segmento correspondiente se puede ver pasando el ratón por encima de un círculo o de la intersección del diagrama de Venn.

Este widget le permite optimizar su estrategia de segmentación mediante la visualización de las similitudes en los resultados de las definiciones de segmentos.

![El widget de superposición de audiencias.](../images/segments/audience-overlap.png)

### [!UICONTROL Informe de superposición de audiencia] {#audience-overlap-report}

Este widget tabula los datos de superposición de audiencias de un segmento específico. Se proporciona una lista de cinco audiencias clasificadas entre los porcentajes de superposición más altos y más bajos para el segmento elegido en el menú desplegable de la parte superior de la pantalla. Para mayor claridad, el segmento elegido se enumera en la variable [!UICONTROL NOMBRE DEL SEGMENTO A] columna. Se proporciona un análisis de superposición de audiencias para el segundo segmento enumerado en la variable [!UICONTROL NOMBRE DEL SEGMENTO B] columna. La superposición porcentual se indica en la tercera columna con una precisión de doce decimales.

El informe de superposición de audiencias le ayuda a crear nuevos segmentos de alto rendimiento. La observación de superposiciones de alto porcentaje le permite suprimir audiencias e impedir que se envíe la misma audiencia a diferentes destinos. También le ayudan a identificar perspectivas ocultas que pueden ayudarle con una mejor segmentación. La superposición de bajo porcentaje ayuda a localizar perfiles únicos que perseguir.

Seleccionar **[!UICONTROL Ver más]** para abrir un cuadro de diálogo de pantalla completa que contenga más datos de superposición de segmentos.

![El widget Informe de superposición de audiencias con la opción Ver más resaltada](../images/segments/audience-overlap-report.png)

El [!UICONTROL Informe de superposición de audiencia] aparece el cuadro de diálogo. Este cuadro de diálogo puede contener hasta 50 filas de análisis de superposición de audiencias divididas en seis columnas. Seleccione el icono de configuración (![El icono de configuración.](../images/segments/settings-icon.png)) para quitar o agregar columnas de la tabla.

![Cuadro de diálogo Informe de superposición de audiencias.](../images/segments/audience-overlap-report-dialog.png)

>[!NOTE]
>
>Seleccione el **[!UICONTROL Superposición]** encabezado de columna para cambiar la clasificación de los resultados entre mayor a menor o menor a mayor.

Para descargar todo el informe en formato de PDF, seleccione el menú de opciones (**`...`**) seguido de **[!UICONTROL Descargar]**.

![El cuadro de diálogo Informe de superposición de audiencias con los puntos suspensivos y la opción Descargar resaltadas.](../images/segments/segments-audience-overlap-report-dialog-download.png)

Seleccione una fila del informe para abrir un diagrama de Venn del análisis de superposición. Pase el ratón sobre una sección del diagrama de Venn para ver el recuento de perfiles en un cuadro de diálogo.

![Cuadro de diálogo Informe de superposición de audiencias con un diagrama de Venn y una fila resaltada.](../images/segments/audience-overlap-report-dialog-venn.png)

Seleccionar **[!UICONTROL Cerrar]** para volver a la [!UICONTROL Segmentos] panel.

### [!UICONTROL Superposición de identidad] {#identity-overlap}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_identityoverlap"
>title="Superposición de identidad"
>abstract="Este widget muestra la superposición de perfiles en el segmento que contiene ambas identidades seleccionadas. Los círculos muestran el tamaño relativo de cada identidad. El número de perfiles que contienen ambas áreas de nombres se representa mediante la superposición entre los círculos."

El **[!UICONTROL Superposición de identidad]** Este widget muestra un diagrama de Venn o un diagrama de conjunto que muestra la superposición de perfiles en el segmento que contiene varias identidades.

Utilice los menús desplegables del widget para seleccionar las identidades que desea comparar. Los círculos muestran el tamaño relativo de cada identidad elegida, y el número de perfiles que contienen ambas áreas de nombres se representa mediante el tamaño de la superposición entre los círculos.

Si un cliente interactúa con su marca en más de un canal, se asociarán varias identidades a ese cliente individual, por lo que es probable que su organización tenga varios perfiles que contengan fragmentos de más de una identidad.

Para obtener más información sobre las identidades, visite la [Documentación del servicio de identidad de Adobe Experience Platform](../../identity-service/home.md).

![Información general del panel Segmentos con el widget de superposición de identidad resaltado.](../images/segments/identity-overlap.png)

### [!UICONTROL Perfiles por identidad] {#profiles-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_profilesbyidentity"
>title="Perfiles por identidad"
>abstract="Este widget muestra el desglose de identidades en cada perfil combinado del segmento seleccionado."

El **[!UICONTROL Perfiles por identidad]** widget muestra el desglose de identidades en cada perfil combinado del segmento seleccionado. El número total de perfiles por identidad puede ser superior al número total de perfiles en el segmento, ya que un perfil podría tener varias identidades asociadas. En otras palabras, sumar los valores mostrados para cada identidad puede sumar más que el tamaño total de la audiencia en el segmento, ya que si un cliente interactúa con su marca en más de un canal, pueden asociarse varias identidades con ese cliente individual.

Seleccionar **[!UICONTROL Subtítulos]** para abrir el diálogo subtítulos automáticos.

![Información general del panel Segmentos con el widget Perfiles por identidad y la opción Subtítulos resaltados.](../images/segments/profiles-by-identity.png)

Un modelo de aprendizaje automático genera automáticamente perspectivas de datos analizando la distribución general y las dimensiones clave de los datos.

Para obtener más información sobre las identidades, visite la [Documentación del servicio de identidad de Adobe Experience Platform](../../identity-service/home.md).

### Activaciones programadas {#scheduled-activations}

El [!UICONTROL Activaciones programadas] El widget proporciona una vista tabulada de los destinos activados más recientemente. La tabla incluye la plataforma de destino, el nombre del flujo de activación a este destino y las fechas de inicio y finalización de la activación del segmento seleccionado. Si no se proporciona ninguna fecha de finalización para la activación, se muestra como [!UICONTROL En curso]. El segmento a analizar se selecciona en el menú desplegable situado en la parte superior de la página.

El widget permite descubrir de un vistazo dónde y cuándo se está activando la audiencia, y hace que las activaciones duplicadas o innecesarias sean más transparentes. Esta información acumulada también resalta dónde se ha dejado de lado cualquier activación.

![El widget Activaciones programadas.](../images/segments/scheduled-activations.png)

## Pasos siguientes

Al seguir este documento, debería poder localizar el panel de segmentos y seleccionar un segmento para verlo. También debe comprender las métricas que se muestran en los widgets disponibles. Para obtener más información sobre cómo trabajar con segmentos en la interfaz de usuario de Experience Platform, consulte [Guía de IU del servicio de segmentación](../../segmentation/ui/overview.md).
