---
title: Pestaña Red
description: Aprenda a utilizar la pestaña Red en Adobe Experience Platform Debugger.
keywords: debugger;extensión de experience Platform Debugger;chrome;extensión;red;información
seo-description: Experience Platform Debugger Network screen
seo-title: Network Tab
uuid: 839686c9-6e4f-4661-acf6-150ea24dc47f
exl-id: ed0579ef-ec26-43df-9453-a395c105038a
source-git-commit: df1a67e4b6f3d2eaeaba2b8d3c9b1588ee0b1461
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 58%

---

# Pestaña Red

El **Red** agrega todas las llamadas de la solución Adobe Experience Cloud realizadas en la página y las muestra en orden de izquierda a derecha. Los parámetros estándar se etiquetan automáticamente con nombres descriptivos y se organizan para agrupar parámetros comunes en la misma función.

![](images/network.jpg)

Esta pantalla es útil para comparar pares de valor clave entre visitas individuales. Aquí se puede confirmar que los parámetros utilizados para las integraciones, como el ID de visitante de Experience Cloud o el ID de datos suplementarios, son coherentes en todas las integraciones.

>[!NOTE]
>
>En este momento, no todos los parámetros pasados en las llamadas de solución (por ejemplo, variables de contexto de Analytics, parámetros personalizados de Target o ID de cliente del servicio de Experience Cloud ID) están visibles en la pantalla Red.

Para cambiar la información por solución, seleccione la solución que desee ver en la lista de la navegación izquierda. El siguiente ejemplo se filtra para mostrar solo Analytics:

![](images/network-analytics.jpg)

Para volver a mostrar todas las soluciones, seleccione **[!UICONTROL Red]**

Seleccione en un elemento de la vista Red para ver una vista expandida. Desde la ventana de vista expandida, puede copiar la información mostrada en el portapapeles.

![](images/network-expand.jpg)

<!--Use the icon at the top of each column to copy the server call URL to your clipboard, where you can paste it into another document for reference or debugging purposes.

![](images/copy.jpg)-->

Para borrar la lista, seleccione **[!UICONTROL Eliminar eventos]**.

Para descargar un archivo de Excel que contenga la información de esta pantalla, seleccione **[!UICONTROL Descargar]**.
