---
keywords: Experience Platform;inicio;temas populares;atributos del cliente
solution: Experience Platform
title: Creación de una conexión de origen de atributos del cliente en la interfaz de usuario
topic: sobre validación
type: Tutorial
description: Aprenda a crear una conexión de origen en la interfaz de usuario para recopilar datos de perfil de atributos del cliente en Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 08a3026e969a8739a8b57226c35a6d1d3150006e
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 6%

---


# Creación de una conexión de origen de Atributos del cliente en la interfaz de usuario

Este tutorial proporciona los pasos para crear una conexión de origen en la interfaz de usuario para recopilar datos de perfil de Atributos del cliente en Adobe Experience Platform. Para obtener más información sobre Atributos del cliente, consulte la [información general sobre Atributos del cliente](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/attributes.html).

>[!IMPORTANT]
>
>Actualmente, las funcionalidades de los flujos de datos deshabilitar, habilitar y eliminar no son compatibles con la fuente de Atributos del cliente.

## Crear una conexión de origen

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Sources]** en el panel de navegación izquierdo para acceder al espacio de trabajo [!UICONTROL Sources]. La pantalla [!UICONTROL Catalog] muestra una variedad de fuentes con las que puede crear una conexión.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar mediante la barra de búsqueda.

En la categoría [!UICONTROL Adobe applications], seleccione **[!UICONTROL Customer Attributes]** y luego seleccione **[!UICONTROL Add data]**.

>[!NOTE]
>
>Si ya ha establecido una conexión de origen para los datos de perfil de Atributos del cliente, se desactiva la opción de conectarse con el origen.

![](../../../../images/tutorials/create/customer-attributes/catalog.png)

La pantalla [!UICONTROL Add data] enumera todas las fuentes de datos disponibles para los Atributos del cliente. Para crear una nueva conexión, seleccione un origen de datos de la lista y, a continuación, seleccione **[!UICONTROL Next]**.

>[!NOTE]
>
>Solo se puede seleccionar un conjunto de datos por conexión de origen de Atributos del cliente.

![](../../../../images/tutorials/create/customer-attributes/add-data.png)

Aparece el paso [!UICONTROL Dataflow detail], que le permite asignar un nombre al nuevo flujo de datos y proporcionarle una breve descripción.

Durante este proceso, también puede habilitar [!UICONTROL Partial ingestion] y [!UICONTROL Error diagnostics]. [!UICONTROL Partial ingestion] proporciona la capacidad de ingerir datos que contengan errores, hasta un umbral determinado que se pueda establecer, mientras que  [!UICONTROL Error diagnostics] proporciona detalles sobre cualquier dato incorrecto que se haya enviado por lotes por separado. Para obtener más información, consulte la [información general sobre la ingesta parcial de lotes](../../../../../ingestion/batch-ingestion/partial.md).

![](../../../../images/tutorials/create/customer-attributes/dataflow-detail.png)

Aparece el paso [!UICONTROL Review], que le permite revisar el nuevo flujo de datos antes de crearlo. Los detalles se agrupan en las siguientes categorías:

* **[!UICONTROL Connection]**: Muestra el tipo de origen, la ruta correspondiente del archivo de origen elegido y el número de columnas dentro de ese archivo de origen.
* **[!UICONTROL Assign dataset & map fields]**: Muestra en qué conjunto de datos se están incorporando los datos de origen, incluido el esquema al que se adhiere el conjunto de datos.

![](../../../../images/tutorials/create/customer-attributes/review.png)

## Pasos siguientes

Una vez creada la conexión, se crea automáticamente un esquema de destinatario y un conjunto de datos para contener los datos entrantes. Cuando se completa la ingesta inicial, los datos de perfil de atributos del cliente pueden ser utilizados por servicios de Platform descendentes como [!DNL Real-time Customer Profile] y [!DNL Segmentation Service]. Consulte los siguientes documentos para obtener más información:

* Información general del [[!DNL Real-time Customer Profile] ](../../../../../profile/home.md)
* Información general del [[!DNL Segmentation Service] ](../../../../../segmentation/home.md)
