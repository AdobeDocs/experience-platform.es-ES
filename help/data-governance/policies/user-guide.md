---
keywords: Experience Platform;inicio;temas populares;control de datos;guía del usuario de políticas de uso de datos
solution: Experience Platform
title: Administrar políticas de uso de datos en la interfaz de usuario
topic-legacy: policies
description: Administración de datos de Adobe Experience Platform proporciona una interfaz de usuario que le permite crear y administrar políticas de uso de datos. Este documento proporciona información general sobre las acciones que se pueden realizar en el espacio de trabajo Directivas de la interfaz de usuario del Experience Platform.
exl-id: 29434dc1-02c2-4267-a1f1-9f73833e76a0
source-git-commit: 5776c691b7f3ec4cb544de59cf6beef162285399
workflow-type: tm+mt
source-wordcount: '1407'
ht-degree: 0%

---

# Administrar políticas de uso de datos en la interfaz de usuario

Administración de datos de Adobe Experience Platform proporciona una interfaz de usuario que le permite crear y administrar políticas de uso de datos. Este documento proporciona información general sobre las acciones que se pueden realizar en la **Políticas** espacio de trabajo [!DNL Experience Platform] interfaz de usuario.

>[!IMPORTANT]
>
>De forma predeterminada, todas las políticas de uso de datos (incluidas las políticas principales proporcionadas por Adobe) están desactivadas. Para que una directiva individual se considere para su aplicación, debe habilitarla manualmente. Consulte la sección sobre [activar políticas](#enable) para ver los pasos sobre cómo hacerlo en la interfaz de usuario.

## Requisitos previos

Esta guía requiere una comprensión práctica de lo siguiente [!DNL Experience Platform] conceptos:

* [Control de datos](../home.md)
* [Políticas de uso de datos](./overview.md)

## Ver directivas existentes {#view-policies}

En el [!DNL Experience Platform] IU, seleccione **[!UICONTROL Políticas]** para abrir el **[!UICONTROL Políticas]** espacio de trabajo. En el **[!UICONTROL Examinar]** , puede ver una lista de las políticas disponibles, incluidas sus etiquetas asociadas, las acciones de marketing y el estado.

![](../images/policies/browse-policies.png)

Si tiene acceso a las directivas de consentimiento, seleccione la opción **[!UICONTROL Políticas de consentimiento]** alterne para visualizarlas en la [!UICONTROL Examinar] pestaña .

![](../images/policies/consent-policy-toggle.png)

Seleccione una directiva de la lista para ver su descripción y tipo. Si se selecciona una directiva personalizada, se muestran controles adicionales para editarla, eliminarla o [habilitar/deshabilitar la directiva](#enable).

![](../images/policies/policy-details.png)

## Crear una directiva personalizada {#create-policy}

Para crear una nueva directiva de uso de datos personalizada, seleccione **[!UICONTROL Crear directiva]** en la esquina superior derecha del **[!UICONTROL Examinar]** en la ficha **[!UICONTROL Políticas]** espacio de trabajo.

![](../images/policies/create-policy-button.png)

Dependiendo de si forma parte de la beta para políticas de consentimiento, se produce una de las siguientes situaciones:

* Si no forma parte de la versión beta, se le dirigirá inmediatamente al flujo de trabajo de [creación de una política de control de datos](#create-governance-policy).
* Si forma parte de la versión beta, un cuadro de diálogo proporciona una opción adicional para [crear una directiva de consentimiento](#consent-policy).
   ![](../images/policies/choose-policy-type.png)

### Crear una directiva de control de datos {#create-governance-policy}

La variable **[!UICONTROL Crear directiva]** flujo de trabajo. Comience por proporcionar un nombre y una descripción para la nueva directiva.

![](../images/policies/create-policy-description.png)

A continuación, seleccione las etiquetas de uso de datos en las que se basará la directiva. Al seleccionar varias etiquetas, se le da la opción de elegir si los datos deben contener todas las etiquetas o solo una de ellas para que se aplique la política. Select **[!UICONTROL Siguiente]** cuando termine.

![](../images/policies/add-labels.png)

La variable **[!UICONTROL Seleccionar acciones de marketing]** aparece. Elija las acciones de marketing adecuadas en la lista proporcionada y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

>[!NOTE]
>
>Al seleccionar varias acciones de marketing, la política las interpreta como una regla &quot;O&quot;. En otras palabras, la política se aplica si **any** de las acciones de marketing seleccionadas se realizan.

![](../images/policies/add-marketing-actions.png)

La variable **[!UICONTROL Consulte]** aparece, lo que le permite revisar los detalles de la nueva directiva antes de crearla. Una vez que esté satisfecho, seleccione **[!UICONTROL Finalizar]** para crear la directiva.

![](../images/policies/policy-review.png)

La variable **[!UICONTROL Examinar]** vuelve a aparecer la pestaña , que ahora enumera la política recién creada en estado &quot;Borrador&quot;. Para habilitar la directiva, consulte la siguiente sección.

![](../images/policies/created-policy.png)

### Crear una directiva de consentimiento {#consent-policy}

>[!IMPORTANT]
>
>Las políticas de consentimiento solo están disponibles para las organizaciones que han comprado **Adobe Escudo Sanitario** o **Protección de seguridad y privacidad de Adobe**.

Si elige crear una directiva de consentimiento, aparece una nueva pantalla que le permite configurar la nueva directiva.

![](../images/policies/consent-policy-dialog.png)

Para poder utilizar las políticas de consentimiento, debe tener atributos de consentimiento presentes en los datos de perfil. Consulte la guía de [procesamiento de consentimiento en el Experience Platform](../../landing/governance-privacy-security/consent/adobe/overview.md) para ver los pasos detallados sobre cómo incluir los atributos necesarios en el esquema de unión.

Las políticas de consentimiento constan de dos componentes lógicos:

* **[!UICONTROL If]**: Condición que déclencheur la comprobación de directivas. Esto se puede basar en una determinada acción de marketing que se está realizando, en la presencia de ciertas etiquetas de uso de datos o en una combinación de ambas.
* **[!UICONTROL Entonces]**: Atributos de consentimiento que deben estar presentes para que un perfil se incluya en la acción que activó la directiva.

#### Configuración de condiciones {#consent-conditions}

>[!CONTEXTUALHELP]
>id="platform_governance_policies_consentif"
>title="Condición If"
>abstract="Comience definiendo las condiciones que déclencheur la comprobación de directivas. Las condiciones pueden incluir determinadas acciones de marketing que se están realizando, la presencia de ciertas etiquetas de control de datos o una combinación de ambas."

En el **[!UICONTROL If]** , seleccione las acciones de marketing o las etiquetas de uso de datos que deben almacenar en déclencheur esta directiva. Select **[!UICONTROL Ver todo]** y **[!UICONTROL Seleccionar etiquetas]** para ver las listas completas de las etiquetas y acciones de marketing disponibles, respectivamente.

Una vez que haya añadido al menos una condición, puede seleccionar **[!UICONTROL Añadir condición]** para seguir añadiendo más condiciones según sea necesario, elija el tipo de condición apropiado en la lista desplegable.

![](../images/policies/add-condition.png)

Si selecciona varias condiciones, puede utilizar el icono que aparece entre ellas para cambiar la relación condicional entre &quot;Y&quot; y &quot;O&quot;.

![](../images/policies/and-or-selection.png)

#### Seleccionar atributos de consentimiento {#consent-attributes}

>[!CONTEXTUALHELP]
>id="platform_governance_policies_consentthen"
>title="Entonces, condición"
>abstract="Una vez definida la condición &quot;If&quot;, utilice la sección &quot;Then&quot; para seleccionar al menos un atributo de consentimiento del esquema de unión. Este es el atributo que debe estar presente para que los perfiles se incluyan en la acción regulada por esta directiva."

En el **[!UICONTROL Entonces]** , seleccione al menos un atributo de consentimiento del esquema de unión. Este es el atributo que debe estar presente para que los perfiles se incluyan en la acción regulada por esta directiva. Puede elegir una de las opciones proporcionadas en la lista o seleccionar **[!UICONTROL Ver todo]** para elegir el atributo directamente desde el esquema de unión.

Al seleccionar el atributo de consentimiento, elija los valores del atributo que desea que compruebe esta directiva.

![](../images/policies/select-schema-field.png)

Después de seleccionar al menos un atributo de consentimiento, la variable **[!UICONTROL Propiedades de directiva]** actualizaciones del panel para mostrar el número estimado de perfiles que se permitirían con esta directiva, incluido el porcentaje del almacén de perfiles total. Esta estimación se actualiza automáticamente al ajustar la configuración de la directiva.

![](../images/policies/audience-preview.png)

Para agregar más atributos de consentimiento a la directiva, seleccione **[!UICONTROL Agregar resultado]**.

![](../images/policies/add-result.png)

Puede seguir agregando y ajustando condiciones y atributos de consentimiento a la directiva según sea necesario. Cuando esté satisfecho con la configuración, proporcione un nombre y una descripción opcional para la política antes de seleccionar **[!UICONTROL Guardar]**.

![](../images/policies/name-and-save.png)

Ahora se crea la directiva de consentimiento y su estado se establece en [!UICONTROL Desactivado] de forma predeterminada. Para activar la directiva de inmediato, seleccione la opción **[!UICONTROL Estado]** alterne en el carril derecho.

![](../images/policies/enable-consent-policy.png)

#### Verificar aplicación de directiva

Después de crear y habilitar una directiva de consentimiento, puede obtener una vista previa de cómo afecta a las audiencias consentidas al activar segmentos en destinos. Consulte la sección sobre [evaluación de la política de consentimiento](../enforcement/auto-enforcement.md#consent-policy-evaluation) para obtener más información.

## Habilitar o deshabilitar una directiva {#enable}

De forma predeterminada, todas las políticas de uso de datos (incluidas las políticas principales proporcionadas por Adobe) están desactivadas. Para que una política individual se considere para su aplicación, debe habilitarla manualmente a través de la API o la interfaz de usuario.

Puede habilitar o deshabilitar las directivas desde la **[!UICONTROL Examinar]** en la ficha **[!UICONTROL Políticas]** espacio de trabajo. Seleccione una directiva personalizada de la lista para mostrar sus detalles a la derecha. En **[!UICONTROL Estado]**, seleccione el botón de alternancia para habilitar o deshabilitar la directiva.

![](../images/policies/enable-policy.png)

## Ver acciones de marketing {#view-marketing-actions}

En el **[!UICONTROL Políticas]** espacio de trabajo, seleccione **[!UICONTROL Acciones de marketing]** para ver una lista de las acciones de marketing disponibles definidas por Adobe y su propia organización.

![](../images/policies/marketing-actions.png)

## Crear una acción de marketing {#create-marketing-action}

Para crear una nueva acción de marketing personalizada, seleccione **[!UICONTROL Crear una acción de marketing]** en la esquina superior derecha del **[!UICONTROL Acciones de marketing]** en la ficha **[!UICONTROL Políticas]** espacio de trabajo.

![](../images/policies/create-marketing-action.png)

La variable **[!UICONTROL Crear una acción de marketing]** se abre. Introduzca un nombre y una descripción para la acción de marketing y, a continuación, seleccione **[!UICONTROL Crear]**.

![](../images/policies/create-marketing-action-details.png)

La acción recién creada aparece en la **[!UICONTROL Acciones de marketing]** pestaña . Ahora puede utilizar la acción de marketing cuando [creación de nuevas políticas de uso de datos](#create-policy).

![](../images/policies/created-marketing-action.png)

## Editar o eliminar una acción de marketing {#edit-delete-marketing-action}

>[!NOTE]
>
>Solo se pueden editar las acciones de marketing personalizadas definidas por su organización. Las acciones de marketing definidas por Adobe no se pueden cambiar ni eliminar.

En el **[!UICONTROL Políticas]** espacio de trabajo, seleccione **[!UICONTROL Acciones de marketing]** para ver una lista de las acciones de marketing disponibles definidas por Adobe y su propia organización. Seleccione una acción de marketing personalizada de la lista y, a continuación, utilice los campos proporcionados en la sección derecha para editar los detalles de la acción de marketing.

![](../images/policies/edit-marketing-action.png)

Si la acción de marketing no está siendo utilizada por ninguna directiva de uso existente, puede eliminarla seleccionando **[!UICONTROL Eliminar acción de marketing]**.

>[!NOTE]
>
>Si se intenta eliminar una acción de marketing que está utilizando una política existente, aparece un mensaje de error que indica que el intento de eliminación ha fallado.

![](../images/policies/delete-marketing-action.png)

## Pasos siguientes

Este documento proporciona información general sobre cómo administrar las políticas de uso de datos en [!DNL Experience Platform] IU. Para ver los pasos sobre cómo administrar las políticas mediante el [!DNL Policy Service API], consulte la [guía para desarrolladores](../api/getting-started.md). Para obtener información sobre cómo aplicar las políticas de uso de datos, consulte la [información general sobre la aplicación de políticas](../enforcement/overview.md).

El siguiente vídeo muestra cómo trabajar con las políticas de uso en la [!DNL Experience Platform] IU:

>[!VIDEO](https://video.tv.adobe.com/v/32977?quality=12&learn=on)
