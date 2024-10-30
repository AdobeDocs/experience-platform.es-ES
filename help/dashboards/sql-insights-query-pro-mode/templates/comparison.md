---
title: Comparación de públicos
description: Aprenda a comparar métricas clave entre diferentes grupos de audiencias mediante el panel Comparación de audiencias. Establezca filtros de audiencia, analice tendencias y exporte perspectivas para decisiones basadas en datos
source-git-commit: 90d5f00648a80d735b92c3bdc540f1ad18ff38f5
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 0%

---

# Comparación de públicos

El panel [!UICONTROL Comparación de audiencias] compara y contrasta las métricas de audiencia clave en una vista en paralelo. Desde este panel, puede realizar diversas acciones para comparar dos grupos de audiencias y analizar métricas clave entre ellos. A continuación, puede tomar decisiones basadas en datos con respecto a la segmentación de audiencia y las estrategias de segmentación.

## Establecer comparaciones de audiencias {#set-audience-comparisons}

Para permitir perspectivas y comparaciones más significativas, utilice los filtros del sistema para dirigirse con precisión a los segmentos de audiencia y al periodo de tiempo que le interese analizar. Seleccione el icono de filtro (![El icono de filtro.](../../../images/icons/filter-icon-white.png)) para elegir dos audiencias diferentes ([!UICONTROL Audiencia A] y [!UICONTROL Audiencia B]) y establecer parámetros específicos para la comparación.

![Cuadro de diálogo Filtros en el panel de comparación de audiencias.](../../images/sql-insights-query-pro-mode/templates/audience-comparison-filters.png)

Aparecerá el cuadro de diálogo [!UICONTROL Filtro]. Para elegir la primera audiencia que analizar, seleccione la lista desplegable **[!UICONTROL Seleccionar audiencia A]**. En este ejemplo, `California Patients` se ha seleccionado como Audiencia A. Esta audiencia aparece en el lado izquierdo de la comparación una vez que se aplica el filtro.

A continuación, elija una segunda audiencia para compararla con [!UICONTROL Audiencia A] en la lista desplegable **[!UICONTROL Seleccionar audiencia B]**. En esta imagen, [!UICONTROL Usuarios que aceptaron enviar correo electrónico] se ha seleccionado como [!UICONTROL Audiencia B]. Esta audiencia se muestra en el lado derecho del panel [!UICONTROL Comparación de audiencias] una vez que se ha aplicado el filtro.

### Ajuste de intervalos de fechas {#adjust-date-ranges}

También puede filtrar los datos por períodos de tiempo específicos para ver cómo funcionan estas audiencias o cómo cambian en un intervalo de fechas personalizado. Para definir un intervalo de tiempo para filtrar los datos de audiencia por un periodo específico, seleccione las fechas de inicio y finalización en los campos del calendario.

El cuadro de diálogo también indica cuántos filtros se aplican (en la captura de pantalla siguiente, se están utilizando dos filtros: audiencia A y audiencia B, y hoy como intervalo de fechas). Para quitar todos los filtros aplicados, seleccione **[!UICONTROL Borrar todo]**.

Después de establecer las audiencias y el intervalo de fechas, seleccione **[!UICONTROL Aplicar]** para actualizar el panel [!UICONTROL Comparación de audiencias].

![Cuadro de diálogo Filtros en el panel de comparación de audiencias con Aplicar resaltado.](../../images/sql-insights-query-pro-mode/templates/audience-comparison-filters-apply.png)

El panel ahora muestra los gráficos comparativos mostrados uno al lado del otro para cada audiencia.

![Panel de comparación de audiencias con varios gráficos que comparan métricas para cada audiencia.](../../images/sql-insights-query-pro-mode/templates/audience-comparison-dashboard.png)

## Gráficos comparativos de audiencia disponibles {#available-charts}

<!-- Potentially could expand this section to include images of each widget.  -->

El panel proporciona varios gráficos para comparar las perspectivas:

- [[!UICONTROL Tamaño de audiencia]](../../guides/audiences.md#audience-size): realice fácilmente un seguimiento del tamaño de cada audiencia en función del número de perfiles que contienen. Esta métrica le ayuda a comprender la escala de las dos audiencias que está comparando.
- [!UICONTROL Desglose de identidad de audiencia]: un gráfico circular proporciona un desglose de la composición relativa de identidades dentro de cada audiencia. Puede ver el número total de identidades y examinar cómo diferentes identificadores (como correo electrónico o ID de CRM) contribuyen a ese total. Este gráfico le ayuda a comprender la composición de cada audiencia en función de los tipos de identidad. Pase el ratón sobre una sección del gráfico circular para ver un número exacto de identidades.
- [[!UICONTROL Tendencia de tamaño de audiencia]](../../guides/audiences.md#audience-size-trend): este gráfico representa las tendencias de tamaño a lo largo del tiempo para la audiencia elegida. Utilice estos gráficos para visualizar cómo ha cambiado el tamaño de cada audiencia en un período de tiempo seleccionado, con picos y valle que indican períodos de crecimiento o reducción en el número de perfiles.
- [[!UICONTROL Tendencia de cambio de tamaño de audiencia]](../../guides/audiences.md#audience-size-change-trend): este gráfico muestra las tendencias de cambio de tamaño para la audiencia elegida. Visualiza cuánto ha aumentado o disminuido el tamaño de la audiencia con el tiempo y le permite identificar cambios o tendencias significativos en la población de audiencias.

>[!NOTE]
>
>Los gráficos [!UICONTROL Tendencia de tamaño de audiencia] y [!UICONTROL Tendencia de cambio de tamaño de audiencia] le ayudan a rastrear y comparar el tamaño absoluto y las fluctuaciones de tamaño entre dos audiencias durante un período especificado. Esta información facilita la comprensión de patrones y factores que influyen en los cambios de audiencia.

## Exportar perspectivas {#export-insights}

Una vez aplicados los filtros y analizadas las audiencias, puede exportar los datos para realizar más análisis sin conexión o generar informes. Para exportar tus datos, selecciona **[!UICONTROL Exportar]** en la parte superior derecha de la tabla. Aparecerá el cuadro de diálogo Imprimir PDF. Desde este cuadro de diálogo, puede guardar como PDF o imprimir los datos que se muestran en la tabla.

Seleccione **[!UICONTROL Plantillas]** para volver a la descripción general de [!UICONTROL Plantilla].

![La vista Audiencia avanzada se superpone con las plantillas resaltadas.](../../images/sql-insights-query-pro-mode/templates/navigation.png)

## Pasos siguientes

Después de leer este documento, ha aprendido a comparar métricas clave entre diferentes grupos de audiencias usando el panel **Comparación de audiencias**. Para seguir mejorando las estrategias de segmentación de audiencia y segmentación, explore otras plantillas de Distiller de datos que proporcionen perspectivas adicionales. Consulte las guías de la interfaz de usuario [Tendencias de audiencia](./trends.md), [Superposiciones de identidad de audiencia](./identity-overlaps.md) y [Superposiciones de audiencia avanzadas](./overlaps.md) para mejorar aún más la toma de decisiones y optimizar los esfuerzos de participación.

