---
title: Tipos de eventos en la extensión del SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo utilizar los tipos de eventos proporcionados por la extensión web SDK de Adobe Experience Platform en Adobe Experience Platform Launch.
solution: Experience Platform
feature: Web SDK
exl-id: b3162406-c5ce-42ec-ab01-af8ac8c63560
source-git-commit: 8f714933e23e281772cd8633d27096021de14c56
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 1%

---

# Tipos de eventos

En esta página se describen los tipos de eventos de Adobe Experience Platform proporcionados por la extensión de etiqueta SDK web de Adobe Experience Platform. Se utilizan para [generar reglas](https://experienceleague.adobe.com/docs/platform-learn/data-collection/tags/build-rules.html) y no se deben confundir con el campo [`eventType` en XDM](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=es).

## [!UICONTROL Enviar evento finalizado]

Normalmente, su propiedad tendría una o más reglas usando la acción [[!UICONTROL Send event]](action-types.md#send-event) para enviar eventos a Adobe Experience Platform Edge Network. Cada vez que se envía un evento a la red perimetral, se devuelve una respuesta al explorador con datos útiles. Sin el tipo de evento [!UICONTROL Send event complete], no tendría acceso a los datos devueltos.

Para acceder a los datos devueltos, cree una regla independiente y añada un evento [!UICONTROL Send event complete] a la regla. Esta regla se activa cada vez que se recibe una respuesta correcta del servidor como resultado de una acción [!UICONTROL Send event].

Cuando un evento [!UICONTROL Send event complete] déclencheur una regla, proporciona datos devueltos por el servidor que pueden resultar útiles para realizar ciertas tareas. Normalmente, se agrega una acción [!UICONTROL Custom code] (de la extensión [!UICONTROL Core]) a la misma regla que contiene el evento [!UICONTROL Send event complete]. En la acción [!UICONTROL Custom code] , el código personalizado tendrá acceso a una variable denominada `event`. Esta variable `event` contiene los datos devueltos por el servidor.

La regla para administrar los datos devueltos por la red perimetral puede tener este aspecto:

![](./assets/send-event-complete.png)

A continuación se muestran algunos ejemplos de cómo realizar determinadas tareas utilizando la acción [!UICONTROL Custom code] en esta regla.

### Representar contenido personalizado manualmente

En la acción Código personalizado , que se encuentra en la regla para administrar los datos de respuesta, puede acceder a las propuestas de personalización que se devolvieron desde el servidor. Para ello, debe escribir el siguiente código personalizado:

```javascript
var propositions = event.propositions;
```

Si existe `event.propositions`, es una matriz que contiene objetos de propuesta de personalización. Las propuestas incluidas en la matriz están determinadas, en gran parte, por la forma en que se envió el evento al servidor.

En este primer escenario, supongamos que no ha marcado la casilla [!UICONTROL Render decisions] y no ha proporcionado ningún [!UICONTROL ámbito de decisión] dentro de la acción [!UICONTROL Send event] responsable de enviar el evento.

![img.png](assets/send-event-render-unchecked-without-scopes.png)

En este ejemplo, la matriz `propositions` solo contiene propuestas relacionadas con el evento que pueden procesarse automáticamente.

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

Al enviar el evento, la casilla de verificación [!UICONTROL Render decisions] no estaba marcada, por lo que el SDK no intentó procesar ningún contenido automáticamente. Sin embargo, el SDK aún recupera automáticamente el contenido apto para el procesamiento automático y se lo ha proporcionado para que lo procese manualmente si desea hacerlo. Observe que cada objeto de propuesta tiene su propiedad `renderAttempted` establecida en `false`.

Si en su lugar hubiera marcado la casilla [!UICONTROL Render decisions] al enviar el evento, el SDK habría intentado procesar cualquier propuesta que fuera apta para el procesamiento automático. Como consecuencia, cada uno de los objetos de propuesta tendría su propiedad `renderAttempted` establecida en `true`. En este caso, no sería necesario procesar manualmente estas propuestas.

Hasta ahora, solo ha observado el contenido de personalización que se puede procesar automáticamente (por ejemplo, cualquier contenido creado en el Compositor de experiencias visuales de Adobe Target). Para recuperar cualquier contenido de personalización _no_ apto para procesamiento automático, solicite el contenido proporcionando ámbitos de decisión utilizando el campo [!UICONTROL Decissscopios] en la acción [!UICONTROL Send event]. Un ámbito es una cadena que identifica una propuesta concreta que desea recuperar del servidor.

La acción [!UICONTROL Send event] tendría el siguiente aspecto:

![img.png](assets/send-event-render-unchecked-with-scopes.png)

En este ejemplo, si las propuestas se encuentran en el servidor que coincide con el ámbito `salutation` o `discount`, se devuelven y se incluyen en la matriz `propositions`. Tenga en cuenta que las propuestas que cumplen los requisitos para el procesamiento automático se seguirán incluyendo en la matriz `propositions`, independientemente de cómo configure los campos [!UICONTROL Render decisions] o [!UICONTROL Decidir ámbitos] en la acción [!UICONTROL Enviar evento]. La matriz `propositions`, en este caso, tendría un aspecto similar a este ejemplo:

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

En este punto, puede procesar el contenido de la propuesta como desee. En este ejemplo, la propuesta que coincide con el ámbito `discount` es una propuesta de HTML creada con el Compositor de experiencias basadas en formularios de Adobe Target. Supongamos que tiene un elemento en la página con el ID de `daily-special` y desea procesar el contenido de la propuesta `discount` en el elemento `daily-special`. Haga lo siguiente:

1. Extraiga propuestas del objeto `event`.
1. Bucle por cada propuesta, buscando la propuesta con un alcance de `discount`.
1. Si encuentra una propuesta, realice un bucle por cada elemento de la propuesta, buscando el elemento que sea contenido HTML. (Es mejor comprobarlo que asumir).
1. Si encuentra un elemento que contenga contenido de HTML, busque el elemento `daily-special` en la página y reemplace su HTML por el contenido personalizado.

El código personalizado dentro de la acción [!UICONTROL Custom Code] puede aparecer de la siguiente manera:

```javascript
var propositions = event.propositions;

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
```

### Acceso a los tokens de respuesta de Adobe Target

El contenido de personalización que Adobe Target devuelve incluye [tokens de respuesta](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html), que son detalles sobre la actividad, la oferta, la experiencia, el perfil de usuario, la información geográfica y mucho más. Estos detalles se pueden compartir con herramientas de terceros o utilizar para la depuración. Los tokens de respuesta se pueden configurar en la interfaz de usuario de Adobe Target.

En la acción Código personalizado , que se encuentra en la regla para administrar los datos de respuesta, puede acceder a las propuestas de personalización que se devolvieron desde el servidor. Para ello, escriba el siguiente código personalizado:

```javascript
var propositions = event.propositions;
```

Si existe `event.propositions`, es una matriz que contiene objetos de propuesta de personalización. Consulte [Renderización manual de contenido personalizado](#manually-render-personalized-content) para obtener más información sobre el contenido de `result.propositions`.

Supongamos que desea recopilar todos los nombres de actividad de todas las propuestas que el SDK web ha procesado automáticamente y colocarlos en una única matriz. Luego puede enviar la matriz única a un tercero. En este caso, escriba el código personalizado dentro de la acción [!UICONTROL Custom Code] para:

1. Extraiga propuestas del objeto `event`.
1. Bucle por cada propuesta.
1. Determine si el SDK procesó la propuesta.
1. Si es así, realice un bucle por cada elemento de la propuesta.
1. Recupere el nombre de la actividad desde la propiedad `meta` , que es un objeto que contiene tokens de respuesta.
1. Inserte el nombre de la actividad en una matriz.
1. Envíe los nombres de la actividad a un tercero.

```javascript
var propositions = event.propositions;
if (propositions) {
  var activityNames = [];
  propositions.forEach(function(proposition) {
    if (proposition.renderAttempted) {
      proposition.items.forEach(function(item) {
        if (item.meta) {
          // item.meta contains the response tokens.
          var activityName = item.meta["activity.name"];
          // Ignore duplicates
          if (activityNames.indexOf(activityName) === -1) {
            activityNames.push(activityName);  
          }
        }
      });
    }
  });
  // Now that activity names are in an array,
  // you can send them to a third party or use
  // them in some other way.
}
```
