---
keywords: Experience Platform;inicio;temas populares;conector de origen de Audience Manager;Audience Manager;conector de Audience Manager
title: Crear una conexión de origen de Adobe Audience Manager en la interfaz de usuario
description: Este tutorial le guía por los pasos para crear una conexión de origen para que Adobe Audience Manager introduzca datos de Evento de experiencia del consumidor en Platform mediante la interfaz de usuario.
exl-id: 90c4a719-aaad-4687-afd8-7a1c0c56f744
source-git-commit: 9cdb8933d166445bf41ed314d7ffc7d5762e1adb
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 0%

---

# Crear una conexión de origen de Adobe Audience Manager en la interfaz de usuario

Este tutorial le guía por los pasos para crear un conector de origen para que Adobe Audience Manager introduzca datos de Evento de experiencia del consumidor en Platform mediante la interfaz de usuario.

## Crear una conexión de origen con Adobe Audience Manager

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Fuentes]** desde el panel de navegación izquierdo para acceder a la [!UICONTROL Fuentes] espacio de trabajo. La variable [!UICONTROL Catálogo] muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar mediante la barra de búsqueda.

En [!UICONTROL Aplicación Adobe], seleccione **[!UICONTROL Adobe Audience Manager]** y, a continuación, seleccione **[!UICONTROL Configuración]**.

![catálogo](../../../../images/tutorials/create/aam/catalog.png)

### Seleccionar características y segmentos

>[!NOTE]
>
>No se pueden ingerir datos regionales del origen del Audience Manager al Experience Platform. Si tiene casos de uso de Analytics que requieren datos regionales, use la variable [Conector de origen de Analytics](../adobe-applications/analytics.md).

La variable [!UICONTROL Seleccionar características y segmentos] aparece, proporcionando una interfaz interactiva para explorar y seleccionar sus características, segmentos y datos.

* El panel izquierdo de la interfaz contiene la variable [!UICONTROL Seleccionar características y segmentos] , así como un directorio jerárquico de todos los segmentos disponibles para usted.
* La mitad derecha de la interfaz le permite interactuar con segmentos seleccionados y elegir los datos específicos que desee utilizar.

![add-data](../../../../images/tutorials/create/aam/add-data.png)

Para navegar por los segmentos disponibles, seleccione la carpeta a la que desee acceder desde la [!UICONTROL Todos los segmentos] panel. La selección de una carpeta le permite recorrer la jerarquía de una carpeta y le proporciona una lista de segmentos para filtrar.

![segment-folder](../../../../images/tutorials/create/aam/segment-folder.png)

Una vez identificados y seleccionados los segmentos que desea utilizar, aparece un panel nuevo a la derecha, que muestra la lista de elementos seleccionados. Puede seguir accediendo a diferentes carpetas y seleccionar diferentes segmentos para la conexión. Al seleccionar más segmentos, se actualiza el panel de la derecha.

![select-data](../../../../images/tutorials/create/aam/select-data.png)

También puede seleccionar el **[!UICONTROL Seleccionar todos los segmentos]** y **[!UICONTROL Seleccionar todas las características]** para abrir el Navegador. Al seleccionar todos los segmentos, los segmentos de Audience Manager se mostrarán en Platform, mientras que al seleccionar todos los rasgos se habilitarán todos los rasgos de origen del Audience Manager.

>[!WARNING]
>
>La ingesta de grandes poblaciones de segmentos de Audience Manager tiene un impacto directo en el recuento total de perfiles cuando envía por primera vez un segmento de Audience Manager a Platform mediante la fuente de Audience Manager. Esto significa que si selecciona todos los segmentos, es posible que se produzca un recuento de perfiles superior a su derecho de uso de licencia. Revise su [asignación de uso de licencia](../../../../../dashboards/guides/license-usage.md) antes de continuar.

Una vez finalizado, seleccione **[!UICONTROL Siguiente]**

![todos los segmentos](../../../../images/tutorials/create/aam/all-segments.png)

La variable [!UICONTROL Consulte] , lo que le permite revisar los rasgos y segmentos seleccionados antes de conectarse a Platform. Los detalles se agrupan en las siguientes categorías:

* **[!UICONTROL Conexión]**: Muestra la plataforma de origen y el estado de la conexión.
* **[!UICONTROL Datos seleccionados]**: Muestra el número de segmentos seleccionados y características habilitadas.

![review](../../../../images/tutorials/create/aam/review.png)

Una vez que haya revisado el flujo de datos, seleccione **[!UICONTROL Finalizar]** y permitir que se cree un flujo de datos.

## Pasos siguientes

Mientras está activo un flujo de datos de Audience Manager, los datos entrantes se introducen automáticamente en Perfiles del cliente en tiempo real. Ahora puede utilizar estos datos entrantes y crear segmentos de audiencia mediante el servicio de segmentación de plataforma. Consulte los siguientes documentos para obtener más información:

* [Resumen del perfil del cliente en tiempo real](../../../../../profile/home.md)
* [Información general del servicio de segmentación](../../../../../segmentation/home.md)
