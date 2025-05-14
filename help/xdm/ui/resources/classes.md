---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos;ui;espacio de trabajo;clase;clases;
solution: Experience Platform
title: Crear y editar clases en la IU
description: Obtenga información sobre cómo crear y editar clases en la interfaz de usuario de Experience Platform.
exl-id: 1b4c3996-2319-45dd-9edd-a5bcad46578b
source-git-commit: a05ee385694b028b513e2fa632079e665ba815bb
workflow-type: tm+mt
source-wordcount: '1691'
ht-degree: 5%

---

# Creación y edición de esquemas en la IU {#ui-create-and-edit}

>[!CONTEXTUALHELP]
>id="platform_schemas_class_filter"
>title="Filtro de clase estándar o personalizado"
>abstract="La lista de clases disponibles se filtra previamente en función de cómo se crearon. Seleccione el botón de opción para elegir entre las opciones Estándar y Personalizado. La opción Estándar muestra las entidades creadas por Adobe e incluye las clases Perfil individual XDM y Evento de experiencia XDM. La opción Personalizado muestra las entidades creadas dentro de su organización. Consulte la documentación para obtener más información sobre la creación y edición de clases."

En Adobe Experience Platform, la clase de un esquema define los aspectos de comportamiento de los datos que contendrá el esquema (registro o serie temporal). Además, las clases describen el menor número de propiedades comunes que todos los esquemas basados en esa clase necesitarían incluir y proporcionan una forma de combinar varios conjuntos de datos compatibles.

Adobe proporciona varias clases de modelo de datos de experiencia (XDM) estándar (&quot;principales&quot;), entre las que se incluyen [XDM Individual Profile](../../classes/individual-profile.md) y [XDM ExperienceEvent](../../classes/experienceevent.md). Además de estas clases principales, también puede crear sus propias clases personalizadas para describir casos de uso más específicos para su organización.

Este documento proporciona información general sobre cómo crear, editar y administrar clases personalizadas en la interfaz de usuario de Experience Platform.

## Requisitos previos {#prerequisites}

Esta guía requiere una comprensión práctica del sistema XDM. Consulte la [descripción general de XDM](../../home.md) para obtener una introducción del papel de XDM en el ecosistema de Experience Platform y los [conceptos básicos de la composición de esquemas](../../schema/composition.md) para conocer cómo las clases contribuyen a los esquemas XDM.

Aunque no es necesario para esta guía, se recomienda que también siga el tutorial sobre [maquetar un esquema en la interfaz de usuario](../../tutorials/create-schema-ui.md) para familiarizarse con las diversas funcionalidades del Editor de esquemas.

## Introducción {#getting-started}

En la interfaz de usuario de Experience Platform, seleccione **[!UICONTROL Esquemas]** en el panel de navegación izquierdo para abrir el área de trabajo [!UICONTROL Esquemas] y, a continuación, seleccione la pestaña **[!UICONTROL Clases]**. Se muestra una lista de las clases disponibles.

![Se ha resaltado el número de clases dentro de la ficha [!UICONTROL Clases] del espacio de trabajo [!UICONTROL Esquemas] [!UICONTROL Clases] y [!UICONTROL Esquemas].](../../images/ui/resources/classes/available-classes.png)

## Filtrar clases {#filter}

La lista de clases se filtra automáticamente en función de cómo se crearon. La configuración predeterminada muestra las clases definidas por Adobe. También puede filtrar la lista para mostrar los que ha creado su organización. Seleccione el botón de opción para elegir entre las opciones [!UICONTROL Estándar] y [!UICONTROL Personalizado]. La opción [!UICONTROL Standard] muestra las entidades creadas por Adobe y la opción [!UICONTROL Custom] muestra las entidades creadas dentro de su organización.

![Se ha resaltado la ficha [!UICONTROL Clases] del área de trabajo [!UICONTROL Esquemas] con [!UICONTROL Estándar] y [!UICONTROL Personalizado].](../../images/ui/resources/classes/standard-and-custom-classes.png)

>[!TIP]
>
>Utilice las funcionalidades de búsqueda para filtrar o encontrar una clase según su nombre. Consulte la guía [Exploración de recursos XDM](../explore.md) para obtener más información.

## Crear una nueva clase {#create}

Existen dos métodos para crear una clase en la interfaz de usuario de Experience Platform, mediante **[!UICONTROL Crear clase]** o **[!UICONTROL Crear esquema]**.

### Crear clase

Seleccione **[!UICONTROL Crear clase]** de la ficha [!UICONTROL Clases] en el área de trabajo de [!UICONTROL Esquemas].

![La ficha [!UICONTROL Clases] del área de trabajo [!UICONTROL Esquemas] con [!UICONTROL Crear clase] resaltada](../../images/ui/resources/classes/create-class.png)

Aparecerá el cuadro de diálogo [!UICONTROL Crear clase]. Escriba un [!UICONTROL Nombre para mostrar] y una [!UICONTROL Descripción] para su clase y elija el comportamiento deseado de la clase con los botones de opción. Las clases pueden ser del tipo [!UICONTROL Registro] o [!UICONTROL Serie temporal]. Seleccione **[!UICONTROL Crear]** para confirmar sus opciones y volver a la ficha [!UICONTROL Clases].

![Se ha resaltado el cuadro de diálogo [!UICONTROL Crear clase] con [!UICONTROL Crear].](../../images/ui/resources/classes/create-class-dialog.png)

La clase que ha creado está disponible y se enumera en la vista [!UICONTROL Clases].

![La ficha [!UICONTROL Clases] del área de trabajo [!UICONTROL Esquemas] con la clase creada recientemente resaltada.](../../images/ui/resources/classes/new-class-listing.png)

### Crear esquema

Como alternativa, puede crear una clase creando manualmente un esquema. Seleccione **[!UICONTROL Crear esquema]** de la ficha [!UICONTROL Clases] en el área de trabajo de [!UICONTROL Esquemas].

![La ficha [!UICONTROL Clases] del área de trabajo [!UICONTROL Esquemas] con [!UICONTROL Crear esquema] resaltado](../../images/ui/resources/classes/create-schema.png)

Seleccione **[!UICONTROL Manual]** en el cuadro de diálogo [!UICONTROL Crear un esquema] que aparece.

>[!NOTE]
>
>Si utiliza el flujo de trabajo de creación de esquemas asistidos por ML, puede cargar un archivo y utilizar algoritmos XML para generar un esquema recomendado. En ese flujo de trabajo de creación de esquemas, no es necesario especificar la clase base para el esquema. Para saber cómo ML puede recomendar una estructura de esquema basada en un archivo csv, consulte la [guía de creación de esquemas asistida por aprendizaje automático](../ml-assisted-schema-creation.md).

![El cuadro de diálogo Crear un esquema con las opciones de flujo de trabajo y la selección resaltadas.](../../images/ui/resources/classes/manually-create-a-schema.png)

Aparecerá el flujo de trabajo de creación de esquemas. En la sección [!UICONTROL Detalles del esquema], seleccione **[!UICONTROL Otro]**. Aparecerá una lista de las clases disponibles. Seleccione **[!UICONTROL Crear clase]**.

![El flujo de trabajo [!UICONTROL Crear esquema] con [!UICONTROL Otros] resaltado en la sección [!UICONTROL Detalles del esquema].](../../images/ui/resources/classes/other-schema-details.png)

Aparecerá el cuadro de diálogo [!UICONTROL Crear clase]. Escriba un [!UICONTROL Nombre para mostrar] y una [!UICONTROL Descripción] para su clase y elija el comportamiento deseado de la clase con los botones de opción. Las clases pueden ser del tipo [!UICONTROL Registro] o [!UICONTROL Serie temporal]. Seleccione **[!UICONTROL Crear]** para confirmar sus opciones y volver a la ficha [!UICONTROL Clases].

![Se ha resaltado el cuadro de diálogo [!UICONTROL Crear clase] con [!UICONTROL Crear].](../../images/ui/resources/classes/create-class-from-schema.png)

La lista de clases se actualiza en la sección [!UICONTROL Detalles del esquema] y la clase recién creada se selecciona automáticamente. Seleccione **[!UICONTROL Siguiente]** para continuar creando su esquema.

![La sección [!UICONTROL Detalles del esquema] con la nueva clase seleccionada y [!UICONTROL Siguiente] resaltada.](../../images/ui/resources/classes/select-new-class.png)

Después de seleccionar una clase, aparece la sección [!UICONTROL Nombre y revisión]. En esta sección, proporcione un nombre y una descripción para identificar el esquema. palo de golfLa estructura base del esquema (proporcionada por la clase ) se muestra en el lienzo para que revise y compruebe la clase y la estructura de esquema seleccionadas.

Escriba un [!UICONTROL nombre para mostrar del esquema] descriptivo en el campo de texto. A continuación, introduzca una descripción adecuada para ayudar a identificar el esquema. Cuando haya revisado la estructura de esquema y esté satisfecho con la configuración, seleccione **[!UICONTROL Finalizar]** para crear el esquema.

![Se ha resaltado la sección [!UICONTROL Nombre y revisión] del flujo de trabajo [!UICONTROL Crear esquema] con [!UICONTROL Nombre para mostrar esquema], [!UICONTROL Descripción] y [!UICONTROL Finalizar].](../../images/ui/resources/classes/schema-details.png)

## Adición de campos a una clase {#add-fields}

Una vez que tenga un esquema que emplee una clase personalizada abierta en el Editor de esquemas, puede empezar a agregar campos a la clase. Para agregar un nuevo campo, seleccione el icono **más (+)** junto al nombre del esquema.

>[!IMPORTANT]
>
>Cuando genere un esquema que implemente una clase definida por su organización, recuerde que los grupos de campos de esquema solo están disponibles para su uso con clases compatibles. Dado que la clase que definió es nueva, no hay grupos de campos compatibles enumerados en el cuadro de diálogo **[!UICONTROL Agregar grupo de campos]**. En su lugar, deberá [crear nuevos grupos de campos](./field-groups.md#create) para usarlos con esa clase. La próxima vez que cree un esquema que implemente la nueva clase, los grupos de campos que definió se enumerarán y estarán disponibles para su uso.

![Editor de esquemas con el botón Agregar resaltado.](../../images/ui/resources/classes/add-field.png)

>[!IMPORTANT]
>
>Tenga en cuenta que cualquier campo que agregue a una clase se utilizará en todos los esquemas que empleen esa clase. Por lo tanto, debe considerar cuidadosamente qué campos son útiles en todos los casos de uso del esquema. Si está pensando en agregar un campo que podría ver el uso solamente en algunos esquemas bajo esta clase, puede que desee considerar agregarlo a esos esquemas [creando un grupo de campos](./field-groups.md#create) en su lugar.

Aparece un marcador de posición **[!UICONTROL Campo sin título]** en el lienzo, y el carril derecho se actualiza para mostrar controles para configurar las propiedades del campo. En **[!UICONTROL Asignar a]**, seleccione **[!UICONTROL Clase]**.

![Campo sin título en el lienzo del Editor de esquemas con la propiedad de campo Asignar a [!UICONTROL Clase] seleccionada y resaltada.](../../images/ui/resources/classes/assign-to-class.png)

Consulte la guía [definición de campos en la interfaz de usuario](../fields/overview.md#define) para ver los pasos específicos sobre cómo configurar y agregar el campo a la clase. Siga agregando tantos campos como sea necesario a la clase. Cuando termine, seleccione **[!UICONTROL Guardar]** para guardar tanto el esquema como la clase.

![Esquema recién creado en el lienzo del Editor de esquemas, con [!UICONTROL Guardar] resaltado.](../../images/ui/resources/classes/save.png)

Si ha creado anteriormente esquemas que emplean esta clase, los campos recién agregados aparecerán automáticamente en esos esquemas.

## Edición de una clase {#edit-a-class}

>[!NOTE]
>
>Solo las clases personalizadas definidas por su organización se pueden editar y personalizar por completo. Para las clases principales definidas por Adobe, solo se pueden editar los nombres para mostrar de sus campos dentro del contexto de esquemas individuales. Consulte la sección sobre [edición de nombres para mostrar para campos de esquema](./schemas.md#display-names) para obtener más información.
>
>Una vez guardada una clase personalizada y utilizada en la ingesta de datos, solo se pueden realizar cambios adicionales en ella a partir de entonces. Consulte las [reglas de evolución de esquema](../../schema/composition.md#evolution) para obtener más información.

Puede editar una clase a través del flujo de trabajo del esquema editando un esquema existente que extienda la clase o creando manualmente un esquema. No es posible editar directamente una clase. Desde la ficha [!UICONTROL Examinar] del área de trabajo [!UICONTROL Esquemas], seleccione una clase existente o **[!UICONTROL Crear un esquema]**.

![Se resaltó el Editor de esquemas con una clase existente y [!UICONTROL Crear un esquema].](../../images/ui/resources/classes/edit-class-options.png)

Si decide crear un nuevo esquema, consulte la sección sobre [creación de un esquema](#create-schema) para obtener detalles. Cuando haya terminado de crear el esquema (o después de seleccionar uno existente), aparecerá el Editor de esquemas. Para actualizar un campo de clase existente, seleccione el campo de la estructura de esquema. La información del campo aparece en el carril derecho. Asegúrese de que [!UICONTROL asigne a]
la opción **[!UICONTROL Class]** está seleccionada o las actualizaciones no afectarán a la clase.

![Editor de esquemas con un campo seleccionado y resaltado, y el carril derecho expuesto, resaltando [!UICONTROL Asignar a].](../../images/ui/resources/classes/edit-existing-field.png)

Realice los cambios que desee en el campo, desplácese hacia abajo en el carril derecho para seleccionar **[!UICONTROL Aplicar]** para guardar los cambios.

>[!IMPORTANT]
>
> Cualquier actualización que realice en los campos se aplicará en todos los esquemas que empleen esa clase, siguiendo las [reglas de evolución del esquema](../../schema/composition.md#evolution).

![Editor de esquemas con un campo seleccionado y el carril derecho expuesto, destacando [!UICONTROL Aplicar].](../../images/ui/resources/classes/save-changes.png)

Para agregar nuevos campos, siga la guía [agregar campos a una clase](#add-fields-to-a-class). Cuando termine, seleccione **[!UICONTROL Guardar]** para guardar tanto el esquema como la clase.

![Se resaltó el editor de esquemas con [!UICONTROL Guardar].](../../images/ui/resources/classes/save-schema.png)

## Cambiar la clase de un esquema {#schema}

Puede cambiar la clase del esquema en cualquier momento durante el proceso de creación inicial antes de guardarlo. Sin embargo, esto debe hacerse con precaución, ya que los grupos de campos solo son compatibles con determinadas clases. Al cambiar la clase, se restablecen el lienzo y los campos que se hayan añadido.
Consulte la guía de [creación y edición de esquemas](./schemas.md#change-class) para obtener más información.

## Pasos siguientes {#next-steps}

En este documento se explica cómo crear y editar clases mediante la interfaz de usuario de Experience Platform. Para obtener más información sobre las capacidades del área de trabajo [!UICONTROL Esquemas], consulte la descripción general del área de trabajo [[!UICONTROL Esquemas]](../overview.md).

Para obtener información sobre cómo administrar clases mediante la API de Registro de esquemas, consulte la [guía de extremo de clases](../../api/classes.md).
