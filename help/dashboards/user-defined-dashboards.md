---
title: Tableros definidos por el usuario
description: Aprenda a crear y administrar tableros personalizados donde puede crear, agregar y editar widgets personalizados para visualizar métricas clave.
exl-id: a9ab83f7-b68d-4dbf-9dc6-ef253df5c82c
source-git-commit: f138bb0f1b8d289cc872afc065d31c5e55d4b05c
workflow-type: tm+mt
source-wordcount: '883'
ht-degree: 0%

---

# Tableros definidos por el usuario (Beta)

>[!IMPORTANT]
>
>La función de tableros definida por el usuario está en versión beta. Sus características y documentación están sujetas a cambios.

Los paneles de Adobe Experience Platform le ayudan a acelerar la información y a personalizar la visualización mediante la función de paneles definida por el usuario. Esta función le permite crear y administrar tableros personalizados en los que puede crear, agregar y editar widgets personalizados para visualizar métricas clave relevantes para su organización.

## Primeros pasos

Para ver los tableros en Adobe Experience Platform debe tener habilitados los permisos adecuados. Lea el [documentación de permisos de tableros](./permissions.md#available-permissions) para aprender a otorgar a los usuarios la capacidad de ver, editar y actualizar tableros de Experience Platform mediante Adobe Admin Console. Si su organización no tiene privilegios de administrador, póngase en contacto con el administrador del producto para obtener los permisos necesarios.

## Crear tableros personalizados

Para crear un tablero personalizado, primero, vaya al inventario del tablero. Select **[!UICONTROL Tableros]** desde la navegación izquierda de la interfaz de usuario de Platform seguida de **[!UICONTROL Crear tablero]**.

Para obtener más información sobre los paneles preconfigurados disponibles, consulte la [información general del inventario del panel](./inventory.md).

>[!NOTE]
>
>Al agregar un tablero personalizado, la lista de tableros preconfigurados se elimina del inventario de tableros. En su lugar, el inventario de tableros consta únicamente de tableros definidos por el usuario.

![El inventario del tablero con &quot;Crear tablero&quot; resaltado.](./images/user-defined-dashboards/create-dashboard.png)

La variable [!UICONTROL Crear tablero] se abre. Escriba un nombre descriptivo y reconocible para la colección de widgets que desee crear y seleccione **[!UICONTROL Guardar]**.

![El cuadro de diálogo Crear tablero .](./images/user-defined-dashboards/create-dashboard-dialog.png)

El panel en blanco recién creado aparece con el nombre elegido en la esquina superior izquierda de la vista.

## Creación de una utilidad

En la nueva vista de tablero, seleccione **[!UICONTROL Agregar nueva utilidad]** para iniciar el proceso de creación de la utilidad.

![El nuevo tablero vacío con Añadir nuevo widget resaltado.](./images/user-defined-dashboards/add-new-widget.png)

### Compositor de utilidades

Aparecerá el espacio de trabajo del compositor de utilidades. A continuación, seleccione **[!UICONTROL Seleccionar datos]** para elegir el modelo de datos desde el que añadir atributos a las utilidades.

![El espacio de trabajo del compositor de utilidades.](./images/user-defined-dashboards/widget-composer.png)

La variable [!UICONTROL Seleccionar datos] se abre. Seleccione un modelo de datos de la columna izquierda para mostrar una lista de vista previa de todas las tablas disponibles.

>[!NOTE]
>
>Actualmente, los tableros definidos por el usuario solo admiten el modelo de datos de perfil. Se admitirán más opciones.

![El cuadro de diálogo Seleccionar datos .](./images/user-defined-dashboards/select-data-dialog.png)

La lista de vista previa proporciona detalles sobre las tablas contenidas en el modelo de datos. La tabla siguiente proporciona descripciones de los campos de columna y sus valores potenciales.

| Campo de columna | Descripción |
|---|---|
| [!UICONTROL Título] | Nombre de la tabla. |
| [!UICONTROL Tipo de tabla] | Tipo de tabla. Los tipos posibles incluyen: `fact`, `dimension`y `none`. |
| [!UICONTROL Búsquedas] | Número de tablas unidas a la tabla elegida. |

Select **[!UICONTROL Siguiente]** para confirmar la elección del modelo de datos. La siguiente vista muestra una lista de las tablas disponibles en el carril izquierdo. Seleccione una tabla para ver un desglose completo de los datos contenidos en la tabla seleccionada.

La variable [!UICONTROL Vista previa] El panel contiene fichas para [!UICONTROL Registros de muestra] y [!UICONTROL Atributos]. La variable [!UICONTROL Registros de muestra] proporciona un subconjunto de los registros de la tabla seleccionada en una vista tabulada. La variable [!UICONTROL Atributos] proporciona el nombre del atributo, el tipo de datos y la tabla de origen para cada atributo asociado a la tabla seleccionada.

Seleccione una tabla de la lista disponible en el carril izquierdo para proporcionar datos para el widget y seleccione **[!UICONTROL Select]** para volver al compositor de utilidades.

![El cuadro de diálogo seleccionar datos con la selección resaltada.](./images/user-defined-dashboards/select-a-table.png)

El compositor de utilidades ahora se rellena con datos de la tabla elegida.

El modelo de datos y la tabla seleccionada actualmente se muestran en la parte superior del carril izquierdo y los atributos disponibles para crear el widget se enumeran en la columna de atributos.

![Un widget rellenado con datos dentro del compositor de utilidades.](./images/user-defined-dashboards/populated-widget-composer.png)

>[!TIP]
>
>Puede cambiar el modelo de datos seleccionado seleccionando el icono de lápiz (![Icono de lápiz.](./images/user-defined-dashboards/edit-icon.png)) en el carril izquierdo.

Seleccione los puntos suspensivos (`...`) junto al nombre de un atributo para agregar un atributo al eje X o al eje Y.

![El compositor de utilidades con la lista desplegable de elipses resaltada para agregar atributos a un eje de utilidades.](./images/user-defined-dashboards/attributes-dropdown.png)

A continuación, seleccione el tipo de gráfico o de gráfico en el [!UICONTROL Marcas] para generar una visualización de vista previa de la configuración actual del widget. En el [!UICONTROL Propiedades] en el lado derecho de la pantalla, escriba un nombre para el widget en la [!UICONTROL Título de la utilidad] campo de texto.

![El compositor de utilidades con la lista desplegable Marcas y el campo de texto Título de la utilidad resaltado.](./images/user-defined-dashboards/marks-dropdown-widget-title.png)

Cuando esté satisfecho con el widget, seleccione **[!UICONTROL Guardar]**. Un icono de visto debajo del nombre del widget indica que el widget se ha guardado.

>[!NOTE]
>
>Guardar en el compositor de utilidades guarda el widget localmente en el tablero. Si sale del editor de tableros sin guardar el tablero, el widget no se guardará en el tablero.

![Nueva confirmación de guardado del widget.](./images/user-defined-dashboards/save-confirmation.png)

Select **[!UICONTROL Cancelar]** para volver al tablero personalizado.

![El compositor de utilidades con un widget de ejemplo creado.](./images/user-defined-dashboards/composed-widget.png)

>[!TIP]
>
>Seleccione el icono de configuración situado junto al nombre del tablero para ver los detalles sobre su creación. Puede cambiar el nombre del tablero en el cuadro de diálogo que aparece.

Los widgets se pueden volver a organizar y cambiar de tamaño mientras se encuentran en este espacio de trabajo. Select **[!UICONTROL Guardar]** para conservar el nombre del tablero y el diseño configurado.

![El tablero definido por el usuario con un widget personalizado y el botón de guardar resaltado.](./images/user-defined-dashboards/user-defined-dashboard.png)

## Pasos siguientes

Al leer este documento, tendrá una mejor comprensión de cómo crear un tablero personalizado y cómo crear, editar y actualizar widgets personalizados para ese tablero.

Para descubrir las métricas y visualizaciones preconfiguradas disponibles para la variable [perfiles](./guides/profiles.md#standard-widgets), [segmentos](./guides/segments.md#standard-widgets)y [destinos](./guides/destinations.md#standard-widgets) tableros, consulte la lista de utilidades estándar en su documentación respectiva.
