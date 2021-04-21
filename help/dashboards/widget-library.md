---
keywords: Experience Platform;interfaz de usuario;IU;paneles;tablero;perfiles;segmentos;destinos;uso de licencias
title: Uso de la biblioteca de utilidades para agregar y crear widgets de tablero
description: 'Esta guía proporciona instrucciones paso a paso para agregar utilidades estándar y crear utilidades personalizadas para visualizar datos de tablero en Adobe Experience Platform. '
topic-legacy: guide
exl-id: 1d33e3ea-a8a8-4a09-8bd9-2e04ecedebdc
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '974'
ht-degree: 1%

---

# (Beta) Biblioteca de utilidades {#widget-library}

>[!IMPORTANT]
>
>La funcionalidad del panel está actualmente en fase beta y no está disponible para todos los usuarios. La documentación y las funciones están sujetas a cambios.

En la interfaz de usuario de Adobe Experience Platform, puede ver e interactuar con los datos de su organización mediante varios tableros. También puede actualizar algunos de estos tableros agregando nuevas utilidades a la vista del tablero. Además de los widgets estándar proporcionados por Adobe, puede crear widgets personalizados y compartirlos en toda la organización.

Esta guía proporciona instrucciones paso a paso para agregar utilidades estándar y crear utilidades personalizadas para personalizar la información que se muestra en los tableros [!UICONTROL Profiles] y [!UICONTROL Segments] en la interfaz de usuario de Platform.

Para obtener información sobre cómo modificar la ubicación y el tamaño de las utilidades en los tableros [!UICONTROL Profiles], [!UICONTROL Destinations] y [!UICONTROL Segments], consulte la [guía para modificar los tableros](modify.md).

>[!NOTE]
>
>Los widgets mostrados en el tablero [!UICONTROL License usage] no se pueden personalizar. Para obtener más información sobre este tablero único, lea la [documentación del tablero de uso de licencias](guides/license-usage.md).

## Acceso a la biblioteca de widgets

Desde cualquier tablero (por ejemplo, el tablero Perfiles), puede seleccionar **[!UICONTROL Modify dashboard]** seguido de **[!UICONTROL Widget library]** para acceder a la biblioteca de widgets.

>[!NOTE]
>
>El botón [!UICONTROL Widget library] solo aparece una vez que se ha seleccionado [!UICONTROL Modify dashboard].

![](images/customization/modify-dashboard.png)

![](images/customization/widget-library-button.png)

El [!UICONTROL Widget library] contiene dos pestañas, [!UICONTROL Standard] y [!UICONTROL Custom].

* La pestaña **[!UICONTROL Standard]** contiene las utilidades creadas por Adobe y le permite actualizar el tablero con estas métricas estándar. Para obtener más información sobre la adición de utilidades estándar al tablero, consulte la sección [utilidades estándar](#standard-widgets) en esta guía.
* La pestaña **[!UICONTROL Custom]** le permite crear y compartir widgets dentro de su organización. Para ver los pasos completos para crear sus propias utilidades, consulte la sección [utilidades personalizadas](#custom-widgets) de esta guía.

![](images/customization/widget-library.png)

## Widgets estándar {#standard-widgets}

La pestaña **[!UICONTROL Standard]** contiene las utilidades creadas por Adobe, desglosadas en categorías. Al seleccionar una categoría, se muestran las utilidades disponibles para ese tablero. Cada widget aparece como una tarjeta, con el título, la descripción y una visualización de muestra de la métrica.

>[!NOTE]
>
>Los widgets solo se pueden agregar al tablero que coincida con la categoría seleccionada. Por ejemplo, solo se pueden agregar widgets de la categoría [!UICONTROL Profiles] al tablero [!UICONTROL Profiles].

![](images/customization/standard-widgets.png)

Para elegir un widget estándar para agregarlo al tablero, resalte el widget y seleccione la casilla de verificación del widget. Con al menos un widget seleccionado, se ilumina el botón **[!UICONTROL Add widget]**.

>[!NOTE]
>
>El contador de la esquina superior derecha de la biblioteca de widgets muestra el número total de widgets seleccionados.

Seleccione **[!UICONTROL Add widget]** para agregar las utilidades seleccionadas al tablero.

![](images/customization/add-widget.png)

## Widgets personalizados {#custom-widgets}

>[!IMPORTANT]
>
>Su organización puede crear un máximo de 20 widgets personalizados en la biblioteca de widgets.

Para personalizar aún más el aspecto de los tableros dentro de Experience Platform, puede crear utilidades y compartirlas con otros usuarios de su organización. En la biblioteca de utilidades, seleccione la pestaña **[!UICONTROL Custom]** para comenzar a crear utilidades personalizadas. En la pestaña [!UICONTROL Custom], se ven todas las utilidades creadas por su organización. En este ejemplo, aún no se han creado widgets personalizados.

![](images/customization/custom-widgets.png)

### Seleccionar atributos

Para crear utilidades personalizadas, se deben identificar los atributos del perfil del cliente en tiempo real para garantizar que los datos se incluyan como parte de la instantánea diaria. Si su organización no ha seleccionado ningún atributo de perfil, aparece el botón [!UICONTROL Configure schema] en la esquina superior derecha de la biblioteca de widgets.

Cuando se ha seleccionado al menos un atributo personalizado, aparece el botón [!UICONTROL Edit schema] en la esquina superior derecha de la biblioteca de widgets. Seleccione **[!UICONTROL Edit schema]** para abrir el cuadro de diálogo **[!UICONTROL Select union schema field]** para ver los atributos seleccionados y agregar más atributos.

>[!IMPORTANT]
>
>Una organización puede seleccionar un máximo de 20 atributos.

![](images/customization/edit-schema.png)

Para seleccionar un atributo, vaya al atributo en el esquema de unión (o utilice la búsqueda) y seleccione la casilla situada junto al atributo. Al seleccionar la casilla de verificación, también se agrega el atributo a la lista **[!UICONTROL Selected Attributes]** en el lado derecho del cuadro de diálogo.

>[!NOTE]
>
>Para que un atributo esté visible para su selección, debe ser uno de los siguientes: Cadena, Fecha, Fecha-Hora, Booleano, Corto, Largo, Entero o Byte. Los tipos de datos Mapa y Doble no son compatibles y aparecen atenuados para que no se puedan seleccionar.

Después de elegir los atributos que desea añadir, seleccione **[!UICONTROL Save]** para guardar los atributos y volver a la pestaña widgets personalizados.

Los atributos recién seleccionados están disponibles después de la instantánea diaria cuando se actualizan los datos.

![](images/customization/select-attribute.png)

### Creación de un widget personalizado

Para crear un widget personalizado, seleccione **[!UICONTROL Create]** en el centro de la biblioteca de widgets o, si ya se han creado widgets personalizados, seleccione **[!UICONTROL Create widget]** en la esquina superior derecha de la biblioteca de widgets.

![](images/customization/create-widget.png)

En el cuadro de diálogo **[!UICONTROL Create widget]**, puede proporcionar un título y una descripción para el nuevo widget y elegir el atributo que desea que se muestre el widget. Para elegir un atributo, seleccione el botón de opción situado junto al atributo que desea añadir.

>[!NOTE]
>
>Solo se puede seleccionar un atributo por widget. Además, si ya se ha creado un widget para un atributo, este aparece atenuado.

![](images/customization/create-widget-dialog.png)

En el cuadro de diálogo aparece una vista previa del nuevo widget, que muestra un gráfico de barras horizontales con datos ficticios.

>[!NOTE]
>
>La única métrica que actualmente se admite para todos los atributos es el recuento de perfiles y la única visualización que actualmente se admite para los widgets personalizados es un gráfico de barras horizontal.
>
>Los datos que se muestran en el widget de ejemplo solo tienen fines ilustrativos. La vista previa no muestra datos reales de su organización.

![](images/customization/create-widget-select-attribute.png)

Para guardar la nueva utilidad y volver a la pestaña [!UICONTROL Custom], seleccione **[!UICONTROL Create]**. La nueva utilidad ya está disponible para agregarse a un tablero. Para ello, elija la utilidad de la biblioteca y seleccione **[!UICONTROL Add widget]**.

### Archivar un widget personalizado

Una vez agregado un widget a la biblioteca, se puede archivar con el botón **[!UICONTROL Archive]**. También puede editar el widget para actualizar los campos de título o descripción.

## Pasos siguientes

Después de leer este documento, ahora puede acceder a [!UICONTROL Widget library] y utilizarlo para agregar widgets a un tablero o crear utilidades personalizadas para su organización. Para modificar el tamaño y la ubicación de las utilidades en el tablero, consulte la [guía para modificar los tableros](modify.md).
