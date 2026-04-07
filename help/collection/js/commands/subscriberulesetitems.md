---
title: subscribeRulesetItems
description: Suscríbase a las tarjetas de contenido de una superficie específica mediante el comando subscribeRulesetItems.
exl-id: bc932ba5-a810-4fa6-82cc-998af39fdd34
source-git-commit: 3ecfc2258e63a34a739ab8b296437c357d1dd9d1
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 3%

---

# `subscribeRulesetItems`

El comando `subscribeRulesetItems` le permite suscribirse a propuestas que son el resultado de conjuntos de reglas satisfechos. Para ello, especifique por qué superficies y esquemas filtrar y proporcione una función de llamada de retorno.

Los conjuntos de reglas se evalúan cada vez que se envía un comando [`sendEvent`](sendevent/overview.md). La función de devolución de llamada recibe un objeto `result` con una matriz de propuestas.

>[!IMPORTANT]
>
>El comando `subscribeRulesetItems` es la única manera de obtener propuestas que provienen de conjuntos de reglas, ya que no se devuelven junto con [`sendEvent`](sendevent/overview.md) resultados. Debe configurar su suscripción antes de llamar a `sendEvent` para asegurarse de que se capturan las propuestas.


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
| `callback` | Función | Una función de llamada de retorno que se invoca cuando las propuestas son el resultado de conjuntos de reglas satisfechos. La función de devolución de llamada recibe dos parámetros cuando se invoca: `result` y `collectEvent`. Consulte [parámetros de devolución de llamada](#callback-parameters) para obtener detalles. |

>[!TIP]
>
>Puede suscribirse a varias superficies y esquemas en un único comando pasando valores adicionales a las matrices `surfaces` y `schemas`.

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


Se puede llamar a la función `collectEvent` de forma independiente fuera de la llamada de retorno. Llamar a esta función es útil cuando se rastrea una interacción o se descarta en un momento posterior, como en respuesta a una acción del usuario.

```js
collectEvent("interact", propositions);
```

## Suscripción a tarjetas de contenido mediante la extensión de etiquetas Web SDK

La extensión de etiquetas Web SDK equivalente a respuestas de comandos es una regla que se suscribe al evento [**[!UICONTROL Subscribe ruleset items]**](/help/tags/extensions/client/web-sdk/event-types.md#subscribe-ruleset-items). El evento permite proporcionar los esquemas y las superficies deseados.
