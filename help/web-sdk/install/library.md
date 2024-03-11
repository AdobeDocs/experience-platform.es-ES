---
title: Instalación del SDK web mediante la biblioteca JavaScript de
description: Haga referencia a la biblioteca del SDK web mediante un archivo CDN independiente.
exl-id: bacfe938-4326-48f6-a321-bd16970e77eb
source-git-commit: 58cd6300307881c3de7c52e07c401bf2ed908517
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# Instalación del SDK web mediante la biblioteca JavaScript de

Una alternativa a instalar el SDK web sin [uso de la extensión de etiqueta](extension.md) es hacer referencia a la biblioteca JavaScript alojada en una CDN. Puede hacer referencia a la biblioteca directamente o descargarla y alojarla en su propia infraestructura. Está disponible en formatos minificado y completo.

La biblioteca del SDK web está disponible mediante la siguiente estructura de URL:

* **Minificado**: `https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.min.js`
* **Completo**: `https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.js`

Consulte la [notas de la versión](../release-notes.md) para que la última versión se incluya en la dirección URL. Por ejemplo, la URL de la versión completa de 2.19.1 es `https://cdn1.adoberesources.net/alloy/2.19.1/alloy.js`.

## Adición del código

Agregue el siguiente bloque de código lo más alto posible en la variable `<head>` de su HTML:

```html
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.19.1/alloy.min.js" async></script>
```

Este código crea de forma asincrónica un `alloy` que le permite llamar a cualquier comando del SDK web. Si desea cargar el SDK web sincrónicamente, puede quitar la variable `async` en la última línea del bloque de código. Eliminación del `async` El atributo impide que el explorador analice y procese el resto del documento de HTML hasta que se cargue y ejecute la biblioteca. Normalmente no se recomienda este retraso adicional antes de mostrar el contenido principal a los usuarios, pero puede tener sentido según las necesidades de la organización.
