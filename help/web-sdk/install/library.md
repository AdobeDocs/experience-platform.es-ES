---
title: Instalar Web SDK mediante la biblioteca de JavaScript
description: Haga referencia a la biblioteca Web SDK mediante un archivo CDN independiente.
exl-id: bacfe938-4326-48f6-a321-bd16970e77eb
source-git-commit: 35429ec2dffacb9c0f2c60b608561988ea487606
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 0%

---

# Instalar Web SDK mediante la biblioteca de JavaScript

Una alternativa a instalar Web SDK sin [usar la extensión de etiqueta](extension.md) es hacer referencia a la biblioteca de JavaScript alojada en una CDN. Puede hacer referencia a la biblioteca directamente o descargarla y alojarla en su propia infraestructura. Está disponible en formatos minificado y completo.

La biblioteca Web SDK está disponible con la siguiente estructura de URL:

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

Este código crea asincrónicamente un objeto `alloy` que le permite llamar a cualquier comando de Web SDK. Si desea cargar Web SDK sincrónicamente, puede quitar el atributo `async` en la última línea del bloque de código. Si se quita el atributo `async`, el explorador no podrá analizar y procesar el resto del documento de HTML hasta que se cargue y ejecute la biblioteca. Normalmente no se recomienda este retraso adicional antes de mostrar el contenido principal a los usuarios, pero puede tener sentido según las necesidades de la organización.
