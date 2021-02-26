---
title: Integración de la compatibilidad con IAB TCF 2.0 mediante Platform launch y la extensión del SDK web de plataforma
description: Obtenga información sobre cómo configurar el consentimiento TCF 2.0 de IAB con Adobe Experience Platform Launch y la extensión Adobe Experience Platform Web SDK.
translation-type: tm+mt
source-git-commit: 1a51ce92eb5c41ff65ebcf4c652640dd0782487f
workflow-type: tm+mt
source-wordcount: '836'
ht-degree: 0%

---


# Integrar la compatibilidad con IAB TCF 2.0 mediante Platform launch y la extensión del SDK web de plataforma

Adobe Experience Platform Web SDK es compatible con Interactive Advertising Bureau Transparency &amp; Consent Framework, versión 2.0 (IAB TCF 2.0). Esta guía muestra cómo configurar una propiedad de Adobe Experience Platform Launch para enviar información de consentimiento TCF 2.0 de IAB a Adobe mediante la extensión de Adobe Experience Platform Web SDK para Experience Platform Launch.

Si no desea utilizar Experience Platform Launch, consulte la guía sobre [uso de IAB TCF 2.0 sin Experience Platform Launch](./without-launch.md).

## Primeros pasos

Para utilizar IAB TCF 2.0 con Experience Platform Launch y la extensión Platform Web SDK, debe tener un esquema XDM y un conjunto de datos disponibles.

Además, en esta guía es necesario que tenga conocimientos prácticos sobre el SDK web de Adobe Experience Platform. Para obtener un repaso rápido, lea la [información general del SDK web de Adobe Experience Platform](../../home.md) y la [documentación de las preguntas más frecuentes](../../web-sdk-faq.md).

## Configuración del consentimiento predeterminado

Dentro de la configuración de extensión, hay una configuración para el consentimiento predeterminado. Esto controla el comportamiento de los clientes que no tienen una cookie de consentimiento. Si desea poner en cola Eventos de experiencias para clientes que no tienen una cookie de consentimiento, establezca este valor en `pending`. También puede utilizar un elemento de datos para establecer dinámicamente el valor de consentimiento predeterminado.

Para obtener más información sobre cómo configurar el consentimiento predeterminado, consulte la [sección de consentimiento predeterminado](../../fundamentals/configuring-the-sdk.md#default-consent) en la guía de configuración del SDK.

## Actualizando información de Perfil con consentimiento {#consent-code-1}

Para llamar a la acción `setConsent` cuando las preferencias de consentimiento de los clientes hayan cambiado, debe crear una nueva regla de Experience Platform Launch. Para inicio, agregue un nuevo evento y elija el tipo de evento &quot;Código personalizado&quot; de la extensión Core.

Utilice el siguiente ejemplo de código para el nuevo evento:

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

Este código personalizado realiza dos acciones:

* Establece dos elementos de datos, uno con la cadena de consentimiento y otro con el indicador `gdprApplies`. Esto resulta útil posteriormente cuando se rellena la acción &quot;Definir consentimiento&quot;.

* Déclencheur la regla cuando las preferencias de consentimiento han cambiado. La acción &quot;Configurar consentimiento&quot; debe utilizarse siempre que se hayan cambiado las preferencias de consentimiento. Añada una acción &quot;Definir consentimiento&quot; en la extensión y rellene el formulario de la siguiente manera:

* Estándar: &quot;IAB TCF&quot;
* Versión: &quot;2.0&quot;
* Valor: &quot;%IAB TCF Consent String%&quot;
* Se aplica el RGPD: &quot;%IAB TCF Consent GDPR%&quot;

![Acción de aprobación de conjunto IAB](../../images/consent/iab-tcf/with-launch/iab-action.png)

>[!IMPORTANT]
>
>No puede elegir estos elementos de datos con el selector de elementos de datos porque se crearon con código personalizado. Debe escribir el nombre del elemento de datos con los signos de porcentaje. Este código actualiza el perfil del cliente con sus nuevas preferencias de consentimiento cada vez que cambian. Además, el servidor devuelve un valor de cookie, lo que podría impedir que el SDK web de Adobe Experience Platform registre Eventos de experiencia.

## Creación de un elemento de datos XDM para Eventos de experiencias

La cadena de consentimiento debe incluirse en el Evento de experiencias XDM. Para ello, utilice el elemento de datos Objeto XDM. Inicio creando un nuevo elemento de datos de objeto XDM o, alternativamente, utilice uno que ya haya creado para enviar eventos. Si ha agregado la combinación de privacidad de Experience Evento al esquema, debe tener una clave `consentStrings` en el objeto XDM.

1. Seleccione **[!UICONTROL permissionStrings]**.

1. Elija **[!UICONTROL Proporcionar elementos individuales]** y seleccione **[!UICONTROL Añadir elemento]**.

1. Expanda el encabezado **[!UICONTROL consentirString]**, expanda el primer elemento y, a continuación, rellene los siguientes valores:

* `consentStandard`:: IAB TCF
* `consentStandardVersion`:: 2,0
* `consentStringValue`:: %IAB Cadena de consentimiento TCF%
* `gdprApplies`:: %IAB Consentimiento TCF GDPR%

>[!IMPORTANT]
>
>No puede elegir estos elementos de datos con el selector de elementos de datos porque se crearon con código personalizado. Debe escribir el nombre del elemento de datos con los signos de porcentaje.

## Envío de un Evento de experiencias inicial con la información de consentimiento TCF 2.0 de IAB

Si el Evento de experiencias inicial de la página se activa con un evento de carga de página, es posible que la cadena de consentimiento no se haya cargado aún. La finalidad de esta regla es reemplazar el evento de carga de la página actual. Para asegurarse de que la información de consentimiento se carga primero, cree una nueva regla y agregue el siguiente código como evento de código personalizado:

```javascript
// Wait for window.__tcfapi to be defined, then trigger when there is a consent string
function addEventListener() {
  if (window.__tcfapi) {
    window.__tcfapi("addEventListener", 2, function (tcData, success) {
      if (success && (tcData.eventStatus === "useractioncomplete" || tcData.eventStatus === "tcloaded")) {
        // save the tcData.tcString in a data element
        _satellite.setVar("IAB TCF Consent String", tcData.tcString);
        _satellite.setVar("IAB TCF GDPR Applies", tcData.gdprApplies);
        trigger();
      }
    });
  } else {
    // window.__tcfapi wasn"t defined. Check again in 100 milliseconds
    setTimeout(addEventListener, 100);
  }
}
addEventListener();
```

Este código es idéntico al código personalizado anterior, excepto que se gestionan tanto los eventos `useractioncomplete` como `tcloaded`. El [código personalizado anterior](#consent-code-1) solo déclencheur cuando el cliente elige sus preferencias por primera vez. Este código también déclencheur cuando el cliente ya ha elegido sus preferencias. Por ejemplo, en la segunda carga de página.

Añada una acción &quot;Enviar Evento&quot; desde la extensión del SDK web de plataforma. En el campo XDM, elija el elemento de datos XDM que creó en la sección anterior.

## Envío de otros eventos con información de consentimiento TCF 2.0 de IAB

Cuando se activan eventos después del Evento de experiencias inicial, los dos elementos de datos siguen definidos y se pueden utilizar para enviar la información de consentimiento de la IAB. Utilice el mismo elemento de datos XDM para enviar eventos futuros. Se incluye la información de IAB TCF 2.0.

## Pasos siguientes

Ahora que ha aprendido a utilizar IAB TCF 2.0 con la extensión Platform Web SDK, también puede optar por integrarse con otras soluciones de Adobe como Adobe Analytics o la plataforma de datos de clientes en tiempo real. Consulte la [información general de IAB Transparency &amp; Consent Framework 2.0](./overview.md) para obtener más información.
