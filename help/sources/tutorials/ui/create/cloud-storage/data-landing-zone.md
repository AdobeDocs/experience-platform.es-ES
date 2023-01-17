---
keywords: Experience Platform;inicio;temas populares;zona de aterrizaje de datos;zona de aterrizaje de datos
title: Conexión de la zona de aterrizaje de datos a la plataforma mediante la interfaz de usuario
description: Obtenga información sobre cómo crear un conector de origen de zona de aterrizaje de datos mediante la interfaz de usuario de Platform.
exl-id: 653c9958-5d89-4b0c-af3d-a3e74aa47a08
source-git-commit: d57060ddeed64d3863f71ac1ea34ccc5c97265ea
workflow-type: tm+mt
source-wordcount: '631'
ht-degree: 0%

---

# Connect [!DNL Data Landing Zone] a Platform mediante la interfaz de usuario

>[!IMPORTANT]
>
>Esta página es específica para la variable [!DNL Data Landing Zone] *source* en el Experience Platform. Para obtener información sobre la conexión a la variable [!DNL Data Landing Zone] *destino* conector, consulte [[!DNL Data Landing Zone] página de documentación de destino](/help/destinations/catalog/cloud-storage/data-landing-zone.md).

[!DNL Data Landing Zone] es un servicio de almacenamiento de archivos seguro y basado en la nube para incorporar archivos a Adobe Experience Platform. Los datos se eliminan automáticamente del [!DNL Data Landing Zone] después de siete días.

Este tutorial proporciona los pasos para crear un [!DNL Data Landing Zone] conexión de origen mediante la interfaz de usuario de Platform.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos de varias fuentes, al mismo tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

## Traiga los archivos de [!DNL Data Landing Zone] a Platform

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Fuentes]** desde el panel de navegación izquierdo para acceder a la [!UICONTROL Fuentes] espacio de trabajo. La variable [!UICONTROL Catálogo] muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar mediante la barra de búsqueda.

En el [!UICONTROL almacenamiento en la nube] categoría, seleccione [!DNL Data Landing Zone] y, a continuación, seleccione **[!UICONTROL Añadir datos]**.

![catálogo](../../../../images/tutorials/create/dlz/catalog.png)

La variable [!UICONTROL Añadir datos] aparece, proporcionando una interfaz para seleccionar y previsualizar los datos que desea traer a Platform.

* La parte izquierda de la interfaz es un explorador de carpetas, que le proporciona una lista de archivos del contenedor que puede traer a Platform.
* La parte derecha de la interfaz permite previsualizar hasta 100 filas de datos de un archivo compatible.

Seleccione el archivo que desea traer a Platform y permita que la interfaz correcta se actualice en una pantalla de vista previa durante unos momentos.

![add-data](../../../../images/tutorials/create/dlz/add-data.png)

>[!TIP]
>
>Platform detecta automáticamente la información de propiedad del archivo seleccionado, incluida la información sobre el formato de datos del archivo, el delimitador de columnas designado y el tipo de compresión.

La interfaz de vista previa permite inspeccionar el contenido y la estructura de un archivo. De forma predeterminada, la interfaz de vista previa muestra el primer archivo de la carpeta seleccionada.

Para obtener una vista previa de un archivo diferente, seleccione el icono de vista previa junto al nombre del archivo que desea inspeccionar.

Cuando termine, seleccione **[!UICONTROL Siguiente]**.

![detección de archivos](../../../../images/tutorials/create/dlz/file-detection.png)

Para obtener una guía detallada y paso a paso sobre cómo crear un flujo de datos para un origen de almacenamiento en la nube, consulte el tutorial sobre [crear un flujo de datos de almacenamiento en la nube para traer datos a Platform](../../dataflow/batch/cloud-storage.md).

## Recupere y actualice su [!DNL Data Landing Zone] credenciales

[!DNL Data Landing Zone] es una fuente lista para usar que viene con la licencia de fuentes de Adobe Experience Platform. [!DNL Data Landing Zone] utiliza un URI SAS y una autenticación basada en tokens SAS. Puede recuperar y actualizar sus credenciales de autenticación desde el [!UICONTROL Catálogo de fuentes] página.

En el [!UICONTROL Catálogo de fuentes], en la sección [!UICONTROL Almacenamiento en la nube] , seleccione los puntos suspensivos (**...**) de **[!UICONTROL Zona de aterrizaje de datos]** tarjeta. En el menú desplegable que aparece, seleccione **[!UICONTROL Ver credenciales]**.

![opciones](../../../../images/tutorials/create/dlz/options.png)

Aparece una ventana emergente que muestra el nombre del contenedor, el token SAS, el nombre de la cuenta de almacenamiento y el URI SAS.

Select **[!UICONTROL Actualizar credenciales]** y permitir que se procesen las credenciales actualizadas durante unos segundos.

>[!TIP]
>
>Su [!DNL Data Landing Zone] las credenciales están configuradas para caducar automáticamente después de 90 días y debe utilizar nuevas credenciales para volver a conectarse a [!DNL Data Landing Zone] después de la caducidad. Los flujos de datos en Platform no se ven afectados por la caducidad de las credenciales y aún puede seguir trabajando con flujos de datos nuevos y existentes con sus nuevas credenciales.

![ver credenciales](../../../../images/tutorials/create/dlz/credentials.png)

## Pasos siguientes

Al seguir este tutorial, ha accedido a su [!DNL Data Landing Zone] y aprendió a recuperar y actualizar sus credenciales. Ahora puede continuar con el siguiente tutorial en [crear un flujo de datos para traer datos de un almacenamiento en la nube a Platform](../../dataflow/batch/cloud-storage.md).
