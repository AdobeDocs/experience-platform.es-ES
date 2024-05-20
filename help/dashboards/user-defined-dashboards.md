---
title: Paneles personalizados
description: Obtenga información sobre cómo crear y administrar paneles personalizados, donde puede crear, añadir y editar widgets personalizados para visualizar métricas clave.
exl-id: a9ab83f7-b68d-4dbf-9dc6-ef253df5c82c
source-git-commit: 17ad52864bbca09844c0241b6451e6811bd8f413
workflow-type: tm+mt
source-wordcount: '1624'
ht-degree: 3%

---

# Paneles personalizados

Utilice los paneles de Adobe Experience Platform para acelerar las perspectivas y personalizar la visualización a través de la función de paneles. Utilice esta función para crear y administrar paneles personalizados, donde puede crear, añadir y editar widgets personalizados para visualizar métricas clave relevantes para su organización.


<!-- Getting started / permissions section commented out for Beta. This will be necessary after GA only

## Getting started

To view dashboards in Adobe Experience Platform you must have the appropriate permissions enabled. Please read the [dashboards permissions documentation](./permissions.md#available-permissions) to learn how to grant users the ability to view, edit, and update Experience Platform dashboards using Adobe Admin Console. If you do not have administrator privileges for your organization, contact your product administrator to obtain the required permissions. -->

## Crear un tablero personalizado

Para crear un tablero personalizado, primero, navegue hasta el inventario del tablero. Seleccionar **[!UICONTROL Paneles]** en la navegación izquierda de la interfaz de usuario de Platform seguida de **[!UICONTROL Crear tablero]**.

![El inventario de tableros con Tableros en la navegación izquierda y &quot;Crear tablero&quot; resaltado.](./images/user-defined-dashboards/create-dashboard.png)

Antes de agregar un tablero personalizado, el inventario de los tableros está vacío y muestra el mensaje &quot;No se encontraron tableros&quot;. Mensaje. Una vez creados, todos los tableros se enumeran en el inventario de tableros.

<!-- >[!NOTE]
>
>To edit an existing dashboard, select the dashboard name from the inventory list followed by the pencil icon (![A pencil icon.](./images/user-defined-dashboards/edit-icon.png))
>![A custom inventory listed in the dashboard inventory.](./images/user-defined-dashboards/dashbaord-inventory.png "A custom inventory listed in the dashboard inventory."){width="100" zoomable="yes"} -->

El [!UICONTROL Crear tablero] aparece el cuadro de diálogo. Introduzca un nombre descriptivo y sencillo para la colección de widgets que desea crear y seleccione **[!UICONTROL Guardar]**.

![Cuadro de diálogo Crear tablero.](./images/user-defined-dashboards/create-dashboard-dialog.png)

Los usuarios que hayan adquirido la SKU de Data Distiller tienen la opción de utilizar consultas SQL personalizadas para crear sus perspectivas. Consulte la [Guía de creación de perspectiva personalizable](./data-distiller/customizable-insights/overview.md) para obtener instrucciones sobre este flujo de trabajo.

El tablero en blanco recién creado aparecerá con el nombre elegido en la esquina superior izquierda de la vista.

## Crear un widget {#create-widget}

>[!CONTEXTUALHELP]
>id="platform_dashboards_udd_maxwidgets"
>title="Número máximo de widgets"
>abstract="Los tableros de servicio admiten hasta diez widgets. Después de añadir diez widgets al tablero, la opción [!UICONTROL Añadir nuevo widget] está desactivada y aparece en gris."

En la nueva vista de panel, seleccione **[!UICONTROL Añadir nuevo widget]** para iniciar el proceso de creación del widget.

>[!IMPORTANT]
>
>Cada tablero admite hasta diez widgets. Después de añadir diez widgets al tablero, la opción [!UICONTROL Añadir nuevo widget] está desactivada y aparece en gris.

![El nuevo tablero vacío con Agregar nuevo widget resaltado.](./images/user-defined-dashboards/add-new-widget.png)

### Compositor de widgets

Aparecerá el espacio de trabajo del compositor de widgets. A continuación, seleccione **[!UICONTROL Seleccionar datos]** para elegir el modelo de datos desde el que desea agregar atributos a los widgets.

![El espacio de trabajo del compositor de widgets.](./images/user-defined-dashboards/widget-composer.png)

#### Seleccionar modelo de datos {#select-data-model}

El [!UICONTROL Seleccionar modelo de datos] aparece el cuadro de diálogo. Seleccione un modelo de datos de la columna izquierda para mostrar una lista de vista previa de todas las tablas disponibles. El modelo de datos preconfigurado para Real-time Customer Data Platform se denomina [!UICONTROL CDPInsights].

>[!TIP]
>
>Seleccione el icono de información (![Un icono de información.](./images/user-defined-dashboards/info-icon.png)) para ver el nombre completo del modelo de datos si es demasiado largo para mostrarlo en el carril de datos.

![Cuadro de diálogo Seleccionar datos.](./images/user-defined-dashboards/select-data-model-dialog.png)

La lista de vista previa proporciona detalles sobre las tablas contenidas en el modelo de datos. La siguiente tabla proporciona descripciones de los campos de columna y sus valores potenciales.

| Campo de columna | Descripción |
|---|---|
| [!UICONTROL Título] | Nombre de la tabla. |
| [!UICONTROL Tipo de tabla] | El tipo de tabla. Los tipos potenciales incluyen: `fact`, `dimension`, y `none`. |
| [!UICONTROL Registros] | El número de registros asociados con la tabla seleccionada. |
| [!UICONTROL Búsquedas] | Número de tablas unidas a la tabla elegida. |
| [!UICONTROL Atributos] | Número de atributos de la tabla seleccionada. |

Seleccionar **[!UICONTROL Siguiente]** para confirmar la elección del modelo de datos. La vista siguiente muestra una lista de las tablas disponibles en el carril izquierdo. Seleccione una tabla para ver un desglose completo de los datos contenidos en la tabla seleccionada.

### Rellenar widget {#populate-widget}

El [!UICONTROL Previsualizar] el panel contiene pestañas para [!UICONTROL Registros de muestra] y [!UICONTROL Atributos]. El [!UICONTROL Registros de muestra] proporciona un subconjunto de los registros de la tabla seleccionada en una vista tabulada. El [!UICONTROL Atributos] proporciona el nombre del atributo, el tipo de datos y la tabla de origen de cada atributo asociado a la tabla seleccionada.

Seleccione una tabla de la lista disponible en el carril izquierdo para proporcionar datos para el widget y seleccione **[!UICONTROL Seleccionar]** para volver al compositor de widgets.

![El cuadro de diálogo Seleccionar datos con la selección resaltada.](./images/user-defined-dashboards/select-a-table.png)

El compositor de widgets ahora se rellena con datos de la tabla elegida.

El modelo de datos y la tabla seleccionada actualmente se muestran en la parte superior del carril izquierdo y los atributos disponibles para crear el widget se enumeran en la [!UICONTROL Atributos] columna. Puede utilizar la barra de búsqueda para buscar atributos en lugar de desplazarse por la lista o cambiar el modelo de datos seleccionado seleccionando el icono de lápiz (![Icono de lápiz.](./images/user-defined-dashboards/edit-icon.png)) en el carril izquierdo.

![Un widget rellenado con datos dentro del compositor de widgets.](./images/user-defined-dashboards/populated-widget-composer.png)

#### Añadir y filtrar atributos {#add-and-filter-attributes}

Seleccione el icono de añadir (![Un icono de añadir.](./images/user-defined-dashboards/add-icon.png)) junto al nombre de un atributo para agregar un atributo al widget. El menú desplegable que aparece le permite agregar un atributo como eje X, eje Y, color o filtro para el widget. El [!UICONTROL Color] El atributo permite diferenciar los resultados de las marcas del eje X e Y en función del color. Para ello, divide los resultados en diferentes colores según su composición de un tercer atributo.

>[!TIP]
>
>Si desea voltear la disposición de los ejes X e Y, seleccione el icono de flecha arriba y abajo (![El icono de flecha arriba y abajo.](./images/user-defined-dashboards/switch-axis-icon.png)) para cambiar su disposición.

![El compositor de widgets con la lista desplegable de add-icon resaltada.](./images/user-defined-dashboards/attributes-dropdown.png)

Para cambiar el tipo de gráfico del widget, seleccione la opción [!UICONTROL Marcas] y elija entre las opciones disponibles. Las opciones incluyen barras, puntos, marcas, líneas o áreas. Una vez seleccionada, se genera una visualización previa de la configuración actual del widget.

![Compositor de widgets con la lista desplegable Marcas resaltada.](./images/user-defined-dashboards/marks-dropdown.png)

Al agregar un atributo como filtro, puede seleccionar qué valores desea incluir o excluir del widget. Después de agregar un filtro desde la lista de atributos, la variable [!UICONTROL Filtrar] aparece un cuadro de diálogo en el que puede seleccionar o anular la selección de valores con su casilla de verificación.

![El cuadro de diálogo de filtro para filtrar los valores del widget.](./images/user-defined-dashboards/filter-dialog.png)

#### Filtrado de datos históricos {#filter-historical-data}

Para filtrar los datos históricos a partir de las perspectivas generadas por el widget, agregue la variable `date_key` como filtro y seleccione **[!UICONTROL Fecha reciente]** seguido de **[!UICONTROL Aplicar]**. Este filtro garantiza que los datos utilizados para obtener perspectivas se tomen de la instantánea del sistema más reciente.

![El [!UICONTROL Filtro: date_key] diálogo con [!UICONTROL Fecha reciente] y [!UICONTROL Aplicar] resaltado.](./images/user-defined-dashboards/recent-date.png)

También puede crear un punto personalizado para filtrar los datos. Seleccionar **[!UICONTROL Seleccionar fechas]** para ampliar el cuadro de diálogo con una lista de fechas disponibles. Utilice el **[!UICONTROL Seleccionar todo]** para activar o desactivar todas las opciones disponibles, o bien marque la casilla de verificación de cada día de forma individual. Finalmente, seleccione **[!UICONTROL Aplicar]** para confirmar sus opciones.

>[!NOTE]
>
>Si la variable `date_key` ya se ha añadido el atributo como filtro, seleccione los puntos suspensivos seguidos de **[!UICONTROL Editar]** en las opciones desplegables para cambiar el periodo de filtro.

![El [!UICONTROL Filtro: date_key] diálogo con casillas de verificación de día individuales marcadas y desmarcadas.](./images/user-defined-dashboards/select-dates.png)

### Propiedades del widget

Seleccione el icono de propiedades (![El icono de propiedades.](./images/user-defined-dashboards/properties-icon.png)) en el carril derecho para abrir el panel de propiedades. En el [!UICONTROL Propiedades] , introduzca un nombre para el widget en el panel [!UICONTROL Título del widget] campo de texto.

![Panel de propiedades con el icono de propiedades y el campo de título del widget resaltado.](./images/user-defined-dashboards/properties-panel.png)

Desde el panel de propiedades del widget, puede editar varios aspectos del widget. Dispone del control completo para editar la ubicación de la leyenda del widget. Para mover la leyenda, seleccione la [!UICONTROL Ubicación de leyenda] y elija la ubicación que desee en la lista de opciones disponibles. También puede cambiar el nombre de la etiqueta asociada con la leyenda y el eje X o Y introduciendo un nuevo nombre en la etiqueta [!UICONTROL Título de leyenda] campo de texto, o [!UICONTROL Etiqueta del eje] campo de texto respectivamente.

#### Guarde el widget {#save-widget}

Al guardar en el compositor de widgets, se guarda el widget localmente en el tablero. Si desea guardar el trabajo y reanudarlo más adelante, seleccione **[!UICONTROL Guardar]**. Un icono de verificación debajo del nombre del widget indica que el widget se ha guardado. Como alternativa, cuando esté satisfecho con el widget, seleccione **[!UICONTROL Guardar y cerrar]** para que el widget esté disponible para todos los demás usuarios con acceso a su tablero. Seleccionar **[!UICONTROL Cancelar]** para abandonar su trabajo y volver a su tablero personalizado.

![Nueva confirmación de guardado del widget.](./images/user-defined-dashboards/save-confirmation.png)

>[!TIP]
>
>Seleccione el icono de propiedades (![El icono de propiedades.](./images/user-defined-dashboards/properties-icon.png)) junto al nombre del tablero para ver detalles sobre su creación. Puede cambiar el nombre del panel en el cuadro de diálogo que aparece.

Los widgets se pueden reorganizar y cambiar de tamaño en este espacio de trabajo. Seleccionar **[!UICONTROL Guardar]** para conservar el nombre del tablero y el diseño configurado.

![El tablero definido por el usuario con un widget personalizado y el botón de guardar resaltados.](./images/user-defined-dashboards/user-defined-dashboard.png)

Para garantizar que cada consulta de un panel de perspectivas de Adobe Real-time Customer Data Platform tenga suficientes recursos para ejecutarse de forma eficaz, la API rastrea el uso de recursos asignando espacios de concurrencia a cada consulta. El sistema puede procesar hasta cuatro consultas simultáneas y, por lo tanto, hay cuatro ranuras de consulta simultáneas disponibles en cualquier momento. Las consultas se colocan en una cola basada en ranuras de concurrencia y, a continuación, espere en la cola hasta que haya suficientes ranuras de concurrencia disponibles.

### Editar, duplicar o eliminar un widget {#duplicate}

Una vez creado un widget, puede editar, duplicar o eliminar widgets completos desde el panel personalizado.

>[!TIP]
>
>Para cambiar entre cualquiera de los paneles personalizados existentes, seleccione Paneles en la barra de navegación izquierda y, a continuación, seleccione el nombre del panel en la lista de inventario.

Seleccione el icono de lápiz (![Un icono de lápiz.](./images/user-defined-dashboards/edit-icon.png)) desde la parte superior derecha del panel personalizado para entrar en el modo de edición.

![Un panel personalizado con el icono de lápiz resaltado.](./images/user-defined-dashboards/edit-mode.png)

A continuación, seleccione los puntos suspensivos en la parte superior derecha del widget que desea editar, copiar o eliminar. Seleccione la acción adecuada en el menú desplegable.

![Un widget en un panel personalizado con los puntos suspensivos y el widget de duplicado resaltados.](./images/user-defined-dashboards/duplicate.png)

>[!NOTE]
>
>La duplicación le permite personalizar los atributos de una perspectiva para crear un widget único sin tener que empezar desde cero. Si duplica un widget, aparecerá en el panel personalizado. A continuación, puede seleccionar los puntos suspensivos del nuevo widget seguido de **[!UICONTROL Editar]**, para personalizar su perspectiva.

## Pasos siguientes y recursos adicionales

Al leer este documento, tiene una mejor comprensión de cómo crear un panel personalizado y cómo crear, editar y actualizar widgets personalizados para ese panel.

Para descubrir las métricas y visualizaciones preconfiguradas disponibles para [perfiles](./guides/profiles.md#standard-widgets), [segmentos](./guides/audiences.md#standard-widgets), y [destinos](./guides/destinations.md#standard-widgets) En los paneles, consulte la lista de widgets estándar en su documentación respectiva.

Para reforzar su comprensión de los paneles de Experience Platform, vea el siguiente vídeo:

>[!VIDEO](https://video.tv.adobe.com/v/3409637?quality=12&learn=on)
