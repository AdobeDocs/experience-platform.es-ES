---
title: Crear un filtro de fecha
description: Obtenga información sobre cómo filtrar sus perspectivas personalizadas por fecha.
exl-id: fa05d651-ea43-41f0-9b7d-f19c4a9ac256
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 0%

---

# Creación de un filtro de fecha {#create-date-filter}

Para filtrar las perspectivas por fecha, debe agregar parámetros a las consultas SQL que puedan aceptar restricciones de fecha. Esto se realiza como parte del flujo de trabajo de creación de perspectivas del modo query pro. Consulte la [documentación del modo query pro](#query-pro-mode) para obtener información sobre cómo introducir SQL para sus datos.

Los parámetros de consulta permiten trabajar con datos dinámicos, ya que actúan como marcadores de posición para los valores que agrega en el momento de la ejecución. Estos valores de marcador de posición se pueden actualizar a través de la interfaz de usuario y permiten que usuarios menos técnicos actualicen las perspectivas en función de intervalos de fechas.

Si no está familiarizado con los parámetros de consulta, consulte la documentación para obtener [instrucciones sobre cómo implementar consultas parametrizadas](../../../../query-service/ui/parameterized-queries.md).

## Aplicar un filtro de fecha a un panel {#apply-date-filter}

Para aplicar un filtro de fecha, seleccione **[!UICONTROL Agregar filtro]** y, a continuación, **[!UICONTROL Filtro de fecha]** en el menú desplegable de la vista de panel.

![Panel personalizado con el elemento Agregar filtro y su menú desplegable resaltados.](../../../images/customizable-insights/add-filter.png)

## Edite el SQL para incluir parámetros de consulta de fecha {#include-date-parameters}

A continuación, asegúrese de que SQL incluya parámetros de consulta para permitir un intervalo de fechas. Si todavía no ha incorporado parámetros de consulta en el SQL, edite las perspectivas para incluir estos parámetros. Consulte la documentación para obtener instrucciones sobre cómo [editar una perspectiva](../query-pro-mode.md#edit).

>[!TIP]
>
>Se recomienda agregar los parámetros `$START_DATE` y `$END_DATE` a la instrucción SQL en cada uno de los gráficos para los que desea habilitar los filtros de fecha.

>[!NOTE]
>
>Los filtros de fecha no admiten restricciones temporales. El filtro solo se aplica a intervalos de fechas. Esto significa que si tiene varios informes en un periodo de 24 horas, no puede distinguir entre distintas horas dentro del mismo día. Por este motivo, se recomienda convertir el componente de tiempo como una fecha.

Si el modelo de datos o las tablas que está analizando tienen un componente de tiempo, puede agrupar los datos por fecha y, a continuación, aplicar estos filtros de fecha.

La instrucción SQL de ejemplo siguiente muestra cómo incorporar `$START_DATE` y `$END_DATE` parámetros y utiliza `cast` para enmarcar el componente de tiempo como una fecha.

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

![Cuadro de diálogo [!UICONTROL Introducir SQL] con los parámetros de fecha resaltados en el SQL.](../../../images/customizable-insights/sql-date-parameters.png)

## Habilitar parámetros de fecha en cada perspectiva {#enable-date-parameters}

Una vez que haya incorporado los parámetros adecuados al SQL de sus perspectivas, las variables `Start_date` y `End_date` ya están disponibles como alternadores en el compositor de widgets. Consulte la [sección de población de widgets del modo query pro](#populate-widget) para obtener información sobre cómo editar una perspectiva.

En el compositor de widgets, seleccione las alternancias para habilitar los parámetros `Start_date` y `End_date`.

![El compositor de widgets con los valores Start_date y End_date resaltados.](../../../images/customizable-insights/widget-composer-date-filter-toggles.png)

A continuación, seleccione los parámetros de consulta adecuados en los menús desplegables.

![El compositor de widgets con el menú desplegable Start_date resaltado.](../../../images/customizable-insights/widget-composer-date-filter-dropdown.png)

Finalmente, selecciona **[!UICONTROL Guardar y cerrar]** para regresar a tu panel. Los filtros de fecha ahora están habilitados para todas las perspectivas que tienen parámetros de fecha de inicio y finalización.

## Uso del filtro de fecha

Para utilizar un filtro de fecha personalizado, seleccione el icono de calendario y elija un inicio y un final en la vista de calendario.

>[!IMPORTANT]
>
>Añadir simplemente un filtro de fecha no hará que los gráficos cambien. Debe editar cada una de las perspectivas para incluir las fechas de inicio y finalización seleccionadas.

![Panel personalizado con el calendario de filtro de fecha resaltado.](../../../images/customizable-insights/date-filter.png)

Una vez que haya seleccionado un intervalo de fechas en el panel, las perspectivas que tengan parámetros de fecha en su SQL verán las opciones de filtro de fecha en el compositor de widgets.

>[!NOTE]
>
>Al seleccionar un intervalo de fechas en el panel, se muestran los alternadores para filtros de fecha como parte del flujo de trabajo de creación de perspectivas.

## Eliminación de un filtro de fecha {#delete-date-filter}

Para quitar el filtro de fecha, seleccione el icono Eliminar filtro (![El icono Eliminar filtro.](/help/images/icons/filter-delete.png)).

![Panel personalizado con el icono de eliminación de filtro resaltado.](../../../images/customizable-insights/delete-date-filter.png)
