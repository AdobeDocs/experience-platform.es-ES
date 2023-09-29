---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos;ui;espacio de trabajo;grupo de campos;grupos de campos;
solution: Experience Platform
title: Creación y edición de grupos de campos de esquema en la interfaz de usuario
description: Obtenga información sobre cómo crear y editar grupos de campos de esquema en la interfaz de usuario de Experience Platform.
exl-id: 928d70a6-0468-4fb7-a53a-6686ac77f2a3
source-git-commit: 4214339c4a661c6bca2cd571919ae205dcb47da1
workflow-type: tm+mt
source-wordcount: '985'
ht-degree: 8%

---

# Creación y edición de grupos de campos de esquema en la IU {#ui-create-and-edit}

>[!CONTEXTUALHELP]
>id="platform_schemas_fieldgroup_filter"
>title="Filtro de grupo de campos estándar o personalizado"
>abstract="La lista de grupos de campos disponibles se filtra previamente en función de cómo se crearon. Seleccione el botón de opción para elegir entre las opciones Estándar y Personalizado. La opción Estándar muestra las entidades creadas por Adobe y la opción Personalizada muestra las entidades creadas dentro de su organización. Consulte la documentación para obtener más información sobre la creación y edición de grupos de campos."

En el modelo de datos de experiencia (XDM), los grupos de campos de esquema son componentes reutilizables que definen uno o varios campos que implementan determinadas funciones, como detalles personales, preferencias de hotel o dirección. Los grupos de campos están pensados para incluirse como parte de un esquema que implementa una clase compatible.

Un grupo de campos define con qué clase es compatible, según el comportamiento de los datos que representa el grupo de campos (registro o serie temporal). Esto significa que no todos los grupos de campos están disponibles para su uso con todas las clases.

Adobe Experience Platform proporciona muchos grupos de campos estándar que abarcan una amplia gama de casos de uso de marketing. Sin embargo, también puede crear y editar sus propios grupos de campos personalizados para definir conceptos adicionales relacionados con su negocio dentro de los esquemas XDM. Esta guía proporciona información general sobre cómo crear, editar y administrar grupos de campos personalizados para su organización en la IU de Platform.

## Requisitos previos

Esta guía requiere una comprensión práctica del sistema XDM. Consulte la [Información general de XDM](../../home.md) para obtener una introducción a la función de XDM dentro del ecosistema de Experience Platform, y la [conceptos básicos de composición de esquemas](../../schema/composition.md) para saber cómo contribuyen los grupos de campos a los esquemas XDM.

Aunque no es necesario para esta guía, se recomienda seguir el tutorial en [composición de un esquema en la IU](../../tutorials/create-schema-ui.md) para familiarizarse con las diversas capacidades de la [!DNL Schema Editor].

## Crear un nuevo grupo de campos {#create}

Para crear un nuevo grupo de campos, primero debe seleccionar un esquema al que se agregará el grupo de campos. Puede elegir entre [crear un nuevo esquema](./schemas.md#create) o [seleccione un esquema existente para editarlo](./schemas.md#edit).

Una vez que tenga el esquema abierto en, [!DNL Schema Editor], seleccione **[!UICONTROL Añadir]** junto al [!UICONTROL Grupos de campos] en el carril izquierdo.

![](../../images/ui/resources/field-groups/add-field-group.png)

En el cuadro de diálogo que aparece, seleccione **[!UICONTROL Crear nuevo grupo de campos]**. Aquí puede proporcionar un **[!UICONTROL Nombre para mostrar]** y **[!UICONTROL Descripción]** para el grupo de campos. Cuando termine, seleccione **[!UICONTROL Adición de grupos de campos]**.

![](../../images/ui/resources/field-groups/create-field-group.png)

El [!DNL Schema Editor] vuelve a aparecer y el nuevo grupo de campos aparece en el carril izquierdo. Dado que es un grupo de campos completamente nuevo, actualmente no proporciona campos al esquema y, por lo tanto, el lienzo permanece sin cambios. Ahora puede iniciar [adición de campos al grupo de campos](#add-fields).

![](../../images/ui/resources/field-groups/field-group-added.png)

## Filtrar grupos de campos {#filter}

La lista de grupos de campos disponibles se filtra previamente en función de cómo se crearon. La configuración predeterminada muestra los grupos de campos definidos por el Adobe. Sin embargo, también puede filtrar la lista para mostrar las creadas por su organización. Seleccione el botón de opción para elegir entre las [!UICONTROL Standard] y [!UICONTROL Personalizado] opciones. El [!UICONTROL Standard] muestra las entidades creadas por Adobe y la opción [!UICONTROL Personalizado] Esta opción muestra las entidades creadas dentro de su organización.

![El [!UICONTROL Grupos de campos] de la pestaña [!UICONTROL Esquemas] workspace con [!UICONTROL Standard] y [!UICONTROL Personalizado] resaltado.](../../images/ui/resources/field-groups/standard-and-custom-field-groups.png)

## Editar un grupo de campos existente {#edit}

>[!NOTE]
>
>Solo los grupos de campos personalizados definidos por su organización se pueden editar y personalizar por completo. Para los grupos de campos principales definidos por Adobe, solo se pueden editar los nombres para mostrar de sus campos en el contexto de esquemas individuales. Consulte la sección sobre [edición de nombres para mostrar para campos de esquema](./schemas.md#display-names) para obtener más información.
>
>Una vez guardado un grupo de campos personalizados y utilizado en un esquema para la ingesta de datos, solo se pueden realizar cambios adicionales en el grupo de campos a partir de entonces. Consulte la [reglas de evolución de esquema](../../schema/composition.md#evolution) para obtener más información.

Para editar un grupo de campos existente, primero debe abrir un esquema que emplee el grupo de campos dentro del [!DNL Schema Editor]. Puede [seleccione un esquema existente para editarlo](./schemas.md#edit), o puede [crear un nuevo esquema](./schemas.md#create) y añada el grupo de campos en cuestión.

Una vez que tenga el esquema abierto en el editor, puede iniciar [adición de campos al grupo de campos](#add-fields).

## Adición de campos a un grupo de campos {#add-fields}

>[!NOTE]
>
>Esta sección se centra en agregar campos a grupos de campos personalizados. Para obtener información sobre cómo añadir campos personalizados a grupos de campos estándar, consulte la [guía de IU de esquemas](./schemas.md#custom-fields-for-standard-groups).

Para agregar campos a un grupo de campos personalizados, comience seleccionando la **más (+)** junto al nombre del esquema en el lienzo.

![](../../images/ui/resources/field-groups/add-field.png)

Un **[!UICONTROL Campo sin título]** el marcador de posición aparece en el lienzo y el carril derecho se actualiza para mostrar los controles y configurar las propiedades del campo. Consulte la guía de [definición de campos en la IU](../fields/overview.md#define) para ver los pasos específicos sobre cómo configurar diferentes tipos de campo.

En **[!UICONTROL Asignar a]**, seleccione la **[!UICONTROL Grupo de campos]** y, a continuación, utilice la lista desplegable para seleccionar el grupo de campos deseado en la lista. Puede empezar a escribir el nombre del grupo de campos para reducir los resultados.

![](../../images/ui/resources/field-groups/select-field-group.png)

En **[!UICONTROL Asignar a]**, seleccione la **[!UICONTROL Grupo de campos]** y, a continuación, utilice la lista desplegable para seleccionar el grupo de campos deseado en la lista. Puede empezar a escribir el nombre del grupo de campos para reducir los resultados.

![](../../images/ui/resources/field-groups/select-field-group.png)

Una vez agregado el campo al esquema, se asigna al grupo de campos seleccionado. Siga agregando tantos campos como sea necesario al grupo de campos. Cuando termine, seleccione **[!UICONTROL Guardar]** para guardar el esquema y el grupo de campos.

![](../../images/ui/resources/field-groups/complete-field-group.png)

Si el mismo grupo de campos ya se emplea en otros esquemas, los campos recién añadidos aparecerán automáticamente en esos esquemas.

## Pasos siguientes

En esta guía se explica cómo crear y editar grupos de campos mediante la IU de Platform. Para obtener más información sobre las capacidades de [!UICONTROL Esquemas] Workspace, consulte la [[!UICONTROL Esquemas] información general de workspace](../overview.md).

Para obtener información sobre cómo administrar grupos de campos mediante [!DNL Schema Registry] API, consulte la [guía de extremo de grupos de campos](../../api/field-groups.md).
