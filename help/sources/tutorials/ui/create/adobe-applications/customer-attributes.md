---
keywords: Experience Platform;inicio;temas populares;atributos del cliente
solution: Experience Platform
title: Crear una conexión de origen de Atributos del cliente en la IU
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen en la interfaz de usuario para incorporar datos de perfil de atributos del cliente a Adobe Experience Platform.
exl-id: 66bdab8f-c00e-4ebe-8b8e-f9e12cf86bbe
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 4%

---

# Crear una conexión de origen de Atributos del cliente en la IU

Este tutorial proporciona los pasos para crear una conexión de origen en la interfaz de usuario para introducir datos de perfil de Atributos del cliente en Adobe Experience Platform. Para obtener más información sobre los Atributos del cliente, consulte la [Información general sobre Atributos del cliente](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/attributes.html?lang=es).

>[!IMPORTANT]
>
>Actualmente, la fuente Atributos del cliente no admite la activación o desactivación de flujos de datos.

## Crear una conexión de origen

>[!NOTE]
>
>Si ya ha establecido una conexión de origen para los datos de perfil de Atributos del cliente, la opción para conectarse con el origen está desactivada.

En la IU de Platform, seleccione **[!UICONTROL Fuentes]** desde la navegación izquierda para acceder a [!UICONTROL Fuentes] workspace. El [!UICONTROL Catálogo] La pantalla muestra una variedad de fuentes con las que puede crear una conexión.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar en la barra de búsqueda.

En el [!UICONTROL aplicaciones de Adobe] categoría, seleccionar **[!UICONTROL Atributos del cliente]** y luego seleccione **[!UICONTROL Añadir datos]**.

![catalogar](../../../../images/tutorials/create/customer-attributes/catalog.png)

### Seleccionar fuente de datos de atributos del cliente

El [!UICONTROL Añadir datos] La pantalla de enumera todas las fuentes de datos disponibles para Atributos del cliente. Solo se puede seleccionar un conjunto de datos por conexión de origen de Atributos del cliente.

>[!NOTE]
>
>Los grupos de campos, los esquemas y los conjuntos de datos se crean de forma predeterminada como parte del aprovisionamiento de flujo. Permanecerán tal cual y tendrá que eliminarlos manualmente, si es necesario.

El origen de atributos del cliente no admite la evolución del esquema. Si se cambia la entrada de esquema de una fuente de datos de atributos del cliente, esto sería incompatible con Platform. Como solución alternativa, puede eliminar un flujo de datos de atributos del cliente existente, junto con su conjunto de datos, esquema y grupo de campos asociados y, a continuación, crear uno nuevo con el esquema y el origen de datos actualizados.

>[!IMPORTANT]
>
>Aunque puede eliminar un flujo de datos de atributos del cliente, su conjunto de datos correspondiente permanecerá incluso después de eliminar el flujo de datos. Consulte la guía de [eliminación de un conjunto de datos](../../../../../catalog/datasets/user-guide.md) para ver los pasos sobre cómo eliminar manualmente un conjunto de datos.

Para crear una nueva conexión, seleccione un origen de datos de la lista y, a continuación, seleccione **[!UICONTROL Siguiente]**.

![add-data](../../../../images/tutorials/create/customer-attributes/add-data.png)

### Proporcionar detalles del flujo de datos

El [!UICONTROL Detalles del flujo de datos] Este paso aparece, lo que le permite proporcionar un nombre y una breve descripción para el flujo de datos. Durante este proceso, también puede configurar las opciones de [!UICONTROL Diagnósticos de error], [!UICONTROL Ingesta parcial], y [!UICONTROL Alertas].

[!UICONTROL Diagnósticos de error] permite generar mensajes de error detallados para cualquier registro erróneo que se produzca en el flujo de datos, mientras que [!UICONTROL Ingesta parcial] permite la ingesta de datos que contienen errores, hasta un determinado umbral que se define manualmente. Consulte la [resumen de ingesta parcial por lotes](../../../../../ingestion/batch-ingestion/partial.md) para obtener más información.

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de fuentes mediante la IU](../../alerts.md).

Cuando haya terminado de proporcionar detalles al flujo de datos, seleccione **[!UICONTROL Siguiente]**.

![data-flow-detail](../../../../images/tutorials/create/customer-attributes/dataflow-detail.png)

### Revisar flujo de datos

El [!UICONTROL Revisar] Este paso aparece, lo que le permite revisar el nuevo flujo de datos antes de crearlo. Los detalles se agrupan en las siguientes categorías:

* **[!UICONTROL Conexión]**: Muestra el tipo de origen, la ruta relevante del archivo de origen elegido y el número de columnas dentro de ese archivo de origen.
* **[!UICONTROL Asignar campos de conjunto de datos y asignación]**: Muestra en qué conjunto de datos se están ingiriendo los datos de origen, incluido el esquema al que se adhiere el conjunto de datos.

![reseña](../../../../images/tutorials/create/customer-attributes/review.png)

## Pasos siguientes

Una vez creada la conexión, se crea automáticamente un esquema de destinatario y un conjunto de datos para contener los datos entrantes. Cuando se completa la ingesta inicial, los datos de perfil de los atributos del cliente se pueden utilizar en servicios de Platform secundarios como [!DNL Real-Time Customer Profile] y [!DNL Segmentation Service]. Consulte los siguientes documentos para obtener más información:

* [Información general del [!DNL Real-Time Customer Profile]](../../../../../profile/home.md)
* [Información general del [!DNL Segmentation Service]](../../../../../segmentation/home.md)
