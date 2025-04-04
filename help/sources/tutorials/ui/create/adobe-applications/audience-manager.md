---
keywords: Experience Platform;inicio;temas populares;conector de origen de Audience Manager;Audience Manager;conector de Audience Manager
title: Creación de una conexión de Adobe Audience Manager Source en la IU
description: Este tutorial le guiará por los pasos para crear una conexión de origen para que Adobe Audience Manager introduzca datos de evento de experiencia del consumidor en Experience Platform mediante la interfaz de usuario.
exl-id: 90c4a719-aaad-4687-afd8-7a1c0c56f744
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 1%

---

# Crear una conexión de origen de Adobe Audience Manager en la interfaz de usuario

Este tutorial le guiará por los pasos para crear un conector de origen para Adobe Audience Manager para introducir datos de evento de experiencia del consumidor en Experience Platform mediante la interfaz de usuario.

## Crear una conexión de origen con Adobe Audience Manager

En la interfaz de usuario de Experience Platform, seleccione **[!UICONTROL Fuentes]** en el panel de navegación izquierdo para acceder al área de trabajo [!UICONTROL Fuentes]. La pantalla [!UICONTROL Catálogo] muestra una variedad de orígenes con los que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar en la barra de búsqueda.

En [!UICONTROL Aplicación de Adobe], seleccione **[!UICONTROL Adobe Audience Manager]** y, a continuación, **[!UICONTROL Configurar]**.

![catálogo](../../../../images/tutorials/create/aam/catalog.png)

### Seleccionar rasgos y segmentos

>[!NOTE]
>
>No puede introducir datos regionales del origen de Audience Manager en Experience Platform. Si tiene casos de uso de Analytics que requieren datos regionales, use el [conector de origen de Analytics](../adobe-applications/analytics.md).

Aparecerá el paso [!UICONTROL Seleccionar características y segmentos], que le proporcionará una interfaz interactiva para explorar y seleccionar sus características, segmentos y datos.

* El panel izquierdo de la interfaz contiene las opciones [!UICONTROL Seleccionar características y segmentos], así como un directorio jerárquico de todos los segmentos disponibles para usted.
* La mitad derecha de la interfaz le permite interactuar con segmentos seleccionados y elegir entre los datos específicos que desea utilizar.

![add-data](../../../../images/tutorials/create/aam/add-data.png)

Para navegar por los segmentos disponibles, seleccione la carpeta a la que desee acceder desde el panel [!UICONTROL Todos los segmentos]. La selección de una carpeta le permite recorrer la jerarquía de una carpeta y le proporciona una lista de segmentos por los que filtrar.

![carpeta-segmento](../../../../images/tutorials/create/aam/segment-folder.png)

Una vez que haya identificado y seleccionado los segmentos que desea utilizar, aparecerá un nuevo panel a la derecha que mostrará la lista de los elementos seleccionados. Puede seguir accediendo a diferentes carpetas y seleccionar distintos segmentos para la conexión. Al seleccionar más segmentos, se actualiza el panel de la derecha.

![select-data](../../../../images/tutorials/create/aam/select-data.png)

También puede seleccionar los cuadros **[!UICONTROL Seleccionar todos los segmentos]** y **[!UICONTROL Seleccionar todos los rasgos]**. La selección de todos los segmentos llevará los segmentos de Audience Manager a Experience Platform, mientras que la selección de todos los rasgos habilita todos los rasgos de origen de Audience Manager.

>[!WARNING]
>
>La ingesta de poblaciones de segmentos de Audience Manager de tamaño considerable tiene un impacto directo en el recuento total de perfiles la primera vez que envía un segmento de Audience Manager a Experience Platform mediante la fuente de Audience Manager. Esto significa que la selección de todos los segmentos puede dar lugar potencialmente a un recuento de perfiles que supere el derecho de uso de la licencia. Revise su [asignación de uso de licencia](../../../../../dashboards/guides/license-usage.md) antes de continuar.

Una vez que finalice, seleccione **[!UICONTROL Siguiente]**

![todos los segmentos](../../../../images/tutorials/create/aam/all-segments.png)

Aparecerá el paso [!UICONTROL Revisar], que le permitirá revisar los rasgos y segmentos seleccionados antes de que se conecten a Experience Platform. Los detalles se agrupan en las siguientes categorías:

* **[!UICONTROL Conexión]**: muestra la plataforma de origen y el estado de la conexión.
* **[!UICONTROL Datos seleccionados]**: muestra el número de segmentos seleccionados y las características habilitadas.

![revisión](../../../../images/tutorials/create/aam/review.png)

Una vez que haya revisado el flujo de datos, seleccione **[!UICONTROL Finalizar]** y espere un poco para que se cree el flujo de datos.

## Pasos siguientes

Mientras hay un flujo de datos de Audience Manager activo, los datos entrantes se incorporan automáticamente a los perfiles de cliente en tiempo real. Ahora puede utilizar estos datos entrantes y crear segmentos de audiencia utilizando el servicio de segmentación de Experience Platform. Consulte los siguientes documentos para obtener más información:

* [Información general del perfil del cliente en tiempo real](../../../../../profile/home.md)
* [Resumen del servicio de segmentación](../../../../../segmentation/home.md)
