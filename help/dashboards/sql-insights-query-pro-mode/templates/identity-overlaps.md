---
title: Superposiciones de identidad de público
description: Obtenga información sobre cómo analizar las superposiciones de identidades de audiencias mediante el panel Superposiciones de identidades de audiencias. Filtre audiencias, especifique políticas de combinación y examine relaciones de identidad para tomar decisiones basadas en datos.
source-git-commit: 90d5f00648a80d735b92c3bdc540f1ad18ff38f5
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 1%

---

# Superposiciones de identidad de público

Analice las superposiciones de identidad de las audiencias seleccionadas con el panel [!UICONTROL Superposiciones de identidad de audiencia]. Puede utilizar perspectivas sobre cómo las distintas identidades de una audiencia se relacionan entre sí para optimizar las estrategias de vinculación, reducir la redundancia y mejorar la precisión de la segmentación de clientes. Desarrolle estrategias de segmentación eficaces y optimice las interacciones con los clientes con una mejor comprensión de la superposición entre los tipos de identidad.

## Filtrado de audiencias {#filter-audiences}

Utilice filtros personalizados para el análisis segmentado de audiencias específicas y tipos de identidad para garantizar que los datos presentados se ajusten a los objetivos del análisis. Para iniciar el análisis, seleccione el icono de filtro (![El icono de filtro.](../../../images/icons/filter-icon-white.png)).

![La identidad de la audiencia se superpone en el panel con el icono de filtro resaltado.](../../images/sql-insights-query-pro-mode/templates/audience-identity-overlaps-filter-icon.png)

Aparecerá el cuadro de diálogo **[!UICONTROL Filtros]**. Desde esta vista, elija los filtros globales para configurar la audiencia, la política de combinación y las identidades para la comparación. Seleccione la configuración de análisis en el menú desplegable de cada sección

1. Seleccione una **[!UICONTROL audiencia]**: elija el segmento de audiencia que desee analizar (por ejemplo, **Canadá - Alberta**).
2. Especificar una **[!UICONTROL política de combinación]**: defina la política de combinación que dicta cómo se combinan las identidades en la audiencia seleccionada (en la captura de pantalla de ejemplo, se selecciona la política **Basada en tiempo predeterminado**).
3. Seleccione una **[!UICONTROL identidad A]** y una **[!UICONTROL identidad B]** para comparar&#x200B;**: elija los dos tipos de identidad que desea comparar. En el ejemplo, &#x200B;** Identidad A **&#x200B; está seleccionada como &quot;crmId&quot; y &#x200B;** Identidad B** está seleccionada como &quot;correo electrónico&quot;.
4. **Establecer un intervalo de fechas**: elija un intervalo predefinido como &quot;Hoy&quot; o establezca manualmente las fechas de inicio y finalización utilizando los campos de calendario.

![Cuadro de diálogo Filtros en el panel Superposiciones de identidad de audiencia.](../../images/sql-insights-query-pro-mode/templates/audience-identity-overlaps-filters-dialog.png)

>[!TIP]
>
>Para borrar todos los filtros globales personalizados, selecciona **[!UICONTROL Borrar todo]** en el cuadro de diálogo [!UICONTROL Filtros]. Para quitar un solo filtro, seleccione &#39;[!UICONTROL X]&#39; a la derecha del nombre del filtro.

Una vez que haya elegido los filtros, seleccione **[!UICONTROL Aplicar]** para actualizar el tablero.

![El cuadro de diálogo Filtros en el panel Audiencia superpuesta de identidad con Aplicar resaltado.](../../images/sql-insights-query-pro-mode/templates/audience-identity-overlaps-apply-filters.png)

## Perspectivas del panel disponibles {#available-insights}

El panel **Superposiciones de identidad de audiencia** proporciona varias visualizaciones y datos tabulados para ayudarle a comprender las superposiciones de identidad y las tendencias dentro de su audiencia.

### Superposiciones de identidad de público {#overlaps-table}

La tabla **[!UICONTROL Superposiciones de identidad de audiencia]** muestra las superposiciones de identidad en función de los filtros seleccionados. Utilice esta información para evaluar la superposición entre diferentes tipos de identidad y comprender con qué eficacia se resuelven las identidades. La siguiente tabla explica cada columna en detalle:

| Nombre de columna | Descripción |
|-----------------|-------------------------------|
| **[!UICONTROL Nombre de audiencia]** | Nombre de la audiencia que se está analizando. Esta columna identifica qué segmento de audiencia se está revisando para garantizar que las perspectivas se centren en el grupo destinatario deseado. |
| **[!UICONTROL Identidad A]** e **[!UICONTROL Identidad B]** | Las identidades que se comparan (por ejemplo, `crmId` y `email`). Saber qué tipos de identidad se comparan le ayuda a identificar qué estrategias de resolución de identidad contribuyen a la superposición de audiencias y a optimizar esas relaciones. |
| **[!UICONTROL Recuento de superposiciones]** | Recuento de perfiles en los que están presentes ambas identidades. Esta métrica proporciona perspectivas sobre el alcance de la superposición de identidades dentro de la audiencia. Esta información es crucial para evaluar la eficacia con la que se resuelven varias identidades en perfiles unificados, lo que a su vez puede mejorar las estrategias de segmentación y personalización. |
| **[!UICONTROL Recuento de identidad A]** | Número total de perfiles en la audiencia seleccionada que contienen **Identidad A**. Utilice esta información para comprender la prevalencia del tipo de identidad principal dentro de la audiencia y evaluar su papel en el análisis de superposición. |

![La tabla de superposiciones de identidad de audiencia del panel de superposiciones de identidad de audiencia.](../../images/sql-insights-query-pro-mode/templates/audience-identity-overlaps-chart.png)

### Desglose de identidad {#identity-breakdown}

El gráfico **[!UICONTROL Desglose de identidad]** muestra la composición relativa de identidades dentro de la audiencia seleccionada. El eje X representa el número total de identidades dentro de la audiencia seleccionada, mientras que el eje Y representa el nombre de la audiencia que se está analizando. Utilice esta visualización para comprender la prevalencia de cada tipo de identidad y evaluar el impacto de su estrategia de administración de identidades. El gráfico diferencia entre tipos de identidad utilizando colores distintos, lo que proporciona una visión general rápida de cómo se distribuyen las identidades entre la audiencia.

>[!TIP]
>
>Pase el ratón sobre las columnas para ver el recuento individual de perfiles de cada tipo de identidad.

![Gráfico de desglose de identidad.](../../images/sql-insights-query-pro-mode/templates/identity-breakdown-chart.png)

### Tendencias de identidad de audiencia {#audience-identity-trends}

El gráfico **[!UICONTROL Tendencias de identidad de audiencia]** proporciona información sobre cómo ha cambiado el número total de identidades con el paso del tiempo. El eje X representa el intervalo de fechas que se está analizando, mientras que el eje Y representa el número total de identidades por audiencia. Utilice esta métrica para rastrear el crecimiento de la identidad, evaluar la estabilidad y medir la eficacia de los esfuerzos actuales de administración de identidades.

>[!TIP]
>
>Pase el ratón sobre una fecha del gráfico para ver la cantidad total de identidades de la audiencia en una fecha específica.

![Gráfico de tendencias de identidad de audiencia.](../../images/sql-insights-query-pro-mode/templates/audience-identity-trends-chart.png)

## Exportar perspectivas {#export-insights}

Después de analizar las superposiciones de identidades, puede exportar los datos para realizar análisis o informes sin conexión. Para exportar los datos, seleccione **[!UICONTROL Exportar]** en la parte superior derecha de la tabla. Aparecerá el cuadro de diálogo Imprimir PDF, que le permitirá guardar los datos visualizados como un PDF o imprimirlos.

![La identidad de la audiencia se superpone en el panel con la exportación resaltada.](../../images/sql-insights-query-pro-mode/templates/audience-identity-overlaps-export.png)

El panel **Superposiciones de identidad de audiencia** proporciona información esencial sobre cómo las distintas identidades se cruzan entre las audiencias seleccionadas. Al aprovechar estas perspectivas, puede refinar las estrategias de vinculación de identidad, reducir la redundancia y garantizar que la segmentación de audiencia sea más precisa y eficaz.

## Pasos siguientes

Después de leer este documento, ha aprendido a obtener información valiosa sobre las superposiciones de identidades para audiencias seleccionadas usando el panel **Superposiciones de identidades de audiencias**. Para comprender mejor la segmentación de audiencia y la administración de identidades, explore otras plantillas de Data Distiller que ofrecen perspectivas completas. Consulte las guías de la interfaz de usuario [Tendencias de audiencia](./trends.md), [Comparación de audiencias](./comparison.md) y [Superposiciones de audiencias avanzadas](./overlaps.md) para seguir mejorando las estrategias de segmentación y participación.

