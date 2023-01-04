---
keywords: Experience Platform;inicio;temas populares;flujo continuo;conector de almacenamiento en la nube;almacenamiento en la nube
solution: Experience Platform
title: Crear un flujo de datos de flujo continuo para un origen de almacenamiento en la nube en la interfaz de usuario
topic-legacy: overview
type: Tutorial
description: Un flujo de datos es una tarea programada que recupera e incorpora datos de un origen a un conjunto de datos de Platform. Este tutorial proporciona pasos para configurar un nuevo flujo de datos con su conector base de almacenamiento en la nube.
exl-id: 75deead6-ef3c-48be-aed2-c43d1f432178
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1055'
ht-degree: 1%

---

# Crear un flujo de datos de flujo continuo para un origen de almacenamiento en la nube en la interfaz de usuario

Un flujo de datos es una tarea programada que recupera e incorpora datos de un origen a un conjunto de datos de Adobe Experience Platform. Este tutorial proporciona pasos para crear un flujo de datos de flujo continuo para un origen de almacenamiento en la nube en la interfaz de usuario.

Antes de intentar este tutorial, primero debe establecer una conexión válida y autenticada entre la cuenta de almacenamiento en la nube y Platform. Si todavía no tiene una conexión autenticada, consulte uno de los siguientes tutoriales para obtener información sobre la autenticación de sus cuentas de almacenamiento de nube de flujo continuo:

- [[!DNL Amazon Kinesis]](../../../ui/create/cloud-storage/kinesis.md)
- [[!DNL Azure Event Hubs]](../../../ui/create/cloud-storage/eventhub.md)
- [[!DNL Google PubSub]](../../../ui/create/cloud-storage/google-pubsub.md)

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

- [Flujos de datos](../../../../../dataflows/home.md): Los flujos de datos son una representación de los trabajos de datos que mueven los datos a través de Platform. Los flujos de datos se configuran en distintos servicios, desde fuentes hasta [!DNL Identity Service], a [!DNL Profile]y [!DNL Destinations].
- [Preparación de datos](../../../../../data-prep/home.md): La preparación de datos permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el Modelo de datos de experiencia (XDM). La preparación de datos aparece como un paso de &quot;mapa&quot; en los procesos de ingesta de datos, incluido el flujo de trabajo de ingesta de CSV.
- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco normalizado por el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   - [Aspectos básicos de la composición del esquema](../../../../../xdm/schema/composition.md): Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   - [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

## Adición de datos

Después de crear la autenticación de su cuenta de almacenamiento de la nube de flujo continuo, la variable **[!UICONTROL Seleccionar datos]** , proporcionando una interfaz para que seleccione el flujo de datos que desea traer a Platform.

- La parte izquierda de la interfaz es un navegador que le permite ver los flujos de datos disponibles en su cuenta;
- La parte derecha de la interfaz le permite previsualizar hasta 100 filas de datos de un archivo JSON.

![interfaz](../../../../images/tutorials/dataflow/cloud-storage/streaming/interface.png)

Seleccione el flujo de datos que desee utilizar y, a continuación, seleccione **[!UICONTROL Elegir archivo]** para cargar un esquema de muestra.

>[!TIP]
>
>Si los datos son compatibles con XDM, puede omitir la carga de un esquema de muestra y seleccionar **[!UICONTROL Siguiente]** para continuar.

![flujo de selección](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-stream.png)

Una vez que se haya cargado el esquema, la interfaz de vista previa se actualiza para mostrar una vista previa del esquema que ha cargado. La interfaz de vista previa permite inspeccionar el contenido y la estructura de un archivo. También puede usar la variable [!UICONTROL Campo de búsqueda] para acceder a elementos específicos desde el esquema.

Cuando termine, seleccione **[!UICONTROL Siguiente]**.

![schema-preview](../../../../images/tutorials/dataflow/cloud-storage/streaming/schema-preview.png)

## Asignación

La variable **[!UICONTROL Asignación]** aparece, proporcionando una interfaz para asignar los datos de origen a un conjunto de datos de Platform.

Elija un conjunto de datos para los datos entrantes en los que se van a introducir. Puede utilizar un conjunto de datos existente o crear uno nuevo.

### Nuevo conjunto de datos

Para introducir datos en un nuevo conjunto de datos, seleccione **[!UICONTROL Nuevo conjunto de datos]** e introduzca un nombre y una descripción para el conjunto de datos en los campos proporcionados. Para añadir un esquema, puede introducir un nombre de esquema existente en la **[!UICONTROL Seleccionar esquema]** para abrir el Navegador. También puede seleccionar **[!UICONTROL Búsqueda avanzada de esquema]** para buscar un esquema adecuado.

![conjunto de datos nuevo](../../../../images/tutorials/dataflow/cloud-storage/streaming/new-dataset.png)

La variable [!UICONTROL Seleccionar esquema] , que le proporciona una lista de los esquemas disponibles para elegir. Seleccione un esquema de la lista para actualizar el carril derecho y mostrar detalles específicos del esquema seleccionado, incluida información sobre si el esquema está habilitado para [!DNL Profile].

Una vez identificado y seleccionado el esquema que desea utilizar, seleccione **[!UICONTROL Listo]**.

![select-schema](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-schema.png)

La variable [!UICONTROL Conjunto de datos de Target] se actualiza la página con el esquema seleccionado mostrado como parte del conjunto de datos. Durante este paso, puede habilitar su conjunto de datos para [!DNL Profile] y crear una vista holística de los atributos y comportamientos de una entidad. Los datos de todos los conjuntos de datos habilitados se incluirán en [!DNL Profile] Los cambios y se aplican cuando guarda el flujo de datos.

Alternar el **[!UICONTROL Conjunto de datos del perfil]** para habilitar el conjunto de datos de target [!DNL Profile].

![nuevo perfil](../../../../images/tutorials/dataflow/cloud-storage/streaming/new-profile.png)

### Conjunto de datos existente

Para introducir datos en un conjunto de datos existente, seleccione **[!UICONTROL Conjunto de datos existente]** y, a continuación, seleccione el icono del conjunto de datos.

![conjunto de datos existente](../../../../images/tutorials/dataflow/cloud-storage/streaming/existing-dataset.png)

La variable **[!UICONTROL Seleccionar conjunto de datos]** , que le proporciona una lista de conjuntos de datos disponibles para elegir. Seleccione un conjunto de datos de la lista para actualizar el carril derecho y mostrar detalles específicos del conjunto de datos seleccionado, incluida información sobre si el conjunto de datos puede habilitarse para [!DNL Profile].

Una vez identificado y seleccionado el conjunto de datos que desea utilizar, seleccione **[!UICONTROL Listo]**.

![select-dataset](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-dataset.png)

Una vez que seleccione el conjunto de datos, seleccione el [!DNL Profile] alternar para habilitar su conjunto de datos para [!DNL Profile].

![existente-profile](../../../../images/tutorials/dataflow/cloud-storage/streaming/existing-profile.png)

### Asignación de campos estándar

Con el conjunto de datos y el esquema establecidos, la variable **[!UICONTROL Asignación de campos estándar]** , lo que le permite configurar manualmente los campos de asignación de los datos.

>[!TIP]
>
>Platform proporciona recomendaciones inteligentes para campos asignados automáticamente en función del esquema o conjunto de datos de destino que haya seleccionado. Puede ajustar manualmente las reglas de asignación para adaptarlas a sus casos de uso.

En función de sus necesidades, puede elegir asignar campos directamente o utilizar funciones de preparación de datos para transformar los datos de origen a fin de derivar valores calculados o calculados. Para ver los pasos completos sobre el uso de la interfaz del asignador y los campos calculados, consulte la [Guía de la interfaz de usuario de preparación de datos](../../../../../data-prep/ui/mapping.md).

Una vez asignados los datos de origen, seleccione **[!UICONTROL Siguiente]**.

![asignación](../../../../images/tutorials/dataflow/cloud-storage/streaming/mapping.png)

## Detalles de flujo de datos

La variable **[!UICONTROL Detalles de flujo de datos]** aparece, lo que le permite asignar un nombre y describir brevemente el nuevo flujo de datos.

Proporcione valores para el flujo de datos y seleccione **[!UICONTROL Siguiente]**.

![dataflow-detail](../../../../images/tutorials/dataflow/cloud-storage/streaming/dataflow-detail.png)

### Revisión

La variable **[!UICONTROL Consulte]** , lo que le permite revisar el nuevo flujo de datos antes de crearlo. Los detalles se agrupan en las siguientes categorías:

- **[!UICONTROL Conexión]**: Muestra el nombre de su cuenta, el tipo de fuente y otra información diversa específica del origen de almacenamiento de la nube de flujo continuo que está utilizando.
- **[!UICONTROL Asignación de campos de conjunto de datos y asignación]**: Muestra el conjunto de datos de destino y el esquema que está utilizando para el flujo de datos.

Una vez que haya revisado el flujo de datos, seleccione **[!UICONTROL Finalizar]** y permitir que se cree un flujo de datos.

![review](../../../../images/tutorials/dataflow/cloud-storage/streaming/review.png)

## Supervisión y eliminación del flujo de datos

Una vez creado el flujo de datos de almacenamiento de la nube de flujo continuo, puede supervisar los datos que se están incorporando a través de él. Para obtener más información sobre la monitorización y eliminación de flujos de datos de flujo continuo, consulte el tutorial sobre [monitorización de flujos de datos de flujo continuo](../../monitor-streaming.md).

## Pasos siguientes

Siguiendo este tutorial, ha creado correctamente un flujo de datos para transmitir datos desde un origen de almacenamiento en la nube. Los datos entrantes ahora se pueden usar en servicios de Platform descendentes como [!DNL Real-Time Customer Profile] y [!DNL Data Science Workspace]. Consulte los siguientes documentos para obtener más información:

- [Información general del [!DNL Real-Time Customer Profile]](../../../../../profile/home.md)
- [Información general del [!DNL Data Science Workspace]](../../../../../data-science-workspace/home.md)