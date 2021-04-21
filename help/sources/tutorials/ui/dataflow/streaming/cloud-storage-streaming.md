---
keywords: Experience Platform;inicio;temas populares;conector de almacenamiento en la nube;almacenamiento en la nube
solution: Experience Platform
title: Configurar un flujo de datos para un conector de flujo de almacenamiento en la nube en la interfaz de usuario
topic-legacy: overview
type: Tutorial
description: Un flujo de datos es una tarea programada que recupera e incorpora datos de un origen a un conjunto de datos de Platform. Este tutorial proporciona pasos para configurar un nuevo flujo de datos con su conector base de almacenamiento en la nube.
exl-id: 75deead6-ef3c-48be-aed2-c43d1f432178
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 1%

---

# Configurar un flujo de datos para una conexión de flujo de almacenamiento en la nube en la interfaz de usuario

Un flujo de datos es una tarea programada que recupera e incorpora datos de un origen a un conjunto de datos [!DNL Platform]. Este tutorial proporciona pasos para configurar un nuevo flujo de datos con su conector base de almacenamiento en la nube.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual se  [!DNL Experience Platform] organizan los datos de experiencia del cliente.
   - [Aspectos básicos de la composición](../../../../../xdm/schema/composition.md) del esquema: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

Además, este tutorial requiere que ya haya creado un conector de almacenamiento en la nube. Puede encontrar una lista de tutoriales para crear diferentes conectores de almacenamiento en la nube en la interfaz de usuario en la [información general de conectores de origen](../../../../home.md).

## Seleccionar datos

Después de crear el conector de almacenamiento en la nube, aparece el paso *Select data*, que proporciona una interfaz para seleccionar el flujo desde el que se retransmitirán los datos.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-data.png)

## Asignación de campos de datos a un esquema XDM

Aparece el paso **[!UICONTROL Mapping]**, que proporciona una interfaz interactiva para asignar los datos de origen a un conjunto de datos [!DNL Platform].

Elija un conjunto de datos para los datos entrantes en los que se van a introducir. Puede utilizar un conjunto de datos existente o crear uno nuevo.

**Usar un conjunto de datos existente**

Para introducir datos en un conjunto de datos existente, seleccione **[!UICONTROL Use existing dataset]** y haga clic en el icono del conjunto de datos.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/use-existing-data.png)

Aparece el cuadro de diálogo **[!UICONTROL Select dataset]**. Busque el conjunto de datos que desea utilizar, selecciónelo y haga clic en **[!UICONTROL Continue]**.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-existing-data.png)

**Usar un nuevo conjunto de datos**

Para introducir datos en un nuevo conjunto de datos, seleccione **[!UICONTROL Create new dataset]** e introduzca un nombre y una descripción para el conjunto de datos en los campos proporcionados. A continuación, seleccione el esquema que desee utilizar en la lista desplegable .

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/use-new-dataset.png)

## Asigne un nombre al flujo de datos

Aparece el paso **[!UICONTROL Dataflow detail]**, que le permite dar un nombre y una breve descripción del nuevo flujo de datos.

Proporcione valores para el flujo de datos y haga clic en **[!UICONTROL Next]**.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/name-your-dataflow.png)

### Revise el flujo de datos

Aparece el paso **[!UICONTROL Review]**, que le permite revisar el nuevo flujo de datos antes de crearlo. Los detalles se agrupan en las siguientes categorías:

- **[!UICONTROL Source details]**: Muestra el tipo de origen y otros detalles relevantes sobre el origen.
- **[!UICONTROL Target details]**: Muestra en qué conjunto de datos se están incorporando los datos de origen, incluido el esquema al que se adhiere el conjunto de datos.

Una vez que haya revisado el flujo de datos, haga clic en **[!UICONTROL Finish]** y permita que se cree el flujo de datos.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/review.png)

## Supervisión y eliminación del flujo de datos

Una vez creado el flujo de datos del almacenamiento en la nube, puede supervisar los datos que se están incorporando a través de él. Para obtener más información sobre la monitorización y eliminación de flujos de datos, consulte el tutorial sobre [monitorización de flujos de datos](../../../../../ingestion/quality/monitor-data-ingestion.md).

## Pasos siguientes

Al seguir este tutorial, ha creado correctamente un flujo de datos para incorporar datos de un almacenamiento en la nube externo y ha obtenido información sobre la monitorización de conjuntos de datos. Los datos entrantes ahora se pueden usar en servicios descendentes [!DNL Platform] como [!DNL Real-time Customer Profile] y [!DNL Data Science Workspace]. Consulte los siguientes documentos para obtener más información:

- Información general del [[!DNL Real-time Customer Profile] ](../../../../../profile/home.md)
- Información general del [[!DNL Data Science Workspace] ](../../../../../data-science-workspace/home.md)

## Apéndice

Las secciones siguientes proporcionan información adicional para trabajar con conectores de origen.

### Desactivación de un flujo de datos

Cuando se crea un flujo de datos, este se activa inmediatamente e ingresa los datos según la programación que se le haya dado. Puede deshabilitar un flujo de datos activo en cualquier momento siguiendo las instrucciones que se indican a continuación.

Dentro del espacio de trabajo **[!UICONTROL Sources]** , haga clic en la pestaña **[!UICONTROL Browse]** . A continuación, haga clic en el nombre de la conexión asociada al flujo de datos activo que desea desactivar.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/browse.png)

Aparece la página **[!UICONTROL Source activity]**. Seleccione el flujo de datos activo de la lista para abrir su columna **[!UICONTROL Properties]** en el lado derecho de la pantalla, que contiene un botón de alternancia **[!UICONTROL Enabled]**. Haga clic en el botón de alternancia para deshabilitar el flujo de datos. Se puede utilizar la misma opción para volver a habilitar un flujo de datos una vez desactivado.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/disable-source.png)

### Activar datos de entrada para la población [!DNL Profile]

Los datos de entrada del conector de origen se pueden utilizar para enriquecer y rellenar los datos [!DNL Real-time Customer Profile]. Para obtener más información sobre cómo rellenar los datos [!DNL Real-time Customer Profile], consulte el tutorial sobre [Población del perfil](../../profile.md).
