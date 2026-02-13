---
title: Procesar automáticamente propuestas de acciones DOM
description: Utilice Web SDK para procesar automáticamente propuestas de acción DOM aptas y gestionar escenarios comunes de renderización de SPA.
keywords: personalización;renderDecisions;dom-action;sendEvent;applyPropositions;aplicación de una sola página;
source-git-commit: e150fa51953edbb0e21de962e066deedaf8bd2d7
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# Procesar propuestas de acciones DOM automáticamente

Utilice este patrón cuando la respuesta de personalización incluya elementos de propuesta con el esquema:

**`https://ns.adobe.com/personalization/dom-action`**

Estos elementos suelen incluir un selector y un tipo de acción (por ejemplo, `setHtml`) que Web SDK puede aplicar automáticamente cuando `renderDecisions` está habilitado.

## &#x200B;1. Administrar el parpadeo (opcional)

Si necesita evitar el parpadeo mientras se aplica contenido personalizado, utilice el método de administración de parpadeo recomendado para su implementación. Consulte [Administrar parpadeo](manage-flicker.md) para ver las opciones disponibles.

## &#x200B;2. Solicitar y procesar decisiones anotadas para procesamiento automático

Establezca `renderDecisions` en `true` al llamar al comando `sendEvent`. El valor predeterminado de la propiedad `renderDecisions` es false cuando se omite.

```js
alloy("sendEvent", {
  renderDecisions: true,
  xdm: {
    web: {
      webPageDetails: {
        name: "home"
      }
    }
  }
});
```

Opcionalmente, si necesita solicitar ubicaciones específicas, incluya `personalization.decisionScopes`:

```js
alloy("sendEvent", {
  renderDecisions: true,
  personalization: {
    decisionScopes: ["hero-banner", "recommendations"]
  },
  xdm: { }
});
```

Vea el objeto [`personalization`](/help/collection/js/commands/sendevent/personalization.md) en el comando [`sendEvent`](/help/collection/js/commands/sendevent/overview.md) para obtener más información.

## &#x200B;3. Mostrar eventos

Si establece `renderDecisions` en `true` y establece `personalization.sendDisplayEvent` en `true` o lo omite, Web SDK enviará eventos de visualización inmediatamente después de que se represente la personalización.

```js
alloy("sendEvent", {
  renderDecisions: true,
  personalization: {
    // sendDisplayEvent defaults to true when omitted
  },
  xdm: { }
});
```

Consulte [Administrar eventos de visualización](display-events.md) para ver opciones alternativas que satisfagan las necesidades de su implementación, como al usar [Eventos de página superior e inferior](top-bottom-page-events.md).

## &#x200B;4. Cambios y nueva renderización de la vista SPA

Para aplicaciones de una sola página, incluya `viewName` en eventos de cambio de vista.

```js
alloy("sendEvent", {
  renderDecisions: true,
  xdm: {
    web: {
      webPageDetails: {
        viewName: "cart"
      }
    }
  }
});
```

Si la SPA vuelve a procesar la IU para la misma vista sin una nueva recuperación de decisión, puede volver a aplicar las propuestas devueltas anteriormente:

```js
let lastPropositions = [];

alloy("sendEvent", {
  renderDecisions: true,
  xdm: {
    web: { webPageDetails: { viewName: "cart" } }
  }
}).then(({ propositions = [] }) => {
  lastPropositions = propositions;
});

// Later, after a UI re-render:
alloy("applyPropositions", {
  propositions: lastPropositions
});
```

Consulte [`applyPropositions`](/help/collection/js/commands/applypropositions.md) para obtener más información.

>[!NOTE]
>
>El comando `applyPropositions` no envía automáticamente eventos de visualización. Si necesita registrar &quot;display&quot; para escenarios de renderización, consulte [Administrar eventos de visualización](display-events.md).
