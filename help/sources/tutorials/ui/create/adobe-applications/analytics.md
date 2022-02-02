---
keywords: Experience Platform;home;popular topics;Analytics source connector;Analytics connector;Analytics source;analytics
solution: Experience Platform
title: Crear una conexión de origen de Adobe Analytics en la interfaz de usuario
topic-legacy: overview
type: Tutorial
description: Aprenda a crear una conexión de origen de Adobe Analytics en la interfaz de usuario para introducir los datos de los consumidores en Adobe Experience Platform.
exl-id: 5ddbaf63-feaa-44f5-b2f2-2d5ae507f423
source-git-commit: d62d1ff9ebef58401911bab1232d1847d65e043f
workflow-type: tm+mt
source-wordcount: '1571'
ht-degree: 1%

---

# Crear una conexión de origen de Adobe Analytics en la interfaz de usuario

This tutorial provides steps for creating an Adobe Analytics source connection in the UI to bring [!DNL Analytics] Report Suite data into Adobe Experience Platform.

## Primeros pasos

This tutorial requires a working understanding of the following components of Adobe Experience Platform:

* [Sistema del Modelo de datos de experiencia (XDM)](../../../../../xdm/home.md): El marco estandarizado mediante el cual el Experience Platform organiza los datos de experiencia del cliente.
* [Perfil del cliente en tiempo real](../../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

### Terminología clave

Es importante comprender los siguientes términos clave utilizados en este documento:

* **Atributo estándar**: Los atributos estándar son cualquier atributo predefinido por Adobe. Contienen el mismo significado para todos los clientes y están disponibles en la variable [!DNL Analytics] datos de origen y [!DNL Analytics] grupos de campos de esquema.
* **Atributo personalizado**: Los atributos personalizados son cualquier atributo de la jerarquía de variables personalizadas en [!DNL Analytics]. Los atributos personalizados se utilizan en una implementación de Adobe Analytics para capturar información específica en un grupo de informes y pueden variar en su uso de Grupo de informes a Grupo de informes. Los atributos personalizados incluyen eVars, props y listas. Consulte lo siguiente [[!DNL Analytics] documentación sobre variables de conversión](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=en) para obtener más información sobre las eVars.
* **Cualquier atributo de los grupos de campos personalizados**: Los atributos que se originan a partir de grupos de campos creados por clientes se definen como usuarios y no se consideran atributos estándar ni personalizados.
* **Nombres descriptivos**: Los nombres descriptivos son etiquetas proporcionadas por el ser humano para variables personalizadas en un [!DNL Analytics] implementación. Consulte lo siguiente [[!DNL Analytics] documentación sobre variables de conversión](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=en) para obtener más información sobre nombres descriptivos.

## Crear una conexión de origen con Adobe Analytics

In the Platform UI, select **[!UICONTROL Sources]** from the left navigation to access the [!UICONTROL Sources] workspace. The [!UICONTROL Catalog] screen displays a variety of sources that you can create an account with.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. You can also use the search bar to narrow down the displayed sources.

En el **[!UICONTROL aplicaciones de Adobe]** categoría, seleccione **[!UICONTROL Adobe Analytics]** y, a continuación, seleccione **[!UICONTROL Añadir datos]**.

![catalog](../../../../images/tutorials/create/analytics/catalog.png)

### Seleccionar datos

La variable **[!UICONTROL Agregar datos de origen de Analytics]** aparece. Select **[!UICONTROL Report Suite]** to start creating a source connection for Analytics Report Suite data, and then select the Report Suite you would like to ingest. Los grupos de informes que no se pueden seleccionar ya se han incorporado, ya sea en este simulador para pruebas o en otro simulador para pruebas. Select **[!UICONTROL Siguiente]** para continuar.

>[!NOTE]
>
>Se pueden realizar varias conexiones entrantes para incorporar varios grupos de informes, pero solo se puede utilizar un grupo de informes con Real-time Customer Data Platform a la vez.

![](../../../../images/tutorials/create/analytics/add-data.png)

<!---Analytics Report Suites can be configured for one sandbox at a time. To import the same Report Suite into a different sandbox, the dataset flow will have to be deleted and instantiated again via configuration for a different sandbox.--->

### Asignación

>[!IMPORTANT]
>
>The Data Prep support feature for the [!DNL Analytics] source is in beta.

Antes de poder asignar su [!DNL Analytics] para dirigirse al esquema XDM, primero debe seleccionar si utiliza un esquema predeterminado o uno personalizado.

A default schema creates a new schema on your behalf, containing the [!DNL Adobe Analytics ExperienceEvent Template] field group. Para utilizar un esquema predeterminado, seleccione **[!UICONTROL Esquema predeterminado]**.

![default-schema](../../../../images/tutorials/create/analytics/default-schema.png)

Con un esquema personalizado, puede elegir cualquier esquema disponible para su [!DNL Analytics] siempre que ese esquema tenga la variable [!DNL Adobe Analytics ExperienceEvent Template] grupo de campos. Para utilizar un esquema personalizado, seleccione **[!UICONTROL Esquema personalizado]**.

![custom-schema](../../../../images/tutorials/create/analytics/custom-schema.png)

La variable [!UICONTROL Asignación] proporciona una interfaz para asignar campos de origen a los campos de esquema de destino correspondientes. Desde aquí, puede asignar variables personalizadas a nuevos grupos de campos de esquema y aplicar cálculos según lo admite la preparación de datos. Select a target schema to start the mapping process.

>[!TIP]
>
>Only schemas that have the [!DNL Adobe Analytics ExperienceEvent Template] field group are displayed in the schema selection menu. Other schemas are omitted. Si no hay esquemas adecuados disponibles para los datos del grupo de informes, debe crear un esquema nuevo. Para ver los pasos detallados sobre la creación de esquemas, consulte la guía de [creación y edición de esquemas en la interfaz de usuario](../../../../../xdm/ui/resources/schemas.md).

![select-schema](../../../../images/tutorials/create/analytics/select-schema.png)

La variable [!UICONTROL Asignación de campos estándar] muestra los paneles para [!UICONTROL Asignaciones estándar aplicadas], [!UICONTROL Asignaciones estándar no coincidentes] y [!UICONTROL Asignaciones personalizadas]. Consulte la siguiente tabla para obtener información específica sobre cada categoría:

| Asignación de campos estándar | Descripción |
| --- | --- |
| [!UICONTROL Asignaciones estándar aplicadas] | La variable [!UICONTROL Asignaciones estándar aplicadas] muestra el número total de atributos asignados. Las asignaciones estándar hacen referencia a conjuntos de asignaciones entre todos los atributos del origen [!DNL Analytics] datos y atributos correspondientes en [!DNL Analytics] grupo de campos. These are pre-mapped and cannot be edited. |
| [!UICONTROL Asignaciones estándar no coincidentes] | La variable [!UICONTROL Asignaciones estándar no coincidentes] hace referencia al número de atributos asignados que contienen conflictos de nombres descriptivos. Estos conflictos aparecen cuando se vuelve a utilizar un esquema que ya tiene un conjunto completo de descriptores de campo de un grupo de informes diferente. Puede continuar con su [!DNL Analytics] flujo de datos incluso con conflictos de nombres descriptivos. |
| [!UICONTROL Asignaciones personalizadas] | La variable [!UICONTROL Asignaciones personalizadas] muestra el número de atributos personalizados asignados, incluidos eVars, props y listas. Las asignaciones personalizadas hacen referencia a conjuntos de asignaciones entre atributos personalizados en el origen [!DNL Analytics] datos y atributos en grupos de campos personalizados incluidos en el esquema seleccionado. |

![map-standard-fields](../../../../images/tutorials/create/analytics/map-standard-fields.png)

To preview the [!DNL Analytics] ExperienceEvent template schema field group, select **[!UICONTROL View]** in the [!UICONTROL Standard mappings applied] panel.

![view](../../../../images/tutorials/create/analytics/view.png)

La variable [!UICONTROL Grupo de campos de esquema de plantilla de Adobe Analytics ExperienceEvent] proporciona una interfaz que se utiliza para inspeccionar la estructura del esquema. When finished, select **[!UICONTROL Close]**.

![field-group-preview](../../../../images/tutorials/create/analytics/field-group-preview.png)

Platform automatically detects your mapping sets for any friendly name conflicts. Si no hay conflictos con los conjuntos de asignaciones, seleccione **[!UICONTROL Siguiente]** para continuar.

![asignación](../../../../images/tutorials/create/analytics/mapping.png)

Si hay conflictos de nombres prácticos entre el grupo de informes de origen y el esquema seleccionado, puede continuar con su [!DNL Analytics] flujo de datos, reconociendo que los descriptores de campo no se cambiarán. También puede optar por crear un nuevo esquema con un conjunto de descriptores en blanco.

Select **[!UICONTROL Siguiente]** para continuar.

![precaución](../../../../images/tutorials/create/analytics/caution.png)

#### Custom mappings

Para utilizar funciones de preparación de datos y añadir nuevos campos calculados o de asignación para atributos personalizados, seleccione **[!UICONTROL Ver asignaciones personalizadas]**.

![view-custom-mapping](../../../../images/tutorials/create/analytics/view-custom-mapping.png)

A continuación, seleccione **[!UICONTROL Añadir nueva asignación]**.

Según sus necesidades, puede seleccionar una de las opciones siguientes: **[!UICONTROL Añadir nueva asignación]** o **[!UICONTROL Añadir campo calculado]** de las opciones que aparecen.

![add-new-mapping](../../../../images/tutorials/create/analytics/add-new-mapping.png)

Aparece un conjunto de asignaciones vacío. Seleccione el icono de asignación para añadir un campo de origen.

![select-source-field](../../../../images/tutorials/create/analytics/select-source-field.png)

Puede utilizar la interfaz para navegar por la estructura del esquema de origen e identificar el nuevo campo de origen que desea utilizar. Una vez seleccionado el campo de origen que desea asignar, seleccione **[!UICONTROL Select]**.

![asignación de selección](../../../../images/tutorials/create/analytics/select-mapping.png)

A continuación, seleccione el icono de asignación en [!UICONTROL Campo de destino] para asignar el campo de origen seleccionado al campo de destino correspondiente.

![select-target-field](../../../../images/tutorials/create/analytics/select-target-field.png)

Al igual que el esquema de origen, se puede utilizar la interfaz para navegar por la estructura del esquema de destino y seleccionar el campo de destino al que desea asignar. Una vez seleccionado el campo de destino correspondiente, seleccione **[!UICONTROL Select]**.

![select-target-mapping](../../../../images/tutorials/create/analytics/select-target-mapping.png)

Una vez completado el conjunto de asignaciones personalizadas, seleccione **[!UICONTROL Siguiente]** para continuar.

![asignación completa-personalizada](../../../../images/tutorials/create/analytics/complete-custom-mapping.png)

La siguiente documentación proporciona más recursos para comprender la preparación de datos, los campos calculados y las funciones de asignación:

* [Resumen de la preparación de datos](../../../../../data-prep/home.md)
* [Data Prep mapping functions](../../../../../data-prep/functions.md)
* [Add calculated fields](../../../../../data-prep/ui/mapping.md#calculated-fields)

### Proporcionar detalles de flujo de datos

The **[!UICONTROL Dataflow detail]** step appears, where you must provide a name and an optional description for the dataflow. Select **[!UICONTROL Siguiente]** cuando termine.

![dataflow-detail](../../../../images/tutorials/create/analytics/dataflow-detail.png)

### Review

La variable [!UICONTROL Consulte] aparece, lo que le permite revisar el nuevo flujo de datos de Analytics antes de crearlo. Los detalles de la conexión se agrupan por categorías, entre ellas:

* [!UICONTROL Connection]: Displays the source platform of the connection.
* [!UICONTROL Tipo de datos]: Muestra el grupo de informes seleccionado y su ID de grupo de informes correspondiente.

![review](../../../../images/tutorials/create/analytics/review.png)

### Monitorizar el flujo de datos

Once your dataflow has been created, you can monitor the data that is being ingested through it. From the [!UICONTROL Catalog] screen, select **[!UICONTROL Dataflows]** to view a list of established flows associated with your Analytics account.

![select-dataflows](../../../../images/tutorials/create/analytics/select-dataflows.png)

The **Dataflows** screen appears. En esta página hay un par de flujos de conjuntos de datos, incluida información sobre su nombre, datos de origen, tiempo de creación y estado.

El conector crea una instancia de dos flujos de conjuntos de datos. One flow represents backfill data and the other is for live data. Los datos de relleno no están configurados para Perfil, pero se envían al lago de datos para casos analíticos y de ciencia de datos.

Para obtener más información sobre el relleno, los datos activos y sus latencias respectivas, consulte la [Resumen de los conectores de datos de Analytics](../../../../connectors/adobe-applications/analytics.md).

Select the dataset flow you wish to view from the list.

![select-target-dataset](../../../../images/tutorials/create/analytics/select-target-dataset.png)

La variable **[!UICONTROL Actividad del conjunto de datos]** se abre. Esta página muestra la tasa de consumo de los mensajes en forma de gráfico. Select **[!UICONTROL Data governance]** from the top header to access the labelling fields.

![actividad del conjunto de datos](../../../../images/tutorials/create/analytics/dataset-activity.png)

Puede ver las etiquetas heredadas de un flujo de datos desde el [!UICONTROL Administración de datos] en el Navegador. Para obtener más información sobre cómo etiquetar datos procedentes de Analytics, visite [guía de etiquetas de uso de datos](../../../../../data-governance/labels/user-guide.md).

![data-gov](../../../../images/tutorials/create/analytics/data-gov.png)

Para eliminar un flujo de datos, vaya a la [!UICONTROL Flujos de datos] y, a continuación, seleccione los puntos suspensivos (`...`) junto al nombre del flujo de datos y, a continuación, seleccione [!UICONTROL Eliminar].

![delete](../../../../images/tutorials/create/analytics/delete.png)

## Pasos siguientes y recursos adicionales

Una vez creada la conexión, el flujo de datos se crea automáticamente para contener los datos entrantes y rellenar un conjunto de datos con el esquema seleccionado. Además, se rellenan los datos de forma retroactiva y se introducen hasta 13 meses de datos históricos. When the initial ingestion completes, [!DNL Analytics] data and be used by downstream Platform services such as [!DNL Real-time Customer Profile] and Segmentation Service. See the following documents for more details:

* [Información general del [!DNL Real-time Customer Profile]](../../../../../profile/home.md)
* [Información general del [!DNL Segmentation Service]](../../../../../segmentation/home.md)
* [Información general del [!DNL Data Science Workspace]](../../../../../data-science-workspace/home.md)
* [Información general del [!DNL Query Service]](../../../../../query-service/home.md)

El siguiente vídeo pretende comprender la ingesta de datos mediante el conector de origen de Adobe Analytics:

>[!WARNING]
>
> La variable [!DNL Platform] La interfaz de usuario que se muestra en el siguiente vídeo no está actualizada. Consulte la documentación anterior para obtener las últimas capturas de pantalla y funciones de la interfaz de usuario.

>[!VIDEO](https://video.tv.adobe.com/v/29687?quality=12&learn=on)
