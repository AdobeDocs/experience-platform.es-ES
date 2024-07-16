---
title: Módulos de biblioteca principales para extensiones web
description: Obtenga información acerca de los módulos de biblioteca principales que puede utilizar en las extensiones web.
exl-id: 7fb63208-aed0-4add-b6da-8e4aea063d0a
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 93%

---

# Módulos de biblioteca principales para extensiones web

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

Este documento proporciona una lista de los módulos de biblioteca principales que puede utilizar en sus extensiones web. Puede acceder a estos módulos mediante el comando `require('@adobe/{MODULE}')`, donde `{MODULE}` corresponde al nombre del módulo principal que desea utilizar.

## [!DNL reactor-object-assign]

`reactor-object-assign` imita el método [`Object.assign`](https://developer.mozilla.org/es-ES/docs/Web/JavaScript/Referencia/Objetos_globales/Object/assign) nativo al copiar las propiedades de los objetos de origen a un objeto de destino.

```javascript
var objectAssign = require('@adobe/reactor-object-assign');
var all = objectAssign({ a: 'a' }, { b: 'b' });
```

## [!DNL reactor-cookie]

El objeto `reactor-cookie` es una utilidad que permite leer y escribir cookies. Consulte el [paquete npm de js-cookie](https://www.npmjs.com/package/js-cookie) para obtener más información.

```javascript
var cookie = require('@adobe/reactor-cookie');
cookie.set('foo', 'bar');
console.log(cookie.get('foo'));
cookie.remove('foo');
```

### [!DNL reactor-document]

`reactor-document` representa el objeto [`Document`](https://developer.mozilla.org/es-ES/docs/Web/API/Document). Esto puede resultar beneficioso para las pruebas del módulo, ya que permite que las pruebas inyecten un objeto `document` ficticio mediante utilidades como [`inject-loader`](https://www.npmjs.com/package/inject-loader).

```javascript
var document = require('@adobe/reactor-document');
console.log(document.location);
```

### [!DNL reactor-query-string]

`reactor-query-string` es una utilidad que permite analizar y serializar [cadenas de consulta](https://developer.mozilla.org/en-US/docs/Web/API/HTMLHyperlinkElementUtils/search).

```javascript
var queryString = require('@adobe/reactor-query-string');
var parsed = queryString.parse(location.search);
console.log(parsed.campaign);
var obj = {
  campaign: 'Campaign A'
};
var stringified = queryString.stringify(obj);
```

La utilidad tiene los métodos siguientes:

* `queryString.parse({STRING})`: analiza una cadena de consulta en un objeto. Tenga en cuenta que la utilidad omite los caracteres iniciales `?`, `#` y `&` de la cadena de consulta.
* `queryString.stringify({OBJECT})`: convierte un objeto en una cadena de consulta.

### [!DNL reactor-load-script]

`reactor-load-script` es una función que carga una secuencia de comandos cuando se proporciona una dirección URL. Se creará y se colocará dentro del nodo `head` del documento una etiqueta de la secuencia de comandos. El sistema devolverá un objeto [promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) que se puede utilizar para determinar cuándo la carga de la secuencia de comandos se realiza de manera satisfactoria o falla.

```javascript
var loadScript = require('@adobe/reactor-load-script');
var url = 'http://code.jquery.com/jquery-3.1.1.js';
loadScript(url).then(function() {
  // Do something ...
})
```

### [!DNL reactor-promise]

`reactor-promise` es un constructor que imita la [API Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) nativa de ECMAScript 6. Si la API Promise nativa está disponible, esta se devolverá en su lugar.

```javascript
var Promise = require('@adobe/reactor-promise');
new Promise(function(resolve) {
  resolve();
}, function(err) {
  console.error(err);
});
```

### [!DNL reactor-window]

`reactor-window` representa el objeto [`Window`](https://developer.mozilla.org/es-ES/docs/Web/API/Window). Esto puede resultar beneficioso al probar el módulo, ya que permite que las pruebas inyecten un objeto ficticio `Window` mediante utilidades como [`inject-loader`](https://www.npmjs.com/package/inject-loader).

```javascript
var window = require('@adobe/reactor-window');
console.log(window.document);
```
