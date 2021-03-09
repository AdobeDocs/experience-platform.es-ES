---
title: Integración de la compatibilidad con IAB TCF 2.0 mediante Platform Launch y la extensión del SDK web de la plataforma
description: Obtenga información sobre cómo configurar el consentimiento IAB TCF 2.0 con Adobe Experience Platform Launch y la extensión web SDK de Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: b9fb71ac7eca95c65165d6780b681ada3f16325b
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 0%

---


# Integración de la compatibilidad con IAB TCF 2.0 mediante Platform Launch y la extensión web SDK de Platform

El SDK web de Adobe Experience Platform es compatible con el marco de transparencia y consentimiento de la agencia de publicidad interactiva, versión 2.0 (IAB TCF 2.0). Esta guía le muestra cómo configurar una propiedad de Adobe Experience Platform Launch para enviar información de consentimiento TCF de IAB a Adobe mediante la extensión web SDK de Adobe Experience Platform para Experience Platform Launch.

Si no desea utilizar Experience Platform Launch, consulte la guía sobre el [uso de IAB TCF 2.0 sin Experience Platform Launch](./without-launch.md).

## Primeros pasos

Para utilizar IAB TCF 2.0 con Experience Platform Launch y la extensión web SDK de Platform, debe tener disponible un esquema XDM y un conjunto de datos.

Además, esta guía requiere que conozca bien el SDK web de Adobe Experience Platform. Para obtener una actualización rápida, consulte la [información general del SDK web de Adobe Experience Platform](../../home.md) y la documentación de las [preguntas más frecuentes](../../web-sdk-faq.md).

## Configuración del consentimiento predeterminado

Dentro de la configuración de extensión, hay un ajuste para el consentimiento predeterminado. Esto controla el comportamiento de los clientes que no tienen una cookie de consentimiento. Si desea poner en cola eventos de experiencia para clientes que no tienen una cookie de consentimiento, configúrela en `pending`. Si desea descartar los eventos de experiencias para los clientes que no tienen una cookie de consentimiento, configúrela en `out`. También puede utilizar un elemento de datos para establecer dinámicamente el valor de consentimiento predeterminado.

Para obtener más información sobre cómo configurar el consentimiento predeterminado, consulte la [sección de consentimiento predeterminado](../../fundamentals/configuring-the-sdk.md#default-consent) en la guía de configuración del SDK.

## Actualización del perfil con información de consentimiento {#consent-code-1}

Para llamar a la acción `setConsent` cuando las preferencias de consentimiento de los clientes hayan cambiado, debe crear una nueva regla de Experience Platform Launch. Comience agregando un nuevo evento y elija el tipo de evento &quot;Custom Code&quot; de la extensión principal.

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

* Establece dos elementos de datos, uno con la cadena de consentimiento y otro con el indicador `gdprApplies`. Esto resulta útil posteriormente al rellenar la acción &quot;Establecer consentimiento&quot;.

* Activa la regla cuando han cambiado las preferencias de consentimiento. La acción &quot;Definir consentimiento&quot; debe utilizarse siempre que se hayan cambiado las preferencias de consentimiento. Añada una acción &quot;Set Consent&quot; en la extensión y rellene el formulario de la siguiente manera:

* Estándar: &quot;TCF de IAB&quot;
* Versión: &quot;2.0&quot;
* Valor: &quot;%cadena de consentimiento TCF de IAB%&quot;
* Se aplica el RGPD: &quot;%IAB TCF Consentimiento RGPD%&quot;

![Acción de consentimiento establecida de IAB](../../images/consent/iab-tcf/with-launch/iab-action.png)

>[!IMPORTANT]
>
>No puede elegir estos elementos de datos con el selector de elementos de datos porque se crearon con código personalizado. Debe escribir el nombre del elemento de datos con los signos de porcentaje. Este código actualiza el perfil del cliente con sus nuevas preferencias de consentimiento cada vez que cambian. Además, el servidor devuelve un valor de cookie, lo que podría impedir que el SDK web de Adobe Experience Platform registrara eventos de experiencia.

## Creación de un elemento de datos XDM para eventos de experiencias

La cadena de consentimiento debe incluirse en el evento de experiencia XDM. Para ello, utilice el elemento de datos Objeto XDM . Comience creando un nuevo elemento de datos de objeto XDM o, alternativamente, utilice uno que ya haya creado para enviar eventos. Si ha añadido la combinación de privacidad de eventos de experiencia al esquema, debe tener una clave `consentStrings` en el objeto XDM.

1. Seleccione **[!UICONTROL permissionStrings]**.

1. Elija **[!UICONTROL Proporcionar elementos individuales]** y seleccione **[!UICONTROL Agregar elemento]**.

1. Expanda el encabezado **[!UICONTROL permissionString]** y expanda el primer elemento y, a continuación, rellene los valores siguientes:

* `consentStandard`: TCF de IAB
* `consentStandardVersion`: 2,0
* `consentStringValue`: %IAB Cadena de consentimiento TCF%
* `gdprApplies`: %IAB Consentimiento TCF RGPD%

>[!IMPORTANT]
>
>No puede elegir estos elementos de datos con el selector de elementos de datos porque se crearon con código personalizado. Debe escribir el nombre del elemento de datos con los signos de porcentaje.

## Envío de un evento de experiencia inicial con información de consentimiento TCF 2.0 de IAB

Si el evento de experiencia inicial de la página se activa con un evento de carga de página, es posible que la cadena de consentimiento no se haya cargado todavía. El objetivo de esta regla es reemplazar el evento de carga de página actual. Para asegurarse de que la información de consentimiento se carga primero, cree una nueva regla y añada el siguiente código como evento de código personalizado:

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

Este código es idéntico al código personalizado anterior, excepto que se gestionan los eventos `useractioncomplete` y `tcloaded` . El [código personalizado anterior](#consent-code-1) solo se activa cuando el cliente elige sus preferencias por primera vez. Este código también se activa cuando el cliente ya ha elegido sus preferencias. Por ejemplo, en la segunda carga de página.

Añada una acción &quot;Enviar evento&quot; desde la extensión web SDK de Platform. Dentro del campo XDM , elija el elemento de datos XDM que creó en la sección anterior.

## Envío de otros eventos con información de consentimiento TCF 2.0 de IAB

Cuando los eventos se activan después del evento de experiencia inicial, los dos elementos de datos siguen definidos y se pueden utilizar para enviar la información de consentimiento de IAB. Utilice el mismo elemento de datos XDM para enviar eventos futuros. Se incluye la información de IAB TCF 2.0.

## Pasos siguientes

Ahora que ha aprendido a utilizar IAB TCF 2.0 con la extensión web SDK de Platform, también puede optar por integrar con otras soluciones de Adobe, como Adobe Analytics o la plataforma de datos del cliente en tiempo real. Consulte la [información general de Transparencia y consentimiento de IAB Framework 2.0](./overview.md) para obtener más información.
