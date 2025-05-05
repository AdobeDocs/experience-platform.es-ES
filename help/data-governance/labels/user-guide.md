---
keywords: Experience Platform;inicio;temas populares;control de datos;etiqueta de uso de datos;servicio de directivas;guía del usuario sobre etiquetas de uso de datos
solution: Experience Platform
title: Administrar etiquetas de uso de datos en la IU
description: Esta guía describe los pasos para trabajar con las etiquetas de uso de datos en la interfaz de usuario de Adobe Experience Platform.
exl-id: aa44d5cc-416a-4ef2-be14-b4f32aec162c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1552'
ht-degree: 17%

---

# Administración de etiquetas de uso de datos en la IU {#user-guide}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataGovernance_description"
>title="Gobernanza del uso de datos en Experience Platform"
>abstract="<h2>Descripción</h2><p>El marco de Gobernanza de datos de Experience Platform le permite etiquetar atributos y conjuntos de datos según las restricciones de uso de datos, así como establecer directivas que identifiquen y apliquen estas limitaciones para acciones de marketing específicas.</p>"

Esta guía del usuario describe los pasos para trabajar con etiquetas de uso de datos en la interfaz de usuario de [!DNL Experience Platform].

## Administrar etiquetas {#manage-labels}

Para aplicar etiquetas a los datos, necesita el permiso **[!UICONTROL Administrar etiquetas de uso]** para utilizarlo en la zona protegida de producción predeterminada llamada &quot;prod&quot;. Para crear una etiqueta personalizada, también debe tener derechos administrativos en el perfil del producto. Cada organización solo tiene una lista de etiquetas aplicables. Usted **no puede** eliminar etiquetas. En su lugar, puede eliminarlos de los conjuntos de datos o campos a los que se aplican.

Consulte la guía sobre cómo [configurar permisos](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html?lang=es) o la [descripción general del control de acceso](../../access-control/home.md) para obtener más información sobre cómo asignar un permiso. Si no tiene acceso a Admin Console para su organización, póngase en contacto con el administrador de la organización.

## Administrar etiquetas en el nivel de esquema

Puede agregar etiquetas directamente a un esquema o campos dentro de ese esquema. Cualquier campo aplicado en el nivel de esquema se propagará a todos los conjuntos de datos basados en ese esquema.

>[!NOTE]
>
>Si las políticas de uso de datos se crearon antes de etiquetar el campo, puede encontrar un cuadro de diálogo de infracción de política de gobernanza al aplicar etiquetas al nuevo esquema. Este cuadro de diálogo indica que la aplicación de esta etiqueta infringirá una política de uso existente. Utilice el diagrama de linaje de datos para comprender qué otros cambios de configuración se deben realizar antes de agregar la etiqueta al campo de esquema.
>
>![Se ha detectado una infracción de directiva de gobernanza de datos en el cuadro de diálogo con el resumen de la infracción y el diagrama de linaje de datos resaltados.](../images/labels/policy-violation-dialog.png)
>
>Consulte la [documentación de infracción de directiva de uso de datos](../enforcement/auto-enforcement.md#data-usage-violation) para obtener más información sobre las infracciones de directiva.

Para administrar etiquetas de uso de datos en el nivel de esquema, debe seleccionar un esquema existente o crear uno nuevo. Después de iniciar sesión en Adobe Experience Platform, seleccione **[!UICONTROL Esquemas]** en el panel de navegación izquierdo para abrir el área de trabajo **[!UICONTROL Esquemas]**. Esta página lista todos los esquemas creados que pertenecen a su organización, junto con detalles útiles relacionados con cada esquema.

![Interfaz de usuario de Adobe Experience Platform con la ficha Esquema resaltada.](../images/labels/schema-tab.png)

En la siguiente sección se proporcionan los pasos para crear un nuevo esquema al que aplicar etiquetas. Si desea editar etiquetas para un esquema existente, seleccione el esquema de la lista y vaya directamente a [agregar etiquetas de uso de datos al esquema](#add-labels).

### Creación de un nuevo esquema

Para crear un nuevo esquema, seleccione **[!UICONTROL Crear esquema]** en la esquina superior derecha del área de trabajo **[!UICONTROL Esquemas]**. Consulte la guía de [cómo crear un esquema con el Editor de esquemas](../../xdm/tutorials/create-schema-ui.md#create) para obtener instrucciones completas. Como alternativa, puede [crear un esquema mediante la API del Registro de esquemas](../../xdm/tutorials/create-schema-api.md) si es necesario.

### Añadir etiquetas de uso de datos a un esquema {#add-labels-to-schema}

Después de crear un esquema nuevo o seleccionar uno existente en la lista de la ficha [!UICONTROL Examinar] del área de trabajo de [!UICONTROL Esquemas], seleccione un campo del esquema en el Editor de esquemas. En la barra lateral de [!UICONTROL Propiedades del campo], seleccione **[!UICONTROL Aplicar etiquetas de acceso y control de datos]**.

![La pestaña Estructura del espacio de trabajo de esquemas muestra la visualización del esquema con las etiquetas Aplicar acceso y Control de datos resaltadas.](../images/labels/schema-label-governance.png)

Aparece un cuadro de diálogo que le permite aplicar y administrar etiquetas de uso de datos en el nivel de esquema y en el nivel de campo. Consulte el tutorial de XDM para obtener instrucciones completas sobre [cómo añadir o editar etiquetas de uso de datos para esquemas XDM](../../xdm/tutorials/labels.md#select-schema-field).

### Añadir etiquetas de uso de datos a un conjunto de datos específico {#add-labels-to-dataset}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataGovernance_instructions"
>title="Instrucciones"
>abstract="<ol><li>Seleccione <a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/user-guide.html?lang=es">Conjuntos de datos</a> en la navegación de la izquierda y el conjunto de datos cuyos datos desee restringir.</li><li>En la vista de detalles del conjunto de datos, seleccione la pestaña <b>Gobernanza de datos</b>.</li><li>Seleccione los campos del conjunto de datos que desea limitar y, a continuación, <b>Editar etiquetas de gobernanza</b> para etiquetar los datos según las restricciones de uso.</li><li>Después de etiquetar los datos, seleccione <a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/overview.html?lang=es">Directivas</a> en la navegación izquierda y <b>Crear directiva</b>.</li><li>Elija crear una <a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/user-guide.html?lang=es#create-governance-policy">Directiva de gobernanza de datos</a> y, a continuación, las etiquetas de uso de datos que le aplicará.</li><li>Seleccione las acciones de marketing que denegará la directiva para los datos que contengan esas etiquetas. Una vez creada la directiva, selecciónela en la lista y habilítela con el botón de alternancia del carril derecho.</li><li>Para cada directiva habilitada, Experience Platform evita que los datos que contienen las etiquetas especificadas se utilicen para la acción o acciones de marketing definidas. Esta aplicación tiene lugar automáticamente cuando intenta activar datos etiquetados en un destino con acciones de marketing asociadas (casos de uso).</li></ol>"

>[!IMPORTANT]
>
>Las etiquetas ya no se pueden aplicar a campos de nivel de conjunto de datos. Este flujo de trabajo ha quedado obsoleto y favorece la aplicación de etiquetas en el nivel de esquema. Cualquier etiqueta aplicada anteriormente en el nivel de objeto del conjunto de datos seguirá siendo compatible mediante la interfaz de usuario de Experience Platform hasta el 31 de mayo de 2024. Para garantizar que las etiquetas sean coherentes en todos los esquemas, cualquier etiqueta adjunta anteriormente a campos de nivel de conjunto de datos debe migrarse al nivel de esquema durante el próximo año. Consulte la documentación para obtener instrucciones sobre [cómo migrar etiquetas aplicadas anteriormente del conjunto de datos al nivel de esquema](../e2e.md#migrate-labels).

Las etiquetas se pueden aplicar a todo el conjunto de datos desde la pestaña **[!UICONTROL Control de datos]** del área de trabajo **[!UICONTROL Conjuntos de datos]**. El espacio de trabajo de le permite administrar etiquetas de uso de datos en el nivel de conjunto de datos.

![La ficha [!UICONTROL Control de datos] del área de trabajo de [!UICONTROL Conjuntos de datos] con el control de datos resaltado.](../images/labels/dataset-governance.png)

Para editar las etiquetas de uso de datos en el nivel de conjunto de datos, comience por seleccionar el icono de lápiz (![Un icono de lápiz.](/help/images/icons/edit.png)) en la fila del nombre del conjunto de datos.

![La ficha [!UICONTROL Control de datos] del área de trabajo de [!UICONTROL Conjuntos de datos] con el icono de lápiz de edición resaltado.](../images/labels/dataset-level-edit.png)

Se abre el cuadro de diálogo **[!UICONTROL Editar etiquetas de control]**. En el cuadro de diálogo, marque las casillas junto a las etiquetas que desee aplicar al conjunto de datos. Recuerde que todos los campos del conjunto de datos heredarán estas etiquetas. El encabezado **[!UICONTROL Etiquetas aplicadas]** se actualiza a medida que marca cada casilla y muestra las etiquetas que ha elegido. Una vez seleccionadas las etiquetas deseadas, seleccione **[!UICONTROL Guardar cambios]**.

![Cuadro de diálogo Editar etiquetas de control con casillas de verificación de etiqueta y Guardar cambios resaltados.](../images/labels/apply-labels-dataset.png)

El área de trabajo **[!UICONTROL Control de datos]** vuelve a aparecer y muestra las etiquetas que ha aplicado en el nivel de conjunto de datos en la fila inicial de la tabla. También puede ver las etiquetas, indicadas por tarjetas individuales, que se heredan hasta cada uno de los campos dentro del conjunto de datos.

![La ficha [!UICONTROL Control de datos] del área de trabajo de [!UICONTROL Conjuntos de datos] con etiquetas de nivel de conjunto de datos aplicadas y etiquetas de campo de conjunto de datos heredado resaltadas.](../images/labels/applied-dataset-labels.png)

### Eliminación de etiquetas de un conjunto de datos {#remove-labels-from-a-dataset}

Las etiquetas agregadas en el nivel de conjunto de datos tienen una &quot;x&quot; junto a su tarjeta. Esto le permite eliminar las etiquetas de todo el conjunto de datos. Las etiquetas heredadas junto a cada campo no tienen una &quot;x&quot; junto a ellas y aparecen &quot;atenuadas&quot;. Estas **etiquetas heredadas son de solo lectura**, lo que significa que no se pueden eliminar ni editar en el nivel de campo.

<!-- ## View labels at the dataset field level {#view-labels-at-dataset-field-level} -->

<!-- To view labels inherited by the dataset from the schema level, select **[!UICONTROL Datasets]** to navigate to the datasets workspace and select the relevant dataset from the list. 

![The Browse tab of the Datasets workspace with Datasets highlighted in the left sidebar.](../images/labels/dataset-navigation.png)

Next, select the **[!UICONTROL Data Governance]** tab to show the labels that have been applied to the dataset. You can also see that the labels are inherited down to each of the fields within the dataset.

![Dataset Labels inherited by fields](../images/labels/dataset-labels-applied.png)

The inherited labels beside each field do not have an "x" next to them and appear "greyed out" with no ability to remove or edit. This is because **inherited fields are read-only**, meaning they cannot be removed at the field level. -->

<!--Beleive can cut above here  -->

La opción **[!UICONTROL Mostrar etiquetas heredadas]** está activada de forma predeterminada, lo que le permite ver cualquier etiqueta heredada desde el esquema a sus campos. Al desactivar, se ocultan las etiquetas heredadas dentro del conjunto de datos.

![Pestaña Control de datos del área de trabajo Conjuntos de datos con la opción Mostrar etiquetas heredadas resaltada.](../images/labels/inherited-labels.png)

<!-- Labels applied to the dataset appear in read-only form within the **[!UICONTROL Data Governance]** view for that dataset. 

![The Data Governance tab of the Datasets workspace with labels highlighted.](../images/labels/read-only-governance-labels.png) -->

>[!NOTE]
>
>Las etiquetas que se aplicaban antes de que la función de etiquetado de conjuntos de datos quedara obsoleta se pueden eliminar del conjunto de datos buscando el conjunto de datos correspondiente y seleccionando el icono Cancelar de la etiqueta.
>![Pestaña Control de datos del área de trabajo Conjuntos de datos con una etiqueta eliminable resaltada.](../images/labels/remove-governance-labels.png)
>Consulte la documentación para obtener instrucciones sobre [cómo migrar etiquetas aplicadas anteriormente del conjunto de datos al nivel de esquema](../e2e.md#migrate-labels).

## Administración de etiquetas personalizadas {#manage-custom-labels}

>[!CONTEXTUALHELP]
>id="platform_governance_createlabels"
>title="Creación de etiquetas"
>abstract="Las etiquetas permiten clasificar los conjuntos de datos y campos según las directivas de uso que se aplican a esos datos. Experience Platform proporciona un conjunto estándar de etiquetas que puede utilizar, pero también puede crear etiquetas personalizadas específicas para su organización."

Puede crear sus propias etiquetas de uso personalizadas en el área de trabajo **[!UICONTROL Políticas]** de la interfaz de usuario de [!DNL Experience Platform]. Seleccione **[!UICONTROL Directivas]** en el panel de navegación izquierdo y, a continuación, seleccione **[!UICONTROL Etiquetas]** para ver una lista de etiquetas existentes. Aquí, seleccione **[!UICONTROL Crear etiqueta]**.

![Área de trabajo de directivas con la directiva de creación resaltada.](../images/labels/create-label-btn.png)

Aparecerá el cuadro de diálogo **[!UICONTROL Crear etiqueta]**. A partir de aquí, proporcione la siguiente información para la nueva etiqueta:

* **[!UICONTROL Nombre]**: Identificador único de la etiqueta. Este valor se utiliza con fines de búsqueda y, por lo tanto, debe ser corto y conciso.
* **[!UICONTROL Nombre descriptivo]**: Un nombre descriptivo para mostrar para la etiqueta.
* **[!UICONTROL Descripción]**: (Opcional) Una descripción de la etiqueta para proporcionar contexto adicional.

Cuando termine, seleccione **[!UICONTROL Crear]**.

![Cuadro de diálogo Crear etiqueta del área de trabajo de directivas con Crear resaltado.](../images/labels/create-label-dialog.png)

El cuadro de diálogo se cierra y la etiqueta personalizada recién creada aparece en la lista de la ficha **[!UICONTROL Etiquetas]**.

![Pestaña Etiquetas del área de trabajo Directivas con la nueva etiqueta personalizada resaltada.](../images/labels/label-created.png)

La etiqueta ahora se puede seleccionar en **[!UICONTROL Etiquetas personalizadas]** al editar etiquetas de uso para conjuntos de datos y campos o al crear directivas de uso de datos.

![Cuadro de diálogo Aplicar etiquetas de acceso y control de datos con las etiquetas personalizadas resaltadas.](../images/labels/add-custom-label.png)

## Pasos siguientes

Ahora que ha agregado etiquetas de uso de datos en el conjunto de datos y nivel de campo, puede empezar a introducir datos en [!DNL Experience Platform]. Para obtener más información, comience por leer la [documentación de ingesta de datos](../../ingestion/home.md).

Ahora también puede definir políticas de uso de datos basadas en las etiquetas aplicadas. Para obtener más información, consulte la [descripción general de las directivas de uso de datos](../policies/overview.md).

<!-- The workflow of this video is now outdated. This can be enabled once the video has been updated

## Additional resources

The following video is intended to support your understanding of Data Governance, and outlines how to apply labels to a dataset and individual fields.

>[!VIDEO](https://video.tv.adobe.com/v/29709?quality=12&enable10seconds=on&speedcontrol=on) -->
