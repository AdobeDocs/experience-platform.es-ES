---
title: Instalación del SDK web mediante la biblioteca de JavaScript
description: Haga referencia a la biblioteca del SDK web mediante un archivo CDN independiente.
exl-id: bacfe938-4326-48f6-a321-bd16970e77eb
source-git-commit: 9876390f7ba34c312f2ce4c00fe39e3ea1ef1ace
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# Instalación del SDK web mediante la biblioteca de JavaScript

Una alternativa a instalar el SDK web sin [usar la extensión de etiqueta](extension.md) es hacer referencia a la biblioteca de JavaScript alojada en una CDN. Puede hacer referencia a la biblioteca directamente o descargarla y alojarla en su propia infraestructura. Está disponible en formatos minificado y completo.

La biblioteca del SDK web está disponible mediante la siguiente estructura de URL:

* **Minificado**: `https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.min.js`
* **Completo**: `https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.js`

Consulte las [notas de la versión](../release-notes.md) para obtener la versión más reciente que se incluirá en la dirección URL. Por ejemplo, la dirección URL de la versión completa de 2.19.1 es `https://cdn1.adoberesources.net/alloy/2.19.1/alloy.js`.

## Adición del código

Agregue el siguiente bloque de código lo más alto posible en la etiqueta `<head>` de su HTML:

```html
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.19.1/alloy.min.js" async></script>
```

Este código crea asincrónicamente un objeto `alloy` que le permite llamar a cualquier comando del SDK web. Si desea cargar el SDK web sincrónicamente, puede quitar el atributo `async` en la última línea del bloque de código. Si se quita el atributo `async`, el explorador no podrá analizar ni procesar el resto del documento del HTML hasta que se cargue y ejecute la biblioteca. Normalmente no se recomienda este retraso adicional antes de mostrar el contenido principal a los usuarios, pero puede tener sentido según las necesidades de la organización.
