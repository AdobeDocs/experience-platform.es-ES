---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;experience data model;data model;ui;workspace;field group;field groups;
solution: Experience Platform
title: Crear y editar grupos de campos de esquema en la interfaz de usuario
description: Obtenga información sobre cómo crear y editar grupos de campos de esquema en la interfaz de usuario del Experience Platform.
topic-legacy: user guide
exl-id: 928d70a6-0468-4fb7-a53a-6686ac77f2a3
source-git-commit: 716250b8bcfa1b2d9c868aa80b3122da401553b9
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 0%

---

# Creación y edición de grupos de campos de esquema en la interfaz de usuario

En Experience Data Model (XDM), los grupos de campos de esquema son componentes reutilizables que definen uno o más campos que implementan determinadas funciones, como detalles personales, preferencias de hotel o dirección. Los grupos de campos están pensados para incluirse como parte de un esquema que implemente una clase compatible.

Un grupo de campos define con qué clases es compatible, en función del comportamiento de los datos que representa el grupo de campos (registro o serie temporal). Esto significa que no todos los grupos de campos están disponibles para su uso con todas las clases.

Adobe Experience Platform proporciona muchos grupos de campos estándar que abarcan una amplia gama de casos de uso de marketing. Sin embargo, también puede crear y editar sus propios grupos de campos personalizados para definir conceptos adicionales relacionados con su negocio dentro de los esquemas XDM. Esta guía proporciona información general sobre cómo crear, editar y administrar grupos de campos personalizados para su organización en la interfaz de usuario de Platform.

## Requisitos previos

Esta guía requiere una comprensión práctica del sistema XDM. Consulte la [Información general de XDM](../../home.md) para una introducción al papel de XDM dentro del ecosistema del Experience Platform, y [conceptos básicos de la composición del esquema](../../schema/composition.md) para saber cómo contribuyen los grupos de campos a los esquemas XDM.

While not required for this guide, it is recommended that you also follow the tutorial on [composing a schema in the UI](../../tutorials/create-schema-ui.md) to familiarize yourself with the various capabilities of the [!DNL Schema Editor].

## Crear un nuevo grupo de campos {#create}

To create a new field group, you must first select a schema that the field group will be added to. Puede elegir [crear un nuevo esquema](./schemas.md#create) o [seleccionar un esquema existente para editar](./schemas.md#edit).

Una vez que haya abierto el esquema en la variable [!DNL Schema Editor], seleccione **[!UICONTROL Agregar]** junto a la variable [!UICONTROL Grupos de campo] en el carril izquierdo.

![](../../images/ui/resources/field-groups/add-field-group.png)

Aparece un cuadro de diálogo que muestra una lista de los grupos de campos existentes para su organización. Cerca de la parte superior del cuadro de diálogo, seleccione **[!UICONTROL Crear nuevo grupo de campos]**. Aquí puede proporcionar un **[!UICONTROL Nombre para mostrar]** y **[!UICONTROL Descripción]** para el grupo de campos. Cuando termine, seleccione **[!UICONTROL Agregar grupo de campos]**.

![](../../images/ui/resources/field-groups/create-field-group.png)

La variable [!DNL Schema Editor] vuelve a aparecer, con el nuevo grupo de campos enumerado en el carril izquierdo. Dado que se trata de un grupo de campos completamente nuevo, actualmente no proporciona ningún campo al esquema y, por lo tanto, el lienzo permanece sin cambios. Ahora puede empezar [adición de campos al grupo de campos](#add-fields).

## Editar un grupo de campos existente {#edit}

>[!NOTE]
>
>Solo los grupos de campos personalizados definidos por su organización pueden editarse y personalizarse completamente. Para los grupos de campos principales definidos por el Adobe, solo se pueden editar los nombres para mostrar de sus campos en el contexto de esquemas individuales. Consulte la sección sobre [edición de nombres para mostrar en campos de esquema](./schemas.md#display-names) para obtener más información.
>
>Once a custom field group has been saved and used in a schema for data ingestion, only additive changes can be made to the field group thereafter. Consulte la [reglas de evolución de esquema](../../schema/composition.md#evolution) para obtener más información.

Para editar un grupo de campos existente, primero debe abrir un esquema que emplee el grupo de campos dentro del [!DNL Schema Editor]. Puede [seleccionar un esquema existente para editar](./schemas.md#edit)o puede [crear un nuevo esquema](./schemas.md#create) y añada el grupo de campos en cuestión.

Una vez que haya abierto el esquema en el editor, puede empezar [adición de campos al grupo de campos](#add-fields).

## Adición de campos a un grupo de campos {#add-fields}

>[!NOTE]
>
>Esta sección se centra en añadir campos a grupos de campos personalizados. Para obtener información sobre cómo agregar campos personalizados a grupos de campos estándar, consulte la [guía de la interfaz de usuario de schemas](./schemas.md#custom-fields-for-standard-groups).

Adición de campos a un grupo de campos personalizados en la variable [!DNL Schema Editor], comience por seleccionar el nombre del grupo de campos en el carril izquierdo y, a continuación, seleccione la opción **plus (+)** junto al nombre del esquema en el lienzo.

![](../../images/ui/resources/field-groups/add-field.png)

A **[!UICONTROL Campo nuevo]** aparece en el lienzo, y el carril derecho se actualiza para mostrar los controles y configurar las propiedades del campo. Consulte la guía de [definición de campos en la interfaz de usuario](../fields/overview.md#define) para ver pasos específicos sobre cómo configurar y añadir el campo al grupo de campos.

Siga agregando tantos campos como sea necesario al grupo de campos. Cuando termine, seleccione **[!UICONTROL Guardar]** para guardar el esquema y el grupo de campos.

![](../../images/ui/resources/field-groups/complete-field-group.png)

Si el mismo grupo de campos ya está empleado en otros esquemas, los campos recién añadidos aparecerán automáticamente en esos esquemas.

## Pasos siguientes

This guide covered how to create and edit field groups using the Platform UI. For more information on the capabilities of the [!UICONTROL Schemas] workspace, see the [[!UICONTROL Schemas] workspace overview](../overview.md).

Para obtener información sobre cómo administrar grupos de campos mediante la variable [!DNL Schema Registry] API, consulte la [guía de extremo de grupos de campos](../../api/field-groups.md).
