---
keywords: Experience Platform;inicio;temas populares;atributos del cliente
solution: Experience Platform
title: Creación de una conexión de Source de Atributos del cliente en la IU
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen en la interfaz de usuario para incorporar datos de perfil de atributos del cliente a Adobe Experience Platform.
exl-id: 66bdab8f-c00e-4ebe-8b8e-f9e12cf86bbe
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 1%

---

# Crear una conexión de origen de Atributos del cliente en la IU

Este tutorial proporciona los pasos para crear una conexión de origen en la interfaz de usuario para introducir datos de perfil de Atributos del cliente en Adobe Experience Platform. Para obtener más información sobre los Atributos del cliente, consulte la [descripción general de los Atributos del cliente](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/attributes.html?lang=es).

>[!IMPORTANT]
>
>Actualmente, la fuente Atributos del cliente no admite la activación o desactivación de flujos de datos.

## Crear una conexión de origen

>[!NOTE]
>
>Si ya ha establecido una conexión de origen para los datos de perfil de Atributos del cliente, la opción para conectarse con el origen está desactivada.

En la interfaz de usuario de Experience Platform, seleccione **[!UICONTROL Fuentes]** en el panel de navegación izquierdo para acceder al área de trabajo [!UICONTROL Fuentes]. La pantalla [!UICONTROL Catálogo] muestra una variedad de orígenes con los que puede crear una conexión.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar en la barra de búsqueda.

En la categoría [!UICONTROL aplicaciones de Adobe], seleccione **[!UICONTROL Atributos del cliente]** y, a continuación, seleccione **[!UICONTROL Agregar datos]**.

![catálogo](../../../../images/tutorials/create/customer-attributes/catalog.png)

### Seleccionar fuente de datos de atributos del cliente

La pantalla [!UICONTROL Agregar datos] enumera todas las fuentes de datos disponibles para los Atributos del cliente. Solo se puede seleccionar un conjunto de datos por conexión de origen de Atributos del cliente.

>[!NOTE]
>
>Los grupos de campos, los esquemas y los conjuntos de datos se crean de forma predeterminada como parte del aprovisionamiento de flujo. Permanecerán tal cual y tendrá que eliminarlos manualmente, si es necesario.

El origen de atributos del cliente no admite la evolución del esquema. Si se cambia la entrada de esquema de una fuente de datos de atributos del cliente, esto sería incompatible con Experience Platform. Como solución alternativa, puede eliminar un flujo de datos de atributos del cliente existente, junto con su conjunto de datos, esquema y grupo de campos asociados y, a continuación, crear uno nuevo con el esquema y el origen de datos actualizados.

>[!IMPORTANT]
>
>Aunque puede eliminar un flujo de datos de atributos del cliente, su conjunto de datos correspondiente permanecerá incluso después de eliminar el flujo de datos. Consulte la guía sobre [eliminación de un conjunto de datos](../../../../../catalog/datasets/user-guide.md) para ver los pasos sobre cómo eliminar manualmente un conjunto de datos.

Para crear una nueva conexión, seleccione un origen de datos en la lista y, a continuación, seleccione **[!UICONTROL Siguiente]**.

![add-data](../../../../images/tutorials/create/customer-attributes/add-data.png)

### Proporcionar detalles del flujo de datos

Aparece el paso [!UICONTROL Detalle del flujo de datos], que le permite proporcionar un nombre y una breve descripción para el flujo de datos. Durante este proceso, también puede configurar las opciones de [!UICONTROL Diagnóstico de errores], [!UICONTROL Ingesta parcial] y [!UICONTROL Alertas].

[!UICONTROL Diagnósticos de error] permite la generación detallada de mensajes de error para cualquier registro erróneo que ocurra en su flujo de datos, mientras que [!UICONTROL Ingesta parcial] le permite ingerir datos que contengan errores, hasta un determinado umbral que usted defina manualmente. Consulte la [descripción general de la ingesta parcial por lotes](../../../../../ingestion/batch-ingestion/partial.md) para obtener más información.

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de fuentes mediante la interfaz de usuario](../../alerts.md).

Cuando termine de proporcionar detalles al flujo de datos, seleccione **[!UICONTROL Siguiente]**.

![detalle de flujo de datos](../../../../images/tutorials/create/customer-attributes/dataflow-detail.png)

### Revisar flujo de datos

Aparece el paso [!UICONTROL Revisar], que le permite revisar el nuevo flujo de datos antes de crearlo. Los detalles se agrupan en las siguientes categorías:

* **[!UICONTROL Conexión]**: muestra el tipo de origen, la ruta de acceso relevante del archivo de origen elegido y el número de columnas dentro de ese archivo de origen.
* **[!UICONTROL Asignar campos de conjunto de datos y asignación]**: muestra en qué conjunto de datos se están ingiriendo los datos de origen, incluido el esquema al que se adhiere el conjunto de datos.

![revisión](../../../../images/tutorials/create/customer-attributes/review.png)

## Pasos siguientes

Una vez creada la conexión, se crea automáticamente un esquema de destino y un conjunto de datos para contener los datos entrantes. Cuando se completa la ingesta inicial, los servicios de Experience Platform descendentes como [!DNL Real-Time Customer Profile] y [!DNL Segmentation Service] pueden usar los datos de perfil de atributos del cliente. Consulte los siguientes documentos para obtener más información:

* [Información general de [!DNL Real-Time Customer Profile]](../../../../../profile/home.md)
* [Información general de [!DNL Segmentation Service]](../../../../../segmentation/home.md)
