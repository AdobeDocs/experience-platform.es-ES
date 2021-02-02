---
keywords: Experience Platform;inicio;temas populares; análisis;clasificaciones
description: Este tutorial proporciona los pasos para crear un conector de datos de clasificaciones de Adobe Analytics en la interfaz de usuario para incluir datos de clasificaciones en Adobe Experience Platform.
solution: Experience Platform
title: Creación de un conector de datos de clasificaciones de Adobe Analytics en la interfaz de usuario
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: 2dbd92efbd992b70f4f750b09e9d2e0626e71315
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 0%

---


# Creación de un conector de datos de clasificaciones de Adobe Analytics en la interfaz de usuario

Este tutorial proporciona los pasos para crear un conector de datos de clasificaciones de Adobe Analytics en la interfaz de usuario para incluir datos de clasificaciones en Adobe Experience Platform.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El esquema estandarizado por el cual el Experience Platform organiza los datos de experiencia del cliente.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md):: Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Plataforma en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

El conector de datos de clasificaciones de Analytics requiere que los datos se hayan migrado a la nueva [!DNL Classifications] infraestructura de Adobe Analytics antes de su uso. Para confirmar el estado de migración de sus datos, póngase en contacto con el administrador de éxito de clientes de Adobe.

## Seleccione las clasificaciones

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder al espacio de trabajo de orígenes. La pantalla **[!UICONTROL Catálogo]** muestra los orígenes disponibles para crear conexiones de entrada con. Cada tarjeta de origen muestra una opción para configurar una cuenta nueva o agregar datos a una cuenta existente.

Puede seleccionar la categoría adecuada en el catálogo a la izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar mediante la opción de búsqueda.

En la categoría **[!UICONTROL aplicaciones de Adobe]**, seleccione la tarjeta **[!UICONTROL Adobe Analytics]** y, a continuación, seleccione **[!UICONTROL Añadir datos]** en inicio para trabajar con datos de clasificaciones de Analytics.

![](../../../../images/tutorials/create/classifications/catalog.png)

Aparece el paso **[!UICONTROL Agregar datos de origen de Analytics]**. Seleccione **[!UICONTROL Clasificaciones]** en el encabezado superior para ver una lista de [!DNL Classifications] conjuntos de datos, incluida la información sobre su ID de dimensión, el nombre del grupo de informes y la ID del grupo de informes.

Cada página muestra hasta diez [!DNL Classifications] conjuntos de datos diferentes que puede elegir. Seleccione **[!UICONTROL Siguiente]** en la parte inferior de la página para buscar más opciones. El panel de la derecha muestra el número total de [!DNL Classifications] conjuntos de datos seleccionados, así como sus nombres. Este panel también le permite eliminar cualquier [!DNL Classifications] conjunto de datos que haya seleccionado por error o borrar todas las selecciones con una sola acción.

Puede seleccionar hasta 30 conjuntos de datos [!DNL Classifications] diferentes para incluirlos en [!DNL Platform].

Una vez que haya seleccionado los [!DNL Classifications] conjuntos de datos, seleccione **[!UICONTROL Siguiente]** en la parte superior derecha de la página.

![](../../../../images/tutorials/create/classifications/add-data.png)

## Revisar las clasificaciones

Aparece el paso **[!UICONTROL Revisar]**, que le permite revisar los [!DNL Classifications] conjuntos de datos seleccionados antes de crearlos. Los detalles se agrupan en las siguientes categorías:

* **[!UICONTROL Conexión]**: Muestra la plataforma de origen y el estado de la conexión.
* **[!UICONTROL Tipo]** de datos: Muestra el número de seleccionados  [!DNL Classifications].
* **[!UICONTROL Programación]**: Muestra la frecuencia de sincronización para  [!DNL Classifications] los datos.

Una vez que haya revisado el flujo de datos, haga clic en **[!UICONTROL Finalizar]** y permita que se cree el flujo de datos.

![](../../../../images/tutorials/create/classifications/review.png)

## Monitorear el flujo de datos de las clasificaciones

Una vez creado el flujo de datos, puede monitorear los datos que se están ingeriendo a través de él. En la pantalla **[!UICONTROL Catálogo]**, seleccione **[!UICONTROL Flujos de datos]** para vista de una lista de flujos establecidos asociados con su cuenta [!DNL Classifications].

![](../../../../images/tutorials/create/classifications/dataflows.png)

Aparece la pantalla **[!UICONTROL Flujos de datos]**. En esta página hay una lista de flujos de datos, que incluye información sobre su nombre, datos de origen y estado de ejecución de flujo de datos. A la derecha se encuentra el panel **[!UICONTROL Propiedades]** que contiene metadatos relativos al flujo de datos [!DNL Classifications].

Seleccione el **[!UICONTROL conjunto de datos de Destinatario]** al que desee acceder.

![](../../../../images/tutorials/create/classifications/list-of-dataflows.png)

La página **[!UICONTROL actividad del conjunto de datos]** muestra información sobre el conjunto de datos del destinatario seleccionado, incluidos detalles sobre el estado del lote, la ID del conjunto de datos y el esquema.

>[!IMPORTANT]
>
>Aunque es posible eliminar conjuntos de datos para otros conectores de origen, no se admite actualmente en el conector de datos de clasificaciones de Analytics. Si elimina un conjunto de datos por error, póngase en contacto con el Servicio de atención al cliente de Adobe.

![](../../../../images/tutorials/create/classifications/dataset.png)


## Pasos siguientes

Siguiendo este tutorial, ha creado un conector de datos de clasificaciones de Analytics que lleva [!DNL Classifications] datos a [!DNL Platform]. Consulte los siguientes documentos para obtener más información sobre los datos [!DNL Analytics] y [!DNL Classifications]:

* [Descripción general del conector de datos de Analytics](../../../../connectors/adobe-applications/analytics.md)
* [Creación de un conector de datos de Analytics en la interfaz de usuario](./analytics.md)
* [Acerca de las clasificaciones](https://experienceleague.adobe.com/docs/analytics/components/classifications/c-classifications.html)