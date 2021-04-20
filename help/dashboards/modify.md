---
keywords: Experience Platform;interfaz de usuario;IU;paneles;tablero;perfiles;segmentos;destinos;uso de licencias
title: Modificación de paneles de plataforma en la interfaz de usuario
description: 'Esta guía proporciona instrucciones paso a paso para personalizar la forma en que se muestran los datos de Adobe Experience Platform de su organización en los paneles. '
topic: guide
translation-type: tm+mt
source-git-commit: 5cc973a5db88eb23c6e1aeee3695820a0555e4cf
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 2%

---


# (Beta) Modificación de tableros {#modify-dashboards}

>[!IMPORTANT]
>
>La funcionalidad del panel está actualmente en fase beta y no está disponible para todos los usuarios. La documentación y las funciones están sujetas a cambios.

En la interfaz de usuario (IU) de Adobe Experience Platform, puede ver e interactuar con los datos de su organización mediante varios paneles. Las utilidades y métricas predeterminadas que se muestran en los tableros se pueden ajustar a nivel de usuario para mostrar los datos y utilidades preferidos y se pueden crear y compartir entre usuarios de la misma organización.

Esta guía proporciona instrucciones paso a paso para personalizar el modo en que se muestran los datos del tablero dentro de los tableros [!UICONTROL Profiles], [!UICONTROL Segments] y [!UICONTROL Destinations] en la interfaz de usuario de Platform.

>[!NOTE]
>
>Los widgets mostrados en el panel de uso de licencias no se pueden personalizar. Consulte la [documentación del tablero de uso de licencias](guides/license-usage.md) para obtener más información sobre este tablero único.

## Primeros pasos

Desde cualquier tablero (por ejemplo, el tablero [!UICONTROL Profiles]), puede seleccionar **[!UICONTROL Modificar tablero]** para cambiar el tamaño y reordenar los widgets existentes.

![](images/customization/modify-dashboard.png)

## Reordenar widgets

Después de modificar el tablero, puede reordenar los widgets seleccionando el título del widget y arrastrando y soltando los widgets en el orden deseado. En este ejemplo, la utilidad **[!UICONTROL Profiles by identity namespace]** se mueve a la fila superior y la utilidad [!UICONTROL Profile Count] aparece ahora en la segunda fila.

![](images/customization/move-widget.png)

## Cambiar el tamaño de los widgets

También puede cambiar el tamaño de un widget seleccionando el símbolo de ángulo en la esquina inferior derecha del widget (`⌟`) y arrastrando el widget al tamaño deseado. En este ejemplo, se cambia el tamaño del widget **[!UICONTROL Profiles by identity namespace]** para rellenar toda la fila superior, moviendo automáticamente los demás widgets a la segunda fila. Observe cómo el eje horizontal se ajusta para proporcionar incrementos más detallados a medida que la utilidad se hace más grande.

>[!NOTE]
>
>A medida que los widgets se ajustan en su tamaño, los widgets circundantes se cambian de posición de forma dinámica. Esto podría hacer que algunos widgets se movieran a filas adicionales, lo que requería que se desplazara para ver todos los widgets.

![](images/customization/resize-widget.png)

## Guardar actualizaciones del tablero

Cuando haya terminado de mover y cambiar el tamaño de las utilidades, seleccione **[!UICONTROL Guardar]** para guardar los cambios y volver a la vista del tablero principal. Si no desea conservar los cambios, seleccione **[!UICONTROL Cancelar]** para restablecer el tablero y volver a la vista del tablero principal.

![](images/customization/save-changes.png)

## Biblioteca de utilidades

Además de cambiar el tamaño y reordenar las utilidades, en los paneles [!UICONTROL Perfiles] y [!UICONTROL Segmentos] puede seleccionar más utilidades para mostrar o crear utilidades utilizando la **[!UICONTROL Biblioteca de utilidades]**.

Para obtener instrucciones paso a paso sobre cómo acceder y trabajar con la [!UICONTROL biblioteca de utilidades], consulte la [guía de biblioteca de utilidades](widget-library.md).

## Pasos siguientes

Después de leer este documento, ha aprendido a utilizar la funcionalidad de modificar tablero para reordenar y cambiar el tamaño de las utilidades y personalizar la vista del tablero. Para aprender a crear y agregar widgets a los tableros, lea la [guía de la biblioteca de widgets](widget-library.md).