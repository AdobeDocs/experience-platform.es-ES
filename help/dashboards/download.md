---
solution: Experience Platform
title: Descargar tableros de Experience Platform para PDF
type: Documentation
description: Guarde copias de las visualizaciones de tablero mediante la función descargar en PDF disponible en la interfaz de usuario de Experience Platform.
exl-id: 838e98a0-ce2e-4dcd-8c8f-d28ef2cb8315
source-git-commit: 5d9428c4323e65c2605fd116160e160af7d9086d
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 0%

---

# Descargar tableros para el PDF

Los paneles de Adobe Experience Platform se pueden descargar en PDF desde la interfaz de usuario de Platform para facilitar el uso compartido de la información con los miembros de la organización.

Este documento proporciona un resumen de cómo descargar tableros mediante la interfaz de usuario de Platform y guardar el tablero en el PDF mediante el menú de impresión predeterminado del explorador.

>[!WARNING]
>
>Los datos contenidos en sus paneles pueden incluir información de identificación personal (PII) sobre sus clientes o datos confidenciales relacionados con su organización. Los datos de tablero guardados en PDF deben gestionarse correctamente según las directrices de privacidad de datos de su organización.

## Descargar tablero

Para comenzar a descargar un panel, vaya al panel que desee descargar (por ejemplo, el panel [!UICONTROL Perfiles]) y, a continuación, seleccione el menú de más opciones (**`...`**) en la esquina superior derecha del panel. A continuación, seleccione **[!UICONTROL Descargar]**.

![Panel de perfiles del Experience Platform con los puntos suspensivos y la lista desplegable de descarga resaltados.](images/download/download-button.png)

## Previsualizar PDF

Después de seleccionar **[!UICONTROL Descargar]**, se abre el menú de impresión predeterminado del explorador. En este ejemplo, se muestra el menú de impresión de Google Chrome.

El menú Imprimir permite obtener una vista previa del PDF que se guardará. El PDF es una representación real de los widgets de panel tal como aparecen en la interfaz de usuario de Platform y el tamaño del PDF se ajusta automáticamente para mostrar todos los widgets de panel visibles actualmente en una sola página.

![La descripción general del perfil se muestra en un formato de una sola página con el panel Opciones de impresión a la derecha.](images/download/download-chrome-print.png)

El PDF incluye un encabezado generado automáticamente que contiene el logotipo del Experience Platform, el nombre del panel, su nombre, y la fecha y hora en que se descargó el panel. Esta información es de solo lectura y no se puede editar en el PDF.

![Un primer plano de la vista preliminar con el encabezado generado automáticamente resaltado.](images/download/download-pdf.png)

## Guardar como PDF

Después de obtener una vista previa del PDF, selecciona **Guardar** para elegir la ubicación en la que deseas guardar el PDF.

>[!NOTE]
>
>Si es necesario, puede usar el menú desplegable **Destino** para seleccionar **Guardar como PDF** si esa opción no está seleccionada automáticamente.

![La descripción general del perfil se muestra en un formato de página única con la opción desplegable Destino Guardar como PDF de impresión resaltada.](images/download/download-chrome-print-destination.png)

## Personalizar PDF de tablero

El PDF que se genera coincide con el panel que se puede ver en la interfaz de usuario e incluye solo los widgets que están visibles actualmente en el panel. Algunos paneles se pueden personalizar para cambiar el tamaño y la ubicación de los widgets o para agregar y quitar widgets de la vista. Al personalizar el aspecto del tablero en la IU de Platform, también se cambia el aspecto del PDF que se genera.

Por ejemplo, puede modificar el aspecto del panel de perfiles para incluir varios widgets de ancho completo apilados encima de tres widgets estándar.

![Se muestra el tablero de perfiles con widgets alargados.](images/download/download-modify.png)

Si selecciona descargar el panel actualizado, se obtiene una nueva vista previa del PDF que coincide con el aspecto del panel de perfiles personalizado. También ajusta automáticamente el tamaño del PDF para asegurarse de que todos los widgets visibles se incluyen en un PDF de una página.

![La descripción general del perfil se muestra en un formato de una sola página con el panel Opciones de impresión a la derecha.](images/download/download-chrome-print-modified.png)

Para obtener más información acerca de cómo personalizar paneles, comience por leer la [descripción general de la personalización de paneles](customize/overview.md).

## Pasos siguientes

Ahora que ha descargado el tablero y lo ha guardado como PDF, puede repetir estos pasos para descargar tableros adicionales o compartir el PDF con miembros de su organización.
