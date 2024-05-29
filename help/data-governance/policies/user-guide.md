---
keywords: Experience Platform;inicio;temas populares;control de datos;guía del usuario sobre la política de uso de datos
solution: Experience Platform
title: Administrar las políticas de uso de datos en la IU
description: Administración de datos de Adobe Experience Platform proporciona una interfaz de usuario que le permite crear y administrar políticas de uso de datos. Este documento proporciona información general sobre las acciones que se pueden realizar en el área de trabajo Directivas en la interfaz de usuario del Experience Platform.
exl-id: 29434dc1-02c2-4267-a1f1-9f73833e76a0
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '1768'
ht-degree: 1%

---

# Administrar las políticas de uso de datos en la IU {#user-guide}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsagePolicies_description"
>title="Integración y aplicación del consentimiento del cliente en los datos de perfil"
>abstract="<h2>Descripción</h2><p>Platform le permite integrar los datos de consentimiento recopilados de sus clientes en sus respectivos perfiles. A continuación, puede configurar políticas de consentimiento para determinar si estos datos se pueden incluir en segmentos activados para determinados destinos.</p>"

Este documento explica cómo usar el **[!UICONTROL Políticas]** espacio de trabajo en la IU de Adobe Experience Platform para crear y administrar políticas de uso de datos.

>[!NOTE]
>
>Para obtener información sobre cómo administrar las directivas de control de acceso en la interfaz de usuario, consulte la [guía de IU de control de acceso basado en atributos](../../access-control/abac/ui/policies.md) en su lugar.

>[!IMPORTANT]
>
>Todas las políticas de uso de datos (incluidas las políticas principales proporcionadas por Adobe) están desactivadas de forma predeterminada. Para que una directiva individual pueda considerarse para su aplicación, debe habilitarla manualmente. Consulte la sección sobre [habilitar directivas](#enable) para obtener información sobre cómo hacerlo en la interfaz de usuario.

## Requisitos previos

Esta guía requiere una comprensión práctica de lo siguiente [!DNL Experience Platform] conceptos:

* [Gobernanza de datos](../home.md)
* [Políticas de uso de datos](./overview.md)

## Ver directivas existentes {#view-policies}

En el [!DNL Experience Platform] IU, seleccione **[!UICONTROL Políticas]** para abrir **[!UICONTROL Políticas]** workspace. En el **[!UICONTROL Examinar]** , puede ver una lista de las directivas disponibles, incluidas sus etiquetas asociadas, acciones de marketing y estado.

![](../images/policies/browse-policies.png)

Si tiene acceso a las directivas de consentimiento, seleccione la **[!UICONTROL Políticas de consentimiento]** para verlas en la pestaña [!UICONTROL Examinar] pestaña.

![](../images/policies/consent-policy-toggle.png)

Seleccione una política de la lista para ver su descripción y tipo. Si se selecciona una directiva personalizada, se muestran controles adicionales para editar, eliminar o [habilitar/deshabilitar la directiva](#enable).

![](../images/policies/policy-details.png)

## Crear una directiva personalizada {#create-policy}

Para crear una nueva directiva de uso de datos personalizada, seleccione **[!UICONTROL Crear política]** en la esquina superior derecha de la **[!UICONTROL Examinar]** en la pestaña **[!UICONTROL Políticas]** workspace.

![](../images/policies/create-policy-button.png)

Dependiendo de si forma parte de la versión beta de las directivas de consentimiento, se produce una de las siguientes situaciones:

* Si no forma parte de la versión beta, se le redirige inmediatamente al flujo de trabajo para [creación de una política de gobernanza de datos](#create-governance-policy).
* Si forma parte de la versión beta, un cuadro de diálogo proporciona una opción adicional para lo siguiente [crear una directiva de consentimiento](#consent-policy).
  ![](../images/policies/choose-policy-type.png)

### Uso conjunto de la gobernanza de datos y las políticas de consentimiento {#combine-policies}

>[!NOTE]
>
>Actualmente, las políticas de consentimiento solo están disponibles para las organizaciones que han adquirido Adobe Healthcare Shield o Adobe Privacy &amp; Security Shield.

Las políticas de gobernanza y consentimiento se pueden usar juntas para crear reglas sólidas para gobernar audiencias asignadas a un destino. Las políticas de consentimiento son de naturaleza inclusiva, lo que significa que dictan qué perfiles se pueden incluir en cada experiencia de marketing. Por el contrario, las directivas de gobernanza excluyen el uso de atributos etiquetados específicos para que no se configuren para la activación.

Con este comportamiento, puede configurar una combinación de directivas y reglas de consentimiento que incluyan los perfiles correctos, pero que impidan incluir datos que vayan en contra de las reglas organizativas establecidas. Un ejemplo de escenario sería, en el que desee excluir la inclusión de datos confidenciales pero que aún puedan dirigirse a usuarios con consentimiento para su marketing a través de los medios sociales. Los pasos necesarios para este escenario se describen en la infografía siguiente.

![Una infografía que describe los pasos para utilizar juntas las políticas de gobernanza y consentimiento para crear reglas sólidas para gobernar las audiencias.](../images/policies/governance-and-consent-policies-infographic.png)

### Crear una política de gobernanza de datos {#create-governance-policy}

El **[!UICONTROL Crear política]** flujo de trabajo aparece. Comience proporcionando un nombre y una descripción para la nueva directiva.

![](../images/policies/create-policy-description.png)

A continuación, seleccione las etiquetas de uso de datos en las que se basará la directiva. Al seleccionar varias etiquetas, se le da la opción de elegir si los datos deben contener todas las etiquetas o solo una de ellas para que se aplique la directiva. Seleccionar **[!UICONTROL Siguiente]** cuando termine.

![](../images/policies/add-labels.png)

El **[!UICONTROL Seleccionar acciones de marketing]** aparece el paso. Elija las acciones de marketing adecuadas en la lista proporcionada y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

>[!NOTE]
>
>Al seleccionar varias acciones de marketing, la directiva las interpreta como una regla &quot;O&quot;. En otras palabras, la política se aplica si **cualquiera** Se realizan una de las acciones de marketing seleccionadas.

![](../images/policies/add-marketing-actions.png)

El **[!UICONTROL Revisar]** Este paso aparece, lo que le permite revisar los detalles de la nueva directiva antes de crearla. Cuando esté satisfecho, seleccione **[!UICONTROL Finalizar]** para crear la directiva.

![](../images/policies/policy-review.png)

El **[!UICONTROL Examinar]** vuelve a aparecer la pestaña, que ahora enumera la directiva recién creada en el estado Borrador. Para habilitar la directiva, consulte la siguiente sección.

![](../images/policies/created-policy.png)

### Crear una directiva de consentimiento {#consent-policy}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsagePolicies_instructions"
>title="Instrucciones"
>abstract="<ul><li>Asegúrese de introducir datos de preferencia en los esquemas de unión a través del conector de origen de OneTrust o del esquema XDM estándar para el consentimiento.</li><li>Seleccionar <a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/overview.html?lang=es">Políticas</a> en el panel de navegación izquierdo, seleccione <a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/user-guide.html#create-governance-policy">Crear política</a>.</li><li>En el <b>If</b> , describa las condiciones o acciones que almacenarán en déclencheur la comprobación de directivas.</li><li>En el <b>Entonces</b> , introduzca los atributos de consentimiento que deben estar presentes para que un perfil se incluya en la acción que activó la directiva.</li><li>Seleccionar <b>Guardar</b> para crear la directiva. Para habilitar la directiva, seleccione <b>Estado</b> alterne en el carril derecho.</li><li>Experience Platform aplica automáticamente las directivas de consentimiento habilitadas al activar segmentos en destinos y proporciona detalles sobre cómo afecta cada directiva al tamaño de la audiencia.</li><li>Para obtener más ayuda con esta función, consulte la guía de <a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/user-guide.html?lang=es#consent-policy">creación de directivas de consentimiento</a> en el Experience League.</li></ul>"

>[!IMPORTANT]
>
>Las políticas de consentimiento solo están disponibles para las organizaciones que han adquirido **Adobe Healthcare Shield** o **Adobe Escudo de seguridad y privacidad**.

Si elige crear una política de consentimiento, aparece una nueva pantalla que le permite configurar la nueva política.

![](../images/policies/consent-policy-dialog.png)

Para utilizar directivas de consentimiento, debe tener atributos de consentimiento presentes en los datos de perfil. Consulte la guía de [procesamiento de consentimiento en Experience Platform](../../landing/governance-privacy-security/consent/adobe/overview.md) para ver los pasos detallados sobre cómo incluir los atributos necesarios en el esquema de unión.

Las políticas de consentimiento se componen de dos componentes lógicos:

* **[!UICONTROL If]**: condición que almacenará en déclencheur la comprobación de directivas. Esto puede basarse en una acción de marketing determinada que se esté realizando, en la presencia de ciertas etiquetas de uso de datos o en una combinación de ambas.
* **[!UICONTROL Entonces]**: Atributos de consentimiento que deben estar presentes para que un perfil se incluya en la acción que activó la directiva.

#### Configuración de condiciones {#consent-conditions}

>[!CONTEXTUALHELP]
>id="platform_governance_policies_consentif"
>title="Condición"
>abstract="Comience por definir las condiciones que almacenarán en déclencheur la comprobación de directivas. Las condiciones pueden incluir ciertas acciones de marketing que se están realizando, ciertas etiquetas de gobernanza de datos que están presentes o una combinación de ambas."

En el **[!UICONTROL If]** , seleccione las acciones de marketing o las etiquetas de uso de datos que deben almacenar en déclencheur esta directiva. Seleccionar **[!UICONTROL Ver todo]** y **[!UICONTROL Seleccionar etiquetas]** para ver las listas completas de las acciones de marketing y etiquetas disponibles, respectivamente.

Una vez que haya añadido al menos una condición, puede seleccionar **[!UICONTROL Añadir condición]** para continuar agregando más condiciones según sea necesario, elija el tipo de condición apropiado en la lista desplegable.

![](../images/policies/add-condition.png)

Si selecciona más de una condición, puede utilizar el icono que aparece entre ellas para cambiar la relación condicional entre &quot;AND&quot; y &quot;OR&quot;.

![](../images/policies/and-or-selection.png)

#### Seleccionar atributos de consentimiento {#consent-attributes}

>[!CONTEXTUALHELP]
>id="platform_governance_policies_consentthen"
>title="Condición «then»"
>abstract="Una vez definida la condición &quot;If&quot;, utilice la sección &quot;Then&quot; para seleccionar al menos un atributo de consentimiento del esquema de unión. Este es el atributo que debe estar presente para que los perfiles se incluyan en la acción regida por esta directiva."

En el **[!UICONTROL Entonces]** , seleccione al menos un atributo de consentimiento del esquema de unión. Este es el atributo que debe estar presente para que los perfiles se incluyan en la acción regida por esta directiva. Puede elegir una de las opciones proporcionadas en la lista o seleccionar **[!UICONTROL Ver todo]** para elegir el atributo directamente desde el esquema de unión.

Al seleccionar el atributo de consentimiento, elija los valores del atributo que desea que compruebe esta directiva.

![](../images/policies/select-schema-field.png)

Después de seleccionar al menos un atributo de consentimiento, la variable **[!UICONTROL Propiedades de directiva]** El panel se actualiza para mostrar el número estimado de perfiles que se permitirían bajo esta directiva, incluido el porcentaje del almacén de perfiles total. Esta estimación se actualiza automáticamente a medida que ajusta la configuración de la directiva.

![](../images/policies/audience-preview.png)

Para añadir más atributos de consentimiento a la directiva, seleccione **[!UICONTROL Añadir resultado]**.

![](../images/policies/add-result.png)

Puede seguir agregando y ajustando condiciones y atributos de consentimiento a la directiva según sea necesario. Cuando esté satisfecho con la configuración, proporcione un nombre y una descripción opcional para la directiva antes de seleccionar **[!UICONTROL Guardar]**.

![](../images/policies/name-and-save.png)

La directiva de consentimiento ahora se crea y su estado se establece en [!UICONTROL Desactivado] de forma predeterminada. Para habilitar la directiva de inmediato, seleccione la **[!UICONTROL Estado]** alterne en el carril derecho.

![](../images/policies/enable-consent-policy.png)

#### Verificar aplicación de políticas

Después de crear y habilitar una directiva de consentimiento, puede obtener una vista previa de cómo afecta a las audiencias consentidas al activar segmentos en los destinos. Consulte la sección sobre [evaluación de directiva de consentimiento](../enforcement/auto-enforcement.md#consent-policy-evaluation) para obtener más información.

## Habilitar o deshabilitar una directiva {#enable}

Todas las políticas de uso de datos (incluidas las políticas principales proporcionadas por Adobe) están desactivadas de forma predeterminada. Para que una directiva individual se considere para su aplicación, debe habilitarla manualmente mediante la API o la interfaz de usuario.

Puede habilitar o deshabilitar directivas desde el **[!UICONTROL Examinar]** en la pestaña **[!UICONTROL Políticas]** workspace. Seleccione una directiva personalizada de la lista para mostrar sus detalles a la derecha. En **[!UICONTROL Estado]**, seleccione el botón de alternancia para activar o desactivar la directiva.

![](../images/policies/enable-policy.png)

## Ver acciones de marketing {#view-marketing-actions}

En el **[!UICONTROL Políticas]** workspace, seleccione **[!UICONTROL Acciones de marketing]** para ver una lista de las acciones de marketing disponibles definidas por Adobe y su propia organización.

![](../images/policies/marketing-actions.png)

## Creación de una acción de marketing {#create-marketing-action}

Para crear una nueva acción de marketing personalizada, seleccione **[!UICONTROL Crear acción de marketing]** en la esquina superior derecha de la **[!UICONTROL Acciones de marketing]** en la pestaña **[!UICONTROL Políticas]** workspace.

![](../images/policies/create-marketing-action.png)

El **[!UICONTROL Crear acción de marketing]** aparece el cuadro de diálogo. Introduzca un nombre y una descripción para la acción de marketing y seleccione **[!UICONTROL Crear]**.

![](../images/policies/create-marketing-action-details.png)

La acción recién creada aparece en el **[!UICONTROL Acciones de marketing]** pestaña. Ahora puede utilizar la acción de marketing cuando [crear nuevas políticas de uso de datos](#create-policy).

![](../images/policies/created-marketing-action.png)

## Editar o eliminar una acción de marketing {#edit-delete-marketing-action}

>[!NOTE]
>
>Solo se pueden editar las acciones de marketing personalizadas definidas por su organización. Las acciones de marketing definidas por el Adobe no se pueden cambiar ni eliminar.

En el **[!UICONTROL Políticas]** workspace, seleccione **[!UICONTROL Acciones de marketing]** para ver una lista de las acciones de marketing disponibles definidas por Adobe y su propia organización. Seleccione una acción de marketing personalizada de la lista y, a continuación, utilice los campos proporcionados en la sección derecha para editar los detalles de la acción de marketing.

![](../images/policies/edit-marketing-action.png)

Si la acción de marketing no se utiliza en ninguna política de uso existente, puede eliminarla seleccionando **[!UICONTROL Eliminar acción de marketing]**.

>[!NOTE]
>
>Si se intenta eliminar una acción de marketing que está siendo utilizada por una directiva existente, aparecerá un mensaje de error que indica que se ha producido un error en el intento de eliminación.

![](../images/policies/delete-marketing-action.png)

## Pasos siguientes

Este documento proporciona información general sobre cómo administrar las políticas de uso de datos en [!DNL Experience Platform] IU. Para ver los pasos de cómo administrar directivas mediante [!DNL Policy Service API], consulte la [guía para desarrolladores](../api/getting-started.md). Para obtener información sobre cómo aplicar las políticas de uso de datos, consulte la [información general sobre aplicación de políticas](../enforcement/overview.md).

El siguiente vídeo proporciona una demostración de cómo trabajar con directivas de uso en la [!DNL Experience Platform] IU:

>[!VIDEO](https://video.tv.adobe.com/v/32977?quality=12&learn=on)
