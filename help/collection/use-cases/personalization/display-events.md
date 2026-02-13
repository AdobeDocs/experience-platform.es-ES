---
title: Administrar eventos de visualización en Web SDK
description: Explica qué son los eventos de visualización y cómo se pueden utilizar en Web SDK.
exl-id: 7150ad6e-7693-4f4d-917e-8d08a39a0b41
keywords: personalización;mostrar eventos;sendEvent;renderDecisions;applyPropositions;propositions;
source-git-commit: e150fa51953edbb0e21de962e066deedaf8bd2d7
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# Administrar eventos de visualización en Web SDK

Los eventos de visualización indican a los servicios de personalización o análisis que se ha mostrado un fragmento específico de contenido personalizado al usuario. El envío de eventos de visualización mejora la precisión de los informes al ayudar a los sistemas descendentes a distinguir entre el contenido *solicitado* y el contenido *mostrado*.

## Enviar eventos de visualización automáticamente

Los eventos de visualización automática suelen ser la opción más sencilla. Se envían inmediatamente después de que Web SDK termine de procesar el contenido apto de la respuesta `sendEvent`, lo que puede mejorar la precisión de la creación de informes.

Para enviar eventos de visualización automáticamente, use una llamada de `sendEvent` que establezca `renderDecisions` en `true` y `personalization.sendDisplayEvent` en `true` (o omita esta acción, ya que `true` es la opción predeterminada):

```js
alloy("sendEvent", {
  renderDecisions: true,
  personalization: { }, // sendDisplayEvent defaults to true
  xdm: {
    web: {
      webPageDetails: {
        name: "home"
      }
    }
  }
});
```

>[!NOTE]
>
>Los eventos de visualización automáticos dependen del procesamiento administrado por SDK. Si procesa contenido manualmente (incluso usando `applyPropositions`), debe enviar eventos de visualización explícitamente usando `sendEvent`.

## Enviar eventos de visualización en llamadas a `sendEvent` subsiguientes

Incluir eventos de visualización en una llamada posterior a `sendEvent` resulta útil cuando desea adjuntar datos de carga de página adicionales que no están disponibles al solicitar la personalización. Se utiliza comúnmente al implementar [eventos de página superior e inferior](/help/collection/use-cases/personalization/top-bottom-page-events.md). La implementación correcta de los eventos de visualización de esta manera ayuda a evitar problemas con la [tasa de salida hacia otro sitio](https://experienceleague.adobe.com/es/docs/analytics/components/metrics/bounce-rate) en Adobe Analytics.

1. En la llamada inicial `sendEvent` (a menudo en la parte superior de la página), solicite y procese contenido, pero suprima los eventos de visualización automática estableciendo `renderDecisions` en `true` y `personalization.sendDisplayEvent` en `false`:

   ```js
   alloy("sendEvent", {
     renderDecisions: true,
     personalization: { sendDisplayEvent: false },
     xdm: {
       web: {
         webPageDetails: {
            name: "home"
         }
       }
     }
   });
   ```

1. Más tarde (a menudo en la parte inferior de la página), llame a `sendEvent` con una carga útil XDM que incluya eventos de visualización para propuestas que se procesaron desde la solicitud anterior estableciendo [`personalization.includeRenderedPropositions`](/help/collection/js/commands/sendevent/personalization.md) en `true`:

   ```js
   alloy("sendEvent", {
     personalization: { includeRenderedPropositions: true },
     xdm: {
       // Add any additional page load telemetry you want to send here
       web: {
         webPageDetails: {
           name: "home"
         }
       }
     }
   });
   ```

>[!NOTE]
>
>Solo se incluyen las propuestas procesadas automáticamente que tenían la pantalla suprimida al utilizar `includeRenderedPropositions`.

## Envío de eventos de visualización para propuestas procesadas manualmente

Si procesa el contenido usted mismo (ya sea de forma completamente manual o mediante `applyPropositions`), debe enviar eventos de visualización explícitamente mediante el comando `sendEvent`. Llame a `sendEvent` con una carga útil XDM que incluya las siguientes propiedades:

* `_experience.decisioning.propositions` que contiene las propuestas procesadas&#39; `id`, `scope` y `scopeDetails`
* `_experience.decisioning.propositionEventType.display` se estableció en `1`

Los dos ejemplos siguientes utilizan esta función de ayuda para crear la carga útil XDM de evento de visualización:

```js
function buildDisplayEventXdm(renderedPropositions) {
  return {
    eventType: "decisioning.propositionDisplay",
    _experience: {
      decisioning: {
        propositions: renderedPropositions.map(({ id, scope, scopeDetails }) => ({
          id,
          scope,
          scopeDetails
        })),
        propositionEventType: { display: 1 }
      }
    }
  };
}
```

El siguiente ejemplo utiliza el procesamiento manual con eventos de visualización:

```js
function renderExample(propositions) {
  // Your custom logic here. Return ONLY the propositions that were actually rendered.
  // For example: return [propositions[0]];
  return [];
}

alloy("sendEvent", {
  personalization: { decisionScopes: ["discount"] },
  xdm: { }
}).then(({ propositions = [] }) => {
  const renderedPropositions = renderExample(propositions);
  if (!renderedPropositions.length) { return; }
  return alloy("sendEvent", { xdm: buildDisplayEventXdm(renderedPropositions) });
});
```

El ejemplo siguiente utiliza el comando `applyPropositions` con eventos de visualización. Encadena a `sendEvent`, `applyPropositions` y después a otro `sendEvent`:

```js
alloy("sendEvent", {
  personalization: { decisionScopes: ["discount", "salutation"] },
  xdm: { }
}).then(({ propositions = [] }) => {
  return alloy("applyPropositions", {
    propositions,
    metadata: {
      salutation: { selector: "#salutation", actionType: "setHtml" },
      discount: { selector: "#daily-special", actionType: "replaceHtml" }
    }
  });
}).then(({ propositions: renderedPropositions = [] }) => {
  if (!renderedPropositions.length) { return; }
  return alloy("sendEvent", { xdm: buildDisplayEventXdm(renderedPropositions) });
});
```

## Errores comunes que se deben evitar

* **Envíe eventos de visualización antes de que finalice el procesamiento**: Envíe eventos de visualización una vez finalizado el procesamiento automático, después de que se resuelva `applyPropositions` o después de que finalice la lógica de procesamiento manual.
* **Envíe eventos de visualización para propuestas que no procesó**: incluya solo las propuestas que se mostraron al usuario.
* **Eliminando`scopeDetails`**: se incluye `scopeDetails` del objeto de propuesta al enviar eventos de visualización.
