---
title: Administración de etiquetas de uso de datos para un esquema
description: Aprenda a añadir etiquetas de uso de datos a los campos de esquema del modelo de datos de experiencia (XDM) en la interfaz de usuario de Adobe Experience Platform.
exl-id: 92284bf7-f034-46cc-b905-bdfb9fcd608a
source-git-commit: 6fe11b909369797e96d8fa52542ebd5761a27b03
workflow-type: tm+mt
source-wordcount: '806'
ht-degree: 8%

---

# Administración de etiquetas de uso de datos para un esquema

>[!IMPORTANT]
>
>El etiquetado basado en esquemas forma parte de [control de acceso basado en atributos](../../access-control/abac/overview.md), que actualmente está disponible en una versión limitada para clientes de atención médica residentes en Estados Unidos. Esta funcionalidad estará disponible para todos los clientes de Adobe Real-time Customer Data Platform una vez que se publique por completo.

Todos los datos introducidos en Adobe Experience Platform están restringidos por esquemas XDM (Experience Data Model). Estos datos pueden estar sujetos a restricciones de uso definidas por su organización o por la normativa legal. Para tener en cuenta esto, la plataforma le permite restringir el uso de ciertos conjuntos de datos y campos mediante el uso de [etiquetas de uso de datos](../../data-governance/labels/overview.md).

Una etiqueta aplicada a un campo de esquema indica las políticas de uso que se aplican a los datos contenidos en ese campo específico.

Las etiquetas se pueden aplicar a esquemas y campos individuales dentro de esos esquemas. Cuando las etiquetas se aplican directamente a un esquema, esas etiquetas se propagan a todos los conjuntos de datos existentes y futuros basados en ese esquema.

Además, cualquier etiqueta de campo que agregue en un esquema se propaga a todos los demás esquemas que emplean el mismo campo desde una clase o grupo de campos compartidos. Esto ayuda a garantizar que las reglas de uso para campos similares sean coherentes en todo el modelo de datos.

Este tutorial trata los pasos para agregar etiquetas a un esquema mediante el Editor de esquemas en la interfaz de usuario de Platform.

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../home.md): El marco estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Editor de esquemas](../ui/overview.md): Aprenda a crear y administrar esquemas y otros recursos en la IU de Platform.
* [[!DNL Adobe Experience Platform Data Governance]](../../data-governance/home.md): Proporciona la infraestructura para aplicar restricciones de uso de datos en operaciones de Platform, mediante directivas que definen qué acciones de marketing se pueden (o no) realizar en datos etiquetados.

## Seleccione un esquema o campo al que añadir etiquetas {#select-schema-field}

>[!CONTEXTUALHELP]
>id="platform_schemas_editgovernancelabels"
>title="Editar etiquetas de gobernanza"
>abstract="Añada una etiqueta a un campo de esquema para indicar las directivas de uso que se aplican a los datos contenidos en ese campo específico."

Para empezar a añadir etiquetas, primero debe [seleccione un esquema existente para editarlo](../ui/resources/schemas.md#edit) o [crear un nuevo esquema](../ui/resources/schemas.md#create) para ver su estructura en el Editor de esquemas.

Para editar las etiquetas de un campo individual, puede seleccionar el campo en el lienzo y luego seleccionar **[!UICONTROL Administrar acceso]** en el carril derecho.

>[!IMPORTANT]
>
>Se puede aplicar un máximo de 300 etiquetas a cualquier esquema.

![Seleccione un campo del lienzo del Editor de esquemas](../images/tutorials/labels/manage-access.png)

También puede seleccionar la variable **[!UICONTROL Etiquetas]** , elija el campo que desee en la lista y seleccione **[!UICONTROL Aplicar etiquetas de acceso y de gobernanza de datos]** en el carril derecho.

![Seleccione un campo de la [!UICONTROL Etiquetas] pestaña](../images/tutorials/labels/select-field-on-labels-tab.png)

Para editar las etiquetas para todo el esquema, en la variable **[!UICONTROL Etiquetas]** , seleccione la casilla de verificación situada debajo del icono de filtro. Esto selecciona todos los campos disponibles en el esquema. A continuación, seleccione **[!UICONTROL Aplicar etiquetas de acceso y de gobernanza de datos]** en el carril derecho.

![Seleccione el nombre del esquema en la lista [!UICONTROL Etiquetas] pestaña](../images/tutorials/labels/select-schema-on-labels-tab.png)

>[!NOTE]
>
>Cuando intenta editar por primera vez las etiquetas de un esquema o campo, aparece un mensaje de exención de responsabilidad que explica cómo el uso de etiquetas afecta a las operaciones descendentes en función de las políticas de su organización. Seleccionar **[!UICONTROL Continuar]** para continuar editando.
>
>![Exención de responsabilidad por uso de etiquetas](../images/tutorials/labels/disclaimer.png)

## Editar las etiquetas del esquema o campo {#edit-labels}

Aparece un cuadro de diálogo que le permite editar las etiquetas del campo seleccionado. Si ha seleccionado un campo de tipo de objeto individual, el carril derecho muestra los subcampos a los que se propagarán las etiquetas aplicadas.

![El cuadro de diálogo Aplicar etiquetas de acceso y control de datos con los campos seleccionados resaltados.](../images/tutorials/labels/edit-labels.png)

>[!NOTE]
>
>Si está editando campos para todo el esquema, el carril derecho no muestra los campos aplicables y muestra el nombre del esquema en su lugar.

Utilice la lista mostrada para seleccionar las etiquetas que desea añadir al esquema o campo. A medida que se eligen las etiquetas, la variable **[!UICONTROL Etiquetas aplicadas]** se actualiza la sección para mostrar las etiquetas seleccionadas hasta el momento.

![El cuadro de diálogo Aplicar etiquetas de acceso y control de datos con las etiquetas aplicadas resaltadas.](../images/tutorials/labels/applied-labels.png)

Para filtrar las etiquetas mostradas por tipo, seleccione la categoría deseada en el carril izquierdo. Para crear una nueva etiqueta personalizada, seleccione **[!UICONTROL Crear etiqueta]**.

![El cuadro de diálogo Aplicar etiquetas de acceso y control de datos con un filtro de tipo de etiqueta aplicado y Crear etiqueta resaltada.](../images/tutorials/labels/filter-and-create-custom.png)

Cuando esté satisfecho con las etiquetas seleccionadas, seleccione **[!UICONTROL Guardar]** para aplicarlos al campo o esquema.

![El cuadro de diálogo Aplicar etiquetas de acceso y control de datos con Guardar resaltado.](../images/tutorials/labels/save-labels.png)

El **[!UICONTROL Etiquetas]** vuelve a aparecer y muestra las etiquetas aplicadas al esquema.

![La pestaña Etiquetas del espacio de trabajo de esquemas con las etiquetas de campo aplicadas resaltadas.](../images/tutorials/labels/field-labels-added.png)

## Pasos siguientes

En esta guía se explica cómo administrar las etiquetas de uso de datos para esquemas y campos. Para obtener información sobre la administración de etiquetas de uso de datos, incluido cómo agregarlas a conjuntos de datos específicos en lugar de hacerlo en el nivel de esquema, consulte la [guía de IU de etiquetas de uso de datos](../../data-governance/labels/user-guide.md).
