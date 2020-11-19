---
title: Uso de IAB TCF 2.0 sin Experience Platform Launch
seo-title: Configuración del consentimiento TCF 2.0 de IAB con el SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo configurar el consentimiento TCF 2.0 de IAB con el SDK web de Adobe Experience Platform
seo-description: Obtenga información sobre cómo configurar el consentimiento TCF 2.0 de IAB con el SDK web de Adobe Experience Platform
translation-type: tm+mt
source-git-commit: 1b5ee9b1f9bdc7835fa8de59020b3eebb4f59505
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 0%

---


# Uso de IAB TCF 2.0 con la extensión AEP Web SDK

Esta guía muestra cómo integrar el módulo de transparencia y consentimiento de la agencia de publicidad interactiva, versión 2.0 (IAB TCF 2.0) con el SDK web de Adobe Experience Platform sin utilizar Experience Platform Launch. Para obtener información general sobre la integración con IAB TCF 2.0, lea la [información general](./overview.md). Para obtener una guía sobre cómo integrarse con Experience Platform Launch, lea la guía TCF 2.0 de [IAB para Experience Platform Launch](./with-launch.md).

## Primeros pasos

Esta guía utiliza la `__tcfapi` interfaz para acceder a la información de consentimiento. Puede que le resulte más fácil integrarse directamente con su proveedor de administración de nube (CMP). Sin embargo, la información de esta guía puede seguir siendo útil porque los CMP generalmente proporcionan una funcionalidad similar a la API de TCF.

>[!NOTE]
>
>Estos ejemplos suponen que para el momento en que se ejecuta el código, `window.__tcfapi` se define en la página. Los CMP pueden proporcionar un gancho donde se pueden ejecutar estas funciones cuando el `__tcfapi` objeto está listo.

Para utilizar IAB TCF 2.0 con Experience Platform Launch y la extensión AEP Web SDK, debe disponer de un esquema XDM disponible. Si no ha configurado ninguno de estos valores, vea esta página para inicio antes de continuar.

Además, en esta guía es necesario que tenga conocimientos prácticos sobre el SDK web de Adobe Experience Platform. Para una rápida actualización, lea la descripción general [del SDK web de](../../home.md) Adobe Experience Platform y la documentación de las preguntas [](../../web-sdk-faq.md) más frecuentes.

## Habilitación del consentimiento predeterminado

Si desea tratar a todos los usuarios desconocidos de la misma manera, puede establecer el consentimiento predeterminado en `pending`. Esto coloca en la cola Eventos de experiencia hasta que se reciben las preferencias de consentimiento.

Para obtener más información sobre el consentimiento predeterminado, consulte la sección [de consentimiento](../../fundamentals/configuring-the-sdk.md#default-consent) predeterminado de la documentación de configuración del SDK web de la plataforma.

### Configuración del consentimiento predeterminado basado en `gdprApplies`

Algunos CMP permiten determinar si el Reglamento General de Protección de Datos (RGPD) se aplica al cliente. Si desea asumir el consentimiento de los clientes a los que no se aplica el RGPD, puede utilizar el `gdprApplies` indicador en la llamada de API de TCF.

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

En este ejemplo, se llama al `configure` comando después de que `tcData` se obtenga desde la API de TCF. Si `gdprApplies` es true, el consentimiento predeterminado se establece en `pending`. Si `gdprApplies` es false, el consentimiento predeterminado se establece en `in`. Asegúrese de completar la `alloyConfiguration` variable con la configuración.

>[!NOTE]
>
>Cuando el consentimiento predeterminado se establece en `in`, el `setConsent` comando puede utilizarse para registrar las preferencias de consentimiento de los clientes.

## Uso del evento setConsent

La API TCF 2.0 de IAB proporciona un evento para cuándo el cliente actualiza el consentimiento. Esto ocurre cuando el cliente establece inicialmente sus preferencias y cuando el cliente actualiza sus preferencias.

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

Este bloque de código escucha el `useractioncomplete` evento y luego establece el consentimiento, pasando la cadena de consentimiento y el `gdprApplies` indicador. Si tiene identidades personalizadas para sus clientes, asegúrese de completar la `identityMap` variable. Consulte la guía de [apoyo al consentimiento](../../consent/supporting-consent.md) para obtener más información sobre cómo llamar `setConsent`.

## Inclusión de información de consentimiento en sendEvent

Dentro de los esquemas XDM, puede almacenar información de preferencias de consentimiento de Eventos de experiencias. Existen dos maneras de agregar esta información a cada evento.

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

Este ejemplo obtiene la información de consentimiento para la API de TCF y, a continuación, envía un evento con la información de consentimiento agregada al esquema de XDM. Consulte la guía de eventos [de](../../fundamentals/tracking-events.md) seguimiento para comprender qué debe haber en las opciones de `sendEvent` comando.

La otra manera de agregar la información de consentimiento a cada solicitud es con la `onBeforeEventSend` llamada de retorno. Lea la sección sobre [modificación global](../../fundamentals/tracking-events.md#modifying-events-globally) de eventos en la documentación de eventos de seguimiento para obtener más información sobre cómo hacerlo.

## Pasos siguientes

Ahora que ha aprendido a utilizar IAB TCF 2.0 con la extensión AEP Web SDK, también puede optar por integrarse con otras soluciones de Adobe como Adobe Analytics o la plataforma de datos de clientes en tiempo real. Consulte la información general [de](./overview.md) IAB Transparency &amp; Consent Framework 2.0 para obtener más información.
