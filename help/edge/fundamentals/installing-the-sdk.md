---
title: Instalación del SDK web de Adobe Experience Platform
seo-title: Adobe Experience Platform Web SDK instalar el SDK
description: Obtenga información sobre cómo instalar el SDK web de Experience Platform
seo-description: Obtenga información sobre cómo instalar el SDK web de Experience Platform
keywords: web sdk installation;installing web sdk;internet explorer;promise;
translation-type: tm+mt
source-git-commit: d23568f7ce63df5aa98dc237a6671eeadde0c9b2
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 2%

---


# Instalación del SDK {#installing-the-sdk}

La forma preferida de utilizar el SDK web de Adobe Experience Platform es a través de [Adobe Experience Platform Launch](http://launch.adobe.com/es). Busque el `AEP Web SDK` en el catálogo de extensiones, instálelo y luego configure la extensión.

El SDK web de AEP también está disponible en un CDN para su uso. Puede hacer referencia a este archivo o descargarlo y alojarlo en su propia infraestructura. Está disponible en una versión minimizada y no minimizada. La versión no minimizada resulta útil para la depuración.

Estructura URL: https://cdn1.adoberesources.net/alloy/[VERSIÓN]/alloy.min.js O alloy.js para la versión sin miniatura.

Por ejemplo:

* Minimizado: [https://cdn1.adoberesources.net/alloy/2.3.0/alloy.min.js](https://cdn1.adoberesources.net/alloy/2.3.0/alloy.min.js)
* No minimizado: [https://cdn1.adoberesources.net/alloy/2.3.0/alloy.js](https://cdn1.adoberesources.net/alloy/2.3.0/alloy.js)

## Añadir el código {#adding-the-code}

El primer paso en la implementación del Adobe Experience Platform [!DNL Web SDK] es copiar y pegar el siguiente &quot;código base&quot; lo más alto posible en la `<head>` etiqueta de su HTML:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.3.0/alloy.min.js" async></script>
```

El código base crea una función global denominada `alloy`. Utilice esta función para interactuar con el SDK. Si desea nombrar la función global otra cosa, puede cambiar el `alloy` nombre de la siguiente manera:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.3.0/alloy.min.js" async></script>
```

En este ejemplo, se cambia el nombre de la función global `mycustomname`en lugar de `alloy`.

>[!IMPORTANT]
>
>Para evitar posibles problemas, utilice un nombre que contenga al menos un carácter que no sea un dígito y que no entre en conflicto con el nombre de una propiedad que ya se encuentre en `window`.

Este código base, además de crear una función global, también carga código adicional contenido en un archivo externo \(`alloy.js`\) alojado en un servidor. De forma predeterminada, este código se carga asincrónicamente para permitir que la página web tenga el máximo rendimiento posible. Ésta es la implementación recomendada.

## Compatibilidad con Internet Explorer {#support-internet-explore}

Este SDK hace uso de las promesas, que es un método para comunicar la finalización de tareas asincrónicas. La implementación [Promise](https://developer.mozilla.org/es-ES/docs/Web/JavaScript/Reference/Global_Objects/Promise) que utiliza el SDK es admitida de forma nativa por todos los exploradores de destinatario excepto [!DNL Internet Explorer]. Para utilizar el SDK en [!DNL Internet Explorer], debe tener `window.Promise` un [relleno](https://remysharp.com/2010/10/08/what-is-a-polyfill).

Para determinar si ya tiene `window.Promise` polirelleno:

1. Abra el sitio web en [!DNL Internet Explorer].
1. Abra la consola de depuración del explorador.
1. Escriba `window.Promise` en la consola y, a continuación, pulse Intro.

Si aparece algo distinto a `undefined` , es probable que ya se haya completado `window.Promise`. Otra manera de determinar si `window.Promise` se ha rellenado con polirelleno es cargando el sitio web después de completar las instrucciones de instalación anteriores. Si el SDK genera un error al mencionar algo acerca de una promesa, es probable que no se haya completado `window.Promise`.

Si ha determinado que necesita rellenar `window.Promise`, incluya la siguiente etiqueta de script encima del código base proporcionado anteriormente:

```html
<script src="https://cdn.jsdelivr.net/npm/promise-polyfill@8/dist/polyfill.min.js"></script>
```

Esto carga una secuencia de comandos que garantiza que `window.Promise` sea una implementación de Promise válida.

>[!NOTE]
>
>Si decide cargar una implementación de Promesa diferente, asegúrese de que admite `Promise.prototype.finally`.

## Carga sincrónica del archivo JavaScript {#loading-javascript-synchronously}

Como se explica en la sección que [Añade el código](#adding-the-code), el código base que ha copiado y pegado en el HTML del sitio web carga un archivo externo con código adicional. Este código adicional contiene la funcionalidad principal del SDK. Cualquier comando que intente ejecutar mientras se carga este archivo se pondrá en cola y, a continuación, se procesará una vez cargado el archivo. Este es el método de instalación de mayor rendimiento.

Sin embargo, bajo ciertas circunstancias, es posible que desee cargar el archivo sincrónicamente \(más detalles sobre estas circunstancias se documentarán más adelante\). De este modo, se bloquea el resto del documento HTML para que el explorador lo analice y procese hasta que se cargue y ejecute el archivo externo. Este retraso adicional antes de mostrar contenido principal a los usuarios suele desaconsejarse, pero puede tener sentido según las circunstancias.

Para cargar el archivo sincrónicamente en lugar de asincrónicamente, elimine el `async` atributo de la segunda `script` etiqueta como se muestra a continuación:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.3.0/alloy.min.js"></script>
```
