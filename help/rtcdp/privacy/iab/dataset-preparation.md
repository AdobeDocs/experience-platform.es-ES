---
keywords: Experience Platform;home;IAB;IAB 2.0;consent;Consent
solution: Experience Platform
title: Compatibilidad con IAB TCF 2.0 en la plataforma de datos del cliente en tiempo real
topic: privacy events
description: Este documento proporciona los pasos para configurar los dos conjuntos de datos necesarios para recopilar datos de consentimiento TCF 2.0 de IAB.
translation-type: tm+mt
source-git-commit: fa667d86c089c692f22cfd1b46f3f11b6e9a68d7
workflow-type: tm+mt
source-wordcount: '1369'
ht-degree: 0%

---


# Crear conjuntos de datos para capturar datos de consentimiento TCF 2.0 de IAB

Para [!DNL Real-time Customer Data Platform] procesar los datos de consentimiento del cliente de acuerdo con la IAB [!DNL Transparency & Consent Framework] (TCF) 2.0, esos datos deben enviarse a conjuntos de datos cuyos esquemas contengan campos de consentimiento TCF 2.0.

Específicamente, se requieren dos conjuntos de datos para capturar los datos de consentimiento TCF 2.0:

* Conjunto de datos basado en la [!DNL XDM Individual Profile] clase, habilitado para su uso en [!DNL Real-time Customer Profile].
* Un conjunto de datos basado en la [!DNL XDM ExperienceEvent] clase.

Este documento proporciona los pasos para configurar estos dos conjuntos de datos a fin de recopilar datos de consentimiento TCF 2.0 de IAB. Para obtener una descripción general del flujo de trabajo completo que se va a configurar [!DNL Real-time CDP] para TCF 2.0, consulte la información general [sobre la compatibilidad con TCF 2.0 de](./overview.md)IAB.

## Requisitos previos

Este tutorial requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

* [Modelo de datos de experiencia (XDM)](../../../xdm/home.md): El marco normalizado por el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Conceptos básicos de la composición](../../../xdm/schema/composition.md)de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM.
   * [Cree un esquema en la interfaz de usuario](../../../xdm/tutorials/create-schema-ui.md): Un tutorial sobre los conceptos básicos del trabajo con el Editor de Esquemas.
* [Adobe Experience Platform Identity Service](../../../identity-service/home.md): Le permite unir las identidades de los clientes desde sus distintas fuentes de datos entre dispositivos y sistemas.
* [Perfil](../../../profile/home.md)del cliente en tiempo real: Aprovecha [!DNL Identity Service] para permitirle crear perfiles detallados de clientes a partir de sus conjuntos de datos en tiempo real. [!DNL Real-time Customer Profile] extrae datos del Data Lake y persiste en los perfiles de los clientes en su propio almacén de datos independiente.

## Estructura de esquema de consentimiento {#structure}

Existen dos mezclas XDM que proporcionan los campos de consentimiento del cliente que se requieren para la compatibilidad con TCF 2.0: uno para datos basados en registros ([!DNL XDM Individual Profile]) y otro para datos basados en series temporales ([!DNL XDM ExperienceEvent]):

| Esquema | Descripción |
| --- | --- |
| Mezcla de privacidad de perfil | Esta mezcla captura las preferencias actuales de consentimiento de un cliente. Cuando se utiliza en un esquema [!DNL Profile]habilitado, los valores proporcionados en esta mezcla se toman como la fuente de la verdad sobre cómo debe aplicarse la aplicación del consentimiento a los datos del cliente. |
| [!DNL Experience Event] mezcla de privacidad | Esta mezcla captura las preferencias de consentimiento de un cliente en un momento dado. Los datos capturados en estos campos se pueden utilizar para rastrear los cambios en las preferencias de consentimiento de un cliente a lo largo del tiempo. |

Aunque el caso de uso de cada mezcla es diferente, los campos específicos que proporcionan son aproximadamente los mismos. Estos campos se explican con más detalle en la siguiente sección.

### Campos de mezcla de consentimiento {#privacy-mixin}

Aunque cada combinación de privacidad varía en la estructura y en los tipos de campos que contiene, ambos proporcionan el `xdm:consentString` atributo, cuyos subcampos son necesarios para que se lleve a cabo la aplicación de TCF 2.0. La estructura de estos campos se muestra a continuación, junto con los tipos de valores que esperan:

```json
{
  "xdm:consentString": {
    "xdm:consentStandard": "IAB TCF",
    "xdm:consentStandardVersion": "2.0",
    "xdm:consentStringValue": "BObdrPUOevsguAfDqFENCNAAAAAmeAAA.PVAfDObdrA.DqFENCAmeAENCDA",
    "xdm:gdprApplies": true,
    "xdm:containsPersonalData": false
  }
}
```

| Propiedad | Descripción |
| --- | --- |
| `xdm:consentString` | Contiene los datos de consentimiento actualizados del cliente y otra información contextual. |
| `xdm:consentStandard` | El marco de consentimiento al que se aplican los datos. Para la conformidad con TCF, el valor debe ser &quot;IAB TCF&quot;. |
| `xdm:consentStandardVersion` | Número de versión del marco de consentimiento indicado por `xdm:consentStandard`. Para la compatibilidad con TCF 2.0, el valor debe ser &quot;2.0&quot;. |
| `xdm:consentStringValue` | La cadena de consentimiento que se generó en función de la configuración de consentimiento seleccionada por el cliente. |
| `xdm:gdprApplies` | Un valor booleano que indica si el RGPD se aplica o no a este cliente. El valor debe establecerse en &quot;true&quot; para que se pueda aplicar TCF 2.0. Si no se incluye, el valor predeterminado es &quot;false&quot;. |
| `xdm:containsPersonalData` | Un valor booleano que indica si la actualización de consentimiento contiene o no datos personales. Si no se incluye, el valor predeterminado es &quot;false&quot;. |

## Crear esquemas de consentimiento del cliente {#create-schemas}

En la interfaz de usuario de la plataforma, haga clic en **[!UICONTROL Esquemas]** en el panel de navegación izquierdo para abrir el espacio de trabajo de **[!UICONTROL Esquemas]** . Desde aquí, siga los pasos de las secciones siguientes para crear cada esquema necesario.

>[!NOTE]
>
>Si ya tiene esquemas XDM que desea utilizar para capturar datos de consentimiento, puede editar esos esquemas en lugar de crear otros nuevos. Sin embargo, al editar esquemas existentes, es importante seguir [los principios de la evolución](../../../xdm/schema/composition.md#evolution) del esquema para evitar que se rompan los cambios.

### Crear un esquema de consentimiento basado en registros {#profile-schema}

En la ficha **[!UICONTROL Examinar]** del espacio de trabajo **[!UICONTROL Esquemas]**, cree un nuevo esquema basado en la [!DNL XDM Individual Profile] clase. Una vez abierto el esquema en el Editor de Esquemas, haga clic en **[!UICONTROL Añadir]** en la sección **[!UICONTROL Mezclas]** de la izquierda del lienzo.

![](../assets/iab/add-mixin-profile.png)

Aparece el cuadro de diálogo **[!UICONTROL Añadir mezcla]** . Desde aquí, seleccione Privacidad **[!UICONTROL de]** Perfil en la lista. Opcionalmente, puede utilizar la barra de búsqueda para reducir los resultados y encontrar la mezcla más fácilmente. Una vez seleccionada la mezcla, haga clic en **[!UICONTROL Añadir mezcla]**.

![](../assets/iab/add-profile-privacy.png)

El lienzo del Editor de Esquemas vuelve a aparecer, permitiéndole revisar la estructura de los campos de cadena de consentimiento agregados.

![](../assets/iab/profile-privacy-structure.png)

A partir de aquí, repita los pasos anteriores para añadir las siguientes mezclas adicionales al esquema:

* [!UICONTROL IdentityMap]
* [!UICONTROL Región de captura de datos para Perfil]
* [!UICONTROL Detalles de la persona de perfil]
* [!UICONTROL Datos personales del perfil]

![](../assets/iab/profile-all-mixins.png)

Si está editando un esquema existente que ya se ha habilitado para su uso en [!DNL Real-time Customer Profile], haga clic en **[!UICONTROL Guardar]** para confirmar los cambios antes de pasar a la sección sobre la [creación de un conjunto de datos en función de su esquema](#dataset)de consentimiento. Si va a crear un nuevo esquema, siga los pasos descritos en la subsección siguiente.

#### Habilitar el esquema para utilizarlo en [!DNL Real-time Customer Profile]

Para [!DNL Real-time CDP] asociar los datos de consentimiento que recibe a perfiles específicos del cliente, el esquema de consentimiento debe estar habilitado para su uso en [!DNL Real-time Customer Profile].

>[!NOTE]
>
>El esquema de ejemplo que se muestra en esta sección utiliza su `identityMap` campo como identidad principal. Si desea establecer otro campo como identidad principal, asegúrese de que está utilizando un identificador indirecto, como un ID de cookie, y no un campo directamente identificable que está prohibido usar en publicidad basada en intereses, como una dirección de correo electrónico. Consulte a su asesor jurídico si no está seguro de qué campos están restringidos.
>
>Los pasos para establecer un campo de identidad principal para un esquema se encuentran en el tutorial [de creación de](../../../xdm/tutorials/create-schema-ui.md#identity-field)esquema.

Para habilitar el esquema para [!DNL Profile], haga clic en el nombre del esquema en el carril izquierdo para abrir el cuadro de diálogo de propiedades **[!UICONTROL del]** Esquema en el carril derecho. Desde aquí, haga clic en el botón de alternancia de **[!UICONTROL Perfil]** .

![](../assets/iab/profile-enable-profile.png)

Aparece una ventana emergente que indica que falta una identidad principal. Seleccione la casilla de verificación para utilizar una identidad principal alternativa, ya que la identidad principal estará contenida en el campo identityMap.

<img src="../assets/iab/missing-primary-identity.png" width="600" /><br>

Por último, haga clic en **[!UICONTROL Guardar]** para confirmar los cambios.

![](../assets/iab/profile-save.png)

### Crear un esquema de consentimiento basado en series temporales {#event-schema}

En la ficha **[!UICONTROL Examinar]** del espacio de trabajo **[!UICONTROL Esquemas]** , cree un nuevo esquema basado en la [!DNL XDM ExperienceEvent] clase. Una vez abierto el esquema en el Editor de Esquemas, haga clic en **[!UICONTROL Añadir]** en la sección **[!UICONTROL Mezclas]** de la izquierda del lienzo.

![](../assets/iab/add-mixin-event.png)

Aparece el cuadro de diálogo **[!UICONTROL Añadir mezcla]** . Desde aquí, seleccione Mezcla **[!UICONTROL de privacidad de]** Experience evento en la lista. Opcionalmente, puede utilizar la barra de búsqueda para reducir los resultados y encontrar la mezcla más fácilmente. Una vez seleccionada la mezcla, haga clic en **[!UICONTROL Añadir mezcla]**.

![](../assets/iab/add-event-privacy.png)

El lienzo del Editor de Esquemas vuelve a aparecer y muestra los campos de cadena de consentimiento agregados.

![](../assets/iab/event-privacy-structure.png)

A partir de aquí, repita los pasos anteriores para añadir las siguientes mezclas adicionales al esquema:

* [!UICONTROL IdentityMap]
* [!UICONTROL Detalles del entorno de ExperienceEvent]
* [!UICONTROL Detalles web de ExperienceEvent]
* [!UICONTROL Detalles de la implementación de ExperienceEvent]

Una vez agregadas las mezclas, termine haciendo clic en **[!UICONTROL Guardar]**.

![](../assets/iab/event-all-mixins.png)

## Crear conjuntos de datos basados en los esquemas de consentimiento {#datasets}

Para cada uno de los esquemas requeridos descritos anteriormente, debe crear un conjunto de datos que, en última instancia, ingrese los datos de consentimiento de los clientes. El conjunto de datos basado en el [!DNL XDM Individual Profile] esquema debe habilitarse para [!DNL Real-time Customer Profile], mientras que el conjunto de datos basado en el [!DNL XDM ExperienceEvent] esquema no debe [!DNL Profile]habilitarse.

Para comenzar, seleccione **[!UICONTROL Conjuntos]** de datos en el panel de navegación izquierdo y, a continuación, haga clic en **[!UICONTROL Crear conjunto de datos]** en la esquina superior derecha.

![](../assets/iab/dataset-create.png)

En la página siguiente, seleccione **[!UICONTROL Crear conjunto de datos desde esquema]**.

![](../assets/iab/dataset-create-from-schema.png)

Aparece el flujo de trabajo **[!UICONTROL Crear conjunto de datos a partir de esquema]** , comenzando por el paso **[!UICONTROL Seleccionar esquema]** . En la lista proporcionada, busque uno de los esquemas de consentimiento que creó anteriormente. De forma opcional, puede utilizar la búsqueda para reducir los resultados y encontrar el esquema más fácilmente. Haga clic en el botón de radio situado junto al esquema para seleccionarlo y, a continuación, haga clic en **[!UICONTROL Siguiente]** para continuar.

![](../assets/iab/dataset-select-schema.png)

Aparece el paso **[!UICONTROL Configurar conjunto de datos]** . Proporcione un nombre y una descripción únicos y fáciles de identificar para el conjunto de datos antes de hacer clic en **[!UICONTROL Finalizar]**.

![](../assets/iab/dataset-configure.png)

Se abre la página de detalles del conjunto de datos recién creado. Si el conjunto de datos se basa en su [!DNL XDM ExperienceEvent] esquema, el proceso se completa. Si el conjunto de datos se basa en su [!DNL XDM Individual Profile] esquema, el paso final del proceso es habilitar el conjunto de datos para su uso en [!DNL Real-time Customer Profile]. En el carril derecho, haga clic en el botón de alternancia de **[!UICONTROL Perfil]** para habilitar el conjunto de datos.

![](../assets/iab/dataset-enable-profile.png)

Siga los pasos anteriores de nuevo para crear el otro conjunto de datos necesario para la compatibilidad con TCF 2.0.

## Pasos siguientes

Siguiendo este tutorial, ha creado dos conjuntos de datos que ahora se pueden utilizar para recopilar datos de consentimiento del cliente:

* Un conjunto de datos [!DNL Profile]habilitado según el [!DNL XDM Individual Profile] esquema.
* Conjunto de datos basado en el [!DNL XDM ExperienceEvent] esquema para el que no está habilitado [!DNL Profile].

Ahora puede volver a la descripción general [de TCF 2.0 de](./overview.md#merge-policies) IAB para continuar el proceso de configuración [!DNL Real-time CDP] para el cumplimiento de TCF 2.0.