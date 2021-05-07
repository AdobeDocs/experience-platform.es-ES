---
keywords: Experience Platform;inicio;temas populares;interfaz de usuario;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos;modelo de datos;editor de esquemas;editor de esquemas;esquema;esquemas;esquemas;crear;relación;referencia;referencia;
solution: Experience Platform
title: Definir una relación entre dos esquemas con el Editor de esquemas
description: Este documento proporciona un tutorial para definir una relación entre dos esquemas con el Editor de esquemas en la interfaz de usuario del Experience Platform.
topic-legacy: tutorial
type: Tutorial
exl-id: feed776b-bc8d-459b-9700-e5c9520788c0
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '921'
ht-degree: 1%

---

# Defina una relación entre dos esquemas con el [!DNL Schema Editor]

La capacidad de comprender las relaciones entre los clientes y sus interacciones con la marca a través de varios canales es una parte importante de Adobe Experience Platform. La definición de estas relaciones dentro de la estructura de los esquemas [!DNL Experience Data Model] (XDM) le permite obtener perspectivas complejas sobre los datos de sus clientes.

Aunque las relaciones de esquema se pueden inferir mediante el uso del esquema de unión y [!DNL Real-time Customer Profile], esto solo se aplica a esquemas que comparten la misma clase. Para establecer una relación entre dos esquemas pertenecientes a diferentes clases, se debe agregar un campo de relación dedicado a un esquema de origen que haga referencia a la identidad de un esquema de destino.

Este documento proporciona un tutorial para definir una relación entre dos esquemas con el Editor de esquemas en la interfaz de usuario [!DNL Experience Platform]. Para ver los pasos sobre la definición de relaciones de esquema mediante la API, consulte el tutorial sobre la [definición de una relación mediante la API del Registro de esquemas](relationship-api.md).

## Primeros pasos

Este tutorial requiere una comprensión práctica de [!DNL XDM System] y del Editor de esquemas en la interfaz de usuario [!DNL Experience Platform]. Antes de comenzar este tutorial, consulte la siguiente documentación:

* [Sistema XDM en Experience Platform](../home.md): Información general sobre XDM y su implementación en  [!DNL Experience Platform].
* [Aspectos básicos de la composición](../schema/composition.md) del esquema: Introducción de los componentes básicos de los esquemas XDM.
* [Cree un esquema con [!DNL Schema Editor]](create-schema-ui.md): Un tutorial que cubre los conceptos básicos del trabajo con  [!DNL Schema Editor].

## Definir un esquema de origen y destino

Se espera que ya haya creado los dos esquemas que se definirán en la relación. Con fines de demostración, este tutorial crea una relación entre los miembros del programa de fidelidad de una organización (definido en un esquema &quot;[!DNL Loyalty Members]&quot;) y su hotel favorito (definido en un esquema &quot;[!DNL Hotels]&quot;).

>[!IMPORTANT]
>
>Para establecer una relación, ambos esquemas deben tener identidades principales definidas y estar habilitados para [!DNL Real-time Customer Profile]. Consulte la sección sobre [habilitación de un esquema para su uso en Perfil](./create-schema-ui.md#profile) en el tutorial de creación de esquemas si necesita instrucciones sobre cómo configurar los esquemas en consecuencia.

Las relaciones de esquema se representan mediante un campo dedicado dentro de un **esquema de origen** que hace referencia a otro campo dentro de un **esquema de destino**. En los pasos siguientes, &quot;[!DNL Loyalty Members]&quot; será el esquema de origen, mientras que &quot;[!DNL Hotels]&quot; actuará como esquema de destino.

Con fines de referencia, las secciones siguientes describen la estructura de cada esquema utilizado en este tutorial antes de que se haya definido una relación.

### [!DNL Loyalty Members] esquema

El esquema de origen &quot;[!DNL Loyalty Members]&quot; se basa en la clase [!DNL XDM Individual Profile] y es el esquema que se construyó en el tutorial para [crear un esquema en la interfaz de usuario](create-schema-ui.md). Incluye un objeto `loyalty` en su espacio de nombres `_tenantId`, que incluye varios campos específicos de lealtad. Uno de estos campos, `loyaltyId`, sirve como identidad principal para el esquema en el espacio de nombres [!UICONTROL Email]. Como se ve en **[!UICONTROL Schema Properties]**, este esquema se ha habilitado para su uso en [!DNL Real-time Customer Profile].

![](../images/tutorials/relationship/loyalty-members.png)

### [!DNL Hotels] esquema

El esquema de destino &quot;[!DNL Hotels]&quot; se basa en una clase &quot;[!DNL Hotels]&quot; personalizada y contiene campos que describen un hotel. El campo `hotelId` sirve como identidad principal para el esquema en un espacio de nombres personalizado `hotelId`. Al igual que el esquema [!DNL Loyalty Members] , este esquema también se ha habilitado para [!DNL Real-time Customer Profile].

![](../images/tutorials/relationship/hotels.png)

## Crear un grupo de campos de esquema de relación

>[!NOTE]
>
>Este paso solo es necesario si el esquema de origen no tiene un campo dedicado de tipo cadena que se vaya a utilizar como referencia al esquema de destino. Si este campo ya está definido en el esquema de origen, vaya al siguiente paso de [definición de un campo de relación](#relationship-field).

Para definir una relación entre dos esquemas, el esquema de origen debe tener un campo dedicado para utilizarlo como referencia del esquema de destino. Puede añadir este campo al esquema de origen creando un nuevo grupo de campos de esquema.

Comience por seleccionar **[!UICONTROL Add]** en la sección **[!UICONTROL Field groups]**.

![](../images/tutorials/relationship/loyalty-add-field-group.png)

Aparece el cuadro de diálogo [!UICONTROL Add field group]. Desde aquí, seleccione **[!UICONTROL Create new field group]**. En los campos de texto que aparecen, introduzca un nombre para mostrar y una descripción para el nuevo grupo de campos. Seleccione **[!UICONTROL Add field groups]** cuando haya terminado.

![](../images/tutorials/relationship/create-field-group.png)

El lienzo vuelve a aparecer con &quot;[!DNL Favorite Hotel]&quot; en la sección **[!UICONTROL Field groups]**. Seleccione el nombre del grupo de campos y, a continuación, seleccione **[!UICONTROL Add field]** junto al campo de nivel raíz `Loyalty Members`.

![](../images/tutorials/relationship/loyalty-add-field.png)

Aparece un nuevo campo en el lienzo debajo del espacio de nombres `_tenantId`. En **[!UICONTROL Field properties]**, proporcione un nombre de campo y un nombre para mostrar para el campo y establezca su tipo en &quot;[!UICONTROL String]&quot;.

![](../images/tutorials/relationship/relationship-field-details.png)

Cuando termine, seleccione **[!UICONTROL Apply]**.

![](../images/tutorials/relationship/relationship-field-apply.png)

El campo `favoriteHotel` actualizado aparece en el lienzo. Seleccione **[!UICONTROL Save]** para finalizar los cambios en el esquema.

![](../images/tutorials/relationship/relationship-field-save.png)

## Definir un campo de relación para el esquema de origen {#relationship-field}

Una vez que el esquema de origen tiene un campo de referencia dedicado definido, puede designarlo como campo de relación.

Seleccione el campo `favoriteHotel` en el lienzo y, a continuación, desplácese hacia abajo en **[!UICONTROL Field properties]** hasta que aparezca la casilla **[!UICONTROL Relationship]**. Seleccione la casilla de verificación para mostrar los parámetros necesarios para configurar un campo de relación.

![](../images/tutorials/relationship/relationship-checkbox.png)

Seleccione el menú desplegable para **[!UICONTROL Reference schema]** y seleccione el esquema de destino para la relación (&quot;[!DNL Hotels]&quot; en este ejemplo). Si el esquema de destino está habilitado para [!DNL Profile], el campo **[!UICONTROL Reference identity namespace]** se establece automáticamente en el área de nombres de la identidad principal del esquema de destino. Si el esquema no tiene una identidad principal definida, debe seleccionar manualmente el área de nombres que desea utilizar en el menú desplegable. Seleccione **[!UICONTROL Apply]** cuando haya terminado.

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

El campo `favoriteHotel` ahora se resalta como una relación en el lienzo, mostrando el nombre y el área de nombres de la identidad de referencia del esquema de destino. Seleccione **[!UICONTROL Save]** para guardar los cambios y completar el flujo de trabajo.

![](../images/tutorials/relationship/relationship-save.png)

## Pasos siguientes

Siguiendo este tutorial, se ha creado correctamente una relación &quot;uno a uno&quot; entre dos esquemas con [!DNL Schema Editor]. Para ver los pasos sobre cómo definir relaciones con la API, consulte el tutorial sobre la [definición de una relación con la API del Registro de esquemas](relationship-api.md).
