---
title: Administrar parpadeo para experiencias personalizadas mediante el SDK web de Adobe Experience Platform
description: Aprenda a utilizar el SDK web de Adobe Experience Platform para administrar el parpadeo en las experiencias del usuario.
keywords: target;parpadeo;prehideStyle;asincrónicamente;asincrónico;
exl-id: f4b59109-df7c-471b-9bd6-7082e00c293b
source-git-commit: e5d279397cab30e997103496beda5265520dca77
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---

# Administrar parpadeo

Al intentar procesar contenido de personalización, el SDK debe asegurarse de que no haya parpadeo. El parpadeo, también llamado FOOC (Flash del contenido original), se produce cuando se muestra brevemente un contenido original antes de que aparezca la alternativa durante las pruebas o la personalización. El SDK intenta aplicar estilos CSS a elementos de la página para garantizar que dichos elementos estén ocultos hasta que el contenido de personalización se represente correctamente.

La funcionalidad de administración de parpadeo tiene algunas fases:

1. Preocultado
1. Preprocesamiento
1. Renderización

## Preocultado

Durante la fase de preocultación, el SDK utiliza la variable `prehidingStyle` para crear una etiqueta de estilo HTML y anexarla al DOM para asegurarse de que las grandes partes de la página están ocultas. Si no está seguro de qué partes de la página se personalizarán, se recomienda configurar `prehidingStyle` a `body { opacity: 0 !important }`. Esto garantiza que toda la página esté oculta. Sin embargo, esto tiene el inconveniente de llevar a un rendimiento de procesamiento de página peor informado por herramientas como Faro, Pruebas de páginas web, etc. Para obtener el mejor rendimiento de procesamiento de página, se recomienda configurar `prehidingStyle` a una lista de elementos de contenedor que contienen las partes de la página que se van a personalizar.

Suponiendo que tiene una página de HTML como la de abajo y solo lo sabe `bar` y `bazz` los elementos de contenedor se personalizarán:

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

## Preprocesamiento

La fase de preprocesamiento se inicia una vez que el SDK ha recibido el contenido personalizado del servidor. Durante esta fase, la respuesta se preprocesa, asegurándose de que los elementos que deben contener contenido personalizado estén ocultos. Una vez que estos elementos están ocultos, la etiqueta de estilo de HTML que se ha creado en función de la variable `prehidingStyle` se elimina y se muestran el cuerpo del HTML o los elementos de contenedor ocultos.

## Renderización

Después de que todo el contenido de personalización se haya procesado correctamente o si se ha producido algún error, se muestran todos los elementos ocultos anteriormente para garantizar que no haya elementos ocultos en la página que el SDK haya ocultado.

## Administración del parpadeo cuando el SDK se carga de forma asíncrona

La recomendación es cargar siempre el SDK de forma asíncrona para obtener el mejor rendimiento de procesamiento de página. Sin embargo, esto tiene algunas implicaciones para la renderización del contenido personalizado. Cuando el SDK se carga de forma asíncrona, es necesario utilizar el fragmento de ocultamiento previo. El fragmento de preocultación debe añadirse antes del SDK en la página HTML. Este es un ejemplo de fragmento que oculta todo el cuerpo:

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

Para asegurarse de que el cuerpo del HTML o los elementos del contenedor no estén ocultos durante un período de tiempo prolongado, el fragmento de ocultamiento previo utiliza un temporizador que, de forma predeterminada, elimina el fragmento después de `3000` milisegundos. La variable `3000` milisegundos es el tiempo de espera máximo. Si la respuesta del servidor se ha recibido y procesado antes, la etiqueta de estilo del HTML de ocultamiento previo se elimina lo antes posible.
