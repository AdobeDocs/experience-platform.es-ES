---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos;ui;espacio de trabajo;mezcla;mezclas
solution: Experience Platform
title: Crear y editar mezclas en la interfaz de usuario
description: Aprenda a crear y editar mezclas en la interfaz de usuario del Experience Platform.
topic-legacy: user guide
exl-id: 240b857d-75ad-42fd-9249-050cbc5306a9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 0%

---

# Crear y editar mezclas en la interfaz de usuario

En el Modelo de datos de experiencia (XDM), las mezclas son componentes reutilizables que definen uno o más campos que implementan determinadas funciones, como detalles personales, preferencias de hotel o dirección. Las mezclas están pensadas para incluirse como parte de un esquema que implemente una clase compatible.

Una mezcla define con qué clase(es) es compatible, en función del comportamiento de los datos que representa la mezcla (registro o serie temporal). Esto significa que no todas las mezclas están disponibles para su uso con todas las clases.

Adobe Experience Platform proporciona muchas mezclas estándar que cubren una amplia gama de casos de uso de marketing. Sin embargo, también puede crear y editar sus propias mezclas personalizadas para definir conceptos adicionales relacionados con su negocio dentro de sus esquemas XDM. Esta guía proporciona información general sobre cómo crear, editar y administrar mezclas personalizadas para su organización en la interfaz de usuario de Platform.

## Requisitos previos

Esta guía requiere una comprensión práctica del sistema XDM. Consulte la [información general de XDM](../../home.md) para obtener una introducción a la función de XDM dentro del ecosistema del Experience Platform y los [conceptos básicos de la composición del esquema](../../schema/composition.md) para saber cómo las mezclas contribuyen a los esquemas de XDM.

Aunque no es necesario para esta guía, se recomienda seguir también el tutorial sobre [composición de un esquema en la interfaz de usuario](../../tutorials/create-schema-ui.md) para familiarizarse con las distintas capacidades de [!DNL Schema Editor].

## Crear una nueva mezcla {#create}

Para crear una nueva mezcla, primero debe seleccionar un esquema al que se añadirá la mezcla. Puede elegir [crear un nuevo esquema](./schemas.md#create) o [seleccionar un esquema existente para editar](./schemas.md#edit).

Una vez que haya abierto el esquema en [!DNL Schema Editor], seleccione **[!UICONTROL Add]** junto a la sección [!UICONTROL Mixins] en el carril izquierdo.

![](../../images/ui/resources/mixins/add-mixin-button.png)

Aparece un cuadro de diálogo que muestra una lista de mezclas existentes para su organización. Cerca de la parte superior del cuadro de diálogo, seleccione **[!UICONTROL Create new mixin]**. Aquí puede proporcionar un **[!UICONTROL Display name]** y **[!UICONTROL Description]** para la mezcla. Cuando termine, seleccione **[!UICONTROL Add mixin]**.

![](../../images/ui/resources/mixins/create-mixin.png)

La [!DNL Schema Editor] vuelve a aparecer, con la nueva mezcla listada en el carril izquierdo. Como se trata de una mezcla completamente nueva, actualmente no proporciona ningún campo al esquema y, por lo tanto, el lienzo permanece sin cambios. Ahora puede empezar a [añadir campos a la mezcla](#add-fields).

## Editar una mezcla existente {#edit}

>[!NOTE]
>
>Solo las mezclas personalizadas definidas por su organización pueden editarse y personalizarse completamente. Para las mezclas principales definidas por Adobe, solo los nombres para mostrar de sus campos se pueden editar dentro del contexto de esquemas individuales. Consulte la sección sobre [edición de nombres para mostrar para campos de esquema](./schemas.md#display-names) para obtener más información.
>
>Una vez guardada y utilizada una mezcla personalizada en un esquema para la ingesta de datos, sólo se pueden realizar cambios aditivos en la mezcla posteriormente. Consulte las [reglas de evolución de esquema](../../schema/composition.md#evolution) para obtener más información.

Para editar una mezcla existente, primero debe abrir un esquema que emplee la mezcla dentro de [!DNL Schema Editor]. Puede [seleccionar un esquema existente para editarlo](./schemas.md#edit) o puede [crear un nuevo esquema](./schemas.md#create) y añadir la mezcla en cuestión.

Una vez que haya abierto el esquema en el editor, puede empezar a [añadir campos a la mezcla](#add-fields).

## Añadir campos a una mezcla {#add-fields}

Para añadir campos a una mezcla en el [!DNL Schema Editor], comience seleccionando el nombre de la mezcla en el carril izquierdo y, a continuación, seleccione el icono **plus (+)** situado junto al nombre del esquema en el lienzo.

![](../../images/ui/resources/mixins/add-field-button.png)

Aparece un **[!UICONTROL New field]** en el lienzo y el carril derecho se actualiza para mostrar los controles que configuran las propiedades del campo. Consulte la guía sobre la [definición de campos en la IU](../fields/overview.md#define) para ver los pasos específicos sobre cómo configurar y añadir el campo a la mezcla.

Siga agregando tantos campos como sea necesario a la mezcla. Cuando termine, seleccione **[!UICONTROL Save]** para guardar el esquema y la mezcla.

![](../../images/ui/resources/mixins/complete-mixin.png)

Si la misma mezcla ya está empleada en otros esquemas, los campos recién añadidos aparecerán automáticamente en esos esquemas.

## Pasos siguientes

Esta guía explica cómo crear y editar mezclas mediante la interfaz de usuario de Platform. Para obtener más información sobre las capacidades del espacio de trabajo [!UICONTROL Schemas], consulte la [[!UICONTROL Schemas] descripción general del espacio de trabajo](../overview.md).

Para aprender a administrar las mezclas utilizando la API [!DNL Schema Registry], consulte la [guía de extremo de las mezclas](../../api/mixins.md).
