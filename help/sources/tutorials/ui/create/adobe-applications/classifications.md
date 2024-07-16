---
keywords: Experience Platform;inicio;temas populares; analytics;clasificaciones
description: Obtenga información sobre cómo crear un conector de origen de Adobe Analytics en la interfaz de usuario para introducir datos de clasificaciones en Adobe Experience Platform.
solution: Experience Platform
title: Creación de una conexión de Adobe Analytics Source para datos de clasificaciones en la IU
type: Tutorial
exl-id: d606720d-f1ca-47cc-919b-643a8fc61e07
source-git-commit: fcebef97ba9cc667f80afd55980c5460912a56fb
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 0%

---

# Crear una conexión de origen de Adobe Analytics para datos de clasificaciones en la interfaz de usuario

En este tutorial se proporcionan los pasos para crear una conexión de origen de datos de clasificaciones de Adobe Analytics en la interfaz de usuario para introducir datos de clasificaciones en Adobe Experience Platform.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual el Experience Platform organiza los datos de experiencia del cliente.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md): el Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

El Conector de datos de clasificaciones de Analytics requiere que los datos se hayan migrado a la nueva infraestructura de [!DNL Classifications] de Adobe Analytics antes de su uso. Para confirmar el estado de migración de sus datos, póngase en contacto con el equipo de la cuenta de Adobe.

## Seleccionar las clasificaciones

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder al área de trabajo de fuentes. La pantalla **[!UICONTROL Catálogo]** muestra los orígenes disponibles para crear conexiones entrantes con. Cada tarjeta de origen muestra una opción para configurar una cuenta nueva o agregar datos a una cuenta existente.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. Como alternativa, puede encontrar la fuente específica con la que desea trabajar mediante la opción de búsqueda.

En la categoría **[!UICONTROL aplicaciones de Adobe]**, seleccione la tarjeta **[!UICONTROL Adobe Analytics]** y, a continuación, seleccione **[!UICONTROL Agregar datos]** para empezar a trabajar con los datos de clasificaciones de Analytics.

![](../../../../images/tutorials/create/classifications/catalog.png)

Aparece el paso **[!UICONTROL Agregar datos de origen de Analytics]**. Seleccione **[!UICONTROL Clasificaciones]** del encabezado superior para ver una lista de [!DNL Classifications] conjuntos de datos, incluida información sobre su ID de dimensión, el nombre del grupo de informes y el ID del grupo de informes.

Cada página muestra hasta diez conjuntos de datos de [!DNL Classifications] diferentes entre los que puede elegir. Seleccione **[!UICONTROL Siguiente]** en la parte inferior de la página para buscar más opciones. El panel de la derecha muestra la cantidad total de [!DNL Classifications] conjuntos de datos que seleccionó, así como sus nombres. Este panel también le permite eliminar cualquier conjunto de datos de [!DNL Classifications] que haya seleccionado por error o borrar todas las selecciones con una acción.

Puede seleccionar hasta 30 conjuntos de datos de [!DNL Classifications] diferentes para incluirlos en [!DNL Platform].

Una vez que haya seleccionado sus [!DNL Classifications] conjuntos de datos, seleccione **[!UICONTROL Siguiente]** en la parte superior derecha de la página.

![](../../../../images/tutorials/create/classifications/add-data.png)

## Revise sus clasificaciones

Aparece el paso **[!UICONTROL Revisar]**, que le permite revisar los conjuntos de datos [!DNL Classifications] seleccionados antes de crearlos. Los detalles se agrupan en las siguientes categorías:

* **[!UICONTROL Conexión]**: muestra la plataforma de origen y el estado de la conexión.
* **[!UICONTROL Tipo de datos]**: Muestra el número de [!DNL Classifications] seleccionados.
* **[!UICONTROL Programación]**: Muestra la frecuencia de sincronización de los datos de [!DNL Classifications].

Una vez que haya revisado el flujo de datos, haga clic en **[!UICONTROL Finalizar]** y espere un poco para que se cree el flujo de datos.

![](../../../../images/tutorials/create/classifications/review.png)

## Monitorizar el flujo de datos de clasificaciones

Una vez creado el flujo de datos, puede monitorizar los datos que se están introduciendo a través de él. En la pantalla **[!UICONTROL Catálogo]**, seleccione **[!UICONTROL Flujos de datos]** para ver una lista de los flujos establecidos asociados con su cuenta de [!DNL Classifications].

![](../../../../images/tutorials/create/classifications/dataflows.png)

Aparece la pantalla **[!UICONTROL Flujos de datos]**. En esta página hay una lista de flujos de datos, que incluye información sobre su nombre, los datos de origen y el estado de ejecución del flujo de datos. A la derecha está el panel **[!UICONTROL Propiedades]** que contiene metadatos sobre el flujo de datos [!DNL Classifications].

Seleccione el **[!UICONTROL conjunto de datos de destino]** al que desee acceder.

![](../../../../images/tutorials/create/classifications/list-of-dataflows.png)

La página **[!UICONTROL Actividad del conjunto de datos]** muestra información sobre el conjunto de datos de destino que seleccionó, incluidos detalles sobre su estado por lotes, el ID del conjunto de datos y el esquema.

![](../../../../images/tutorials/create/classifications/dataset.png)

## Pasos siguientes

Siguiendo este tutorial, ha creado un conector de datos de clasificaciones de Analytics que lleva datos de [!DNL Classifications] a [!DNL Platform]. Consulte los siguientes documentos para obtener más información sobre los datos de [!DNL Analytics] y [!DNL Classifications]:

* [Resumen del conector de datos de Analytics](../../../../connectors/adobe-applications/analytics.md)
* [Creación de una conexión de datos de Analytics en la IU](./analytics.md)
* [Acerca de las clasificaciones](https://experienceleague.adobe.com/docs/analytics/components/classifications/c-classifications.html)
