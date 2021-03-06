---
keywords: Experience Platform;interfaz de usuario;IU;paneles;tablero;perfiles;segmentos;destinos;uso de licencias;utilidades;métricas;
title: Creación de utilidades personalizadas para tableros
description: 'Esta guía proporciona instrucciones paso a paso para crear utilidades personalizadas para utilizarlas en tableros de Adobe Experience Platform. '
source-git-commit: 3235c48ec1f449e45b3f4b096585b67e14600407
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 0%

---


# Creación de widgets personalizados para tableros

En Adobe Experience Platform, puede ver e interactuar con los datos de su organización mediante varios tableros. También puede actualizar ciertos tableros agregando nuevas utilidades a la vista del tablero. Además de los widgets estándar proporcionados por Adobe, también puede crear widgets personalizados y compartirlos en toda la organización.

Esta guía proporciona instrucciones paso a paso para crear y agregar utilidades personalizadas a los tableros [!UICONTROL Profiles], [!UICONTROL Segments] y [!UICONTROL Destinations] en la interfaz de usuario de Platform.

Para obtener más información sobre las utilidades estándar, consulte la guía para [agregar utilidades estándar a los tableros](standard-widgets.md).

>[!NOTE]
>
>Los widgets que se muestran en el panel [!UICONTROL Licencia de uso] no se pueden personalizar. Para obtener más información sobre este tablero único, lea la [documentación del tablero de uso de licencias](../guides/license-usage.md).

## Biblioteca de utilidades {#widget-library}

Esta guía requiere acceso a la [!UICONTROL biblioteca de utilidades] dentro de Experience Platform. Para obtener más información sobre la biblioteca de widgets y cómo acceder a ella dentro de la interfaz de usuario, lea por favor la [descripción general de la biblioteca de utilidades](widget-library.md).

## Introducción a los widgets personalizados

Dentro de la biblioteca de utilidades, la pestaña **[!UICONTROL Personalizado]** le permite crear utilidades y compartirlas con otros usuarios de su organización para personalizar el aspecto de sus tableros.

>[!IMPORTANT]
>
>Su organización puede crear un máximo de 20 widgets personalizados en la biblioteca de widgets.

Seleccione la pestaña **[!UICONTROL Personalizado]** para comenzar a crear widgets personalizados o para ver los widgets personalizados que su organización ya ha creado.

![](../images/customization/custom-widgets.png)

## Creación de un widget personalizado

Para crear un widget personalizado, seleccione **[!UICONTROL Crear widget]** en la esquina superior derecha de la biblioteca de widgets o, si este es el primer widget personalizado de la organización, seleccione **[!UICONTROL Crear]** en el centro de la biblioteca de widgets.

![](../images/customization/create-widget.png)

En el cuadro de diálogo **[!UICONTROL Crear utilidad]**, proporcione un título y una descripción para el nuevo widget y elija el atributo que desea que se muestre el widget.

>[!NOTE]
>
>La lista de atributos disponibles depende del esquema que se haya configurado para la organización. Para obtener más información sobre la selección de atributos y la configuración de esquema, lea la guía sobre la [edición del esquema para crear widgets personalizados](edit-schema.md).

Para elegir un atributo, seleccione el botón de opción situado junto al atributo que desea añadir.

>[!NOTE]
>
>Solo se puede seleccionar un atributo por widget y solo se puede crear un widget por atributo. Si ya se ha creado un widget para un atributo, este aparece atenuado.

![](../images/customization/create-widget-dialog.png)

## Seleccionar una visualización

Después de seleccionar un atributo, aparece una vista previa del nuevo widget en el cuadro de diálogo. La inteligencia artificial se utiliza para seleccionar automáticamente una visualización que se ajuste mejor a los datos de atributo y para proporcionar opciones de visualización adicionales que puede seleccionar manualmente.

En función del atributo , la API recomienda diferentes opciones de visualización. La lista completa de visualizaciones incluye:

* Gráfico de barras horizontales: Las líneas horizontales se utilizan para representar valores.
* Gráfico de barras verticales: Las líneas verticales se utilizan para representar valores.
* Gráfico circular: Al igual que un gráfico circular, los valores se muestran como partes o partes de un todo.
* Diagrama de dispersión: Utiliza un eje horizontal y vertical para indicar valores.
* Gráfico de líneas: Los valores se muestran utilizando una sola línea para mostrar los cambios a lo largo de un período de tiempo.
* Tarjeta de número: Muestra un número de resumen para representar un valor de clave única.
* Tabla de datos: Los valores se muestran como filas en una tabla.

>[!NOTE]
>
>La única métrica admitida actualmente para todos los atributos es el recuento de perfiles.
>
>Los datos que se muestran en el widget de ejemplo solo tienen fines ilustrativos. La vista previa no muestra datos reales de su organización.

Para guardar la nueva utilidad y volver a la pestaña [!UICONTROL Personalizado], seleccione **[!UICONTROL Crear]**.

![](../images/customization/create-widget-select-attribute.png)

La nueva utilidad ya está disponible para agregarse a un tablero. Para ello, elija la utilidad de la biblioteca y seleccione **[!UICONTROL Agregar utilidad]**.

![](../images/customization/custom-widgets-new.png)

## Ocultar un widget personalizado

Después de agregar un widget a la biblioteca, se puede ocultar seleccionando los puntos suspensivos (`...`) en la tarjeta del widget y luego seleccionando **[!UICONTROL Ocultar widget]**. También puede obtener una vista previa y editar el widget desde la misma lista desplegable.

Para ver los widgets que se han ocultado, seleccione **[!UICONTROL Mostrar widgets ocultos]** en la esquina superior derecha de la biblioteca de widgets.

>[!WARNING]
>
>Ocultar un widget en la biblioteca no elimina el widget de los tableros de usuarios individuales. Si una utilidad ya no debe utilizarse en su organización, asegúrese de comunicarla directamente a todos los usuarios de Platform, ya que deberán eliminarla de sus tableros.

![](../images/customization/hide-widget.png)

## Editar un widget personalizado

Puede editar widgets personalizados en la biblioteca de utilidades seleccionando los elipses (`...`) en la tarjeta de la utilidad y luego seleccionando **[!UICONTROL Editar]** en el menú desplegable.

![](../images/customization/custom-widget-edit.png)

En el cuadro de diálogo **[!UICONTROL Editar utilidad]**, puede editar el título y la descripción del widget, así como previsualizar y seleccionar distintas visualizaciones. Después de realizar las ediciones, seleccione **[!UICONTROL Guardar]** para guardar los cambios y volver a la pestaña de widgets personalizados.

>[!WARNING]
>
>La edición de un widget en la biblioteca no actualiza el widget para usuarios individuales. Si se ha actualizado un widget, asegúrese de comunicarlo directamente a todos los usuarios de Platform, ya que deberán eliminar el widget obsoleto de sus tableros y, a continuación, seleccionar y agregar el widget actualizado desde la biblioteca de widgets.

![](../images/customization/edit-widget.png)

## Pasos siguientes

Después de leer este documento, puede acceder a la biblioteca de widgets y utilizarla para crear y agregar utilidades personalizadas para su organización. Para modificar el tamaño y la ubicación de las utilidades que aparecen en el tablero, consulte la [guía para modificar los tableros](modify.md).
