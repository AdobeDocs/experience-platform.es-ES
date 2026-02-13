---
title: Procesar ofertas de HTML sin selectores
description: Procese elementos de propuesta de HTML que no incluyan selectores proporcionando metadatos para aplicar propuestas y, a continuación, registre eventos de visualización.
keywords: personalización;applyPropositions;metadatos;actionType;decisionScopes;mostrar eventos;
source-git-commit: e150fa51953edbb0e21de962e066deedaf8bd2d7
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---

# Procesar ofertas de HTML sin selectores

Utilice este patrón cuando las propuestas incluyan contenido de HTML, pero debe proporcionar dónde aplicarlo (selector) y cómo aplicarlo (tipo de acción). Puede hacerlo llamando a [`applyPropositions`](/help/collection/js/commands/applypropositions.md) con un objeto `metadata` escrito por el ámbito. `actionType` valores admitidos son `setHtml`, `replaceHtml` y `appendHtml`.

## &#x200B;1. Administrar el parpadeo (opcional)

Si oculta contenido durante el procesamiento, es usted el responsable de mostrarlo una vez finalizado el procesamiento. Consulte [Administrar parpadeo](manage-flicker.md) para obtener más información.

## &#x200B;2. Solicite propuestas para los ámbitos que desea procesar

```js
alloy("sendEvent", {
  personalization: {
    decisionScopes: ["discount", "salutation"]
  },
  xdm: { }
}).then(({ propositions = [] }) => {
  // Render in the next step
});
```

Consulte [`personalization.decisionScopes`](/help/collection/js/commands/sendevent/personalization.md) para obtener más información.

## &#x200B;3. Procesar ofertas con `applyPropositions` metadatos

```js
alloy("sendEvent", {
  personalization: {
    decisionScopes: ["discount", "salutation"]
  },
  xdm: { }
}).then(({ propositions = [] }) => {
  return alloy("applyPropositions", {
    propositions,
    metadata: {
      salutation: {
        selector: "#salutation",
        actionType: "setHtml"
      },
      discount: {
        selector: "#daily-special",
        actionType: "replaceHtml"
      }
    }
  }).then(({ propositions: renderedPropositions = [] }) => {
    return { renderedPropositions };
  });
});
```

## &#x200B;4. Registre eventos de visualización para propuestas procesadas

Los eventos de visualización no se envían automáticamente al llamar a `applyPropositions`. Una vez finalizado el procesamiento, utilice una llamada a `sendEvent` que haga referencia a las propuestas procesadas:

```js
function toDisplayPayload(propositions) {
  return propositions.map((p) => ({
    id: p.id,
    scope: p.scope,
    scopeDetails: p.scopeDetails
  }));
}

alloy("sendEvent", {
  personalization: {
    decisionScopes: ["discount", "salutation"]
  },
  xdm: { }
}).then(({ propositions = [] }) => {
  return alloy("applyPropositions", {
    propositions,
    metadata: {
      salutation: { selector: "#salutation", actionType: "setHtml" },
      discount: { selector: "#daily-special", actionType: "replaceHtml" }
    }
  }).then(({ propositions: renderedPropositions = [] }) => {
    return alloy("sendEvent", {
      xdm: {
        _experience: {
          decisioning: {
            propositions: toDisplayPayload(renderedPropositions),
            propositionEventType: { display: 1 }
          }
        }
      }
    });
  });
});
```

Consulte [Administrar eventos de visualización](display-events.md) para obtener más información.

>[!TIP]
>
>Si usa [eventos de página superior e inferior](top-bottom-page-events.md), esta llamada de &quot;visualización de registros&quot; se implementa comúnmente en la llamada inferior `sendEvent`.

## &#x200B;5. Nueva renderización

Si su implementación requiere que se vuelva a procesar más adelante (por ejemplo, en aplicaciones de una sola página), vuelva a llamar a `applyPropositions` con las mismas propuestas y metadatos:

```js
alloy("applyPropositions", {
  propositions,
  metadata: {
    discount: { selector: "#daily-special", actionType: "replaceHtml" }
  }
});
```

Si necesita registrar un evento de visualización para ese nuevo procesamiento, consulte [Administrar eventos de visualización](display-events.md).
