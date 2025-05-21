---
title: Conectar Adobe Analytics A Experience Platform
description: Aprenda a llevar los datos del grupo de informes de Adobe Analytics a Experience Platform
exl-id: 5ddbaf63-feaa-44f5-b2f2-2d5ae507f423
source-git-commit: 086777a09eec17c94a7e0a5d2db58e4a1f6b523f
workflow-type: tm+mt
source-wordcount: '2731'
ht-degree: 3%

---

# Conectar Adobe Analytics a Experience Platform

Lea esta guía para aprender a utilizar la fuente de Adobe Analytics para introducir los datos del grupo de informes de Analytics en Adobe Experience Platform.

## Introducción 

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* Sistema [Experience Data Model (XDM)](../../../../../xdm/home.md): El marco de trabajo estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
* [Perfil del cliente en tiempo real](../../../../../profile/home.md): Proporciona un perfil de consumidor unificado en tiempo real basado en datos agregados de múltiples fuentes.
* [Zonas protegidas](../../../../../sandboxes/home.md): Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Experience Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

### Terminología clave

Es importante comprender los siguientes términos clave utilizados en este documento:

* **Atributo estándar**: Los atributos estándar son cualquier atributo predefinido por Adobe. Contienen el mismo significado para todos los clientes y están disponibles en los grupos de campos Datos de origen de Analytics y Esquema de Analytics.
* **Atributo personalizado**: Los atributos personalizados son cualquier atributo de la jerarquía de variables personalizada en Analytics. Los atributos personalizados se utilizan dentro de una implementación de Adobe Analytics para capturar información específica en un grupo de informes y pueden diferir en su uso de un grupo de informes a otro. Los atributos personalizados incluyen eVars, props y listas. Consulte la siguiente [documentación de Analytics sobre las variables de conversión](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=es) para obtener más información sobre las eVars.
* **Cualquier atributo de los grupos de campos personalizados**: Los atributos que se originan en grupos de campos creados por clientes están todos definidos por el usuario y no se consideran atributos estándar ni personalizados.

## Navegar por el catálogo de fuentes

>[!NOTE]
>
>Al crear un flujo de datos de origen de Analytics en una zona protegida de producción, se crean dos flujos de datos:
>
>* Un flujo de datos que rellena los datos históricos del grupo de informes con un retraso de 13 meses en el lago de datos. Este flujo de datos finaliza cuando se completa el relleno.
>* Flujo de flujo de datos que envía datos activos al lago de datos y a [!DNL Real-Time Customer Profile]. Este flujo de datos se ejecuta continuamente.

En la interfaz de usuario de Experience Platform, seleccione **[!UICONTROL Sources]** en el panel de navegación izquierdo para acceder al área de trabajo [!UICONTROL Sources]. En la categoría *[!UICONTROL aplicaciones de Adobe]*, seleccione la tarjeta Adobe Analytics y, a continuación, seleccione **[!UICONTROL Agregar datos]**.

![El catálogo de orígenes con la tarjeta de origen de Adobe Analytics seleccionada.](../../../../images/tutorials/create/analytics/catalog.png)

## Seleccionar datos

>[!IMPORTANT]
>
>* Los grupos de informes enumerados en la pantalla pueden provenir de varias regiones. Usted es responsable de comprender las limitaciones y obligaciones de sus datos y de cómo los utiliza en las regiones cruzadas de Adobe Experience Platform. Asegúrese de que su empresa lo permita.
>* Los datos de varios grupos de informes se pueden habilitar para Perfil del cliente en tiempo real solo si no hay conflictos de datos, como dos propiedades personalizadas (eVars, listas y props) con un significado diferente.

Un grupo de informes es un contenedor de datos que forma la base de los informes de Analytics. Una organización puede tener muchos grupos de informes, cada uno con diferentes conjuntos de datos.

Puede ingerir grupos de informes de cualquier región (Estados Unidos, Reino Unido o Singapur) siempre y cuando se asignen a la misma organización que la instancia de zona protegida de Experience Platform en la que se crea la conexión de origen. Un grupo de informes se puede ingerir utilizando un solo flujo de datos activo. Si un grupo de informes es gris y no se puede seleccionar, ya se ha introducido, ya sea en la zona protegida que está utilizando o en una zona protegida diferente.

Se pueden realizar varias conexiones entrantes para colocar varios grupos de informes en la misma zona protegida. Si los grupos de informes tienen distintos esquemas para las variables (como eVars o eventos), deben asignarse a campos específicos en los grupos de campos personalizados y evitar conflictos de datos con [preparación de datos](../../../../../data-prep/ui/mapping.md). Los grupos de informes solo se pueden añadir a una sola zona protegida.

Seleccione **[!UICONTROL Grupo de informes]** y, a continuación, utilice la interfaz de *[!UICONTROL Agregar datos de origen de Analytics]* para navegar por la lista e identificar el grupo de informes de Analytics que desea introducir en Experience Platform. Seleccione **[!UICONTROL Siguiente]** para continuar.

![Se ha seleccionado un grupo de informes de análisis para la ingesta y el botón &quot;Siguiente&quot; está resaltado](../../../../images/tutorials/create/analytics/add-data.png)

&lt;!: los grupos de informes de Analytics se pueden configurar para una zona protegida a la vez. Para importar el mismo grupo de informes en una zona protegida diferente, el flujo del conjunto de datos deberá eliminarse y volver a crearse una instancia mediante la configuración para una zona protegida diferente.—>

## Asignación {#mapping}

>[!IMPORTANT]
>
>Las transformaciones de la preparación de datos pueden añadir latencia al flujo de datos general. La latencia adicional añadida varía en función de la complejidad de la lógica de transformación.

Antes de poder asignar los datos de Analytics al esquema XDM de destino, primero debe determinar si está utilizando un esquema predeterminado o personalizado.

>[!BEGINTABS]

>[!TAB Esquema predeterminado]

Un esquema predeterminado crea un nuevo esquema en su nombre. Este esquema recién creado contiene el grupo de campos [!DNL Adobe Analytics ExperienceEvent Template]. Para usar un esquema predeterminado, seleccione **[!UICONTROL Esquema predeterminado]**.

![Paso de selección de esquema del flujo de trabajo de origen de Analytics, con &quot;Esquema predeterminado&quot; seleccionado.](../../../../images/tutorials/create/analytics/default-schema.png)

>[!TAB Esquema personalizado]

Con un esquema personalizado, puede elegir cualquier esquema disponible para los datos de Analytics, siempre y cuando ese esquema tenga el grupo de campos [!DNL Adobe Analytics ExperienceEvent Template]. Para usar un esquema personalizado, seleccione **[!UICONTROL Esquema personalizado]**.

![Paso de selección de esquema del flujo de trabajo de origen de Analytics, con &quot;Esquema personalizado&quot; seleccionado.](../../../../images/tutorials/create/analytics/custom-schema.png)

>[!ENDTABS]

Utilice la interfaz *[!UICONTROL Mapping]* para asignar campos de origen a sus campos de esquema de destino correspondientes. Puede asignar variables personalizadas a nuevos grupos de campos de esquema y aplicar cálculos según lo admitido por la preparación de datos. Seleccione un esquema de destino para iniciar el proceso de asignación.

>[!TIP]
>
>En el menú de selección de esquemas solo se muestran los esquemas que tienen el grupo de campos [!DNL Adobe Analytics ExperienceEvent Template]. Se omiten otros esquemas. Si no hay esquemas adecuados disponibles para los datos del grupo de informes, debe crear un nuevo esquema. Para ver los pasos detallados sobre la creación de esquemas, consulte la guía de [creación y edición de esquemas en la interfaz de usuario](../../../../../xdm/ui/resources/schemas.md).

![Panel de selección de esquema de destino de la interfaz de asignación.](../../../../images/tutorials/create/analytics/select-schema.png)

Puede consultar el panel [!UICONTROL Asignar campos estándar] para ver las métricas de las [!UICONTROL asignaciones estándar aplicadas]. [!UICONTROL Asignaciones estándar con conflictos de nombre de descriptor] y [!DNL Custom mappings].

| Asignar campos estándar | Descripción |
| --- | --- |
| [!UICONTROL Asignaciones estándar aplicadas] | El panel [!UICONTROL Asignaciones estándar aplicadas] muestra la cantidad total de atributos asignados. Las asignaciones estándar hacen referencia a asignaciones entre todos los atributos de los datos de Analytics de origen y los atributos correspondientes del grupo de campos de Analytics. Están preasignados y no se pueden editar. |
| [!UICONTROL Asignaciones estándar con conflictos de nombre de descriptor] | El panel [!UICONTROL Asignaciones estándar con conflictos de nombre de descriptor] hace referencia al número de atributos asignados que contienen conflictos de nombre. Estos conflictos aparecen cuando se reutiliza un esquema que ya tiene un conjunto rellenado de descriptores de campo de un grupo de informes diferente. Puede continuar con el flujo de datos de Analytics incluso con conflictos de nombres. |
| [!UICONTROL Asignaciones personalizadas] | El panel [!UICONTROL Asignaciones personalizadas] muestra el número de atributos personalizados asignados, incluidos eVars, props y listas. Las asignaciones personalizadas hacen referencia a la asignación entre atributos personalizados en los datos de Analytics de origen y atributos en grupos de campos personalizados incluidos en el esquema seleccionado. |

### Asignaciones estándar {#standard-mappings}

Experience Platform detecta automáticamente la asignación para cualquier conflicto de nombres. Si no hay conflictos con sus asignaciones, seleccione **[!UICONTROL Siguiente]** para continuar.

![El encabezado de asignaciones estándar no muestra ningún conflicto de nombres](../../../../images/tutorials/create/analytics/standard.png)

>[!TIP]
>
>Si hay conflictos de nombre entre el grupo de informes de origen y el esquema seleccionado, puede continuar con el flujo de datos de Analytics, reconociendo que los descriptores de campo no se cambiarán. También puede optar por crear un nuevo esquema con un conjunto de descriptores en blanco.

## Asignaciones personalizadas {#custom-mappings}

Puede utilizar las funciones de preparación de datos para agregar nuevas asignaciones personalizadas o campos calculados para atributos personalizados. Para agregar asignaciones personalizadas, seleccione **[!UICONTROL Personalizado]**.

![Ficha de asignación personalizada en el flujo de trabajo de origen de Analytics.](../../../../images/tutorials/create/analytics/custom.png)

* **[!UICONTROL Campos de filtro]**: use la entrada de texto [!UICONTROL Campos de filtro] para filtrar campos de asignación específicos en sus asignaciones.
* **[!UICONTROL Agregar nueva asignación]**: para agregar un nuevo campo de origen y asignación de campo de destino, seleccione **[!UICONTROL Agregar nueva asignación]**.
* **[!UICONTROL Agregar campo calculado]**: Si es necesario, puede seleccionar **[!UICONTROL Agregar campo calculado]** para crear un nuevo campo calculado para sus asignaciones.
* **[!UICONTROL Asignación de importación]**: puede reducir el tiempo de configuración manual del proceso de ingesta de datos y limitar los errores mediante la funcionalidad de asignación de importación de la preparación de datos. Seleccione **[!UICONTROL Importar asignación]** para importar asignaciones de un flujo existente o de un archivo exportado. Para obtener más información, lea [la guía sobre importación y exportación de asignaciones](../../../../../data-prep/ui/mapping.md#import-mapping).
* **[!UICONTROL Descargar plantilla]**: también puede descargar una copia CSV de sus asignaciones y configurar las asignaciones en su dispositivo local. Seleccione **[!UICONTROL Descargar plantilla]** para descargar una copia CSV de sus asignaciones. Debe asegurarse de que solo utiliza los campos proporcionados en el archivo de origen y en el esquema de destino.

Consulte la siguiente documentación para obtener más información sobre la preparación de datos.

* [Resumen de preparación de datos](../../../../../data-prep/home.md)
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

## Filtrado para el perfil del cliente en tiempo real {#filtering-for-profile}

>[!CONTEXTUALHELP]
>id="platform_data_prep_analytics_filtering"
>title="Crear reglas de filtro"
>abstract="Defina las reglas de filtrado de nivel de fila y columna al enviar datos al perfil del cliente en tiempo real. Utilice el filtrado de nivel de fila para aplicar condiciones y dictar qué datos **incluir para la ingesta de perfiles**. Utilice el filtrado de nivel de columna para seleccionar las columnas de datos que desea **excluir para la ingesta de perfiles**. Las reglas de filtrado no se aplican a los datos enviados al lago de datos."

Una vez que haya completado las asignaciones para los datos del grupo de informes de Analytics, puede aplicar reglas y condiciones de filtrado para incluir o excluir selectivamente los datos de la ingesta en el Perfil del cliente en tiempo real. La compatibilidad con el filtrado solo está disponible para datos de Analytics y los datos solo se filtran antes de introducir [!DNL Profile.]. Todos los datos se incorporan al lago de datos.

>[!BEGINSHADEBOX]

**Información adicional sobre preparación de datos y filtrado de datos de Analytics para el perfil del cliente en tiempo real**

* Puede utilizar la funcionalidad de filtrado para los datos que se dirigen a Perfil, pero no para los que se dirigen al lago de datos.
* Puede utilizar el filtrado para los datos activos, pero no puede filtrar los datos de relleno.
   * La fuente de Analytics no rellena los datos en el perfil.
* Si utiliza las configuraciones de la preparación de datos durante la configuración inicial de un flujo de Analytics, esos cambios también se aplican al relleno automático de 13 meses.
   * Sin embargo, este no es el caso del filtrado, ya que solo se reserva para datos activos.
* La preparación de datos se aplica a las rutas de ingesta por flujo continuo y por lotes. Si modifica una configuración de preparación de datos existente, esos cambios se aplican a los nuevos datos entrantes en las rutas de ingesta por flujo continuo y por lotes.
   * Sin embargo, cualquier configuración de la preparación de datos no se aplica a los datos que ya se han introducido en Experience Platform, independientemente de si son datos de flujo continuo o por lotes.
* Los atributos estándar de Analytics siempre se asignan automáticamente. Por lo tanto, no se pueden aplicar transformaciones a atributos estándar.
   * Sin embargo, puede filtrar los atributos estándar siempre que no sean necesarios en el servicio de identidad o en el perfil.
* No se puede utilizar el filtrado a nivel de columna para filtrar los campos obligatorios y los campos de identidad.
* Aunque puede filtrar las identidades secundarias, específicamente AAID y AACustomID, no puede filtrar los ECID.
* Cuando se produce un error de transformación, la columna correspondiente resulta en NULL.

>[!ENDSHADEBOX]

### Filtrado de nivel de fila

>[!IMPORTANT]
>
>Utilice el filtrado de nivel de fila para aplicar condiciones y dictar qué datos **incluir para la ingesta de perfiles**. Use el filtrado a nivel de columna para seleccionar las columnas de datos que desea **excluir para la ingesta de perfiles**.

Puede filtrar los datos para la ingesta de perfiles en los niveles de fila y columna. Utilice el filtrado de nivel de fila para definir criterios como que la cadena contiene, es igual a, comienza o termina con. También puede usar el filtrado de nivel de fila para unir condiciones usando `AND` así como `OR`, y negar condiciones usando `NOT`.

Para filtrar los datos de Analytics en el nivel de fila, seleccione **[!UICONTROL Filtro de fila]** y utilice el carril izquierdo para navegar por la jerarquía de esquema e identificar el atributo de esquema que desee seleccionar.

![Interfaz de filtro de fila para datos de Analytics.](../../../../images/tutorials/create/analytics/row-filter.png)

Una vez identificado el atributo que desea configurar, selecciónelo y arrástrelo del carril izquierdo al panel de filtrado.

![Atributo &quot;Manufacturer&quot; seleccionado para el filtrado.](../../../../images/tutorials/create/analytics/filtering-panel.png)

Para configurar diferentes condiciones, seleccione **[!UICONTROL es igual a]** y luego seleccione una condición en la ventana desplegable que aparece.

La lista de condiciones configurables incluye:

* [!UICONTROL es igual que]
* [!UICONTROL no es igual a]
* [!UICONTROL comienza con]
* [!UICONTROL termina con]
* [!UICONTROL no termina con]
* [!UICONTROL contiene]
* [!UICONTROL no contiene]
* [!UICONTROL existe]
* [!UICONTROL no existe]

![Menú desplegable de condiciones con una lista de operadores de condición.](../../../../images/tutorials/create/analytics/conditions.png)

A continuación, introduzca los valores que desea incluir en función del atributo seleccionado. En el ejemplo siguiente, [!DNL Apple] y [!DNL Google] están seleccionados para su ingesta como parte del atributo **[!UICONTROL Manufacturer]**.

![Panel de filtrado con los atributos y valores seleccionados incluidos.](../../../../images/tutorials/create/analytics/include.png)

Para especificar más las condiciones de filtrado, agregue otro atributo del esquema y, a continuación, agregue valores basados en ese atributo. En el ejemplo siguiente, se agrega el atributo **[!UICONTROL Model]** y los modelos como [!DNL iPhone 16] y [!DNL Google Pixel 9] se filtran para su ingesta.

![Atributos y valores adicionales incluidos en el contenedor.](../../../../images/tutorials/create/analytics/include-model.png)

Para agregar un nuevo contenedor, seleccione los puntos suspensivos (`...`) en la parte superior derecha de la interfaz de filtrado y, a continuación, seleccione **[!UICONTROL Agregar contenedor]**.

![Se seleccionó el menú desplegable &quot;Agregar contenedor&quot;.](../../../../images/tutorials/create/analytics/add-container.png)

Una vez agregado un nuevo contenedor, selecciona **[!UICONTROL Incluir]** y luego selecciona **[!UICONTROL Excluir]** en el menú desplegable. Agregue los atributos y valores que desee excluir y, cuando termine, seleccione **[!UICONTROL Siguiente]**.

![Atributos y valores filtrados para exclusión.](../../../../images/tutorials/create/analytics/exclude.png)

### Filtrado de nivel de columna

Seleccione **[!UICONTROL Filtro de columna]** del encabezado para aplicar el filtrado de nivel de columna.

La página se actualiza a un árbol de esquema interactivo y muestra los atributos de esquema en el nivel de columna. Desde aquí, puede seleccionar las columnas de datos que desea excluir de la Ingesta de perfiles. También puede expandir una columna y seleccionar atributos específicos para la exclusión.

De forma predeterminada, todos los análisis se dirigen a un perfil y este proceso permite excluir las ramas de datos XDM de la ingesta de perfiles.

![Interfaz de filtro de columna con el árbol de esquema.](../../../../images/tutorials/create/analytics/column-filter.png)

### Filtrar identidades secundarias

Utilice un filtro de columna para excluir las identidades secundarias de la ingesta de perfiles. Para filtrar identidades secundarias, seleccione **[!UICONTROL Filtro de columna]** y luego seleccione **[!UICONTROL _identidades]**.

El filtro solo se aplica cuando una identidad se marca como secundaria. Si se seleccionan identidades, pero llega un evento con una de las identidades marcadas como principales, estas no se filtran.

![Identidades secundarias en el árbol de esquema para el filtrado de columnas.](../../../../images/tutorials/create/analytics/secondary-identities.png)

### Proporcionar detalles del flujo de datos

Aparece el paso **[!UICONTROL Detalle del flujo de datos]**, donde debe proporcionar un nombre y una descripción opcional para el flujo de datos. Seleccione **[!UICONTROL Siguiente]** cuando haya terminado.

![Interfaz de detalles del flujo de datos. del flujo de trabajo de ingesta.](../../../../images/tutorials/create/analytics/dataflow-detail.png)

### Revisar

Aparecerá el paso [!UICONTROL Revisar], que le permitirá revisar su nuevo flujo de datos de Analytics antes de crearlo. Los detalles de la conexión se agrupan por categorías, incluidas:

* [!UICONTROL Conexión]: Muestra la plataforma de origen de la conexión.
* [!UICONTROL Tipo de datos]: muestra el grupo de informes seleccionado y su ID de grupo de informes correspondiente.

![Interfaz de revisión del flujo de trabajo de ingesta.](../../../../images/tutorials/create/analytics/review.png)

## Monitorización del flujo de datos {#monitor-your-dataflow}

Una vez completado el flujo de datos, puede usar la interfaz *[!UICONTROL Dataflows]* para supervisar el estado del flujo de datos de Analytics.

Utilice la interfaz [!UICONTROL Actividad del conjunto de datos] para obtener información sobre el progreso de los datos que se envían de Analytics a Experience Platform. La interfaz muestra métricas como el total de registros del mes anterior, el total de registros ingeridos en los últimos siete días y el tamaño de los datos del mes anterior.

El origen crea una instancia de dos flujos de conjuntos de datos. Un flujo representa los datos de relleno y el otro es para los datos activos. Los datos de relleno no están configurados para su incorporación al Perfil del cliente en tiempo real, sino que se envían al lago de datos para casos de uso analíticos y de ciencia de datos.

Para obtener más información sobre el relleno, los datos activos y sus respectivas latencias, lea la [descripción general del origen de Analytics](../../../../connectors/adobe-applications/analytics.md).

![Página de actividad del conjunto de datos de un conjunto de datos de destinatario determinado para los datos de Adobe Analytics.](../../../../images/tutorials/create/analytics/dataset-activity.png)

>[!NOTE]
>
>La página de actividad del conjunto de datos no muestra información sobre los lotes, ya que el conector de origen de Analytics lo administra completamente Adobe. Puede monitorizar que los datos fluyen mirando las métricas alrededor de los registros ingeridos.

## Eliminar el flujo de datos {#delete-dataflow}

Para eliminar el flujo de datos de Analytics, seleccione **[!UICONTROL Flujos de datos]** en el encabezado superior del área de trabajo de orígenes. Utilice la página de flujos de datos para localizar el flujo de datos de Analytics que desea eliminar y, a continuación, seleccione los puntos suspensivos (`...`) que aparecen junto a él. A continuación, usa el menú desplegable y selecciona **[!UICONTROL Eliminar]**.

* Al eliminar el flujo de datos activo de Analytics, también se eliminará su conjunto de datos subyacente.
* Al eliminar el flujo de datos de Analytics de relleno no se elimina el conjunto de datos subyacente, pero se detendrá el proceso de relleno para su grupo de informes correspondiente. Si elimina el flujo de datos de relleno, los datos ingeridos pueden seguir viéndose a través del conjunto de datos.

## Pasos siguientes y recursos adicionales

Una vez creada la conexión, el flujo de datos se crea automáticamente para contener los datos entrantes y rellenar un conjunto de datos con el esquema seleccionado. Además, se rellenan los datos de forma retroactiva y se introducen hasta 13 meses de datos históricos. Cuando se complete la ingesta inicial, los datos de Analytics y los servicios de Experience Platform descendentes, como [!DNL Real-Time Customer Profile] y el servicio de segmentación, los usarán. Consulte los siguientes documentos para obtener más información:

* [Información general de [!DNL Real-Time Customer Profile]](../../../../../profile/home.md)
* [Información general de [!DNL Segmentation Service]](../../../../../segmentation/home.md)
* [Información general de [!DNL Data Science Workspace]](../../../../../data-science-workspace/home.md)
* [Información general de [!DNL Query Service]](../../../../../query-service/home.md)

El siguiente vídeo tiene como objetivo ayudarle a comprender la ingesta de datos mediante el conector de Source de Adobe Analytics:

>[!WARNING]
>
> La interfaz de usuario [!DNL Experience Platform] que se muestra en el siguiente vídeo no está actualizada. Consulte la documentación anterior para obtener las capturas de pantalla y la funcionalidad más recientes de la interfaz de usuario.

>[!VIDEO](https://video.tv.adobe.com/v/3430250?quality=12&learn=on&captions=spa)

