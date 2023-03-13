---
title: Integración de la compatibilidad con IAB TCF 2.0 mediante el SDK web de Adobe Experience Platform
description: Aprenda a configurar la compatibilidad con IAB TCF 2.0 para su sitio web sin utilizar etiquetas.
seo-description: Learn how to set up IAB TCF 2.0 consent with Adobe Experience Platform Web SDK
exl-id: 14f1802a-0f8d-487f-ae17-5daaaab05162
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 0%

---

# Integración de la compatibilidad con IAB TCF 2.0 con el SDK web de Platform

Esta guía muestra cómo integrar Interactive Advertising Bureau Transparency &amp; Consent Framework, versión 2.0 (IAB TCF 2.0) con el SDK web de Adobe Experience Platform sin utilizar etiquetas. Para obtener una descripción general de la integración con IAB TCF 2.0, lea la [descripción general](./overview.md). Para obtener una guía sobre cómo integrar con etiquetas, lea la [Guía de IAB TCF 2.0 para etiquetas](./with-launch.md).

## Primeros pasos

Esta guía utiliza el `__tcfapi` para acceder a la información de consentimiento. Puede que le resulte más fácil integrarse directamente con su proveedor de administración en la nube (CMP). Sin embargo, la información de esta guía puede seguir siendo útil porque las CMP suelen proporcionar una funcionalidad similar a la de la API de TCF.

>[!NOTE]
>
>En estos ejemplos se supone que para cuando se ejecute el código, `window.__tcfapi` se define en la página. Las CMP pueden proporcionar un vínculo en el que ejecutar estas funciones cuando el `__tcfapi` el objeto está listo.

Para utilizar IAB TCF 2.0 con etiquetas y la extensión SDK para web de Adobe Experience Platform, debe tener disponible un esquema XDM. Si no ha configurado ninguno de estos elementos, comience por ver esta página antes de continuar.

Además, esta guía requiere tener una comprensión práctica del SDK web de Adobe Experience Platform. Para un repaso rápido, lea la [Información general del SDK web de Adobe Experience Platform](../../home.md) y el [Preguntas más frecuentes](../../web-sdk-faq.md) documentación.

## Habilitar el consentimiento predeterminado

Si desea tratar a todos los usuarios desconocidos de la misma manera, puede establecer el consentimiento predeterminado en `pending` o `out`. Esto pone en cola o descarta los eventos de experiencia hasta que se reciben las preferencias de consentimiento.

Para obtener más información sobre el consentimiento predeterminado, consulte la [sección de consentimiento predeterminado](../../fundamentals/configuring-the-sdk.md#default-consent) en la documentación de configuración del SDK web de Platform.

### Configuración del consentimiento predeterminado en función de `gdprApplies`

Algunas CMP permiten determinar si el Reglamento general de protección de datos (RGPD) se aplica al cliente. Si desea dar su consentimiento a clientes en los que no se aplica el RGPD, puede utilizar la variable `gdprApplies` en la llamada de API de TCF.

El siguiente ejemplo muestra una forma de hacerlo:

```javascript
var alloyConfiguration = { ... };
window.__tcfapi('getTCData', 2, function (tcData, success) {
  if (success) {
    alloyConfiguration.defaultConsent = tcData.gdprApplies ? "pending" : "in";
    window.alloy("configure", alloyConfiguration);
  }
});
```

En este ejemplo, la variable `configure` se llama al comando después de que `tcData` se obtiene de la API de TCF. If `gdprApplies` es true, el consentimiento predeterminado se establece en `pending`. If `gdprApplies` es false, el consentimiento predeterminado se establece en `in`. Asegúrese de rellenar el `alloyConfiguration` con su configuración.

>[!NOTE]
>
>Cuando el consentimiento predeterminado está establecido en `in`, el `setConsent` aún se puede usar para registrar las preferencias de consentimiento de los clientes.

## Uso del evento setConsent

La API de IAB TCF 2.0 proporciona un evento para el momento en que el cliente actualiza el consentimiento. Esto ocurre cuando el cliente establece inicialmente sus preferencias y cuando el cliente actualiza sus preferencias.

El siguiente ejemplo muestra una forma de hacerlo:

```javascript
const identityMap = { ... };
window.__tcfapi('addEventListener', 2, function (tcData, success) {
  if (success && tcData.eventStatus === 'useractioncomplete') {
    window.alloy("setConsent", {
      identityMap,
      consent: [
        {
          standard: "IAB TCF",
          version: "2.0",
          value: tcData.tcString,
          gdprApplies: tcData.gdprApplies
        }
      ]
    });
  }
});
```

Este bloque de código escucha la `useractioncomplete` y, a continuación, establece el consentimiento, pasando la cadena de consentimiento `gdprApplies` Indicador. Si tiene identidades personalizadas para sus clientes, asegúrese de rellenar el `identityMap` variable. Consulte la guía de [consentimiento justificativo](../../consent/supporting-consent.md) para obtener más información sobre cómo llamar a `setConsent`.

## Inclusión de información de consentimiento en sendEvent

Dentro de los esquemas XDM, puede almacenar información de preferencias de consentimiento de Eventos de experiencia. Hay dos formas de añadir esta información a cada evento.

En primer lugar, puede proporcionar el esquema XDM relevante en cada `sendEvent` llamada. El siguiente ejemplo muestra una forma de hacerlo:

```javascript
var sendEventOptions = { ... };
window.__tcfapi('getTCData', 2, function (tcData, success) {
  if (success) {
    sendEventOptions.xdm.consentStrings = [{
      consentStandard: "IAB TCF"
      consentStandardVersion: "2.0"
      consentStringValue: tcData.tcString,
      gdprApplies: tcData.gdprApplies
    }];
    window.alloy("sendEvent", sendEventOptions);
  }
});
```

En este ejemplo se obtiene la información de consentimiento para la API de TCF y, a continuación, se envía un evento con la información de consentimiento añadida al esquema XDM. Consulte la [seguimiento de eventos](../../fundamentals/tracking-events.md) guía para comprender qué debe contener la variable `sendEvent` opciones de comando.

La otra forma de agregar la información de consentimiento a cada solicitud es con el `onBeforeEventSend` devolución de llamada. Lea la sección sobre [modificación de eventos globalmente](../../fundamentals/tracking-events.md#modifying-events-globally) en la documentación de eventos de seguimiento para obtener más información sobre cómo hacerlo.

## Pasos siguientes

Ahora que ha aprendido a utilizar IAB TCF 2.0 con la extensión del SDK web de Platform, también puede optar por integrar con otras soluciones de Adobe como Adobe Analytics o Adobe Real-time Customer Data Platform. Consulte la [Información general sobre el marco de transparencia y consentimiento IAB 2.0](./overview.md) para obtener más información.
