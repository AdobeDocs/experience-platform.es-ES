---
keywords: Experience Platform;interfaz de usuario;IU;paneles;tablero;perfiles;segmentos;destinos;uso de licencias;utilidades;métricas;
title: Creación de utilidades personalizadas para tableros
description: 'Esta guía proporciona instrucciones paso a paso para crear utilidades personalizadas para utilizarlas en tableros de Adobe Experience Platform. '
exl-id: 1d33e3ea-a8a8-4a09-8bd9-2e04ecedebdc
source-git-commit: a07eb2baec48ad514ff0afc0548f53baf34da561
workflow-type: tm+mt
source-wordcount: '589'
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

Para crear un widget personalizado, seleccione **[!UICONTROL Crear]** en el centro de la biblioteca de widgets o, si ya se han creado widgets personalizados, seleccione **[!UICONTROL Crear widget]** en la esquina superior derecha de la biblioteca de widgets.

![](../images/customization/create-widget.png)

En el cuadro de diálogo **[!UICONTROL Crear utilidad]**, puede proporcionar un título y una descripción para la nueva utilidad y elegir el atributo que desea que muestre la utilidad.

>[!NOTE]
>
>La lista de atributos disponibles depende del esquema que se haya configurado para la organización. Para obtener más información sobre la selección de atributos y la configuración de esquema, lea la guía sobre la [edición del esquema para crear widgets personalizados](edit-schema.md).

Para elegir un atributo, seleccione el botón de opción situado junto al atributo que desea añadir.

>[!NOTE]
>
>Solo se puede seleccionar un atributo por widget y solo se puede crear un widget por atributo. Si ya se ha creado un widget para un atributo, este aparece atenuado.

![](../images/customization/create-widget-dialog.png)

## Vista previa de un widget personalizado

En el cuadro de diálogo aparece una vista previa del nuevo widget, que muestra un gráfico de barras horizontales con datos ficticios.

>[!NOTE]
>
>La única métrica que actualmente se admite para todos los atributos es el recuento de perfiles y la única visualización que actualmente se admite para los widgets personalizados es un gráfico de barras horizontal.
>
>Los datos que se muestran en el widget de ejemplo solo tienen fines ilustrativos. La vista previa no muestra datos reales de su organización.

![](../images/customization/create-widget-select-attribute.png)

Para guardar la nueva utilidad y volver a la pestaña [!UICONTROL Personalizado], seleccione **[!UICONTROL Crear]**. La nueva utilidad ya está disponible para agregarse a un tablero. Para ello, elija la utilidad de la biblioteca y seleccione **[!UICONTROL Agregar utilidad]**.

## Archivar un widget personalizado

Una vez agregado un widget a la biblioteca, se puede archivar con el botón **[!UICONTROL Archive]**. También puede editar el widget para actualizar los campos de título o descripción.

## Pasos siguientes

Después de leer este documento, puede acceder a la biblioteca de widgets y utilizarla para crear y agregar utilidades personalizadas para su organización. Para modificar el tamaño y la ubicación de las utilidades que aparecen en el tablero, consulte la [guía para modificar los tableros](modify.md).
