---
keywords: Experience Platform;inicio;temas populares; analytics;clasificaciones
description: Obtenga información sobre cómo crear un conector de origen de Adobe Analytics en la interfaz de usuario para introducir datos de clasificaciones en Adobe Experience Platform.
solution: Experience Platform
title: Creación de una conexión de origen de Adobe Analytics para datos de clasificaciones en la IU
type: Tutorial
exl-id: d606720d-f1ca-47cc-919b-643a8fc61e07
source-git-commit: fcebef97ba9cc667f80afd55980c5460912a56fb
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 2%

---

# Crear una conexión de origen de Adobe Analytics para datos de clasificaciones en la interfaz de usuario

En este tutorial se proporcionan los pasos para crear una conexión de origen de datos de clasificaciones de Adobe Analytics en la interfaz de usuario para introducir datos de clasificaciones en Adobe Experience Platform.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md): El Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

El Conector de datos de clasificaciones de Analytics requiere que los datos se hayan migrado al nuevo [!DNL Classifications] de Adobe Analytics antes de su uso. Para confirmar el estado de migración de sus datos, póngase en contacto con el equipo de la cuenta de Adobe.

## Seleccionar las clasificaciones

Iniciar sesión en [Adobe Experience Platform](https://platform.adobe.com) y luego seleccione **[!UICONTROL Fuentes]** desde la barra de navegación izquierda para acceder al espacio de trabajo de orígenes. El **[!UICONTROL Catálogo]** La pantalla de muestra las fuentes disponibles para crear conexiones entrantes con. Cada tarjeta de origen muestra una opción para configurar una cuenta nueva o agregar datos a una cuenta existente.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. Como alternativa, puede encontrar la fuente específica con la que desea trabajar mediante la opción de búsqueda.

En el **[!UICONTROL aplicaciones de Adobe]** categoría, seleccione la **[!UICONTROL Adobe Analytics]** y seleccione. **[!UICONTROL Añadir datos]** para empezar a trabajar con los datos de clasificaciones de Analytics.

![](../../../../images/tutorials/create/classifications/catalog.png)

El **[!UICONTROL Añadir datos de origen de Analytics]** aparece el paso. Seleccionar **[!UICONTROL Clasificaciones]** desde el encabezado superior para ver una lista de [!DNL Classifications] conjuntos de datos, incluida información sobre su ID de dimensión, nombre del grupo de informes e ID del grupo de informes.

Cada página muestra hasta diez páginas diferentes [!DNL Classifications] conjuntos de datos entre los que puede elegir. Seleccionar **[!UICONTROL Siguiente]** en la parte inferior de la página para buscar más opciones. El panel de la derecha muestra la cantidad total de [!DNL Classifications] conjuntos de datos que ha seleccionado, así como sus nombres. Este panel también le permite eliminar cualquier [!DNL Classifications] conjuntos de datos que puede haber seleccionado por error o borrar todas las selecciones con una acción.

Puede seleccionar hasta 30 opciones diferentes [!DNL Classifications] conjuntos de datos para incorporar a [!DNL Platform].

Una vez que haya seleccionado su [!DNL Classifications] conjuntos de datos, seleccione **[!UICONTROL Siguiente]** en la parte superior derecha de la página.

![](../../../../images/tutorials/create/classifications/add-data.png)

## Revise sus clasificaciones

El **[!UICONTROL Revisar]** Este paso aparece, lo que le permite revisar la [!DNL Classifications] conjuntos de datos antes de crearse. Los detalles se agrupan en las siguientes categorías:

* **[!UICONTROL Conexión]**: Muestra la plataforma de origen y el estado de la conexión.
* **[!UICONTROL Tipo de datos]**: Muestra el número de seleccionados [!DNL Classifications].
* **[!UICONTROL Programación]**: Muestra la frecuencia de sincronización para [!DNL Classifications] datos.

Una vez revisado el flujo de datos, haga clic en **[!UICONTROL Finalizar]** y deje pasar un tiempo para crear el flujo de datos.

![](../../../../images/tutorials/create/classifications/review.png)

## Monitorizar el flujo de datos de clasificaciones

Una vez creado el flujo de datos, puede monitorizar los datos que se están introduciendo a través de él. Desde el **[!UICONTROL Catálogo]** pantalla, seleccione **[!UICONTROL Flujos de datos]** para ver una lista de los flujos establecidos asociados a su [!DNL Classifications] cuenta.

![](../../../../images/tutorials/create/classifications/dataflows.png)

El **[!UICONTROL Flujos de datos]** aparece la pantalla. En esta página hay una lista de flujos de datos, que incluye información sobre su nombre, los datos de origen y el estado de ejecución del flujo de datos. A la derecha, está la **[!UICONTROL Propiedades]** panel que contiene metadatos sobre su [!DNL Classifications] flujo de datos.

Seleccione el **[!UICONTROL Conjunto de datos de Target]** desea acceder a.

![](../../../../images/tutorials/create/classifications/list-of-dataflows.png)

El **[!UICONTROL Actividad de conjunto de datos]** Esta página muestra información sobre el conjunto de datos de destino seleccionado, incluidos detalles sobre su estado del lote, ID del conjunto de datos y esquema.

![](../../../../images/tutorials/create/classifications/dataset.png)

## Pasos siguientes

Al seguir este tutorial, ha creado un conector de datos de clasificaciones de Analytics que trae lo siguiente [!DNL Classifications] datos en [!DNL Platform]. Consulte los siguientes documentos para obtener más información sobre [!DNL Analytics] y [!DNL Classifications] datos:

* [Resumen del conector de datos de Analytics](../../../../connectors/adobe-applications/analytics.md)
* [Creación de una conexión de datos de Analytics en la IU](./analytics.md)
* [Acerca de las clasificaciones](https://experienceleague.adobe.com/docs/analytics/components/classifications/c-classifications.html?lang=es)
