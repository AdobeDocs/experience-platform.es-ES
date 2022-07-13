---
keywords: Experience Platform;inicio;temas populares;interfaz de usuario;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos;modelo de datos;editor de esquemas;editor de esquemas;esquema;esquemas;esquemas;crear;relación;referencia;referencia;
solution: Experience Platform
title: Definir una relación entre dos esquemas con el Editor de esquemas
description: Este documento proporciona un tutorial para definir una relación entre dos esquemas con el Editor de esquemas en la interfaz de usuario del Experience Platform.
topic-legacy: tutorial
type: Tutorial
exl-id: feed776b-bc8d-459b-9700-e5c9520788c0
source-git-commit: a95e5cf02e993d6c761abd74c98c0967a89eb678
workflow-type: tm+mt
source-wordcount: '1172'
ht-degree: 0%

---

# Defina una relación uno a uno entre dos esquemas mediante la variable [!DNL Schema Editor]

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

Mientras que las relaciones de esquema se pueden inferir mediante el uso del esquema de unión y [!DNL Real-time Customer Profile], esto solo se aplica a esquemas que comparten la misma clase. Para establecer una relación entre dos esquemas pertenecientes a diferentes clases, se debe agregar un campo de relación dedicado a un esquema de origen que haga referencia a la identidad de un esquema de destino.

Este documento proporciona un tutorial para definir una relación entre dos esquemas con el Editor de esquemas en la [!DNL Experience Platform] interfaz de usuario. Para ver los pasos sobre la definición de relaciones de esquema mediante la API, consulte el tutorial sobre [definición de una relación mediante la API del Registro de Esquemas](relationship-api.md).

>[!NOTE]
>
>Para ver los pasos sobre cómo crear una relación &quot;varios a uno&quot; en Real-time Customer Data Platform B2B Edition, consulte la guía de [creación de relaciones B2B](./relationship-b2b.md).

## Primeros pasos

Este tutorial requiere una comprensión práctica de [!DNL XDM System] y el Editor de esquemas en la [!DNL Experience Platform] IU. Antes de comenzar este tutorial, consulte la siguiente documentación:

* [Sistema XDM en Experience Platform](../home.md): Información general sobre XDM y su implementación en [!DNL Experience Platform].
* [Aspectos básicos de la composición del esquema](../schema/composition.md): Introducción de los componentes básicos de los esquemas XDM.
* [Cree un esquema utilizando la variable [!DNL Schema Editor]](create-schema-ui.md): Un tutorial que cubre los conceptos básicos del trabajo con la variable [!DNL Schema Editor].

## Definir un esquema de origen y destino

Se espera que ya haya creado los dos esquemas que se definirán en la relación. Para fines de demostración, este tutorial crea una relación entre los miembros del programa de lealtad de una organización (definido en un[!DNL Loyalty Members]&quot; esquema) y su hotel favorito (definido en un[!DNL Hotels]&quot; esquema).

>[!IMPORTANT]
>
>Para establecer una relación, ambos esquemas deben tener definidas identidades principales y estar habilitados para [!DNL Real-time Customer Profile]. Consulte la sección sobre [activación de un esquema para su uso en Perfil](./create-schema-ui.md#profile) en el tutorial de creación de esquemas si necesita instrucciones sobre cómo configurar los esquemas en consecuencia.

Las relaciones de esquema se representan mediante un campo dedicado dentro de un **esquema de origen** que hace referencia a otro campo dentro de un **esquema de destino**. En los pasos siguientes, &quot;[!DNL Loyalty Members]&quot; será el esquema de origen, mientras que &quot;[!DNL Hotels]&quot; actuará como esquema de destino.

Con fines de referencia, las secciones siguientes describen la estructura de cada esquema utilizado en este tutorial antes de que se haya definido una relación.

### [!DNL Loyalty Members] esquema

El esquema de origen &quot;[!DNL Loyalty Members]&quot; se basa en la variable [!DNL XDM Individual Profile] y es el esquema que se construyó en el tutorial para [creación de un esquema en la interfaz de usuario](create-schema-ui.md). Incluye un `loyalty` objeto debajo de `_tenantId` área de nombres, que incluye varios campos específicos de lealtad. Uno de estos campos, `loyaltyId`, sirve como identidad principal para el esquema en la variable [!UICONTROL Correo electrónico] espacio de nombres. Como se ve en **[!UICONTROL Propiedades del esquema]**, este esquema se ha habilitado para utilizarse en [!DNL Real-time Customer Profile].

![](../images/tutorials/relationship/loyalty-members.png)

### [!DNL Hotels] esquema

El esquema de destino &quot;[!DNL Hotels]&quot; se basa en un &quot;[!DNL Hotels]&quot; clase, y contiene campos que describen un hotel.

![](../images/tutorials/relationship/hotels.png)

Para participar en una relación, el esquema de destino debe tener una identidad principal. En este ejemplo, la variable `hotelId` se utiliza como identidad principal, utilizando un área de nombres de identidad &quot;ID de hotel&quot; personalizada.

![Identidad primaria del hotel](../images/tutorials/relationship/hotel-identity.png)

>[!NOTE]
>
>Para aprender a crear áreas de nombres de identidad personalizadas, consulte la [Documentación del servicio de identidad](../../identity-service/namespaces.md#manage-namespaces).

Una vez configurada la identidad principal, el esquema de destino debe habilitarse para [!DNL Real-time Customer Profile].

![Habilitar para perfil](../images/tutorials/relationship/hotel-profile.png)

## Crear un grupo de campos de esquema de relación

>[!NOTE]
>
>Este paso solo es necesario si el esquema de origen no tiene un campo dedicado de tipo cadena que se vaya a utilizar como referencia al esquema de destino. Si este campo ya está definido en el esquema de origen, vaya al paso siguiente de [definición de un campo de relación](#relationship-field).

Para definir una relación entre dos esquemas, el esquema de origen debe tener un campo dedicado para utilizarlo como referencia del esquema de destino. Puede añadir este campo al esquema de origen creando un nuevo grupo de campos de esquema.

Comience por seleccionar **[!UICONTROL Agregar]** en el **[!UICONTROL Grupos de campo]** para obtener más información.

![](../images/tutorials/relationship/loyalty-add-field-group.png)

La variable [!UICONTROL Agregar grupo de campos] se abre. Desde aquí, seleccione **[!UICONTROL Crear nuevo grupo de campos]**. En los campos de texto que aparecen, introduzca un nombre para mostrar y una descripción para el nuevo grupo de campos. Select **[!UICONTROL Agregar grupos de campos]** cuando termine.

![](../images/tutorials/relationship/create-field-group.png)

El lienzo vuelve a aparecer con &quot;[!DNL Favorite Hotel]&quot; que aparece en el **[!UICONTROL Grupos de campo]** para obtener más información. Seleccione el nombre del grupo de campos y, a continuación, seleccione **[!UICONTROL Añadir campo]** junto al nivel raíz `Loyalty Members` campo .

![](../images/tutorials/relationship/loyalty-add-field.png)

Aparece un nuevo campo en el lienzo debajo del `_tenantId` espacio de nombres. En **[!UICONTROL Propiedades del campo]**, proporcione un nombre de campo y un nombre para mostrar para el campo y establezca su tipo en &quot;[!UICONTROL Cadena]&quot;.

![](../images/tutorials/relationship/relationship-field-details.png)

Cuando termine, seleccione **[!UICONTROL Aplicar]**.

![](../images/tutorials/relationship/relationship-field-apply.png)

El `favoriteHotel` aparece en el lienzo. Select **[!UICONTROL Guardar]** para finalizar los cambios en el esquema.

![](../images/tutorials/relationship/relationship-field-save.png)

## Definir un campo de relación para el esquema de origen {#relationship-field}

Una vez que el esquema de origen tiene un campo de referencia dedicado definido, puede designarlo como campo de relación.

>[!NOTE]
>
>Los pasos siguientes explican cómo definir un campo de relación utilizando los controles del carril derecho del lienzo. Si tiene acceso a Real-Time CDP B2B Edition, también puede definir una relación &quot;uno a uno&quot; mediante el [mismo cuadro de diálogo](./relationship-b2b.md#relationship-field) al igual que cuando se crean relaciones &quot;varios a uno&quot;.

Seleccione el `favoriteHotel` en el lienzo, desplácese hacia abajo por debajo **[!UICONTROL Propiedades del campo]** hasta que **[!UICONTROL Relación]** aparecerá la casilla de verificación. Seleccione la casilla de verificación para mostrar los parámetros necesarios para configurar un campo de relación.

![](../images/tutorials/relationship/relationship-checkbox.png)

Seleccione la lista desplegable para **[!UICONTROL Esquema de referencia]** y seleccione el esquema de destino para la relación (&quot;[!DNL Hotels]&quot; en este ejemplo). Si el esquema de destino está habilitado para [!DNL Profile], el **[!UICONTROL Área de nombres de identidad de referencia]** se establece automáticamente en el área de nombres de la identidad principal del esquema de destino. Si el esquema no tiene una identidad principal definida, debe seleccionar manualmente el área de nombres que desea utilizar en el menú desplegable. Select **[!UICONTROL Aplicar]** cuando termine.

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

La variable `favoriteHotel` ahora se resalta como una relación en el lienzo, mostrando el nombre y el área de nombres de la identidad de referencia del esquema de destino. Select **[!UICONTROL Guardar]** para guardar los cambios y completar el flujo de trabajo.

![](../images/tutorials/relationship/relationship-save.png)

## Pasos siguientes

Siguiendo este tutorial, se ha creado correctamente una relación &quot;uno a uno&quot; entre dos esquemas con la variable [!DNL Schema Editor]. Para ver los pasos sobre cómo definir relaciones mediante la API, consulte el tutorial sobre [definición de una relación mediante la API del Registro de Esquemas](relationship-api.md).
