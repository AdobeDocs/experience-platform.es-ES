---
keywords: Experience Platform;interfaz de usuario;IU;paneles;tablero;perfiles;segmentos;destinos
title: Información general sobre la personalización de paneles
description: Obtenga más información sobre las formas de personalizar los datos que se muestran en los paneles de Adobe Experience Platform.
exl-id: efabdb61-4148-4b0e-b7a1-6e788b5e43a8
source-git-commit: 27252d547afd30acc7b334d5054f1350dc0031b7
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---

# Información general sobre la personalización de paneles

Los paneles de perfiles, segmentos y destinos disponibles en Adobe Experience Platform se pueden personalizar de varias formas. Esta guía proporciona información general sobre las personalizaciones disponibles, con vínculos a instrucciones paso a paso que le guiarán a través de cómo personalizar qué utilidades se muestran en los tableros, así como el tamaño, la forma y la ubicación de esas utilidades.

>[!NOTE]
>
>Los widgets mostrados en la variable [!UICONTROL Uso de licencias] tablero no se puede personalizar. Para obtener más información sobre este tablero único, lea la [documentación del panel de uso de licencias](../guides/license-usage.md).

## Modificar tablero

Selección **[!UICONTROL Modificar tablero]** desde los paneles perfiles, segmentos o destinos , puede ajustar el tamaño, el orden y la ubicación de las utilidades que están visibles en el tablero. Para obtener información sobre cómo modificar el aspecto de las utilidades en los paneles, consulte la [guía de modificación de tableros](modify.md).

## La biblioteca de utilidades

La biblioteca de utilidades del Experience Platform es donde puede ver todas las [standard](#standard-widgets) y [custom](#custom-widgets) widgets disponibles para su organización. Desde los tableros (por ejemplo, el tablero de perfiles), puede seleccionar **[!UICONTROL Modificar tablero]** para mostrar la variable **[!UICONTROL Biblioteca de utilidades]** botón.

![El panel Perfiles con el panel Modificar resaltado.](../images/customization/modify-dashboard.png)

Select **[!UICONTROL Biblioteca de utilidades]** para abrir la biblioteca de utilidades y ver todas las métricas estándar disponibles o empezar a crear utilidades personalizadas.

![Panel de perfiles con biblioteca de widgets resaltada.](../images/customization/widget-library-button.png)

### Widgets estándar {#standard-widgets}

Las utilidades estándar hacen referencia a las utilidades que proporciona el Adobe para su uso en los tableros. Estas utilidades son de solo lectura y su organización no puede editarlas.

Dentro de la biblioteca de utilidades, la variable **[!UICONTROL Estándar]** contiene todos los widgets estándar disponibles proporcionados por Adobe. Puede actualizar los tableros utilizando cualquiera de estas métricas estándar. Para obtener más información sobre la adición de utilidades estándar al tablero, consulte la guía de [uso de widgets estándar en tableros](standard-widgets.md).

### Widgets personalizados {#custom-widgets}

Las utilidades personalizadas hacen referencia a las utilidades creadas y compartidas por miembros de su organización. Estos widgets se crean mediante la variable **[!UICONTROL Personalizado]** de la biblioteca de utilidades y requerir que su organización especifique las métricas disponibles mediante el uso de un [esquema](#edit-schema)

Para ver los pasos completos para crear sus propias utilidades, consulte la [guía de widgets personalizados para tableros](custom-widgets.md).

![Espacio de trabajo de la biblioteca de utilidades con las opciones Estándar y Personalizado resaltadas.](../images/customization/widget-library.png)

#### Editar esquema {#edit-schema}

Para crear un [utilidad personalizada](#custom-widgets) para los tableros, primero debe identificar el atributo Perfil del cliente en tiempo real en el que se basará el widget.

Para obtener instrucciones paso a paso sobre la edición del esquema de su organización con el fin de crear widgets de tablero personalizados, visite la guía de [editar el esquema del panel](edit-schema.md).

## Pasos siguientes

Después de leer este documento, está listo para empezar a personalizar los tableros de Experience Platform modificando el tamaño, la forma y el orden de los widgets existentes, añadiendo widgets estándar proporcionados por el Adobe o creando y compartiendo widgets personalizados con su organización.
