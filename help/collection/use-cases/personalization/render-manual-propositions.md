---
title: Procesar propuestas manualmente
description: Procese el contenido de la propuesta con su propia lógica de interfaz de usuario (HTML, JSON o esquemas personalizados) y, a continuación, registre eventos de visualización.
keywords: personalización;propuestas;procesamiento manual;sendEvent;decisionScopes;mostrar eventos;
source-git-commit: e150fa51953edbb0e21de962e066deedaf8bd2d7
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# Procesar propuestas manualmente

Utilice este patrón cuando necesite un control total sobre cómo se aplican los elementos de la propuesta. Por ejemplo, está creando una interfaz de usuario compleja a partir del contenido JSON o desea aplicar reglas empresariales personalizadas antes del procesamiento.

## &#x200B;1. Solicitar propuestas

```js
alloy("sendEvent", {
  personalization: {
    decisionScopes: ["salutation", "discount"]
  },
  xdm: { }
}).then(({ propositions = [] }) => {
  // Render in the next step
});
```

Vea el objeto [`personalization`](/help/collection/js/commands/sendevent/personalization.md) en el comando [`sendEvent`](/help/collection/js/commands/sendevent/overview.md) para obtener más información.

## &#x200B;2. Procesar elementos de propuesta (ejemplo)

Al procesar propuestas manualmente, pueden adoptar muchos formularios o formas diferentes. El siguiente es un ejemplo mínimo que busca una propuesta por ámbito y, a continuación, aplica el primer elemento de contenido de HTML que encuentra.

```js
function findPropositionByScope(propositions, scope) {
  return propositions.find((p) => p.scope === scope);
}

function renderHtmlInto(selector, html) {
  const el = document.querySelector(selector);
  if (!el) return;
  el.innerHTML = html;
}

alloy("sendEvent", {
  personalization: { decisionScopes: ["discount"] },
  xdm: { }
}).then(({ propositions = [] }) => {
  const discount = findPropositionByScope(propositions, "discount");
  if (!discount) return { propositions, rendered: [] };

  const htmlItem = discount.items?.find(
    (i) => i.schema === "https://ns.adobe.com/personalization/html-content-item"
  );

  if (!htmlItem) return { propositions, rendered: [] };

  renderHtmlInto("#daily-special", htmlItem.data.content);
  return { propositions, rendered: [discount] };
});
```

>[!IMPORTANT]
>
>Si procesa HTML, asegúrese de que sea seguro para su entorno. Considere la representación de contenido como un límite de seguridad (saneamiento, fuentes de confianza y consideraciones de CSP).

## &#x200B;3. Registre eventos de visualización para lo que ha procesado

Para las propuestas procesadas manualmente, los eventos de visualización se registran a través de `sendEvent` llamadas que hacen referencia a las propuestas procesadas.

```js
function toDisplayPayload(propositions) {
  return propositions.map((p) => ({
    id: p.id,
    scope: p.scope,
    scopeDetails: p.scopeDetails
  }));
}

// Example: record display for the propositions you actually rendered.
alloy("sendEvent", {
  xdm: {
    _experience: {
      decisioning: {
        propositions: toDisplayPayload(renderedPropositions),
        propositionEventType: { display: 1 }
      }
    }
  }
});
```

Consulte [Administrar eventos de visualización](display-events.md) para obtener más información.

## &#x200B;4. Nueva renderización

Cuando los cambios en la IU requieran un nuevo procesamiento, ejecute de nuevo la lógica de procesamiento manual con los datos de la propuesta que ha almacenado en caché (o recupere si es necesario). Si necesita registrar una pantalla para escenarios de nuevo procesamiento, consulte [Administrar eventos de visualización](display-events.md).
