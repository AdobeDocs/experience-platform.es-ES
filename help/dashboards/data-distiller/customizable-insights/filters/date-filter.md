---
title: Crear un filtro de fecha
description: Obtenga información sobre cómo filtrar sus perspectivas personalizadas por fecha.
source-git-commit: 17ad52864bbca09844c0241b6451e6811bd8f413
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 0%

---

# Creación de un filtro de fecha {#create-date-filter}

Para filtrar las perspectivas por fecha, debe agregar parámetros a las consultas SQL que puedan aceptar restricciones de fecha. Esto se realiza como parte del flujo de trabajo de creación de perspectivas del modo query pro. Consulte la [documentación del modo query pro](#query-pro-mode) para aprender a introducir SQL para sus perspectivas.

Los parámetros de consulta permiten trabajar con datos dinámicos, ya que actúan como marcadores de posición para los valores que agrega en el momento de la ejecución. Estos valores de marcador de posición se pueden actualizar a través de la interfaz de usuario y permiten que usuarios menos técnicos actualicen las perspectivas en función de intervalos de fechas.

Si no conoce los parámetros de consulta, consulte la documentación de [instrucciones sobre cómo implementar consultas con parámetros](../../../../query-service/ui/parameterized-queries.md).

## Aplicar un filtro de fecha a un panel {#apply-date-filter}

Para aplicar un filtro de fecha, seleccione **[!UICONTROL Añadir filtro]**, entonces **[!UICONTROL Filtro de fecha]** en el menú desplegable de la vista de panel.

![Un panel personalizado con el filtro Agregar y su menú desplegable resaltado.](../../../images/customizable-insights/add-filter.png)

## Edite el SQL para incluir parámetros de consulta de fecha {#include-date-parameters}

A continuación, asegúrese de que SQL incluya parámetros de consulta para permitir un intervalo de fechas. Si todavía no ha incorporado parámetros de consulta en el SQL, edite las perspectivas para incluir estos parámetros. Consulte la documentación para obtener instrucciones sobre cómo [editar una perspectiva](../query-pro-mode.md#edit).

>[!TIP]
>
>Se recomienda añadir `$START_DATE` y `$END_DATE` parámetros a la instrucción SQL en cada uno de los gráficos para los que desea habilitar filtros de fecha.

>[!NOTE]
>
>Los filtros de fecha no admiten restricciones temporales. El filtro solo se aplica a intervalos de fechas. Esto significa que si tiene varios informes en un periodo de 24 horas, no puede distinguir entre distintas horas dentro del mismo día. Por este motivo, se recomienda convertir el componente de tiempo como una fecha.

Si el modelo de datos o las tablas que está analizando tienen un componente de tiempo, puede agrupar los datos por fecha y, a continuación, aplicar estos filtros de fecha.

La instrucción SQL de ejemplo siguiente muestra cómo incorporar `$START_DATE` y `$END_DATE` parámetros y usos `cast` para enmarcar el componente tiempo como una fecha.

```sql
SELECT Sum(personalization_consent_count) AS Personalization,
       Sum(datacollection_consent_count)  AS Datacollection,
       Sum(datasharing_consent_count)     AS Datasharing
FROM   fact_daily_consent_aggregates f
       INNER JOIN dim_consent_valued
               ON f.consent_value_id = d.consent_value_id
WHERE  f.date BETWEEN Upper(Coalesce(Cast('$START_DATE' AS date), '')) AND Upper
                      (
                             Coalesce(Cast('$END_DATE' AS date), ''))
       AND ( ( Upper(Coalesce($consent_value_filter, '')) IN ( '', 'NULL' ) )
              OR ( f.consent_value_id IN ( $consent_value_filter ) ) )
LIMIT  0; 
```

La captura de pantalla siguiente resalta las restricciones de fecha incorporadas en la instrucción SQL y los pares de valor clave de parámetro de consulta.

>[!NOTE]
>
>Al maquetar la instrucción en modo query pro, debe proporcionar valores de ejemplo para cada parámetro para ejecutar la instrucción SQL y crear el gráfico. Los valores de ejemplo que proporcione al maquetar la instrucción se sustituirán por los valores reales que seleccione para el filtro de fecha (o global) durante la ejecución.

![El [!UICONTROL Introducir SQL] con los parámetros de fecha resaltados en el SQL.](../../../images/customizable-insights/sql-date-parameters.png)

## Habilitar parámetros de fecha en cada perspectiva {#enable-date-parameters}

Una vez que haya incorporado los parámetros adecuados al SQL de sus perspectivas, la variable `Start_date` y `End_date` Las variables de ya están disponibles como alternadores en el compositor de widgets. Consulte la [sección de población de widgets del modo query pro](#populate-widget) para obtener información sobre cómo editar una perspectiva.

En el compositor de widgets, seleccione alternadores para habilitar el `Start_date` y `End_date` parámetros.

![El compositor de widgets con los alternadores Start_date y End_date resaltados.](../../../images/customizable-insights/widget-composer-date-filter-toggles.png)

A continuación, seleccione los parámetros de consulta adecuados en los menús desplegables.

![Compositor de widgets con el menú desplegable Fecha_inicial resaltado.](../../../images/customizable-insights/widget-composer-date-filter-dropdown.png)

Finalmente, seleccione **[!UICONTROL Guardar y cerrar]** para volver al tablero. Los filtros de fecha ahora están habilitados para todas las perspectivas que tienen parámetros de fecha de inicio y finalización.

## Uso del filtro de fecha

Para utilizar un filtro de fecha personalizado, seleccione el icono de calendario y elija un inicio y un final en la vista de calendario.

>[!IMPORTANT]
>
>Añadir simplemente un filtro de fecha no hará que los gráficos cambien. Debe editar cada una de las perspectivas para incluir las fechas de inicio y finalización seleccionadas.

![Un panel personalizado con el calendario del filtro de fecha resaltado.](../../../images/customizable-insights/date-filter.png)

Una vez que haya seleccionado un intervalo de fechas en el panel, las perspectivas que tengan parámetros de fecha en su SQL verán las opciones de filtro de fecha en el compositor de widgets.

>[!NOTE]
>
>Al seleccionar un intervalo de fechas en el panel, se muestran los alternadores para filtros de fecha como parte del flujo de trabajo de creación de perspectivas.

## Eliminación de un filtro de fecha {#delete-date-filter}

Para eliminar el filtro de fecha, seleccione el icono Eliminar filtro (![Icono Eliminar filtro.](../../../images/customizable-insights/delete-filter-icon.png)).

![Un tablero personalizado con el icono de eliminación de filtro resaltado.](../../../images/customizable-insights/delete-date-filter.png)
