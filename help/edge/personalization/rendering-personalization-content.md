---
title: Representar contenido personalizado mediante el SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo procesar contenido personalizado con el SDK web de Adobe Experience Platform.
keywords: personalización;renderdecisions;sendEvent;decisionScopes;propositions;
exl-id: 6a3252ca-cdec-48a0-a001-2944ad635805
source-git-commit: c75a8bdeaba67259b5f4b4ce025d5e128d763040
workflow-type: tm+mt
source-wordcount: '962'
ht-degree: 2%

---

# Representar contenido personalizado

El SDK web de Adobe Experience Platform admite la recuperación de contenido personalizado desde soluciones de personalización de Adobe, incluidas [Adobe Target](https://business.adobe.com/es/products/target/adobe-target.html), [offer decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/starting-offer-decisioning.html?lang=es) y [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=es).

Además, el SDK web potencia las capacidades de personalización de la misma página y de la página siguiente a través de destinos de personalización de Adobe Experience Platform, como [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) y [conexión personalizada personalizada](../../destinations/catalog/personalization/custom-personalization.md). Para obtener información sobre cómo configurar Experience Platform para la personalización de la misma página y de la página siguiente, consulte la [guía dedicada](../../destinations/ui/configure-personalization-destinations.md).

Contenido creado en Adobe Target [Compositor de experiencias visuales](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) y Adobe Journey Optimizer [Interfaz de usuario de Web Campaign](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html) el SDK puede recuperarlo y procesarlo automáticamente. Contenido creado en Adobe Target [Compositor de experiencias basadas en formularios](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html) o Offer decisioning no se puede representar automáticamente por el SDK. En su lugar, debe solicitar este contenido mediante el SDK y, a continuación, renderizar el contenido manualmente.

## Procesamiento automático de contenido

Al enviar eventos al servidor, puede establecer la variable `renderDecisions` a `true`. De este modo, el SDK debe procesar automáticamente cualquier contenido personalizado que sea apto para el procesamiento automático.

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

El renderizado de contenido personalizado es asíncrono, por lo que no debe realizar suposiciones sobre cuándo un fragmento de contenido en particular habrá completado el renderizado.

## Representación manual de contenido

Para acceder a cualquier contenido de personalización, puede proporcionar una función de llamada de retorno que se llamará después de que el SDK reciba una respuesta correcta del servidor. La devolución de llamada se proporciona como `result` que puede contener un `propositions` que contenga cualquier contenido de personalización devuelto. A continuación, se muestra un ejemplo de cómo proporcionaría una función de llamada de retorno al enviar un evento.

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

La variable `propositions` puede tener un aspecto similar al de este ejemplo:

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

En el ejemplo, la variable `renderDecisions` no se ha definido como `true` cuando la variable `sendEvent` se ejecutó, por lo que el SDK no intentó procesar ningún contenido automáticamente. Sin embargo, el SDK sigue recuperando automáticamente el contenido apto para el procesamiento automático y se lo ha proporcionado para que lo procese manualmente si desea hacerlo. Observe que cada objeto de propuesta tiene su `renderAttempted` propiedad establecida en `false`.

Si en su lugar hubiera configurado la variable `renderDecisions` a `true` al enviar el evento, el SDK habría intentado procesar cualquier propuesta que fuera apta para el procesamiento automático (como se describió anteriormente). Como consecuencia, cada uno de los objetos de propuesta tendría su `renderAttempted` propiedad establecida en `true`. En este caso, no sería necesario procesar manualmente estas propuestas.

Hasta ahora, solo hemos hablado del contenido de personalización que se puede procesar automáticamente (es decir, cualquier contenido creado en el Compositor de experiencias visuales de Adobe Target o en la interfaz de usuario de Adobe Journey Optimizer Web Campaign). Para recuperar cualquier contenido personalizado _not_ apto para el procesamiento automático, debe solicitar el contenido rellenando la variable `decisionScopes` al enviar el evento. Un ámbito es una cadena que identifica una propuesta concreta que desea recuperar del servidor.

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

En este ejemplo, si se encuentran propuestas en el servidor que coinciden con la variable `salutation` o `discount` , se devuelven y se incluyen en la variable `result.propositions` matriz. Tenga en cuenta que las propuestas que califiquen para el procesamiento automático se seguirán incluyendo en la variable `propositions` matriz, independientemente de cómo configure `renderDecisions` o `decisionScopes` opciones. La variable `propositions` array, en este caso, tendría un aspecto similar al de este ejemplo:

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

En este punto, puede procesar el contenido de la propuesta como desee. En este ejemplo, la propuesta que coincide con la variable `discount` scope es una propuesta de HTML creada con el Compositor de experiencias basadas en formularios de Adobe Target. Suponiendo que tiene un elemento en la página con el ID de `daily-special` y desea renderizar el contenido de `discount` en la variable `daily-special` haga lo siguiente:

1. Extraer propuestas de `result` objeto.
1. Bucle por cada propuesta, buscando la propuesta con un alcance de `discount`.
1. Si encuentra una propuesta, realice un bucle por cada elemento de la propuesta, buscando el elemento que sea contenido HTML. (Es mejor comprobarlo que asumir).
1. Si encuentra un elemento que contenga contenido de HTML, busque la variable `daily-special` en la página y reemplace su HTML por el contenido personalizado.
1. Una vez representado el contenido, envíe un `display` evento.

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
>Si usa Adobe Target, los ámbitos se corresponden con los mboxes del servidor, excepto que todos se solicitan a la vez en lugar de individualmente. El mbox global siempre se devuelve.

### Administrar parpadeo

El SDK proporciona instalaciones para [administrar parpadeo](../personalization/manage-flicker.md) durante el proceso de personalización.

## Procesar propuestas en aplicaciones de una sola página sin incrementar las métricas {#applypropositions}

La variable `applyPropositions` permite procesar o ejecutar una matriz de propuestas de [!DNL Target] en aplicaciones de una sola página, sin incrementar el [!DNL Analytics] y [!DNL Target] métricas. Esto aumenta la precisión de los informes.

>[!IMPORTANT]
>
>Si las propuestas para la variable `__view__` el ámbito (o una superficie web) se representaba al cargar la página, sus `renderAttempted` el indicador se establecerá en `true`. La variable `applyPropositions` no vuelve a procesar el `__view__` propuestas de ámbito (o superficie web) que tengan la variable `renderAttempted: true` indicador.

### Caso de uso 1: Volver a procesar propuestas de vista de aplicación de una sola página

El caso de uso descrito en el ejemplo siguiente vuelve a procesar las propuestas de vista del carro recuperadas anteriormente y procesadas sin enviar notificaciones de visualización.

En el ejemplo siguiente, la variable `sendEvent` se activa tras un cambio de vista y guarda el objeto resultante en una constante.

A continuación, cuando se actualiza la vista o un componente, la variable `applyPropositions` se llama al comando , con las propuestas del anterior `sendEvent` para volver a procesar las propuestas de vista.

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

### Caso de uso 2: Representar propuestas que no tengan un selector

Este caso de uso se aplica a las ofertas de actividad creadas con el [!DNL Target Form-based Experience Composer].

Debe proporcionar el selector, la acción y el ámbito en la variable `applyPropositions` llamada a .

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
