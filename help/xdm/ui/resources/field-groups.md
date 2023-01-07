---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos;ui;espacio de trabajo;grupo de campos;grupos de campos;
solution: Experience Platform
title: Crear y editar grupos de campos de esquema en la interfaz de usuario
description: Obtenga información sobre cómo crear y editar grupos de campos de esquema en la interfaz de usuario del Experience Platform.
topic-legacy: user guide
exl-id: 928d70a6-0468-4fb7-a53a-6686ac77f2a3
source-git-commit: 57e7386ad631f2ce3d9b28d2532655a2668bdcaa
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 0%

---

# Creación y edición de grupos de campos de esquema en la interfaz de usuario

En Experience Data Model (XDM), los grupos de campos de esquema son componentes reutilizables que definen uno o más campos que implementan determinadas funciones, como detalles personales, preferencias de hotel o dirección. Los grupos de campos están pensados para incluirse como parte de un esquema que implemente una clase compatible.

Un grupo de campos define con qué clases es compatible, en función del comportamiento de los datos que representa el grupo de campos (registro o serie temporal). Esto significa que no todos los grupos de campos están disponibles para su uso con todas las clases.

Adobe Experience Platform proporciona muchos grupos de campos estándar que abarcan una amplia gama de casos de uso de marketing. Sin embargo, también puede crear y editar sus propios grupos de campos personalizados para definir conceptos adicionales relacionados con su negocio dentro de los esquemas XDM. Esta guía proporciona información general sobre cómo crear, editar y administrar grupos de campos personalizados para su organización en la interfaz de usuario de Platform.

## Requisitos previos

Esta guía requiere una comprensión práctica del sistema XDM. Consulte la [Información general de XDM](../../home.md) para una introducción al papel de XDM dentro del ecosistema del Experience Platform, y [conceptos básicos de la composición del esquema](../../schema/composition.md) para saber cómo contribuyen los grupos de campos a los esquemas XDM.

Aunque no es necesario para esta guía, se recomienda seguir también el tutorial de [composición de un esquema en la interfaz de usuario](../../tutorials/create-schema-ui.md) para familiarizarse con las diversas capacidades de la [!DNL Schema Editor].

## Crear un nuevo grupo de campos {#create}

Para crear un nuevo grupo de campos, primero debe seleccionar un esquema al que se agregará el grupo de campos. Puede elegir [crear un nuevo esquema](./schemas.md#create) o [seleccionar un esquema existente para editar](./schemas.md#edit).

Una vez que haya abierto el esquema en la variable [!DNL Schema Editor], seleccione **[!UICONTROL Agregar]** junto a la variable [!UICONTROL Grupos de campo] en el carril izquierdo.

![](../../images/ui/resources/field-groups/add-field-group.png)

En el cuadro de diálogo que aparece, seleccione **[!UICONTROL Crear nuevo grupo de campos]**. Aquí puede proporcionar un **[!UICONTROL Nombre para mostrar]** y **[!UICONTROL Descripción]** para el grupo de campos. Cuando termine, seleccione **[!UICONTROL Agregar grupos de campos]**.

![](../../images/ui/resources/field-groups/create-field-group.png)

La variable [!DNL Schema Editor] vuelve a aparecer, con el nuevo grupo de campos enumerado en el carril izquierdo. Dado que se trata de un grupo de campos completamente nuevo, actualmente no proporciona ningún campo al esquema y, por lo tanto, el lienzo permanece sin cambios. Ahora puede empezar [adición de campos al grupo de campos](#add-fields).

![](../../images/ui/resources/field-groups/field-group-added.png)

## Editar un grupo de campos existente {#edit}

>[!NOTE]
>
>Solo los grupos de campos personalizados definidos por su organización pueden editarse y personalizarse completamente. Para los grupos de campos principales definidos por el Adobe, solo se pueden editar los nombres para mostrar de sus campos en el contexto de esquemas individuales. Consulte la sección sobre [edición de nombres para mostrar en campos de esquema](./schemas.md#display-names) para obtener más información.
>
>Una vez guardado y utilizado un grupo de campos personalizados en un esquema para la ingesta de datos, solo se pueden realizar cambios adicionales en el grupo de campos a partir de entonces. Consulte la [reglas de evolución de esquema](../../schema/composition.md#evolution) para obtener más información.

Para editar un grupo de campos existente, primero debe abrir un esquema que emplee el grupo de campos dentro del [!DNL Schema Editor]. Puede [seleccionar un esquema existente para editar](./schemas.md#edit)o puede [crear un nuevo esquema](./schemas.md#create) y añada el grupo de campos en cuestión.

Una vez que haya abierto el esquema en el editor, puede empezar [adición de campos al grupo de campos](#add-fields).

## Adición de campos a un grupo de campos {#add-fields}

>[!NOTE]
>
>Esta sección se centra en añadir campos a grupos de campos personalizados. Para obtener información sobre cómo agregar campos personalizados a grupos de campos estándar, consulte la [guía de la interfaz de usuario de schemas](./schemas.md#custom-fields-for-standard-groups).

Para agregar campos a un grupo de campos personalizados, comience por seleccionar la variable **plus (+)** junto al nombre del esquema en el lienzo.

![](../../images/ui/resources/field-groups/add-field.png)

A **[!UICONTROL Campo nuevo]** aparece en el lienzo, y el carril derecho se actualiza para mostrar los controles y configurar las propiedades del campo. Consulte la guía de [definición de campos en la interfaz de usuario](../fields/overview.md#define) para ver pasos específicos sobre cómo configurar diferentes tipos de campos.

En **[!UICONTROL Asignar a]**, seleccione **[!UICONTROL Grupo de campos]** , utilice la lista desplegable para seleccionar el grupo de campos deseado de la lista. Puede empezar a escribir en el nombre del grupo de campos para reducir los resultados.

![](../../images/ui/resources/field-groups/select-field-group.png)

Una vez agregado el campo al esquema, se asigna al grupo de campos seleccionado. Siga agregando tantos campos como sea necesario al grupo de campos. Cuando termine, seleccione **[!UICONTROL Guardar]** para guardar el esquema y el grupo de campos.

![](../../images/ui/resources/field-groups/complete-field-group.png)

Si el mismo grupo de campos ya está empleado en otros esquemas, los campos recién añadidos aparecerán automáticamente en esos esquemas.

## Pasos siguientes

Esta guía explica cómo crear y editar grupos de campos mediante la interfaz de usuario de Platform. Para obtener más información sobre las capacidades de la variable [!UICONTROL Esquemas] espacio de trabajo, consulte [[!UICONTROL Esquemas] información general del espacio de trabajo](../overview.md).

Para obtener información sobre cómo administrar grupos de campos mediante la variable [!DNL Schema Registry] API, consulte la [guía de extremo de grupos de campos](../../api/field-groups.md).
