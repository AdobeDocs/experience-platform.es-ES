---
title: subscribeRulesetItems
description: Suscríbase a las tarjetas de contenido de una superficie específica mediante el comando subscribeRulesetItems.
exl-id: bc932ba5-a810-4fa6-82cc-998af39fdd34
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 3%

---

# `subscribeRulesetItems`

El comando `subscribeRulesetItems` le permite suscribirse a propuestas que son el resultado de conjuntos de reglas satisfechos. Para ello, especifique por qué superficies y esquemas filtrar y proporcione una función de llamada de retorno.

Cada vez que se evalúan los conjuntos de reglas, la función de devolución de llamada recibe un objeto `result` con una matriz de propuestas.

>[!IMPORTANT]
>
>El comando `subscribeRulesetItems` es la única manera de obtener propuestas que provienen de conjuntos de reglas, ya que no se devuelven junto con [`sendEvent`](sendevent/overview.md) resultados.


```js
alloy("subscribeRulesetItems", {
  surfaces: ["web://example.com/#welcome"],
  schemas: ["https://ns.adobe.com/personalization/message/content-card"],
  callback: (result, collectEvent) => {
    const { propositions = [] } = result;
    renderMyPropositions(propositions);
    collectEvent("display", propositions);    
  },
});
```

El código anterior se suscribe a la superficie `web://example.com/#welcome` para las tarjetas de contenido y utiliza el método de conveniencia `collectEvent` para emitir eventos `display` para todas las propuestas.

## Opciones de comando {#command-options}

Este comando toma un objeto `options` con las siguientes propiedades:

| Propiedad | Tipo | Descripción |
| --- | --- | --- |
| `surfaces` | Matriz de cadenas | Una lista de superficies. La función de llamada de retorno solo recibirá las propuestas que coincidan con una de las superficies proporcionadas aquí. |
| `schemas` | Matriz de cadenas | Una lista de esquemas. La función de llamada de retorno solo recibirá las propuestas que coincidan con uno de los esquemas proporcionados aquí. |
| `callback` | Función | Una función de llamada de retorno que se invocará cuando las propuestas sean el resultado de conjuntos de reglas satisfechos. La función de devolución de llamada recibe dos parámetros cuando se invoca: `result` y `collectEvent`. Consulte [parámetros de devolución de llamada](#callback-parameters) para obtener detalles. |

### Parámetros de devolución de llamada {#callback-parameters}

La función de llamada de retorno recibe los dos parámetros descritos en la tabla siguiente cuando se invoca.

| Parámetro | Tipo | Descripción |
| --- | --- | --- |
| `result` | Objeto | Este objeto contiene una matriz `propositions`.  Estas propuestas son el resultado directo de conjuntos de reglas satisfechos. El objeto `result` tiene la misma estructura que el objeto [result](command-responses.md) devuelto por `sendEvent` mediante una cláusula `then`. |
| `collectEvent` | Función | Una función de conveniencia que puede utilizar para enviar eventos de Edge Network para rastrear interacciones, visualizaciones y otros eventos. |

### Función `collectEvent` {#collectevent-function}

La función `collectEvent` es una función de conveniencia que puede utilizar para enviar eventos de Edge Network con el fin de realizar un seguimiento de interacciones, visualizaciones y otros eventos. Acepta los dos parámetros descritos en la tabla siguiente.

| Parámetro | Tipo | Descripción |
| --- | --- | --- |
| Tipo de evento | Cadena | Cadena que indica qué tipo de evento de propuesta se va a emitir. Los tipos de eventos admitidos son `display`, `interact` o `dismiss`. |
| `propositions` | Matriz | Una matriz de propuestas correspondientes al evento. |

## Suscripción a tarjetas de contenido mediante la extensión de etiquetas Web SDK

La extensión de etiquetas Web SDK equivalente a respuestas de comandos es una regla que se suscribe al evento [**[!UICONTROL Subscribe ruleset items]**](/help/tags/extensions/client/web-sdk/event-types.md#subscribe-ruleset-items). El evento permite proporcionar los esquemas y las superficies deseados.
