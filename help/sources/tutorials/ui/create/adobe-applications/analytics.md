---
keywords: Experience Platform;inicio;temas populares;Conector de origen de Analytics;Conector de Analytics;Fuente de Analytics;Analytics
solution: Experience Platform
title: Crear una conexión de origen de Adobe Analytics en la interfaz de usuario
topic-legacy: overview
type: Tutorial
description: Aprenda a crear una conexión de origen de Adobe Analytics en la interfaz de usuario para introducir los datos de los consumidores en Adobe Experience Platform.
exl-id: 5ddbaf63-feaa-44f5-b2f2-2d5ae507f423
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 2%

---

# Crear una conexión de origen de Adobe Analytics en la interfaz de usuario

Este tutorial proporciona los pasos para crear una conexión de origen de Adobe Analytics en la interfaz de usuario para introducir los datos de los consumidores en Adobe Experience Platform.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Sistema del Modelo de datos de experiencia (XDM)](../../../../../xdm/home.md): El marco estandarizado mediante el cual el Experience Platform organiza los datos de experiencia del cliente.
* [Perfil](../../../../../profile/home.md) del cliente en tiempo real: Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.
* [Simuladores para pruebas](../../../../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

## Crear una conexión de origen con Adobe Analytics

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Sources]** en la barra de navegación izquierda para acceder al espacio de trabajo de orígenes. La pantalla **Catalog** muestra los orígenes disponibles para crear conexiones entrantes con y cada origen muestra el número de cuentas existentes y los flujos de conjuntos de datos asociados a ellas.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. Alternativamente, puede encontrar la fuente específica con la que desea trabajar usando la opción de búsqueda.

En la categoría **[!UICONTROL Adobe applications]** , seleccione **[!UICONTROL Adobe Analytics]** para mostrar una barra de información en el lado derecho de la pantalla. La barra de información proporciona una breve descripción del origen seleccionado, así como opciones para conectarse con el origen o ver su documentación. Para ver las cuentas existentes, seleccione **[!UICONTROL Accounts]**.

![](../../../../images/tutorials/create/analytics/catalog.png)

### Seleccionar datos

Aparece el paso **[!UICONTROL Adobe Analytics]**. Los flujos de conjuntos de datos establecidos anteriormente para Analytics se muestran en esta pantalla. Puede crear un nuevo flujo de conjuntos de datos haciendo clic en **[!UICONTROL Select data]**.

>[!NOTE]
>
>Se pueden realizar varias conexiones entrantes a un origen para introducir datos diferentes.

![](../../../../images/tutorials/create/analytics/dataset-flows.png)

<!---Analytics report suites can be configured for one sandbox at a time. To import the same report suite into a different sandbox, the dataset flow will have to be deleted and instantiated again via configuration for a different sandbox.--->

En la lista de grupos de informes disponibles, seleccione el que desee incluir en Platform y haga clic en **[!UICONTROL Next]**.

![](../../../../images/tutorials/create/analytics/select-data.png)

### Asigne un nombre al flujo de conjuntos de datos

Aparece el paso **[!UICONTROL Dataset flow detail]**, donde debe proporcionar un nombre y una descripción opcional para el flujo del conjunto de datos. Seleccione **[!UICONTROL Next]** cuando haya terminado.

![](../../../../images/tutorials/create/analytics/dataset-flow-detail.png)

### Revisar el flujo del conjunto de datos

Aparece el paso **[!UICONTROL Review]**, que le permite revisar el nuevo flujo de conjuntos de datos enlazados de Analytics antes de crearlo. Los detalles de la conexión se agrupan por categorías, entre ellas:

* **[!UICONTROL Connection]**: Muestra el tipo de conexión de origen y el grupo de informes seleccionado.
* **[!UICONTROL Assign dataset & map fields]**: Al crear otros conectores de origen, este contenedor muestra en qué conjunto de datos se incorporan los datos de origen, incluido el esquema al que se adhiere el conjunto de datos. El esquema de salida y el conjunto de datos se configuran automáticamente para los flujos de conjuntos de datos de Analytics.

![](../../../../images/tutorials/create/analytics/review.png)

### Monitorización del flujo de conjuntos de datos

Una vez creado el flujo del conjunto de datos, puede monitorizar los datos que se están incorporando a través de él. En la pantalla **[!UICONTROL Catalog]**, seleccione **[!UICONTROL Dataset flows]** para ver una lista de los flujos establecidos asociados a su cuenta de Analytics.

![](../../../../images/tutorials/create/analytics/catalog-dataset-flows.png)

Aparece la pantalla **Dataset flows**. En esta página hay un par de flujos de conjuntos de datos, incluida información sobre su nombre, datos de origen, tiempo de creación y estado.

El conector crea una instancia de dos flujos de conjuntos de datos. Un flujo representa los datos de relleno y el otro es para los datos activos. Los datos de relleno no están configurados para Perfil, pero se envían al lago de datos para casos analíticos y de ciencia de datos.

Para obtener más información sobre el relleno, los datos activos y sus latencias respectivas, consulte la [información general del conector de datos de Analytics](../../../../connectors/adobe-applications/analytics.md).

Seleccione el flujo del conjunto de datos que desee ver en la lista.

![](../../../../images/tutorials/create/analytics/backfill.png)

Aparece la página **Actividad del conjunto de datos**. Esta página muestra la tasa de consumo de los mensajes en forma de gráfico. Seleccione *Control de datos* en el encabezado superior para acceder a los campos de etiquetado.

![](../../../../images/tutorials/create/analytics/batches.png)

Puede ver las etiquetas heredadas de un flujo de conjuntos de datos desde la pantalla *Control de datos*. Para acceder a etiquetas específicas, seleccione el botón de edición en la parte superior derecha.

![](../../../../images/tutorials/create/analytics/data-gov.png)

Aparece el panel **Editar etiquetas de control**. Esta pantalla le permite acceder y editar el contrato, la identidad y las etiquetas confidenciales de un flujo de datos.

Para obtener más información sobre cómo etiquetar datos procedentes de Analytics, visite la [guía de etiquetas de uso de datos](../../../../../data-governance/labels/user-guide.md).

![](../../../../images/tutorials/create/analytics/labels.png)

## Pasos siguientes y recursos adicionales

Una vez creada la conexión, se crea automáticamente un esquema de destino y un flujo de conjunto de datos para contener los datos entrantes. Además, se rellenan los datos de forma retroactiva y se introducen hasta 13 meses de datos históricos. Cuando se complete la introducción inicial, los datos de Analytics y se utilizarán en servicios de Platform descendentes, como Perfil del cliente en tiempo real y Servicio de segmentación. Consulte los siguientes documentos para obtener más información:

* [Resumen del perfil del cliente en tiempo real](../../../../../profile/home.md)
* [Información general del servicio de segmentación](../../../../../segmentation/home.md)
* [Información general de Data Science Workspace](../../../../../data-science-workspace/home.md)
* [Información general del servicio de consultas](../../../../../query-service/home.md)

El siguiente vídeo pretende comprender la ingesta de datos mediante el conector de origen de Adobe Analytics:

>[!WARNING]
>
> La interfaz de usuario [!DNL Platform] que se muestra en el siguiente vídeo no está actualizada. Consulte la documentación anterior para obtener las últimas capturas de pantalla y funciones de la interfaz de usuario.

>[!VIDEO](https://video.tv.adobe.com/v/29687?quality=12&learn=on)
