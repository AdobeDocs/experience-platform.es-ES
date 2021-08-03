---
title: Representar contenido personalizado mediante el SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo procesar contenido personalizado con el SDK web de Adobe Experience Platform.
keywords: personalización;renderdecisions;sendEvent;decisionScopes;propositions;
exl-id: 6a3252ca-cdec-48a0-a001-2944ad635805
source-git-commit: 5ae7488e715ff97d2b667c40505b79433eb74f49
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 1%

---

# Representar contenido personalizado

El SDK web de Adobe Experience Platform admite la recuperación de contenido personalizado de soluciones de personalización en el Adobe, incluidas [Adobe Target](https://business.adobe.com/products/target/adobe-target.html) y [Offer decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/starting-offer-decisioning.html?lang=es). El SDK puede recuperar y representar automáticamente el contenido creado en el [Compositor de experiencias visuales](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) de Adobe Target. El SDK no puede representar automáticamente el contenido creado en el [Compositor de experiencias basadas en formularios](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html) o Offer decisioning de Adobe Target. En su lugar, debe solicitar este contenido mediante el SDK y, a continuación, renderizar el contenido manualmente.

## Procesamiento automático de contenido

Al enviar eventos al servidor, puede establecer la opción `renderDecisions` en `true`. De este modo, el SDK debe procesar automáticamente cualquier contenido personalizado que sea apto para el procesamiento automático.

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

Para acceder a cualquier contenido de personalización, puede proporcionar una función de llamada de retorno que se llamará después de que el SDK reciba una respuesta correcta del servidor. Se proporciona un objeto `result` a la rellamada, que puede contener una propiedad `propositions` que contenga cualquier contenido de personalización devuelto. A continuación, se muestra un ejemplo de cómo proporcionaría una función de llamada de retorno al enviar un evento.

```javascript
alloy("sendEvent", {
    xdm: {}
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions
    }
  });
```

En este ejemplo, `result.propositions`, si existe, es una matriz que contiene propuestas de personalización relacionadas con el evento. De forma predeterminada, solo incluye propuestas que pueden procesarse automáticamente.

La matriz `propositions` puede tener un aspecto similar al de este ejemplo:

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
    "renderAttempted": false
  }
]
```

En el ejemplo, la opción `renderDecisions` no se estableció en `true` cuando se ejecutó el comando `sendEvent`, por lo que el SDK no intentó procesar automáticamente ningún contenido. Sin embargo, el SDK aún recupera automáticamente el contenido apto para el procesamiento automático y se lo ha proporcionado para que lo procese manualmente si desea hacerlo. Observe que cada objeto de propuesta tiene su propiedad `renderAttempted` establecida en `false`.

Si, en su lugar, hubiera establecido la opción `renderDecisions` en `true` al enviar el evento, el SDK habría intentado procesar todas las propuestas aptas para el procesamiento automático (como se describió anteriormente). Como consecuencia, cada uno de los objetos de propuesta tendría su propiedad `renderAttempted` establecida en `true`. En este caso, no sería necesario procesar manualmente estas propuestas.

Hasta ahora, solo hemos hablado del contenido de personalización que se puede procesar automáticamente (es decir, cualquier contenido creado en el Compositor de experiencias visuales de Adobe Target). Para recuperar cualquier contenido de personalización _no_ apto para el procesamiento automático, debe solicitar el contenido rellenando la opción `decisionScopes` al enviar el evento. Un ámbito es una cadena que identifica una propuesta concreta que desea recuperar del servidor.

Vea el siguiente ejemplo:

```javascript
alloy("sendEvent", {
    xdm: {},
    decisionScopes: ['salutation', 'discount']
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions
    }
  });
```

En este ejemplo, si las propuestas se encuentran en el servidor que coincide con el ámbito `salutation` o `discount`, se devuelven y se incluyen en la matriz `result.propositions`. Tenga en cuenta que las propuestas que califiquen para procesamiento automático se seguirán incluyendo en la matriz `propositions` , independientemente de cómo configure las opciones `renderDecisions` o `decisionScopes` . La matriz `propositions`, en este caso, tendría un aspecto similar a este ejemplo:

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
    "renderAttempted": false
  }
]
```

En este punto, puede procesar el contenido de la propuesta como desee. En este ejemplo, la propuesta que coincide con el ámbito `discount` es una propuesta HTML creada con el Compositor de experiencias basadas en formularios de Adobe Target. Suponiendo que tiene un elemento en la página con el ID de `daily-special` y desea procesar el contenido de la propuesta `discount` en el elemento `daily-special`, haga lo siguiente:

1. Extraiga propuestas del objeto `result`.
1. Bucle por cada propuesta, buscando la propuesta con un alcance de `discount`.
1. Si encuentra una propuesta, realice un bucle por cada elemento de la propuesta, buscando el elemento que sea contenido HTML. (Es mejor comprobarlo que asumir).
1. Si encuentra un elemento que contenga contenido HTML, busque el elemento `daily-special` en la página y reemplace su HTML por el contenido personalizado.

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
        break;
      }
    }
  }

  if (discountHtml) {
    // Discount HTML exists. Time to render it.
    var dailySpecialElement = document.getElementById("daily-special");
    dailySpecialElement.innerHTML = discountHtml;
  }
});
```


>[!TIP]
>
>Si usa Adobe Target, los ámbitos se corresponden con los mboxes del servidor, excepto que todos se solicitan a la vez en lugar de individualmente. El mbox global siempre se devuelve.

### Administrar parpadeo

El SDK proporciona funciones para [administrar el parpadeo](../personalization/manage-flicker.md) durante el proceso de personalización.
