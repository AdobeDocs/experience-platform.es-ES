---
title: Paneles definidos por el usuario
description: Obtenga información sobre cómo crear y administrar paneles personalizados, donde puede crear, añadir y editar widgets personalizados para visualizar métricas clave.
exl-id: a9ab83f7-b68d-4dbf-9dc6-ef253df5c82c
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '956'
ht-degree: 0%

---

# Paneles definidos por el usuario

Los paneles de Adobe Experience Platform le ayudan a acelerar las perspectivas y personalizar la visualización a través de la función de paneles definida por el usuario. Esta función le permite crear y administrar paneles personalizados, donde puede crear, añadir y editar widgets personalizados para visualizar métricas clave relevantes para su organización.

<!-- Getting started / permissions section commented out for Beta. This will be necessary after GA only

## Getting started

To view dashboards in Adobe Experience Platform you must have the appropriate permissions enabled. Please read the [dashboards permissions documentation](./permissions.md#available-permissions) to learn how to grant users the ability to view, edit, and update Experience Platform dashboards using Adobe Admin Console. If you do not have administrator privileges for your organization, contact your product administrator to obtain the required permissions. -->

## Creación de paneles personalizados

Para crear un tablero personalizado, primero, navegue hasta el inventario del tablero. Seleccionar **[!UICONTROL Paneles]** en la navegación izquierda de la interfaz de usuario de Platform seguida de **[!UICONTROL Crear tablero]**.

![El inventario de tableros con Tableros en la navegación izquierda y &quot;Crear tablero&quot; resaltado.](./images/user-defined-dashboards/create-dashboard.png)

Antes de agregar un tablero personalizado, el inventario de los tableros está vacío y muestra el mensaje &quot;No se encontraron tableros&quot;. Mensaje. Una vez creados, todos los tableros definidos por el usuario se enumeran en el inventario de tableros.

El [!UICONTROL Crear tablero] aparece el cuadro de diálogo. Introduzca un nombre descriptivo y sencillo para la colección de widgets que desea crear y seleccione **[!UICONTROL Guardar]**.

![Cuadro de diálogo Crear tablero.](./images/user-defined-dashboards/create-dashboard-dialog.png)

El tablero en blanco recién creado aparecerá con el nombre elegido en la esquina superior izquierda de la vista.

## Crear un widget {#create-widget}

>[!CONTEXTUALHELP]
>id="platform_dashboards_udd_maxwidgets"
>title="Número máximo de widgets"
>abstract="Los paneles definidos por el usuario admiten hasta diez widgets. Después de agregar diez widgets al panel, la variable [!UICONTROL Añadir nuevo widget] La opción está desactivada y aparece en gris."

En la nueva vista de panel, seleccione **[!UICONTROL Añadir nuevo widget]** para iniciar el proceso de creación del widget.

>[!IMPORTANT]
>
>Los paneles definidos por el usuario admiten hasta diez widgets. Después de agregar diez widgets al panel, la variable [!UICONTROL Añadir nuevo widget] La opción está desactivada y aparece en gris.

![El nuevo tablero vacío con Agregar nuevo widget resaltado.](./images/user-defined-dashboards/add-new-widget.png)

### Compositor de widgets

Aparecerá el espacio de trabajo del compositor de widgets. A continuación, seleccione **[!UICONTROL Seleccionar datos]** para elegir el modelo de datos desde el que desea agregar atributos a los widgets.

![El espacio de trabajo del compositor de widgets.](./images/user-defined-dashboards/widget-composer.png)

El [!UICONTROL Seleccionar datos] aparece el cuadro de diálogo. Seleccione un modelo de datos de la columna izquierda para mostrar una lista de vista previa de todas las tablas disponibles.

>[!NOTE]
>
>Actualmente, los paneles definidos por el usuario solo admiten el modelo de datos de perfil. Se admitirán más opciones.

![Cuadro de diálogo Seleccionar datos.](./images/user-defined-dashboards/select-data-dialog.png)

La lista de vista previa proporciona detalles sobre las tablas contenidas en el modelo de datos. La siguiente tabla proporciona descripciones de los campos de columna y sus valores potenciales.

| Campo de columna | Descripción |
|---|---|
| [!UICONTROL Título] | Nombre de la tabla. |
| [!UICONTROL Tipo de tabla] | El tipo de tabla. Los tipos potenciales incluyen: `fact`, `dimension`, y `none`. |
| [!UICONTROL Búsquedas] | Número de tablas unidas a la tabla elegida. |

Seleccionar **[!UICONTROL Siguiente]** para confirmar la elección del modelo de datos. La vista siguiente muestra una lista de las tablas disponibles en el carril izquierdo. Seleccione una tabla para ver un desglose completo de los datos contenidos en la tabla seleccionada.

El [!UICONTROL Previsualizar] el panel contiene pestañas para [!UICONTROL Registros de muestra] y [!UICONTROL Atributos]. El [!UICONTROL Registros de muestra] proporciona un subconjunto de los registros de la tabla seleccionada en una vista tabulada. El [!UICONTROL Atributos] proporciona el nombre del atributo, el tipo de datos y la tabla de origen de cada atributo asociado a la tabla seleccionada.

Seleccione una tabla de la lista disponible en el carril izquierdo para proporcionar datos para el widget y seleccione **[!UICONTROL Seleccionar]** para volver al compositor de widgets.

![El cuadro de diálogo Seleccionar datos con la selección resaltada.](./images/user-defined-dashboards/select-a-table.png)

El compositor de widgets ahora se rellena con datos de la tabla elegida.

El modelo de datos y la tabla seleccionada actualmente se muestran en la parte superior del carril izquierdo, y los atributos disponibles para crear el widget se enumeran en la columna de atributos.

![Un widget rellenado con datos dentro del compositor de widgets.](./images/user-defined-dashboards/populated-widget-composer.png)

>[!TIP]
>
>Puede cambiar el modelo de datos elegido seleccionando el icono de lápiz (![Icono de lápiz.](./images/user-defined-dashboards/edit-icon.png)) en el carril izquierdo.

Seleccione el icono de añadir (./images/user-defined-dashboards/add-icon.png) junto a un nombre de atributo para agregar un atributo al eje X o Y.

![El compositor de widgets con la lista desplegable de añadir icono resaltada para añadir atributos a un eje de widgets.](./images/user-defined-dashboards/attributes-dropdown.png)

A continuación, seleccione el tipo de gráfico en la [!UICONTROL Marcas] para generar una visualización previa de la configuración actual del widget. En el [!UICONTROL Propiedades] carril de la derecha de la pantalla, introduzca un nombre para el widget en la [!UICONTROL Título del widget] campo de texto.

![El compositor de widgets con el campo desplegable Marcas y el texto de título del widget resaltado.](./images/user-defined-dashboards/marks-dropdown-widget-title.png)

Cuando esté satisfecho con el widget, seleccione **[!UICONTROL Guardar]**. Un icono de verificación debajo del nombre del widget indica que el widget se ha guardado.

>[!NOTE]
>
>Al guardar en el compositor de widgets, se guarda el widget localmente en el tablero. Si sale del editor de tableros sin guardar el tablero, el widget no se guardará en el tablero.

![Nueva confirmación de guardado del widget.](./images/user-defined-dashboards/save-confirmation.png)

Seleccionar **[!UICONTROL Cancelar]** para volver al tablero personalizado.

![Compositor de widgets con un widget de ejemplo creado.](./images/user-defined-dashboards/composed-widget.png)

>[!TIP]
>
>Seleccione el icono de configuración junto al nombre del panel para ver los detalles sobre su creación. Puede cambiar el nombre del panel en el cuadro de diálogo que aparece.

Los widgets se pueden reorganizar y cambiar de tamaño en este espacio de trabajo. Seleccionar **[!UICONTROL Guardar]** para conservar el nombre del tablero y el diseño configurado.

![El tablero definido por el usuario con un widget personalizado y el botón de guardar resaltados.](./images/user-defined-dashboards/user-defined-dashboard.png)

Para garantizar que cada consulta de un panel de perspectivas de Adobe Real-time Customer Data Platform tenga suficientes recursos para ejecutarse de forma eficaz, la API rastrea el uso de recursos asignando espacios de concurrencia a cada consulta. El sistema puede procesar hasta cuatro consultas simultáneas y, por lo tanto, hay cuatro ranuras de consulta simultáneas disponibles en cualquier momento. Las consultas se colocan en una cola basada en ranuras de concurrencia y, a continuación, espere en la cola hasta que haya suficientes ranuras de concurrencia disponibles.

## Pasos siguientes y recursos adicionales

Al leer este documento, tiene una mejor comprensión de cómo crear un panel personalizado y cómo crear, editar y actualizar widgets personalizados para ese panel.

Para descubrir las métricas y visualizaciones preconfiguradas disponibles para [perfiles](./guides/profiles.md#standard-widgets), [segmentos](./guides/segments.md#standard-widgets), y [destinos](./guides/destinations.md#standard-widgets) En los paneles, consulte la lista de widgets estándar en su documentación respectiva.

Para comprender mejor los paneles definidos por el usuario en Experience Platform, vea el siguiente vídeo:

>[!VIDEO](https://video.tv.adobe.com/v/3409637?quality=12&learn=on)
