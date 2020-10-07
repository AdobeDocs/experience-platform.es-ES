---
keywords: Experience Platform;home;popular topics;ui;UI;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema editor;Schema Editor;schema;Schema;schemas;Schemas;create;relationship;Relationship;reference;Reference;
solution: Experience Platform
title: Definir una relación entre dos esquemas mediante el Editor de Esquemas de Esquema
description: Este documento proporciona un tutorial para definir una relación entre dos esquemas mediante el Editor de Esquemas en la interfaz de usuario del Experience Platform.
topic: tutorial
type: Tutorials
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 0%

---


# Defina una relación entre dos esquemas mediante la variable [!DNL Schema Editor]

La capacidad de comprender las relaciones entre sus clientes y sus interacciones con su marca en diversos canales es una parte importante de Adobe Experience Platform. La definición de estas relaciones dentro de la estructura de sus esquemas [!DNL Experience Data Model] (XDM) le permite obtener perspectivas complejas sobre los datos de sus clientes.

Aunque las relaciones de esquema pueden inferirse mediante el uso del esquema de unión y [!DNL Real-time Customer Profile], esto sólo se aplica a esquemas que comparten la misma clase. Para establecer una relación entre dos esquemas pertenecientes a diferentes clases, se debe agregar un campo de relación dedicado a un esquema de origen, que haga referencia a la identidad de un esquema de destino.

Este documento proporciona un tutorial para definir una relación entre dos esquemas mediante el Editor de Esquemas en la interfaz de usuario [!DNL Experience Platform] . Para ver los pasos sobre la definición de relaciones de esquema mediante la API, consulte el tutorial sobre la [definición de una relación mediante la API](relationship-api.md)del Registro de Esquema.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de [!DNL XDM System] y del Editor de Esquemas en la [!DNL Experience Platform] interfaz de usuario. Antes de comenzar este tutorial, consulte la siguiente documentación:

* [Sistema XDM en Experience Platform](../home.md): Información general sobre XDM y su implementación en [!DNL Experience Platform].
* [Conceptos básicos de la composición](../schema/composition.md)de esquemas: Introducción de los componentes básicos de los esquemas XDM.
* [Cree un esquema con los [!DNL Schema Editor]](create-schema-ui.md)siguientes elementos: Un tutorial que cubre los conceptos básicos del trabajo con el [!DNL Schema Editor].

## Definir un esquema de origen y destino

Se espera que ya haya creado los dos esquemas que se definirán en la relación. Para fines de demostración, este tutorial crea una relación entre los miembros del programa de lealtad de una organización (definido en un esquema &quot;[!DNL Loyalty Members]&quot;) y su hotel favorito (definido en un esquema &quot;[!DNL Hotels]&quot;).

>[!IMPORTANT]
>
>Para establecer una relación, ambos esquemas deben tener identidades primarias definidas y estar habilitados para [!DNL Real-time Customer Profile]. Consulte la sección sobre la [activación de un esquema para su uso en Perfil](./create-schema-ui.md#profile) en el tutorial de creación de esquema si necesita instrucciones sobre cómo configurar los esquemas en consecuencia.

Las relaciones de esquema están representadas por un campo dedicado dentro de un esquema **de** origen que hace referencia a otro campo dentro de un esquema **de** destino. En los pasos siguientes, &quot;[!DNL Loyalty Members]&quot; será el esquema de origen, mientras que &quot;[!DNL Hotels]&quot; actuará como el esquema de destino.

Con fines de referencia, las siguientes secciones describen la estructura de cada esquema utilizado en este tutorial antes de definir una relación.

### [!DNL Loyalty Members] esquema

El esquema de origen &quot;[!DNL Loyalty Members]&quot; se basa en la [!DNL XDM Individual Profile] clase y es el esquema que se creó en el tutorial para [crear un esquema en la interfaz de usuario](create-schema-ui.md). Incluye un `loyalty` objeto bajo su `_tenantId` Área de nombres, que incluye varios campos específicos de lealtad. Uno de estos campos, `loyaltyId`, sirve como identidad principal para el esquema bajo la Área de nombres [!UICONTROL Correo electrónico] . Como se muestra en Propiedades **[!UICONTROL de]** Esquema, este esquema se ha habilitado para su uso en [!DNL Real-time Customer Profile].

![](../images/tutorials/relationship/loyalty-members.png)

### [!DNL Hotels] esquema

El esquema de destino &quot;[!DNL Hotels]&quot; se basa en una clase &quot;[!DNL Hotels]&quot; personalizada y contiene campos que describen un hotel. El `hotelId` campo sirve como identidad principal para el esquema en una `hotelId` Área de nombres personalizada. Al igual que el [!DNL Loyalty Members] esquema, este esquema también se ha habilitado para [!DNL Real-time Customer Profile].

![](../images/tutorials/relationship/hotels.png)

## Crear una mezcla de relación

>[!NOTE]
>
>Este paso solo es necesario si el esquema de origen no tiene un campo de tipo de cadena dedicado que se pueda utilizar como referencia al esquema de destino. Si este campo ya está definido en el esquema de origen, vaya al siguiente paso para [definir un campo](#relationship-field)de relación.

Para definir una relación entre dos esquemas, el esquema de origen debe tener un campo específico para utilizarlo como referencia al esquema de destino. Puede agregar este campo al esquema de origen creando una nueva mezcla.

Para inicio, seleccione **[!UICONTROL Añadir]** en la sección **[!UICONTROL Mezclas]** .

![](../images/tutorials/relationship/loyalty-add-mixin.png)

Aparecerá el cuadro de diálogo [!UICONTROL Añadir mezcla] . Desde aquí, seleccione **[!UICONTROL Crear nueva mezcla]**. En los campos de texto que aparecen, introduzca un nombre para mostrar y una descripción para la nueva combinación. Seleccione **[!UICONTROL Añadir mezcla]** cuando termine.

<img src="../images/tutorials/relationship/loyalty-create-new-mixin.png" width="750"><br>

El lienzo vuelve a aparecer con &quot;[!DNL Favorite Hotel]&quot; en la sección **[!UICONTROL Mixins]** . Seleccione el nombre de la mezcla y, a continuación, seleccione **[!UICONTROL Añadir campo]** junto al `Loyalty Members` campo de nivel raíz.

![](../images/tutorials/relationship/loyalty-add-field.png)

Aparece un nuevo campo en el lienzo debajo de la `_tenantId` Área de nombres. En Propiedades **** de campo, proporcione un nombre de campo y un nombre para mostrar para el campo y defina su tipo en &quot;[!UICONTROL String]&quot;.

![](../images/tutorials/relationship/relationship-field-details.png)

Cuando termine, seleccione **[!UICONTROL Aplicar]**.

![](../images/tutorials/relationship/relationship-field-apply.png)

El `favoriteHotel` campo actualizado aparece en el lienzo. Seleccione **[!UICONTROL Guardar]** para finalizar los cambios en el esquema.

![](../images/tutorials/relationship/relationship-field-save.png)

## Definir un campo de relación para el esquema de origen {#relationship-field}

Una vez definido el esquema de origen, puede designarlo como un campo de relación.

Seleccione el `favoriteHotel` campo en el lienzo y, a continuación, desplácese hacia abajo en las propiedades **** Campo hasta que aparezca la casilla de verificación **[!UICONTROL Relación]** . Seleccione la casilla de verificación para mostrar los parámetros necesarios para configurar un campo de relación.

![](../images/tutorials/relationship/relationship-checkbox.png)

Seleccione la lista desplegable para el esquema **[!UICONTROL de]** referencia y seleccione el esquema de destino para la relación (&quot;[!DNL Hotels]&quot; en este ejemplo). Si el esquema de destino está habilitado para [!DNL Profile], el campo Área de nombres **[!UICONTROL de identidad de]** referencia se establece automáticamente en la Área de nombres de la identidad principal del esquema de destino. Si el esquema no tiene definida una identidad principal, debe seleccionar manualmente la Área de nombres que va a utilizar en el menú desplegable. Seleccione **[!UICONTROL Aplicar]** cuando termine.

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

El `favoriteHotel` campo ahora se resalta como una relación en el lienzo, mostrando el nombre y la Área de nombres de identidad de referencia del esquema de destino. Seleccione **[!UICONTROL Guardar]** para guardar los cambios y completar el flujo de trabajo.

![](../images/tutorials/relationship/relationship-save.png)

## Pasos siguientes

Siguiendo este tutorial, ha creado correctamente una relación uno a uno entre dos esquemas mediante el uso del [!DNL Schema Editor]. Para ver los pasos sobre cómo definir relaciones mediante la API, consulte el tutorial sobre la [definición de una relación mediante la API](relationship-api.md)del Registro de Esquema.