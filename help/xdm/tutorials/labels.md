---
title: Administración de etiquetas de uso de datos para un esquema
description: Obtenga información sobre cómo añadir etiquetas de uso de datos a los campos del Modelo de datos de experiencia (XDM esquema) en los campos del IU Adobe Experience Platform.
exl-id: 92284bf7-f034-46cc-b905-bdfb9fcd608a
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 9%

---

# Administración de etiquetas de uso de datos para una esquema

Todos los datos que se incorporan a Adobe Experience Platform están restringidos por esquemas del Modelo de datos de experiencia (XDM). Estos datos pueden estar sujetos a restricciones de uso definidas por su organización o por la normativa legal. Para cuenta esto, el Experience Platform permite restringir el uso de ciertos conjuntos de datos y campos mediante el uso de etiquetas de uso de [datos](../../data-governance/labels/overview.md).

Una etiqueta aplicada a un campo de esquema indica las políticas de uso que se aplican a los datos contenidos en ese campo específico.

Las etiquetas se pueden aplicar a esquemas y campos individuales dentro de esos esquemas. Cuando las etiquetas se aplican directamente a un esquema, esas etiquetas se propagan a todos los conjuntos de datos existentes y futuros basados en ese esquema.

Además, cualquier etiqueta de campo que agregue en un esquema se propaga a todos los demás esquemas que emplean el mismo campo desde una clase o grupo de campos compartidos. Esto ayuda a garantizar que las reglas de uso para campos similares sean coherentes en todo el modelo de datos.

Este tutorial trata los pasos para agregar etiquetas a un esquema mediante el Editor de esquemas en la interfaz de usuario de Experience Platform.

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../home.md): El marco de trabajo estandarizado según el cual [!DNL Experience Platform] organiza experiencia del cliente datos.
   * [Editor](../ui/overview.md) de esquemas: aprenda a crear y administrar esquemas y otros recursos en el IU Experience Platform.
* [[!DNL Adobe Experience Platform Data Governance]](../../data-governance/home.md): proporciona la infraestructura para aplicar restricciones de uso de datos en Experience Platform operaciones, mediante directivas que definen qué acciones de marketing se pueden (o no) realizar en datos etiquetados.

## Seleccione un esquema o campo al que añadir etiquetas {#select-schema-field}

>[!CONTEXTUALHELP]
>id="platform_schemas_editgovernancelabels"
>title="Editar etiquetas de gobernanza"
>abstract="Añada una etiqueta a un campo de esquema para indicar las directivas de uso que se aplican a los datos contenidos en ese campo específico."

Para empezar a agregar etiquetas, primero debe [seleccionar un esquema existente para editar](../ui/resources/schemas.md#edit) o [crear un nuevo esquema](../ui/resources/schemas.md#create) para ver su estructura en el Editor de esquemas.

Para editar las etiquetas de un campo individual, puede seleccionar el campo en el lienzo y luego seleccionar **[!UICONTROL Manage access]** en el carril derecho.

>[!IMPORTANT]
>
>Se puede aplicar un máximo de 300 etiquetas a cualquier esquema.

![Seleccione un campo del lienzo del Editor de esquemas](../images/tutorials/labels/manage-access.png)

También puede seleccionar la ficha **[!UICONTROL Labels]**, elegir el campo deseado de la lista y seleccionar **[!UICONTROL Apply Access and Data Governance Labels]** en el carril derecho.

![Seleccione un campo del [!UICONTROL Labels] pestaña](../images/tutorials/labels/select-field-on-labels-tab.png)

Para editar las etiquetas de todo el esquema, en la **[!UICONTROL Labels]** pestaña, seleccione la casilla situada debajo del icono de filtro. Se seleccionan todos los campos disponibles en el esquema. Siguiente, seleccione **[!UICONTROL Apply Access and Data Governance Labels]** en el carril derecho.

![Seleccione el nombre esquema en el [!UICONTROL Labels] pestaña](../images/tutorials/labels/select-schema-on-labels-tab.png)

>[!NOTE]
>
>Cuando intenta editar por primera vez las etiquetas de un esquema o campo, aparece un mensaje de exención de responsabilidad que explica cómo el uso de etiquetas afecta a las operaciones descendentes en función de las políticas de su organización. Seleccione **[!UICONTROL Proceed]** para continuar editando.
>
>![Exención de responsabilidad por uso de etiquetas](../images/tutorials/labels/disclaimer.png)

## Editar las etiquetas del esquema o campo {#edit-labels}

Aparece un cuadro de diálogo que le permite editar las etiquetas del campo seleccionado. Si ha seleccionado un campo de tipo de objeto individual, el carril derecho muestra los subcampos a los que se propagarán las etiquetas aplicadas.

![Se resaltó el cuadro de diálogo Aplicar etiquetas de acceso y control de datos con los campos seleccionados.](../images/tutorials/labels/edit-labels.png)

>[!NOTE]
>
>Si está editando campos para todo el esquema, el carril derecho no muestra los campos aplicables y muestra el nombre del esquema en su lugar.

Utilice el lista mostrado para seleccionar las etiquetas que desea añadir al esquema o al campo. A medida que se eligen las etiquetas, la **[!UICONTROL Applied labels]** sección se actualiza para mostrar las etiquetas que se han seleccionado hasta el momento.

![Cuadro de diálogo Etiquetas de acceso y control de datos de Aplicar con las etiquetas aplicadas resaltadas.](../images/tutorials/labels/applied-labels.png)

Para filtrar las etiquetas mostradas por tipo, seleccione la categoría que desee en el carril izquierdo. Para crear una nueva etiqueta personalizada, seleccione **[!UICONTROL Create label]**.

![Se ha aplicado el cuadro de diálogo Aplicar etiquetas de acceso y control de datos con un filtro de tipo de etiqueta y se ha resaltado la etiqueta Crear.](../images/tutorials/labels/filter-and-create-custom.png)

Una vez que esté satisfecho con las etiquetas seleccionadas, seleccione **[!UICONTROL Save]** para aplicarlas al campo o esquema.

![Se resaltó el cuadro de diálogo Aplicar etiquetas de acceso y control de datos con Guardar.](../images/tutorials/labels/save-labels.png)

La pestaña **[!UICONTROL Labels]** vuelve a aparecer y muestra las etiquetas aplicadas al esquema.

![La pestaña Etiquetas del espacio de trabajo de esquemas con las etiquetas de campo aplicadas resaltadas.](../images/tutorials/labels/field-labels-added.png)

## Próximos pasos

En este guía se explica cómo administrar etiquetas de uso de datos para esquemas y campos. Para obtener información sobre la administración de etiquetas de uso de datos, incluido cómo agregarlas a conjuntos de datos específicos en lugar de al nivel de esquema, consulte las etiquetas de [uso de datos IU guía](../../data-governance/labels/user-guide.md).
