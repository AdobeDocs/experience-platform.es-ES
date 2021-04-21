---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos;ui;espacio de trabajo;clase;clases;
solution: Experience Platform
title: Crear y editar clases en la interfaz de usuario
description: Obtenga información sobre cómo crear y editar clases en la interfaz de usuario del Experience Platform.
topic-legacy: user guide
exl-id: 1b4c3996-2319-45dd-9edd-a5bcad46578b
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '865'
ht-degree: 0%

---

# Crear y editar clases en la interfaz de usuario

En Experience Data Model (XDM), las clases definen los aspectos de comportamiento de los datos que contendrá un esquema (registro o serie temporal). Además de esto, las clases describen el menor número de propiedades comunes que todos los esquemas basados en esa clase necesitarían para incluir y proporcionar una forma de combinar varios conjuntos de datos compatibles.

Adobe proporciona varias clases XDM estándar (&quot;core&quot;), incluidas [!DNL XDM Individual Profile] y [!DNL XDM ExperienceEvent]. Además de estas clases principales, también puede crear sus propias clases personalizadas para describir casos de uso más específicos para su organización.

Este documento proporciona información general sobre cómo crear, editar y administrar clases personalizadas en la interfaz de usuario de Adobe Experience Platform.

## Requisitos previos

Esta guía requiere una comprensión práctica del sistema XDM. Consulte la [información general de XDM](../../home.md) para obtener una introducción a la función de XDM dentro del ecosistema del Experience Platform y los [conceptos básicos de la composición del esquema](../../schema/composition.md) para conocer cómo las clases contribuyen a los esquemas XDM.

Aunque no es necesario para esta guía, se recomienda seguir también el tutorial sobre [composición de un esquema en la interfaz de usuario](../../tutorials/create-schema-ui.md) para familiarizarse con las distintas capacidades de [!DNL Schema Editor].

## Crear una nueva clase {#create}

En el espacio de trabajo **[!UICONTROL Schemas]**, seleccione **[!UICONTROL Create schema]** y, a continuación, seleccione **[!UICONTROL Browse]** en la lista desplegable.

![](../../images/ui/resources/classes/browse-classes.png)

Aparece un cuadro de diálogo que le permite seleccionar entre una lista de clases disponibles. En la parte superior del cuadro de diálogo, seleccione **[!UICONTROL Create new class]**. A continuación, puede darle a la nueva clase un nombre para mostrar (un nombre corto, descriptivo, único y descriptivo para la clase), una descripción y un comportamiento para los datos que el esquema definirá (&quot;[!UICONTROL Record]&quot; o &quot;[!UICONTROL Time-series]&quot;).

Cuando termine, seleccione **[!UICONTROL Assign class]**.

![](../../images/ui/resources/classes/class-details.png)

Aparece el [!DNL Schema Editor], que muestra un nuevo esquema en el lienzo basado en la clase personalizada que acaba de crear. Dado que todavía no se han agregado campos a la clase, el esquema solo contiene un campo `_id`, que representa el identificador único generado por el sistema que se aplica automáticamente a todos los recursos en [!DNL Schema Registry].

![](../../images/ui/resources/classes/schema.png)

>[!IMPORTANT]
>
>Al crear un esquema que implemente una clase definida por su organización, recuerde que las mezclas están disponibles para su uso únicamente con clases compatibles. Como la clase que ha definido es nueva, no hay mezclas compatibles enumeradas en el cuadro de diálogo **[!UICONTROL Add mixin]**. En su lugar, necesitará [crear nuevas mezclas](./mixins.md#create) para usarlas con esa clase. La próxima vez que componga un esquema que implemente la nueva clase, las mezclas que haya definido se enumerarán y estarán disponibles para su uso.

Ahora puede empezar a [añadir campos a la clase](#add-fields), que compartirán todos los esquemas que empleen la clase.

## Editar una clase existente {#edit}

>[!NOTE]
>
>Solo las clases personalizadas definidas por su organización pueden editarse y personalizarse completamente. Para las clases principales definidas por Adobe, solo se pueden editar los nombres para mostrar de sus campos en el contexto de esquemas individuales. Consulte la sección sobre [edición de nombres para mostrar para campos de esquema](./schemas.md#display-names) para obtener más información.
>
>Una vez que se ha guardado y utilizado una clase personalizada en el consumo de datos, solo se pueden realizar cambios aditivos en ella posteriormente. Consulte las [reglas de evolución de esquema](../../schema/composition.md#evolution) para obtener más información.

Para editar una clase existente, seleccione la pestaña **[!UICONTROL Browse]** y, a continuación, seleccione el nombre de un esquema que emplea la clase que desea editar.

![](../../images/ui/resources/classes/select-for-edit.png)

>[!TIP]
>
>Puede utilizar las capacidades de búsqueda y filtrado del espacio de trabajo para ayudar a encontrar el esquema más fácil. Consulte la guía sobre [exploración de recursos XDM](../explore.md) para obtener más información.

Aparece el [!DNL Schema Editor], con la estructura del esquema mostrada en el lienzo. Ahora puede empezar a [añadir campos a la clase](#add-fields).

![](../../images/ui/resources/classes/edit.png)

## Añadir campos a una clase {#add-fields}

Una vez que tenga un esquema que emplee una clase personalizada abierta en [!UICONTROL Schema Editor], puede empezar a añadir campos a la clase. Para agregar un nuevo campo, seleccione el icono **plus (+)** junto al nombre del esquema.

![](../../images/ui/resources/classes/add-field.png)

>[!IMPORTANT]
>
>Tenga en cuenta que cualquier campo que agregue a una clase se utilizará en todos los esquemas que empleen esa clase. Por lo tanto, debe tener en cuenta qué campos serán útiles en todos los casos de uso del esquema. Si está pensando en añadir un campo que solo pueda verse utilizado en algunos esquemas de esta clase, puede que desee considerar la posibilidad de añadirlo a esos esquemas [creando una mezcla](./mixins.md#create) en su lugar.

Aparece un **[!UICONTROL New field]** en el lienzo y el carril derecho se actualiza para mostrar los controles que configuran las propiedades del campo. Consulte la guía de [definición de campos en la interfaz de usuario](../fields/overview.md#define) para ver los pasos específicos sobre cómo configurar y añadir el campo a la clase.

Siga agregando tantos campos como sea necesario a la clase. Cuando termine, seleccione **[!UICONTROL Save]** para guardar el esquema y la clase.

![](../../images/ui/resources/classes/save.png)

Si ha creado esquemas anteriormente que emplean esta clase, los campos recién añadidos aparecerán automáticamente en esos esquemas.

## Cambiar la clase de un esquema {#schema}

Puede cambiar la clase del esquema en cualquier momento durante el proceso de creación inicial antes de guardarlo. Consulte la guía sobre [creación y edición de esquemas](./schemas.md#change-class) para obtener más información.

## Pasos siguientes

Este documento trata sobre cómo crear y editar clases mediante la interfaz de usuario de Platform. Para obtener más información sobre las capacidades del espacio de trabajo [!UICONTROL Schemas], consulte la [[!UICONTROL Schemas] descripción general del espacio de trabajo](../overview.md).

Para aprender a administrar clases usando la API [!DNL Schema Registry], consulte la [guía de extremo de clases](../../api/classes.md).
