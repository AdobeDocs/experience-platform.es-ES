---
keywords: Experience Platform;inicio;temas populares;control de acceso;control de acceso basado en atributos;
title: Guía completa de control de acceso basado en atributos
description: Este documento proporciona una guía completa sobre el control de acceso basado en atributos en Adobe Experience Platform
role: Developer
exl-id: 7e363adc-628c-4a66-a3bd-b5b898292394
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '1714'
ht-degree: 17%

---

# Guía completa de control de acceso basado en atributos

Utilice el control de acceso basado en atributos en Adobe Experience Platform para ofrecerse a usted y a otros clientes conscientes de la privacidad de varias marcas una mayor flexibilidad para administrar el acceso de los usuarios. El acceso a objetos individuales, como campos de esquema y segmentos, se puede conceder con directivas basadas en los atributos y la función del objeto. Esta función le permite conceder o revocar el acceso a objetos individuales para usuarios de Platform específicos de su organización.

Esta funcionalidad le permite categorizar campos de esquema, segmentos, etc. con etiquetas que definen ámbitos organizativos o de uso de datos. Puede aplicar estas mismas etiquetas a recorridos, ofertas y otros objetos en Adobe Journey Optimizer. Al mismo tiempo, los administradores pueden definir políticas de acceso relacionadas con los campos de esquema del Modelo de datos de experiencia (XDM) y administrar mejor qué usuarios o grupos (usuarios internos, externos o de terceros) pueden acceder a esos campos.

>[!NOTE]
>
>Este documento se centra en el caso de uso de las políticas de control de acceso. Si intenta configurar directivas que gobiernen el **use** de datos en lugar de los usuarios de Platform que tienen acceso a ellos, consulte la guía completa sobre [gobernanza de datos](../../data-governance/e2e.md) en su lugar.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../xdm/home.md): El marco estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
   * [Conceptos básicos de composición de esquemas](../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [Servicio de segmentación de Adobe Experience Platform](../../segmentation/home.md): el motor de segmentación dentro de [!DNL Platform] se utiliza para crear segmentos de audiencia a partir de los perfiles de clientes en función de los comportamientos y atributos de los clientes.

### Resumen del caso de uso

Pasará por un flujo de trabajo de control de acceso basado en atributos de ejemplo en el que creará y asignará funciones, etiquetas y directivas para configurar si los usuarios pueden acceder o no a recursos específicos de su organización. Esta guía utiliza un ejemplo de restricción del acceso a datos confidenciales para mostrar el flujo de trabajo. Este caso de uso se describe a continuación:

Es un proveedor de atención médica y desea configurar el acceso a los recursos de su organización.

* Su equipo de marketing interno debe poder acceder a **[!UICONTROL PHI/ Datos de salud regulados]** datos.
* Su agencia externa no debería poder acceder a **[!UICONTROL PHI/ Datos de salud regulados]** datos.

Para ello, debe configurar las funciones, los recursos y las directivas.

Lo hará:

* [Etiquetado de las funciones de los usuarios](#label-roles): utilice el ejemplo de un proveedor de atención médica (ACME Business Group) cuyo grupo de marketing trabaja con agencias externas.
* [Etiquetado de recursos (campos y segmentos de esquema)](#label-resources): Asigne el **[!UICONTROL PHI/ Datos de salud regulados]** etiqueta para esquemas de recursos y segmentos.
* 
   * [Active la directiva que los vinculará:](#policy): habilite la directiva predeterminada para evitar el acceso a los campos y segmentos de esquema conectando las etiquetas de los recursos a las etiquetas de la función. Los usuarios con etiquetas coincidentes recibirán acceso al campo de esquema y al segmento en todas las zonas protegidas.

## Permisos

[!UICONTROL Permisos] es el área de Experience Cloud donde los administradores pueden definir roles de usuario y directivas para administrar permisos para funciones y objetos dentro de una aplicación de producto.

Pasante [!UICONTROL Permisos]Además, puede crear y administrar funciones y asignar los permisos de recursos deseados para estas funciones. [!UICONTROL Permisos] también le permite administrar las etiquetas, los entornos limitados y los usuarios asociados a una función específica.

Póngase en contacto con el administrador del sistema para obtener acceso si no tiene privilegios de administrador.

Una vez que tenga privilegios de administrador, vaya a [Adobe Experience Cloud](https://experience.adobe.com/) e inicie sesión con sus credenciales de Adobe. Una vez que haya iniciado sesión, la **[!UICONTROL Información general]** para su organización para la que tiene privilegios de administrador. Esta página muestra los productos a los que está suscrita su organización, junto con otros controles para agregar usuarios y administradores a la organización. Seleccionar **[!UICONTROL Permisos]** para abrir el espacio de trabajo de la integración de Platform.

![Imagen que muestra el producto Permisos seleccionado en Adobe Experience Cloud](../images/flac-ui/flac-select-product.png)

Aparece el área de trabajo Permisos para la IU de Platform, que se abre en la **[!UICONTROL Funciones]** página.

## Aplicar etiquetas a una función {#label-roles}

>[!CONTEXTUALHELP]
>id="platform_permissions_labels_about"
>title="¿Qué son las etiquetas?"
>abstract="Las etiquetas permiten clasificar los conjuntos de datos y campos según las directivas de uso que se aplican a esos datos. Platform proporciona varias etiquetas de uso de datos “principales” definidas por Adobe, que abarcan una amplia variedad de restricciones comunes aplicables a la gobernanza de datos. Por ejemplo, las etiquetas “S” confidenciales, como RHD (Datos protegidos de salud), permiten clasificar los datos que hacen referencia a la información confidencial sobre salud (PHI). También puede definir sus propias etiquetas personalizadas para que se adapten a las necesidades de su organización."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html?lang=es#understanding-data-usage-labels" text="Información general sobre las etiquetas de uso de datos"

>[!CONTEXTUALHELP]
>id="platform_permissions_labels_about_create"
>title="Crear nueva etiqueta"
>abstract="Puede crear sus propias etiquetas personalizadas para adaptarlas a las necesidades de su organización. Las etiquetas personalizadas se pueden usar para aplicar a los datos configuraciones de control de acceso y de gobernanza de datos."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html?lang=es#manage-labels" text="Administrar etiquetas personalizadas"

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_about"
>title="¿Qué son las funciones?"
>abstract="Las funciones son formas de clasificar los tipos de usuarios que interactúan con la instancia de Platform y que son componentes básicos de las directivas de control de acceso. Una función tiene un conjunto determinado de permisos y a los miembros de su organización se les puede asignar una o más funciones, según el ámbito de vista o acceso de escritura que necesiten."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/roles.html?lang=es" text="Administrar funciones"

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_about_create"
>title="Crear nueva función"
>abstract="Puede crear una nueva función para clasificar mejor a los usuarios que acceden a su instancia de Platform. Por ejemplo, puede crear una función para un equipo de marketing interno y aplicar la etiqueta RHD a esa función, lo que permite que su equipo de marketing interno acceda a la información confidencial sobre salud (PHI). Alternativamente, también puede crear una función para una agencia externa y denegar el acceso de esa función a los datos de PHI al no aplicar la etiqueta RHD a esa función."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/roles.html?lang=es#create-a-new-role" text="Crear una nueva función"

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_details"
>title="Información general sobre la función"
>abstract="El cuadro de diálogo de información general sobre la función muestra los recursos y las zonas protegidas a los que puede acceder una función determinada."

Las funciones son formas de categorizar los tipos de usuarios que interactúan con la instancia de Platform y son componentes básicos de las directivas de control de acceso. Una función tiene un conjunto determinado de permisos y los miembros de la organización pueden asignarse a una o varias funciones, según el ámbito de acceso que necesiten.

Para empezar, seleccione **[!UICONTROL Grupo empresarial ACME]** desde el desde el **[!UICONTROL Funciones]** página.

![Imagen que muestra el rol de negocio ACME seleccionado en roles](../images/abac-end-to-end-user-guide/abac-select-role.png)

A continuación, seleccione **[!UICONTROL Etiquetas]** y luego seleccione **[!UICONTROL Añadir etiquetas]**.

![Imagen que muestra las etiquetas de adición seleccionadas en la pestaña Etiquetas](../images/abac-end-to-end-user-guide/abac-select-add-labels.png)

Aparecerá una lista de todas las etiquetas de su organización. Seleccionar **[!UICONTROL RHD]** para añadir la etiqueta para **[!UICONTROL PHI/Datos de salud regulados]**. Espere unos momentos para que aparezca una marca de verificación azul junto a la etiqueta y, a continuación, seleccione **[!UICONTROL Guardar]**.

![Imagen que muestra la etiqueta RHD seleccionada y guardada](../images/abac-end-to-end-user-guide/abac-select-role-label.png)

>[!NOTE]
>
>Al agregar un grupo de organización a una función, todos los usuarios de ese grupo se agregarán a la función. Cualquier cambio en el grupo de organización (usuarios eliminados o añadidos) se actualizará automáticamente dentro de la función.

## Aplicar etiquetas a campos de esquema {#label-resources}

Ahora que ha configurado una función de usuario con la variable [!UICONTROL RHD] , el siguiente paso es agregar la misma etiqueta a los recursos que desea controlar para ese rol.

Seleccionar **[!UICONTROL Esquemas]** en el panel de navegación izquierdo y seleccione **[!UICONTROL ACME Healthcare]** de la lista de esquemas que aparecen.

![Imagen que muestra el esquema de ACME Healthcare seleccionado de la pestaña Esquemas](../images/abac-end-to-end-user-guide/abac-select-schema.png)

A continuación, seleccione **[!UICONTROL Etiquetas]** para ver una lista que muestre los campos asociados al esquema. Desde aquí, puede asignar etiquetas a uno o varios campos a la vez. Seleccione el **[!UICONTROL Glucosa en Sangre]** y **[!UICONTROL NivelDeInsulina]** y, a continuación, seleccione **[!UICONTROL Aplicación de etiquetas de acceso y de gobernanza de datos]**.

![Imagen que muestra los niveles de glucosa e insulina en sangre que se están seleccionando y se aplican las etiquetas de acceso y de control de datos que se están seleccionando](../images/abac-end-to-end-user-guide/abac-select-schema-labels-tab.png)

El **[!UICONTROL Editar etiquetas]** aparece un cuadro de diálogo que le permite elegir las etiquetas que desea aplicar a los campos de esquema. Para este caso de uso, seleccione la **[!UICONTROL PHI/ Datos de salud regulados]** etiqueta, luego seleccione **[!UICONTROL Guardar]**.

![Imagen que muestra la etiqueta RHD seleccionada y guardada](../images/abac-end-to-end-user-guide/abac-select-schema-labels.png)

>[!NOTE]
>
>Cuando se agrega una etiqueta a un campo, esa etiqueta se aplica al recurso principal de ese campo (una clase o un grupo de campos). Si la clase principal o el grupo de campos están empleados por otros esquemas, esos esquemas heredarán la misma etiqueta.

## Aplicación de etiquetas a segmentos

Una vez que haya completado el etiquetado de los campos de esquema, puede empezar a etiquetar los segmentos.

Seleccionar **[!UICONTROL Segmentos]** en el panel de navegación izquierdo. Se muestra una lista de los segmentos disponibles en su organización. En este ejemplo, los dos segmentos siguientes deben etiquetarse, ya que contienen datos confidenciales de estado:

* Glucosa en sangre > 100
* Insulina &lt;50

Seleccionar **[!UICONTROL Glucosa en sangre > 100]** para empezar a etiquetar el segmento.

![Imagen que muestra la glucosa en sangre >100 seleccionada en la ficha Segmentos](../images/abac-end-to-end-user-guide/abac-select-segment.png)

El segmento **[!UICONTROL Detalles]** aparece la pantalla. Seleccionar **[!UICONTROL Administrar acceso]**.

![Imagen que muestra la selección del acceso de Administración](../images/abac-end-to-end-user-guide/abac-segment-fields-manage-access.png)

El **[!UICONTROL Editar etiquetas]** aparece un cuadro de diálogo que le permite elegir las etiquetas que desea aplicar al segmento. Para este caso de uso, seleccione la **[!UICONTROL PHI/ Datos de salud regulados]** etiqueta, luego seleccione **[!UICONTROL Guardar]**.

![Imagen que muestra la selección de la etiqueta RHD y el guardado que se está seleccionando](../images/abac-end-to-end-user-guide/abac-select-segment-labels.png)

Repita los pasos anteriores con **[!UICONTROL Insulina &lt;50]**.

## Activación de la directiva de control de acceso {#policy}

La directiva de control de acceso predeterminada aprovecha las etiquetas para definir qué funciones de usuario tienen acceso a recursos de Platform específicos. En este ejemplo, el acceso a los campos y segmentos de esquema se denegará en todas las zonas protegidas para los usuarios que no estén en una función que tenga las etiquetas correspondientes en el campo de esquema.

Para activar la directiva de control de acceso, seleccione [!UICONTROL Permisos] en el panel de navegación izquierdo y seleccione **[!UICONTROL Políticas]**.

![Lista de directivas mostradas](../images/abac-end-to-end-user-guide/abac-policies-page.png)

A continuación, seleccione los puntos suspensivos (`...`) junto al nombre de la directiva, y un menú desplegable muestra controles para editar, activar, eliminar o duplicar la función. Seleccionar **[!UICONTROL Activar]** en el menú desplegable.

![Menú desplegable para activar la directiva](../images/abac-end-to-end-user-guide/abac-policies-activate.png)

Aparecerá el cuadro de diálogo Activar directiva, que le pedirá que confirme la activación. Seleccionar **[!UICONTROL Confirmar]**.

![Activar cuadro de diálogo de política](../images/abac-end-to-end-user-guide/abac-activate-policies-dialog.png)

Se recibe la confirmación de la activación de la directiva y se le devuelve al [!UICONTROL Políticas] página.

![Activar confirmación de directiva](../images/abac-end-to-end-user-guide/abac-policies-confirm-activate.png)

<!-- ## Create an access control policy {#policy}

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about"
>title="What are policies?"
>abstract="Policies are statements that bring attributes together to establish permissible and impermissible actions. Every organization comes with a default policy that you must activate to define rules for resources like segments and schema fields. Default policies can neither be edited nor deleted. However, default policies can be activated or deactivated."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html" text="Manage policies"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about_create"
>title="Create a policy"
>abstract="Create a policy to define the actions that your users can and cannot take against your segments and schema fields."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html#create-a-new-policy" text="Create a policy"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_permitdeny"
>title="Configure permissible and impermissible actions for a policy"
>abstract="A <b>deny access to</b> policy will deny users access when the criteria is met. Combined with <b>The following being false</b> - all users will be denied access unless they meet the matching criteria set. This type of policy allows you to protect a sensitive resource and only allow access to users with matching labels. <br>A <b>permit access to</b> policy will permit users access when the criteria are met. When combined with <b>The following being true</b> - users will be given access if they meet the matching criteria set. This does not explicitly deny access to users, but adds a permit access. This type of policy allows you to give additional access to resource and in addition to those users who might already have access through role permissions."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html#edit-a-policy" text="Edit a policy"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_resource"
>title="Configure permissions for a resource"
>abstract="A resource is the asset or object that a user can or cannot access. Resources can be segments or schemas fields. You can configure write, read, or delete permissions for segments and schema fields."

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_condition"
>title="Edit conditions"
>abstract="Apply conditional statements to your policy to configure user access to certain resources. Select match all to require users to have roles with the same labels as a resource to be permitted access. Select match any to require users to have a role with just one label matching a label on a resource. Labels can either be defined as core or custom labels, with core labels representing labels created and provided by Adobe and custom labels representing labels that you created for your organization."

Access control policies leverage labels to define which user roles have access to specific Platform resources. Policies can either be local or global and can override other policies. In this example, access to schema fields and segments will be denied in all sandboxes for users who don't have the corresponding labels in the schema field.

>[!NOTE]
>
>A "deny policy" is created to grant access to sensitive resources because the role grants permission to the subjects. The written policy in this example **denies** you access if you are missing the required labels.

To create an access control policy, select **[!UICONTROL Permissions]** from the left navigation and then select **[!UICONTROL Policies]**. Next, select **[!UICONTROL Create policy]**.

![Image showing Create policy being selected in the Permissions](../images/abac-end-to-end-user-guide/abac-create-policy.png)

The **[!UICONTROL Create new policy]** dialog appears, prompting you to enter a name and an optional description. Select **[!UICONTROL Confirm]** when finished.

![Image showing the Create new policy dialog and selecting Confirm](../images/abac-end-to-end-user-guide/abac-create-policy-details.png)

To deny access to the schema fields, use the dropdown arrow and select **[!UICONTROL Deny access to]** and then select **[!UICONTROL No resource selected]**. Next, select **[!UICONTROL Schema Field]** and then select **[!UICONTROL All]**.

![Image showing Deny access and resources selected](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-schema.png)

The table below shows the conditions available when creating a policy:

| Conditions | Description |
| --- | --- |
| The following being false| When 'Deny access to' is set, access will be restricted if the user does not meet the criteria selected. |
| The following being true| When 'Permit access to' is set, access will be permitted if the user meets the selected criteria. |
| Matches any| The user has a label that matches any label applied to a resource. |
| Matches all| The user has all labels that matches all labels applied to a resource. |
| Core label| A core label is an Adobe-defined label that is available in all Platform instances.|
| Custom label| A custom label is a label that has been created by your organization.|

Select **[!UICONTROL The following being false]** and then select **[!UICONTROL No attribute selected]**. Next, select the user **[!UICONTROL Core label]**, then select **[!UICONTROL Matches all]**. Select the resource **[!UICONTROL Core label]** and finally select **[!UICONTROL Add resource]**.

![Image showing the conditions being selected and Add resource being selected](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-schema-expression.png)

>[!TIP]
>
>A resource is the asset or object that a subject can or cannot access. Resources can be segments or schemas.

To deny access to the segments, use the dropdown arrow and select **[!UICONTROL Deny access to]** and then select **[!UICONTROL No resource selected]**. Next, select **[!UICONTROL Segment]** and then select **[!UICONTROL All]**.

Select **[!UICONTROL The following being false]** and then select **[!UICONTROL No attribute selected]**. Next, select the user **[!UICONTROL Core label]**, then select **[!UICONTROL Matches all]**. Select the resource **[!UICONTROL Core label]** and finally select **[!UICONTROL Save]**.

![Image showing conditions selected and Save being selected](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-segment.png)

Select **[!UICONTROL Activate]** to activate the policy, and a dialog appears which prompts you to confirm activation. Select **[!UICONTROL Confirm]** and then select **[!UICONTROL Close]**.

![Image showing the Policy being activated ](../images/abac-end-to-end-user-guide/abac-create-policy-activation.png) -->

## Pasos siguientes

Ha completado la aplicación de etiquetas a un rol, campos de esquema y segmentos. La agencia externa asignada a estas funciones tiene restringido el acceso a la visualización de estas etiquetas y sus valores en la vista de esquema, conjunto de datos y perfil. Estos campos también están restringidos para no utilizarse en la definición del segmento al utilizar el Generador de segmentos.

Para obtener más información sobre el control de acceso basado en atributos, consulte la [información general sobre el control de acceso basado en atributos](./overview.md).

El siguiente vídeo tiene como objetivo facilitar la comprensión del control de acceso basado en atributos y describe cómo configurar funciones, recursos y directivas.

>[!VIDEO](https://video.tv.adobe.com/v/345641?learn=on)
