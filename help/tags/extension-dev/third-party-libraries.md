---
title: Implementación de bibliotecas de terceros
description: Obtenga información acerca de los diferentes métodos para alojar bibliotecas de terceros dentro de sus extensiones de etiquetas de Adobe Experience Platform.
exl-id: d8eaf814-cce8-499d-9f02-b2ed3c5ee4d0
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '1330'
ht-degree: 98%

---

# Implementación de bibliotecas de terceros

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

Uno de los principales objetivos de las extensiones de etiquetas en Adobe Experience Platform es permitir la implementación sencilla de las tecnologías de marketing (bibliotecas) existentes en su sitio web. Con las extensiones, puede implementar bibliotecas proporcionadas por redes de envío de contenido de terceros (CDN) sin tener que editar manualmente el HTML del sitio web.

Existen varios métodos para alojar bibliotecas de terceros (proveedores) en sus extensiones. Este documento proporciona información general de estos distintos métodos de implementación y detalla los pros y los contras de cada uno.

## Requisitos previos

Este documento requiere una comprensión práctica de las extensiones de etiquetas, incluido lo que pueden hacer y cómo están compuestas. Consulte la [información general sobre el desarrollo de extensiones](./overview.md) para obtener más información.

## Proceso de carga de código base

Fuera del contexto de las etiquetas, es importante comprender cómo se suelen cargar las tecnologías de marketing en un sitio web. Los proveedores de bibliotecas de terceros proporcionan un fragmento de código (denominado código base) que debe incrustarse en el HTML del sitio web para poder cargar las funcionalidades de la biblioteca.

En general, los códigos base para las tecnologías de marketing ejecutan alguna variante del siguiente proceso al cargarse en el sitio:

1. Configure una función global que pueda utilizarse para interactuar con la biblioteca del proveedor.
1. Cargue la biblioteca del proveedor.
1. Realice una serie de llamadas iniciales en cola a la función global para la configuración y el seguimiento.

Cuando la función global se haya configurado inicialmente, aún podrá realizar llamadas a la función antes de que finalice la carga de la biblioteca. Todas las llamadas que realice se añadirán al mecanismo de colocación en cola del código base y se ejecutarán en orden secuencial una vez que se cargue la biblioteca.

Una vez que la biblioteca termina de cargarse, la función global se sustituye por una nueva que evita la cola y, en su lugar, procesa inmediatamente cualquier llamada futura a la función.

### Ejemplo de código base

El siguiente código de JavaScript es un ejemplo de código base sin reducir para la [etiqueta de conversión de Pinterest](https://developers.pinterest.com/docs/ad-tools/conversion-tag/?), a la que se hará referencia más adelante en este documento para demostrar cómo se adapta el código base a las distintas estrategias de implementación con etiquetas:

```js
!function(scriptUrl) {
  if (!window.pintrk) {
    window.pintrk = function() {
      window.pintrk.queue.push(
        Array.prototype.slice.call(arguments)
      );
    };
    window.pintrk.queue = []; 
    window.pintrk.version = '3.0';
    var scriptElement = document.createElement('script');
    scriptElement.async = true;
    scriptElement.src = scriptUrl;
    var firstScriptElement = 
      document.getElementsByTagName('script')[0];
    firstScriptElement.parentNode.insertBefore(
      scriptElement, firstScriptElement
    );
  }
}('https://s.pinimg.com/ct/core.js');
pintrk('load', 'YOUR_TAG_ID');
pintrk('page');
```

En resumen, el código base anterior proporciona una [expresión de función invocada inmediatamente (IIFE)](https://developer.mozilla.org/es-ES/docs/Glossary/IIFE) que crea una función global para interactuar con la biblioteca (`window.pintrk`). También asigna a una variable `scriptURL` el valor de `https://s.pinimg.com/ct/core.js`, que es donde se encuentra la biblioteca. Como se ha explicado anteriormente, todas las funciones que se llaman antes de que se cargue la biblioteca se insertan en una cola (`window.pintrk.queue`) para ejecutarse en secuencia una vez que la biblioteca esté disponible.

La siguiente parte del código base es la más relevante a la hora de comprender cómo se carga la biblioteca en el sitio:

```js
var scriptElement = document.createElement("script");
scriptElement.async = true;
scriptElement.src = scriptUrl;
var firstScriptElement = 
  document.getElementsByTagName("script")[0];
firstScriptElement.parentNode.insertBefore(
  scriptElement, firstScriptElement
);
```

El código base crea un elemento de secuencia de comandos, lo configura para que se cargue de forma asíncrona y establece la dirección URL `src` en `https://s.pinimg.com/ct/core.js`. A continuación, añade el elemento de secuencia de comandos al documento insertándolo antes del primer elemento de secuencia de comandos que ya se encuentra en el documento.

## Opciones de implementación de etiquetas

Las secciones siguientes muestran las diferentes maneras de cargar bibliotecas de proveedores en sus extensiones utilizando el código base de Pinterest que se mostró anteriormente como ejemplo. Cada uno de estos ejemplos implica crear un [tipo de acción para una extensión web](./web/action-types.md) que cargue la biblioteca en el sitio web.

>[!NOTE]
>
>Aunque los ejemplos siguientes utilizan tipos de acción para fines de demostración, puede aplicar los mismos principios a cualquier función que cargue la biblioteca de etiquetas en su sitio web.


Los métodos disponibles son los siguientes:

- [Implementación de bibliotecas de terceros](#implementing-third-party-libraries)
   - [Requisitos previos](#prerequisites)
   - [Proceso de carga de código base](#base-code-loading-process)
      - [Ejemplo de código base](#base-code-example)
   - [Opciones de implementación de etiquetas](#tags-implementation-options)
      - [Cargar en tiempo de ejecución desde el host de proveedor {#vendor-host}](#load-at-runtime-from-the-vendor-host-vendor-host)
      - [Cargar en tiempo de ejecución desde el host de biblioteca de etiquetas](#load-at-runtime-from-the-tag-library-host)
      - [Incrustar la biblioteca directamente](#embed-the-library-directly)
   - [Pasos siguientes](#next-steps)

### Cargar en tiempo de ejecución desde el host de proveedor {#vendor-host}

El método más común para alojar la biblioteca de proveedores es utilizar la CDN del proveedor. Como el código base de la mayoría de las bibliotecas de proveedores ya está configurado para cargar la biblioteca desde la CDN del proveedor, puede configurar la extensión para cargar la biblioteca desde la misma ubicación.

Este método es generalmente el más fácil de mantener, ya que las actualizaciones que se realicen en el archivo en la CDN se cargarán automáticamente mediante la extensión.

Al utilizar este método, simplemente puede pegar todo el código base directamente en un tipo de acción como se muestra a continuación:

```js
module.exports = function() {
  !function(scriptUrl) {
    if (!window.pintrk) {
      window.pintrk = function() {
        window.pintrk.queue.push(
          Array.prototype.slice.call(arguments)
        );
      };
      window.pintrk.queue = []; 
      window.pintrk.version = "3.0";
      var scriptElement = document.createElement("script");
      scriptElement.async = true;
      scriptElement.src = scriptUrl;
      var firstScriptElement = 
        document.getElementsByTagName("script")[0];
      firstScriptElement.parentNode.insertBefore(
        scriptElement, firstScriptElement
      );
    }
  }("https://s.pinimg.com/ct/core.js");
  pintrk('load', 'YOUR_TAG_ID');
  pintrk('page');
};
```

De forma opcional, puede realizar pasos adicionales para cambiar el factor de esta implementación. Dado que las variables `scriptElement` y `firstScriptElement` ahora forman parte del ámbito de la función exportada, puede eliminar el IIFE, ya que estas variables no corren el riesgo de convertirse en globales.

Además, las etiquetas proporcionan varios [módulos principales](./web/core.md) que son utilidades que cualquier extensión puede utilizar. Específicamente, el módulo `@adobe/reactor-load-script` carga una secuencia de comandos desde una ubicación remota creando un elemento de secuencia de comandos y añadiéndolo al documento. Al utilizar este módulo para el proceso de carga de secuencias de comandos, puede redimensionar aún más el código de acción:

```js
var loadScript = require('@adobe/reactor-load-script');
var scriptUrl = 'https://s.pinimg.com/ct/core.js';
module.exports = function() {
  if (!window.pintrk) {
    window.pintrk = function() {
      window.pintrk.queue.push(
        Array.prototype.slice.call(arguments)
      );
    };
    window.pintrk.queue = []; 
    window.pintrk.version = "3.0";
    loadScript(scriptUrl);   
  }
  pintrk('load', 'YOUR_TAG_ID');
  pintrk('page');
};
```

### Cargar en tiempo de ejecución desde el host de biblioteca de etiquetas

Utilizar una CDN de un proveedor para el alojamiento de bibliotecas plantea varios riesgos: la CDN puede fallar, el archivo puede actualizarse con un error crítico en cualquier momento o puede verse comprometido por acciones malintencionadas.

Para resolver estos problemas, puede optar por incluir la biblioteca del proveedor como un archivo independiente dentro de la extensión. La extensión se puede configurar para que el archivo se aloje junto con la biblioteca principal de etiquetas. En tiempo de ejecución, la extensión carga la biblioteca del proveedor desde el mismo servidor que entregó la biblioteca principal al sitio web.

>[!IMPORTANT]
>
>En algunos casos, la biblioteca de proveedores puede cargar código adicional desde servidores de terceros, como sucede con la biblioteca de proveedores de Pinterest. En estos casos, agrupar la biblioteca de proveedores con su extensión podría no solucionar por completo todos los problemas relacionados con el riesgo.

Para implementar esto, primero debe descargar la biblioteca del proveedor en el equipo. En el caso de Pinterest, la biblioteca del proveedor se encuentra en [https://s.pinimg.com/ct/core.js](https://s.pinimg.com/ct/core.js). Una vez descargado el archivo, debe colocarlo dentro del proyecto de extensión. En el ejemplo siguiente, el archivo se denomina `pinterest.js` y se encuentra dentro de una carpeta `vendor` en el directorio del proyecto.

Una vez que el archivo de biblioteca esté en el proyecto, debe actualizar el [manifiesto de extensión](./manifest.md) (`extension.json`) para indicar que la biblioteca del proveedor debe entregarse junto con la biblioteca principal de etiquetas. Esto se realiza añadiendo la ruta al archivo de biblioteca dentro de una matriz `hostedLibFiles`:

```json
{
  "hostedLibFiles": ["vendor/pinterest.js"]
}
```

Finalmente, debe configurar el código de acción para cargar la biblioteca del proveedor desde el mismo servidor que aloja la biblioteca principal. El ejemplo siguiente utiliza el código de acción integrado en la [sección anterior](#vendor-host) como punto de partida. Al utilizar el [objeto de turbina](./turbine.md), debe pasar el nombre de archivo (sin ninguna ruta de acceso) del archivo de proveedor como se indica a continuación:

```js
var loadScript = require('@adobe/reactor-load-script');
var scriptUrl = turbine.getHostedLibFileUrl('pinterest.js');
module.exports = function() {
  if (!window.pintrk) {
    window.pintrk = function() {
      window.pintrk.queue.push(
        Array.prototype.slice.call(arguments)
      );
    };
    window.pintrk.queue = []; 
    window.pintrk.version = "3.0";
    loadScript(scriptUrl);   
  }
  pintrk('load', 'YOUR_TAG_ID');
  pintrk('page');
};
```

Es importante tener en cuenta que, al utilizar este método, debe actualizar manualmente el archivo de proveedor descargado cada vez que se actualice la biblioteca en su CDN y lanzar los cambios en una nueva versión de la extensión.

### Incrustar la biblioteca directamente

Puede evitar tener que cargar la biblioteca del proveedor por completo incrustando directamente el código de la biblioteca en el propio código de acción, lo que lo convierte en parte de la biblioteca principal de etiquetas. Utilizar este método aumenta el tamaño de la biblioteca principal, pero evita la necesidad de realizar una solicitud HTTP adicional para recuperar un archivo independiente.

Utilizando el código de acción integrado en la [sección anterior](#vendor-host) como punto de partida, puede reemplazar la línea donde se carga la secuencia de comandos con el contenido de la propia secuencia de comandos:

```js
module.exports = function() {
  if (!window.pintrk) {
    window.pintrk = function() {
      window.pintrk.queue.push(
        Array.prototype.slice.call(arguments)
      );
    };
    window.pintrk.queue = []; 
    window.pintrk.version = "3.0";
    // Paste the full vendor library code here.
  }
  pintrk('load', 'YOUR_TAG_ID');
  pintrk('page');
};
```

## Pasos siguientes

Este documento proporciona una visión general de los diferentes métodos para alojar bibliotecas de terceros en las extensiones de etiquetas. Aunque los ejemplos proporcionados se centraban en las bibliotecas, estas técnicas se aplican a cualquier parte de código que su extensión pueda utilizar.

Consulte la documentación relacionada en esta guía para obtener más información sobre las herramientas que puede utilizar para configurar las extensiones, incluidos los tipos de acciones, el manifiesto de extensión, los módulos principales y el objeto de turbina.
