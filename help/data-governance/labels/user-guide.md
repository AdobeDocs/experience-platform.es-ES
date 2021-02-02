---
keywords: Experience Platform;inicio;temas populares;administración de datos;etiqueta de uso de datos;servicio de políticas;guía del usuario de etiquetas de uso de datos
solution: Experience Platform
title: Guía del usuario de etiquetas de uso de datos
topic: labels
description: Esta guía del usuario describe los pasos para trabajar con etiquetas de uso de datos en la interfaz de usuario de Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 00010d38a5d05800aeac9af8505093fee3593b45
workflow-type: tm+mt
source-wordcount: '1136'
ht-degree: 0%

---


# Guía del usuario de etiquetas de uso de datos

Esta guía del usuario cubre los pasos para trabajar con etiquetas de uso de datos dentro de la interfaz de usuario [!DNL Experience Platform]. Antes de utilizar la guía, consulte la [[!DNL Data Governance] información general](../home.md) para obtener una introducción más sólida al [!DNL Data Governance] marco de trabajo.

## Administración de etiquetas de uso de datos en el nivel de conjunto de datos

Para administrar las etiquetas de uso de datos en el nivel de conjunto de datos, debe seleccionar un conjunto de datos existente o crear uno nuevo. Después de iniciar sesión en Adobe Experience Platform, seleccione **[!UICONTROL Datasets]** en el panel de navegación izquierdo para abrir el área de trabajo **[!UICONTROL Datasets]**. Esta página lista todos los conjuntos de datos creados que pertenecen a su organización, junto con detalles útiles relacionados con cada conjunto de datos.

![Ficha Conjunto de datos dentro de Área de datos](../images/labels/datasets.png)

En la siguiente sección se proporcionan los pasos para crear un nuevo conjunto de datos al que aplicar etiquetas. Si desea editar las etiquetas de un conjunto de datos existente, seleccione el conjunto de datos de la lista y vaya a [agregar las etiquetas de uso de datos al conjunto de datos](#add-labels).

### Crear un nuevo conjunto de datos

>[!NOTE]
>
>En este ejemplo, se crea un conjunto de datos con un esquema preconfigurado [!DNL Experience Data Model] (XDM). Para obtener más información sobre los esquemas XDM, consulte la [descripción general del sistema XDM](../../xdm/home.md) y [conceptos básicos de la composición de esquema](../../xdm/schema/composition.md).

Para crear un nuevo conjunto de datos, seleccione **[!UICONTROL Crear conjunto de datos]** en la esquina superior derecha del espacio de trabajo **[!UICONTROL Conjuntos de datos]**.

![](../images/labels/create_dataset.png)

Aparece la pantalla **[!UICONTROL Crear conjunto de datos]**. Desde aquí, seleccione **[!UICONTROL Crear conjunto de datos a partir de Esquema]**.

![Crear conjunto de datos a partir de Esquema](../images/labels/dataset_create.png)

Aparece la pantalla **[!UICONTROL Seleccionar Esquema]**, que lista todos los esquemas disponibles que puede utilizar para crear un conjunto de datos. Seleccione el botón de radio situado junto a un esquema para seleccionarlo. La sección **[!UICONTROL Esquemas]** del lado derecho muestra detalles adicionales sobre el esquema seleccionado. Una vez que haya seleccionado un esquema, seleccione **[!UICONTROL Siguiente]**.

![Seleccionar Esquema de conjunto de datos](../images/labels/dataset_schema.png)

Aparece la pantalla **[!UICONTROL Configurar conjunto de datos]**. Proporcione un nombre (obligatorio) y una descripción (opcional, pero recomendada) para el nuevo conjunto de datos y, a continuación, seleccione **[!UICONTROL Finalizar]**.

![Configurar conjunto de datos con nombre y descripción](../images/labels/dataset_configure.png)

Se abre la página **[!UICONTROL Actividad del conjunto de datos]**, que muestra información sobre el conjunto de datos recién creado. En este ejemplo, el conjunto de datos se denomina &quot;Miembros de lealtad&quot;, por lo que la navegación superior muestra **Conjuntos de datos > Miembros de lealtad**.

![Página Actividad de conjunto de datos](../images/labels/dataset_activity.png)

### Añadir etiquetas de uso de datos en el conjunto de datos {#add-labels}

Después de crear un nuevo conjunto de datos o seleccionar un conjunto de datos existente de la lista en el área de trabajo **[!UICONTROL Datasets]**, seleccione **[!UICONTROL Data Governance]** para abrir el área de trabajo **[!UICONTROL Data Governance]**. El espacio de trabajo permite administrar etiquetas de uso de datos en el nivel de conjunto de datos y en el nivel de campo.

![Ficha Administración de datos de conjunto de datos](../images/labels/dataset_data_governance.png)

Para editar las etiquetas de uso de datos en el nivel de conjunto de datos, seleccione el inicio del lápiz junto al nombre del conjunto de datos.

![Editar etiquetas de nivel de conjunto de datos](../images/labels/dataset_labels_edit_button.png)

Se abre el cuadro de diálogo **[!UICONTROL Editar etiquetas de gobernanza]**. Dentro del cuadro de diálogo, marque las casillas junto a las etiquetas que desee aplicar al conjunto de datos. Recuerde que estas etiquetas serán heredadas por todos los campos dentro del conjunto de datos. El encabezado **[!UICONTROL Etiquetas aplicadas]** se actualiza a medida que marca cada casilla y muestra las etiquetas que ha elegido. Una vez que haya seleccionado las etiquetas que desee, seleccione **[!UICONTROL Guardar cambios]**.

<img alt="Aplicar etiquetas de gobernanza en el nivel de conjunto de datos" src="../images/labels/apply-labels-dataset.png" width="700"><br>

El espacio de trabajo **[!UICONTROL Administración de datos]** vuelve a aparecer, mostrando las etiquetas que ha aplicado en el nivel de conjunto de datos. También puede ver que las etiquetas se heredan a cada uno de los campos dentro del conjunto de datos.

![Etiquetas de conjuntos de datos heredadas por campos](../images/labels/dataset_inherited_labels.png)

Observe que aparece una &quot;x&quot; junto a las etiquetas en el nivel de conjunto de datos, lo que le permite eliminar las etiquetas. Las etiquetas heredadas al lado de cada campo no tienen una &quot;x&quot; junto a ellas y aparecen &quot;atenuadas&quot; sin capacidad para eliminarlas o editarlas. Esto se debe a que **los campos heredados son de sólo lectura**, lo que significa que no se pueden quitar en el nivel de campo.

La opción **[!UICONTROL Mostrar etiquetas heredadas]** está activada de forma predeterminada, lo que permite ver las etiquetas heredadas del conjunto de datos a sus campos. Al desactivar la opción, se ocultan todas las etiquetas heredadas del conjunto de datos.

![Ocultar etiquetas heredadas](../images/labels/hide_inherited_labels.png)

## Administración de etiquetas de uso de datos en el nivel de campo de conjunto de datos

Si continúa el flujo de trabajo para [agregar y editar etiquetas de uso de datos a nivel de conjunto de datos](#add-labels), también puede administrar etiquetas a nivel de campo dentro del área de trabajo **[!UICONTROL Administración de datos]** para ese conjunto de datos.

Para aplicar etiquetas de uso de datos a un campo individual, seleccione la casilla de verificación situada junto al nombre del campo y, a continuación, seleccione **[!UICONTROL Editar etiquetas de gobernanza]**.

![Editar etiquetas de campo](../images/labels/fields_single_field.png)

Aparece el cuadro de diálogo **[!UICONTROL Editar etiquetas de gobernanza]**. El cuadro de diálogo muestra encabezados que muestran campos seleccionados, etiquetas aplicadas y etiquetas heredadas. Observe que las etiquetas heredadas (C2 y C5) aparecen atenuadas en el cuadro de diálogo. Son etiquetas de solo lectura heredadas del nivel de conjunto de datos y, por lo tanto, solo se pueden editar en el nivel de conjunto de datos.

<img alt="Editar etiquetas de gobernabilidad para un campo individual" src="../images/labels/field-label-inheritance.png" width="700"><br>

Seleccione las etiquetas de nivel de campo seleccionando la casilla de verificación situada junto a cada etiqueta que desee utilizar. Al seleccionar etiquetas, el encabezado **[!UICONTROL Etiquetas aplicadas]** se actualiza para mostrar las etiquetas aplicadas a los campos mostrados en el encabezado **[!UICONTROL Campos seleccionados]**. Una vez que haya terminado de seleccionar etiquetas de nivel de campo, seleccione **[!UICONTROL Guardar cambios]**.

<img alt="Aplicar etiquetas de nivel de campo" src="../images/labels/apply-labels-field.png" width="700"><br>

Vuelve a aparecer el espacio de trabajo **[!UICONTROL Administración de datos]**, que ahora muestra las etiquetas de nivel de campo seleccionadas en la fila junto al nombre del campo. Observe que la etiqueta de nivel de campo tiene una &quot;x&quot; junto a ella, lo que le permite quitar la etiqueta.

![Campo que muestra etiquetas de nivel de campo](../images/labels/fields_show_field_level_labels.png)

Puede repetir estos pasos para continuar agregando y editando etiquetas de campo para campos adicionales, incluso seleccionando varios campos para aplicar etiquetas de campo simultáneamente.

![Seleccione varios campos para aplicar etiquetas de nivel de campo simultáneamente.](../images/labels/fields_select_multiple.png)

Es importante recordar que la herencia se mueve sólo desde el nivel superior hacia abajo (conjunto de datos → campos), lo que significa que las etiquetas aplicadas en el nivel de campo no se propagan a otros campos o conjuntos de datos.

## Administración de etiquetas personalizadas

Puede crear sus propias etiquetas de uso personalizadas dentro del espacio de trabajo **[!UICONTROL Directivas]** en la interfaz de usuario [!DNL Experience Platform]. Seleccione **[!UICONTROL Directivas]** en el panel de navegación izquierdo y, a continuación, seleccione **[!UICONTROL Etiquetas]** para vista de una lista de las etiquetas existentes. Desde aquí, seleccione **[!UICONTROL Crear etiqueta]**.

![](../images/labels/create-label-btn.png)

Aparece el cuadro de diálogo **[!UICONTROL Crear etiqueta]**. A partir de aquí, proporcione la siguiente información para la nueva etiqueta:

* **[!UICONTROL Identificador]**: Identificador único de la etiqueta. Este valor se utiliza con fines de búsqueda y, por lo tanto, debe ser corto y conciso.
* **[!UICONTROL Nombre]**: Un nombre descriptivo para la etiqueta.
* **[!UICONTROL Descripción]**: (Opcional) Una descripción de la etiqueta para proporcionar contexto adicional.

Cuando termine, seleccione **[!UICONTROL Crear]**.

![](../images/labels/create-label.png)

El cuadro de diálogo se cierra y la etiqueta personalizada recién creada aparece en la lista en la ficha **[!UICONTROL Etiquetas]**.

![](../images/labels/label-created.png)

La etiqueta ahora se puede seleccionar en **[!UICONTROL Etiquetas personalizadas]** al editar etiquetas de uso para conjuntos de datos y campos, o al crear políticas de uso de datos.

<img src="../images/labels/add-custom-label.png" width="600" /><br>

## Pasos siguientes

Ahora que ha agregado etiquetas de uso de datos a nivel de conjunto de datos y campo, puede empezar a ingestar datos en [!DNL Experience Platform]. Para obtener más información, lea la [documentación de ingestión de datos](../../ingestion/home.md) para obtener inicio.

Ahora también puede definir directivas de uso de datos en función de las etiquetas que haya aplicado. Para obtener más información, consulte la [descripción general de las directivas de uso de datos](../policies/overview.md).

## Recursos adicionales

El siguiente vídeo está diseñado para admitir su comprensión de [!DNL Data Governance] y describe cómo aplicar etiquetas a un conjunto de datos y a campos individuales.

>[!VIDEO](https://video.tv.adobe.com/v/29709?quality=12&enable10seconds=on&speedcontrol=on)
