---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos;ui;espacio de trabajo;esquema;esquemas;
solution: Experience Platform
title: Crear y editar esquemas en la interfaz de usuario
description: Obtenga información sobre los conceptos básicos de cómo crear y editar esquemas en la interfaz de usuario del Experience Platform.
topic-legacy: user guide
exl-id: be83ce96-65b5-4a4a-8834-16f7ef9ec7d1
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1340'
ht-degree: 0%

---

# Crear y editar esquemas en la interfaz de usuario

Esta guía proporciona información general sobre cómo crear, editar y administrar esquemas del Modelo de datos de experiencia (XDM) para su organización en la interfaz de usuario de Adobe Experience Platform.

>[!IMPORTANT]
>
>Los esquemas XDM son extremadamente personalizables y, por lo tanto, los pasos involucrados en la creación de un esquema pueden variar según el tipo de datos que desee capturar. Como resultado, este documento solo cubre las interacciones básicas que puede realizar con los esquemas en la interfaz de usuario y excluye los pasos relacionados como la personalización de clases, mezclas, tipos de datos y campos.
>
>Para obtener un recorrido completo por el proceso de creación del esquema, siga el tutorial de creación de esquema [schema](../../tutorials/create-schema-ui.md) para crear un esquema de ejemplo completo y familiarizarse con las muchas funciones de [!DNL Schema Editor].

## Requisitos previos

Esta guía requiere una comprensión práctica del sistema XDM. Consulte la [información general de XDM](../../home.md) para obtener una introducción a la función de XDM dentro del ecosistema del Experience Platform y los [conceptos básicos de la composición del esquema](../../schema/composition.md) para obtener información general sobre cómo se construyen los esquemas.

## Crear un nuevo esquema {#create}

En el espacio de trabajo [!UICONTROL Schemas], seleccione **[!UICONTROL Create schema]** en la esquina superior derecha. En el menú desplegable que aparece, puede elegir entre **[!UICONTROL XDM Individual Profile]** y **[!UICONTROL XDM ExperienceEvent]** como clase base para el esquema. También puede seleccionar **[!UICONTROL Browse]** para seleccionarlo de la lista completa de clases disponibles o [crear una nueva clase personalizada](./classes.md#create) en su lugar.

![](../../images/ui/resources/schemas/create-schema.png)

Una vez seleccionada una clase, aparece [!DNL Schema Editor] y la estructura base del esquema (proporcionada por la clase) se muestra en el lienzo. Desde aquí, puede utilizar el carril derecho para añadir un **[!UICONTROL Display name]** y **[!UICONTROL Description]** para el esquema.

![](../../images/ui/resources/schemas/schema-details.png)

Ahora puede empezar a crear la estructura del esquema [añadiendo mezclas](#add-mixins).

## Editar un esquema existente {#edit}

>[!NOTE]
>
>Una vez guardado y utilizado un esquema en la ingesta de datos, solo se pueden realizar cambios aditivos en él. Consulte las [reglas de evolución de esquema](../../schema/composition.md#evolution) para obtener más información.

Para editar un esquema existente, seleccione la pestaña **[!UICONTROL Browse]** y, a continuación, seleccione el nombre del esquema que desea editar.

![](../../images/ui/resources/schemas/edit-schema.png)

>[!TIP]
>
>Puede utilizar las capacidades de búsqueda y filtrado del espacio de trabajo para ayudar a encontrar el esquema más fácil. Consulte la guía sobre [exploración de recursos XDM](../explore.md) para obtener más información.

Una vez seleccionado un esquema, el [!DNL Schema Editor] aparece con la estructura del esquema mostrada en el lienzo. Ahora puede [añadir mezclas](#add-mixins) al esquema, [editar nombres de visualización de campos](#display-names) o [editar mezclas personalizadas existentes](./mixins.md#edit) si el esquema emplea alguna.

## Añadir mezclas a un esquema {#add-mixins}

>[!NOTE]
>
>En esta sección se explica cómo añadir mezclas existentes a un esquema. Si desea crear una nueva mezcla personalizada, consulte la guía sobre [creación y edición de mezclas](./mixins.md#create) en su lugar.

Una vez que haya abierto un esquema dentro de [!DNL Schema Editor], puede añadir campos al esquema mediante el uso de mezclas. Para comenzar, seleccione **[!UICONTROL Add]** junto a **[!UICONTROL Mixins]** en el carril izquierdo.

![](../../images/ui/resources/schemas/add-mixin-button.png)

Aparece un cuadro de diálogo que muestra una lista de mezclas que puede seleccionar para el esquema. Dado que las mezclas sólo son compatibles con una clase, sólo se enumerarán las mezclas asociadas con la clase seleccionada del esquema. De forma predeterminada, las mezclas enumeradas se ordenan según su popularidad de uso dentro de su organización.

![](../../images/ui/resources/schemas/mixin-popularity.png)

Si conoce la actividad general o el área de negocio de los campos de mezcla que desea agregar, seleccione una o más de las categorías verticales del sector en el carril izquierdo para filtrar la lista mostrada de mezclas.

![](../../images/ui/resources/schemas/industry-filter.png)

>[!NOTE]
>
>Para obtener más información sobre las prácticas recomendadas para el modelado de datos específico del sector en XDM, consulte la documentación sobre [modelos de datos del sector](../../schema/industries/overview.md).

También puede utilizar la barra de búsqueda para localizar la mezcla deseada. Las mezclas cuyo nombre coincida con la consulta aparecen en la parte superior de la lista. En **[!UICONTROL Standard Fields]**, se muestran las mezclas que contienen campos que describen atributos de datos deseados.

![](../../images/ui/resources/schemas/mixin-search.png)

Seleccione la casilla de verificación situada junto al nombre de la mezcla que desea añadir al esquema. Puede seleccionar varias mezclas de la lista, y cada una de ellas aparecerá en el carril derecho.

![](../../images/ui/resources/schemas/add-mixin.png)

>[!TIP]
>
>Para cualquier mezcla enumerada, puede mantener el puntero o centrarse en el icono de información (![](../../images/ui/resources/schemas/info-icon.png)) para ver una breve descripción del tipo de datos que captura la mezcla. También puede seleccionar el icono de vista previa (![](../../images/ui/resources/schemas/preview-icon.png)) para ver la estructura de los campos que proporciona la mezcla antes de decidir agregarla al esquema.

Una vez seleccionadas las mezclas, seleccione **[!UICONTROL Add mixin]** para agregarlas al esquema.

![](../../images/ui/resources/schemas/add-mixin-finish.png)

El [!DNL Schema Editor] vuelve a aparecer con los campos proporcionados por la mezcla representados en el lienzo.

![](../../images/ui/resources/schemas/mixins-added.png)

## Habilitar un esquema para el perfil de cliente en tiempo real {#profile}

[Los ](../../../profile/home.md) perfiles del cliente en tiempo real emergen datos de fuentes diferentes para construir una vista completa de cada cliente individual. Si desea que los datos capturados por un esquema participen en este proceso, debe activar el esquema para utilizarlo en [!DNL Profile].

>[!IMPORTANT]
>
>Para habilitar un esquema para [!DNL Profile], debe tener un campo de identidad principal definido. Consulte la guía sobre [definición de campos de identidad](../fields/identity.md) para obtener más información.

Para habilitar el esquema, comience seleccionando el nombre del esquema en el carril izquierdo y, a continuación, seleccione el botón **[!UICONTROL Profile]** en el carril derecho.

![](../../images/ui/resources/schemas/profile-toggle.png)

Aparece una ventana emergente que le advierte de que una vez que un esquema se ha habilitado y guardado, no se puede desactivar. Seleccione **[!UICONTROL Enable]** para continuar.

![](../../images/ui/resources/schemas/profile-confirm.png)

El lienzo vuelve a aparecer con la opción [!UICONTROL Profile] activada.

>[!IMPORTANT]
>
>Dado que el esquema aún no se ha guardado, este es el punto de no retorno si cambia de opinión sobre permitir que el esquema participe en el perfil del cliente en tiempo real: una vez guardado un esquema habilitado, ya no se puede desactivar. Seleccione de nuevo la opción **[!UICONTROL Profile]** para deshabilitar el esquema.

Para finalizar el proceso, seleccione **[!UICONTROL Save]** para guardar el esquema.

![](../../images/ui/resources/schemas/profile-enabled.png)

El esquema ahora está habilitado para utilizarse en el perfil del cliente en tiempo real. Cuando Platform incorpora datos en conjuntos de datos basados en este esquema, esos datos se incorporan a los datos de perfil amalgamados.

## Editar nombres para mostrar para campos de esquema {#display-names}

Una vez que haya asignado una clase y agregado mezclas a un esquema, puede editar los nombres para mostrar de cualquiera de los campos del esquema, independientemente de si esos campos han sido proporcionados por recursos XDM estándar o personalizados.

>[!NOTE]
>
>Tenga en cuenta que los nombres para mostrar de los campos que pertenecen a clases o mezclas estándar solo se pueden editar en el contexto de un esquema específico. En otras palabras, cambiar el nombre para mostrar de un campo estándar en un esquema no afecta a otros esquemas que emplean la misma clase o mezcla asociada.

Para editar el nombre para mostrar de un campo de esquema, seleccione el campo en el lienzo. En el carril derecho, proporcione el nuevo nombre en **[!UICONTROL Display name]**.

![](../../images/ui/resources/schemas/display-name.png)

Seleccione **[!UICONTROL Apply]** en el carril derecho y el lienzo se actualizará para mostrar el nuevo nombre para mostrar del campo. Seleccione **[!UICONTROL Save]** para aplicar los cambios al esquema.

![](../../images/ui/resources/schemas/display-name-changed.png)

## Cambiar la clase de un esquema {#change-class}

Puede cambiar la clase de un esquema en cualquier momento durante el proceso de composición inicial antes de guardar el esquema.

>[!WARNING]
>
>La reasignación de la clase para un esquema debe realizarse con extrema precaución. Las mezclas solo son compatibles con ciertas clases y, por lo tanto, cambiar la clase restablecerá el lienzo y los campos que haya agregado.

Para reasignar una clase, seleccione **[!UICONTROL Assign]** en el lado izquierdo del lienzo.

![](../../images/ui/resources/schemas/assign-class-button.png)

Aparece un cuadro de diálogo que muestra una lista de todas las clases disponibles, incluidas las definidas por su organización (el propietario es &quot;[!UICONTROL Customer]&quot;), así como las clases estándar definidas por el Adobe.

Seleccione una clase de la lista para mostrar su descripción en el lado derecho del cuadro de diálogo. También puede seleccionar **[!UICONTROL Preview class structure]** para ver los campos y metadatos asociados a la clase. Seleccione **[!UICONTROL Assign class]** para continuar.

![](../../images/ui/resources/schemas/assign-class.png)

Se abre un nuevo cuadro de diálogo en el que se le pedirá que confirme que desea asignar una nueva clase. Seleccione **[!UICONTROL Assign]** para confirmar.

![](../../images/ui/resources/schemas/assign-confirm.png)

Después de confirmar el cambio de clase, el lienzo se restablecerá y se perderá todo el progreso de composición.

## Pasos siguientes

Este documento abarcaba los aspectos básicos de la creación y edición de esquemas en la interfaz de usuario de Platform. Se recomienda encarecidamente revisar el [tutorial de creación de esquemas](../../tutorials/create-schema-ui.md) para obtener un flujo de trabajo completo para crear un esquema completo en la interfaz de usuario, incluida la creación de mezclas personalizadas y tipos de datos para casos de uso únicos.

Para obtener más información sobre las capacidades del espacio de trabajo [!UICONTROL Schemas], consulte la [[!UICONTROL Schemas] descripción general del espacio de trabajo](../overview.md).

Para obtener información sobre cómo administrar esquemas en la API [!DNL Schema Registry], consulte la [guía de extremo de esquemas](../../api/schemas.md).
