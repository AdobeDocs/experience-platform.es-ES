---
title: Representación de contenido personalizado
seo-title: Adobe Experience Platform Web SDK Representación de contenido personalizado
description: Obtenga información sobre cómo procesar contenido personalizado con el SDK web de la plataforma de experiencia
seo-description: Obtenga información sobre cómo procesar contenido personalizado con el SDK web de la plataforma de experiencia
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (Beta) Representación de contenido personalizado

>[!IMPORTANT]
>
>El SDK web de la plataforma de experiencia de Adobe se encuentra en fase beta y no está disponible para todos los usuarios. La documentación y la funcionalidad están sujetas a cambios.

El SDK procesa automáticamente el contenido personalizado cuando envía un evento al servidor y lo establece `viewStart` como `true` opción en el evento.

```javascript
alloy("event", {
  "viewStart": true,
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
});
```

El procesamiento del contenido personalizado es asincrónico, por lo que no debe haber ninguna suposición cuando una parte concreta del contenido forma parte de la página.

## Administración del parpadeo

Al intentar representar contenido de personalización, el SDK debe asegurarse de que no hay parpadeo. El parpadeo, también llamado FOOC (Flash of Original Content), se produce cuando se muestra brevemente un contenido original antes de que aparezca la alternativa durante la prueba o personalización. El SDK intenta aplicar estilos CSS a elementos de la página para garantizar que dichos elementos se ocultan hasta que el contenido de personalización se procese correctamente.

La funcionalidad de administración de parpadeo tiene algunas fases:

1. Preocultado
1. Preprocesamiento
1. Representación

### Preocultado

Durante la fase de ocultación previa, el SDK utiliza la opción de configuración para crear una etiqueta de estilo HTML y anexarla al DOM para asegurarse de que grandes partes de la página están ocultas. `prehidingStyle` Si no está seguro de qué partes de la página se personalizarán, se recomienda establecer `prehidingStyle` en `body { opacity: 0 !important }`. Esto garantiza que toda la página esté oculta. Sin embargo, esto tiene el inconveniente de llevar a un peor rendimiento de procesamiento de página informado por herramientas como Lighthouse, Pruebas de página Web, etc. Para obtener el mejor rendimiento de representación de página, se recomienda establecer `prehidingStyle` en una lista de elementos contenedores que contengan las partes de la página que se personalizarán.

Suponiendo que tiene una página HTML como la de abajo y sabe que solo se personalizarán los elementos `bar` y `bazz` contenedores:

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

Entonces el `prehidingStyle` debe ser ajustado a algo como `#bar, #bazz { opacity: 0 !important }`.

### Preprocesamiento

La fase de preprocesamiento comienza una vez que el SDK ha recibido el contenido personalizado del servidor. Durante esta fase, la respuesta se preprocesa, asegurándose de que los elementos que deben contener contenido personalizado estén ocultos. Una vez ocultos estos elementos, se elimina la etiqueta de estilo HTML que se ha creado en función de la opción de configuración y se muestra el cuerpo HTML o los elementos de contenedor ocultos. `prehidingStyle`

### Representación

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

Para asegurarse de que el cuerpo HTML o los elementos del contenedor no están ocultos durante un período de tiempo prolongado, el fragmento de ocultamiento previo utiliza un temporizador que, de forma predeterminada, elimina el fragmento después de `3000` milisegundos. Los `3000` milisegundos son el tiempo de espera máximo. Si la respuesta del servidor se ha recibido y procesado antes, la etiqueta de estilo HTML oculta previamente se eliminará lo antes posible.
