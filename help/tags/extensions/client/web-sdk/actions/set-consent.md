---
title: Definir consentimiento
description: Establece el consentimiento deseado para el visitante.
source-git-commit: 8dd658c46fc92ae6d450213ab79f2766f4211c53
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# Definir consentimiento

La acción **[!UICONTROL Set consent]** determina si la extensión de etiqueta debe enviar datos (adhesión), descartar datos (exclusión) o usar [consentimiento predeterminado](../configure/consent.md) (consentimiento desconocido). Cuando un usuario permite o deniega el consentimiento en el sitio, puede utilizar esta acción para sincronizar sus preferencias con la extensión de etiqueta. El equivalente de biblioteca JavaScript de esta acción es el comando [`setConsent`](/help/collection/js/commands/setconsent.md).

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Rules]** y, a continuación, seleccione la regla que desee.
1. En [!UICONTROL Actions], seleccione una acción existente o cree una acción.
1. Establezca el campo desplegable [!UICONTROL Extension] en **[!UICONTROL Adobe Experience Platform Web SDK]**, luego establezca [!UICONTROL Action type] en **[!UICONTROL Set consent]**.

La extensión de etiquetas admite los siguientes estándares:

* **[estándar Adobe](/help/landing/governance-privacy-security/consent/adobe/overview.md)**: Se admiten los estándares 1.0 y 2.0.
* **[Marco de transparencia y consentimiento IAB](/help/landing/governance-privacy-security/consent/iab/overview.md)**: Si usa este estándar, el Perfil del cliente en tiempo real del visitante se actualiza con la información de consentimiento si la implementación está configurada correctamente:
   1. El esquema de perfil individual de XDM contiene el [grupo de campos de consentimiento TCF de IAB 2.0](/help/xdm/field-groups/profile/iab.md).
   1. El esquema Experience Event contiene el [grupo de campos de consentimiento TCF 2.0 de IAB](/help/xdm/field-groups/event/iab.md).

Adobe recomienda almacenar cualquier preferencia del cuadro de diálogo de consentimiento por separado, como en un elemento de datos. La extensión de etiqueta no ofrece una forma de recuperar el consentimiento. Para asegurarse de que las preferencias del usuario permanecen sincronizadas con la extensión de etiqueta, puede activar esta acción en cada carga de página.

## Campos disponibles

Este tipo de acción admite las siguientes opciones de configuración:

* **[!UICONTROL Instance]**: la instancia de SDK a la que se aplica la acción. Este menú desplegable está desactivado si su implementación utiliza una sola instancia de SDK.
* **[!UICONTROL Identity map]**: elemento de datos que controla cómo se genera un ECID y a qué ID está asociada la información de consentimiento.
* **[!UICONTROL Consent information]**: determina si desea rellenar un formulario o proporcionar un elemento de datos que contenga información de consentimiento.
* **[!UICONTROL Standard]**: el estándar de consentimiento que desea utilizar. Las opciones disponibles incluyen &#39;[!UICONTROL Adobe]&#39; y &#39;[!UICONTROL IAB TCF]&#39;.
* **[!UICONTROL Version]**: versión del estándar de consentimiento que desea utilizar.
* **[!UICONTROL Datastream configuration overrides]**: este comando admite las invalidaciones de configuración de la secuencia de datos, lo que le permite controlar qué aplicaciones y servicios reciben estos datos. Cuando se establece una anulación de la configuración de la secuencia de datos tanto en un comando individual como en los ajustes de configuración de la extensión de la etiqueta, el comando individual tiene prioridad. Consulte [Anulaciones de configuración de secuencia de datos](../configure/configuration-overrides.md) para obtener más información.

## Creación de una regla que actualice la información de consentimiento

Un momento ideal para utilizar esta acción es cuando las preferencias de consentimiento de un cliente han cambiado. Puede crear una regla de etiqueta para detectar este cambio.

1. Dentro de una propiedad de etiqueta, navegue hasta **[!UICONTROL Rules]** y seleccione **[!UICONTROL Add rule]**.
1. Asigne un nombre a la regla y, a continuación, seleccione el icono &#39;`+`&#39; junto a **[!UICONTROL Events]**.
1. Establezca las siguientes propiedades a la izquierda:
   * **[!UICONTROL Extension]**: [!UICONTROL Core]
   * **[!UICONTROL EVent type]**: [!UICONTROL Custom code]
1. Abra el editor de la derecha y utilice el siguiente código como plantilla:

```javascript
// Wait for window.__tcfapi to be defined, then trigger when the customer has completed their consent and preferences.
function addEventListener() {
  if (window.__tcfapi) {
    window.__tcfapi("addEventListener", 2, function (tcData, success) {
      if (success && tcData.eventStatus === "useractioncomplete") {
        // save the tcData.tcString in a data element
        _satellite.setVar("IAB TCF Consent String", tcData.tcString);
        _satellite.setVar("IAB TCF Consent GDPR", tcData.gdprApplies);
        trigger();
      }
    });
  } else {
    // window.__tcfapi wasn't defined. Check again in 100 milliseconds
    setTimeout(addEventListener, 100);
  }
}
addEventListener();
```

1. Seleccione **[!UICONTROL Keep changes]**.

El bloque de código personalizado anterior hace dos cosas:

* Almacena en déclencheur la regla cuando las preferencias de consentimiento han cambiado.
* Establece dos elementos de datos: **cadena de consentimiento TCF de IAB** y **RGPD de consentimiento TCF de IAB**.

Estos elementos de datos son útiles al configurar la acción &#39;[!UICONTROL Set Consent]&#39;:

1. Seleccione el icono &#39;`+`&#39; junto a **[!UICONTROL Actions]**.
1. Establezca las siguientes propiedades a la izquierda:
   * **[!UICONTROL Extension]**: [!UICONTROL Adobe Experience Platform Web SDK]
   * **[!UICONTROL Action type]**: [!UICONTROL Set consent]
1. Establezca las siguientes propiedades a la derecha:
   * **[!UICONTROL Standard]**: [!UICONTROL IAB TCF]
   * **[!UICONTROL Version]**: [!UICONTROL 2.0]
   * **[!UICONTROL Value]**: `%IAB TCF Consent String%`
   * **[!UICONTROL Does GDPR apply to this consent value]**: [!UICONTROL Provide a data element], con el valor `%IAB TCF Consent GDPR%`

![Acción de consentimiento de conjunto de IAB](../assets/iab-action.png)

>[!NOTE]
>
>No puede elegir estos elementos de datos mediante el selector de elementos de datos porque se crearon mediante código personalizado. Debe escribir el nombre del elemento de datos con los símbolos de porcentaje.
