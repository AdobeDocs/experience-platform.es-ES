---
title: Tipos de eventos en la extensión SDK para web de Adobe Experience Platform
description: Obtenga información acerca de cómo utilizar los tipos de eventos proporcionados por la extensión SDK para web de Adobe Experience Platform en Adobe Experience Platform Launch.
solution: Experience Platform
exl-id: b3162406-c5ce-42ec-ab01-af8ac8c63560
source-git-commit: b37bf09e3ec16f29d6acee3bca71463fa2c876ce
workflow-type: tm+mt
source-wordcount: '1490'
ht-degree: 0%

---

# Tipos de eventos

En esta página se describen los tipos de eventos de Adobe Experience Platform que proporciona la extensión de etiquetas de SDK web de Adobe Experience Platform. Se usan para [generar reglas](https://experienceleague.adobe.com/docs/platform-learn/data-collection/tags/build-rules.html?lang=es) y no deben confundirse con el campo `eventType` en el objeto [`xdm`](/help/web-sdk/commands/sendevent/xdm.md).

## Enlace de monitorización activado {#monitoring-hook-triggered}

El SDK web de Adobe Experience Platform incluye vínculos de monitorización que puede utilizar para monitorizar varios eventos del sistema. Estas herramientas son útiles para desarrollar sus propias herramientas de depuración y capturar registros del SDK web.

Para obtener información detallada acerca de los parámetros que contiene cada evento de vínculo de supervisión, consulte la [documentación sobre los vínculos de supervisión del SDK web](../../../../web-sdk/monitoring-hooks.md).

![Imagen de la interfaz de usuario de etiquetas que muestra el tipo de evento del vínculo de monitorización](assets/monitoring-hook-triggered.png)

La extensión de etiqueta del SDK web admite los siguientes vínculos de monitorización:

* **[!UICONTROL onInstanceCreated]**: este evento de vínculo de supervisión se activa cuando se crea correctamente una nueva instancia del SDK web.
* **[!UICONTROL onInstanceConficonfigured]**: el SDK web activa este evento de vínculo de supervisión cuando el comando [`configure`](../../../../web-sdk/commands/configure/overview.md) se resuelve correctamente
* **[!UICONTROL onBeforeCommand]**: el SDK web activa este evento de vínculo de supervisión antes de ejecutar cualquier otro comando. Puede utilizar este vínculo de monitorización para recuperar las opciones de configuración de un comando específico.
* **[!UICONTROL onCommandResolved]**: este evento de vínculo de supervisión se activa antes de resolver la promesa de comando. Puede utilizar esta función para ver las opciones y el resultado del comando.
* **[!UICONTROL onCommandRejected]**: este evento de vínculo de supervisión se activa cuando se rechaza una promesa de comando y contiene información sobre la causa del error.
* **[!UICONTROL onBeforeNetworkRequest]**: este evento de vínculo de supervisión se activa antes de que se ejecute una solicitud de red.
* **[!UICONTROL onNetworkResponse]**: este evento de vínculo de supervisión se activa cuando el explorador recibe una respuesta.
* **[!UICONTROL onNetworkError]**: este evento de vínculo de supervisión se activa cuando falla la solicitud de red.
* **[!UICONTROL onBeforeLog]**: este evento de vínculo de supervisión se activa antes de que el SDK web registre algo en la consola.
* **[!UICONTROL onContentRendering]**: este evento de vínculo de supervisión se activa mediante el componente `personalization` y le ayuda a depurar la representación del contenido de personalización. Este evento puede tener diferentes estados:
   * `rendering-started`: indica que el SDK web está a punto de procesar propuestas. Antes de que el SDK web empiece a procesar una vista o un ámbito de decisión, en el objeto `data` puede ver las propuestas que están a punto de ser representadas por el componente `personalization` y el nombre del ámbito.
   * `no-offers`: indica que no se recibió carga útil para los parámetros solicitados.
   * `rendering-failed`: indica que el SDK web no pudo procesar una propuesta.
   * `rendering-succeeded`: indica que se ha completado el procesamiento para un ámbito de decisión.
   * `rendering-redirect`: indica que el SDK web ejecutará una propuesta de redirección.
* **[!UICONTROL onContentHiding]**: este evento de vínculo de supervisión se activa cuando se aplica o se quita un estilo de ocultamiento previo.


## [!UICONTROL Enviar evento completado]

Normalmente, su propiedad tendría una o más reglas que usarían la acción [[!UICONTROL Enviar evento]](action-types.md#send-event) para enviar eventos al Edge Network de Adobe Experience Platform. Cada vez que se envía un evento al Edge Network, se devuelve una respuesta al explorador con datos útiles. Sin el tipo de evento [!UICONTROL Enviar evento completado], no tendría acceso a estos datos devueltos.

Para obtener acceso a los datos devueltos, cree una regla independiente y luego agregue un evento [!UICONTROL Enviar evento completado] a la regla. Esta regla se activa cada vez que se recibe una respuesta correcta del servidor como resultado de una acción [!UICONTROL Enviar evento].

Cuando un evento [!UICONTROL Enviar evento completado] déclencheur una regla, proporciona datos devueltos por el servidor que pueden ser útiles para realizar ciertas tareas. Normalmente, agregará una acción [!UICONTROL Custom Code] (de la extensión [!UICONTROL Core]) a la misma regla que contiene el evento [!UICONTROL Enviar evento completado]. En la acción [!UICONTROL Custom Code], su Custom Code tendrá acceso a una variable denominada `event`. Esta variable `event` contendrá los datos devueltos por el servidor.

La regla para administrar los datos devueltos por Edge Network puede tener un aspecto similar al siguiente:

![](assets/send-event-complete.png)

A continuación se muestran algunos ejemplos de cómo realizar ciertas tareas utilizando la acción [!UICONTROL Custom Code] en esta regla.

### Procesar manualmente contenido personalizado

En la acción Custom Code, que se encuentra en la regla para administrar los datos de respuesta, puede acceder a las propuestas de personalización que se devolvieron desde el servidor. Para ello, debe escribir el siguiente código personalizado:

```javascript
var propositions = event.propositions;
```

Si `event.propositions` existe, es una matriz que contiene objetos de propuesta de personalización. Las propuestas incluidas en la matriz están determinadas, en gran parte, por la forma en que se envió el evento al servidor.

Para este primer escenario, suponga que no ha marcado la casilla de verificación [!UICONTROL Procesar decisiones] y no ha proporcionado ningún [!UICONTROL ámbito de decisión] dentro de la acción [!UICONTROL Enviar evento] responsable de enviar el evento.

![img.png](assets/send-event-render-unchecked-without-scopes.png)

En este ejemplo, la matriz `propositions` solo contiene propuestas relacionadas con el evento que cumplen los requisitos para la representación automática.

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

Al enviar el evento, la casilla de verificación [!UICONTROL Procesar decisiones] no estaba marcada, por lo que el SDK no intentó procesar automáticamente ningún contenido. Sin embargo, el SDK recuperó automáticamente el contenido apto para el procesamiento automático y le proporcionó el procesamiento manual si así lo desea. Observe que cada objeto de propuesta tiene su propiedad `renderAttempted` establecida en `false`.

Si, en su lugar, hubiera marcado la casilla de verificación [!UICONTROL Decisiones de procesamiento] al enviar el evento, el SDK habría intentado procesar todas las propuestas que cumplen los requisitos para el procesamiento automático. Como consecuencia, cada uno de los objetos de la propuesta tendría su propiedad `renderAttempted` establecida en `true`. No sería necesario procesar manualmente estas propuestas en este caso.

Hasta ahora, solo ha visto el contenido de personalización que puede procesarse automáticamente (por ejemplo, cualquier contenido creado en el Compositor de experiencias visuales de Adobe Target). Para recuperar cualquier contenido de personalización _que no sea_ apto para el procesamiento automático, solicite el contenido proporcionando ámbitos de decisión utilizando el campo [!UICONTROL ámbitos de decisión] en la acción [!UICONTROL Enviar evento]. Un ámbito es una cadena que identifica una propuesta concreta que desea recuperar del servidor.

La acción [!UICONTROL Enviar evento] tendría el siguiente aspecto:

![img.png](assets/send-event-render-unchecked-with-scopes.png)

En este ejemplo, si las propuestas se encuentran en el servidor que coincide con el ámbito `salutation` o `discount`, se devuelven y se incluyen en la matriz `propositions`. Tenga en cuenta que las propuestas que cumplen los requisitos para el procesamiento automático se seguirán incluyendo en la matriz `propositions`, independientemente de cómo configure los campos [!UICONTROL Decisiones de procesamiento] o [!UICONTROL Ámbitos de decisión] en la acción [!UICONTROL Enviar evento]. La matriz `propositions`, en este caso, tendría un aspecto similar al de este ejemplo:

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

En este punto, puede procesar el contenido de la propuesta como crea conveniente. En este ejemplo, la propuesta que coincide con el ámbito `discount` es una propuesta de HTML creada con el Compositor de experiencias basadas en formularios de Adobe Target. Supongamos que tiene un elemento en la página con el identificador `daily-special` y que desea procesar el contenido de la propuesta `discount` en el elemento `daily-special`. Haga lo siguiente:

1. Extraer propuestas del objeto `event`.
1. Recorra en bucle cada propuesta, buscando la propuesta con un ámbito de `discount`.
1. Si encuentra una propuesta, revise cada elemento de la propuesta en busca del elemento que sea contenido del HTML. (Es mejor comprobar que suponer).
1. Si encuentra un elemento con contenido de HTML, busque el elemento `daily-special` en la página y reemplace su HTML por el contenido personalizado.

Su código personalizado en la acción [!UICONTROL Custom code] puede aparecer de la siguiente manera:

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

### Acceso a tokens de respuesta de Adobe Target

El contenido de Personalization devuelto desde Adobe Target incluye [tokens de respuesta](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html), que son detalles acerca de la actividad, oferta, experiencia, perfil de usuario, información geográfica y más. Estos detalles se pueden compartir con herramientas de terceros o utilizar para la depuración. Los tokens de respuesta se pueden configurar en la interfaz de usuario de Adobe Target.

En la acción Custom Code, que se encuentra en la regla para administrar los datos de respuesta, puede acceder a las propuestas de personalización que se devolvieron desde el servidor. Para ello, escriba el siguiente código personalizado:

```javascript
var propositions = event.propositions;
```

Si `event.propositions` existe, es una matriz que contiene objetos de propuesta de personalización. Consulte [Procesar manualmente contenido personalizado](#manually-render-personalized-content) para obtener más información sobre el contenido de `result.propositions`.

Supongamos que desea recopilar todos los nombres de las actividades de todas las propuestas que el SDK web procesó automáticamente e insertarlos en una sola matriz. A continuación, puede enviar la matriz única a un tercero. En este caso, escriba el código personalizado dentro de la acción [!UICONTROL Custom Code] para:

1. Extraer propuestas del objeto `event`.
1. Recorra en bucle cada propuesta.
1. Determine si el SDK procesó la propuesta.
1. Si es así, realice un bucle en cada elemento de la propuesta.
1. Recupere el nombre de la actividad de la propiedad `meta`, que es un objeto que contiene tokens de respuesta.
1. Inserte el nombre de la actividad en una matriz.
1. Envíe los nombres de las actividades a un tercero.

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

## [!UICONTROL Suscribir elementos del conjunto de reglas] {#subscribe-ruleset-items}

El tipo de evento **[!UICONTROL Suscribir elementos del conjunto de reglas]** le permite suscribirse a tarjetas de contenido de Adobe Journey Optimizer para una superficie. Cada vez que se evalúan los conjuntos de reglas, la llamada de retorno proporcionada a este comando recibe un objeto result con propuestas que contienen los datos de la tarjeta de contenido.

![Imagen de la interfaz de usuario de etiquetas de Experience Platform que muestra el tipo de evento Suscribir elementos de conjunto de reglas.](assets/subscribe-ruleset-items.png)

Este tipo de evento admite las siguientes propiedades configurables:

* **[!UICONTROL Esquemas]**: una matriz de esquemas a los que desea suscribirse para las tarjetas de contenido. Puede introducir los esquemas manualmente o proporcionando un elemento de datos.
* **[!UICONTROL Superficies]**: Matriz de superficies a las que desea suscribirse a tarjetas de contenido. Puede introducir las superficies manualmente o proporcionando un elemento de datos.
