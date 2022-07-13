---
title: Definir una relación entre dos esquemas en Real-time Customer Data Platform B2B Edition
description: Aprenda a definir una relación "varios a uno" entre dos esquemas en Real-time Customer Data Platform B2B Edition.
exl-id: 14032754-c7f5-46b6-90e6-c6e99af1efba
source-git-commit: a95e5cf02e993d6c761abd74c98c0967a89eb678
workflow-type: tm+mt
source-wordcount: '1401'
ht-degree: 0%

---

# Definir una relación &quot;varios a uno&quot; entre dos esquemas en Real-time Customer Data Platform B2B Edition

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_reference_schema"
>title="Esquema de referencia"
>abstract="Seleccione el esquema con el que desea establecer una relación. Según la clase del esquema, también puede tener relaciones existentes con otras entidades en el contexto B2B. Consulte la documentación para conocer cómo se relacionan las clases de esquema B2B entre sí."

Real-time Customer Data Platform B2B Edition proporciona varias clases de Experience Data Model (XDM) que capturan entidades de datos B2B fundamentales, incluidas [cuentas](../classes/b2b/business-account.md), [oportunidades](../classes/b2b/business-opportunity.md), [campañas](../classes/b2b/business-campaign.md), y más. Crear esquemas basados en estas clases y permitirles usarlos en [Perfil del cliente en tiempo real](../../profile/home.md), puede combinar datos de orígenes diferentes en una representación unificada denominada esquema de unión.

Sin embargo, los esquemas de unión solo pueden contener campos capturados por esquemas que comparten la misma clase. Aquí es donde entran en juego las relaciones de esquema. Al implementar relaciones en sus esquemas B2B, puede describir cómo se relacionan estas entidades comerciales entre sí y puede incluir atributos de múltiples clases en casos de uso de segmentación descendente.

El diagrama siguiente proporciona un ejemplo de cómo las diferentes clases B2B se pueden relacionar entre sí en una implementación básica:

![Relaciones de clase B2B](../images/tutorials/relationship-b2b/classes.png)

Este tutorial trata los pasos para definir una relación &quot;varios a uno&quot; entre dos esquemas en tiempo real CDP B2B Edition.

>[!NOTE]
>
>Si no utiliza Real-time Customer Data Platform B2B Edition o desea crear una relación uno a uno, consulte la guía de [creación de una relación uno a uno](./relationship-ui.md) en su lugar.
>
>Este tutorial se centra en cómo establecer manualmente relaciones entre esquemas B2B en la interfaz de usuario de Platform. Si obtiene datos de una conexión de origen B2B, puede utilizar una utilidad de generación automática para crear en su lugar los esquemas, identidades y relaciones necesarios. Consulte la documentación de fuentes sobre los esquemas y áreas de nombres B2B para obtener más información sobre [uso de la utilidad de generación automática](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md).

## Primeros pasos

Este tutorial requiere una comprensión práctica de [!DNL XDM System] y el Editor de esquemas en la [!DNL Experience Platform] IU. Antes de comenzar este tutorial, consulte la siguiente documentación:

* [Sistema XDM en Experience Platform](../home.md): Información general sobre XDM y su implementación en [!DNL Experience Platform].
* [Aspectos básicos de la composición del esquema](../schema/composition.md): Introducción de los componentes básicos de los esquemas XDM.
* [Cree un esquema utilizando la variable [!DNL Schema Editor]](create-schema-ui.md): Un tutorial que cubre los conceptos básicos de cómo crear y editar esquemas en la interfaz de usuario.

## Definir un esquema de origen y destino

Se espera que ya haya creado los dos esquemas que se definirán en la relación. Para fines de demostración, este tutorial crea una relación entre las oportunidades comerciales (definidas en un &quot;[!DNL Opportunities]&quot; esquema) y su cuenta comercial asociada (definida en un[!DNL Accounts]&quot; esquema).

Las relaciones de esquema se representan mediante un campo dedicado dentro de un **esquema de origen** que hace referencia al campo de identidad principal de un **esquema de destino**. En los pasos siguientes, &quot;[!DNL Opportunities]&quot; sirve como esquema de origen, mientras que &quot;[!DNL Accounts]&quot; actúa como esquema de destino.

### Explicación de las identidades en las relaciones B2B

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_identity_namespace"
>title="Área de nombres de identidad de referencia"
>abstract="El espacio de nombres (tipo) del campo de identidad principal del esquema de referencia. El esquema de referencia debe tener un campo de identidad principal establecido para participar en una relación. Consulte la documentación para obtener más información sobre las identidades en las relaciones B2B."

Para establecer una relación, el esquema de destino debe tener una identidad principal definida. Al configurar una identidad principal para una entidad B2B, tenga en cuenta que los ID de entidad basados en cadenas pueden superponerse si los recopila en diferentes sistemas o ubicaciones, lo que podría provocar conflictos de datos en Platform.

Para tener en cuenta esto, todas las clases B2B estándar contienen campos &quot;clave&quot; que se ajustan al [[!UICONTROL Fuente B2B] tipo de datos](../data-types/b2b-source.md). Este tipo de datos proporciona campos para un identificador de cadena para la entidad B2B junto con otra información contextual sobre el origen del identificador. Uno de estos campos, `sourceKey`, concatena los valores de los demás campos del tipo de datos para producir un identificador único total para la entidad. Este campo siempre debe utilizarse como identidad principal para esquemas de entidad B2B.

![Campo sourceKey](../images/tutorials/relationship-b2b/sourcekey.png)

>[!NOTE]
>
>When [configuración de un campo XDM como identidad](../ui/fields/identity.md), debe proporcionar un área de nombres de identidad para definir la identidad en. Puede ser un área de nombres estándar proporcionada por Adobe o un área de nombres personalizada definida por su organización. En la práctica, el área de nombres es simplemente una cadena contextual y se puede establecer en cualquier valor que desee, siempre que tenga sentido para la organización categorizar el tipo de identidad. Consulte la descripción general sobre [áreas de nombres de identidad](../../identity-service/namespaces.md) para obtener más información.

Con fines de referencia, las secciones siguientes describen la estructura de cada esquema utilizado en este tutorial antes de que se haya definido una relación. Tenga en cuenta dónde se han definido las identidades principales en la estructura de esquema y los espacios de nombres personalizados que utilizan.

### [!DNL Opportunities] esquema

El esquema de origen &quot;[!DNL Opportunities]&quot; se basa en la variable [!UICONTROL Oportunidad comercial XDM] Clase . Uno de los campos proporcionados por la clase , `opportunityKey`, sirve como identificador del esquema . Específicamente, la variable `sourceKey` en el campo `opportunityKey` se establece como la identidad principal del esquema en un espacio de nombres personalizado denominado [!DNL B2B Opportunity].

Como se ve en **[!UICONTROL Propiedades del esquema]**, este esquema se ha habilitado para utilizarse en [!DNL Real-time Customer Profile].

![Esquema de oportunidades](../images/tutorials/relationship-b2b/opportunities.png)

### [!DNL Accounts] esquema

El esquema de destino &quot;[!DNL Accounts]&quot; se basa en la variable [!UICONTROL Cuenta XDM] Clase . El nivel raíz `accountKey` El campo contiene la variable `sourceKey` que actúa como su identidad principal bajo un espacio de nombres personalizado llamado [!DNL B2B Account]. Este esquema también se ha habilitado para su uso en Perfil.

![Esquema de cuentas](../images/tutorials/relationship-b2b/accounts.png)

## Definir un campo de relación para el esquema de origen {#relationship-field}

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_relationship_name_current"
>title="Nombre de relación del esquema actual"
>abstract="Etiqueta que describe la relación entre el esquema actual y el esquema de referencia (por ejemplo, &quot;Cuenta relacionada&quot;). Esta etiqueta se utiliza en Perfil y Segmentación para dar contexto a los datos de entidades B2B relacionadas. Consulte la documentación para obtener más información sobre la creación de relaciones de esquema B2B."

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_relationship_name_reference"
>title="Nombre de relación del esquema de referencia"
>abstract="Etiqueta que describe la relación entre el esquema de referencia y el esquema actual (por ejemplo, &quot;Oportunidades relacionadas&quot;). Esta etiqueta se utiliza en Perfil y Segmentación para dar contexto a los datos de entidades B2B relacionadas. Consulte la documentación para obtener más información sobre la creación de relaciones de esquema B2B."

Para definir una relación entre dos esquemas, el esquema de origen debe tener un campo dedicado que haga referencia a la identidad principal del esquema de destino. Las clases B2B estándar incluyen campos clave de origen específicos para entidades comerciales relacionadas de forma habitual. Por ejemplo, la variable [!UICONTROL Oportunidad comercial XDM] la clase contiene campos de clave de origen para una cuenta relacionada (`accountKey`) y una campaña relacionada (`campaignKey`). Sin embargo, también puede agregar otras [!UICONTROL Fuente B2B] campos al esquema utilizando grupos de campos personalizados si necesita más de los componentes predeterminados.

>[!NOTE]
>
>Actualmente, solo se pueden definir relaciones &quot;varios a uno&quot; y &quot;uno a uno&quot; de un esquema de origen a un esquema de destino. Para las relaciones uno a varios, debe definir el campo de relación en el esquema que representa el &quot;varios&quot;.

Para establecer un campo de relación, seleccione el icono de flecha (![Icono de flecha](../images/tutorials/relationship-b2b/arrow.png)) junto al campo en cuestión dentro del lienzo. En el caso del [!DNL Opportunities] esquema, este es el `accountKey.sourceKey` , ya que el objetivo es establecer una relación &quot;varios a uno&quot; con una cuenta.

![Botón Relación](../images/tutorials/relationship-b2b/relationship-button.png)

Aparece un cuadro de diálogo que le permite especificar los detalles de la relación. El tipo de relación se establece automáticamente como **[!UICONTROL Varios a uno]**.

![Diálogo de relaciones](../images/tutorials/relationship-b2b/relationship-dialog.png)

En **[!UICONTROL Esquema de referencia]**, utilice la barra de búsqueda para encontrar el nombre del esquema de destino. Cuando resalte el nombre del esquema de destino, la variable **[!UICONTROL Espacio de nombres de identidad de referencia]** se actualiza automáticamente al espacio de nombres de la identidad principal del esquema.

![Esquema de referencia](../images/tutorials/relationship-b2b/reference-schema.png)

En **[!UICONTROL Nombre de relación del esquema actual]** y **[!UICONTROL Nombre de relación desde esquema de referencia]**, proporcione nombres descriptivos para la relación en el contexto de los esquemas de origen y destino, respectivamente. Cuando termine, seleccione **[!UICONTROL Guardar]** para aplicar los cambios y guardar el esquema.

![Nombre de relación](../images/tutorials/relationship-b2b/relationship-name.png)

El lienzo vuelve a aparecer y el campo de relación ahora está marcado con el nombre descriptivo que ha proporcionado anteriormente. El nombre de la relación también se muestra bajo el carril izquierdo para facilitar la referencia.

![Relación aplicada](../images/tutorials/relationship-b2b/relationship-applied.png)

Si ve la estructura del esquema de destino, el marcador de relación aparece junto al campo de identidad principal del esquema y en el carril izquierdo.

![Marcador de relación del esquema de destino](../images/tutorials/relationship-b2b/destination-relationship.png)

## Pasos siguientes

Siguiendo este tutorial, se ha creado correctamente una relación &quot;varios a uno&quot; entre dos esquemas con la variable [!DNL Schema Editor]. Una vez introducidos los datos mediante conjuntos de datos basados en estos esquemas y que se hayan activado los datos en el almacén de datos de perfil, puede utilizar atributos de ambos esquemas para casos de uso de segmentación de varias clases. Consulte la documentación sobre CDP B2B Edition en tiempo real para obtener más información.
