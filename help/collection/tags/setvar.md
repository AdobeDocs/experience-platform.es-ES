---
title: setVar()
description: Establece un valor que se puede recuperar más adelante mediante getVar().
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---

# `setVar()`

El método `_satellite.setVar()` le permite establecer uno o más pares de nombre/valor personalizados a los que [`_satellite.getVar()`](getvar.md) puede hacer referencia posteriormente.

```ts
// Set a single name/value pair
_satellite.setVar(name: string, value: unknown): void

// Set multiple name/value pairs at once
_satellite.setVar(vars: { [name: string]: unknown }): void;
```

>[!IMPORTANT]
>
>Aunque el método `getVar()` puede recuperar tanto los elementos de datos como los valores establecidos por `setVar()`, estos dos tipos de entidades son independientes. El uso de `setVar()` para establecer un valor con el mismo nombre que un elemento de datos en la interfaz de usuario de etiquetas no lo sobrescribe.

## Persistencia y ámbito

`setVar()` valores solo se encuentran en la memoria de la página:

* **Solo página actual**: los valores persisten hasta que se descarga la página. En aplicaciones de una sola página, persisten hasta que se vuelve a cargar por completo o se sobrescriben o borran.
* **Sin almacenamiento en el explorador**: no se escribe nada en las cookies, el almacenamiento local o el almacenamiento de sesión.

## Valores de referencia establecidos con `setVar()`

Puede recuperar valores en el código personalizado mediante `getVar()`:

```js
// Set a custom variable using setVar()
_satellite.setVar('Ad location','Banner advertisement');

// Returns the string 'Banner advertisement'
_satellite.getVar('Ad location');
```

También puede hacer referencia a estas variables en la interfaz de usuario de etiquetas en campos que admiten la notación de elementos de datos:

```text
%Ad location%
```

>[!NOTE]
>
>Si un conjunto de valores que utiliza `setVar()` utiliza el mismo nombre que un elemento de datos y hace referencia a ese nombre en la notación de elementos de datos, el elemento de datos tiene prioridad.

## Ejemplos

```js
// Set a single name/value pair
_satellite.setVar('product', 'Circuit Pro');

// Set multiple name/value pairs at once (same as calling setVar() three times)
_satellite.setVar({ 'title': 'Blinding Light', 'category': 'Game', 'genre': 'Tower defense' });

// Retrieve each value
_satellite.getVar('title'); // Blinding Light
_satellite.getVar('category'); // Game
_satellite.getVar('genre'); // Tower defense
```
