---
title: Tableros definidos por el usuario
description: Aprenda a crear y administrar tableros personalizados donde puede crear, agregar y editar widgets personalizados para visualizar métricas clave.
exl-id: a9ab83f7-b68d-4dbf-9dc6-ef253df5c82c
source-git-commit: a0be2f8625ca60f9c8f355c1230a889002436d6d
workflow-type: tm+mt
source-wordcount: '1307'
ht-degree: 0%

---

# Tableros definidos por el usuario

Los paneles de Adobe Experience Platform le ayudan a acelerar la información y a personalizar la visualización mediante la función de paneles definida por el usuario. Esta función le permite crear y administrar tableros personalizados en los que puede crear, agregar y editar widgets personalizados para visualizar métricas clave relevantes para su organización.

<!-- Getting started / permissions section commented out for Beta. This will be necessary after GA only

## Getting started

To view dashboards in Adobe Experience Platform you must have the appropriate permissions enabled. Please read the [dashboards permissions documentation](./permissions.md#available-permissions) to learn how to grant users the ability to view, edit, and update Experience Platform dashboards using Adobe Admin Console. If you do not have administrator privileges for your organization, contact your product administrator to obtain the required permissions. -->

## Crear un tablero personalizado

Para crear un tablero personalizado, primero, vaya al inventario del tablero. Select **[!UICONTROL Tableros]** desde la navegación izquierda de la interfaz de usuario de Platform seguida de **[!UICONTROL Crear tablero]**.

![El inventario de tableros con Tableros en el panel de navegación izquierdo y &quot;Crear tablero&quot; resaltado.](./images/user-defined-dashboards/create-dashboard.png)

Antes de agregar un tablero personalizado, el inventario de tableros está vacío y muestra &quot;No se encontraron tableros&quot;. mensaje. Una vez creados, todos los tableros definidos por el usuario se enumeran en el inventario de tableros.

>[!NOTE]
>
>Para editar un tablero existente, seleccione el nombre del tablero en la lista de inventario seguido del icono de lápiz (![Un icono de lápiz.](./images/user-defined-dashboards/edit-icon.png))

La variable [!UICONTROL Crear tablero] se abre. Escriba un nombre descriptivo y reconocible para la colección de widgets que desee crear y seleccione **[!UICONTROL Guardar]**.

![El cuadro de diálogo Crear tablero .](./images/user-defined-dashboards/create-dashboard-dialog.png)

El panel en blanco recién creado aparece con el nombre elegido en la esquina superior izquierda de la vista.

## Crear un widget {#create-widget}

>[!CONTEXTUALHELP]
>id="platform_dashboards_udd_maxwidgets"
>title="Número máximo de widgets"
>abstract="Los tableros definidos por el usuario admiten hasta diez widgets. Después de agregar diez widgets al tablero, la variable [!UICONTROL Agregar nueva utilidad] está desactivada y aparece en gris."

En la nueva vista de tablero, seleccione **[!UICONTROL Agregar nueva utilidad]** para iniciar el proceso de creación de la utilidad.

>[!IMPORTANT]
>
>Los tableros definidos por el usuario admiten hasta diez widgets. Después de agregar diez widgets al tablero, la variable [!UICONTROL Agregar nueva utilidad] está desactivada y aparece en gris.

![El nuevo tablero vacío con Añadir nuevo widget resaltado.](./images/user-defined-dashboards/add-new-widget.png)

### Compositor de utilidades

Aparecerá el espacio de trabajo del compositor de utilidades. A continuación, seleccione **[!UICONTROL Seleccionar datos]** para elegir el modelo de datos desde el que añadir atributos a las utilidades.

![El espacio de trabajo del compositor de utilidades.](./images/user-defined-dashboards/widget-composer.png)

#### Seleccionar modelo de datos {#select-data-model}

La variable [!UICONTROL Seleccionar modelo de datos] se abre. Seleccione un modelo de datos de la columna izquierda para mostrar una lista de vista previa de todas las tablas disponibles. El modelo de datos preconfigurado para Real-time Customer Data Platform recibe su nombre [!UICONTROL CDPInsights].

>[!TIP]
>
>Seleccione el icono de información (![Un icono de información.](./images/user-defined-dashboards/info-icon.png)) para ver el nombre completo del modelo de datos si es demasiado largo para mostrarlo en el carril de datos.

![El cuadro de diálogo Seleccionar datos .](./images/user-defined-dashboards/select-data-model-dialog.png)

La lista de vista previa proporciona detalles sobre las tablas contenidas en el modelo de datos. La tabla siguiente proporciona descripciones de los campos de columna y sus valores potenciales.

| Campo de columna | Descripción |
|---|---|
| [!UICONTROL Título] | Nombre de la tabla. |
| [!UICONTROL Tipo de tabla] | Tipo de tabla. Los tipos posibles incluyen: `fact`, `dimension`y `none`. |
| [!UICONTROL Registros] | Número de registros asociados a la tabla elegida. |
| [!UICONTROL Búsquedas] | Número de tablas unidas a la tabla elegida. |
| [!UICONTROL Atributos] | Número de atributos de la tabla elegida. |

Select **[!UICONTROL Siguiente]** para confirmar la elección del modelo de datos. La siguiente vista muestra una lista de las tablas disponibles en el carril izquierdo. Seleccione una tabla para ver un desglose completo de los datos contenidos en la tabla seleccionada.

### Rellenar widget {#populate-widget}

La variable [!UICONTROL Vista previa] El panel contiene fichas para [!UICONTROL Registros de muestra] y [!UICONTROL Atributos]. La variable [!UICONTROL Registros de muestra] proporciona un subconjunto de los registros de la tabla seleccionada en una vista tabulada. La variable [!UICONTROL Atributos] proporciona el nombre del atributo, el tipo de datos y la tabla de origen para cada atributo asociado a la tabla seleccionada.

Seleccione una tabla de la lista disponible en el carril izquierdo para proporcionar datos para el widget y seleccione **[!UICONTROL Select]** para volver al compositor de utilidades.

![El cuadro de diálogo seleccionar datos con la selección resaltada.](./images/user-defined-dashboards/select-a-table.png)

El compositor de utilidades ahora se rellena con datos de la tabla elegida.

El modelo de datos y la tabla seleccionada actualmente se muestran en la parte superior del carril izquierdo, y los atributos disponibles para crear el widget se enumeran en la [!UICONTROL Atributos] para abrir el Navegador. Puede utilizar la barra de búsqueda para buscar atributos en lugar de desplazarse por la lista, o cambiar el modelo de datos seleccionado seleccionando el icono de lápiz (![Icono de lápiz.](./images/user-defined-dashboards/edit-icon.png)) en el carril izquierdo.

![Un widget rellenado con datos dentro del compositor de utilidades.](./images/user-defined-dashboards/populated-widget-composer.png)

#### Añadir y filtrar atributos {#add-and-filter-attributes}

Seleccione el icono añadir (![Un icono de añadir.](./images/user-defined-dashboards/add-icon.png)) junto al nombre de un atributo para agregar un atributo al widget. El menú desplegable que aparece le permite añadir un atributo como eje X, eje Y, color o filtro para el widget. La variable [!UICONTROL Color] permite diferenciar los resultados de las marcas de los ejes X e Y según el color. Para ello, divide los resultados en diferentes colores según su composición de un tercer atributo.

>[!TIP]
>
>Si desea girar la disposición de los ejes X e Y, seleccione el icono de flecha arriba y abajo (![El icono de flecha arriba y abajo.](./images/user-defined-dashboards/switch-axis-icon.png)) para cambiar de disposición.

![El compositor de utilidades con el menú desplegable de icono de complemento resaltado.](./images/user-defined-dashboards/attributes-dropdown.png)

Para cambiar el tipo de gráfico de la utilidad, seleccione la opción [!UICONTROL Marcas] y elija entre las opciones disponibles. Las opciones incluyen barras, puntos, comillas, líneas o áreas. Una vez seleccionada, se genera una visualización previa de la configuración actual del widget.

![El compositor de utilidades con la lista desplegable Marcas resaltada.](./images/user-defined-dashboards/marks-dropdown.png)

Al agregar un atributo como filtro, puede seleccionar qué valores incluir o excluir del widget. Después de agregar un filtro de la lista de atributos, la variable [!UICONTROL Filtro] aparece el cuadro de diálogo donde puede seleccionar o deseleccionar valores mediante su casilla de verificación.

![El cuadro de diálogo de filtro para filtrar valores del widget.](./images/user-defined-dashboards/filter-dialog.png)

### Propiedades de los widgets

Seleccione el icono de propiedades (![El icono de propiedades.](./images/user-defined-dashboards/properties-icon.png)) en el carril derecho para abrir el panel de propiedades. En el [!UICONTROL Propiedades] , escriba un nombre para el widget en la [!UICONTROL Título de la utilidad] campo de texto.

![El panel de propiedades con el icono de propiedades y el campo Título de la utilidad resaltados.](./images/user-defined-dashboards/properties-panel.png)

Desde el panel de propiedades del widget, puede editar varios aspectos del widget. Tiene control completo para editar la ubicación del pie de ilustración del widget. Para mover la leyenda, seleccione la opción [!UICONTROL Colocación de la leyenda] y elija la ubicación que desee en la lista de opciones disponibles. También puede cambiar el nombre de la etiqueta asociada con la leyenda y el eje X o Y introduciendo un nuevo nombre en el [!UICONTROL Título de leyenda] campo de texto, o [!UICONTROL Etiqueta de eje] campo de texto respectivamente.

#### Guardar la utilidad {#save-widget}

Guardar en el compositor de utilidades guarda el widget localmente en el tablero. Si desea guardar el trabajo y reanudarlo más tarde, seleccione **[!UICONTROL Guardar]**. Un icono de visto debajo del nombre del widget indica que el widget se ha guardado. Como alternativa, cuando esté satisfecho con el widget, seleccione **[!UICONTROL Guardar y cerrar]** para que el widget esté disponible para todos los demás usuarios con acceso al tablero. Select **[!UICONTROL Cancelar]** para abandonar el trabajo y volver al tablero personalizado.

![Nueva confirmación de guardado del widget.](./images/user-defined-dashboards/save-confirmation.png)

>[!TIP]
>
>Seleccione el icono de propiedades (![El icono de propiedades.](./images/user-defined-dashboards/properties-icon.png)) junto al nombre del tablero para ver los detalles sobre su creación. Puede cambiar el nombre del tablero en el cuadro de diálogo que aparece.

Los widgets se pueden volver a organizar y cambiar de tamaño mientras se encuentran en este espacio de trabajo. Select **[!UICONTROL Guardar]** para conservar el nombre del tablero y el diseño configurado.

![El tablero definido por el usuario con un widget personalizado y el botón de guardar resaltado.](./images/user-defined-dashboards/user-defined-dashboard.png)

Para garantizar que cada consulta de un panel de perspectivas de Adobe Real-time Customer Data Platform tenga recursos suficientes para ejecutarse de forma eficaz, la API rastrea el uso de los recursos asignando espacios de concurrencia a cada consulta. El sistema puede procesar hasta cuatro consultas simultáneas y, por lo tanto, hay cuatro ranuras de consulta simultáneas disponibles en un momento determinado. Las consultas se ponen en cola en función de las ranuras de concurrencia y después esperan en la cola hasta que haya suficientes ranuras de concurrencia disponibles.

## Pasos siguientes y recursos adicionales

Al leer este documento, tiene una mejor comprensión de cómo crear un tablero personalizado y cómo crear, editar y actualizar widgets personalizados para ese tablero.

Para descubrir las métricas y visualizaciones preconfiguradas disponibles para la variable [perfiles](./guides/profiles.md#standard-widgets), [segmentos](./guides/segments.md#standard-widgets)y [destinos](./guides/destinations.md#standard-widgets) tableros, consulte la lista de utilidades estándar en su documentación respectiva.

Para comprender mejor los paneles definidos por el usuario en Experience Platform, vea el siguiente vídeo:

>[!VIDEO](https://video.tv.adobe.com/v/3409637?quality=12&learn=on)
