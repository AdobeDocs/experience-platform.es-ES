---
title: Instalación del SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo instalar el SDK web de Experience Platform.
keywords: instalación de sdk web;instalar sdk web;explorador de Internet;promesa;paquete npm
translation-type: tm+mt
source-git-commit: 29272856d766e5adeb4b00ea62b28ea77abe338e
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 4%

---


# Instalación del SDK {#installing-the-sdk}

Existen tres formas compatibles de utilizar el SDK web de Adobe Experience Platform:

1. La forma preferida de utilizar el SDK web de Adobe Experience Platform es mediante [Adobe Experience Platform Launch](https://launch.adobe.com/).
1. El SDK web de Adobe Experience Platform también está disponible en una red de entrega de contenido (CDN) que puede utilizar.
1. Utilice la biblioteca NPM que exporta los módulos EcmaScript 5 y EcmaScript 2015 (ES6).

## Opción 1: Instalación de la extensión de Adobe Experience Platform Launch

Para obtener documentación sobre la extensión de Adobe Experience Platform Launch, consulte la [documentación de Launch](https://docs.adobe.com/content/help/es-ES/launch/using/extensions-ref/adobe-extension/aep-extension/overview.html)

## Opción 2: Instalación de la versión independiente precompilada

La versión prediseñada está disponible en una CDN. Puede hacer referencia a la biblioteca en la CDN directamente en la página, o descargarla y alojarla en su propia infraestructura. Está disponible en formatos minificados y no minificados. La versión no minificada es útil para fines de depuración.

Estructura de la URL: https://cdn1.adoberesources.net/alloy/[VERSIÓN]/alloy.min.js O alloy.js para la versión no minificada.

Por ejemplo:

* Minificado: [https://cdn1.adoberesources.net/alloy/2.3.0/alloy.min.js](https://cdn1.adoberesources.net/alloy/2.3.0/alloy.min.js)
* No minificado: [https://cdn1.adoberesources.net/alloy/2.3.0/alloy.js](https://cdn1.adoberesources.net/alloy/2.3.0/alloy.js)

### Adición del código {#adding-the-code}

La versión independiente prediseñada requiere un &quot;código base&quot; añadido directamente a la página. Copie y pegue el siguiente &quot;código base&quot; lo más alto posible en la etiqueta `<head>` de su HTML:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.3.0/alloy.min.js" async></script>
```

El &quot;código base&quot; crea una función global denominada `alloy`. Utilice esta función para interactuar con el SDK. Si desea nombrar la función global como otra cosa, cambie el nombre `alloy` como se indica a continuación:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.3.0/alloy.min.js" async></script>
```

En este ejemplo, se ha cambiado el nombre de la función global `mycustomname` en lugar de `alloy`.

>[!IMPORTANT]
>
>Para evitar posibles problemas, utilice un nombre que contenga al menos un carácter que no sea un dígito y que no entre en conflicto con el nombre de una propiedad que ya se encuentra en `window`.

Este código base, además de crear una función global, también carga código adicional contenido en un archivo externo \(`alloy.js`\) alojado en un servidor. De forma predeterminada, este código se carga asincrónicamente para permitir que su página web tenga el máximo rendimiento posible. Esta es la implementación recomendada.

### Compatibilidad con Internet Explorer {#support-internet-explore}

Este SDK utiliza promesas, que son un método para comunicar la finalización de tareas asincrónicas. La implementación [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) utilizada por el SDK se admite de forma nativa en todos los navegadores de destino excepto [!DNL Internet Explorer]. Para utilizar el SDK en [!DNL Internet Explorer], debe tener `window.Promise` [polyfill](https://remysharp.com/2010/10/08/what-is-a-polyfill).

Para determinar si ya tiene `window.Promise` polirelleno:

1. Abra el sitio web en [!DNL Internet Explorer].
1. Abra la consola de depuración del explorador.
1. Escriba `window.Promise` en la consola y pulse Intro.

Si aparece algo que no sea `undefined`, es probable que ya haya rellenado `window.Promise`. Otra manera de determinar si `window.Promise` está polirelleno es cargando su sitio web después de haber completado las instrucciones de instalación anteriores. Si el SDK genera un error mencionando algo sobre una promesa, es probable que no haya rellenado el `window.Promise`.

Si ha determinado que debe rellenar `window.Promise`, incluya la siguiente etiqueta de script encima del código base proporcionado anteriormente:

```html
<script src="https://cdn.jsdelivr.net/npm/promise-polyfill@8/dist/polyfill.min.js"></script>
```

Esta etiqueta carga una secuencia de comandos que garantiza que `window.Promise` sea una implementación de Promise válida.

>[!NOTE]
>
>Si decide cargar una implementación de Promise diferente, asegúrese de que admita `Promise.prototype.finally`.

### Carga sincrónica del archivo JavaScript {#loading-javascript-synchronously}

Como se explica en la sección [Adición del código](#adding-the-code), el código base que ha copiado y pegado en el HTML del sitio web carga un archivo externo. El archivo externo contiene la funcionalidad principal del SDK. Todos los comandos que intente ejecutar mientras se carga este archivo se ponen en cola y luego se procesan después de cargar el archivo. La carga asíncrona del archivo es el método de instalación más eficaz.

Sin embargo, en determinadas circunstancias, es posible que desee cargar el archivo sincrónicamente \ (más detalles sobre estas circunstancias se documentarán posteriormente\). Al hacerlo, se bloquea el resto del documento HTML para que el explorador lo analice y procese hasta que se cargue y ejecute el archivo externo. Este retraso adicional antes de mostrar el contenido principal a los usuarios suele desalentarse, pero puede tener sentido según las circunstancias.

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

## Opción 3: Uso del paquete NPM

El SDK web de Adobe Experience Platform también está disponible como paquete NPM. [](https://www.npmjs.com) NPMes el administrador de paquetes para JavaScript. La instalación del paquete NPM permite controlar el proceso de compilación del JavaScript del SDK web de Adobe Experience Platform. El paquete NPM expone los módulos de la versión 5 de EcmaScript o los módulos de la versión 2015 (ES6) de EcmaScript que deben ejecutarse en el explorador.

```bash
npm install @adobe/alloy
```

El paquete NPM del SDK web de Adobe Experience Platform expone una función `createInstance`. Esta función se utiliza para crear una instancia. La opción name que se pasa a la función controla el prefijo utilizado en el registro. A continuación se muestran ejemplos de uso del paquete.

### Uso del paquete como módulo ECMAScript 2015 (ES6)

```javascript
import { createInstance } from "@adobe/alloy";
const alloy = createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

### Uso del paquete como módulo ECMAScript 5

```javascript
var alloyLibrary = require("@adobe/alloy");
var alloy = alloyLibrary.createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

### Compatibilidad con Internet Explorer

El SDK de Adobe Experience Platform utiliza promesas, que son un método para comunicar la finalización de tareas asincrónicas. La implementación [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) utilizada por el SDK se admite de forma nativa en todos los navegadores de destino excepto [!DNL Internet Explorer]. Para utilizar el SDK en [!DNL Internet Explorer], debe tener `window.Promise` [polyfill](https://remysharp.com/2010/10/08/what-is-a-polyfill).

Una biblioteca que podría usar para rellenar la promesa es la promesa-polirelleno. Para obtener más información sobre cómo instalar con NPM, consulte la [prometer-polyfill documentation](https://www.npmjs.com/package/promise-polyfill).

>[!NOTE]
>
>Si decide cargar una implementación de Promise diferente, asegúrese de que admita `Promise.prototype.finally`.