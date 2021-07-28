---
title: Integración de la compatibilidad con IAB TCF 2.0 mediante el SDK web de Adobe Experience Platform
description: Aprenda a configurar la compatibilidad con IAB TCF 2.0 para su sitio web sin utilizar etiquetas.
seo-description: Obtenga información sobre cómo configurar el consentimiento IAB TCF 2.0 con el SDK web de Adobe Experience Platform
exl-id: 14f1802a-0f8d-487f-ae17-5daaaab05162
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 0%

---

# Integración de la compatibilidad con IAB TCF 2.0 con el SDK web de la plataforma

Esta guía muestra cómo integrar el marco de transparencia y consentimiento de la agencia de publicidad interactiva, versión 2.0 (IAB TCF 2.0) con el SDK web de Adobe Experience Platform sin utilizar etiquetas. Para obtener una descripción general de la integración con IAB TCF 2.0, lea la [descripción general](./overview.md). Para obtener una guía sobre cómo integrar con etiquetas, lea la [guía TCF de IAB 2.0 para etiquetas](./with-launch.md).

## Primeros pasos

Esta guía utiliza la interfaz `__tcfapi` para acceder a la información de consentimiento. Puede que le resulte más fácil integrarlo directamente con su proveedor de administración de la nube (CMP). Sin embargo, la información de esta guía puede seguir siendo útil porque las CMP generalmente proporcionan una funcionalidad similar a la API de TCF.

>[!NOTE]
>
>Estos ejemplos suponen que para el momento en que se ejecuta el código, `window.__tcfapi` se define en la página. Las CMP pueden proporcionar un enlace en el que se pueden ejecutar estas funciones cuando el objeto `__tcfapi` está listo.

Para utilizar IAB TCF 2.0 con etiquetas y la extensión Adobe Experience Platform Web SDK, debe tener disponible un esquema XDM. Si no ha configurado ninguno de estos elementos, comience por ver esta página antes de continuar.

Además, esta guía requiere que conozca bien el SDK web de Adobe Experience Platform. Para obtener una actualización rápida, lea la [información general del SDK web de Adobe Experience Platform](../../home.md) y la documentación de las [preguntas más frecuentes](../../web-sdk-faq.md).

## Habilitación del consentimiento predeterminado

Si desea tratar a todos los usuarios desconocidos de la misma manera, puede establecer el consentimiento predeterminado en `pending` o `out`. Esto coloca en cola o descarta los eventos de experiencia hasta que se reciben las preferencias de consentimiento.

Para obtener más información sobre el consentimiento predeterminado, consulte la [sección de consentimiento predeterminado](../../fundamentals/configuring-the-sdk.md#default-consent) en la documentación de configuración del SDK web de Platform.

### Configuración del consentimiento predeterminado basada en `gdprApplies`

Algunas CMP permiten determinar si el Reglamento General de Protección de Datos (RGPD) se aplica al cliente. Si desea asumir el consentimiento para los clientes a los que no se aplica el RGPD, puede utilizar el indicador `gdprApplies` en la llamada a la API de TCF.

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

En este ejemplo, se llama al comando `configure` después de obtener el `tcData` de la API de TCF. Si `gdprApplies` es verdadero, el consentimiento predeterminado se establece en `pending`. Si `gdprApplies` es false, el consentimiento predeterminado se establece en `in`. Asegúrese de rellenar la variable `alloyConfiguration` con la configuración.

>[!NOTE]
>
>Cuando el consentimiento predeterminado se establece en `in`, el comando `setConsent` puede seguir utilizándose para registrar las preferencias de consentimiento de los clientes.

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

Este bloque de código escucha el evento `useractioncomplete` y luego establece el consentimiento, pasando la cadena de consentimiento y el indicador `gdprApplies`. Si tiene identidades personalizadas para sus clientes, asegúrese de rellenar la variable `identityMap` . Consulte la guía de [compatibilidad con consentimiento](../../consent/supporting-consent.md) para obtener más información sobre cómo llamar a `setConsent`.

## Inclusión de información de consentimiento en sendEvent

Dentro de los esquemas XDM, puede almacenar información de preferencias de consentimiento de Experience Events. Existen dos maneras de agregar esta información a cada evento.

En primer lugar, puede proporcionar el esquema XDM relevante en cada llamada `sendEvent` . El siguiente ejemplo muestra una forma de hacerlo:

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

En este ejemplo se obtiene la información de consentimiento para la API de TCF y, a continuación, se envía un evento con la información de consentimiento agregada al esquema XDM. Consulte la guía [tracking events](../../fundamentals/tracking-events.md) para comprender qué debe haber en las opciones del comando `sendEvent`.

La otra forma de agregar la información de consentimiento a cada solicitud es con la llamada de retorno `onBeforeEventSend` . Lea la sección sobre [modificación global de eventos](../../fundamentals/tracking-events.md#modifying-events-globally) desde la documentación de seguimiento de eventos para obtener más información sobre cómo hacerlo.

## Pasos siguientes

Ahora que ha aprendido a utilizar IAB TCF 2.0 con la extensión web SDK de Platform, también puede optar por integrar con otras soluciones de Adobe, como Adobe Analytics o la plataforma de datos del cliente en tiempo real. Consulte la [información general de Transparencia y consentimiento de IAB Framework 2.0](./overview.md) para obtener más información.
