---
title: getVar()
description: Devuelve un valor de un elemento de datos o un conjunto de valores mediante setVar().
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 2%

---

# `getVar()`

El método `_satellite.getVar()` devuelve el valor actual de un [elemento de datos](/help/tags/ui/managing-resources/data-elements.md) o un valor establecido mediante [`_satellite.setVar()`](setvar.md). Si un elemento de datos y un valor `setVar()` comparten el mismo nombre, el elemento de datos tiene prioridad. Si llama a un identificador de cadena que aún no existe, el método devuelve `undefined`. La evaluación es sincrónica.

```js
_satellite.getVar(name: string, event?: unknown) => unknown
```

El valor devuelto y el tipo dependen del tipo de elemento de datos al que haga referencia. Por ejemplo, si llama a `getVar()` que recupera una variable de cadena, el tipo devuelto es `string`. Si llama a `getVar()` que devuelve un elemento de datos de variable de Web SDK, el tipo devuelto es un `object` que contiene todas las propiedades establecidas en esa variable.

```js
// Retrieves the value in the `Example` data element
_satellite.getVar('Example');

// Execute custom logic depending on the numeric value in the `cartTotal` data element
const cartValue = Number(_satellite.getVar('cartTotal'));
if (cartValue > 100) {
  _satellite.logger.info('Purchase larger than $100 detected');
}

// Some data elements like Web SDK variables support deeply nested properties
const pageName = _satellite.getVar('Data layer')?.web?.webPageDetails?.name;
if (!pageName) {
  _satellite.logger.warn('Page name is not set');
}

// Custom code data elements support a second argument
// Works in a Launch custom code block where `event` is provided by the rule engine.
const rule = _satellite.getVar('Return event rule', event);
```

## Campos disponibles

El método `getVar()` admite dos argumentos. La mayoría de los casos de uso no incluyen el segundo argumento opcional.

| Nombre | Tipo | Requerido | Descripción |
| --- | --- | --- | --- |
| **`name`** | `string` | Sí | El nombre del elemento de datos que desea recuperar. Los nombres de los elementos de datos distinguen entre mayúsculas y minúsculas. |
| **`event`** | `object` | No | Contexto del evento de la regla de activación. Solo se usa en casos de uso avanzados por elementos de datos que usan [código personalizado](/help/tags/ui/managing-resources/data-elements.md#custom-code) o extensiones personalizadas. Cuando una regla se activa mediante un evento (como un clic, un envío de formulario o un envío de JavaScript personalizado), el objeto de evento asociado se incluye aquí. Los elementos de datos pueden utilizar esta información para devolver valores contextuales, como los detalles o las propiedades del elemento en el que se hizo clic desde un evento personalizado. |
