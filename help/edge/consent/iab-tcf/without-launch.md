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

# Integración de la compatibilidad con IAB TCF 2.0 con el SDK web de la plataforma

Esta guía muestra cómo integrar el marco de transparencia y consentimiento de la agencia de publicidad interactiva, versión 2.0 (IAB TCF 2.0) con el SDK web de Adobe Experience Platform sin utilizar etiquetas. Para obtener una descripción general de la integración con IAB TCF 2.0, lea la [información general](./overview.md). Para obtener una guía sobre cómo integrarse con etiquetas, lea la [Guía de TCF de IAB 2.0 para etiquetas](./with-launch.md).

## Primeros pasos

Esta guía utiliza la variable `__tcfapi` para acceder a la información de consentimiento. Puede que le resulte más fácil integrarlo directamente con su proveedor de administración de la nube (CMP). Sin embargo, la información de esta guía puede seguir siendo útil porque las CMP generalmente proporcionan una funcionalidad similar a la API de TCF.

>[!NOTE]
>
>Estos ejemplos suponen que para el momento en que se ejecuta el código, `window.__tcfapi` se define en la página. Las CMP pueden proporcionar un vínculo en el que puede ejecutar estas funciones cuando el `__tcfapi` está listo.

Para utilizar IAB TCF 2.0 con etiquetas y la extensión Adobe Experience Platform Web SDK, debe tener disponible un esquema XDM. Si no ha configurado ninguno de estos elementos, comience por ver esta página antes de continuar.

Además, esta guía requiere que conozca bien el SDK web de Adobe Experience Platform. Para un refresco rápido, lea el [Información general del SDK web de Adobe Experience Platform](../../home.md) y [Preguntas frecuentes](../../web-sdk-faq.md) documentación.

## Habilitación del consentimiento predeterminado

Si desea tratar a todos los usuarios desconocidos de la misma manera, puede establecer el consentimiento predeterminado en `pending` o `out`. Esto coloca en cola o descarta los eventos de experiencia hasta que se reciben las preferencias de consentimiento.

Para obtener más información sobre el consentimiento predeterminado, consulte la [sección de consentimiento predeterminado](../../fundamentals/configuring-the-sdk.md#default-consent) en la documentación de configuración de Platform Web SDK.

### Configuración del consentimiento predeterminado basada en `gdprApplies`

Algunas CMP permiten determinar si el Reglamento General de Protección de Datos (RGPD) se aplica al cliente. Si desea asumir el consentimiento de los clientes a los que no se aplica el RGPD, puede usar la variable `gdprApplies` en la llamada de API de TCF.

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

En este ejemplo, la variable `configure` se llama después de `tcData` se obtiene de la API de TCF. If `gdprApplies` es true, el consentimiento predeterminado está establecido en `pending`. If `gdprApplies` es false, el consentimiento predeterminado está establecido en `in`. Asegúrese de rellenar el `alloyConfiguration` con su configuración.

>[!NOTE]
>
>Cuando el consentimiento predeterminado está establecido en `in`, el `setConsent` puede seguir utilizándose para registrar las preferencias de consentimiento de los clientes.

## Uso del evento setConsent

La API TCF 2.0 de IAB proporciona un evento para cuándo el cliente actualiza el consentimiento. Esto ocurre cuando el cliente establece inicialmente sus preferencias y cuando actualiza sus preferencias.

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

Este bloque de código escucha para la variable `useractioncomplete` y establece el consentimiento, pasando la cadena de consentimiento y la variable `gdprApplies` indicador. Si tiene identidades personalizadas para sus clientes, asegúrese de rellenar la variable `identityMap` variable. Consulte la guía de [consentimiento de soporte](../../consent/supporting-consent.md) para obtener más información sobre cómo invocar `setConsent`.

## Inclusión de información de consentimiento en sendEvent

Dentro de los esquemas XDM, puede almacenar información de preferencias de consentimiento de Experience Events. Existen dos maneras de agregar esta información a cada evento.

En primer lugar, puede proporcionar el esquema XDM relevante en cada `sendEvent` llamada a . El siguiente ejemplo muestra una forma de hacerlo:

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

En este ejemplo se obtiene la información de consentimiento para la API de TCF y, a continuación, se envía un evento con la información de consentimiento agregada al esquema XDM. Consulte la [seguimiento de eventos](../../fundamentals/tracking-events.md) guía para comprender qué debería estar en la variable `sendEvent` opciones del comando.

La otra forma de añadir la información de consentimiento a cada solicitud es con la variable `onBeforeEventSend` llamada de retorno. Lea la sección en [modificar eventos globalmente](../../fundamentals/tracking-events.md#modifying-events-globally) desde la documentación de seguimiento de eventos para obtener más información sobre cómo hacerlo.

## Pasos siguientes

Ahora que ha aprendido a utilizar IAB TCF 2.0 con la extensión web SDK de Platform, también puede optar por integrar con otras soluciones de Adobe, como Adobe Analytics o Adobe Real-time Customer Data Platform. Consulte la [Resumen de Transparencia y Consentimiento de IAB Framework 2.0](./overview.md) para obtener más información.
