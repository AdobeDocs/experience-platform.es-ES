---
title: track()
description: Déclencheur de una regla de llamada directa.
source-git-commit: a36e5af39f904370c1e97a9ee1badad7a2eac32e
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 2%

---

# `track()`

El método `_satellite.track()` le permite almacenar en déclencheur una [regla de llamada directa](/help/tags/extensions/client/core/overview.md#direct-call-event).

>[!IMPORTANT]
>
>Adobe considera `_satellite.track()` un **método de implementación heredado**. Aunque todavía es totalmente compatible, Adobe recomienda encarecidamente usar prácticas de implementación más modernas, como [Adobe Client Data Layer](/help/tags/extensions/client/client-data-layer/overview.md), que es el enfoque recomendado para nuevas implementaciones.
>
>Si opta por usar `_satellite.track()` en su sitio, **proteja cada llamada** para que su sitio no esté perfectamente acoplado a la biblioteca de etiquetas. Si no se protege, si se quita la propiedad de etiqueta en el futuro, todas las referencias al objeto `_satellite` producirán errores.

```ts
_satellite.track(identifier: string, detail?: unknown ): void;
```

Cuando llama a `_satellite.track()` con el identificador configurado en la interfaz de usuario de etiquetas, esa regla se activa inmediatamente. Llamar a este método solo actúa como evento de regla; las condiciones de la regla siguen aplicándose antes de ejecutar las acciones de la regla. Varias reglas de llamada directa pueden utilizar el mismo identificador, lo que le permite almacenar en déclencheur todas esas reglas a la vez mediante una sola llamada de `_satellite.track()`. Cada regla activada sigue comprobando sus propias condiciones antes de realizar una acción, incluso si varias reglas comparten el mismo identificador.

## Campos disponibles

El método `_satellite.track()` admite dos argumentos:

| Nombre | Tipo | Requerido | Descripción |
|---|---|---|---|
| **`identifier`** | `string` | Sí | Identificador de la regla de llamada directa. Este identificador se establece al configurar la regla en la interfaz de usuario de etiquetas. |
| **`detail`** | `unknown` | No | Una carga útil opcional que contiene la información deseada. Al configurar una regla, puede acceder a la carga útil mediante `event.detail` (código personalizado) o `%event.detail%` (campos de texto que admiten la notación de elementos de datos). |

```js
// Trigger rules with the identifier 'example'
if (window._satellite?.track) {
  _satellite.track('example');
}

// Trigger a direct call rule with an optional payload that your tag rule can use
_satellite.track('contact_submit', { name: 'John Doe' });
// When configuring the rule, access the payload field using:
// event.detail.name (custom code block) or
// %event.detail.name% (data element)
```
