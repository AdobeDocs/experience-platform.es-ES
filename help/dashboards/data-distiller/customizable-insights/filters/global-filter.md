---
title: Crear un filtro global
description: Obtenga información sobre cómo filtrar las perspectivas de datos con un filtro personalizado aplicado globalmente.
exl-id: a0084039-8809-4883-9f68-c666dcac5881
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---

# Crear un filtro global {#create-global-filter}

Para crear un filtro global, primero selecciona **[!UICONTROL Agregar filtro]** en la vista del panel y luego **[!UICONTROL Filtro global]** en el menú desplegable.

>[!IMPORTANT]
>
>Asegúrese de asignar los filtros globales a todos los gráficos. Este no es un proceso automático. Para usar un filtro global, debe incluir un [parámetro de consulta](../../../../query-service/ui/parameterized-queries.md) en el SQL del gráfico, [habilitar el filtro global](#enable-global-filter) en el compositor de widgets y [seleccionar un valor de tiempo de ejecución](#select-global-filter) para el parámetro en el cuadro de diálogo del filtro global. Consulte la guía del profesional de consultas para obtener información sobre cómo editar el SQL si necesita incorporar un parámetro de consulta.

![Panel personalizado con el elemento Agregar filtro y su menú desplegable resaltados.](../../../images/customizable-insights/add-filter.png)

Puede cambiar rápidamente las perspectivas proporcionadas por su SQL con filtros globales personalizados.

Se abre el cuadro de diálogo [!UICONTROL Crear un filtro global]. La creación de un filtro global sigue el mismo proceso que la creación de una perspectiva con SQL. En primer lugar, seleccione una base de datos (modelo de datos de perspectivas) para realizar una consulta y, a continuación, escriba el SQL personalizado en el Editor de consultas y, finalmente, seleccione el icono de ejecución (![Icono de ejecución.](/help/images/icons/play.png)).

>[!IMPORTANT]
>
>Debe incluir un ID y un valor al crear un filtro global. Los valores de ejemplo permiten ejecutar la instrucción SQL y crear el gráfico. Tenga en cuenta que los valores de ejemplo que proporcione al maquetar la instrucción se sustituirán por los valores reales que seleccione para la fecha o el filtro global durante la ejecución.

Después de ejecutar correctamente la consulta, la pestaña resultados muestra los resultados. Seleccione **[!UICONTROL Siguiente]**.

![Cuadro de diálogo [!UICONTROL Crear un filtro global] con el menú desplegable del conjunto de datos, el icono de ejecución y Siguiente resaltados.](../../../images/customizable-insights/global-filter.png)

El último paso del flujo de trabajo de creación de filtros globales requiere que añada una etiqueta para el filtro. Agregue una etiqueta al campo de texto **[!UICONTROL Etiqueta de filtro]** y seleccione un tipo de filtro en el cuadro desplegable.

>[!NOTE]
>
>Actualmente solo se admite la opción de tipo de filtro [!UICONTROL Cuadro combinado].

Finalmente, seleccione **[!UICONTROL Seleccionar]** para regresar a la vista del panel.

![Cuadro de diálogo [!UICONTROL Crear un filtro global] con la opción Seleccionar y la entrada de texto de la etiqueta Filtro resaltada.](../../../images/customizable-insights/global-filter-label.png)

## Habilitar el filtro global para cada perspectiva {#enable-global-filter}

>[!TIP]
>
>Habilite los filtros globales en cada gráfico que cree. Esto garantiza que los valores que elija como filtro global se reflejen en todos los gráficos.

Después de crear el filtro global para el tablero, la opción de ese filtro global está disponible como parte del compositor de widgets.

![Se ha resaltado la opción del compositor de widgets con el filtro global.](../../../images/customizable-insights/global-filter-consent.png)

>[!IMPORTANT]
>
>Asegúrese de que el parámetro de filtro global se incluya en el SQL de cada perspectiva.

## Seleccionar un filtro global {#select-global-filter}

Para abrir el cuadro de diálogo [!UICONTROL Filtros] que enumera todos los filtros personalizados, seleccione el icono de filtro (![Un icono de filtro.](/help/images/icons/filter.png)) a la izquierda del tablero. A continuación, para aplicar los efectos en las perspectivas del panel, elija una opción en el menú desplegable del filtro global y seleccione **[!UICONTROL Aplicar]**.

![Un panel personalizado con el cuadro de diálogo de filtro resaltado.](../../../images/customizable-insights/custom-filters.png)
