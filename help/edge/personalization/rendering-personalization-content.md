---
title: Representar contenido personalizado mediante el SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo procesar contenido personalizado con el SDK web de Adobe Experience Platform.
keywords: personalización;renderDecisions;sendEvent;decisionScopes;propositions;
exl-id: 6a3252ca-cdec-48a0-a001-2944ad635805
source-git-commit: 5f205792a03c3c7dd9074827ce4a989fae2e45d9
workflow-type: tm+mt
source-wordcount: '962'
ht-degree: 2%

---

# Procesar contenido personalizado

El SDK web de Adobe Experience Platform admite la recuperación de contenido personalizado de soluciones de personalización de Adobe, entre las que se incluyen [Adobe Target](https://business.adobe.com/es/products/target/adobe-target.html), [Offer decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/starting-offer-decisioning.html?lang=es) y [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=es).

Además, el SDK web potencia las capacidades de personalización de la misma página y de la siguiente página a través de destinos de personalización de Adobe Experience Platform, como [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) y el [conexión de personalización personalizada](../../destinations/catalog/personalization/custom-personalization.md). Para obtener información sobre cómo configurar Experience Platform para la personalización de la misma página y de la página siguiente, consulte la [guía especializada](../../destinations/ui/activate-edge-personalization-destinations.md).

Contenido creado en el de Adobe Target [Compositor de experiencias visuales](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) y de Adobe Journey Optimizer [IU de Campaña web](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html) El SDK puede recuperarlo y procesarlo automáticamente. Contenido creado en el de Adobe Target [Compositor de experiencias basadas en formularios](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html) El SDK no puede procesar automáticamente el Offer decisioning o. En su lugar, debe solicitar este contenido mediante el SDK y, a continuación, procesar manualmente el contenido.

## Representación automática del contenido {#automatic}

Al enviar eventos al servidor, puede configurar el `renderDecisions` opción para `true`. Esto obliga al SDK a procesar automáticamente cualquier contenido personalizado que sea apto para el procesamiento automático.

```javascript
alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
});
```

La representación del contenido personalizado es asíncrona, por lo que no debe realizar suposiciones sobre cuándo se habrá completado la representación de un fragmento de contenido determinado.

## Representación manual del contenido {#manual}

Para acceder a cualquier contenido de personalización, puede proporcionar una función de llamada de retorno a la que se llamará después de que el SDK reciba una respuesta correcta del servidor. La llamada de retorno se proporciona como `result` objeto, que puede contener un `propositions` que contenga cualquier contenido de personalización devuelto. A continuación se muestra un ejemplo de cómo proporcionaría una función de llamada de retorno al enviar un evento.

```javascript
alloy("sendEvent", {
    xdm: {}
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions and send "display" event
    }
  });
```

En este ejemplo, `result.propositions`, si existe, es una matriz que contiene propuestas de personalización relacionadas con el evento. De forma predeterminada, solo incluye propuestas que pueden procesarse automáticamente.

El `propositions` La matriz puede tener un aspecto similar al de este ejemplo:

```json
[
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "__view__",
    "items": [
      {
        "id": "11223344",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">An HTML proposition.</h2>",
          "selector": "#hero",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      ...
    },
    "renderAttempted": false
  },
  {
    "id": "AT:PyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ8",
    "scope": "__view__",
    "items": [
      {
        "id": "11223345",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">Another HTML proposition.</h2>",
          "selector": "#sidebar",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      ...
    },
    "renderAttempted": false
  }
]
```

En el ejemplo, la variable `renderDecisions` La opción no se ha establecido en `true` cuando la variable `sendEvent` se ejecutó, por lo que el SDK no intentó procesar automáticamente ningún contenido. Sin embargo, el SDK recuperó automáticamente el contenido apto para el procesamiento automático y le proporcionó esto para que lo procesara manualmente si así lo deseaba. Observe que cada objeto de propuesta tiene su `renderAttempted` propiedad establecida en `false`.

Si, en su lugar, hubiera establecido `renderDecisions` opción para `true` al enviar el evento, el SDK habría intentado procesar todas las propuestas para que se procesaran automáticamente (como se describió anteriormente). Como consecuencia, cada uno de los objetos de la propuesta tendría su `renderAttempted` propiedad establecida en `true`. No sería necesario procesar manualmente estas propuestas en este caso.

Hasta ahora, solo hemos hablado del contenido de personalización que puede procesarse automáticamente (es decir, cualquier contenido creado en el Compositor de experiencias visuales de Adobe Target o en la IU de la campaña web de Adobe Journey Optimizer). Para recuperar cualquier contenido de personalización _no_ apto para el procesamiento automático, debe solicitar el contenido rellenando la variable `decisionScopes` al enviar el evento. Un ámbito es una cadena que identifica una propuesta concreta que desea recuperar del servidor.

Vea el siguiente ejemplo:

```javascript
alloy("sendEvent", {
    xdm: {},
    decisionScopes: ['salutation', 'discount']
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions and send "display" event
    }
  });
```

En este ejemplo, si las propuestas se encuentran en el servidor que coinciden con la variable `salutation` o `discount` ámbito, se devuelven y se incluyen en la variable `result.propositions` matriz. Tenga en cuenta que las propuestas que cumplen los requisitos para el procesamiento automático seguirán incluyéndose en la `propositions` matriz, independientemente de cómo configure `renderDecisions` o `decisionScopes` opciones. El `propositions` , en este caso, tendría un aspecto similar al de este ejemplo:

```json
[
  {
    "id": "AT:cZJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ2",
    "scope": "salutation",
    "items": [
      {
        "schema": "https://ns.adobe.com/personalization/json-content-item",
        "data": {
          "id": "4433221",
          "content": {
            "salutation": "Welcome, esteemed visitor!"
          }
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      "id": "AT:cZJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ2",
      "activity": {
        "id": "384456"
      }
    },  
    "renderAttempted": false
  },
  {
    "id": "AT:FZJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ0",
    "scope": "discount",
    "items": [
      {
        "schema": "https://ns.adobe.com/personalization/html-content-item",
        "data": {
          "id": "4433222",
          "content": "<div>50% off your order!</div>",
          "format": "text/html"
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      "id": "AT:FZJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ0",
      "activity": {
        "id": "384457"
      }
    },
    "renderAttempted": false
  },
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "__view__",
    "items": [
      {
        "id": "11223344",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">An HTML proposition.</h2>",
          "selector": "#hero",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      "id": "AT:PyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ8",
      "activity": {
        "id": "384459"
      }
    },
    "renderAttempted": false
  },
  {
    "id": "AT:PyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ8",
    "scope": "__view__",
    "items": [
      {
        "id": "11223345",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">Another HTML proposition.</h2>",
          "selector": "#sidebar",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      "id": "AT:PyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ8",
      "activity": {
        "id": "384459"
      }
    },
    "renderAttempted": false
  }
]
```

En este punto, puede procesar el contenido de la propuesta como crea conveniente. En este ejemplo, la propuesta que coincide con el `discount` El ámbito es una propuesta del HTML creada con el Compositor de experiencias basadas en formularios de Adobe Target. Suponiendo que tenga un elemento en la página con el ID de `daily-special` y desea procesar el contenido del `discount` propuesta en la `daily-special` , haga lo siguiente:

1. Extraer propuestas de `result` objeto.
1. Recorra en bucle cada propuesta, buscando la propuesta con un ámbito de `discount`.
1. Si encuentra una propuesta, revise cada elemento de la propuesta en busca del elemento que sea contenido del HTML. (Es mejor comprobar que suponer).
1. Si encuentra un elemento con contenido de HTML, busque la variable `daily-special` en la página y reemplace su HTML por el contenido personalizado.
1. Una vez procesado el contenido, envíe un `display` evento.

El código tendría el siguiente aspecto:

```javascript
alloy("sendEvent", {
  xdm: {},
  decisionScopes: ['salutation', 'discount']
}).then(function(result) {
  var propositions = result.propositions;

  var discountProposition;
  if (propositions) {
    // Find the discount proposition, if it exists.
    for (var i = 0; i < propositions.length; i++) {
      var proposition = propositions[i];
      if (proposition.scope === "discount") {
        discountProposition = proposition;
        break;
      }
    }
  }

  var discountHtml;
  if (discountProposition) {
    // Find the item from proposition that should be rendered.
    // Rather than assuming there a single item that has HTML
    // content, find the first item whose schema indicates
    // it contains HTML content.
    for (var j = 0; j < discountProposition.items.length; j++) {
      var discountPropositionItem = discountProposition.items[i];
      if (discountPropositionItem.schema === "https://ns.adobe.com/personalization/html-content-item") {
        discountHtml = discountPropositionItem.data.content;
        // Render the content
        var dailySpecialElement = document.getElementById("daily-special");
        dailySpecialElement.innerHTML = discountHtml;
        
        // For this example, we assume there is only a signle place to update in the HTML.
        break;  
      }
    }
      // Send a "display" event 
    alloy("sendEvent", {
      xdm: {
        eventType: "decisioning.propositionDisplay",
        _experience: {
          decisioning: {
            propositions: [
              {
                id: discountProposition.id,
                scope: discountProposition.scope,
                scopeDetails: discountProposition.scopeDetails
              }
            ]
          }
        }
      }
    });
  }
});
```


>[!TIP]
>
>Si usa Adobe Target, los ámbitos corresponden a mboxes del servidor, excepto que todos se solicitan a la vez en lugar de individualmente. El mbox global siempre se devuelve.

### Administrar parpadeo

El SDK proporciona funciones para lo siguiente [gestionar parpadeo](../personalization/manage-flicker.md) durante el proceso de personalización.

## Procesar propuestas en aplicaciones de una sola página sin incrementar las métricas {#applypropositions}

El `applyPropositions` permite procesar o ejecutar una matriz de propuestas desde [!DNL Target] en aplicaciones de una sola página, sin incrementar el [!DNL Analytics] y [!DNL Target] métricas. Esto aumenta la precisión de los informes.

>[!IMPORTANT]
>
>Si hay propuestas para `__view__` ámbitos (o una superficie web) se procesaban al cargar la página, su `renderAttempted` el indicador se establecerá en `true`. El `applyPropositions` El comando no volverá a procesar el `__view__` propuestas de ámbito (o superficie web) que tienen la variable `renderAttempted: true` Indicador.

### Caso de uso 1: Volver a procesar propuestas de vista de aplicación de una sola página

El caso de uso descrito en el ejemplo siguiente vuelve a procesar las propuestas de vista del carro de compras recuperadas y procesadas anteriormente sin enviar notificaciones de visualización.

En el ejemplo siguiente, la variable `sendEvent` se activa al cambiar la vista y guarda el objeto resultante en una constante.

A continuación, cuando se actualiza la vista o un componente, la variable `applyPropositions` se llama al comando, con las propuestas del anterior `sendEvent` , para volver a procesar las propuestas de vista.

```js
var cartPropositions = alloy("sendEvent", {
    renderDecisions: true,
    xdm: {
        web: {
            webPageDetails: {
                viewName: "cart"
            }
        }
    }
}).then(function(result) {
    var propositions = result.propositions;

    // Collect response tokens, etc.
    return propositions;
});

// Call applyPropositions to re-render the view propositions from the previous sendEvent command.
alloy("applyPropositions", {
    propositions: cartPropositions
});
```

### Caso de uso 2: Procesar propuestas que no tienen selector

Este caso de uso se aplica a las ofertas de actividad creadas con [!DNL Target Form-based Experience Composer].

Debe proporcionar el selector, la acción y el ámbito en la variable `applyPropositions` llamada.

Admitido `actionTypes` son:

* `setHtml`
* `replaceHtml`
* `appendHtml`

```js
// Retrieve propositions for salutation and discount scopes
alloy("sendEvent", {
    decisionScopes: ["salutation", "discount"]
}).then(function(result) {
    var retrievedPropositions = result.propositions;
    // Render propositions on the page by providing additional metadata

    return alloy("applyPropositions", {
        propositions: retrievedPropositions,
        metadata: {
            salutation: {
                selector: "#first-form-based-offer",
                actionType: "setHtml"
            },
            discount: {
                selector: "#second-form-based-offer",
                actionType: "replaceHtml"
            }
        }
    }).then(function(applyPropositionsResult) {
        var renderedPropositions = applyPropositionsResult.propositions;

        // Send the display notifications via sendEvent command
        alloy("sendEvent", {
            xdm: {
                eventType: "decisioning.propositionDisplay",
                _experience: {
                    decisioning: {
                        propositions: renderedPropositions
                    }
                }
            }
        });
    });
});
```

Si no proporciona metadatos para un ámbito de decisión, no se procesarán las propuestas asociadas.
