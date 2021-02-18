---
title: Instalación del SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo instalar el SDK web de Experience Platform.
keywords: instalación de sdk web;instalación de sdk web;explorador de Internet;promesa;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 2%

---


# Instalación del SDK {#installing-the-sdk}

La forma preferida de utilizar el SDK web de Adobe Experience Platform es mediante [Adobe Experience Platform Launch](http://launch.adobe.com/es). Busque `AEP Web SDK` en el catálogo de extensiones, instale y configure la extensión.

El SDK web de Adobe Experience Platform también está disponible en un CDN para su uso. Puede hacer referencia a este archivo o descargarlo y alojarlo en su propia infraestructura. Está disponible en una versión minimizada y no minimizada. La versión no minimizada resulta útil para la depuración.

Estructura URL: https://cdn1.adoberesources.net/alloy/[VERSIÓN]/alloy.min.js OR alloy.js para la versión sin miniatura.

Por ejemplo:

* Minimizado: [https://cdn1.adoberesources.net/alloy/2.3.0/alloy.min.js](https://cdn1.adoberesources.net/alloy/2.3.0/alloy.min.js)
* No minimizado: [https://cdn1.adoberesources.net/alloy/2.3.0/alloy.js](https://cdn1.adoberesources.net/alloy/2.3.0/alloy.js)

## Añadiendo el código {#adding-the-code}

El primer paso para implementar Adobe Experience Platform [!DNL Web SDK] es copiar y pegar el siguiente &quot;código base&quot; lo más alto posible en la etiqueta `<head>` de su HTML:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.3.0/alloy.min.js" async></script>
```

El código base crea una función global denominada `alloy`. Utilice esta función para interactuar con el SDK. Si desea nombrar la función global otra cosa, puede cambiar el nombre `alloy` de la siguiente manera:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.3.0/alloy.min.js" async></script>
```

En este ejemplo, se cambia el nombre de la función global `mycustomname` en lugar de `alloy`.

>[!IMPORTANT]
>
>Para evitar posibles problemas, utilice un nombre que contenga al menos un carácter que no sea un dígito y que no entre en conflicto con el nombre de una propiedad que ya se encuentre en `window`.

Este código base, además de crear una función global, también carga código adicional dentro de un archivo externo \(`alloy.js`\) alojado en un servidor. De forma predeterminada, este código se carga asincrónicamente para permitir que la página web tenga el máximo rendimiento posible. Ésta es la implementación recomendada.

## Compatibilidad con Internet Explorer {#support-internet-explore}

Este SDK hace uso de las promesas, que es un método para comunicar la finalización de tareas asincrónicas. La implementación [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) utilizada por el SDK es admitida de forma nativa por todos los exploradores de destinatario excepto [!DNL Internet Explorer]. Para utilizar el SDK en [!DNL Internet Explorer], debe tener `window.Promise` [polirelleno](https://remysharp.com/2010/10/08/what-is-a-polyfill).

Para determinar si ya tiene `window.Promise` polirelleno:

1. Abra el sitio web en [!DNL Internet Explorer].
1. Abra la consola de depuración del explorador.
1. Escriba `window.Promise` en la consola y, a continuación, pulse Intro.

Si aparece algo distinto a `undefined`, es probable que ya haya polirelleno `window.Promise`. Otra manera de determinar si `window.Promise` está polirelleno es cargando el sitio web después de haber completado las instrucciones de instalación anteriores. Si el SDK genera un error al mencionar algo acerca de una promesa, probablemente no se ha polirelleno `window.Promise`.

Si ha determinado que necesita rellenar `window.Promise`, incluya la siguiente etiqueta de script encima del código base proporcionado anteriormente:

```html
<script src="https://cdn.jsdelivr.net/npm/promise-polyfill@8/dist/polyfill.min.js"></script>
```

Esto carga una secuencia de comandos que garantiza que `window.Promise` sea una implementación de Promise válida.

>[!NOTE]
>
>Si decide cargar una implementación de Promise diferente, asegúrese de que admite `Promise.prototype.finally`.

## Carga sincrónica del archivo JavaScript {#loading-javascript-synchronously}

Como se explica en la sección [que Añade el código](#adding-the-code), el código base que ha copiado y pegado en el HTML del sitio web carga un archivo externo con código adicional. Este código adicional contiene la funcionalidad principal del SDK. Cualquier comando que intente ejecutar mientras se carga este archivo se pondrá en cola y, a continuación, se procesará una vez cargado el archivo. Este es el método de instalación de mayor rendimiento.

Sin embargo, bajo ciertas circunstancias, es posible que desee cargar el archivo sincrónicamente \(más detalles sobre estas circunstancias se documentarán más adelante\). De este modo, se bloquea el resto del documento HTML para que el explorador lo analice y procese hasta que se cargue y ejecute el archivo externo. Este retraso adicional antes de mostrar contenido principal a los usuarios suele desaconsejarse, pero puede tener sentido según las circunstancias.

Para cargar el archivo sincrónicamente en lugar de asincrónicamente, elimine el atributo `async` de la segunda etiqueta `script` como se muestra a continuación:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.3.0/alloy.min.js"></script>
```
