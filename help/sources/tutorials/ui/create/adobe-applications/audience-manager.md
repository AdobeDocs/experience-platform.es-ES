---
keywords: Experience Platform;inicio;temas populares;conector de origen de Audience Manager;Audience Manager;conector de Audience Manager
solution: Experience Platform
title: Crear una conexión de origen de Adobe Audience Manager en la interfaz de usuario
topic-legacy: overview
type: Tutorial
description: Este tutorial le guía por los pasos para crear un conector de origen para que Adobe Audience Manager introduzca datos de Evento de experiencia del consumidor en Platform mediante la interfaz de usuario.
exl-id: 90c4a719-aaad-4687-afd8-7a1c0c56f744
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---

# Crear una conexión de origen de Adobe Audience Manager en la interfaz de usuario

Este tutorial le guía por los pasos para crear un conector de origen para que Adobe Audience Manager introduzca datos de Evento de experiencia del consumidor en Platform mediante la interfaz de usuario.

## Crear una conexión de origen con Adobe Audience Manager

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Sources]** en la barra de navegación izquierda para acceder al espacio de trabajo [!UICONTROL Sources]. La pantalla [!UICONTROL Catalog] muestra una variedad de fuentes para las que puede crear una cuenta.

En la categoría [!UICONTROL Adobe applications], seleccione **[!UICONTROL Adobe Audience Manager]** y luego seleccione **[!UICONTROL Configure]**.

![catálogo](../../../../images/tutorials/create/aam/catalog.png)

Aparece el paso [!UICONTROL Select traits and segments], que le proporciona una interfaz interactiva para explorar y seleccionar sus rasgos, segmentos y datos.

* El panel izquierdo de la interfaz contiene las opciones [!UICONTROL Select traits and segments], así como un directorio jerárquico de todos los segmentos disponibles para usted.
* La mitad derecha de la interfaz le permite interactuar con segmentos seleccionados y elegir los datos específicos que desee utilizar.

![add-data](../../../../images/tutorials/create/aam/add-data.png)

Para navegar por los segmentos disponibles, seleccione la carpeta a la que desee acceder desde el panel [!UICONTROL All Segments] . La selección de una carpeta le permite recorrer la jerarquía de una carpeta y le proporciona una lista de segmentos para filtrar.

![segment-folder](../../../../images/tutorials/create/aam/segment-folder.png)

Una vez identificados y seleccionados los segmentos que desea utilizar, aparece un panel nuevo a la derecha, que muestra la lista de elementos seleccionados. Puede seguir accediendo a diferentes carpetas y seleccionar diferentes segmentos para la conexión. Al seleccionar más segmentos, se actualiza el panel de la derecha.

![select-data](../../../../images/tutorials/create/aam/select-data.png)

También puede seleccionar los cuadros **[!UICONTROL Select all segments]** y **[!UICONTROL Select all traits]**. Al seleccionar todos los segmentos, los segmentos de Audience Manager se mostrarán en Platform, mientras que al seleccionar todos los rasgos se habilitarán todos los rasgos de origen del Audience Manager.

Una vez finalizado, seleccione **[!UICONTROL Next]**

![todos los segmentos](../../../../images/tutorials/create/aam/all-segments.png)

Aparece el paso [!UICONTROL Review] , que le permite revisar los rasgos y segmentos seleccionados antes de que se conecten a Platform. Los detalles se agrupan en las siguientes categorías:

* **[!UICONTROL Connection]**: Muestra la plataforma de origen y el estado de la conexión.
* **[!UICONTROL Selected data]**: Muestra el número de segmentos seleccionados y características habilitadas.

![review](../../../../images/tutorials/create/aam/review.png)

Una vez que haya revisado el flujo de datos, seleccione **[!UICONTROL Finish]** y permita que se cree el flujo de datos.

## Pasos siguientes

Mientras está activo un flujo de datos de Audience Manager, los datos entrantes se introducen automáticamente en Perfiles del cliente en tiempo real. Ahora puede utilizar estos datos entrantes y crear segmentos de audiencia mediante el servicio de segmentación de plataforma. Consulte los siguientes documentos para obtener más información:

* [Resumen del perfil del cliente en tiempo real](../../../../../profile/home.md)
* [Información general del servicio de segmentación](../../../../../segmentation/home.md)
