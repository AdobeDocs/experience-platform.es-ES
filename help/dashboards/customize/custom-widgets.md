---
keywords: Experience Platform;interfaz de usuario;IU;tableros;tablero;perfiles;segmentos;destinos;uso de licencias;widgets;métricas;
title: Creación de widgets personalizados para paneles
description: Esta guía proporciona instrucciones paso a paso para crear widgets personalizados y utilizarlos en paneles de Adobe Experience Platform.
exl-id: 0168ab1e-0b7d-4faf-852e-7208a2b09a04
source-git-commit: 386d805eadf335b95b6eac92c7663fcee17b4b2d
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 0%

---

# Creación de widgets personalizados para paneles

En Adobe Experience Platform, puede ver los datos de su organización e interactuar con ellos mediante varios paneles. También puede actualizar ciertos tableros agregando nuevos widgets a la vista de tablero. Además de los widgets estándar que proporciona Adobe, también puede crear widgets personalizados y compartirlos en toda la organización.

Esta guía proporciona instrucciones paso a paso para crear y agregar widgets personalizados al [!UICONTROL Perfiles], [!UICONTROL Segmentos], y [!UICONTROL Destinos] paneles en la IU de Platform.

Para obtener más información sobre los widgets estándar, consulte la guía de [adición de widgets estándar a los paneles](standard-widgets.md).

>[!NOTE]
>
>Los widgets que se muestran en la [!UICONTROL Uso de licencias] el tablero no se puede personalizar. Para obtener más información sobre este tablero único, lea la [documentación del tablero de uso de licencias](../guides/license-usage.md).

## Biblioteca de widgets {#widget-library}

Esta guía requiere acceso a [!UICONTROL Biblioteca de widgets] en el Experience Platform. Para obtener más información sobre la biblioteca de widgets y cómo acceder a ella dentro de la interfaz de usuario, comience por leer el [introducción a la biblioteca de widgets](widget-library.md).

## Introducción a los widgets personalizados

En la biblioteca de widgets, la variable **[!UICONTROL Personalizado]** Esta pestaña permite crear widgets y compartirlos con otros usuarios de su organización para personalizar el aspecto de los paneles.

>[!IMPORTANT]
>
>Su organización puede crear un máximo de 20 widgets personalizados en la biblioteca de widgets.

Seleccione el **[!UICONTROL Personalizado]** para empezar a crear widgets personalizados o para ver widgets personalizados que su organización ya ha creado.

![Espacio de trabajo de la biblioteca de widgets con la pestaña Personalizado resaltada.](../images/customization/custom-widgets.png)

## Crear un widget personalizado

Para crear un widget personalizado, seleccione **[!UICONTROL Crear widget]** en la esquina superior derecha de la biblioteca de widgets o, si se trata del primer widget personalizado de su organización, seleccione **[!UICONTROL Crear]** desde el centro de la biblioteca de widgets.

![La pestaña Personalizado del espacio de trabajo de la biblioteca de widgets con Crear resaltado.](../images/customization/create-widget.png)

En el **[!UICONTROL Crear widget]** , proporcione un título y una descripción para el widget nuevo y elija el atributo que desea que muestre el widget.

>[!NOTE]
>
>La lista de atributos disponibles depende del esquema que se haya configurado para su organización. Para obtener más información sobre la selección de atributos y la configuración de esquema, lea la guía de [edición del esquema para crear widgets personalizados](edit-schema.md).

Para elegir un atributo, seleccione el botón de opción situado junto al atributo que desee añadir.

>[!NOTE]
>
>Solo se puede seleccionar un atributo por widget y solo se puede crear un widget por atributo. Si ya se ha creado un widget para un atributo, el atributo aparece atenuado.

![Cuadro de diálogo Crear widget.](../images/customization/create-widget-dialog.png)

## Seleccionar una visualización

Después de seleccionar un atributo, aparece una previsualización del nuevo widget en el cuadro de diálogo. La inteligencia artificial se utiliza para seleccionar automáticamente una visualización que se ajuste mejor a los datos de atributos y para proporcionar opciones de visualización adicionales que puede seleccionar manualmente.

Según el atributo, la IA recomienda distintas opciones de visualización. La lista completa de visualizaciones incluye:

* Gráfico de barras horizontales: se utilizan líneas horizontales para representar valores.
* Gráfico de barras verticales: las líneas verticales se utilizan para representar valores.
* Gráfico de anillo: similar a un gráfico circular, los valores se muestran como partes o fragmentos de un todo.
* Diagrama de puntos: Utiliza un eje horizontal y vertical para indicar valores.
* Gráfico de líneas: los valores se muestran con una sola línea para mostrar los cambios durante un periodo de tiempo.
* Tarjeta de número: muestra un número de resumen para representar un solo valor de clave.
* Tabla de datos: los valores se muestran como filas en una tabla.

>[!NOTE]
>
>La única métrica que se admite actualmente para todos los atributos es el recuento de perfiles.
>
>Los datos que se muestran en el widget de ejemplo solo tienen fines ilustrativos. La vista previa no muestra datos reales de su organización.

Para guardar el widget nuevo y volver al [!UICONTROL Personalizado] pestaña, seleccione **[!UICONTROL Crear]**.

![El cuadro de diálogo Crear widget con las opciones de visualización y Crear resaltadas.](../images/customization/create-widget-select-attribute.png)

El nuevo widget ya está disponible para añadirse a un panel seleccionando el widget de la biblioteca y haciendo clic en **[!UICONTROL Añadir widget]**.

![La pestaña Personalizado del espacio de trabajo de la biblioteca de widgets con el nuevo widget y Agregar widget resaltados.](../images/customization/custom-widgets-new.png)

## Ocultar un widget personalizado

Una vez agregado un widget a la biblioteca, se puede ocultar seleccionando los puntos suspensivos (`...`) en la tarjeta del widget y, a continuación, seleccione **[!UICONTROL Ocultar widget]**. También puede previsualizar y editar el widget desde el mismo menú desplegable.

Para ver los widgets ocultos, seleccione **[!UICONTROL Mostrar widgets ocultos]** desde la esquina superior derecha de la biblioteca de widgets.

>[!WARNING]
>
>Al ocultar un widget en la biblioteca, no se elimina de los paneles de los usuarios individuales. Si un widget ya no debe utilizarse en su organización, asegúrese de comunicarlo directamente a todos los usuarios de Platform, ya que deberán eliminar el widget de sus paneles.

![La pestaña Personalizado del espacio de trabajo de la biblioteca de widgets con las opciones de menú desplegable de widgets y Mostrar widgets ocultos resaltados.](../images/customization/hide-widget.png)

## Editar un widget personalizado

Puede editar los widgets personalizados en la biblioteca de widgets seleccionando los puntos suspensivos (`...`) en la tarjeta del widget y, a continuación, seleccione **[!UICONTROL Editar]** en el menú desplegable.

![Las opciones del menú desplegable del widget con los puntos suspensivos y la opción Editar resaltados.](../images/customization/custom-widget-edit.png)

En el **[!UICONTROL Editar widget]** , puede editar el título y la descripción del widget, así como previsualizar y seleccionar diferentes visualizaciones. Una vez realizadas las ediciones, seleccione **[!UICONTROL Guardar]** para guardar los cambios y volver a la pestaña widgets personalizados.

>[!WARNING]
>
>La edición de un widget en la biblioteca no actualiza el widget para usuarios individuales. Si se ha actualizado un widget, asegúrese de comunicarlo directamente a todos los usuarios de Platform, ya que deberán eliminar el widget obsoleto de sus paneles y, a continuación, seleccione y añada el widget actualizado de la biblioteca de widgets.

![Cuadro de diálogo Editar widget.](../images/customization/edit-widget.png)

## Pasos siguientes

Después de leer este documento, puede acceder a la biblioteca de widgets y utilizarla para crear y agregar widgets personalizados para su organización. Para modificar el tamaño y la ubicación de los widgets que aparecen en el panel, consulte la [guía de modificación de paneles](modify.md).
