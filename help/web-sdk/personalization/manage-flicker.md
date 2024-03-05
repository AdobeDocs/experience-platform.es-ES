---
title: Administración del parpadeo para experiencias personalizadas mediante el SDK web de Adobe Experience Platform
description: Aprenda a utilizar el SDK web de Adobe Experience Platform para administrar el parpadeo en las experiencias de los usuarios.
keywords: target;parpadeo;preocultando estilo;asincrónicamente;asíncrono;
exl-id: f4b59109-df7c-471b-9bd6-7082e00c293b
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 0%

---

# Administrar parpadeo

Al intentar procesar contenido de personalización, el SDK debe asegurarse de que no haya parpadeo. El parpadeo, también llamado FOOC (Flash del contenido original), se produce cuando se muestra un contenido original brevemente antes de que aparezca la alternativa durante las pruebas o la personalización. El SDK intenta aplicar estilos CSS a los elementos de la página para garantizar que dichos elementos estén ocultos hasta que el contenido de personalización se procese correctamente.

La forma de administrar el parpadeo depende de si implementa el SDK web de forma sincrónica o asincrónica. Compruebe la `<head>` etiqueta donde se implementa `alloy.js` o el cargador de etiquetas. La presencia del `async` en el `<script>` determina si el SDK web se carga asincrónicamente.

```html
<!-- This tag loads synchronously -->
<script src="https://assets.adobedtm.com/[...]/launch-example.min.js"></script>

<!-- This tag loads asynchronously -->
<script src="https://assets.adobedtm.com/[...]/launch-example.min.js" async></script>

<!-- This library loads synchronously -->
<script src="https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js"></script>

<!-- This library loads asynchronously -->
<script src="https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js" async></script>
```

## Administración del parpadeo para implementaciones sincrónicas

La administración sincrónica de parpadeos se divide en tres fases:

1. Preocultación
1. Preprocesamiento
1. Renderización

Durante el **fase preocultación**, el SDK utiliza el [`prehidingStyle`](../commands/configure/prehidingstyle.md) propiedad de configuración para crear una etiqueta de estilo de HTML y anexarla al DOM para asegurarse de que las secciones deseadas de la página estén ocultas. Si no está seguro de qué partes de la página se personalizarán, se recomienda configurar `prehidingStyle` hasta `body { opacity: 0 !important }`. Esto garantiza que toda la página esté oculta. Sin embargo, esto tiene el inconveniente de provocar un rendimiento de procesamiento de páginas peor reportado por herramientas como Lighthouse, Pruebas de páginas web, etc. Para obtener el mejor rendimiento de procesamiento de páginas, se recomienda establecer `prehidingStyle` a una lista de elementos contenedores que contienen las partes de la página que se personalizarán.

Suponiendo que tenga una página de HTML como la de abajo y solo lo sepa `bar` y `bazz` los elementos de contenedor siempre se personalizarán:

```html
<html>
  <head>
  </head>
  <body>
    <div id="foo">
      Foo foo foo
    </div>

    <div id="bar">
      Bar bar bar
    </div>

    <div id="bazz">
      Bazz bazz bazz
    </div>
  </body>
</html>
```

A continuación, el `prehidingStyle` debe configurarse como algo similar a `#bar, #bazz { opacity: 0 !important }`.

Una vez que el SDK ha recibido contenido personalizado del servidor, la variable **fase de preprocesamiento** comienza. Durante esta fase, la respuesta se preprocesa, asegurándose de que los elementos que deben contener contenido personalizado estén ocultos. Una vez ocultos estos elementos, la etiqueta de estilo de HTML creada en función de la variable `prehidingStyle` La opción de configuración se elimina y se muestran el cuerpo del HTML o los elementos de contenedor ocultos.

Después de que todo el contenido de personalización se haya representado correctamente, o si hubo algún error, la variable **fase de procesamiento** comienza. Se muestran todos los elementos ocultos anteriormente para asegurarse de que no haya elementos ocultos en la página que el SDK haya ocultado.

## Administrar el parpadeo en implementaciones asíncronas

La recomendación es cargar siempre el SDK de forma asíncrona para obtener el mejor rendimiento de procesamiento de páginas. Sin embargo, esto tiene algunas implicaciones para la renderización del contenido personalizado. Cuando el SDK se carga asincrónicamente, es necesario utilizar el fragmento de preocultación. El fragmento de preocultación debe añadirse antes del SDK en la página de HTML. A continuación se muestra un fragmento de ejemplo que oculta todo el cuerpo:

```html
<script>
  !function(e,a,n,t){
    if (a) return;
    var i=e.head;if(i){
    var o=e.createElement("style");
    o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),
    setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
    (document, document.location.href.indexOf("adobe_authoring_enabled") !== -1, "body { opacity: 0 !important }", 3000);
</script>
```

Para asegurarse de que el cuerpo del HTML o los elementos del contenedor no estén ocultos durante un período de tiempo prolongado, el fragmento de preocultación utiliza un temporizador que, de forma predeterminada, elimina el fragmento después de `3000` milisegundos. El `3000` milisegundos es el tiempo de espera máximo. Si la respuesta del servidor se ha recibido y procesado antes, la etiqueta de estilo del HTML de preocultación se elimina lo antes posible.
