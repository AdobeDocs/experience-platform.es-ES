---
keywords: Experience Platform;inicio;temas populares;Conector de origen de Analytics;Conector de Analytics;Fuente de Analytics;Analytics
solution: Experience Platform
title: Crear una conexión de origen de Adobe Analytics en la interfaz de usuario
topic-legacy: overview
type: Tutorial
description: Aprenda a crear una conexión de origen de Adobe Analytics en la interfaz de usuario para introducir los datos de los consumidores en Adobe Experience Platform.
exl-id: 5ddbaf63-feaa-44f5-b2f2-2d5ae507f423
source-git-commit: e67b3a6f9f57a3971a5bfa755db3b1043bebc96b
workflow-type: tm+mt
source-wordcount: '2301'
ht-degree: 2%

---

# Crear una conexión de origen de Adobe Analytics en la interfaz de usuario

Este tutorial proporciona los pasos para crear una conexión de origen de Adobe Analytics en la interfaz de usuario para introducir los datos del grupo de informes de Adobe Analytics en Adobe Experience Platform.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [Sistema del Modelo de datos de experiencia (XDM)](../../../../../xdm/home.md): El marco estandarizado mediante el cual el Experience Platform organiza los datos de experiencia del cliente.
* [Perfil del cliente en tiempo real](../../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

### Terminología clave

Es importante comprender los siguientes términos clave utilizados en este documento:

* **Atributo estándar**: Los atributos estándar son cualquier atributo predefinido por Adobe. Contienen el mismo significado para todos los clientes y están disponibles en la variable [!DNL Analytics] datos de origen y [!DNL Analytics] grupos de campos de esquema.
* **Atributo personalizado**: Los atributos personalizados son cualquier atributo de la jerarquía de variables personalizadas en [!DNL Analytics]. Los atributos personalizados se utilizan en una implementación de Adobe Analytics para capturar información específica en un grupo de informes y pueden variar en su uso de un grupo de informes a otro. Los atributos personalizados incluyen eVars, props y listas. Consulte lo siguiente [[!DNL Analytics] documentación sobre variables de conversión](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=en) para obtener más información sobre las eVars.
* **Cualquier atributo de los grupos de campos personalizados**: Los atributos que se originan a partir de grupos de campos creados por clientes se definen como usuarios y no se consideran atributos estándar ni personalizados.
* **Nombres descriptivos**: Los nombres descriptivos son etiquetas proporcionadas por el ser humano para variables personalizadas en un [!DNL Analytics] implementación. Consulte lo siguiente [[!DNL Analytics] documentación sobre variables de conversión](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=en) para obtener más información sobre nombres descriptivos.

## Crear una conexión de origen con Adobe Analytics

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Fuentes]** desde el panel de navegación izquierdo para acceder a la [!UICONTROL Fuentes] espacio de trabajo. La variable [!UICONTROL Catálogo] muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede utilizar la barra de búsqueda para reducir los orígenes mostrados.

En el **[!UICONTROL aplicaciones de Adobe]** categoría, seleccione **[!UICONTROL Adobe Analytics]** y, a continuación, seleccione **[!UICONTROL Añadir datos]**.

![catálogo](../../../../images/tutorials/create/analytics/catalog.png)

### Selección de datos

La variable **[!UICONTROL Agregar datos de origen de Analytics]** le proporciona una lista de [!DNL Analytics] datos del grupo de informes para crear una conexión de origen.

Un grupo de informes es un contenedor de datos que forma la base de [!DNL Analytics] informes. Una organización puede tener muchos grupos de informes, cada uno con diferentes conjuntos de datos.

Puede ingerir grupos de informes de cualquier región (Estados Unidos, Reino Unido o Singapur) siempre que estén asignados a la misma organización que la instancia de entorno limitado del Experience Platform en la que se está creando la conexión de origen. Un grupo de informes se puede ingerir utilizando un único flujo de datos activo. Ya se ha introducido un grupo de informes que no se puede seleccionar, ya sea en el simulador de pruebas que está utilizando o en otro simulador de pruebas.

Se pueden realizar varias conexiones entrantes para incluir varios grupos de informes en el mismo simulador de pruebas. Si los grupos de informes tienen esquemas diferentes para variables (como eVars o eventos), deben asignarse a campos específicos de los grupos de campos personalizados y evitar conflictos de datos mediante [Preparación de datos](../../../../../data-prep/ui/mapping.md). Los grupos de informes solo se pueden agregar a un solo simulador de pruebas.

![](../../../../images/tutorials/create/analytics/report-suite.png)

>[!NOTE]
>
>Los datos de varios grupos de informes solo se pueden habilitar para el perfil del cliente en tiempo real si no hay conflictos de datos, como dos propiedades personalizadas (eVars, listas y props) que tengan un significado diferente.

Para crear un [!DNL Analytics] conexión de origen, seleccione un grupo de informes y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![](../../../../images/tutorials/create/analytics/add-data.png)

<!---Analytics Report Suites can be configured for one sandbox at a time. To import the same Report Suite into a different sandbox, the dataset flow will have to be deleted and instantiated again via configuration for a different sandbox.--->

### Asignación

>[!IMPORTANT]
>
>Las transformaciones de la preparación de datos pueden añadir latencia al flujo de datos general. La latencia adicional añadida varía según la complejidad de la lógica de transformación.

Antes de poder asignar su [!DNL Analytics] para dirigirse al esquema XDM, primero debe seleccionar si utiliza un esquema predeterminado o uno personalizado.

Un esquema predeterminado crea un nuevo esquema en su nombre, que contiene la variable [!DNL Adobe Analytics ExperienceEvent Template] grupo de campos. Para utilizar un esquema predeterminado, seleccione **[!UICONTROL Esquema predeterminado]**.

![default-schema](../../../../images/tutorials/create/analytics/default-schema.png)

Con un esquema personalizado, puede elegir cualquier esquema disponible para su [!DNL Analytics] siempre que ese esquema tenga la variable [!DNL Adobe Analytics ExperienceEvent Template] grupo de campos. Para utilizar un esquema personalizado, seleccione **[!UICONTROL Esquema personalizado]**.

![custom-schema](../../../../images/tutorials/create/analytics/custom-schema.png)

La variable [!UICONTROL Asignación] proporciona una interfaz para asignar campos de origen a los campos de esquema de destino correspondientes. Desde aquí, puede asignar variables personalizadas a nuevos grupos de campos de esquema y aplicar cálculos según lo admite la preparación de datos. Seleccione un esquema de destino para iniciar el proceso de asignación.

>[!TIP]
>
>Solo los esquemas que tienen la variable [!DNL Adobe Analytics ExperienceEvent Template] el grupo de campos se muestra en el menú de selección de esquema. Se omiten otros esquemas. Si no hay esquemas adecuados disponibles para los datos del grupo de informes, debe crear un esquema nuevo. Para ver los pasos detallados sobre la creación de esquemas, consulte la guía de [creación y edición de esquemas en la interfaz de usuario](../../../../../xdm/ui/resources/schemas.md).

![select-schema](../../../../images/tutorials/create/analytics/select-schema.png)

La variable [!UICONTROL Asignación de campos estándar] muestra los paneles para [!UICONTROL Asignaciones estándar aplicadas], [!UICONTROL Asignaciones estándar no coincidentes] y [!UICONTROL Asignaciones personalizadas]. Consulte la siguiente tabla para obtener información específica sobre cada categoría:

| Asignación de campos estándar | Descripción |
| --- | --- |
| [!UICONTROL Asignaciones estándar aplicadas] | La variable [!UICONTROL Asignaciones estándar aplicadas] muestra el número total de atributos asignados. Las asignaciones estándar hacen referencia a conjuntos de asignaciones entre todos los atributos del origen [!DNL Analytics] datos y atributos correspondientes en [!DNL Analytics] grupo de campos. Están preasignados y no se pueden editar. |
| [!UICONTROL Asignaciones estándar no coincidentes] | La variable [!UICONTROL Asignaciones estándar no coincidentes] hace referencia al número de atributos asignados que contienen conflictos de nombres descriptivos. Estos conflictos aparecen cuando se vuelve a utilizar un esquema que ya tiene un conjunto completo de descriptores de campo de un grupo de informes diferente. Puede continuar con su [!DNL Analytics] flujo de datos incluso con conflictos de nombres descriptivos. |
| [!UICONTROL Asignaciones personalizadas] | La variable [!UICONTROL Asignaciones personalizadas] muestra el número de atributos personalizados asignados, incluidos eVars, props y listas. Las asignaciones personalizadas hacen referencia a conjuntos de asignaciones entre atributos personalizados en el origen [!DNL Analytics] datos y atributos en grupos de campos personalizados incluidos en el esquema seleccionado. |

![map-standard-fields](../../../../images/tutorials/create/analytics/map-standard-fields.png)

Para previsualizar el [!DNL Analytics] Grupo de campos de esquema de plantilla de ExperienceEvent, seleccione **[!UICONTROL Ver]** en el [!UICONTROL Asignaciones estándar aplicadas] panel.

![view](../../../../images/tutorials/create/analytics/view.png)

La variable [!UICONTROL Grupo de campos de esquema de plantilla de Adobe Analytics ExperienceEvent] proporciona una interfaz que se utiliza para inspeccionar la estructura del esquema. Cuando termine, seleccione **[!UICONTROL Cerrar]**.

![field-group-preview](../../../../images/tutorials/create/analytics/field-group-preview.png)

Platform detecta automáticamente los conjuntos de asignaciones para cualquier conflicto de nombres descriptivo. Si no hay conflictos con los conjuntos de asignaciones, seleccione **[!UICONTROL Siguiente]** para continuar.

![asignación](../../../../images/tutorials/create/analytics/mapping.png)

Si hay conflictos de nombres prácticos entre el grupo de informes de origen y el esquema seleccionado, puede continuar con su [!DNL Analytics] flujo de datos, reconociendo que los descriptores de campo no se cambiarán. También puede optar por crear un nuevo esquema con un conjunto de descriptores en blanco.

Select **[!UICONTROL Siguiente]** para continuar.

![precaución](../../../../images/tutorials/create/analytics/caution.png)

#### Asignaciones personalizadas

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
* [Funciones de asignación de preparación de datos](../../../../../data-prep/functions.md)
* [Añadir campos calculados](../../../../../data-prep/ui/mapping.md#calculated-fields)

### Filtrado para [!DNL Profile Service] (Beta) {#filtering-for-profile}

>[!CONTEXTUALHELP]
>id="platform_data_prep_analytics_filtering"
>title="Crear reglas de filtro"
>abstract="Defina las reglas de filtrado de nivel de fila y columna al enviar datos al Perfil del cliente en tiempo real. Utilice el filtrado de nivel de fila para aplicar condiciones y dictar a qué datos **incluir para la ingesta de perfiles**. Utilice el filtrado de nivel de columna para seleccionar las columnas de datos que desea **excluir para la ingesta de perfiles**. Las reglas de filtrado no se aplican a los datos enviados al lago de datos."

>[!IMPORTANT]
>
>Compatibilidad con el filtrado [!DNL Analytics] actualmente los datos están en versión beta y no están disponibles para todos los usuarios. La documentación y las funciones están sujetas a cambios.

Una vez que haya completado las asignaciones para su [!DNL Analytics] datos del grupo de informes, puede aplicar reglas y condiciones de filtrado para incluir o excluir selectivamente los datos de la ingesta a la variable [!DNL Profile Service]. La compatibilidad con el filtrado solo está disponible para [!DNL Analytics] los datos y datos solo se filtran antes de introducirse [!DNL Profile.] Todos los datos se incorporan en el lago de datos.

#### Filtro de nivel de fila

>[!IMPORTANT]
>
>Utilice el filtrado de nivel de fila para aplicar condiciones y dictar a qué datos **incluir para la ingesta de perfiles**. Utilice el filtrado de nivel de columna para seleccionar las columnas de datos que desea **excluir para la ingesta de perfiles**.

Puede filtrar los datos para [!DNL Profile] ingesta en el nivel de fila y columna. El filtrado a nivel de fila permite definir criterios como contiene, es igual a, comienza o termina con. También puede utilizar el filtrado a nivel de fila para unir condiciones mediante `AND` así como `OR`y negar condiciones usando `NOT`.

Para filtrar su [!DNL Analytics] datos en el nivel de fila, seleccione **[!UICONTROL Filtro de fila]**.

![row-filter](../../../../images/tutorials/create/analytics/row-filter.png)

Utilice el carril izquierdo para navegar por la jerarquía de esquemas y seleccione el atributo de esquema que desee para explorar más en profundidad un esquema concreto.

![carril izquierdo](../../../../images/tutorials/create/analytics/left-rail.png)

Una vez identificado el atributo que desea configurar, selecciónelo y arrástrelo del carril izquierdo al panel de filtrado.

![filtering-panel](../../../../images/tutorials/create/analytics/filtering-panel.png)

Para configurar diferentes condiciones, seleccione **[!UICONTROL es igual que]** y, a continuación, seleccione una condición en la ventana desplegable que aparece.

La lista de condiciones configurables incluye:

* [!UICONTROL es igual que]
* [!UICONTROL no es igual]
* [!UICONTROL comienza con]
* [!UICONTROL finaliza con]
* [!UICONTROL no termina con]
* [!UICONTROL contiene]
* [!UICONTROL no contiene]
* [!UICONTROL existe]
* [!UICONTROL no existe]

![condiciones](../../../../images/tutorials/create/analytics/conditions.png)

A continuación, introduzca los valores que desea incluir en función del atributo seleccionado. En el ejemplo siguiente, [!DNL Apple] y [!DNL Google] se seleccionan para su ingesta como parte del **[!UICONTROL Fabricante]** atributo.

![incluir-fabricante](../../../../images/tutorials/create/analytics/include-manufacturer.png)

Para especificar aún más las condiciones de filtrado, añada otro atributo del esquema y, a continuación, añada valores basados en ese atributo. En el ejemplo siguiente, la variable **[!UICONTROL Modelo]** y modelos como el [!DNL iPhone 13] y [!DNL Google Pixel 6] se filtran para su ingesta.

![include-model](../../../../images/tutorials/create/analytics/include-model.png)

Para agregar un contenedor nuevo, seleccione los puntos suspensivos (`...`) en la parte superior derecha de la interfaz de filtrado y, a continuación, seleccione **[!UICONTROL Agregar contenedor]**.

![add-container](../../../../images/tutorials/create/analytics/add-container.png)

Una vez agregado un contenedor nuevo, seleccione **[!UICONTROL Incluir]** y, a continuación, seleccione **[!UICONTROL Excluir]** en la ventana desplegable que aparece.

![excluir](../../../../images/tutorials/create/analytics/exclude.png)

A continuación, complete el mismo proceso arrastrando atributos de esquema y agregando los valores correspondientes que desee excluir del filtrado. En el ejemplo siguiente, la variable [!DNL iPhone 12], [!DNL iPhone 12 mini]y [!DNL Google Pixel 5] se filtran de la exclusión de la **[!UICONTROL Modelo]** , el horizontal se excluye de la función **[!UICONTROL Orientación de la pantalla]** y número de modelo [!DNL A1633] se excluye de **[!UICONTROL Número de modelo]**.

Cuando termine, seleccione **[!UICONTROL Siguiente]**.

![exclude-example](../../../../images/tutorials/create/analytics/exclude-examples.png)

#### Filtro de nivel de columna

Select **[!UICONTROL Filtro de columna]** del encabezado para aplicar el filtrado a nivel de columna.

![column-filter](../../../../images/tutorials/create/analytics/column-filter.png)

La página se actualiza en un árbol de esquema interactivo y muestra los atributos de esquema en el nivel de columna. Desde aquí puede seleccionar las columnas de datos que desea excluir [!DNL Profile] ingesta. Como alternativa, puede expandir una columna y seleccionar atributos específicos para la exclusión.

De forma predeterminada, todas las [!DNL Analytics] vaya a [!DNL Profile] y este proceso permite excluir ramas de datos XDM [!DNL Profile] ingesta.

Cuando termine, seleccione **[!UICONTROL Siguiente]**.

![columnas seleccionadas](../../../../images/tutorials/create/analytics/columns-selected.png)

### Proporcionar detalles de flujo de datos

La variable **[!UICONTROL Detalles de flujo de datos]** , donde debe proporcionar un nombre y una descripción opcional para el flujo de datos. Select **[!UICONTROL Siguiente]** cuando termine.

![dataflow-detail](../../../../images/tutorials/create/analytics/dataflow-detail.png)

### Revisión

La variable [!UICONTROL Consulte] aparece, lo que le permite revisar el nuevo flujo de datos de Analytics antes de crearlo. Los detalles de la conexión se agrupan por categorías, entre ellas:

* [!UICONTROL Conexión]: Muestra la plataforma de origen de la conexión.
* [!UICONTROL Tipo de datos]: Muestra el grupo de informes seleccionado y su ID de grupo de informes correspondiente.

![review](../../../../images/tutorials/create/analytics/review.png)

### Monitorizar el flujo de datos

Una vez creado el flujo de datos, puede monitorizar los datos que se están incorporando a través de él. En el [!UICONTROL Catálogo] pantalla, seleccionar **[!UICONTROL Flujos de datos]** para ver una lista de los flujos establecidos asociados a su cuenta de Analytics.

![select-dataflows](../../../../images/tutorials/create/analytics/select-dataflows.png)

La variable **Flujos de datos** se abre. En esta página hay un par de flujos de conjuntos de datos, incluida información sobre su nombre, datos de origen, tiempo de creación y estado.

El conector crea una instancia de dos flujos de conjuntos de datos. Un flujo representa los datos de relleno y el otro es para los datos activos. Los datos de relleno no están configurados para Perfil, pero se envían al lago de datos para casos analíticos y de ciencia de datos.

Para obtener más información sobre el relleno, los datos activos y sus latencias respectivas, consulte la [Resumen de los conectores de datos de Analytics](../../../../connectors/adobe-applications/analytics.md).

Seleccione el flujo del conjunto de datos que desee ver en la lista.

![select-target-dataset](../../../../images/tutorials/create/analytics/select-target-dataset.png)

La variable **[!UICONTROL Actividad del conjunto de datos]** se abre. Esta página muestra la tasa de consumo de los mensajes en forma de gráfico. Select **[!UICONTROL Administración de datos]** desde el encabezado superior para acceder a los campos de etiquetado.

![actividad del conjunto de datos](../../../../images/tutorials/create/analytics/dataset-activity.png)

Puede ver las etiquetas heredadas de un flujo de datos desde el [!UICONTROL Administración de datos] en el Navegador. Para obtener más información sobre cómo etiquetar datos procedentes de Analytics, visite [guía de etiquetas de uso de datos](../../../../../data-governance/labels/user-guide.md).

![data-gov](../../../../images/tutorials/create/analytics/data-gov.png)

Para eliminar un flujo de datos, vaya a la [!UICONTROL Flujos de datos] y, a continuación, seleccione los puntos suspensivos (`...`) junto al nombre del flujo de datos y, a continuación, seleccione [!UICONTROL Eliminar].

![delete](../../../../images/tutorials/create/analytics/delete.png)

## Pasos siguientes y recursos adicionales

Una vez creada la conexión, el flujo de datos se crea automáticamente para contener los datos entrantes y rellenar un conjunto de datos con el esquema seleccionado. Además, se rellenan los datos de forma retroactiva y se introducen hasta 13 meses de datos históricos. Cuando termina la ingesta inicial, [!DNL Analytics] datos y ser utilizados por servicios de Platform descendentes como [!DNL Real-time Customer Profile] y el servicio de segmentación. Consulte los siguientes documentos para obtener más información:

* [Información general del [!DNL Real-time Customer Profile]](../../../../../profile/home.md)
* [Información general del [!DNL Segmentation Service]](../../../../../segmentation/home.md)
* [Información general del [!DNL Data Science Workspace]](../../../../../data-science-workspace/home.md)
* [Información general del [!DNL Query Service]](../../../../../query-service/home.md)

El siguiente vídeo pretende comprender la ingesta de datos mediante el conector de origen de Adobe Analytics:

>[!WARNING]
>
> La variable [!DNL Platform] La interfaz de usuario que se muestra en el siguiente vídeo no está actualizada. Consulte la documentación anterior para obtener las últimas capturas de pantalla y funciones de la interfaz de usuario.

>[!VIDEO](https://video.tv.adobe.com/v/29687?quality=12&learn=on)
