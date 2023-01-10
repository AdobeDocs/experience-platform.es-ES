---
keywords: Experience Platform;inicio;temas populares; analytics;clasificaciones
description: Aprenda a crear un conector de origen de Adobe Analytics en la interfaz de usuario para introducir los datos de las clasificaciones en Adobe Experience Platform.
solution: Experience Platform
title: Crear una conexión de origen de Adobe Analytics para datos de clasificaciones en la interfaz de usuario
type: Tutorial
exl-id: d606720d-f1ca-47cc-919b-643a8fc61e07
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 6%

---

# Crear una conexión de origen de Adobe Analytics para los datos de clasificaciones en la interfaz de usuario

Este tutorial proporciona los pasos para crear una conexión de origen de datos de clasificaciones de Adobe Analytics en la interfaz de usuario para introducir los datos de las clasificaciones en Adobe Experience Platform.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual el Experience Platform organiza los datos de experiencia del cliente.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

El conector de datos de clasificaciones de Analytics requiere que los datos se hayan migrado al nuevo [!DNL Classifications] infraestructura de Adobe Analytics antes de su uso. Para confirmar el estado de migración de los datos, póngase en contacto con el administrador de éxito de los clientes de Adobe.

## Seleccionar las clasificaciones

Iniciar sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder al espacio de trabajo de orígenes. La variable **[!UICONTROL Catálogo]** muestra los orígenes disponibles para crear conexiones entrantes con. Cada tarjeta de origen muestra una opción para configurar una nueva cuenta o agregar datos a una cuenta existente.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. Alternativamente, puede encontrar la fuente específica con la que desea trabajar usando la opción de búsqueda.

En el **[!UICONTROL aplicaciones de Adobe]** seleccione la categoría **[!UICONTROL Adobe Analytics]** tarjeta y, a continuación, seleccione **[!UICONTROL Añadir datos]** para empezar a trabajar con los datos de clasificaciones de Analytics.

![](../../../../images/tutorials/create/classifications/catalog.png)

La variable **[!UICONTROL Agregar datos de origen de Analytics]** aparece. Select **[!UICONTROL Clasificaciones]** desde el encabezado superior para ver una lista de [!DNL Classifications] conjuntos de datos de , incluida información sobre su ID de dimensión, el nombre del grupo de informes y el ID del grupo de informes.

Cada página muestra hasta diez [!DNL Classifications] conjuntos de datos de los que puede elegir. Select **[!UICONTROL Siguiente]** en la parte inferior de la página para buscar más opciones. El panel de la derecha muestra el número total de [!DNL Classifications] conjuntos de datos seleccionados, así como sus nombres. Este panel también le permite quitar cualquier [!DNL Classifications] los conjuntos de datos que haya seleccionado por error o borre todas las selecciones con una acción.

Puede seleccionar hasta 30 diferentes [!DNL Classifications] conjuntos de datos para importar [!DNL Platform].

Una vez que haya seleccionado la [!DNL Classifications] conjuntos de datos, seleccione **[!UICONTROL Siguiente]** en la parte superior derecha de la página.

![](../../../../images/tutorials/create/classifications/add-data.png)

## Revisar las clasificaciones

La variable **[!UICONTROL Consulte]** , lo que le permite revisar los [!DNL Classifications] conjuntos de datos antes de crearlos. Los detalles se agrupan en las siguientes categorías:

* **[!UICONTROL Conexión]**: Muestra la plataforma de origen y el estado de la conexión.
* **[!UICONTROL Tipo de datos]**: Muestra el número de [!DNL Classifications].
* **[!UICONTROL Programación]**: Muestra la frecuencia de sincronización para [!DNL Classifications] datos.

Una vez que haya revisado el flujo de datos, haga clic en **[!UICONTROL Finalizar]** y permitir que se cree un flujo de datos.

![](../../../../images/tutorials/create/classifications/review.png)

## Monitorice el flujo de datos de las clasificaciones

Una vez creado el flujo de datos, puede monitorizar los datos que se están incorporando a través de él. En el **[!UICONTROL Catálogo]** pantalla, seleccionar **[!UICONTROL Flujos de datos]** para ver una lista de los flujos establecidos asociados con su [!DNL Classifications] cuenta.

![](../../../../images/tutorials/create/classifications/dataflows.png)

La variable **[!UICONTROL Flujos de datos]** se abre. En esta página hay una lista de flujos de datos, que incluye información sobre su nombre, datos de origen y estado de ejecución del flujo de datos. A la derecha, está el **[!UICONTROL Propiedades]** panel que contiene metadatos sobre su [!DNL Classifications] flujo de datos.

Seleccione el **[!UICONTROL Conjunto de datos de Target]** desea acceder a .

![](../../../../images/tutorials/create/classifications/list-of-dataflows.png)

La variable **[!UICONTROL Actividad del conjunto de datos]** muestra información sobre el conjunto de datos de destino que ha seleccionado, incluidos detalles sobre su estado de lote, ID de conjunto de datos y esquema.

>[!IMPORTANT]
>
>Mientras que la eliminación de conjuntos de datos es posible para otros conectores de origen, actualmente no es compatible con el Conector de datos de clasificaciones de Analytics. Si elimina un conjunto de datos por error, póngase en contacto con el Servicio de atención al cliente de Adobe.

![](../../../../images/tutorials/create/classifications/dataset.png)


## Pasos siguientes

Siguiendo este tutorial, ha creado un conector de datos de clasificaciones de Analytics que ofrece [!DNL Classifications] datos en [!DNL Platform]. Consulte los siguientes documentos para obtener más información sobre [!DNL Analytics] y [!DNL Classifications] datos:

* [Resumen del conector de datos de Analytics](../../../../connectors/adobe-applications/analytics.md)
* [Creación de una conexión de datos de Analytics en la interfaz de usuario](./analytics.md)
* [Acerca de las clasificaciones](https://experienceleague.adobe.com/docs/analytics/components/classifications/c-classifications.html?lang=es)
