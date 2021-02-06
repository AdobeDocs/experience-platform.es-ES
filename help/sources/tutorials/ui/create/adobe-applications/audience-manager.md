---
keywords: Experience Platform;inicio;temas populares;conector de origen del administrador de Audiencias;Audience Manager;conector del administrador de audiencias
solution: Experience Platform
title: Creación de una conexión de origen de Adobe Audience Manager en la interfaz de usuario
topic: overview
type: Tutorial
description: Este tutorial lo acompaña a través de los pasos para crear un conector de origen para Adobe Audience Manager con el fin de incorporar datos de Evento de experiencias de consumo a la plataforma mediante la interfaz de usuario.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---


# Creación de una conexión de origen de Adobe Audience Manager en la interfaz de usuario

Este tutorial lo acompaña a través de los pasos para crear un conector de origen para Adobe Audience Manager con el fin de incorporar datos de Evento de experiencias de consumo a la plataforma mediante la interfaz de usuario.

## Creación de una conexión de origen con Adobe Audience Manager

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder al espacio de trabajo [!UICONTROL Fuentes]. La pantalla [!UICONTROL Catálogo] muestra una variedad de fuentes con las que puede crear una cuenta.

En la categoría [!UICONTROL aplicaciones de Adobe], seleccione **[!UICONTROL Adobe Audience Manager]** y, a continuación, seleccione **[!UICONTROL Configurar]**.

![catálogo](../../../../images/tutorials/create/aam/catalog.png)

Aparece el paso [!UICONTROL Seleccionar características y segmentos], que le proporciona una interfaz interactiva para explorar y seleccionar sus características, segmentos y datos.

* El panel izquierdo de la interfaz contiene las opciones [!UICONTROL Seleccionar características y segmentos], así como un directorio jerárquico de todos los segmentos disponibles para usted.
* La mitad correcta de la interfaz le permite interactuar con segmentos seleccionados y elegir los datos específicos que desee utilizar.

![add-data](../../../../images/tutorials/create/aam/add-data.png)

Para navegar por los segmentos disponibles, seleccione la carpeta a la que desea acceder desde el panel [!UICONTROL Todos los segmentos]. La selección de una carpeta le permite recorrer la jerarquía de una carpeta y le proporciona una lista de segmentos para filtrar.

![segment-folder](../../../../images/tutorials/create/aam/segment-folder.png)

Una vez identificados y seleccionados los segmentos que desea utilizar, aparece un nuevo panel a la derecha, que muestra la lista de los elementos seleccionados. Puede seguir accediendo a diferentes carpetas y seleccionar diferentes segmentos para la conexión. Al seleccionar más segmentos, se actualiza el panel de la derecha.

![select-data](../../../../images/tutorials/create/aam/select-data.png)

También puede seleccionar los cuadros **[!UICONTROL Seleccionar todos los segmentos]** y **[!UICONTROL Seleccionar todas las características]**. Si selecciona todos los segmentos, los segmentos de Audience Manager se mostrarán en la plataforma, mientras que si selecciona todas las características, se habilitarán todas las características de origen del Audience Manager.

Una vez finalizado, seleccione **[!UICONTROL Siguiente]**

![todos los segmentos](../../../../images/tutorials/create/aam/all-segments.png)

Aparece el paso [!UICONTROL Revisar], que le permite revisar los rasgos y segmentos seleccionados antes de que estén conectados a Plataforma. Los detalles se agrupan en las siguientes categorías:

* **[!UICONTROL Conexión]**: Muestra la plataforma de origen y el estado de la conexión.
* **[!UICONTROL Datos]** seleccionados: Muestra el número de segmentos seleccionados y características habilitadas.

![revisión](../../../../images/tutorials/create/aam/review.png)

Una vez que haya revisado el flujo de datos, seleccione **[!UICONTROL Finalizar]** y permita que se cree el flujo de datos.

## Pasos siguientes

Mientras un flujo de datos de Audience Manager está activo, los datos entrantes se ingieren automáticamente en Perfiles del cliente en tiempo real. Ahora puede utilizar estos datos entrantes y crear segmentos de audiencia mediante el servicio de segmentación de plataformas. Consulte los siguientes documentos para obtener más información:

* [Información general sobre el Perfil del cliente en tiempo real](../../../../../profile/home.md)
* [Descripción general del servicio de segmentación](../../../../../segmentation/home.md)