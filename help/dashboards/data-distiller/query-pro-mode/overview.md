---
title: Información general sobre el modo Query Pro
description: Aprenda a utilizar consultas SQL en la interfaz de usuario de Adobe Experience Platform para generar gráficos para sus paneles personalizados.
exl-id: 15c664c4-8546-4e04-b81d-c78bf83500d3
source-git-commit: 0970fd8fbea86115d92dc78cdba753da69cc2ee6
workflow-type: tm+mt
source-wordcount: '1062'
ht-degree: 0%

---

# Información general sobre el modo Query Pro {#query-pro-mode}

El modo de consulta profesional es un flujo de trabajo basado en editor SQL que le guía a través del proceso de generación de perspectivas con consultas SQL personalizadas en la interfaz de usuario de Adobe Experience Platform. Para poder generar perspectivas con consultas SQL personalizadas, primero debe [crear un tablero](./overview.md#create-custom-dashboard).

## Componer SQL {#compose-sql}

Una vez que haya elegido crear un tablero con el modo query pro, aparecerá el cuadro de diálogo **[!UICONTROL Introducir SQL]**. Seleccione una base de datos (modelo de datos de perspectivas) para realizar una consulta desde el menú desplegable e introduzca una consulta adecuada para su conjunto de datos en el editor de query pro.

>[!NOTE]
>
>El modo de consulta profesional solo está disponible para los usuarios que hayan adquirido la SKU de Data Distiller. El [[!UICONTROL modo de diseño guiado]](../../user-defined-dashboards.md) está disponible para que todos los usuarios creen perspectivas a partir de un modelo de datos existente.

Consulte la [guía del usuario del Editor de consultas](../../../query-service/ui/user-guide.md#query-authoring) para obtener información sobre sus elementos de interfaz de usuario.

![Se ha resaltado el cuadro de diálogo [!UICONTROL Introducir SQL] con el menú desplegable del conjunto de datos y el icono de ejecución. El cuadro de diálogo tiene una consulta SQL rellenada y se muestra la pestaña de parámetros de consulta.](../../images/sql-insights/enter-sql-database-dropdown.png)

### Parámetros de consulta {#query-parameters}

Para incluir [filtros globales](./filters/global-filter.md) o [filtros de fecha](./filters/date-filter.md), su consulta **debe** usar parámetros de consulta. Al maquetar la instrucción en el modo query pro, debe proporcionar valores de muestra si la consulta utiliza parámetros de consulta. Los valores de ejemplo permiten ejecutar la instrucción SQL y crear el gráfico. Tenga en cuenta que los valores de ejemplo que proporcione al maquetar la instrucción se sustituirán por los valores reales que seleccione para la fecha o el filtro global durante la ejecución.

>[!IMPORTANT]
>
>Si desea utilizar un filtro global, debe colocar un parámetro de consulta en el SQL y luego vincular ese parámetro de consulta al filtro global en el compositor de widgets. En la captura de pantalla siguiente, `CONSENT_VALUE_FILTER` se usa en SQL como parámetro de consulta para un filtro global. Consulte la [documentación del filtro global](./filters/global-filter.md#enable-global-filter) para obtener más información sobre cómo hacerlo.

Para ejecutar la consulta, seleccione el icono de ejecución (![Icono de ejecución.](/help/images/icons/play.png)). El Editor de consultas muestra la pestaña de resultados. A continuación, para confirmar la configuración y abrir el compositor de widgets, seleccione **[!UICONTROL Seleccionar]**.

>[!TIP]
>
>Si la consulta utiliza parámetros de consulta, ejecute la consulta una vez para rellenar previamente todas las claves de parámetros de consulta utilizadas. La consulta fallará, pero la interfaz de usuario muestra automáticamente la pestaña Parámetros de consulta y enumera todas las claves incluidas. Agregue los valores adecuados para las claves.

![Cuadro de diálogo [!UICONTROL Introducir SQL] con entrada SQL, se muestra la pestaña de resultados y se resalta la opción Seleccionar.](../../images/sql-insights/enter-sql-select.png)

## Rellenar widget {#populate-widget}

El compositor de widgets ahora se rellena con las columnas del SQL ejecutado. El tipo de panel se indica en la parte superior izquierda, en este caso es [!UICONTROL Entrada SQL Manual]. Seleccione el icono de lápiz (![Un icono de lápiz.](/help/images/icons/edit.png)) para editar el SQL en cualquier momento.

>[!TIP]
>
>Los atributos disponibles son columnas tomadas del SQL ejecutado.

Para crear su widget, utilice los atributos enumerados en la columna [!UICONTROL Atributos]. Puede utilizar la barra de búsqueda para buscar atributos o desplazarse por la lista.

![Compositor de widgets con el método de creación y la columna de atributo resaltados.](../../images/sql-insights/creation-method-and-attribute-column.png)

### Añadir atributos {#add-attributes}

Para agregar un atributo al widget, seleccione el icono más (![Un icono más.](/help/images/icons/add-circle.png)) junto a un nombre de atributo. El menú desplegable que aparece permite agregar un atributo al gráfico desde las opciones determinadas por el SQL. Los distintos tipos de gráfico tienen diferentes opciones, como una lista desplegable de ejes X e Y.

En este ejemplo de gráfico circular, las opciones son tamaño y color. El color desglosa los resultados del gráfico de anillo y el tamaño es la métrica real utilizada. Agregue un atributo al campo [!UICONTROL Color] para dividir los resultados en diferentes colores según su composición de ese atributo.

>[!TIP]
>
>Seleccione el icono de flecha arriba y abajo (![El icono de flecha arriba y abajo.](/help/images/icons/switch.png)) para cambiar la disposición del eje X e Y en gráficos de barras o de líneas.

![El compositor de widgets con la lista desplegable de iconos de complemento y las flechas de cambio resaltadas.](../../images/sql-insights/add-icon-and-switch-arrows.png)

Para cambiar el tipo de gráfico del widget, selecciona una de las opciones disponibles en la lista desplegable [!UICONTROL Marcas]. Las opciones incluyen [!UICONTROL Línea], [!UICONTROL Anillo], [!UICONTROL Número grande] y [!UICONTROL Barra]. Una vez seleccionada, se genera una visualización previa de la configuración actual del widget.

![Compositor de widgets con la vista previa de widget resaltada.](../../images/sql-insights/widget-preview.png)

## Propiedades del widget {#properties}

Seleccione el icono de propiedades (![El icono de propiedades.](/help/images/icons/properties.png)) en el carril derecho para abrir el panel de propiedades. En el panel [!UICONTROL Propiedades], escriba un nombre para el widget en el campo de texto **[!UICONTROL Título del widget]**. También puede cambiar el nombre de varios aspectos del gráfico.

>[!NOTE]
>
>Los campos específicos disponibles en la barra lateral de propiedades varían según el tipo de gráfico que esté editando.

![Compositor de widgets con el icono de propiedades y el campo de título de widget resaltados.](../../images/sql-insights/widget-properties-title-text.png)

## Guarde el widget {#save-widget}

Al guardar en el compositor de widgets, se guarda el widget localmente en el tablero. Si desea guardar el trabajo y reanudarlo más tarde, seleccione **[!UICONTROL Guardar]**. Un icono de verificación debajo del nombre del widget indica que el widget se ha guardado. Alternativamente, cuando esté satisfecho con el widget, seleccione **[!UICONTROL Guardar y cerrar]** para que el widget esté disponible para todos los demás usuarios con acceso a su panel. Seleccione Cancelar para abandonar su trabajo y volver a su panel personalizado.

![El compositor de widgets con las opciones Guardar, Widget guardado y Guardar y cerrar resaltadas.](../../images/sql-insights/insight-saved.png)

## Edite el tablero y los gráficos {#edit}

Seleccione **[!UICONTROL Editar]** para editar todo el tablero o cualquiera de sus datos. Desde el modo de edición, puede cambiar el tamaño de los widgets, editar el SQL o crear y aplicar filtros globales y temporales. Estos filtros restringen los datos mostrados en los widgets del panel. Es una forma cómoda de actualizar y ajustar rápidamente sus perspectivas para diferentes casos de uso.

![Panel personalizado con la opción Editar resaltada.](../../images/sql-insights/edit-dashboard.png)

Seleccione **[!UICONTROL Agregar filtro]** para crear un [[!UICONTROL Filtro de fecha]](#create-date-filter) o un [[!UICONTROL Filtro global]](#create-global-filter). Una vez creados, todos los filtros globales y de fecha están disponibles en [el icono de filtro](#select-global-filter) (![Un icono de filtro.](/help/images/icons/filter.png)) de su tablero.

![Panel personalizado con el menú desplegable Agregar filtro resaltado.](../../images/query-pro-mode/add-filter.png)

## Editar, duplicar o eliminar una perspectiva

Consulte la guía de panel personalizado para obtener instrucciones sobre cómo [editar, duplicar o eliminar un widget existente](../../user-defined-dashboards.md#duplicate).

## Pasos siguientes

Después de leer este documento, ahora sabe cómo escribir consultas SQL en la interfaz de usuario de Adobe Experience Platform para generar gráficos para sus paneles personalizados. A continuación, debería aprender a enriquecer aún más los datos [creando un filtro de fecha](./filters/date-filter.md) o [creando un filtro global](./filters/global-filter.md).

También puede obtener más información sobre otras características de Perspectivas personalizadas, como [las diferentes opciones de visualización de los datos analizados por SQL](./view-more.md) o cómo [ver el SQL subyacente a sus perspectivas personalizadas](./view-sql.md).
