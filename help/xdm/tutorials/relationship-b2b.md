---
title: Definir una relación entre dos esquemas en Real-time Customer Data Platform B2B Edition
description: Aprenda a definir una relación varios a uno entre dos esquemas en Adobe Real-time Customer Data Platform B2B Edition.
exl-id: 14032754-c7f5-46b6-90e6-c6e99af1efba
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1363'
ht-degree: 15%

---

# Defina una relación de varios a uno entre dos esquemas en Real-time Customer Data Platform B2B Edition {#relationship-b2b}

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_reference_schema"
>title="Esquema de referencia"
>abstract="Seleccione el esquema con el que desea establecer una relación. Según la clase del esquema, también puede tener relaciones existentes con otras entidades en el contexto B2B. Consulte la documentación para obtener más información acerca de cómo se relacionan las clases de esquema B2B entre sí."

Adobe Real-time Customer Data Platform B2B Edition proporciona varias clases de modelo de datos de experiencia (XDM) que capturan entidades de datos B2B fundamentales, como [cuentas](../classes/b2b/business-account.md), [oportunidades](../classes/b2b/business-opportunity.md), [campañas](../classes/b2b/business-campaign.md) y más. Si crea esquemas basados en estas clases y los habilita para su uso en [Perfil del cliente en tiempo real](../../profile/home.md), podrá combinar datos de distintas fuentes en una representación unificada denominada esquema de unión.

Sin embargo, los esquemas de unión solo pueden contener campos capturados por esquemas que comparten la misma clase. Aquí es donde entran en juego las relaciones de esquema. Al implementar relaciones en los esquemas B2B, puede describir cómo se relacionan entre sí estas entidades comerciales y puede incluir atributos de varias clases en casos de uso de segmentación descendente.

El diagrama siguiente proporciona un ejemplo de cómo las diferentes clases B2B pueden relacionarse entre sí en una implementación básica:

![relaciones de clase B2B](../images/tutorials/relationship-b2b/classes.png)

Este tutorial trata los pasos para definir una relación varios a uno entre dos esquemas en Real-Time CDP B2B Edition.

>[!NOTE]
>
>Si no usa Real-time Customer Data Platform B2B Edition o desea crear una relación uno a uno, consulte la guía sobre [creación de una relación uno a uno](./relationship-ui.md) en su lugar.
>
>Este tutorial se centra en cómo establecer manualmente relaciones entre esquemas B2B en la IU de Platform. Si va a traer datos desde una conexión de origen B2B, puede utilizar una utilidad de generación automática para crear los esquemas, identidades y relaciones necesarios en su lugar. Consulte la documentación de fuentes sobre áreas de nombres y esquemas B2B para obtener más información sobre [el uso de la utilidad de generación automática](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md).

## Introducción

Este tutorial requiere una comprensión práctica de [!DNL XDM System] y del Editor de esquemas en la interfaz de usuario de [!DNL Experience Platform]. Antes de comenzar este tutorial, revise la siguiente documentación:

* [Sistema XDM en Experience Platform](../home.md): Información general sobre XDM y su implementación en [!DNL Experience Platform].
* [Conceptos básicos de la composición de esquemas](../schema/composition.md): introducción a los componentes básicos de los esquemas XDM.
* [Crear un esquema con [!DNL Schema Editor]](create-schema-ui.md): Un tutorial que cubre los conceptos básicos de cómo crear y editar esquemas en la interfaz de usuario.

## Definir un esquema de origen y de referencia

Se espera que ya haya creado los dos esquemas que se definirán en la relación. Para fines de demostración, este tutorial crea una relación entre oportunidades comerciales (definidas en un esquema &quot;[!DNL Opportunities]&quot;) y su cuenta comercial asociada (definida en un esquema &quot;[!DNL Accounts]&quot;).

Las relaciones de esquema están representadas por un campo dedicado dentro de un **esquema de origen** que hace referencia al campo de identidad principal de un **esquema de referencia**. En los pasos siguientes, &quot;[!DNL Opportunities]&quot; sirve como esquema de origen, mientras que &quot;[!DNL Accounts]&quot; actúa como esquema de referencia.

### Explicación de las identidades en las relaciones B2B

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_identity_namespace"
>title="Área de nombres de identidad de referencia"
>abstract="El área de nombres (tipo) del campo de identidad principal del esquema de referencia. El esquema de referencia debe tener un campo de identidad principal establecido para participar en una relación. Consulte la documentación para obtener más información sobre las identidades en las relaciones B2B."

Para establecer una relación, el esquema de referencia debe tener una identidad principal definida. Al establecer una identidad principal para una entidad B2B, tenga en cuenta que los ID de entidad basados en cadenas pueden superponerse si los recopila en diferentes sistemas o ubicaciones, lo que podría provocar conflictos de datos en Platform.

Para tener en cuenta esto, todas las clases B2B estándar contienen campos &quot;clave&quot; que se ajustan al tipo de datos [[!UICONTROL B2B Source]](../data-types/b2b-source.md). Este tipo de datos proporciona campos para un identificador de cadena para la entidad B2B junto con otra información contextual sobre el origen del identificador. Uno de estos campos, `sourceKey`, concatena los valores de los demás campos en el tipo de datos para producir un identificador totalmente único para la entidad. Este campo siempre debe utilizarse como identidad principal para los esquemas de entidad B2B.

![campo sourceKey](../images/tutorials/relationship-b2b/sourcekey.png)

>[!NOTE]
>
>Al [establecer un campo XDM como identidad](../ui/fields/identity.md), debe proporcionar un área de nombres de identidad para definir la identidad en. Puede ser un área de nombres estándar proporcionada por Adobe o un área de nombres personalizada definida por su organización. En la práctica, el área de nombres es simplemente una cadena contextual y se puede establecer en cualquier valor que desee, siempre que tenga sentido para su organización categorizar el tipo de identidad. Consulte la descripción general de [áreas de nombres de identidad](../../identity-service/features/namespaces.md) para obtener más información.

Como referencia, las secciones siguientes describen la estructura de cada esquema utilizado en este tutorial antes de definir una relación. Tome nota de dónde se han definido las identidades principales en la estructura de esquema y las áreas de nombres personalizadas que utilizan.

### Esquema [!DNL Opportunities]

El esquema de origen &quot;[!DNL Opportunities]&quot; se basa en la clase [!UICONTROL XDM Business Opportunity]. Uno de los campos proporcionados por la clase `opportunityKey` sirve como identificador del esquema. En concreto, el campo `sourceKey` del objeto `opportunityKey` se establece como identidad principal del esquema en un área de nombres personalizada denominada [!DNL B2B Opportunity].

Como se ve en **[!UICONTROL Propiedades del esquema]**, este esquema se ha habilitado para su uso en [!DNL Real-Time Customer Profile].

![Esquema de oportunidades](../images/tutorials/relationship-b2b/opportunities.png)

### Esquema [!DNL Accounts]

El esquema de referencia &quot;[!DNL Accounts]&quot; se basa en la clase [!UICONTROL XDM Account]. El campo de nivel raíz `accountKey` contiene `sourceKey` que actúa como su identidad principal bajo un área de nombres personalizada denominada [!DNL B2B Account]. Este esquema también se ha habilitado para su uso en el perfil.

![Esquema de cuentas](../images/tutorials/relationship-b2b/accounts.png)

## Definición de un campo de relación para el esquema de origen {#relationship-field}

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_relationship_name_current"
>title="Nombre de relación del esquema actual"
>abstract="Etiqueta que describe la relación entre el esquema actual y el esquema de referencia (por ejemplo, “Cuenta relacionada”). Esta etiqueta se utiliza en Perfil y Segmentación para dar contexto a los datos de entidades B2B relacionadas. Consulte la documentación para obtener más información sobre la creación de relaciones de esquemas B2B."

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_relationship_name_reference"
>title="Nombre de relación del esquema de referencia"
>abstract="Etiqueta que describe la relación entre el esquema de referencia y el esquema actual (por ejemplo, “Oportunidades relacionadas”). Esta etiqueta se utiliza en Perfil y Segmentación para dar contexto a los datos de entidades B2B relacionadas. Consulte la documentación para obtener más información sobre la creación de relaciones de esquemas B2B."

Para definir una relación entre dos esquemas, el esquema de origen debe tener un campo dedicado que indique la identidad principal del esquema de referencia. Las clases B2B estándar incluyen campos de clave de origen dedicados para entidades comerciales comúnmente relacionadas. Por ejemplo, la clase [!UICONTROL XDM Business Opportunity] contiene campos de clave de origen para una cuenta relacionada (`accountKey`) y una campaña relacionada (`campaignKey`). Sin embargo, también puede agregar otros campos de [!UICONTROL B2B Source] al esquema mediante grupos de campos personalizados si necesita más que los componentes predeterminados.

>[!NOTE]
>
>Actualmente, solo se pueden definir relaciones varios a uno y uno a uno desde un esquema de origen a un esquema de referencia. Para las relaciones uno a varios, debe definir el campo de relación en el esquema que representa a &quot;varios&quot;.

Para establecer un campo de relación, seleccione el icono de flecha (![Icono de flecha](../images/tutorials/relationship-b2b/arrow.png)) junto al campo en cuestión en el lienzo. En el caso del esquema [!DNL Opportunities], este es el campo `accountKey.sourceKey`, ya que el objetivo es establecer una relación de varios a uno con una cuenta.

![Botón de relación](../images/tutorials/relationship-b2b/relationship-button.png)

Aparece un cuadro de diálogo que le permite especificar los detalles de la relación. El tipo de relación se establece automáticamente en **[!UICONTROL Varios a uno]**.

![Diálogo de relación](../images/tutorials/relationship-b2b/relationship-dialog.png)

En **[!UICONTROL Esquema de referencia]**, utilice la barra de búsqueda para encontrar el nombre del esquema de referencia. Cuando resalta el nombre del esquema de referencia, el campo **[!UICONTROL Área de nombres de identidad de referencia]** se actualiza automáticamente al área de nombres de la identidad principal del esquema.

![Esquema de referencia](../images/tutorials/relationship-b2b/reference-schema.png)

En **[!UICONTROL Nombre de relación del esquema actual]** y **[!UICONTROL Nombre de relación del esquema de referencia]**, proporcione nombres descriptivos para la relación en el contexto de los esquemas de origen y referencia, respectivamente. Cuando termine, seleccione **[!UICONTROL Guardar]** para aplicar los cambios y guardar el esquema.

![Nombre de relación](../images/tutorials/relationship-b2b/relationship-name.png)

El lienzo vuelve a aparecer y el campo de relación ahora está marcado con el nombre descriptivo proporcionado anteriormente. El nombre de la relación también se enumera bajo el carril izquierdo para facilitar la referencia.

![Relación Aplicada](../images/tutorials/relationship-b2b/relationship-applied.png)

Si se ve la estructura del esquema de referencia, el marcador de relación aparece junto al campo de identidad principal del esquema y en el carril izquierdo.

![Marcador de relación de esquema de destino](../images/tutorials/relationship-b2b/destination-relationship.png)

## Pasos siguientes

Al seguir este tutorial, ha creado correctamente una relación de varios a uno entre dos esquemas con el [!DNL Schema Editor]. Una vez que los datos se han introducido utilizando conjuntos de datos basados en estos esquemas y que dichos datos se han activado en el almacén de datos de perfil, puede utilizar atributos de ambos esquemas para [casos de uso de segmentación de varias clases](../../rtcdp/segmentation/b2b.md).
