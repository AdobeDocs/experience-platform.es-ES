---
keywords: Experience Platform;inicio;temas populares;interfaz de usuario;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos;modelo de datos;editor de esquemas;editor de esquemas;esquema;esquemas;esquemas;crear;relación;referencia;referencia;
solution: Experience Platform
title: Definir una relación entre dos esquemas con el Editor de esquemas
description: Este documento proporciona un tutorial para definir una relación entre dos esquemas con el Editor de esquemas en la interfaz de usuario del Experience Platform.
type: Tutorial
exl-id: feed776b-bc8d-459b-9700-e5c9520788c0
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '1109'
ht-degree: 0%

---

# Defina una relación uno a uno entre dos esquemas mediante la variable [!DNL Schema Editor] {#relationship-ui}

>[!CONTEXTUALHELP]
>id="platform_schemas_relationships"
>title="Relaciones de esquema"
>abstract="Los esquemas pertenecientes a diferentes clases se pueden vincular contextualmente a través de campos de relación, lo que permite crear reglas de segmentación más complejas. Consulte la documentación para obtener más información sobre las relaciones de esquema."

>[!CONTEXTUALHELP]
>id="platform_xdm_1to1_reference_schema"
>title="Esquema de referencia"
>abstract="Seleccione el esquema con el que desea establecer una relación. Este esquema puede ser una clase diferente del esquema actual. Consulte la documentación para obtener más información sobre las relaciones de esquema."

>[!CONTEXTUALHELP]
>id="platform_xdm_1to1_identity_namespace"
>title="Área de nombres de identidad de referencia"
>abstract="El espacio de nombres (tipo) del campo de identidad principal del esquema de referencia. El esquema de referencia debe tener un campo de identidad principal establecido para participar en una relación. Consulte la documentación para obtener más información sobre las relaciones de esquema."

La capacidad de comprender las relaciones entre los clientes y sus interacciones con la marca a través de varios canales es una parte importante de Adobe Experience Platform. Definición de estas relaciones dentro de la estructura del [!DNL Experience Data Model] Los esquemas (XDM) le permiten obtener perspectivas complejas sobre los datos de sus clientes.

Mientras que las relaciones de esquema se pueden inferir mediante el uso del esquema de unión y [!DNL Real-Time Customer Profile], esto solo se aplica a esquemas que comparten la misma clase. Para establecer una relación entre dos esquemas pertenecientes a diferentes clases, se debe agregar un campo de relación dedicado a un esquema de origen que haga referencia a la identidad del otro esquema relacionado.

Este documento proporciona un tutorial para definir una relación entre dos esquemas con el Editor de esquemas en la [!DNL Experience Platform] interfaz de usuario. Para ver los pasos sobre la definición de relaciones de esquema mediante la API, consulte el tutorial sobre [definición de una relación mediante la API del Registro de Esquemas](relationship-api.md).

>[!NOTE]
>
>Para ver los pasos sobre cómo crear una relación &quot;varios a uno&quot; en Adobe Real-time Customer Data Platform B2B Edition, consulte la guía de [creación de relaciones B2B](./relationship-b2b.md).

## Primeros pasos

Este tutorial requiere una comprensión práctica de [!DNL XDM System] y el Editor de esquemas en la [!DNL Experience Platform] IU. Antes de comenzar este tutorial, consulte la siguiente documentación:

* [Sistema XDM en Experience Platform](../home.md): Información general sobre XDM y su implementación en [!DNL Experience Platform].
* [Aspectos básicos de la composición del esquema](../schema/composition.md): Introducción de los componentes básicos de los esquemas XDM.
* [Cree un esquema utilizando la variable [!DNL Schema Editor]](create-schema-ui.md): Un tutorial que cubre los conceptos básicos del trabajo con la variable [!DNL Schema Editor].

## Definición de un esquema de origen y referencia

Se espera que ya haya creado los dos esquemas que se definirán en la relación. Para fines de demostración, este tutorial crea una relación entre los miembros del programa de lealtad de una organización (definido en un[!DNL Loyalty Members]&quot; esquema) y su hotel favorito (definido en un[!DNL Hotels]&quot; esquema).

>[!IMPORTANT]
>
>Para establecer una relación, ambos esquemas deben tener definidas identidades principales y estar habilitados para [!DNL Real-Time Customer Profile]. Consulte la sección sobre [activación de un esquema para su uso en Perfil](./create-schema-ui.md#profile) en el tutorial de creación de esquemas si necesita instrucciones sobre cómo configurar los esquemas en consecuencia.

Las relaciones de esquema se representan mediante un campo dedicado dentro de un **esquema de origen** que señala a otro campo dentro de un **esquema de referencia**. En los pasos siguientes, &quot;[!DNL Loyalty Members]&quot; será el esquema de origen, mientras que &quot;[!DNL Hotels]&quot; actuará como esquema de referencia.

Las siguientes secciones describen la estructura de cada esquema utilizado en este tutorial antes de que se haya definido una relación.

### [!DNL Loyalty Members] esquema

El esquema de origen &quot;[!DNL Loyalty Members]&quot; se basa en la variable [!DNL XDM Individual Profile] , que contiene el campo que describe los miembros de un programa de fidelidad. Uno de estos campos, `personalEmail.addess`, sirve como identidad principal para el esquema en la variable [!UICONTROL Correo electrónico] espacio de nombres. Como se ve en **[!UICONTROL Propiedades del esquema]**, este esquema se ha habilitado para utilizarse en [!DNL Real-Time Customer Profile].

![](../images/tutorials/relationship/loyalty-members.png)

### [!DNL Hotels] esquema

El esquema de referencia &quot;[!DNL Hotels]&quot; se basa en un &quot;[!DNL Hotels]&quot; clase, y contiene campos que describen un hotel. Para participar en una relación, el esquema de referencia también debe tener una identidad principal definida y habilitada para [!UICONTROL Perfil]. En este caso, `_tenantId.hotelId`actúa como la identidad principal del esquema, utilizando un &quot;[!DNL Hotel ID]&quot; área de nombres de identidad.

![Habilitar para perfil](../images/tutorials/relationship/hotels.png)

>[!NOTE]
>
>Para aprender a crear áreas de nombres de identidad personalizadas, consulte la [Documentación del servicio de identidad](../../identity-service/namespaces.md#manage-namespaces).

## Crear un grupo de campos de relación

>[!NOTE]
>
>Este paso solo es necesario si el esquema de origen no tiene un campo dedicado de tipo cadena que se vaya a utilizar como puntero a la identidad principal del esquema de referencia. Si este campo ya está definido en el esquema de origen, vaya al paso siguiente de [definición de un campo de relación](#relationship-field).

Para definir una relación entre dos esquemas, el esquema de origen debe tener un campo dedicado que indique la identidad principal del esquema de referencia. Puede añadir este campo al esquema de origen creando un nuevo grupo de campos de esquema o ampliando uno existente.

En el caso del [!DNL Loyalty Members] esquema, un nuevo `preferredHotel` se agregará para indicar el hotel preferido del miembro socio para las visitas de la empresa. Comience por seleccionar el icono del signo más (**+**) junto al nombre del esquema de origen.

![](../images/tutorials/relationship/loyalty-add-field.png)

Aparece un nuevo marcador de posición de campo en el lienzo. En **[!UICONTROL Propiedades del campo]**, proporcione un nombre de campo y un nombre para mostrar para el campo y establezca su tipo en &quot;[!UICONTROL Cadena]&quot;. En **[!UICONTROL Asignar a]**, seleccione un grupo de campos existente para ampliar o escriba un nombre único para crear un nuevo grupo de campos. En este caso, un nuevo &quot;[!DNL Preferred Hotel]&quot; grupo de campos.

![](../images/tutorials/relationship/relationship-field-details.png)

Cuando termine, seleccione **[!UICONTROL Aplicar]**.

![](../images/tutorials/relationship/relationship-field-apply.png)

El `preferredHotel` aparece en el lienzo, ubicado debajo de un `_tenantId` porque es un campo personalizado. Select **[!UICONTROL Guardar]** para finalizar los cambios en el esquema.

![](../images/tutorials/relationship/relationship-field-save.png)

## Definir un campo de relación para el esquema de origen {#relationship-field}

Una vez que el esquema de origen tiene un campo de referencia dedicado definido, puede designarlo como campo de relación.

>[!NOTE]
>
>Los pasos siguientes explican cómo definir un campo de relación utilizando los controles del carril derecho del lienzo. Si tiene acceso a Real-Time CDP B2B Edition, también puede definir una relación &quot;uno a uno&quot; mediante el [mismo cuadro de diálogo](./relationship-b2b.md#relationship-field) al igual que cuando se crean relaciones &quot;varios a uno&quot;.

Seleccione el `preferredHotel` en el lienzo, desplácese hacia abajo por debajo **[!UICONTROL Propiedades del campo]** hasta que **[!UICONTROL Relación]** aparecerá la casilla de verificación. Seleccione la casilla de verificación para mostrar los parámetros necesarios para configurar un campo de relación.

![](../images/tutorials/relationship/relationship-checkbox.png)

Seleccione la lista desplegable para **[!UICONTROL Esquema de referencia]** y seleccione el esquema de referencia para la relación (&quot;[!DNL Hotels]&quot; en este ejemplo). En **[!UICONTROL Área de nombres de identidad de referencia]**, seleccione el área de nombres del campo de identidad del esquema de referencia (en este caso, &quot;[!DNL Hotel ID]&quot;). Select **[!UICONTROL Aplicar]** cuando termine.

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

La variable `preferredHotel` ahora se resalta como una relación en el lienzo, mostrando el nombre del esquema de referencia. Select **[!UICONTROL Guardar]** para guardar los cambios y completar el flujo de trabajo.

![](../images/tutorials/relationship/relationship-save.png)

## Pasos siguientes

Siguiendo este tutorial, se ha creado correctamente una relación &quot;uno a uno&quot; entre dos esquemas con la variable [!DNL Schema Editor]. Para ver los pasos sobre cómo definir relaciones mediante la API, consulte el tutorial sobre [definición de una relación mediante la API del Registro de Esquemas](relationship-api.md).
