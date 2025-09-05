---
keywords: Experience Platform;perfil;audiencia;audiencias;segmentación;interfaz de usuario;IU;personalización;tablero de audiencias;tablero
title: Tablero de audiencias
description: Adobe Experience Platform proporciona un tablero a través del cual puede ver información importante acerca de las audiencias que ha creado su organización.
type: Documentation
exl-id: de5e07bc-2c44-416e-99db-7607059117cb
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '3136'
ht-degree: 9%

---

# Panel [!UICONTROL Audiencias] {#audiences-dashboard}

La interfaz de usuario (IU) de Adobe Experience Platform proporciona un tablero a través del cual puede ver información importante acerca de sus audiencias, tal como se captura durante una instantánea diaria. Esta guía describe cómo acceder y trabajar con el panel [!UICONTROL Audiencias] en la interfaz de usuario y proporciona más información sobre las visualizaciones que se muestran en el panel.

Para obtener una descripción general de todas las características del servicio de segmentación de Adobe Experience Platform dentro de la interfaz de usuario de Experience Platform, visite la [guía de la interfaz de usuario del servicio de segmentación](../../segmentation/ui/overview.md).

## [!UICONTROL Audiencias] datos de panel

El panel [!UICONTROL Audiencias] muestra una instantánea de los datos de atributo (registro) que su organización tiene en el almacén de perfiles en Experience Platform. La instantánea no incluye datos de evento (series temporales).

Los datos de atributos de la instantánea muestran los datos exactamente como aparecen en el momento específico en el que se tomó la instantánea. En otras palabras, la instantánea no es una aproximación o una muestra de los datos y el panel [!UICONTROL Audiencias] no se actualiza en tiempo real.

>[!NOTE]
>
>Los cambios o actualizaciones realizados en los datos desde que se tomó la instantánea no se reflejarán en el tablero hasta que se tome la siguiente instantánea.

## Explorar el panel [!UICONTROL Audiencias] {#explore}

Para ir al panel [!UICONTROL Audiencias] en la interfaz de usuario de Experience Platform, selecciona **[!UICONTROL Audiencias]** en el carril izquierdo y, a continuación, selecciona la pestaña **[!UICONTROL Información general]** para mostrar el panel.

>[!NOTE]
>
>Si su organización es nueva en Experience Platform y aún no ha creado conjuntos de datos de perfil o políticas de combinación activos, el panel [!UICONTROL Audiencias] no estará visible. En su lugar, la pestaña [!UICONTROL Información general] muestra vínculos y documentación para ayudarle a empezar con la segmentación.

![La pestaña [!UICONTROL Audiencias] del panel [!UICONTROL Información general] con [!UICONTROL Audiencias] y [!UICONTROL Información general] resaltadas.](../images/audiences/dashboard-overview.png)

### Modificar el panel [!UICONTROL Audiencias] {#modify}

Puede modificar el aspecto del panel [!UICONTROL Audiencias] seleccionando **[!UICONTROL Modificar panel]**. Esto le permite mover, agregar y quitar widgets del tablero, así como acceder a la **[!UICONTROL biblioteca de widgets]** para explorar los widgets disponibles y crear widgets personalizados para su organización.

Consulte la documentación de [modificación de paneles](../customize/modify.md) y [descripción general de la biblioteca de widgets](../customize/widget-library.md) para obtener más información.

### Añadir widgets {#add-widget}

Seleccione **[!UICONTROL Agregar widget]** para navegar a la biblioteca de widgets y ver una lista de los widgets disponibles para agregar al tablero.

![Resumen del panel de [!UICONTROL Audiencias] con [!UICONTROL Agregar widget] resaltado.](../images/audiences/audiences-overview-add-widget.png)

Desde la biblioteca de widgets, puede examinar la selección de widgets de audiencia estándar y personalizados. Para obtener información sobre cómo agregar widgets, consulte la documentación de la biblioteca de widgets sobre cómo [agregar un widget](../customize/widget-library.md#add-widgets).

### Ver SQL {#view-sql}

Puede ver el SQL que genera las perspectivas visualizadas en su panel con un conmutador en el espacio de trabajo [!UICONTROL Información general]. Puede inspirarse en el SQL de sus perspectivas existentes para crear nuevas consultas que deriven perspectivas únicas de los datos de Experience Platform en función de sus necesidades comerciales. Para obtener más información acerca de esta característica, consulte la [Guía de la interfaz de usuario de SQL de vista](../view-sql.md).

## Seleccionar una audiencia {#select-audience}

El panel selecciona automáticamente una audiencia para mostrarla. Sin embargo, puede cambiar la audiencia mediante el menú desplegable o el selector de audiencia.

Para elegir otra audiencia, seleccione la lista desplegable junto al nombre de la audiencia o utilice el selector de audiencia para abrir el cuadro de diálogo de selección de audiencias.

>[!IMPORTANT]
>
>En la lista de audiencias seleccionables solo se muestran las audiencias con un recuento de perfiles superior a cero.

![Información general del panel Audiencias con el menú desplegable de audiencia global resaltado.](../images/audiences/change-audience.png)

![Cuadro de diálogo [!UICONTROL Seleccionar audiencia] que muestra todas las audiencias disponibles.](../images/audiences/select-audience-dialog.png)

## Widgets y métricas {#widgets-and-metrics}

El panel [!UICONTROL Audiencias] está compuesto por widgets, que son métricas de solo lectura que proporcionan información importante sobre la audiencia seleccionada.

La fecha y la hora de la instantánea más reciente se muestran en la parte superior de la pestaña [!UICONTROL Información general] junto al menú desplegable de audiencia. Todos los datos del widget son precisos a partir de esa fecha y hora. La marca de tiempo de la instantánea se proporciona en formato UTC; no se encuentra en la zona horaria del usuario u organización individual.

![La ficha Información general de audiencias con una marca de tiempo de widget resaltada.](../images/audiences/widget-timestamp.png)

## Widgets predeterminados {#default-widgets}

Se proporciona una carga de widget predeterminada para todas las instancias nuevas de Adobe Experience Platform que resalta las perspectivas disponibles más recientes de sus datos. Los siguientes widgets están preconfigurados en la vista de segmentos desde el principio. Puede encontrar todos los detalles sobre el propósito y la función de los widgets en sus secciones respectivas.

* [[!UICONTROL Tamaño de público]](#audience-size)
* [[!UICONTROL Tendencia de cambio de tamaño de audiencia]](#audience-size-change-trend)
* [[!UICONTROL Superposición de identidad]](#identity-overlap)
* [[!UICONTROL Perfiles por identidad]](#profiles-by-identity)

>[!NOTE]
>
>El 26 de julio de 2023, los paneles de [!UICONTROL Perfiles], [!UICONTROL Audiencias] y [!UICONTROL Destinos] de Información general se restablecieron a una nueva carga de widget predeterminada para todos los usuarios que no modificaron sus vistas en los seis meses anteriores.
>>Consulte la documentación en las secciones de widgets predeterminados de [Perfiles](./profiles.md#default-widgets) y [Destinos](./destinations.md#default-widgets) para obtener detalles sobre qué widgets se incluyen como parte de las cargas de widgets predeterminados. Puede seguir personalizando los widgets del tablero como antes.

## Widgets de Customer AI {#customer-ai-audiences-widgets}

La AI del cliente se utiliza para generar puntuaciones de tendencia personalizadas, como la generación y la conversión de perfiles individuales a escala. La inteligencia artificial aplicada al cliente lo hace analizando los datos de evento de experiencia del consumidor existentes para predecir **puntuaciones de tendencia de pérdida o conversión**. Estos modelos de tendencia de los clientes de alta precisión permiten una segmentación y una segmentación más exactas. La [distribución de puntuaciones](#customer-ai-distribution-of-scores) y las perspectivas de [resumen de puntuación](#customer-ai-scoring-summary) demuestran la división en su audiencia. Resaltan qué perfiles son los de tendencia alta/baja/media y cómo se distribuyen en los recuentos de perfiles.

* [[!UICONTROL Resumen de puntuación de inteligencia artificial aplicada al cliente]](#customer-ai-scoring-summary)
* [[!UICONTROL Distribución de puntuaciones de inteligencia artificial aplicada al cliente]](#customer-ai-distribution-of-scores)

### [!UICONTROL Distribución de puntuaciones de inteligencia artificial aplicada al cliente] {#customer-ai-distribution-of-scores}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_distributionOfScores"
>title="Distribución de las puntuaciones"
>abstract="Este widget visualiza la distribución del número total de perfiles por sus puntuaciones de tendencia en incrementos de cinco por ciento. La distribución del recuento de perfiles viene determinada por el modelo de inteligencia artificial y las políticas de combinación seleccionadas. Puede cambiar el modelo de inteligencia artificial desde el menú desplegable debajo del título del widget."

El widget de distribución de puntuaciones [!UICONTROL Customer AI] categoriza el número total de perfiles según sus puntuaciones de tendencia. La distribución del recuento de perfiles viene determinada por el modelo de IA y la política de combinación seleccionada y, a continuación, se visualiza en incrementos de cinco por ciento que indican su tendencia. El recuento de perfiles se proporciona a lo largo del eje Y y las puntuaciones de tendencia se proporcionan a lo largo del eje X.

>[!NOTE]
>
>Si la visualización es una puntuación de tendencia de conversión, las puntuaciones más altas se muestran en verde y las más bajas en rojo. Si predice una tendencia a la pérdida invertida, las puntuaciones más altas están en rojo y las más bajas en verde. El cubo mediano permanece amarillo independientemente del tipo de tendencia que elija.

El modelo de IA que determina las puntuaciones de tendencia se elige del selector desplegable debajo del título del widget. La lista desplegable contiene una lista de todos los modelos de inteligencia artificial aplicada al cliente configurados. Seleccione el modelo de IA adecuado para el análisis en la lista de modelos disponibles. Si no hay ningún modelo de inteligencia artificial aplicada al cliente disponible, un mensaje dentro del widget le indica que configure al menos un modelo de inteligencia artificial aplicada al cliente y proporciona un hipervínculo a la página de configuración del modelo de inteligencia artificial aplicada al cliente. Consulte la documentación para obtener instrucciones sobre [cómo configurar una instancia de inteligencia artificial aplicada al cliente](../../intelligent-services/customer-ai/user-guide/configure.md).

>[!NOTE]
>
>Seleccione el menú desplegable situado inmediatamente debajo de la pestaña Información general para cambiar la política de combinación que determina qué perfiles se incluyen en el análisis. Consulte la sección sobre [políticas de combinación](#merge-policies) para obtener una breve descripción o la [descripción general de la política de combinación](../../profile/merge-policies/overview.md) para obtener más detalles.

Para ir a la página de detalles del modelo de inteligencia artificial aplicada al cliente seleccionado, seleccione **[!UICONTROL Ver detalles del modelo]**.

![Se ha resaltado el panel Audiencias de Experience Platform con la distribución de puntuaciones[!UICONTROL  de la inteligencia artificial aplicada al cliente y el widget ]Ver detalles del modelo[!UICONTROL .]](../images/segments/customer-ai-distribution-of-scores.png)

Aparecerá la página de información detallada del modelo.

![Página de información para la inteligencia artificial aplicada al cliente.](../images/profiles/customer-ai-insights-page.png)

Encontrará más información sobre inteligencia artificial aplicada al cliente en la [guía de la interfaz de usuario de Discover insights](../../intelligent-services/customer-ai/user-guide/discover-insights.md).

### [!UICONTROL Resumen de puntuación de inteligencia artificial aplicada al cliente] {#customer-ai-scoring-summary}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_scoringSummary"
>title="Resumen de las puntuaciones"
>abstract="Este widget muestra el número total de perfiles puntuados y los clasifica en bloques que contienen una tendencia alta, media y baja. El gráfico de anillo ilustra la composición proporcional de los perfiles totales en las tendencias alta, media y baja."

Este widget muestra el número total de perfiles marcados y los clasifica en bloques que contienen alta, media y baja tendencia como verde, amarillo y rojo respectivamente. Se utiliza un gráfico de anillo para ilustrar la composición proporcional de los perfiles totales entre tendencias altas, medias y bajas como el verde, el amarillo y el rojo, respectivamente. Un perfil cumple los requisitos para una alta tendencia a más de 75 años, una tendencia media entre 25 y 74 años y una baja tendencia a menos de 24 años. Una leyenda indica el código de color y los umbrales de tendencia. Los recuentos de perfiles para las tendencias alta, media y baja se muestran en un cuadro de diálogo cuando el cursor se pasa por encima de la sección correspondiente del gráfico circular.

>[!NOTE]
>
>Si la visualización es una puntuación de tendencia de conversión, las puntuaciones más altas se muestran en verde y las más bajas en rojo. Si predice una tendencia a la pérdida invertida, las puntuaciones más altas están en rojo y las más bajas en verde. El cubo mediano permanece amarillo independientemente del tipo de tendencia que elija.

El menú desplegable debajo del título del widget proporciona una lista de todos los modelos de inteligencia artificial aplicada al cliente configurados. Seleccione el modelo de IA adecuado para el análisis en la lista de modelos disponibles. Si no hay ningún modelo de inteligencia artificial aplicada al cliente disponible, un mensaje dentro del widget le indica que configure al menos un modelo de inteligencia artificial aplicada al cliente y proporciona un hipervínculo a la página de configuración del modelo de inteligencia artificial aplicada al cliente. Consulte la documentación sobre [cómo configurar una instancia de inteligencia artificial aplicada al cliente](../../intelligent-services/customer-ai/user-guide/configure.md) para obtener instrucciones detalladas.

>[!NOTE]
>
>El número total de perfiles calculados depende de la política de combinación elegida. Para cambiar la política de combinación utilizada, seleccione el menú desplegable situado inmediatamente debajo de la pestaña de información general. Consulte la sección sobre [políticas de combinación](#merge-policies) para obtener una breve descripción o la [descripción general de la política de combinación](../../profile/merge-policies/overview.md) para obtener más detalles.

![Panel de audiencias de Experience Platform con el widget de resumen de puntuación de inteligencia artificial aplicada al cliente resaltado.](../images/segments/customer-ai-scoring-summary.png)

Seleccione **[!UICONTROL Ver detalles del modelo]** para navegar a la página de información detallada del modelo de inteligencia artificial aplicada al cliente seleccionado. Encontrará más información sobre inteligencia artificial aplicada al cliente en la [guía de la interfaz de usuario de Discover insights](../../intelligent-services/customer-ai/user-guide/discover-insights.md).

## Widgets estándar {#standard-widgets}

Adobe proporciona varios widgets estándar que puede utilizar para visualizar diferentes métricas relacionadas con las audiencias. También puede crear widgets personalizados para compartirlos con su organización mediante la [!UICONTROL biblioteca de widgets]. Para obtener más información sobre cómo crear widgets personalizados, empieza por leer la [descripción general de la biblioteca de widgets](../customize/widget-library.md).

Para obtener más información sobre cada uno de los widgets estándar disponibles, seleccione el nombre de un widget en la siguiente lista:

* [[!UICONTROL Tamaño de público]](#audience-size)
* [[!UICONTROL Pedido de activación de audiencia]](#audience-activation-order)
* [[!UICONTROL Tendencia de tamaño de público]](#audience-size-trend)
* [[!UICONTROL Tendencia de cambio de tamaño de audiencia]](#audience-size-change-trend)
* [[!UICONTROL Tendencia del tamaño de la audiencia por identidad]](#audience-size-trend-by-identity)
* [[!UICONTROL Superposición de audiencia]](#audience-overlap)
* [[!UICONTROL Informe de superposición de audiencias]](#audience-overlap-report)
* [[!UICONTROL Superposición de identidad]](#identity-overlap)
* [[!UICONTROL Perfiles por identidad]](#profiles-by-identity)
* [[!UICONTROL Activaciones programadas]](#scheduled-activations)

### [!UICONTROL Tamaño de público] {#audience-size}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_audiencesize"
>title="Tamaño de público"
>abstract="Este widget muestra el número total de perfiles combinados dentro del público seleccionado. Este número depende de las políticas de combinación aplicadas a los datos y es correcto en el momento de la instantánea más reciente."

El widget **[!UICONTROL Tamaño de audiencia]** muestra el número total de perfiles combinados dentro de la audiencia seleccionada en el momento en que se tomó la instantánea. Este número es el resultado de aplicar la política de combinación de audiencias a los datos del perfil para combinar fragmentos de perfil y formar un único perfil para cada individuo en la audiencia.

Para obtener más información sobre fragmentos y perfiles combinados, consulte la [descripción general del perfil del cliente en tiempo real](../../profile/home.md).

![Información general del tablero [!UICONTROL Audiencias] con el widget [!UICONTROL Tamaño de audiencia] resaltado.](../images/audiences/audience-size.png)

### [!UICONTROL Tendencia de tamaño de público] {#audience-size-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_audiencesizetrend"
>title="Tendencia de tamaño de público"
>abstract="Este widget proporciona información sobre el número total de perfiles que cumplen los criterios de **cualquier** definición de segmentos, según lo capturado durante la instantánea diaria, los últimos 30 días, 90 días o 12 meses."

El widget de tendencia de tamaño de audiencia **[!UICONTROL Audience size]** proporciona una ilustración de gráfico de líneas para la cantidad total de perfiles que califican para la audiencia **any** durante un período de tiempo determinado. La tendencia del tamaño de la audiencia se puede visualizar en períodos de 30 días, 90 días y 12 meses. El período de tiempo se elige en un menú desplegable del widget. El tamaño de la audiencia se refleja en el eje y y el tiempo en el eje x.

Este widget también incluye la característica automática [!UICONTROL Subtítulos], donde un modelo de aprendizaje automático analiza el gráfico y los datos de audiencia y genera automáticamente subtítulos para describir las tendencias clave y los eventos importantes. Seleccione **[!UICONTROL Subtítulos]** para abrir el cuadro de diálogo de subtítulos automáticos.

![La descripción general de [!UICONTROL Audiencias] muestra el widget de tendencia de tamaño de audiencia.](../images/audiences/audience-size-trend-captions.png)

El cuadro de diálogo de subtítulos automáticos se abre para proporcionar información sobre los datos.

![Cuadro de diálogo de subtítulos automáticos para el widget de tendencia de tamaño de audiencia.](../images/audiences/audience-size-trend-automatic-captions-dialog.png)

Para obtener más información sobre la evaluación de audiencias y cómo los perfiles califican y salen de las audiencias, consulte la [documentación del servicio de segmentación](../../segmentation/home.md).

### [!UICONTROL Tendencia de cambio de tamaño de audiencia] {#audience-size-change-trend}

Este widget proporciona un gráfico de líneas que ilustra la diferencia en el número total de perfiles aptos para una audiencia determinada entre las instantáneas diarias más recientes. La audiencia elegida para el análisis se selecciona en la lista desplegable de información general. El periodo de análisis de tendencias se puede visualizar en periodos de 30 días, 90 días y 12 meses. El período de tiempo se elige en un menú desplegable del widget. El tamaño de la audiencia se refleja en el eje y y el tiempo en el eje x.

![El widget de tendencia de cambio de tamaño de audiencia.](../images/audiences/audience-size-change-trend.png)

### [!UICONTROL Tendencia del tamaño de la audiencia por identidad] {#audience-size-trend-by-identity}

Este widget ilustra la tendencia del tamaño de la audiencia de una audiencia en particular en función del tipo de identidad elegido en el menú desplegable de widgets. La audiencia utilizada para el análisis se selecciona en la lista desplegable de información general. El periodo de análisis de tendencias se puede visualizar en periodos de 30 días, 90 días y 12 meses. El período de tiempo se elige en un menú desplegable del widget.

![Tendencia del tamaño de la audiencia según el widget de identidad.](../images/audiences/audience-size-trend-by-identity.png)

### [!UICONTROL Pedido de activación de audiencia] {#audience-activation-order}

El widget de orden de activación de audiencia [!UICONTROL Audience] proporciona una tabla de tres columnas que indica el nombre de destino, la plataforma y la fecha de activación de la audiencia. La lista se ordena de alta a baja según la actualización y puede alojar hasta 10 filas.

![El widget de orden de activación de audiencia.](../images/audiences/audience-activation-order.png)

### [!UICONTROL Superposición de audiencia] {#audience-overlap}

Este widget utiliza un diagrama de Venn para visualizar el número de personas que coinciden con los criterios de ambas audiencias. Las audiencias utilizadas para la comparación se seleccionan en los menús desplegables de widgets. El número total de perfiles contenidos dentro de la definición del segmento correspondiente se puede ver pasando el ratón por encima de un círculo o de la intersección del diagrama de Venn.

Este widget le permite optimizar su estrategia de segmentación mediante la visualización de las similitudes en los resultados de las definiciones de segmentos.

![Widget de superposición de audiencias.](../images/audiences/audience-overlap.png)

### [!UICONTROL Informe de superposición de audiencias] {#audience-overlap-report}

Este widget tabula los datos de superposición de perfiles de una audiencia específica. Se proporciona una lista de cinco audiencias clasificadas entre los porcentajes de superposición más altos y más bajos para la audiencia elegida en el menú desplegable de la parte superior de la pantalla. Para mayor claridad, la audiencia elegida se enumera en la columna [!UICONTROL AUDIENCIA A NOMBRE]. Se proporciona un análisis de superposición de audiencias para la segunda audiencia enumerada en la columna [!UICONTROL AUDIENCE B NAME]. La superposición porcentual se indica en la tercera columna con una precisión de doce decimales.

El informe de superposición de audiencias le ayuda a crear audiencias nuevas y de alto rendimiento. La observación de superposiciones de alto porcentaje le permite suprimir audiencias e impedir que se envíe la misma audiencia a diferentes destinos. También le ayudan a identificar perspectivas ocultas que pueden ayudarle con una mejor segmentación. La superposición de bajo porcentaje ayuda a localizar perfiles únicos que perseguir.

Seleccione **[!UICONTROL Ver más]** para abrir un cuadro de diálogo de pantalla completa que contenga más datos de superposición de audiencias.

![Widget del informe de superposición de audiencia con Ver más resaltado .](../images/audiences/audience-overlap-report.png)

Aparecerá el cuadro de diálogo [!UICONTROL Informe de superposición de audiencias]. Este cuadro de diálogo puede contener hasta 50 filas de análisis de superposición de audiencias divididas en seis columnas. Seleccione el icono de configuración (![El icono de configuración.](/help/images/icons/settings.png)) para quitar o agregar columnas de la tabla.

![Cuadro de diálogo del informe de superposición de audiencias.](../images/audiences/audience-overlap-report-dialog.png)

>[!NOTE]
>
>Seleccione el encabezado de columna **[!UICONTROL Superposición]** para cambiar la clasificación de los resultados de mayor a menor o de menor a mayor.

Para descargar todo el informe en formato PDF, seleccione el menú de opciones (**`...`**) seguido de **[!UICONTROL Descargar]**.

![Cuadro de diálogo del informe de superposición de audiencias con los puntos suspensivos y la opción de descarga resaltados.](../images/audiences/audience-overlap-report-dialog-download.png)

Seleccione una fila del informe para abrir un diagrama de Venn del análisis de superposición. Pase el ratón sobre una sección del diagrama de Venn para ver el recuento de perfiles en un cuadro de diálogo.

![Cuadro de diálogo Informe de superposición de audiencia con un diagrama de Venn y una fila resaltada.](../images/audiences/audience-overlap-report-dialog-venn.png)

Seleccione **[!UICONTROL Cerrar]** para volver al panel [!UICONTROL Audiencias].

### [!UICONTROL Superposición de identidad] {#identity-overlap}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_identityoverlap"
>title="Superposición de identidad"
>abstract="Este widget muestra la superposición de perfiles en el público que contiene ambas identidades seleccionadas. Los círculos muestran el tamaño relativo de cada identidad. El número de perfiles que contienen ambas áreas de nombres se representa mediante la superposición entre los círculos."

El widget **[!UICONTROL Superposición de identidad]** muestra un diagrama de Venn o un diagrama de conjunto que muestra la superposición de perfiles en la audiencia que contiene varias identidades.

Utilice los menús desplegables del widget para seleccionar las identidades que desea comparar. Los círculos muestran el tamaño relativo de cada identidad elegida, y el número de perfiles que contienen ambas áreas de nombres se representa mediante el tamaño de la superposición entre los círculos.

Si un cliente interactúa con su marca en más de un canal, se asociarán varias identidades a ese cliente individual. Esta situación hace probable que su organización tenga varios perfiles que contengan fragmentos de más de una identidad.

Para obtener más información sobre identidades, visita la [documentación del servicio de identidad](../../identity-service/home.md).

![Información general del panel [!UICONTROL Audiencias] con el widget de superposición de identidad resaltado.](../images/audiences/identity-overlap.png)

### [!UICONTROL Perfiles por identidad] {#profiles-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_profilesbyidentity"
>title="Perfiles por identidad"
>abstract="Este widget muestra el desglose de identidades en cada perfil combinado del público seleccionado."

El widget **[!UICONTROL Perfiles por identidad]** muestra el desglose de identidades en todos los perfiles combinados de la audiencia seleccionada. El número total de perfiles por identidad puede ser mayor que el número total de perfiles en la audiencia, ya que un perfil podría tener varias identidades asociadas. En otras palabras, si se suman los valores mostrados para cada identidad, el total puede ser mayor que el tamaño total de la audiencia. Esto se debe a que si un cliente interactúa con su marca en más de un canal, pueden asociarse varias identidades con ese cliente individual.

Seleccione **[!UICONTROL Subtítulos]** para abrir el cuadro de diálogo de subtítulos automáticos.

![Descripción general del tablero [!UICONTROL Audiencias] con la opción Perfiles por widget de identidad y Subtítulos resaltada.](../images/audiences/profiles-by-identity.png)

Un modelo de aprendizaje automático genera automáticamente perspectivas de datos analizando la distribución general y las dimensiones clave de los datos.

Para obtener más información sobre identidades, visita la [documentación del servicio de identidad](../../identity-service/home.md).

### Activaciones programadas {#scheduled-activations}

El widget [!UICONTROL Activaciones programadas] proporciona una vista tabularizada de los destinos activados más recientemente. La tabla incluye la plataforma de destino, el nombre del flujo de activación a este destino y las fechas de inicio y finalización de la activación de la audiencia seleccionada. Si no se proporciona una fecha de finalización para la activación, se mostrará como [!UICONTROL En curso]. La audiencia analizada se selecciona en el menú desplegable situado en la parte superior de la página.

El widget permite descubrir de un vistazo dónde y cuándo se está activando la audiencia, y hace que las activaciones duplicadas o innecesarias sean más transparentes. Esta información acumulada también resalta dónde se ha dejado de lado cualquier activación.

![Widget de activaciones programadas.](../images/audiences/scheduled-activations.png)

## Próximos pasos

Siguiendo este documento, debería poder encontrar el panel [!UICONTROL Audiencias] y seleccionar una audiencia para verla. También debe comprender las métricas que se muestran en los widgets disponibles. Para obtener más información sobre cómo trabajar con audiencias en la interfaz de usuario de Experience Platform, consulte la [guía de la interfaz de usuario del servicio de segmentación](../../segmentation/ui/overview.md).
