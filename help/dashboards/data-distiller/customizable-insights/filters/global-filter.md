---
title: Crear un filtro global
description: Obtenga información sobre cómo filtrar las perspectivas de datos con un filtro personalizado aplicado globalmente.
source-git-commit: b95616263d5a6dd26f7fce61d5d0b33c2d470c46
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---

# Creación de un filtro global {#create-global-filter}

Para crear un filtro global, seleccione primero **[!UICONTROL Añadir filtro]** en la vista de panel, haga clic en **[!UICONTROL Filtro global]** en el menú desplegable.

>[!IMPORTANT]
>
>Asegúrese de asignar los filtros globales a todos los gráficos. Este no es un proceso automático. Para utilizar un filtro global, debe incluir un [parámetro de consulta](../../../../query-service/ui/parameterized-queries.md) en el SQL del gráfico, [activación del filtro global](#enable-global-filter) en el compositor de widgets, y [seleccionar un valor de tiempo de ejecución](#select-global-filter) para el parámetro en el cuadro de diálogo filtro global. Consulte la guía del profesional de consultas para obtener información sobre cómo editar el SQL si necesita incorporar un parámetro de consulta.

![Un panel personalizado con el filtro Agregar y su menú desplegable resaltado.](../../../images/customizable-insights/add-filter.png)

Puede cambiar rápidamente las perspectivas proporcionadas por su SQL con filtros globales personalizados.

El [!UICONTROL Creación de un filtro global] se abre. La creación de un filtro global sigue el mismo proceso que la creación de una perspectiva con SQL. En primer lugar, seleccione una base de datos (modelo de datos de perspectivas) para consultar, luego introduzca su SQL personalizado en el Editor de consultas y, por último, seleccione el icono de ejecución (![Un icono de ejecución.](../../../images/customizable-insights/run-icon.png)).

>[!IMPORTANT]
>
>Debe incluir un ID y un valor al crear un filtro global. Los valores de ejemplo permiten ejecutar la instrucción SQL y crear el gráfico. Tenga en cuenta que los valores de ejemplo que proporcione al maquetar la instrucción se sustituirán por los valores reales que seleccione para la fecha o el filtro global durante la ejecución.

Después de ejecutar correctamente la consulta, la pestaña resultados muestra los resultados. Seleccione **[!UICONTROL Siguiente]**.

![El [!UICONTROL Cuadro de diálogo Crear un filtro global] con el menú desplegable conjunto de datos, el icono ejecutar y Siguiente resaltados.](../../../images/customizable-insights/global-filter.png)

El último paso del flujo de trabajo de creación de filtros globales requiere que añada una etiqueta para el filtro. Añada una etiqueta a **[!UICONTROL Etiqueta de filtro]** y seleccione un tipo de filtro en el cuadro desplegable.

>[!NOTE]
>
>Solo el [!UICONTROL Cuadro combinado] actualmente se admite la opción de tipo de filtro.

Finalmente, seleccione **[!UICONTROL Seleccionar]** para volver a la vista del panel.

![El [!UICONTROL Cuadro de diálogo Crear un filtro global] con Seleccionar y la entrada de texto Etiqueta de filtro resaltada.](../../../images/customizable-insights/global-filter-label.png)

## Habilitar el filtro global para cada perspectiva {#enable-global-filter}

>[!TIP]
>
>Habilite los filtros globales en cada gráfico que cree. Esto garantiza que los valores que elija como filtro global se reflejen en todos los gráficos.

Después de crear el filtro global para el tablero, la opción de ese filtro global está disponible como parte del compositor de widgets.

![Compositor de widgets con la opción de filtro global resaltada.](../../../images/customizable-insights/global-filter-consent.png)

>[!IMPORTANT]
>
>Asegúrese de que el parámetro de filtro global se incluya en el SQL de cada perspectiva.

## Seleccionar un filtro global {#select-global-filter}

Para abrir [!UICONTROL Filtros] que enumera todos los filtros personalizados, seleccione el icono de filtro (![Un icono de filtro.](../../../images/customizable-insights/filter.png)), a la izquierda del tablero. A continuación, para aplicar los efectos a las perspectivas del panel, elija una opción en el menú desplegable del filtro global y, a continuación, seleccione **[!UICONTROL Aplicar]**.

![Un panel personalizado con el cuadro de diálogo de filtro resaltado.](../../../images/customizable-insights/custom-filters.png)
