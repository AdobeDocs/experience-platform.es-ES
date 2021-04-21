---
keywords: Experience Platform;inicio;temas populares; analytics;clasificaciones
description: Aprenda a crear un conector de origen de Adobe Analytics en la interfaz de usuario para introducir los datos de las clasificaciones en Adobe Experience Platform.
solution: Experience Platform
title: Crear una conexión de origen de Adobe Analytics para datos de clasificaciones en la interfaz de usuario
topic-legacy: overview
type: Tutorial
exl-id: d606720d-f1ca-47cc-919b-643a8fc61e07
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '631'
ht-degree: 0%

---

# Crear una conexión de origen de Adobe Analytics para los datos de clasificaciones en la interfaz de usuario

Este tutorial proporciona los pasos para crear una conexión de origen de datos de clasificaciones de Adobe Analytics en la interfaz de usuario para introducir los datos de las clasificaciones en Adobe Experience Platform.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual el Experience Platform organiza los datos de experiencia del cliente.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

El conector de datos de clasificaciones de Analytics requiere que los datos se hayan migrado a la nueva [!DNL Classifications] infraestructura de Adobe Analytics antes de su uso. Para confirmar el estado de migración de los datos, póngase en contacto con el administrador de éxito de los clientes de Adobe.

## Seleccionar las clasificaciones

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Sources]** en la barra de navegación izquierda para acceder al espacio de trabajo de orígenes. La pantalla **[!UICONTROL Catalog]** muestra los orígenes disponibles para crear conexiones entrantes con. Cada tarjeta de origen muestra una opción para configurar una nueva cuenta o agregar datos a una cuenta existente.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. Alternativamente, puede encontrar la fuente específica con la que desea trabajar usando la opción de búsqueda.

En la categoría **[!UICONTROL Adobe applications]** , seleccione la tarjeta **[!UICONTROL Adobe Analytics]** y, a continuación, seleccione **[!UICONTROL Add data]** para comenzar a trabajar con los datos de clasificaciones de Analytics.

![](../../../../images/tutorials/create/classifications/catalog.png)

Aparece el paso **[!UICONTROL Analytics source add data]**. Seleccione **[!UICONTROL Classifications]** en el encabezado superior para ver una lista de [!DNL Classifications] conjuntos de datos, que incluye información sobre su ID de dimensión, nombre del grupo de informes e ID del grupo de informes.

Cada página muestra hasta diez conjuntos de datos [!DNL Classifications] diferentes entre los que puede elegir. Seleccione **[!UICONTROL Next]** en la parte inferior de la página para buscar más opciones. El panel de la derecha muestra el número total de [!DNL Classifications] conjuntos de datos que seleccionó, así como sus nombres. Este panel también le permite eliminar cualquier conjunto de datos [!DNL Classifications] que haya seleccionado por error o borrar todas las selecciones con una acción.

Puede seleccionar hasta 30 conjuntos de datos [!DNL Classifications] diferentes para incluirlos en [!DNL Platform].

Una vez que haya seleccionado sus [!DNL Classifications] conjuntos de datos, seleccione **[!UICONTROL Next]** en la parte superior derecha de la página.

![](../../../../images/tutorials/create/classifications/add-data.png)

## Revisar las clasificaciones

Aparece el paso **[!UICONTROL Review]** , que le permite revisar los [!DNL Classifications] conjuntos de datos seleccionados antes de crearlos. Los detalles se agrupan en las siguientes categorías:

* **[!UICONTROL Connection]**: Muestra la plataforma de origen y el estado de la conexión.
* **[!UICONTROL Data type]**: Muestra el número de seleccionados  [!DNL Classifications].
* **[!UICONTROL Scheduling]**: Muestra la frecuencia de sincronización de los  [!DNL Classifications] datos.

Una vez que haya revisado el flujo de datos, haga clic en **[!UICONTROL Finish]** y permita que se cree el flujo de datos.

![](../../../../images/tutorials/create/classifications/review.png)

## Monitorice el flujo de datos de las clasificaciones

Una vez creado el flujo de datos, puede monitorizar los datos que se están incorporando a través de él. En la pantalla **[!UICONTROL Catalog]**, seleccione **[!UICONTROL Dataflows]** para ver una lista de los flujos establecidos asociados a su cuenta [!DNL Classifications].

![](../../../../images/tutorials/create/classifications/dataflows.png)

Aparece la pantalla **[!UICONTROL Dataflows]**. En esta página hay una lista de flujos de datos, que incluye información sobre su nombre, datos de origen y estado de ejecución del flujo de datos. A la derecha, se encuentra el panel **[!UICONTROL Properties]** que contiene metadatos relacionados con su flujo de datos [!DNL Classifications].

Seleccione el **[!UICONTROL Target dataset]** al que desee acceder.

![](../../../../images/tutorials/create/classifications/list-of-dataflows.png)

La página **[!UICONTROL Dataset activity]** muestra información sobre el conjunto de datos de destino seleccionado, incluidos detalles sobre su estado de lote, ID de conjunto de datos y esquema.

>[!IMPORTANT]
>
>Mientras que la eliminación de conjuntos de datos es posible para otros conectores de origen, actualmente no es compatible con el conector de datos de clasificaciones de Analytics. Si elimina un conjunto de datos por error, póngase en contacto con el Servicio de atención al cliente de Adobe.

![](../../../../images/tutorials/create/classifications/dataset.png)


## Pasos siguientes

Siguiendo este tutorial, ha creado un conector de datos de clasificaciones de Analytics que introduce [!DNL Classifications] datos en [!DNL Platform]. Consulte los siguientes documentos para obtener más información sobre los datos [!DNL Analytics] y [!DNL Classifications]:

* [Resumen del conector de datos de Analytics](../../../../connectors/adobe-applications/analytics.md)
* [Creación de una conexión de datos de Analytics en la interfaz de usuario](./analytics.md)
* [Acerca de las clasificaciones](https://experienceleague.adobe.com/docs/analytics/components/classifications/c-classifications.html)
