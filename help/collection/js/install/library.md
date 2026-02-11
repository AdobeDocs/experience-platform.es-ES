---
title: Instalar la biblioteca Web SDK JavaScript
description: Haga referencia a la biblioteca Web SDK mediante un archivo CDN independiente.
exl-id: bacfe938-4326-48f6-a321-bd16970e77eb
source-git-commit: 010192e91185c11d5454d4153913c06b90fe2122
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---

# Instalar la biblioteca Web SDK JavaScript

Si decide no utilizar la [extensión de etiquetas Web SDK](/help/tags/extensions/client/web-sdk/overview.md), puede instalar Web SDK haciendo referencia a la biblioteca JavaScript independiente alojada en la CDN de Adobe. Puede hacer referencia a la biblioteca directamente o descargarla y alojarla en su propia infraestructura. Está disponible en formatos minificado y completo.

La biblioteca Web SDK está disponible con la siguiente estructura de URL:

* **Minificado**: `https://cdn1.adoberesources.net/alloy/<VERSION>/alloy.min.js`
* **Completo**: `https://cdn1.adoberesources.net/alloy/<VERSION>/alloy.js`

Consulte las [notas de la versión de Web SDK](../release-notes.md) para obtener la versión más reciente que se incluirá en la dirección URL. Por ejemplo, la dirección URL de la versión completa de 2.19.1 es `https://cdn1.adoberesources.net/alloy/2.19.1/alloy.js`.

## Adición del código base y del cargador de biblioteca

El código que se va a agregar consta de dos secciones:

* **Código base**: permite el arranque mediante comandos en cola mientras Web SDK se carga asincrónicamente. Consulte [Código base](base-code.md) para obtener más información. Adobe recomienda utilizar el código base al cargar la biblioteca de forma asíncrona para evitar condiciones de carrera al llamar a comandos de Web SDK durante la carga de la página.
* **Cargador de biblioteca**: carga la biblioteca JavaScript completa.

Agregue el siguiente bloque de código lo más alto posible en la etiqueta `<head>`, antes de cualquier script que pueda llamar a Web SDK:

```html
<!-- Base code -->
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<!-- Library loader -->
<script src="https://cdn1.adoberesources.net/alloy/<VERSION>/alloy.min.js" async></script>
```

Si desea cargar Web SDK sincrónicamente, puede quitar el atributo `async` al cargar la biblioteca. Al eliminar el atributo `async`, se bloquea el análisis de HTML mientras el explorador recupera y ejecuta la biblioteca. Normalmente no se recomienda este retraso adicional antes de mostrar el contenido principal a los usuarios, pero puede tener sentido según las necesidades de la organización.
