---
keywords: Experience Platform;interfaz de usuario;IU;paneles;tablero;perfiles;segmentos;destinos
title: Información general sobre la personalización de paneles
description: Obtenga más información sobre las formas de personalizar los datos que se muestran en los paneles de Adobe Experience Platform.
source-git-commit: a07eb2baec48ad514ff0afc0548f53baf34da561
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---


# Información general sobre la personalización de paneles

Los paneles de perfiles, segmentos y destinos disponibles en Adobe Experience Platform se pueden personalizar de varias formas. Esta guía proporciona información general sobre las personalizaciones disponibles, con vínculos a instrucciones paso a paso que le guiarán a través de cómo personalizar qué utilidades se muestran en los tableros, así como el tamaño, la forma y la ubicación de esas utilidades.

>[!NOTE]
>
>Los widgets que se muestran en el panel [!UICONTROL Licencia de uso] no se pueden personalizar. Para obtener más información sobre este tablero único, lea la [documentación del tablero de uso de licencias](../guides/license-usage.md).

## Modificar tablero

Al seleccionar **[!UICONTROL Modificar tablero]** entre los tableros de perfiles, segmentos o destinos, puede ajustar el tamaño, el orden y la ubicación de las utilidades que actualmente están visibles en el tablero. Para obtener información sobre cómo modificar el aspecto de las utilidades en los tableros, consulte la [guía de modificación de tableros](modify.md).

## La biblioteca de utilidades

La biblioteca de utilidades dentro de Experience Platform es donde puede ver todos los widgets [standard](#standard-widgets) y [personalizados](#custom-widgets) disponibles para su organización. Desde los tableros (por ejemplo, el tablero de perfiles), puede seleccionar **[!UICONTROL Modificar tablero]** para mostrar el botón **[!UICONTROL Biblioteca de utilidades]**.

![](../images/customization/modify-dashboard.png)

Seleccione **[!UICONTROL Biblioteca de utilidades]** para abrir la biblioteca de utilidades y ver todas las métricas estándar disponibles o empezar a crear utilidades personalizadas.

![](../images/customization/widget-library-button.png)

### Widgets estándar {#standard-widgets}

Las utilidades estándar hacen referencia a las utilidades que proporciona el Adobe para su uso en los tableros. Estas utilidades son de solo lectura y su organización no puede editarlas.

En la biblioteca de utilidades, la pestaña **[!UICONTROL Standard]** contiene todos los widgets estándar disponibles proporcionados por Adobe. Puede actualizar los tableros utilizando cualquiera de estas métricas estándar. Para obtener más información sobre la adición de widgets estándar al tablero, consulte la guía para [usar widgets estándar en tableros](standard-widgets.md).

### Widgets personalizados {#custom-widgets}

Los widgets personalizados hacen referencia a utilidades creadas y compartidas por miembros de su organización. Estos widgets se crean mediante la pestaña **[!UICONTROL Custom]** de la biblioteca de utilidades y requieren que la organización especifique las métricas disponibles mediante el uso de un [esquema](#edit-schema)

Para obtener los pasos completos para crear sus propias utilidades, consulte la [guía de widgets personalizados para tableros](custom-widgets.md).

![](../images/customization/widget-library.png)

#### Edición del esquema {#edit-schema}

Para crear un [widget personalizado](#custom-widgets) para los tableros, primero debe identificar el atributo Perfil del cliente en tiempo real en el que se basará el widget.

Para obtener instrucciones paso a paso sobre la edición del esquema de su organización para crear widgets de tablero personalizados, visite la guía para [editar el esquema de tablero](edit-schema.md).

## Pasos siguientes

Después de leer este documento, está listo para empezar a personalizar los tableros de Experience Platform modificando el tamaño, la forma y el orden de los widgets existentes, añadiendo widgets estándar proporcionados por el Adobe o creando y compartiendo widgets personalizados con su organización.
