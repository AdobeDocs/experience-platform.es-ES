---
keywords: Experience Platform;interfaz de usuario;IU;tableros;tablero;perfiles;segmentos;destinos
title: Información general de personalización de paneles
description: Obtenga más información acerca de las formas en que puede personalizar los datos mostrados en los paneles de Adobe Experience Platform.
exl-id: efabdb61-4148-4b0e-b7a1-6e788b5e43a8
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---

# Resumen de personalización de paneles

Los paneles de perfiles, segmentos y destinos disponibles en Adobe Experience Platform se pueden personalizar de varias formas. Esta guía proporciona información general sobre las personalizaciones disponibles, con vínculos a instrucciones paso a paso que le guían a través de cómo personalizar qué widgets se muestran en los paneles, así como el tamaño, la forma y la ubicación de esos widgets.

>[!NOTE]
>
>Los widgets que se muestran en la [!UICONTROL Uso de licencias] el tablero no se puede personalizar. Para obtener más información sobre este tablero único, lea la [documentación del tablero de uso de licencias](../guides/license-usage.md).

## Modificar tablero

Seleccionar **[!UICONTROL Modificar tablero]** desde los paneles de perfiles, segmentos o destinos puede ajustar el tamaño, el orden y la ubicación de los widgets que están visibles actualmente en el panel. Para obtener información sobre cómo modificar el aspecto de los widgets en los paneles, consulte la [guía de modificación de paneles](modify.md).

## La biblioteca de widgets

La biblioteca de widgets dentro de Experience Platform es donde puede ver todas las [standard](#standard-widgets) y [personalizado](#custom-widgets) widgets disponibles para su organización. En los paneles (por ejemplo, el panel de perfiles), puede seleccionar **[!UICONTROL Modificar tablero]** para mostrar el **[!UICONTROL Biblioteca de widgets]** botón.

![Panel de perfiles con el panel de modificación resaltado.](../images/customization/modify-dashboard.png)

Seleccionar **[!UICONTROL Biblioteca de widgets]** para abrir la biblioteca de widgets y ver todas las métricas estándar disponibles o empezar a crear widgets personalizados.

![El panel Perfiles con la biblioteca Widget resaltada.](../images/customization/widget-library-button.png)

### Widgets estándar {#standard-widgets}

Los widgets estándar hacen referencia a los widgets que proporciona el Adobe para su uso en los paneles. Estos widgets son de solo lectura y su organización no puede editarlos.

En la biblioteca de widgets, la variable **[!UICONTROL Standard]** La pestaña contiene todos los widgets estándar disponibles proporcionados por Adobe. Puede actualizar los paneles mediante cualquiera de estas métricas estándar. Para obtener más información sobre cómo añadir widgets estándar al panel, consulte la guía de [uso de widgets estándar en paneles](standard-widgets.md).

### Widgets personalizados {#custom-widgets}

Los widgets personalizados hacen referencia a widgets creados y compartidos por miembros de su organización. Estos widgets se crean mediante la variable **[!UICONTROL Personalizado]** de la biblioteca de widgets y requiere que su organización especifique las métricas disponibles mediante el uso de una [esquema](#edit-schema)

Para ver los pasos completos para crear sus propios widgets, consulte la [guía de widgets personalizados para paneles](custom-widgets.md).

![Espacio de trabajo de la biblioteca de widgets con resaltados Estándar y Personalizado.](../images/customization/widget-library.png)

#### Editar esquema {#edit-schema}

Para crear un [widget personalizado](#custom-widgets) para los paneles, primero debe identificar el atributo Perfil del cliente en tiempo real en el que se basará el widget.

Para obtener instrucciones paso a paso sobre cómo editar el esquema de su organización para crear widgets de panel personalizados, visite la guía de [edición del esquema del tablero](edit-schema.md).

## Pasos siguientes

Después de leer este documento, está listo para empezar a personalizar los paneles de Experience Platform modificando el tamaño, la forma y el orden de los widgets existentes, agregando widgets estándar proporcionados por Adobe o creando y compartiendo widgets personalizados con su organización.
