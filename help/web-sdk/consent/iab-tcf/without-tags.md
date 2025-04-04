---
title: Integración de la compatibilidad con IAB TCF 2.0 mediante Adobe Experience Platform Web SDK
description: Aprenda a configurar la compatibilidad con IAB TCF 2.0 para su sitio web sin utilizar etiquetas.
seo-description: Learn how to set up IAB TCF 2.0 consent with Adobe Experience Platform Web SDK
exl-id: 14f1802a-0f8d-487f-ae17-5daaaab05162
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 0%

---

# Integración de la compatibilidad con IAB TCF 2.0 con Experience Platform Web SDK

Esta guía muestra cómo integrar Interactive Advertising Bureau Transparency &amp; Consent Framework, versión 2.0 (IAB TCF 2.0) con Adobe Experience Platform Web SDK sin utilizar etiquetas. Para obtener una descripción general de la integración con IAB TCF 2.0, lea la [descripción general](./overview.md). Para obtener una guía sobre cómo integrar con etiquetas, lea la [guía IAB TCF 2.0 para etiquetas](./with-tags.md).

## Introducción

Esta guía utiliza la interfaz `__tcfapi` para obtener acceso a la información de consentimiento. Puede que le resulte más fácil integrarse directamente con su proveedor de administración en la nube (CMP). Sin embargo, la información de esta guía puede seguir siendo útil porque las CMP suelen proporcionar una funcionalidad similar a la de la API de TCF.

>[!NOTE]
>
>En estos ejemplos se supone que para cuando se ejecute el código, `window.__tcfapi` se habrá definido en la página. Las CMP pueden proporcionar un vínculo en el que ejecutar estas funciones cuando el objeto `__tcfapi` esté listo.

Para utilizar IAB TCF 2.0 con etiquetas y la extensión Adobe Experience Platform Web SDK, debe tener disponible un esquema XDM. Si no ha configurado ninguno de estos elementos, comience por ver esta página antes de continuar.

Además, esta guía requiere que tenga una comprensión práctica de Adobe Experience Platform Web SDK. Para obtener un repaso rápido, lea la [descripción general de Adobe Experience Platform Web SDK](../../home.md) y la [documentación de preguntas más frecuentes](../../faq.md).

## Habilitar el consentimiento predeterminado

Si desea tratar a todos los usuarios desconocidos de la misma manera, puede establecer [`defaultConsent`](/help/web-sdk/commands/configure/defaultconsent.md) en `pending` o `out`. Esto pone en cola o descarta los eventos de experiencia hasta que se reciben las preferencias de consentimiento.

### Estableciendo el consentimiento predeterminado en función de `gdprApplies`

Algunas CMP permiten determinar si el Reglamento general de protección de datos (RGPD) se aplica al cliente. Si desea dar su consentimiento a clientes en los que no se aplique el RGPD, puede utilizar el indicador `gdprApplies` en la llamada de API de TCF.

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

En este ejemplo, se llama al comando `configure` después de obtener `tcData` de la API de TCF. Si `gdprApplies` es verdadero, el consentimiento predeterminado es `pending`. Si `gdprApplies` es falso, el consentimiento predeterminado se establece en `in`. Asegúrese de completar la variable `alloyConfiguration` con la configuración.

>[!NOTE]
>
>Cuando el consentimiento predeterminado se establece en `in`, el comando `setConsent` se puede seguir usando para registrar las preferencias de consentimiento de los clientes.

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

Este bloque de código escucha el evento `useractioncomplete` y, a continuación, establece el consentimiento, pasando la cadena de consentimiento y la marca `gdprApplies`. Si tiene identidades personalizadas para sus clientes, asegúrese de rellenar la variable `identityMap`. Consulte la guía de [setConsent](../../../web-sdk/commands/setconsent.md) para obtener más información.

## Inclusión de información de consentimiento en sendEvent

Dentro de los esquemas XDM, puede almacenar información de preferencias de consentimiento de Eventos de experiencia. Hay dos formas de añadir esta información a cada evento.

En primer lugar, puede proporcionar el esquema XDM relevante en cada llamada de `sendEvent`. El siguiente ejemplo muestra una forma de hacerlo:

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

En este ejemplo se obtiene la información de consentimiento para la API de TCF y, a continuación, se envía un evento con la información de consentimiento añadida al esquema XDM.

La otra forma de agregar la información de consentimiento a cada solicitud es con la llamada de retorno [`onBeforeEventSend`](/help/web-sdk/commands/configure/onbeforeeventsend.md).

## Pasos siguientes

Ahora que ha aprendido a utilizar IAB TCF 2.0 con la extensión Experience Platform Web SDK, también puede optar por integrar con otras soluciones de Adobe, como Adobe Analytics o Adobe Real-Time Customer Data Platform. Consulte la [Información general sobre el marco de transparencia y consentimiento IAB 2.0](./overview.md) para obtener más información.
