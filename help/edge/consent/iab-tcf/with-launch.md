---
title: Integración de la compatibilidad con IAB TCF 2.0 mediante etiquetas y la extensión SDK para web de Platform
description: Obtenga información sobre cómo configurar el consentimiento IAB TCF 2.0 con etiquetas y la extensión SDK para web de Adobe Experience Platform.
exl-id: dc0e6b68-8257-4862-9fc4-50b370ef204f
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '839'
ht-degree: 0%

---

# Integración de la compatibilidad con IAB TCF 2.0 mediante etiquetas y la extensión SDK para web de Platform

El SDK web de Adobe Experience Platform es compatible con el marco de transparencia y consentimiento del Interactive Advertising Bureau, versión 2.0 (IAB TCF 2.0). Esta guía muestra cómo configurar una propiedad de etiqueta para enviar información de consentimiento IAB TCF 2.0 al Adobe mediante la extensión de etiqueta SDK para web de Adobe Experience Platform.

Si no desea utilizar etiquetas, consulte la guía de [uso de IAB TCF 2.0 sin etiquetas](./without-launch.md).

## Primeros pasos

Para utilizar IAB TCF 2.0 con etiquetas y la extensión SDK para web de Platform, debe tener disponibles un esquema XDM y un conjunto de datos.

Además, esta guía requiere tener una comprensión práctica del SDK web de Adobe Experience Platform. Para un repaso rápido, lea la [Información general del SDK web de Adobe Experience Platform](../../home.md) y el [Preguntas más frecuentes](../../web-sdk-faq.md) documentación.

## Configuración del consentimiento predeterminado

Dentro de la configuración de la extensión, hay una configuración para el consentimiento predeterminado. Controla el comportamiento de los clientes que no tienen una cookie de consentimiento. Si desea poner eventos de experiencia en cola para clientes que no tienen una cookie de consentimiento, establézcala en `pending`. Si desea descartar los eventos de experiencia para los clientes que no tienen una cookie de consentimiento, establézcala en `out`. También puede utilizar un elemento de datos para establecer dinámicamente el valor de consentimiento predeterminado.

Para obtener más información sobre cómo configurar el consentimiento predeterminado, consulte la [sección de consentimiento predeterminado](../../fundamentals/configuring-the-sdk.md#default-consent) en la guía de configuración de SDK.

## Actualización del perfil con información de consentimiento {#consent-code-1}

Para llamar a `setConsent` acción cuando las preferencias de consentimiento de los clientes hayan cambiado, debe crear una nueva regla de etiqueta. Comience agregando un nuevo evento y elija el tipo de evento &quot;Código personalizado&quot; de la extensión principal.

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

Este código personalizado hace dos cosas:

* Establece dos elementos de datos, uno con la cadena de consentimiento y otro con la variable `gdprApplies` Indicador. Esto resulta útil posteriormente al rellenar la acción &quot;Establecer consentimiento&quot;.

* Almacena en déclencheur la regla cuando las preferencias de consentimiento han cambiado. La acción &quot;Establecer consentimiento&quot; debe utilizarse siempre que las preferencias de consentimiento hayan cambiado. Añada una acción &quot;Set Consent&quot; en la extensión y rellene el formulario como se indica a continuación:

* Estándar: &quot;IAB TCF&quot;
* Versión: &quot;2.0&quot;
* Valor: &quot;%IAB TCF Consent String%&quot;
* Se aplica el RGPD: &quot;%IAB TCF Consent RGPD%&quot;

![Acción de consentimiento del conjunto IAB](../../assets/consent/iab-tcf/with-launch/iab-action.png)

>[!IMPORTANT]
>
>No puede elegir estos elementos de datos mediante el selector de elementos de datos porque se crearon mediante código personalizado. Debe escribir el nombre del elemento de datos con los símbolos de porcentaje. Este código actualiza el perfil del cliente con sus nuevas preferencias de consentimiento cada vez que cambian. Además, el servidor devuelve un valor de cookie que podría evitar que el SDK web de Adobe Experience Platform registre eventos de experiencia.

## Creación de un elemento de datos XDM para eventos de experiencia

La cadena de consentimiento debe incluirse en el evento de experiencia XDM. Para ello, utilice el elemento de datos Objeto XDM. Comience creando un nuevo elemento de datos de objeto XDM o, alternativamente, utilice uno que ya haya creado para enviar eventos. Si ha agregado el grupo de campos del esquema Privacidad de Experience Event a su esquema, debe tener un `consentStrings` en el objeto XDM.

1. Seleccionar **[!UICONTROL permissionStrings]**.

1. Elegir **[!UICONTROL Proporcionar elementos individuales]** y seleccione **[!UICONTROL Agregar elemento]**.

1. Expanda el **[!UICONTROL permissionString]** y expanda el primer elemento y, a continuación, rellene los siguientes valores:

* `consentStandard`: TCF de IAB
* `consentStandardVersion`: 2.0
* `consentStringValue`: %Cadena de consentimiento TCF de IAB%
* `gdprApplies`: %RGPD% de consentimiento de TCF de IAB

>[!IMPORTANT]
>
>No puede elegir estos elementos de datos mediante el selector de elementos de datos porque se crearon mediante código personalizado. Debe escribir el nombre del elemento de datos con los símbolos de porcentaje.

## Envío de un evento de experiencia inicial con información de consentimiento de IAB TCF 2.0

Si el evento de experiencia inicial en la página se activa con un evento de carga de página, es posible que la cadena de consentimiento aún no se haya cargado. Esta regla está diseñada para reemplazar el evento de carga de página actual. Para asegurarse de que la información de consentimiento se carga primero, cree una nueva regla y agregue el siguiente código como evento de código personalizado:

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

Este código es idéntico al código personalizado anterior, excepto que ambos `useractioncomplete` y `tcloaded` se gestionan los eventos. El [código personalizado anterior](#consent-code-1) solo déclencheur cuando el cliente elige sus preferencias por primera vez. Este código también déclencheur cuando el cliente ya ha elegido sus preferencias. Por ejemplo, en la segunda carga de página.

Añada una acción &quot;Enviar evento&quot; desde la extensión del SDK web de Platform. En el campo XDM, elija el elemento de datos XDM que ha creado en la sección anterior.

## Envío de otros eventos con información de consentimiento de IAB TCF 2.0

Cuando los eventos se activan después del evento de experiencia inicial, los dos elementos de datos se definen y se pueden utilizar para enviar la información de consentimiento de IAB. Utilice el mismo elemento de datos XDM para enviar eventos futuros. Se incluye la información de IAB TCF 2.0.

## Pasos siguientes

Ahora que ha aprendido a utilizar IAB TCF 2.0 con la extensión del SDK web de Platform, también puede optar por integrar con otras soluciones de Adobe como Adobe Analytics o Adobe Real-time Customer Data Platform. Consulte la [Información general sobre el marco de transparencia y consentimiento IAB 2.0](./overview.md) para obtener más información.
