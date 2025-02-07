---
title: Conexión de la zona de aterrizaje de datos a Platform mediante la IU
description: Obtenga información sobre cómo crear un conector de origen de zona de aterrizaje de datos mediante la interfaz de usuario de Platform.
exl-id: 653c9958-5d89-4b0c-af3d-a3e74aa47a08
source-git-commit: cdcce07a5adf08bf9d5e6a08d6bc965d37458a5d
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 0%

---

# Conectar [!DNL Data Landing Zone] a Platform mediante la interfaz de usuario

>[!IMPORTANT]
>
>Esta página es específica para el conector [!DNL Data Landing Zone] *source* en el Experience Platform. Para obtener información sobre cómo conectarse al conector [!DNL Data Landing Zone] *destination*, consulte la [[!DNL Data Landing Zone] página de documentación de destino](/help/destinations/catalog/cloud-storage/data-landing-zone.md).

[!DNL Data Landing Zone] es una función de almacenamiento de archivos segura y basada en la nube que permite traer archivos a Adobe Experience Platform. Los datos se eliminan automáticamente de [!DNL Data Landing Zone] pasados siete días.

Este tutorial proporciona los pasos para crear una conexión de origen [!DNL Data Landing Zone] mediante la interfaz de usuario de Platform.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): El Experience Platform permite la ingesta de datos de varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Zonas protegidas](../../../../../sandboxes/home.md): El Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

## Traer los archivos de [!DNL Data Landing Zone] a Platform

>[!IMPORTANT]
>
> Para conectarse al origen, necesita los permisos de control de acceso de **[!UICONTROL Ver orígenes]** y **[!UICONTROL Administrar orígenes]**. Lea la [descripción general del control de acceso](../../../../../access-control/home.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Sources]** en el panel de navegación izquierdo para acceder al área de trabajo [!UICONTROL Sources]. La pantalla [!UICONTROL Catálogo] muestra una variedad de orígenes con los que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar en la barra de búsqueda.

En la categoría [!UICONTROL almacenamiento en la nube], seleccione [!DNL Data Landing Zone] y luego **[!UICONTROL Agregar datos]**.

![El catálogo de orígenes con la zona de aterrizaje de datos seleccionada.](../../../../images/tutorials/create/dlz/catalog.png)

Aparecerá el paso [!UICONTROL Agregar datos], que le proporcionará una interfaz para seleccionar y previsualizar los datos que desea llevar a Platform.

* La parte izquierda de la interfaz es un explorador de carpetas, que le proporciona una lista de archivos del contenedor que puede llevar a Platform.
* La parte derecha de la interfaz de permite obtener una vista previa de hasta 100 filas de datos de un archivo compatible.

Seleccione el archivo que desea llevar al Experience Platform y espere unos momentos para que la interfaz correcta se actualice en una pantalla de previsualización.

![Interfaz de agregar datos del área de trabajo de orígenes.](../../../../images/tutorials/create/dlz/add-data.png)

>[!TIP]
>
>Platform detecta automáticamente la información de propiedad del archivo seleccionado, incluida la información sobre el formato de datos del archivo, el delimitador de columna designado y el tipo de compresión.

La interfaz de vista previa permite inspeccionar el contenido y la estructura de un archivo. De forma predeterminada, la interfaz de vista previa muestra el primer archivo de la carpeta seleccionada.

Para obtener una vista previa de un archivo diferente, seleccione el icono de vista previa junto al nombre del archivo que desea inspeccionar.

Cuando termine, seleccione **[!UICONTROL Siguiente]**.

![Página de vista previa de datos del área de trabajo de orígenes.](../../../../images/tutorials/create/dlz/file-detection.png)

Para obtener una guía detallada paso a paso sobre cómo crear un flujo de datos para una fuente de almacenamiento en la nube, consulte el tutorial sobre [creación de un flujo de datos de almacenamiento en la nube para llevar datos a Platform](../../dataflow/batch/cloud-storage.md).

## Recuperar sus credenciales de [!DNL Data Landing Zone]

[!DNL Data Landing Zone] es un origen que viene con su licencia de Adobe Experience Platform Sources. [!DNL Data Landing Zone] utiliza un URI SAS y una autenticación basada en token SAS. Puede recuperar sus credenciales de autenticación desde la página [!UICONTROL Catálogo de fuentes].

Para recuperar sus credenciales, seleccione la tarjeta **[!UICONTROL Zona de aterrizaje de datos]** y copie sus credenciales del carril derecho que aparece.

![Una lista de opciones de vista para la zona de aterrizaje de datos.](../../../../images/tutorials/create/dlz/view-credentials.png)

Aparece una ventana emergente que muestra el nombre del contenedor, el token SAS, el nombre de la cuenta de almacenamiento, el URI SAS y la fecha de caducidad.

## Actualizar sus credenciales de [!DNL Data Landing Zone]

Sus credenciales de [!DNL Data Landing Zone] están configuradas para que caduquen automáticamente pasados 90 días y debe usar nuevas credenciales para volver a conectarse a [!DNL Data Landing Zone] después del vencimiento. Los flujos de datos de Experience Platform no se ven afectados por la caducidad de las credenciales y puede seguir trabajando con los flujos de datos nuevos y existentes con las credenciales nuevas.

Existen dos maneras de actualizar las credenciales de [!DNL Data Landing Zone]:

>[!BEGINTABS]

>[!TAB Usar la tarjeta de origen]

Para actualizar sus credenciales desde la página del catálogo de orígenes, seleccione los puntos suspensivos (**`...`**) en la tarjeta [!DNL Data Landing Zone] y, a continuación, seleccione **[!UICONTROL Actualizar credenciales]**.

![Actualice las credenciales con la tarjeta de origen.](../../../../images/tutorials/create/dlz/refresh-with-card.png)

Aparece una ventana emergente que le solicita confirmación antes de continuar. Cuando esté listo, seleccione **[!UICONTROL Actualizar credenciales]**.

![Ventana de confirmación de credenciales de actualización.](../../../../images/tutorials/create/dlz/confirm.png)

>[!TAB Usar el carril derecho]

Para actualizar las credenciales con el carril derecho, seleccione la tarjeta de origen **[!UICONTROL Zona de aterrizaje de datos]** y, a continuación, seleccione **[!UICONTROL Más acciones]**. A continuación, seleccione **[!UICONTROL Actualizar credenciales]** y confirme el uso de la ventana emergente que aparece.

![Actualice las credenciales con el carril derecho.](../../../../images/tutorials/create/dlz/refresh-with-right-rail.png)

>[!ENDTABS]

## Pasos siguientes

Al seguir este tutorial, ha tenido acceso al contenedor de [!DNL Data Landing Zone] y ha aprendido a recuperar y actualizar las credenciales. Ahora puede continuar con el siguiente tutorial sobre [creación de un flujo de datos para llevar datos de un almacenamiento en la nube a Platform](../../dataflow/batch/cloud-storage.md).
