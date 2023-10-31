---
title: Crear una conexión de origen de Adobe Analytics en la interfaz de usuario
description: Obtenga información sobre cómo crear una conexión de origen de Adobe Analytics en la interfaz de usuario para llevar los datos de los consumidores a Adobe Experience Platform.
exl-id: 5ddbaf63-feaa-44f5-b2f2-2d5ae507f423
source-git-commit: 358daa9511f647749a8198893b712d00a5cfbc5d
workflow-type: tm+mt
source-wordcount: '2481'
ht-degree: 6%

---

# Crear una conexión de origen de Adobe Analytics en la interfaz de usuario

Este tutorial proporciona los pasos para crear una conexión de origen de Adobe Analytics en la interfaz de usuario para introducir datos del grupo de informes de Adobe Analytics en Adobe Experience Platform.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [Sistema de modelo de datos de experiencia (XDM)](../../../../../xdm/home.md): El marco estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
* [Perfil del cliente en tiempo real](../../../../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.
* [Zonas protegidas](../../../../../sandboxes/home.md): El Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

### Terminología clave

Es importante comprender los siguientes términos clave utilizados en este documento:

* **Atributo estándar**: los atributos estándar son cualquier atributo predefinido por el Adobe. Contienen el mismo significado para todos los clientes y están disponibles en el [!DNL Analytics] datos de origen y [!DNL Analytics] grupos de campos de esquema.
* **Atributo personalizado**: Los atributos personalizados son cualquier atributo en la jerarquía de variables personalizada en [!DNL Analytics]. Los atributos personalizados se utilizan dentro de una implementación de Adobe Analytics para capturar información específica en un grupo de informes y pueden diferir en su uso de un grupo de informes a otro. Los atributos personalizados incluyen eVars, props y listas. Consulte lo siguiente [[!DNL Analytics] documentación sobre variables de conversión](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=en) para obtener más información sobre las eVars.
* **Cualquier atributo de los grupos de campos personalizados**: todos los atributos que se originan en grupos de campos creados por clientes están definidos por el usuario y se consideran no atributos estándar ni personalizados.
* **Nombres descriptivos**: los nombres descriptivos son etiquetas proporcionadas por humanos para variables personalizadas en un [!DNL Analytics] implementación. Consulte lo siguiente [[!DNL Analytics] documentación sobre variables de conversión](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=en) para obtener más información sobre nombres descriptivos.

## Crear una conexión de origen con Adobe Analytics

>[!NOTE]
>
>Al crear un flujo de datos de origen de Analytics en una zona protegida de producción, se crean dos flujos de datos:
>
>* Un flujo de datos que rellena los datos históricos del grupo de informes con un retraso de 13 meses en el lago de datos. Este flujo de datos finaliza cuando se completa el relleno.
>* Un flujo de datos que envía datos activos al lago de datos y a [!DNL Real-Time Customer Profile]. Este flujo de datos se ejecuta continuamente.

En la IU de Platform, seleccione **[!UICONTROL Fuentes]** desde la navegación izquierda para acceder a [!UICONTROL Fuentes] workspace. El [!UICONTROL Catálogo] La pantalla muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede utilizar la barra de búsqueda para reducir los orígenes mostrados.

En el **[!UICONTROL aplicaciones de Adobe]** categoría, seleccionar **[!UICONTROL Adobe Analytics]** y luego seleccione **[!UICONTROL Añadir datos]**.

![catalogar](../../../../images/tutorials/create/analytics/catalog.png)

### Seleccionar datos

>[!IMPORTANT]
>
>Los grupos de informes enumerados en la pantalla pueden provenir de varias regiones. Usted es responsable de comprender las limitaciones y obligaciones de sus datos y de cómo los utiliza en las regiones cruzadas de Adobe Experience Platform. Asegúrese de que su empresa lo permita.

El **[!UICONTROL Añadir datos de origen de Analytics]** Este paso le proporciona una lista de [!DNL Analytics] datos del grupo de informes para crear una conexión de origen con.

Un grupo de informes es un contenedor de datos que constituye la base de [!DNL Analytics] informes. Una organización puede tener muchos grupos de informes, cada uno con diferentes conjuntos de datos.

Puede ingerir grupos de informes de cualquier región (Estados Unidos, Reino Unido o Singapur) siempre y cuando se asignen a la misma organización que la instancia de zona protegida Experience Platform en la que se crea la conexión de origen. Un grupo de informes se puede ingerir utilizando un solo flujo de datos activo. Ya se ha introducido un grupo de informes que no se puede seleccionar, ya sea en la zona protegida que está utilizando o en una zona protegida diferente.

Se pueden realizar varias conexiones entrantes para colocar varios grupos de informes en la misma zona protegida. Si los grupos de informes tienen distintos esquemas para las variables (como eVars o eventos), deben asignarse a campos específicos en los grupos de campos personalizados y evitar conflictos de datos mediante [Preparación de datos](../../../../../data-prep/ui/mapping.md). Los grupos de informes solo se pueden añadir a una sola zona protegida.

![](../../../../images/tutorials/create/analytics/report-suite.png)

>[!NOTE]
>
>Los datos de varios grupos de informes se pueden habilitar para Perfil del cliente en tiempo real solo si no hay conflictos de datos, como dos propiedades personalizadas (eVars, listas y props) con un significado diferente.

Para crear un [!DNL Analytics] conexión de origen, seleccione un grupo de informes y luego seleccione **[!UICONTROL Siguiente]** para continuar.

![](../../../../images/tutorials/create/analytics/add-data.png)

&lt;!: los grupos de informes de Analytics se pueden configurar para una zona protegida a la vez. Para importar el mismo grupo de informes en una zona protegida diferente, el flujo del conjunto de datos deberá eliminarse y volver a crearse una instancia mediante la configuración para una zona protegida diferente.—>

### Asignación

>[!IMPORTANT]
>
>Las transformaciones de la preparación de datos pueden añadir latencia al flujo de datos general. La latencia adicional añadida varía en función de la complejidad de la lógica de transformación.

Antes de poder asignar su [!DNL Analytics] para segmentar el esquema XDM, primero debe seleccionar si está utilizando un esquema predeterminado o personalizado.

Un esquema predeterminado crea un nuevo esquema en su nombre, que contiene el [!DNL Adobe Analytics ExperienceEvent Template] grupo de campos. Para utilizar un esquema predeterminado, seleccione **[!UICONTROL Esquema predeterminado]**.

![default-schema](../../../../images/tutorials/create/analytics/default-schema.png)

Con un esquema personalizado, puede elegir cualquier esquema disponible para su [!DNL Analytics] datos, siempre que ese esquema tenga el valor [!DNL Adobe Analytics ExperienceEvent Template] grupo de campos. Para utilizar un esquema personalizado, seleccione **[!UICONTROL Esquema personalizado]**.

![custom-schema](../../../../images/tutorials/create/analytics/custom-schema.png)

El [!UICONTROL Asignación] Esta página proporciona una interfaz para asignar campos de origen a sus campos de esquema de destino adecuados. Desde aquí, puede asignar variables personalizadas a nuevos grupos de campos de esquema y aplicar cálculos según sea compatible con la preparación de datos. Seleccione un esquema de destino para iniciar el proceso de asignación.

>[!TIP]
>
>Solo los esquemas que tienen el [!DNL Adobe Analytics ExperienceEvent Template] Los grupos de campos se muestran en el menú de selección de esquema. Se omiten otros esquemas. Si no hay esquemas adecuados disponibles para los datos del grupo de informes, debe crear un nuevo esquema. Para ver los pasos detallados sobre la creación de esquemas, consulte la guía de [creación y edición de esquemas en la interfaz de usuario](../../../../../xdm/ui/resources/schemas.md).

![select-schema](../../../../images/tutorials/create/analytics/select-schema.png)

El [!UICONTROL Asignar campos estándar] La sección muestra paneles para [!UICONTROL Asignaciones estándar aplicadas], [!UICONTROL Asignaciones estándar no coincidentes] y [!UICONTROL Asignaciones personalizadas]. Consulte la siguiente tabla para obtener información específica sobre cada categoría:

| Asignar campos estándar | Descripción |
| --- | --- |
| [!UICONTROL Asignaciones estándar aplicadas] | El [!UICONTROL Asignaciones estándar aplicadas] el panel muestra el número total de atributos asignados. Las asignaciones estándar hacen referencia a conjuntos de asignaciones entre todos los atributos del origen [!DNL Analytics] datos y atributos correspondientes en [!DNL Analytics] grupo de campos. Están preasignados y no se pueden editar. |
| [!UICONTROL Asignaciones estándar no coincidentes] | El [!UICONTROL Asignaciones estándar no coincidentes] panel hace referencia al número de atributos asignados que contienen conflictos de nombres descriptivos. Estos conflictos aparecen cuando se reutiliza un esquema que ya tiene un conjunto rellenado de descriptores de campo de un grupo de informes diferente. Puede continuar con su [!DNL Analytics] flujo de datos incluso con conflictos de nombres descriptivos. |
| [!UICONTROL Asignaciones personalizadas] | El [!UICONTROL Asignaciones personalizadas] El panel muestra el número de atributos personalizados asignados, incluidas eVars, props y listas. Las asignaciones personalizadas hacen referencia a conjuntos de asignaciones entre atributos personalizados en el origen [!DNL Analytics] datos y atributos en grupos de campos personalizados incluidos en el esquema seleccionado. |

![map-standard-fields](../../../../images/tutorials/create/analytics/map-standard-fields.png)

Para obtener una vista previa [!DNL Analytics] grupo de campos de esquema de plantilla ExperienceEvent, seleccione **[!UICONTROL Ver]** en el [!UICONTROL Asignaciones estándar aplicadas] panel.

![view](../../../../images/tutorials/create/analytics/view.png)

El [!UICONTROL Grupo de campos de esquema de plantilla de Adobe Analytics ExperienceEvent] proporciona una interfaz para utilizar para inspeccionar la estructura del esquema. Cuando termine, seleccione **[!UICONTROL Cerrar]**.

![field-group-preview](../../../../images/tutorials/create/analytics/field-group-preview.png)

Platform detecta automáticamente los conjuntos de asignaciones para cualquier conflicto de nombres descriptivos. Si no hay conflictos con los conjuntos de asignaciones, seleccione **[!UICONTROL Siguiente]** para continuar.

![asignación](../../../../images/tutorials/create/analytics/mapping.png)

>[!TIP]
>
>Si existen conflictos de nombres descriptivos entre el grupo de informes de origen y el esquema seleccionado, aún puede continuar con su [!DNL Analytics] flujo de datos, lo que reconoce que los descriptores de campo no se cambiarán. También puede optar por crear un nuevo esquema con un conjunto de descriptores en blanco.

#### Asignaciones personalizadas

Puede utilizar las funciones de preparación de datos para agregar nuevas asignaciones personalizadas o campos calculados para atributos personalizados. Para añadir asignaciones personalizadas, seleccione **[!UICONTROL Personalizado]**.

![personalizado](../../../../images/tutorials/create/analytics/custom.png)

Según sus necesidades, puede seleccionar cualquiera de las siguientes opciones **[!UICONTROL Añadir nueva asignación]** o **[!UICONTROL Añadir campo calculado]** y continúe creando asignaciones personalizadas para los atributos personalizados. Para ver los pasos completos sobre cómo utilizar las funciones de preparación de datos, lea la [Guía de IU de preparación de datos](../../../../../data-prep/ui/mapping.md).

La siguiente documentación proporciona más recursos para comprender la preparación de datos, los campos calculados y las funciones de asignación:

* [Información general de preparación de datos](../../../../../data-prep/home.md)
* [Funciones de asignación de preparación de datos](../../../../../data-prep/functions.md)
* [Añadir campos calculados](../../../../../data-prep/ui/mapping.md#calculated-fields)

<!-- 
To use Data Prep functions and add new mapping or calculated fields for custom attributes, select **[!UICONTROL View custom mappings]**.

![view-custom-mapping](../../../../images/tutorials/create/analytics/view-custom-mapping.png)

Next, select **[!UICONTROL Add new mapping]**.

Depending on your needs, you can select either **[!UICONTROL Add new mapping]** or **[!UICONTROL Add calculated field]** from the options that appear. 

![add-new-mapping](../../../../images/tutorials/create/analytics/add-new-mapping.png)

An empty mapping set appears. Select the mapping icon to add a source field.

![select-source-field](../../../../images/tutorials/create/analytics/select-source-field.png)

You can use the interface to navigate through the source schema structure and identify the new source field that you want to use. Once you have selected the source field that you want to map, select **[!UICONTROL Select]**.

![select-mapping](../../../../images/tutorials/create/analytics/select-mapping.png)

Next, select the mapping icon under [!UICONTROL Target Field] to map your selected source field to its appropriate target field.

![select-target-field](../../../../images/tutorials/create/analytics/select-target-field.png)

Similar to the source schema, you can use the interface to navigate through the target schema structure and select the target field you want to map to. Once you have selected the appropriate target field, select **[!UICONTROL Select]**.

![select-target-mapping](../../../../images/tutorials/create/analytics/select-target-mapping.png)

With your custom mapping set completed, select **[!UICONTROL Next]** to proceed.

![complete-custom-mapping](../../../../images/tutorials/create/analytics/complete-custom-mapping.png) -->

### Filtrado para el perfil del cliente en tiempo real {#filtering-for-profile}

>[!CONTEXTUALHELP]
>id="platform_data_prep_analytics_filtering"
>title="Crear reglas de filtro"
>abstract="Defina las reglas de filtrado de nivel de fila y columna al enviar datos al perfil del cliente en tiempo real. Utilice el filtrado de nivel de fila para aplicar condiciones y dictar qué datos **incluir para la ingesta de perfiles**. Utilice el filtrado de nivel de columna para seleccionar las columnas de datos que desea **excluir para la ingesta de perfiles**. Las reglas de filtrado no se aplican a los datos enviados al lago de datos."

Una vez que haya completado las asignaciones para su [!DNL Analytics] datos del grupo de informes, puede aplicar reglas y condiciones de filtrado para incluir o excluir selectivamente datos de la ingesta en el Perfil del cliente en tiempo real. La compatibilidad con el filtrado solo está disponible para [!DNL Analytics] Los datos de y solo se filtran antes de introducir [!DNL Profile.] Todos los datos se incorporan al lago de datos.

#### Filtrado de nivel de fila

>[!IMPORTANT]
>
>Utilice el filtrado de nivel de fila para aplicar condiciones y dictar qué datos **incluir para la ingesta de perfiles**. Utilice el filtrado de nivel de columna para seleccionar las columnas de datos que desea **excluir para la ingesta de perfiles**.

Puede filtrar los datos de [!DNL Profile] la ingesta a nivel de fila y a nivel de columna. El filtrado de nivel de fila permite definir criterios como que la cadena contiene, es igual a, comienza o termina con. También puede utilizar el filtrado de nivel de fila para unir condiciones mediante `AND` así como `OR`, y niegue condiciones utilizando `NOT`.

Para filtrar su [!DNL Analytics] datos en el nivel de fila, seleccione **[!UICONTROL Filtro de fila]**.

![row-filter](../../../../images/tutorials/create/analytics/row-filter.png)

Utilice el carril izquierdo para navegar por la jerarquía de esquemas y seleccionar el atributo de esquema que desee para explorar en profundidad un esquema determinado.

![carril izquierdo](../../../../images/tutorials/create/analytics/left-rail.png)

Una vez identificado el atributo que desea configurar, selecciónelo y arrástrelo del carril izquierdo al panel de filtrado.

![filtering-panel](../../../../images/tutorials/create/analytics/filtering-panel.png)

Para configurar diferentes condiciones, seleccione **[!UICONTROL igual a]** y, a continuación, seleccione una condición en la ventana desplegable que aparece.

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

A continuación, introduzca los valores que desea incluir en función del atributo seleccionado. En el ejemplo siguiente, [!DNL Apple] y [!DNL Google] se seleccionan para su ingesta como parte de **[!UICONTROL Fabricante]** atributo.

![include-manufacturer](../../../../images/tutorials/create/analytics/include-manufacturer.png)

Para especificar más las condiciones de filtrado, agregue otro atributo del esquema y, a continuación, agregue valores basados en ese atributo. En el ejemplo siguiente, la variable **[!UICONTROL Modelo]** se añade el atributo y modelos como el [!DNL iPhone 13] y [!DNL Google Pixel 6] se filtran para su ingesta.

![include-model](../../../../images/tutorials/create/analytics/include-model.png)

Para añadir un nuevo contenedor, seleccione los puntos suspensivos (`...`), en la parte superior derecha de la interfaz de filtrado, y seleccione **[!UICONTROL Agregar contenedor]**.

![add-container](../../../../images/tutorials/create/analytics/add-container.png)

Una vez agregado un nuevo contenedor, seleccione **[!UICONTROL Incluir]** y luego seleccione **[!UICONTROL Excluir]** en la ventana desplegable que aparece.

![excluir](../../../../images/tutorials/create/analytics/exclude.png)

A continuación, complete el mismo proceso arrastrando los atributos de esquema y agregando sus valores correspondientes que desee excluir del filtrado. En el ejemplo siguiente, la variable [!DNL iPhone 12], [!DNL iPhone 12 mini], y [!DNL Google Pixel 5] se filtran todos de la exclusión del **[!UICONTROL Modelo]** atributo, el horizontal se excluye del **[!UICONTROL Orientación de pantalla]**, y número de modelo [!DNL A1633] se excluye de **[!UICONTROL Número de modelo]**.

Cuando termine, seleccione **[!UICONTROL Siguiente]**.

![exclude-samples](../../../../images/tutorials/create/analytics/exclude-examples.png)

#### Filtrado de nivel de columna

Seleccionar **[!UICONTROL Filtro de columna]** en el encabezado para aplicar el filtrado en el nivel de columna.

![column-filter](../../../../images/tutorials/create/analytics/column-filter.png)

La página se actualiza a un árbol de esquema interactivo y muestra los atributos de esquema en el nivel de columna. Aquí puede seleccionar las columnas de datos que desea excluir de [!DNL Profile] ingesta. También puede expandir una columna y seleccionar atributos específicos para la exclusión.

De forma predeterminada, todas las [!DNL Analytics] ir a [!DNL Profile] y este proceso permite excluir ramas de datos XDM de [!DNL Profile] ingesta.

Cuando termine, seleccione **[!UICONTROL Siguiente]**.

![columns-selected](../../../../images/tutorials/create/analytics/columns-selected.png)

### Proporcionar detalles del flujo de datos

El **[!UICONTROL Detalles del flujo de datos]** , donde debe proporcionar un nombre y una descripción opcional para el flujo de datos. Seleccionar **[!UICONTROL Siguiente]** cuando termine.

![data-flow-detail](../../../../images/tutorials/create/analytics/dataflow-detail.png)

### Consulte

El [!UICONTROL Revisar] Este paso aparece, lo que le permite revisar el nuevo flujo de datos de Analytics antes de crearlo. Los detalles de la conexión se agrupan por categorías, incluidas:

* [!UICONTROL Conexión]: Muestra la plataforma de origen de la conexión.
* [!UICONTROL Tipo de datos]: Muestra el grupo de informes seleccionado y su ID de grupo de informes correspondiente.

![reseña](../../../../images/tutorials/create/analytics/review.png)

## Monitorización del flujo de datos {#monitor-your-dataflow}

Una vez completado el flujo de datos, seleccione **[!UICONTROL Flujos de datos]** en el catálogo de fuentes para monitorizar la actividad y el estado de los datos.

![El catálogo de fuentes con la pestaña de flujos de datos seleccionada.](../../../../images/tutorials/create/analytics/select-dataflows.png)

Aparece una lista de los flujos de datos de Analytics existentes en su organización. Aquí, seleccione un conjunto de datos de destinatario para ver su actividad de ingesta correspondiente.

![Una lista de flujos de datos de Adobe Analytics existentes en su organización.](../../../../images/tutorials/create/analytics/select-target-dataset.png)

El [!UICONTROL Actividad de conjunto de datos] Esta página proporciona información sobre el progreso de los datos que se envían de Analytics a Experience Platform. La interfaz muestra métricas como el número de registros ingeridos, el número de lotes ingeridos y el número de lotes fallidos.

El origen crea una instancia de dos flujos de conjuntos de datos. Un flujo representa los datos de relleno y el otro es para los datos activos. Los datos de relleno no están configurados para su incorporación al Perfil del cliente en tiempo real, sino que se envían al lago de datos para casos de uso analíticos y de ciencia de datos.

Para obtener más información sobre el relleno, los datos activos y sus respectivas latencias, lea la [Resumen de origen de Analytics](../../../../connectors/adobe-applications/analytics.md).

![Página de actividad del conjunto de datos de un conjunto de datos de destinatario determinado para datos de Adobe Analytics.](../../../../images/tutorials/create/analytics/dataset-activity.png)

+++Ver lotes individuales mediante la interfaz de monitorización heredada

La página de actividad del conjunto de datos no muestra una lista de lotes individuales. Para ver una lista de lotes individuales, seleccione un gráfico en la interfaz de actividad del conjunto de datos.

![La página de actividad del conjunto de datos con un gráfico seleccionado.](../../../../images/tutorials/create/analytics/select-chart.png)

Se le redirigirá al panel de monitorización. A continuación, seleccione **[!UICONTROL SOLO ERRORES DE INGESTA: SÍ]** para borrar el filtro y ver una lista de lotes individuales.

![Panel de monitorización con el filtro de error seleccionado.](../../../../images/tutorials/create/analytics/clear-filter.png)

La interfaz se actualiza a una lista de lotes individuales, que incluye información sobre sus métricas respectivas.

![La página de monitorización heredada para datos por lotes.](../../../../images/tutorials/create/analytics/batch-end-to-end.png)

| Métricas | Descripción |
| --- | --- |
| ID de lote | El ID de un lote determinado. Este valor se genera internamente. |
| Nombre del conjunto de datos | Nombre de un conjunto de datos determinado que se utiliza para los datos de Analytics. |
| Fuente | Origen de los datos introducidos. |
| Actualizado   | La fecha de la iteración de ejecución de flujo más reciente. |
| Registros en conjunto de datos | Recuento total de registros en el conjunto de datos. **Nota**: este parámetro muestra ocasionalmente un estado de `in-progress`. Este estado indica que el proceso de ingesta de registros aún no ha finalizado. |
| Nuevos fragmentos de perfil | Recuento total de nuevos fragmentos de perfil que se ingirieron. |
| Fragmentos de perfil existentes | Recuento total de fragmentos de perfil existentes. |
| Registros de identidad vinculados | El recuento total de registros de identidad que se vincularon después de la ingesta. |
| Registros en el perfil | Recuento total de registros que se ingirieron en el perfil del cliente en tiempo real. |

{style="table-layout:auto"}

+++

## Pasos siguientes y recursos adicionales

Una vez creada la conexión, el flujo de datos se crea automáticamente para contener los datos entrantes y rellenar un conjunto de datos con el esquema seleccionado. Además, se rellenan los datos de forma retroactiva y se introducen hasta 13 meses de datos históricos. Cuando finaliza la ingesta inicial, [!DNL Analytics] y puedan ser utilizados por servicios de Platform secundarios como [!DNL Real-Time Customer Profile] y el servicio de segmentación. Consulte los siguientes documentos para obtener más información:

* [Información general del [!DNL Real-Time Customer Profile]](../../../../../profile/home.md)
* [Información general del [!DNL Segmentation Service]](../../../../../segmentation/home.md)
* [Información general del [!DNL Data Science Workspace]](../../../../../data-science-workspace/home.md)
* [Información general del [!DNL Query Service]](../../../../../query-service/home.md)

El siguiente vídeo tiene como objetivo ayudarle a comprender la ingesta de datos mediante el conector de origen de Adobe Analytics:

>[!WARNING]
>
> El [!DNL Platform] La interfaz de usuario que se muestra en el siguiente vídeo no está actualizada. Consulte la documentación anterior para obtener las capturas de pantalla y la funcionalidad más recientes de la interfaz de usuario.

>[!VIDEO](https://video.tv.adobe.com/v/29687?quality=12&learn=on)
