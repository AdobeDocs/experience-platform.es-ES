---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos;ui;espacio de trabajo;esquema;esquemas;
solution: Experience Platform
title: Crear y editar esquemas en la interfaz de usuario
description: Obtenga información sobre los conceptos básicos de cómo crear y editar esquemas en la interfaz de usuario del Experience Platform.
topic-legacy: user guide
exl-id: be83ce96-65b5-4a4a-8834-16f7ef9ec7d1
source-git-commit: 49a54b78d1e3745694352e779fb2226acd99d663
workflow-type: tm+mt
source-wordcount: '1434'
ht-degree: 0%

---

# Crear y editar esquemas en la interfaz de usuario

Esta guía proporciona información general sobre cómo crear, editar y administrar esquemas del Modelo de datos de experiencia (XDM) para su organización en la interfaz de usuario de Adobe Experience Platform.

>[!IMPORTANT]
>
>Los esquemas XDM son extremadamente personalizables y, por lo tanto, los pasos involucrados en la creación de un esquema pueden variar según el tipo de datos que desee capturar. Como resultado, este documento solo cubre las interacciones básicas que puede realizar con los esquemas en la interfaz de usuario y excluye los pasos relacionados como la personalización de clases, grupos de campos de esquema, tipos de datos y campos.
>
>Para obtener un recorrido completo por el proceso de creación de esquemas, siga junto con la [tutorial de creación de esquemas](../../tutorials/create-schema-ui.md) para crear un esquema de ejemplo completo y familiarizarse con las muchas capacidades de la variable [!DNL Schema Editor].

## Requisitos previos

Esta guía requiere una comprensión práctica del sistema XDM. Consulte la [Información general de XDM](../../home.md) para una introducción al papel de XDM dentro del ecosistema del Experience Platform, y [conceptos básicos de la composición del esquema](../../schema/composition.md) para obtener una descripción general de cómo se construyen los esquemas.

## Crear un nuevo esquema {#create}

En el [!UICONTROL Esquemas] espacio de trabajo, seleccione **[!UICONTROL Crear esquema]** en la esquina superior derecha. En el menú desplegable que aparece, puede elegir entre **[!UICONTROL Perfil individual XDM]** y **[!UICONTROL XDM ExperienceEvent]** como clase base para el esquema. También puede seleccionar **[!UICONTROL Examinar]** para seleccionar entre la lista completa de clases disponibles, o [crear una nueva clase personalizada](./classes.md#create) en su lugar.

![](../../images/ui/resources/schemas/create-schema.png)

Una vez seleccionada una clase, la variable [!DNL Schema Editor] y la estructura base del esquema (proporcionada por la clase ) se muestra en el lienzo. Desde aquí, puede utilizar el carril derecho para agregar un **[!UICONTROL Nombre para mostrar]** y **[!UICONTROL Descripción]** para el esquema .

![](../../images/ui/resources/schemas/schema-details.png)

Ahora puede empezar a crear la estructura del esquema mediante [adición de grupos de campos de esquema](#add-field-groups).

## Edición de un esquema existente {#edit}

>[!NOTE]
>
>Una vez guardado y utilizado un esquema en la ingesta de datos, solo se pueden realizar cambios aditivos en él. Consulte la [reglas de evolución de esquema](../../schema/composition.md#evolution) para obtener más información.

Para editar un esquema existente, seleccione la opción **[!UICONTROL Examinar]** y, a continuación, seleccione el nombre del esquema que desea editar.

![](../../images/ui/resources/schemas/edit-schema.png)

>[!TIP]
>
>Puede utilizar las capacidades de búsqueda y filtrado del espacio de trabajo para ayudar a encontrar el esquema más fácil. Consulte la guía de [exploración de recursos XDM](../explore.md) para obtener más información.

Una vez que seleccione un esquema, la variable [!DNL Schema Editor] aparece con la estructura del esquema en el lienzo. Ahora puede [agregar grupos de campos](#add-field-groups) al esquema, [editar nombres para mostrar de campos](#display-names)o [editar grupos de campos personalizados existentes](./field-groups.md#edit) si el esquema emplea alguno.

## Añadir grupos de campos a un esquema {#add-field-groups}

>[!NOTE]
>
>Esta sección explica cómo agregar grupos de campos existentes a un esquema. Si desea crear un nuevo grupo de campos personalizados, consulte la guía de [creación y edición de grupos de campos](./field-groups.md#create) en su lugar.

Una vez que haya abierto un esquema dentro de la variable [!DNL Schema Editor], puede añadir campos al esquema mediante el uso de grupos de campos. Para empezar, seleccione **[!UICONTROL Agregar]** junto a **[!UICONTROL Grupos de campo]** en el carril izquierdo.

![](../../images/ui/resources/schemas/add-field-group-button.png)

Aparece un cuadro de diálogo que muestra una lista de los grupos de campos que puede seleccionar para el esquema. Dado que los grupos de campos solo son compatibles con una clase, solo se enumerarán los grupos de campos asociados con la clase seleccionada del esquema. De forma predeterminada, los grupos de campos enumerados se ordenan según su popularidad de uso dentro de su organización.

![](../../images/ui/resources/schemas/field-group-popularity.png)

Si conoce la actividad general o el área comercial de los campos que desea agregar, seleccione una o varias categorías verticales del sector en el carril izquierdo para filtrar la lista mostrada de grupos de campos.

![](../../images/ui/resources/schemas/industry-filter.png)

>[!NOTE]
>
>Para obtener más información sobre las prácticas recomendadas para el modelado de datos específico del sector en XDM, consulte la documentación sobre [modelos de datos del sector](../../schema/industries/overview.md).

También puede utilizar la barra de búsqueda para localizar el grupo de campos deseado. Los grupos de campos cuyo nombre coincida con la consulta aparecen en la parte superior de la lista. En **[!UICONTROL Campos estándar]**, se muestran los grupos de campos que contienen campos que describen atributos de datos deseados.

![](../../images/ui/resources/schemas/field-group-search.png)

Active la casilla situada junto al nombre del grupo de campos que desea agregar al esquema. Puede seleccionar varios grupos de campos en la lista, y cada grupo de campos seleccionado aparecerá en el carril derecho.

![](../../images/ui/resources/schemas/add-field-group.png)

>[!TIP]
>
>Para cualquier grupo de campos enumerado, puede mantener el puntero sobre él o centrarse en el icono de información (![](../../images/ui/resources/schemas/info-icon.png)) para ver una breve descripción del tipo de datos que captura el grupo de campos. También puede seleccionar el icono de vista previa (![](../../images/ui/resources/schemas/preview-icon.png)) para ver la estructura de los campos que proporciona el grupo de campos antes de decidir agregarla al esquema.

Una vez que haya elegido los grupos de campos, seleccione **[!UICONTROL Agregar grupos de campos]** para agregarlas al esquema.

![](../../images/ui/resources/schemas/add-field-group-finish.png)

La variable [!DNL Schema Editor] vuelve a aparecer con los campos proporcionados por el grupo de campos representados en el lienzo.

![](../../images/ui/resources/schemas/field-groups-added.png)

## Activación de un esquema para el perfil de cliente en tiempo real {#profile}

[Perfil del cliente en tiempo real](../../../profile/home.md) combina datos de fuentes diferentes para construir una vista completa de cada cliente individual. Si desea que los datos capturados por un esquema participen en este proceso, debe activar el esquema para utilizarlo en [!DNL Profile].

>[!IMPORTANT]
>
>Para habilitar un esquema para [!DNL Profile], debe tener un campo de identidad principal definido. Consulte la guía de [definición de campos de identidad](../fields/identity.md) para obtener más información.

Para habilitar el esquema, comience por seleccionar el nombre del esquema en el carril izquierdo y, a continuación, seleccione la opción **[!UICONTROL Perfil]** alterne en el carril derecho.

![](../../images/ui/resources/schemas/profile-toggle.png)

Aparece una ventana emergente que le advierte de que una vez que un esquema se ha habilitado y guardado, no se puede desactivar. Select **[!UICONTROL Habilitar]** para continuar.

![](../../images/ui/resources/schemas/profile-confirm.png)

El lienzo vuelve a aparecer con la variable [!UICONTROL Perfil] activar.

>[!IMPORTANT]
>
>Dado que el esquema aún no se ha guardado, este es el punto de no retorno si cambia de opinión sobre permitir que el esquema participe en el perfil del cliente en tiempo real: una vez guardado un esquema habilitado, ya no se puede desactivar. Seleccione el **[!UICONTROL Perfil]** volver a alternar para deshabilitar el esquema.

Para finalizar el proceso, seleccione **[!UICONTROL Guardar]** para guardar el esquema.

![](../../images/ui/resources/schemas/profile-enabled.png)

El esquema ahora está habilitado para utilizarse en el perfil del cliente en tiempo real. Cuando Platform incorpora datos en conjuntos de datos basados en este esquema, esos datos se incorporan a los datos de perfil amalgamados.

## Edición de nombres para mostrar en campos de esquema {#display-names}

Una vez que haya asignado una clase y agregado grupos de campos a un esquema, puede editar los nombres para mostrar de cualquiera de los campos del esquema, independientemente de si esos campos han sido proporcionados por recursos XDM estándar o personalizados.

>[!NOTE]
>
>Tenga en cuenta que los nombres para mostrar de los campos que pertenecen a clases estándar o grupos de campos solo se pueden editar en el contexto de un esquema específico. En otras palabras, cambiar el nombre para mostrar de un campo estándar en un esquema no afecta a otros esquemas que emplean la misma clase o grupo de campos asociado.
>
>Una vez realizados los cambios en los nombres para mostrar de los campos de un esquema, esos cambios se reflejan inmediatamente en cualquier conjunto de datos existente basado en ese esquema.

Para editar el nombre para mostrar de un campo de esquema, seleccione el campo en el lienzo. En el carril derecho, proporcione el nuevo nombre en **[!UICONTROL Nombre para mostrar]**.

![](../../images/ui/resources/schemas/display-name.png)

Select **[!UICONTROL Aplicar]** en el carril derecho y el lienzo se actualiza para mostrar el nuevo nombre para mostrar del campo. Select **[!UICONTROL Guardar]** para aplicar los cambios al esquema.

![](../../images/ui/resources/schemas/display-name-changed.png)

## Cambiar la clase de un esquema {#change-class}

Puede cambiar la clase de un esquema en cualquier momento durante el proceso de composición inicial antes de guardar el esquema.

>[!WARNING]
>
>La reasignación de la clase para un esquema debe realizarse con extrema precaución. Los grupos de campos solo son compatibles con ciertas clases y, por lo tanto, al cambiar la clase se restablecerá el lienzo y los campos que haya agregado.

Para reasignar una clase, seleccione **[!UICONTROL Asignar]** en el lado izquierdo del lienzo.

![](../../images/ui/resources/schemas/assign-class-button.png)

Aparece un cuadro de diálogo que muestra una lista de todas las clases disponibles, incluidas las definidas por su organización (siendo el propietario &quot;[!UICONTROL Cliente]&quot;) así como las clases estándar definidas por el Adobe.

Seleccione una clase de la lista para mostrar su descripción en el lado derecho del cuadro de diálogo. También puede seleccionar **[!UICONTROL Vista previa de la estructura de la clase]** para ver los campos y metadatos asociados a la clase . Select **[!UICONTROL Asignar clase]** para continuar.

![](../../images/ui/resources/schemas/assign-class.png)

Se abre un nuevo cuadro de diálogo en el que se le pedirá que confirme que desea asignar una nueva clase. Select **[!UICONTROL Asignar]** para confirmar.

![](../../images/ui/resources/schemas/assign-confirm.png)

Después de confirmar el cambio de clase, el lienzo se restablecerá y se perderá todo el progreso de composición.

## Pasos siguientes

Este documento abarcaba los aspectos básicos de la creación y edición de esquemas en la interfaz de usuario de Platform. Se recomienda que revise la [tutorial de creación de esquemas](../../tutorials/create-schema-ui.md) para obtener un flujo de trabajo completo para crear un esquema completo en la interfaz de usuario, incluida la creación de grupos de campos personalizados y tipos de datos para casos de uso únicos.

Para obtener más información sobre las capacidades de la variable [!UICONTROL Esquemas] espacio de trabajo, consulte [[!UICONTROL Esquemas] información general del espacio de trabajo](../overview.md).

Para aprender a administrar esquemas en la [!DNL Schema Registry] API, consulte la [guía de extremo de esquemas](../../api/schemas.md).
