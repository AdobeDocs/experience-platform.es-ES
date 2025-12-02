---
title: _monitores
description: Agregue detectores de eventos para depurar la implementación de etiquetas.
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 1%

---

# `_monitors`

El objeto `_satellite._monitors` le permite crear detectores de eventos y ejecutar código personalizado cuando la biblioteca detecta una regla desencadenada. Su uso principal es ayudar a depurar la implementación para garantizar que las reglas se ajusten correctamente al déclencheur.

>[!IMPORTANT]
>
>Este objeto solo se utiliza con fines de depuración. No ate la lógica de producción a este objeto. Adobe puede cambiar la disponibilidad de propiedades o nombres dentro de este objeto en cualquier momento.

```ts
_satellite._monitors?: {
  ruleTriggered(event: { rule: Rule }): void;
  ruleCompleted(event: { rule: Rule }): void;
  ruleConditionFailed(event: { rule: Rule; condition: Condition }): void;
}[];
```

Puede escuchar los siguientes tipos de eventos:

## `ruleTriggered`

Esta función de llamada de retorno se activa cuando un evento almacena en déclencheur una regla antes de que se hayan procesado las condiciones y acciones de la regla. Si esta función presenta un déclencheur, `ruleCompleted` o `ruleConditionFailed` déclencheur poco después (se excluyen mutuamente).

## `ruleCompleted`

La función de devolución de llamada `ruleCompleted` se activa después de `ruleTriggered` cuando los criterios de condición de la regla se cumplen y se ejecutan todas las acciones de la regla.

## `ruleConditionFailed`

La función de devolución de llamada `ruleConditionFailed` se activa después de `ruleTriggered` cuando falla al menos una de las condiciones de la regla.

## `Rule` objeto

Cada función de devolución de llamada expone un objeto `Rule` que proporciona información sobre la propia regla.

```ts
type Rule = {
  id: string;
  name: string;
  events: Event[]; // Rule-specific events
  conditions: Condition[]; // Rule-specific conditions
  actions: Action[]; // Rule-specific actions
}
```

| Nombre | Tipo | Descripción |
|---|---|---|
| **`id`** | `string` | El identificador único de la regla. |
| **`name`** | `string` | Nombre descriptivo de la regla. |
| **`events`** | `Event[]` | Una matriz de eventos que ha configurado para almacenar en déclencheur la regla. |
| **`conditions`** | `Condition[]` | Una matriz de condiciones que ha configurado para almacenar en déclencheur la regla. |
| **`actions`** | `Action[]` | Una matriz de acciones que ha configurado para ejecutarse cuando se active la regla. |

## Ejemplo

Agregue el siguiente fragmento de código a su HTML en la etiqueta `<head>` antes de llamar a su cargador de biblioteca de etiquetas:

```html
<script>
  window._satellite ??= {};
  window._satellite._monitors ??= [];
  window._satellite._monitors.push({
    ruleTriggered(event) { console.log('Rule triggered', event.rule);},
    ruleCompleted(event) { console.log('Rule completed', event.rule);},
    ruleConditionFailed(event) { console.log('Rule condition failed', event.rule, event.condition);}
  });
</script>
<script src="https://assets.adobedtm.com/.../launch-EN...js" async></script>
```

Dado que la biblioteca de etiquetas aún no se ha cargado en este punto de la página, se crea el objeto `_satellite` inicial y se inicializa una matriz en `_satellite._monitors`. A continuación, el script agrega un objeto de monitor a esa matriz.

Tenga en cuenta las siguientes sugerencias al utilizar monitores:

* Tenga en cuenta que estos mensajes de depuración utilizan `console.log` en lugar de [`_satellite.logger`](logger.md) porque los vínculos se crean antes de que se cargue la biblioteca de etiquetas.
* Aunque el ejemplo de código incluye las tres funciones de llamada de retorno, no son campos obligatorios. Solo puede incluir los vínculos deseados al depurar las reglas del sitio.
* Se permiten varios monitores, incluso para los mismos eventos. Si utiliza varios monitores para un único evento, no se garantiza el orden de las llamadas.
* Asegúrese de crear `_monitors` _antes de_ cargar la biblioteca de etiquetas. Si crea estos vínculos después de cargar la biblioteca, solo se capturan las reglas que entran en déclencheur a partir de ese momento.
