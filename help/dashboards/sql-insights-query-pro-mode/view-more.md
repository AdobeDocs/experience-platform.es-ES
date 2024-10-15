---
title: Ver más
description: Obtenga información sobre las distintas opciones de visualización para los datos analizados por SQL. En el panel personalizado puede ver los resultados tabulados del análisis o descargar los datos procesados en formato CSV.
exl-id: f57d85cf-dbd2-415c-bf01-8faa49871377
source-git-commit: ddf886052aedc025ff125c03ab63877cb049583d
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 1%

---

# Ver más {#view-more}

Una vez que haya creado una [perspectiva personalizada](./overview.md) con [query pro mode](./overview.md#query-pro-mode), podrá ver los datos del gráfico en diferentes formatos. Puede ver un formulario tabulado de los resultados o descargar los datos como un archivo CSV para verlos en una hoja de cálculo.

## Resultados tabulados {#tabulated-results}

Para cada gráfico creado con el modo query pro a través de SQL, puede ver los resultados tabulados del análisis en la interfaz de usuario de Experience Platform.

En el tablero personalizado, seleccione los puntos suspensivos (`...`) de cualquier widget para acceder a las opciones [!UICONTROL Ver más] y [!UICONTROL Ver SQL].

![Panel personalizado con menú desplegable de puntos suspensivos de una perspectiva y las opciones Ver más y Ver SQL resaltadas.](../images/sql-insights-query-pro-mode/ellipses-dropdown.png)

## Descargar CSV {#download-csv}

La característica [!UICONTROL Ver más] muestra los puntos de datos específicos del gráfico en forma de tabla. Para simplificar el proceso de uso compartido y manipulación de datos, puede descargar los datos procesados en formato CSV desde este cuadro de diálogo. Seleccione **[!UICONTROL Descargar CSV]** para descargar los datos.

>[!NOTE]
>
>La descarga de CSV está limitada a los 500 primeros registros.

![Cuadro de diálogo que muestra una vista previa de su perspectiva y los resultados tabularizados de su SQL que generó la perspectiva.](../images/sql-insights-query-pro-mode/view-more-download-csv.png)

## Ordenar por columna {#sort-column}

Al ver los resultados en forma de tabla, puede utilizar la funcionalidad de ordenación para ordenar por columna en orden ascendente o descendente. En el tablero personalizado, seleccione los puntos suspensivos (`...`) de cualquier tabla para obtener acceso a la opción [!UICONTROL Ver más].

![Panel personalizado con menú desplegable de elipses de tabla y la opción Ver más resaltada.](../images/sql-insights-query-pro-mode/advanced-ellipses-dropdown.png)

Puede ordenar las columnas seleccionando el menú desplegable junto al nombre de la columna y, a continuación, **[!UICONTROL Orden ascendente]** o **[!UICONTROL Orden descendente]**.

>[!NOTE]
>
>Las opciones [!UICONTROL Orden ascendente] y [!UICONTROL Orden descendente] solo aparecerán para las columnas que se hayan configurado con [funcionalidad de ordenación](./overview.md#advanced-attributes).

![Menú desplegable de columna de tabla que muestra las opciones Orden ascendente y Orden descendente resaltadas.](../images/sql-insights-query-pro-mode/advanced-sort-dropdown.png)

## Cambiar el tamaño de una columna {#resize-column}

Puede cambiar el tamaño de las columnas en los resultados tabulados para mejorar la legibilidad de los datos. En el tablero personalizado, seleccione los puntos suspensivos (`...`) de la tabla para obtener acceso a la opción [!UICONTROL Ver más]. Utilice el menú desplegable situado junto al nombre de la columna para cambiar su tamaño y, a continuación, seleccione **[!UICONTROL Cambiar tamaño de columna]**.

![Menú desplegable de columna de tabla que muestra resaltada la opción Cambiar tamaño de columna.](../images/sql-insights-query-pro-mode/advanced-resize-dropdown.png)

Seleccione el control deslizante y arrastre hacia la izquierda o la derecha para ajustar el tamaño de la columna según sea necesario.

![Tabla que muestra la barra de cambio de tamaño de columna resaltada.](../images/sql-insights-query-pro-mode/advanced-resize-column.png)

## Paginación de tabla {#table-pagination}

La paginación se aplica automáticamente a las tablas en la característica [!UICONTROL Ver más], lo que elimina la necesidad de modificar manualmente las consultas SQL. Esta función garantiza que los datos se presenten en un formato más manejable, lo que facilita el proceso de navegar por conjuntos de datos grandes.

Puede ver hasta 500 registros por página. Para navegar por los registros, use **[!UICONTROL >]** ubicado en la parte inferior de la página.

![Resultados tabulados con resultados y paginación resaltados.](../images/sql-insights-query-pro-mode/advanced-table-pagination.png)

## Pasos siguientes

Después de leer este documento, ahora sabe cómo ver los resultados tabulados del análisis SQL del gráfico personalizado y descargar los datos como archivo CSV. Consulte el documento Ver SQL para aprender a [ver el SQL subyacente a sus datos personalizados](./view-sql.md).

También puede aprender a generar gráficos a partir de modelos de datos existentes en la interfaz de usuario de Adobe Experience Platform con la [guía del modo de diseño guiado](../standard-dashboards.md).
