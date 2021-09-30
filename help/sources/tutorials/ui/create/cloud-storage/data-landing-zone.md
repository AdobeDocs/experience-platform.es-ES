---
keywords: Experience Platform;inicio;temas populares;zona de aterrizaje de datos;zona de aterrizaje de datos
solution: Experience Platform
title: Conexión de la zona de aterrizaje de datos a la plataforma mediante la interfaz de usuario
topic-legacy: overview
type: Tutorial
description: Obtenga información sobre cómo crear un conector de origen de zona de aterrizaje de datos mediante la interfaz de usuario de Platform.
exl-id: 653c9958-5d89-4b0c-af3d-a3e74aa47a08
source-git-commit: ca7197036283ee15dbf60c113d361a5ea34d65c1
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---

# Conectar [!DNL Data Landing Zone] a Platform mediante la interfaz de usuario

[!DNL Data Landing Zone] es una funcionalidad de almacenamiento de datos basada en la nube para el almacenamiento temporal de archivos aprovisionado con Adobe Experience Platform. [!DNL Data Landing Zone] se utiliza únicamente para el ingreso y la salida de sus datos dentro y fuera de Platform. Los datos se eliminan automáticamente del [!DNL Data Landing Zone] después de siete días.

Este tutorial proporciona pasos para crear una conexión de origen [!DNL Data Landing Zone] mediante la interfaz de usuario de Platform.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos de varias fuentes, al mismo tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Simuladores para pruebas](../../../../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

## Traer los archivos de [!DNL Data Landing Zone] a Platform

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Sources]** en el panel de navegación izquierdo para acceder al espacio de trabajo [!UICONTROL Sources]. La pantalla [!UICONTROL Catalog] muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar mediante la barra de búsqueda.

En la categoría [!UICONTROL cloud storage], seleccione [!DNL Data Landing Zone] y, a continuación, **[!UICONTROL Add data]**.

![catálogo](../../../../images/tutorials/create/dlz/catalog.png)

Aparece el paso [!UICONTROL Add data], que proporciona una interfaz para seleccionar y previsualizar los datos que desea traer a Platform.

![add-data](../../../../images/tutorials/create/dlz/add-data.png)

Para obtener una guía detallada y paso a paso sobre cómo crear un flujo de datos para una fuente de almacenamiento en la nube, consulte el tutorial sobre la [creación de un flujo de datos de almacenamiento en la nube para traer datos a Platform](../../dataflow/batch/cloud-storage.md).

## Recupere y actualice sus [!DNL Data Landing Zone] credenciales

[!DNL Data Landing Zone] es una fuente lista para usar que viene con la licencia de fuentes de Adobe Experience Platform. [!DNL Data Landing Zone] utiliza un URI SAS y una autenticación basada en tokens SAS. Puede recuperar y actualizar sus credenciales de autenticación desde la página [!UICONTROL Catálogo de fuentes].

En el [!UICONTROL Catálogo de fuentes], en la categoría [!UICONTROL Cloud storage], seleccione los puntos suspensivos (**...**) de la tarjeta **[!UICONTROL Zona de aterrizaje de datos]**. En el menú desplegable que aparece, seleccione **[!UICONTROL Ver credenciales]**.

![opciones](../../../../images/tutorials/create/dlz/options.png)

Aparece una ventana emergente que muestra el nombre del contenedor, el token SAS, el nombre de la cuenta de almacenamiento y el URI SAS.

Seleccione **[!UICONTROL Actualizar credenciales]** y permita que se procesen las credenciales actualizadas durante unos segundos.

![ver credenciales](../../../../images/tutorials/create/dlz/credentials.png)

## Pasos siguientes

Al seguir este tutorial, ha accedido al contenedor [!DNL Data Landing Zone] y ha aprendido a recuperar y actualizar sus credenciales. Ahora puede continuar con el siguiente tutorial sobre la [creación de un flujo de datos para llevar los datos de un almacenamiento en la nube a Platform](../../dataflow/batch/cloud-storage.md).
