---
keywords: Experience Platform;inicio;temas populares;Conector de origen de Analytics;Conector de Analytics;Fuente de Analytics;Analytics
solution: Experience Platform
title: Crear una conexión de origen de Adobe Analytics en la interfaz de usuario
topic-legacy: overview
type: Tutorial
description: Aprenda a crear una conexión de origen de Adobe Analytics en la interfaz de usuario para introducir los datos de los consumidores en Adobe Experience Platform.
exl-id: 5ddbaf63-feaa-44f5-b2f2-2d5ae507f423
source-git-commit: e28158bbd4e89e5fcf19f4dc89f266d737b34e65
workflow-type: tm+mt
source-wordcount: '1493'
ht-degree: 1%

---

# Crear una conexión de origen de Adobe Analytics en la interfaz de usuario

Este tutorial proporciona los pasos para crear una conexión de origen de Adobe Analytics en la interfaz de usuario para introducir datos del [!DNL Analytics] grupo de informes en Adobe Experience Platform.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Sistema del Modelo de datos de experiencia (XDM)](../../../../../xdm/home.md): El marco estandarizado mediante el cual el Experience Platform organiza los datos de experiencia del cliente.
* [Perfil](../../../../../profile/home.md) del cliente en tiempo real: Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.
* [Simuladores para pruebas](../../../../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

### Terminología clave

Es importante comprender los siguientes términos clave utilizados en este documento:

* **Atributo** estándar: Los atributos estándar son cualquier atributo predefinido por Adobe. Contienen el mismo significado para todos los clientes y están disponibles en los grupos de campos de esquema [!DNL Analytics] y de datos de origen [!DNL Analytics] .
* **Atributo** personalizado: Los atributos personalizados son cualquier atributo de la jerarquía de variables personalizadas de  [!DNL Analytics]. Los atributos personalizados se utilizan en una implementación de Adobe Analytics para capturar información específica en un grupo de informes y pueden variar en su uso de Grupo de informes a Grupo de informes. Los atributos personalizados incluyen eVars, props y listas. Consulte la siguiente [[!DNL Analytics] documentación sobre variables de conversión](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=en) para obtener más información sobre las eVars.
* **Cualquier atributo de los grupos** de campos personalizados: Los atributos que se originan a partir de grupos de campos creados por clientes se definen como usuarios y no se consideran atributos estándar ni personalizados.
* **Nombres** descriptivos: Los nombres descriptivos son etiquetas proporcionadas por el ser humano para variables personalizadas en una  [!DNL Analytics] implementación. Consulte la siguiente [[!DNL Analytics] documentación sobre variables de conversión](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=en) para obtener más información sobre nombres descriptivos.

## Crear una conexión de origen con Adobe Analytics

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Sources]** en el panel de navegación izquierdo para acceder al espacio de trabajo [!UICONTROL Sources]. La pantalla [!UICONTROL Catalog] muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede utilizar la barra de búsqueda para reducir los orígenes mostrados.

En la categoría **[!UICONTROL Aplicaciones de Adobe]**, seleccione **[!UICONTROL Adobe Analytics]** y, a continuación, seleccione **[!UICONTROL Agregar datos]**.

![catálogo](../../../../images/tutorials/create/analytics/catalog.png)

### Seleccionar datos

Aparece el paso **[!UICONTROL Analytics source add data]**. Seleccione **[!UICONTROL Grupo de informes]** para empezar a crear una conexión de origen para los datos del grupo de informes de Analytics y, a continuación, seleccione el grupo de informes que desee ingerir. Los grupos de informes que no se pueden seleccionar ya se han incorporado, ya sea en este simulador para pruebas o en otro simulador para pruebas. Seleccione **[!UICONTROL Siguiente]** para continuar.

>[!NOTE]
>
>Se pueden realizar varias conexiones entrantes para incorporar varios grupos de informes, pero solo se puede utilizar un grupo de informes con la plataforma de datos del cliente en tiempo real a la vez.

![](../../../../images/tutorials/create/analytics/add-data.png)

<!---Analytics Report Suites can be configured for one sandbox at a time. To import the same Report Suite into a different sandbox, the dataset flow will have to be deleted and instantiated again via configuration for a different sandbox.--->

### Asignación

>[!IMPORTANT]
>
>La función de soporte de preparación de datos para el origen [!DNL Analytics] está en versión beta.

La página [!UICONTROL Mapping] proporciona una interfaz para asignar los campos de origen a los campos de esquema de destino adecuados. Desde aquí, puede asignar variables personalizadas a nuevos grupos de campos de esquema y aplicar cálculos según lo admite la preparación de datos. Seleccione un esquema de destino para iniciar el proceso de asignación.

>[!TIP]
>
>En el menú de selección de esquema solo se muestran los esquemas que tienen el grupo de campos de plantilla [!DNL Analytics]. Se omiten otros esquemas. Si no hay esquemas adecuados disponibles para los datos del grupo de informes, debe crear un esquema nuevo. Para ver los pasos detallados sobre la creación de esquemas, consulte la guía sobre la [creación y edición de esquemas en la IU](../../../../../xdm/ui/resources/schemas.md).

![select-schema](../../../../images/tutorials/create/analytics/select-schema.png)

La sección [!UICONTROL Map standard fields] muestra los paneles para [!UICONTROL Asignaciones estándar aplicadas], [!UICONTROL Asignaciones estándar no coincidentes] y [!UICONTROL Asignaciones personalizadas]. Consulte la siguiente tabla para obtener información específica sobre cada categoría:

| Asignación de campos estándar | Descripción |
| --- | --- |
| [!UICONTROL Asignaciones estándar aplicadas] | El panel [!UICONTROL Asignaciones estándar aplicadas] muestra el número total de atributos asignados. Las asignaciones estándar hacen referencia a conjuntos de asignaciones entre todos los atributos de los datos de origen [!DNL Analytics] y los atributos correspondientes del grupo de campos [!DNL Analytics]. Están preasignados y no se pueden editar. |
| [!UICONTROL Asignaciones estándar no coincidentes] | El panel [!UICONTROL Asignaciones estándar no coincidentes] hace referencia al número de atributos asignados que contienen conflictos de nombres descriptivos. Estos conflictos aparecen cuando se vuelve a utilizar un esquema que ya tiene un conjunto completo de descriptores de campo de un grupo de informes diferente. Puede continuar con el flujo de datos [!DNL Analytics] incluso con conflictos de nombres prácticos. |
| [!UICONTROL Asignaciones personalizadas] | El panel [!UICONTROL Asignaciones personalizadas] muestra el número de atributos personalizados asignados, incluidas eVars, props y listas. Las asignaciones personalizadas hacen referencia a conjuntos de asignación entre atributos personalizados en los datos de origen [!DNL Analytics] y atributos en grupos de campos personalizados incluidos en el esquema seleccionado. |

![map-standard-fields](../../../../images/tutorials/create/analytics/map-standard-fields.png)

Para obtener una vista previa del grupo de campos de esquema de plantilla [!DNL Analytics] ExperienceEvent, seleccione **[!UICONTROL View]** en el panel [!UICONTROL Standard mappings apply].

![view](../../../../images/tutorials/create/analytics/view.png)

La página [!UICONTROL Adobe Analytics ExperienceEvent Template Schema Field Group] proporciona una interfaz que se puede utilizar para inspeccionar la estructura del esquema. Cuando termine, seleccione **[!UICONTROL Cerrar]**.

![field-group-preview](../../../../images/tutorials/create/analytics/field-group-preview.png)

Platform detecta automáticamente los conjuntos de asignaciones para cualquier conflicto de nombres descriptivo. Si no hay ningún conflicto con los conjuntos de asignaciones, seleccione **[!UICONTROL Next]** para continuar.

![asignación](../../../../images/tutorials/create/analytics/mapping.png)

Si hay conflictos de nombres prácticos entre el grupo de informes de origen y el esquema seleccionado, puede continuar con el flujo de datos [!DNL Analytics], reconociendo que los descriptores de campo no se cambiarán. También puede optar por crear un nuevo esquema con un conjunto de descriptores en blanco.

Seleccione **[!UICONTROL Siguiente]** para continuar.

![precaución](../../../../images/tutorials/create/analytics/caution.png)

#### Asignaciones personalizadas

Para utilizar funciones de preparación de datos y agregar nuevos campos calculados o de asignación para atributos personalizados, seleccione **[!UICONTROL Ver asignaciones personalizadas]**.

![view-custom-mapping](../../../../images/tutorials/create/analytics/view-custom-mapping.png)

A continuación, seleccione **[!UICONTROL Add new mapping]**.

Según sus necesidades, puede seleccionar **[!UICONTROL Add new mapping]** o **[!UICONTROL Add calculated field]** entre las opciones que aparecen.

![add-new-mapping](../../../../images/tutorials/create/analytics/add-new-mapping.png)

Aparece un conjunto de asignaciones vacío. Seleccione el icono de asignación para añadir un campo de origen.

![select-source-field](../../../../images/tutorials/create/analytics/select-source-field.png)

Puede utilizar la interfaz para navegar por la estructura del esquema de origen e identificar el nuevo campo de origen que desea utilizar. Una vez seleccionado el campo de origen que desea asignar, seleccione **[!UICONTROL Seleccionar]**.

![asignación de selección](../../../../images/tutorials/create/analytics/select-mapping.png)

A continuación, seleccione el icono de asignación en [!UICONTROL Target Field] para asignar el campo de origen seleccionado al campo de destino correspondiente.

![select-target-field](../../../../images/tutorials/create/analytics/select-target-field.png)

Al igual que el esquema de origen, se puede utilizar la interfaz para navegar por la estructura del esquema de destino y seleccionar el campo de destino al que desea asignar. Una vez seleccionado el campo de destino correspondiente, seleccione **[!UICONTROL Select]**.

![select-target-mapping](../../../../images/tutorials/create/analytics/select-target-mapping.png)

Con el conjunto de asignaciones personalizadas completado, seleccione **[!UICONTROL Next]** para continuar.

![asignación completa-personalizada](../../../../images/tutorials/create/analytics/complete-custom-mapping.png)

La siguiente documentación proporciona más recursos para comprender la preparación de datos, los campos calculados y las funciones de asignación:

* [Resumen de la preparación de datos](../../../../../data-prep/home.md)
* [Funciones de asignación de preparación de datos](../../../../../data-prep/functions.md)
* [Añadir campos calculados](../../../../../data-prep/calculated-fields.md)

### Proporcionar detalles de flujo de datos

Aparece el paso **[!UICONTROL Dataflow detail]**, donde debe proporcionar un nombre y una descripción opcional para el flujo de datos. Seleccione **[!UICONTROL Next]** cuando termine.

![dataflow-detail](../../../../images/tutorials/create/analytics/dataflow-detail.png)

### Consulte

Aparece el paso [!UICONTROL Review], que le permite revisar el nuevo flujo de datos de Analytics antes de crearlo. Los detalles de la conexión se agrupan por categorías, entre ellas:

* [!UICONTROL Conexión]: Muestra la plataforma de origen de la conexión.
* [!UICONTROL Tipo] de datos: Muestra el grupo de informes seleccionado y su ID de grupo de informes correspondiente.

![review](../../../../images/tutorials/create/analytics/review.png)

### Monitorizar el flujo de datos

Una vez creado el flujo de datos, puede monitorizar los datos que se están incorporando a través de él. En la pantalla [!UICONTROL Catálogo], seleccione **[!UICONTROL Flujos de datos]** para ver una lista de los flujos establecidos asociados a su cuenta de Analytics.

![select-dataflows](../../../../images/tutorials/create/analytics/select-dataflows.png)

Aparece la pantalla **Flujos de datos**. En esta página hay un par de flujos de conjuntos de datos, incluida información sobre su nombre, datos de origen, tiempo de creación y estado.

El conector crea una instancia de dos flujos de conjuntos de datos. Un flujo representa los datos de relleno y el otro es para los datos activos. Los datos de relleno no están configurados para Perfil, pero se envían al lago de datos para casos analíticos y de ciencia de datos.

Para obtener más información sobre el relleno, los datos activos y sus latencias respectivas, consulte la [información general del conector de datos de Analytics](../../../../connectors/adobe-applications/analytics.md).

Seleccione el flujo del conjunto de datos que desee ver en la lista.

![select-target-dataset](../../../../images/tutorials/create/analytics/select-target-dataset.png)

Aparece la página **[!UICONTROL Actividad del conjunto de datos]**. Esta página muestra la tasa de consumo de los mensajes en forma de gráfico. Seleccione **[!UICONTROL Control de datos]** en el encabezado superior para acceder a los campos de etiquetado.

![actividad del conjunto de datos](../../../../images/tutorials/create/analytics/dataset-activity.png)

Puede ver las etiquetas heredadas de un flujo de conjuntos de datos desde la pantalla [!UICONTROL Control de datos]. Para obtener más información sobre cómo etiquetar datos procedentes de Analytics, visite la [guía de etiquetas de uso de datos](../../../../../data-governance/labels/user-guide.md).

![data-gov](../../../../images/tutorials/create/analytics/data-gov.png)

Para eliminar un flujo de datos, diríjase a la página [!UICONTROL Flujos de datos] y seleccione los puntos suspensivos (`...`) junto al nombre del flujo de datos y, a continuación, seleccione [!UICONTROL Eliminar].

![delete](../../../../images/tutorials/create/analytics/delete.png)

## Pasos siguientes y recursos adicionales

Una vez creada la conexión, el flujo de datos se crea automáticamente para contener los datos entrantes y rellenar un conjunto de datos con el esquema seleccionado. Además, se rellenan los datos de forma retroactiva y se introducen hasta 13 meses de datos históricos. Cuando se complete la ingesta inicial, los [!DNL Analytics] datos y se utilizarán en servicios de Platform descendentes como [!DNL Real-time Customer Profile] y el servicio de segmentación. Consulte los siguientes documentos para obtener más información:

* [Información general del [!DNL Real-time Customer Profile]](../../../../../profile/home.md)
* [Información general del [!DNL Segmentation Service]](../../../../../segmentation/home.md)
* [Información general del [!DNL Data Science Workspace]](../../../../../data-science-workspace/home.md)
* [Información general del [!DNL Query Service]](../../../../../query-service/home.md)

El siguiente vídeo pretende comprender la ingesta de datos mediante el conector de origen de Adobe Analytics:

>[!WARNING]
>
> La interfaz de usuario [!DNL Platform] que se muestra en el siguiente vídeo no está actualizada. Consulte la documentación anterior para obtener las últimas capturas de pantalla y funciones de la interfaz de usuario.

>[!VIDEO](https://video.tv.adobe.com/v/29687?quality=12&learn=on)
