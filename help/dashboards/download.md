---
solution: Experience Platform
title: Descargar tableros de Experience Platform al PDF
type: Documentation
description: Guarde copias de las visualizaciones de tablero mediante la función de descarga a PDF disponible en la interfaz de usuario del Experience Platform.
exl-id: 838e98a0-ce2e-4dcd-8c8f-d28ef2cb8315
source-git-commit: 5d9428c4323e65c2605fd116160e160af7d9086d
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 0%

---

# Descargar tableros en el PDF

Los tableros dentro de Adobe Experience Platform se pueden descargar al PDF desde la interfaz de usuario de Platform para facilitar el intercambio de información con los miembros de su organización.

En este documento se proporciona un resumen de cómo descargar tableros mediante la interfaz de usuario de Platform y guardar el tablero en el PDF mediante el menú de impresión predeterminado del explorador.

>[!WARNING]
>
>Los datos contenidos en los paneles pueden incluir información de identificación personal (PII) sobre sus clientes o datos confidenciales relacionados con su organización. Los datos del tablero guardados en el PDF deben gestionarse adecuadamente de acuerdo con las directrices de privacidad de datos de su organización.

## Descargar tablero

Para empezar a descargar un tablero, vaya al tablero que desea descargar (por ejemplo, el [!UICONTROL Perfiles] tablero) y, a continuación, seleccione el menú más opciones (**`...`**) desde la esquina superior derecha del tablero. A continuación, seleccione **[!UICONTROL Descargar]**.

![El tablero Perfiles del Experience Platform con los elipsis y la lista desplegable Descargar resaltados.](images/download/download-button.png)

## PDF de vista previa

Después de seleccionar **[!UICONTROL Descargar]**, se abrirá el menú de impresión predeterminado del explorador. En este ejemplo, se muestra el menú de impresión de Google Chrome.

El menú de impresión le permite previsualizar el PDF que se guardará. El PDF es una representación verdadera de los widgets de tablero tal como aparecen en la interfaz de usuario de Platform y el tamaño del PDF se ajusta automáticamente para mostrar todos los widgets de tablero visibles actualmente en una sola página.

![La descripción general del perfil se muestra en un formato de una sola página con el panel Opciones de impresión a la derecha.](images/download/download-chrome-print.png)

El PDF incluye un encabezado generado automáticamente que contiene el logotipo del Experience Platform, el nombre del tablero, su nombre y la fecha y hora en que se descargó el tablero. Esta información es de solo lectura y no se puede editar en el PDF.

![Cierre de la vista previa de impresión con el encabezado generado automáticamente resaltado.](images/download/download-pdf.png)

## Guardar como PDF

Después de obtener una vista previa del PDF, seleccione **Guardar** para elegir la ubicación en la que desea guardar al PDF.

>[!NOTE]
>
>Si es necesario, puede usar la variable **Destino** lista desplegable para seleccionar **Guardar como PDF** si esa opción no está seleccionada automáticamente.

![La descripción general del perfil se muestra en un formato de una sola página con la opción de impresión desplegable Destino Guardar como PDF resaltada.](images/download/download-chrome-print-destination.png)

## Personalizar PDF de tablero

El PDF que se genera coincide con el panel que puede ver en la interfaz de usuario e incluye solo las utilidades que están visibles actualmente en el panel. Algunos tableros se pueden personalizar para cambiar el tamaño y la ubicación de las utilidades o para agregar y quitar utilidades de la vista. Al personalizar el aspecto del tablero en la interfaz de usuario de Platform, también se cambia el aspecto del PDF que se genera.

Por ejemplo, puede modificar el aspecto del tablero de perfiles para incluir varias utilidades de ancho completo apiladas por encima de tres utilidades estándar.

![Se muestra el panel Perfil que muestra el widget alargado.](images/download/download-modify.png)

Al seleccionar para descargar el tablero actualizado, se obtiene una nueva vista previa del PDF que coincide con el aspecto del tablero de perfiles personalizado. También ajusta automáticamente el tamaño del PDF para garantizar que todos los widgets visibles se incluyen en un PDF de una página.

![La descripción general del perfil se muestra en un formato de una sola página con el panel Opciones de impresión a la derecha.](images/download/download-chrome-print-modified.png)

Para obtener más información sobre la personalización de tableros, comience por leer la [información general sobre la personalización de tableros](customize/overview.md).

## Pasos siguientes

Ahora que ha descargado el tablero y lo ha guardado como PDF, puede repetir estos pasos para descargar tableros adicionales o compartir el PDF con miembros de su organización.
