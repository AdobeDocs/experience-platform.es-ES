---
title: Instalación del SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo instalar el SDK web de Experience Platform.
exl-id: b1de7ca1-d0d2-4661-a273-a1acf29afcd5
source-git-commit: a8b1aa87ecd85c530188e520db2f17136a63ae44
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 0%

---

# Instalación del SDK web {#installing-the-sdk}

Existen tres formas compatibles de instalar el SDK web de Adobe Experience Platform:

1. La forma preferida de utilizar el SDK web de Adobe Experience Platform es mediante la IU de recopilación de datos o la IU del Experience Platform.
1. El SDK web de Adobe Experience Platform también está disponible en una red de distribución de contenido (CDN) que puede utilizar.
1. Utilice la biblioteca NPM que exporta los módulos EcmaScript 5 y EcmaScript 2015 (ES6).

## Opción 1: Instalación de la extensión de etiqueta

Para obtener documentación sobre la extensión de etiqueta, consulte la [Documentación de etiquetas](../../tags/extensions/client/web-sdk/overview.md)

## Opción 2: instalar la versión independiente prediseñada

La versión prediseñada está disponible en una CDN. Puede hacer referencia a la biblioteca en la CDN directamente en la página o descargarla y alojarla en su propia infraestructura. Está disponible en formatos minificado y no minificado. La versión no minificada es útil para la depuración.

Estructura de la URL: https://cdn1.adoberesources.net/alloy/[VERSIÓN]/alloy.min.js o alloy.js para la versión no minificada.

Por ejemplo:

* Minificado: [https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js](https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js)
* Sin reducir: [https://cdn1.adoberesources.net/alloy/2.14.0/alloy.js](https://cdn1.adoberesources.net/alloy/2.14.0/alloy.js)


### Adición del código {#adding-the-code}

La versión independiente creada previamente requiere un &quot;código base&quot; añadido directamente a la página. Copie y pegue el siguiente &quot;código base&quot; lo más alto posible en la `<head>` de su HTML:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js" async></script>
```

El &quot;código base&quot; crea una función global denominada `alloy`. Utilice esta función para interactuar con el SDK. Si desea asignar otro nombre a la función global, cambie el `alloy` nombrar como sigue:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js" async></script>
```

En este ejemplo, se cambia el nombre de la función global `mycustomname`, en lugar de `alloy`.

>[!IMPORTANT]
>
>Para evitar posibles problemas, utilice un nombre que contenga al menos un carácter que no sea un dígito y que no entre en conflicto con el nombre de una propiedad ya encontrada en `window`.

Este código base, además de crear una función global, también carga código adicional contenido en un archivo externo \(`alloy.js`\) alojado en un servidor. De forma predeterminada, este código se carga asincrónicamente para permitir que la página web tenga el mayor rendimiento posible. Esta es la implementación recomendada.

### Compatibilidad con Internet Explorer {#support-internet-explore}

>[!IMPORTANT]
>
>A finales de abril de 2024, el SDK web de Adobe Experience Platform eliminará la compatibilidad con todas las versiones de Internet Explorer.

Este SDK utiliza promesas, que son un método de comunicación de la finalización de tareas asincrónicas. El [Promesa](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) La implementación utilizada por el SDK es compatible de forma nativa con todos los navegadores de destino, excepto [!DNL Internet Explorer]. Para usar el SDK en [!DNL Internet Explorer], debe tener `window.Promise` [polillenado](https://remysharp.com/2010/10/08/what-is-a-polyfill).

Para determinar si ya tiene `window.Promise` polillenado:

1. Abra el sitio web en [!DNL Internet Explorer].
1. Abra la consola de depuración del explorador.
1. Tipo `window.Promise` en la consola y pulse Intro.

Si algo distinto de `undefined` aparece, probablemente ya haya rellenado correctamente `window.Promise`. Otra forma de determinar si `window.Promise` es polyfill es cargando su sitio web después de haber completado las instrucciones de instalación anteriores. Si el SDK genera un error al mencionar algo sobre una promesa, es probable que no haya rellenado correctamente `window.Promise`.

Si ha determinado que debe rellenar políticamente `window.Promise`, incluya la siguiente etiqueta de script encima del código base proporcionado anteriormente:

```html
<script src="https://cdn.jsdelivr.net/npm/promise-polyfill@8/dist/polyfill.min.js"></script>
```

Esta etiqueta carga una secuencia de comandos que garantiza que `window.Promise` es una implementación de Promise válida.

>[!NOTE]
>
>Si decide cargar una implementación de Promise diferente, asegúrese de que admita `Promise.prototype.finally`.

### Carga sincrónica del archivo JavaScript {#loading-javascript-synchronously}

Como se explica en la sección [Adición del código](#adding-the-code), el código base que ha copiado y pegado en el HTML del sitio web carga un archivo externo. El archivo externo contiene la funcionalidad principal del SDK. Cualquier comando que intente ejecutar mientras se carga este archivo se pone en cola y se procesa después de cargar el archivo. La carga asíncrona del archivo es el método de instalación más eficaz.

En determinadas circunstancias, sin embargo, es posible que desee cargar el archivo sincrónicamente. Al hacerlo, el explorador impide que analice y procese el resto del documento del HTML hasta que se haya cargado y ejecutado el archivo externo. Normalmente no se recomienda este retraso adicional antes de mostrar el contenido principal a los usuarios, pero puede tener sentido según las circunstancias.

Para cargar el archivo sincrónicamente en lugar de asincrónicamente, quite el `async` atributo del segundo `script` como se muestra a continuación:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js"></script>
```

## Opción 3: Uso del paquete NPM

El SDK web de Adobe Experience Platform también está disponible como paquete NPM. [NPM](https://www.npmjs.com) es el administrador de paquetes para JavaScript. La instalación del paquete NPM permite controlar el proceso de compilación para el JavaScript del SDK web de Adobe Experience Platform. El paquete NPM expone módulos EcmaScript versión 5 o módulos EcmaScript versión 2015 (ES6) pensados para ejecutarse en el navegador.

```bash
npm install @adobe/alloy
```

El paquete NPM del SDK web de Adobe Experience Platform expone un `createInstance` función. Esta función se utiliza para crear una instancia de. La opción de nombre pasada a la función controla el prefijo utilizado en el registro. A continuación se muestran ejemplos de uso del paquete.

### Uso del paquete como módulo ECMAScript 2015 (ES6)

```javascript
import { createInstance } from "@adobe/alloy";
const alloy = createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

>[!NOTE]
>
>El paquete NPM se basa en módulos CommonJS; por lo tanto, cuando utilice un paquete, asegúrese de que el paquete admita módulos CommonJS. Algunos paquetes, como [Resumen](https://rollupjs.org), requiere un [plugin](https://www.npmjs.com/package/@rollup/plugin-commonjs) que proporciona compatibilidad con CommonJS.

### Uso del paquete como módulo ECMAScript 5

```javascript
var alloyLibrary = require("@adobe/alloy");
var alloy = alloyLibrary.createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

### Compatibilidad con Internet Explorer

El SDK de Adobe Experience Platform utiliza promesas, que son un método de comunicación de la finalización de tareas asincrónicas. El [Promesa](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) La implementación utilizada por el SDK es compatible de forma nativa con todos los navegadores de destino, excepto [!DNL Internet Explorer]. Para usar el SDK en [!DNL Internet Explorer], debe tener `window.Promise` [polillenado](https://remysharp.com/2010/10/08/what-is-a-polyfill).

Una biblioteca que podría usar para polyfill promise es promise-polyfill. Consulte la [documentación de promise-polyfill](https://www.npmjs.com/package/promise-polyfill) para obtener más información sobre cómo instalar con NPM.

>[!NOTE]
>
>Si decide cargar una implementación de Promise diferente, asegúrese de que admita `Promise.prototype.finally`.
