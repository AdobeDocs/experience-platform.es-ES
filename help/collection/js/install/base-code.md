---
title: Código base
description: Comandos de cola (bootstrap) mientras la biblioteca de recopilación de datos se carga asincrónicamente.
source-git-commit: 0a45b688243b17766143b950994f0837dc0d0b48
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# Código base

El código base habilita el arranque poniendo en cola comandos mientras Adobe Experience Platform Web SDK se carga asincrónicamente. Una vez que se ejecute el código base, puede llamar inmediatamente a cualquier comando como [`configure`](../commands/configure/overview.md) o [`sendEvent`](../commands/sendevent/overview.md) sin preocuparse por las condiciones de carrera o el momento en que la biblioteca termina de cargarse. Cuando Web SDK termina de cargarse, los comandos en cola se ejecutan en el orden de entrada y de salida (el mismo orden en que se pusieron en cola).

Los comandos devuelven Promesas, incluso cuando están en cola. Si un comando está en cola, la promesa se resuelve o rechaza después de que el comando se ejecute cuando Web SDK termine de cargarse. Si Web SDK nunca termina de cargarse (por ejemplo, la biblioteca no se puede cargar), las promesas en cola permanecen pendientes.

## Añadir el código base

Coloque el código base lo más alto posible en la etiqueta `<head>`, antes de los scripts que puedan llamar a Web SDK.

```html
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
  (window,["alloy"]);
</script>
```

Después de agregar el código base, cargue Web SDK con el método elegido ([cargador de biblioteca JavaScript](library.md) o [código incrustado de etiquetas](/help/tags/extensions/client/web-sdk/getting-started.md)). Para implementaciones basadas en etiquetas, el código base es compatible con la extensión de etiquetas Web SDK 2.34.0 y posteriores.

Este código base **no** es necesario en los siguientes casos:

* Si carga la biblioteca de JavaScript sincrónicamente. Bloques de carga sincrónica que analizan mientras se busca y ejecuta la biblioteca.
* Si se utiliza la extensión de etiquetas, todas las llamadas a Web SDK se realizan dentro de reglas o acciones de etiquetas. Solo es necesario incluir el código base si la implementación hace referencia a Web SDK fuera de la biblioteca de etiquetas. La mayoría de las implementaciones de etiquetas no suelen llamar a Web SDK fuera de la biblioteca de etiquetas, por lo que la mayoría de las implementaciones de etiquetas no requieren el código base.

## Ejemplos

Vea los comentarios incluidos en este ejemplo de código para comprender el tiempo que transcurre entre la cola y la resolución de los comandos. Este ejemplo se aplica tanto a la biblioteca de JavaScript como a la extensión de etiquetas:

```html
<head>
  <script>
    // Calls made before the base code runs are not captured (alloy is not yet defined).
    // Always make sure that the base code runs before any attempt to call commands.
    // alloy("getLibraryInfo").then(console.log).catch(console.error);
  </script>

  <!-- Base code -->
  <script>
    !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
    []).push(o),n[o]=function(){var u=arguments;return new Promise(
    function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
    (window,["alloy"]);
  </script>

  <!-- Queued command -->
  <script>
    alloy("getLibraryInfo").then(result => {
      console.log("Queued call resolved:", result);
    }).catch(console.error);
  </script>

  <!-- Load the Web SDK using the JavaScript loader -->
  <script src="https://cdn1.adoberesources.net/alloy/<VERSION>/alloy.min.js" async></script>
  <!-- or the tag extension -->
  <!-- <script src=".../launch-<ENV>.min.js" async></script> -->

  <!-- Another call (queued if the library is still loading; immediate if it is ready) -->
  <script>
    alloy("getLibraryInfo").then(result => {
      console.log("Immediate call resolved:", result);
    }).catch(console.error);
  </script>
</head>
```

## Cambiar nombre de instancia de SDK

Puede cambiar el nombre de la función global a la que llama modificando la última línea del código base. Cambiar:

```js
(window,["alloy"]);
```

Hasta:

```js
(window,["ingot"]);
```

Este cambio le permite llamar a comandos usando `ingot` en lugar de `alloy`:

```js
ingot("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

## Varias instancias de SDK

Opcionalmente, puede utilizar el código base para configurar más de una instancia de SDK en una página. Consulte [Usar varias instancias de Web SDK](../../use-cases/multiple-instances.md) para obtener más información.
