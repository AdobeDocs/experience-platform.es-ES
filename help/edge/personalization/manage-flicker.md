---
title: Administrar parpadeo para experiencias personalizadas mediante el SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo utilizar el SDK web de Adobe Experience Platform para administrar el parpadeo en las experiencias de los usuarios.
keywords: destinatario;parpadeo;anteocultamientoEstilo;asincrónico;asincrónico;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---


# Administrar parpadeo

Al intentar representar contenido de personalización, el SDK debe asegurarse de que no hay parpadeo. El parpadeo, también llamado FOOC (Flash del contenido original), se produce cuando se muestra brevemente un contenido original antes de que aparezca la alternativa durante la prueba/personalización. El SDK intenta aplicar estilos CSS a elementos de la página para garantizar que dichos elementos se ocultan hasta que el contenido de personalización se procese correctamente.

La funcionalidad de administración de parpadeo tiene algunas fases:

1. Preocultado
1. Preprocesamiento
1. Renderización

## Preocultado

Durante la fase de ocultación previa, el SDK utiliza la opción de configuración `prehidingStyle` para crear una etiqueta de estilo HTML y anexarla al DOM para asegurarse de que grandes partes de la página están ocultas. Si no está seguro de qué partes de la página se personalizarán, se recomienda establecer `prehidingStyle` en `body { opacity: 0 !important }`. Esto garantiza que toda la página esté oculta. Sin embargo, esto tiene el inconveniente de llevar a un peor rendimiento de procesamiento de página informado por herramientas como Lighthouse, Pruebas de página Web, etc. Para obtener el mejor rendimiento de representación de página, se recomienda establecer `prehidingStyle` en una lista de elementos de contenedor que contengan las partes de la página que se personalizarán.

Suponiendo que tiene una página HTML como la de abajo y sabe que sólo se personalizarán los elementos de contenedor `bar` y `bazz`:

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

Luego el `prehidingStyle` debe configurarse en algo como `#bar, #bazz { opacity: 0 !important }`.

## Preprocesamiento

La fase de preprocesamiento se inicia una vez que el SDK ha recibido el contenido personalizado del servidor. Durante esta fase, la respuesta se preprocesa, asegurándose de que los elementos que deben contener contenido personalizado estén ocultos. Una vez ocultos estos elementos, se elimina la etiqueta de estilo HTML que se ha creado en función de la opción de configuración `prehidingStyle` y se muestra el cuerpo HTML o los elementos de contenedor ocultos.

## Renderización

Una vez que todo el contenido de personalización se ha procesado correctamente o si se ha producido algún error, se muestran todos los elementos ocultos anteriormente para garantizar que no haya elementos ocultos en la página que hayan sido ocultos por el SDK.

## Administración del parpadeo cuando el SDK se carga asincrónicamente

La recomendación es cargar siempre el SDK de forma asíncrona para obtener el mejor rendimiento de representación de página. Sin embargo, esto tiene algunas implicaciones para la representación de contenido personalizado. Cuando el SDK se carga asincrónicamente, es necesario utilizar el fragmento de ocultación previa. El fragmento de ocultación previa debe agregarse antes del SDK en la página HTML. Este es un ejemplo de fragmento que oculta todo el cuerpo:

```html
<script>
  !function(e,a,n,t){
    if (a) return;
    var i=e.head;if(i){
    var o=e.createElement("style");
    o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),
    setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
    (document, document.location.href.indexOf("mboxEdit") !== -1, "body { opacity: 0 !important }", 3000);
</script>
```

Para asegurarse de que el cuerpo HTML o los elementos de contenedor no están ocultos durante un período de tiempo prolongado, el fragmento de ocultamiento previo utiliza un temporizador que, de forma predeterminada, elimina el fragmento después de `3000` milisegundos. El `3000` milisegundos es el tiempo de espera máximo. Si la respuesta del servidor se ha recibido y procesado antes, la etiqueta de estilo HTML oculta previamente se eliminará lo antes posible.
