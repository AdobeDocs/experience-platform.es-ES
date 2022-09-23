---
keywords: Experience Platform;inicio;temas populares;control de acceso;control de acceso basado en atributos;
title: Guía de extremo a extremo del control de acceso basado en atributos
description: Este documento proporciona una guía completa sobre el control de acceso basado en atributos en Adobe Experience Platform
hide: true
hidefromtoc: true
source-git-commit: 230bcfdb92c3fbacf2e24e7210d61e2dbe0beb86
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Guía de extremo a extremo del control de acceso basado en atributos

El control de acceso basado en atributos es una función de Adobe Experience Platform que proporciona a las marcas conscientes de la privacidad buena flexibilidad para administrar el acceso de los usuarios. Los objetos individuales, como los campos de esquema y los segmentos, se pueden asignar a las funciones de usuario. Esta función le permite conceder o revocar acceso a objetos individuales para usuarios específicos de Platform de su organización.

Esta funcionalidad le permite categorizar campos de esquema, segmentos, etc. con etiquetas que definen ámbitos organizativos o de uso de datos. En Adobe Journey Optimizer, puede aplicar las mismas etiquetas a recorridos y ofertas. En paralelo, los administradores pueden definir las políticas de acceso que rodean los campos de esquema XDM y administrar mejor qué usuarios o grupos (usuarios internos, externos o de terceros) pueden acceder a dichos campos.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../xdm/home.md): El marco estandarizado mediante el cual el Experience Platform organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición del esquema](../../xdm/schema/composition.md): Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../xdm/tutorials/create-schema-ui.md): Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [Servicio de segmentación de Adobe Experience Platform](../../segmentation/home.md): El motor de segmentación dentro de [!DNL Platform] se utiliza para crear segmentos de audiencia a partir de perfiles de clientes en función de los comportamientos y atributos de los clientes.

### Información general del caso de uso

Esta guía utiliza un ejemplo de uso de restringir el acceso a datos confidenciales para demostrar el flujo de trabajo. Realizará un flujo de trabajo de control de acceso basado en atributos de ejemplo en el que creará y asignará funciones, etiquetas y políticas para configurar si los usuarios pueden o no acceder a ciertos recursos de su organización. Este caso de uso se describe a continuación:

Es un proveedor de atención médica y desea configurar el acceso a los recursos de su organización.

* El equipo de marketing interno debe poder acceder a **[!UICONTROL Datos de Salud Regulados/ PHI]** datos.
* Su agencia externa no debería poder acceder a **[!UICONTROL Datos de Salud Regulados/ PHI]** datos.

Para ello, debe configurar funciones, recursos y políticas.

Usted:

* [Etiquetado de funciones para los usuarios](#label-roles): Utilice el ejemplo de un proveedor de atención médica (ACME Business Group) cuyo grupo de marketing trabaja con agencias externas.
* [Etiquetado de recursos (campos de esquema y segmentos)](#label-resources): Asigne la variable **[!UICONTROL Datos de Salud Regulados/ PHI]** a recursos y segmentos de esquema.
* [Cree la directiva que los vinculará](#policy): Cree una directiva para vincular las etiquetas de los recursos a las etiquetas de la función que deniegan el acceso a los campos y segmentos de esquema. Esto denegará el acceso al campo de esquema y al segmento en todos los entornos limitados para los usuarios que no tengan etiquetas coincidentes.

## Permisos

[!UICONTROL Permisos] es el área de Experience Cloud en la que los administradores pueden definir funciones de usuario y políticas de acceso para administrar permisos de acceso para funciones y objetos dentro de una aplicación de producto.

Hasta [!UICONTROL Permisos], puede crear y administrar funciones, así como asignar los permisos de recursos deseados para estas funciones. [!UICONTROL Permisos] también le permiten administrar las etiquetas, los entornos limitados y los usuarios asociados a una función específica.

Si no tiene privilegios de administrador, póngase en contacto con el administrador del sistema para obtener acceso.

Una vez que tenga privilegios de administrador, vaya a [Adobe Experience Cloud](https://experience.adobe.com/) e inicie sesión con sus credenciales de Adobe. Una vez que haya iniciado sesión, la variable **[!UICONTROL Información general]** para su organización tiene privilegios de administrador para . Esta página muestra los productos a los que está suscrita su organización, junto con otros controles para agregar usuarios y administradores a la organización en su conjunto. Select **[!UICONTROL Permisos]** para abrir el espacio de trabajo para la integración de Platform.

![Imagen que muestra el producto Permisos seleccionado en Adobe Experience Cloud](../images/flac-ui/flac-select-product.png)

Aparece el espacio de trabajo Permisos para la interfaz de usuario de Platform , que se abre en la variable **[!UICONTROL Funciones]** página.

## Aplicar etiquetas a una función {#label-roles}

>[!CONTEXTUALHELP]
>id="platform_permissions_labels_about"
>title="¿Qué son las etiquetas?"
>abstract="Las etiquetas permiten categorizar los conjuntos de datos y campos según las políticas de uso que se aplican a esos datos. Platform proporciona varias etiquetas de uso de datos &quot;principales&quot; definidas por Adobe, que abarcan una amplia variedad de restricciones comunes aplicables al control de datos. Por ejemplo, las etiquetas &quot;S&quot; confidenciales, como RHD (Datos de salud regulados), permiten clasificar los datos que hacen referencia a Información de salud protegida (PHI). También puede definir sus propias etiquetas personalizadas que se adapten a las necesidades de su organización."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html?lang=en#understanding-data-usage-labels" text="Información general sobre las etiquetas de uso de datos"

>[!CONTEXTUALHELP]
>id="platform_permissions_labels_about_create"
>title="Crear nueva etiqueta"
>abstract="Puede crear sus propias etiquetas personalizadas para adaptarlas a las necesidades de su organización. Las etiquetas personalizadas se pueden usar para aplicar a los datos configuraciones de control de datos y control de acceso."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html?lang=en#manage-labels" text="Administrar etiquetas personalizadas"

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_about"
>title="¿Qué son los roles?"
>abstract="Las funciones son formas de categorizar los tipos de usuarios que interactúan con la instancia de Platform y que son componentes básicos de las políticas de control de acceso. Una función tiene un conjunto determinado de permisos y los miembros de su organización pueden asignarse a una o más funciones, según el ámbito de vista o acceso de escritura que necesiten."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/roles.html?lang=en" text="Administrar funciones"

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_about_create"
>title="Crear nueva función"
>abstract="Puede crear una nueva función para categorizar mejor a los usuarios que acceden a su instancia de Platform. Por ejemplo, puede crear una función para un equipo de marketing interno y aplicar la etiqueta RHD a esa función, lo que permitirá que su equipo de marketing interno acceda a la información de salud protegida (PHI). Alternativamente, también puede crear una función para una Agencia Externa y negar el acceso a los datos de PHI al no aplicar la etiqueta RHD a esa función."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/roles.html?lang=en#create-a-new-role" text="Crear una función nueva"

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_details"
>title="Información general sobre la función"
>abstract="El cuadro de diálogo de descripción general de funciones muestra los recursos y entornos limitados a los que se permite acceder una función determinada."

Las funciones son formas de categorizar los tipos de usuarios que interactúan con la instancia de Platform y son componentes básicos de las políticas de control de acceso. Una función tiene un conjunto determinado de permisos y los miembros de su organización pueden asignarse a una o más funciones, según el alcance de acceso que necesiten.

Para empezar, seleccione **[!UICONTROL Grupo empresarial ACME]** desde el **[!UICONTROL Funciones]** página.

![Imagen que muestra la función empresarial ACME seleccionada en Funciones](../images/abac-end-to-end-user-guide/abac-select-role.png)

A continuación, seleccione **[!UICONTROL Etiquetas]** y, a continuación, seleccione **[!UICONTROL Agregar etiquetas]**.

![Imagen que muestra Agregar etiquetas seleccionadas en la ficha Etiquetas](../images/abac-end-to-end-user-guide/abac-select-add-labels.png)

Aparecerá una lista de todas las etiquetas de su organización. Select **[!UICONTROL RHD]** para añadir la etiqueta **[!UICONTROL Datos de Salud Regulados/PHI]**. Espere unos momentos para que aparezca una marca de verificación azul junto a la etiqueta y, a continuación, seleccione **[!UICONTROL Guardar]**.

![Imagen que muestra la etiqueta RHD seleccionada y guardada](../images/abac-end-to-end-user-guide/abac-select-role-label.png)

## Aplicar etiquetas a campos de esquema {#label-resources}

Ahora que ha configurado una función de usuario con el [!UICONTROL RHD] , el siguiente paso es agregar la misma etiqueta a los recursos que desea controlar para esa función.

Select **[!UICONTROL Esquemas]** en el panel de navegación izquierdo y, a continuación, seleccione **[!UICONTROL Atención médica de ACME]** de la lista de esquemas que aparecen.

![Imagen que muestra el esquema de ACME Healthcare seleccionado en la pestaña Esquemas](../images/abac-end-to-end-user-guide/abac-select-schema.png)

A continuación, seleccione **[!UICONTROL Etiquetas]** para ver una lista que muestra los campos asociados al esquema. Desde aquí puede asignar etiquetas a uno o varios campos a la vez. Seleccione el **[!UICONTROL Glucosa sanguínea]** y **[!UICONTROL InsulinaLevel]** y, a continuación, seleccione **[!UICONTROL Editar etiquetas de control]**.

![Imagen que muestra la selección de BloodGlucosa e InsulinaLevel y la edición de las etiquetas de gobierno seleccionadas.](../images/abac-end-to-end-user-guide/abac-select-schema-labels-tab.png)

La variable **[!UICONTROL Editar etiquetas]** , que le permite elegir las etiquetas que desea aplicar a los campos de esquema. Para este caso de uso, seleccione la opción **[!UICONTROL Datos de Salud Regulados/ PHI]** etiqueta y, a continuación, seleccione **[!UICONTROL Guardar]**.

![Imagen que muestra la etiqueta RHD seleccionada y guardada](../images/abac-end-to-end-user-guide/abac-select-schema-labels.png)

>[!NOTE]
>
>Cuando se agrega una etiqueta a un campo, esa etiqueta se aplica al recurso principal de ese campo (ya sea una clase o un grupo de campos). Si la clase principal o el grupo de campos están empleados por otros esquemas, estos esquemas heredarán la misma etiqueta.

## Aplicar etiquetas a segmentos

Una vez que haya completado el etiquetado de los campos de esquema, puede empezar a etiquetar los segmentos.

Select **[!UICONTROL Segmentos]** desde el panel de navegación izquierdo. Se muestra una lista de segmentos disponibles en su organización. En este ejemplo, se deben etiquetar los dos segmentos siguientes, ya que contienen datos de estado confidenciales:

* Glucosa en sangre >100
* Insulina &lt;50

Select **[!UICONTROL Glucosa en sangre >100]** para empezar a etiquetar el segmento.

![Imagen que muestra la glucosa sanguínea >100 seleccionada en la ficha Segmentos](../images/abac-end-to-end-user-guide/abac-select-segment.png)

El segmento **[!UICONTROL Detalles]** se abre. Select **[!UICONTROL Administrar acceso]**.

![Imagen que muestra la selección de acceso a Administración](../images/abac-end-to-end-user-guide/abac-segment-fields-manage-access.png)

La variable **[!UICONTROL Editar etiquetas]** , que le permite elegir las etiquetas que desea aplicar al segmento. Para este caso de uso, seleccione la opción **[!UICONTROL Datos de Salud Regulados/ PHI]** etiqueta y, a continuación, seleccione **[!UICONTROL Guardar]**.

![Imagen que muestra la selección de la etiqueta RHD y el guardado seleccionado](../images/abac-end-to-end-user-guide/abac-select-segment-labels.png)

Repita los pasos anteriores con **[!UICONTROL Insulina &lt;50]**.

## Crear una directiva de control de acceso {#policy}

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about"
>title="¿Qué son las políticas?"
>abstract="Las políticas son declaraciones que reúnen atributos para establecer acciones permisibles e inadmisibles. Cada organización incluye una política predeterminada que debe activar para definir reglas para recursos como segmentos y campos de esquema. Las políticas predeterminadas no se pueden editar ni eliminar. Sin embargo, las directivas predeterminadas se pueden activar o desactivar."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html?lang=en" text="Administrar políticas"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about_create"
>title="Crear una directiva"
>abstract="Cree una directiva para definir las acciones que los usuarios pueden y no pueden realizar con los segmentos y los campos de esquema."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html?lang=en#create-a-new-policy" text="Crear una directiva"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_permitdeny"
>title="Configurar acciones permisibles e inadmisibles para una directiva"
>abstract="A <b>denegar el acceso a</b> la directiva denegará el acceso a los usuarios cuando se cumplan los criterios. Cuando se combina con <b>siendo false lo siguiente</b> : se denegará el acceso a todos los usuarios a menos que cumplan los criterios coincidentes establecidos. Este tipo de directiva le permite proteger un recurso confidencial y solo permitir el acceso a los usuarios que tengan etiquetas coincidentes. <br>A <b>permitir acceso a</b> esta directiva permitirá a los usuarios acceder cuando se cumplan los criterios. Cuando se combina con <b>Lo siguiente es verdadero</b> : los usuarios tendrán acceso si cumplen los criterios coincidentes establecidos. Esto no deniega explícitamente el acceso a los usuarios, pero añade un acceso de permiso. Este tipo de directiva le permite dar acceso adicional a los recursos y además de a los usuarios que ya tienen acceso a través de permisos de funciones&quot;.</br>
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/policies.html?lang=en#edit-a-policy" text="Editar una directiva"

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_resource"
>title="Configuración de permisos para un recurso"
>abstract="Un recurso es el recurso o el objeto al que un usuario puede acceder o no. Los recursos pueden ser segmentos o esquemas. Puede configurar permisos de escritura, lectura o eliminación para segmentos y campos de esquema."

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_edit_condition"
>title="Editar condiciones"
>abstract="Aplique afirmaciones condicionales a la directiva para configurar el acceso del usuario a ciertos recursos. Seleccione hacer coincidir todo para requerir que los usuarios tengan funciones con las mismas etiquetas que un recurso para que se les permita el acceso. Seleccione hacer coincidir cualquier para requerir que solo los usuarios tengan una función con una única etiqueta que coincida con un recurso. Las etiquetas se pueden definir como etiquetas principales o personalizadas, y las etiquetas principales representan las etiquetas creadas y proporcionadas por el Adobe y las etiquetas personalizadas que representan las etiquetas creadas para su organización."

Las políticas de control de acceso aprovechan las etiquetas para definir qué funciones de usuario tienen acceso a los recursos específicos de la plataforma. Las políticas pueden ser locales o globales y pueden anular otras directivas. En este ejemplo, se denegará el acceso a los campos y segmentos de esquema en todos los entornos limitados para los usuarios que no tengan las etiquetas correspondientes en el campo de esquema.

Para crear una directiva de control de acceso, seleccione **[!UICONTROL Permisos]** en el panel de navegación izquierdo y, a continuación, seleccione **[!UICONTROL Políticas]**. A continuación, seleccione **[!UICONTROL Crear directiva]**.

![Imagen que muestra la política Crear seleccionada en los Permisos](../images/abac-end-to-end-user-guide/abac-create-policy.png)

La variable **[!UICONTROL Crear nueva directiva]** , solicitándole que introduzca un nombre y una descripción opcional. Select **[!UICONTROL Confirmar]** cuando termine.

![Imagen que muestra el cuadro de diálogo Crear nueva directiva y que selecciona Confirmar](../images/abac-end-to-end-user-guide/abac-create-policy-details.png)

Para denegar el acceso a los campos del esquema, utilice la flecha desplegable y seleccione **[!UICONTROL Denegar acceso a]** y, a continuación, seleccione **[!UICONTROL No se ha seleccionado ningún recurso]**. A continuación, seleccione **[!UICONTROL Campo de esquema]** y, a continuación, seleccione **[!UICONTROL Todo]**.

![Imagen que muestra Denegar acceso y recursos seleccionados](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-schema.png)

La tabla siguiente muestra las condiciones disponibles al crear una política:

| Condiciones | Descripción |
| --- | --- |
| siendo false lo siguiente | Cuando se establece &quot;Denegar acceso a&quot;, el acceso se restringirá si el usuario no cumple los criterios seleccionados. |
| Lo siguiente es verdadero | Cuando se configura &#39;Permitir acceso a&#39;, se restringirá el acceso si el usuario cumple los criterios seleccionados. |
| Coincide con cualquier | El usuario tiene una etiqueta que coincide con cualquier etiqueta aplicada a un recurso. |
| Coincide con todo | El usuario tiene todas las etiquetas que coinciden con todas las etiquetas aplicadas a un recurso. |
| Etiqueta principal | Una etiqueta principal es una etiqueta definida por Adobe que está disponible en todas las instancias de Platform. |
| Etiqueta personalizada | Una etiqueta personalizada es una etiqueta que su organización ha creado. |

Select **[!UICONTROL siendo false lo siguiente]** y, a continuación, seleccione **[!UICONTROL No se ha seleccionado ningún atributo]**. A continuación, seleccione el usuario **[!UICONTROL Etiqueta principal]** y, a continuación, seleccione **[!UICONTROL Coincide con todo]**. Seleccione el recurso **[!UICONTROL Etiqueta principal]** y finalmente seleccione **[!UICONTROL Agregar recurso]**.

![Imagen que muestra las condiciones seleccionadas y Añadir recurso seleccionado](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-schema-expression.png)

>[!TIP]
>
>Un recurso es el recurso o objeto al que un sujeto puede acceder o no. Los recursos pueden ser segmentos o esquemas.

Para denegar el acceso a los segmentos, utilice la flecha desplegable y seleccione **[!UICONTROL Denegar acceso a]** y, a continuación, seleccione **[!UICONTROL No se ha seleccionado ningún recurso]**. A continuación, seleccione **[!UICONTROL Segmento]** y, a continuación, seleccione **[!UICONTROL Todo]**.

Select **[!UICONTROL siendo false lo siguiente]** y, a continuación, seleccione **[!UICONTROL No se ha seleccionado ningún atributo]**. A continuación, seleccione el usuario **[!UICONTROL Etiqueta principal]** y, a continuación, seleccione **[!UICONTROL Coincide con todo]**. Seleccione el recurso **[!UICONTROL Etiqueta principal]** y finalmente seleccione **[!UICONTROL Guardar]**.

![Imagen que muestra las condiciones seleccionadas y Guardar seleccionado](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-segment.png)

Select **[!UICONTROL Activar]** para activar la directiva, aparece un cuadro de diálogo que le solicita que confirme la activación. Select **[!UICONTROL Confirmar]** y, a continuación, seleccione **[!UICONTROL Cerrar]**.

![Imagen que muestra la directiva que se está activando ](../images/abac-end-to-end-user-guide/abac-create-policy-activation.png)

## Pasos siguientes

Ha completado la aplicación de etiquetas a una función, campos de esquema y segmentos. La agencia externa asignada a estas funciones está restringida de ver estas etiquetas y sus valores en el esquema, el conjunto de datos y la vista de perfil. Estos campos también están restringidos de utilizarse en la definición del segmento al usar el Generador de segmentos.

Para obtener más información sobre el control de acceso basado en atributos, consulte la [información general sobre el control de acceso basado en atributos](./overview.md).
