---
title: Tipos de evento para extensiones web
description: Obtenga información sobre cómo definir un módulo de biblioteca de tipo evento para una extensión web en Adobe Experience Platform.
exl-id: dbdd1c88-5c54-46be-9824-2f15cce3d160
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 70%

---

# Tipos de eventos para extensiones web

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

En una regla de etiqueta, un evento es una actividad que debe producirse para que se active una regla. Por ejemplo, una extensión web podría proporcionar un tipo de evento de &quot;gesto&quot; que supervise la producción de un determinado gesto táctil o movimiento del ratón. Una vez que se produce el gesto, la lógica de evento activaría la regla.

Un módulo de biblioteca de tipo de evento está diseñado para detectar cuándo se produce una actividad y, a continuación, llamar a una función para activar una regla asociada. El evento que detecta se puede personalizar. Por ejemplo, puede detectar cuándo un usuario realiza un gesto determinado, se desplaza rápidamente o interactúa con algo.

Este documento explica cómo definir tipos de eventos para una extensión web en Adobe Experience Platform.

>[!NOTE]
>
>Este documento supone que se ha familiarizado con los módulos de la biblioteca y con la forma en que se integran con las extensiones web. Consulte la información general sobre el [formato del módulo de biblioteca](./format.md) para obtener una introducción a su implementación antes de volver a esta guía.

Los tipos de eventos se definen mediante extensiones y suelen consistir en lo siguiente:

1. Una [vista](./views.md) que se muestra en la IU del Experience Platform y en la IU de recopilación de datos y que permite a los usuarios modificar la configuración del evento.
2. Módulo de biblioteca que se emite dentro de la biblioteca de tiempo de ejecución de la etiqueta para interpretar la configuración y supervisar que se produzca una determinada actividad.

Las `module.exports` aceptan los parámetros `settings` y `trigger`. Esto permite la personalización del tipo de evento.

```js
module.exports = function(settings, trigger) { … };
```

| Parámetro | Descripción |
| --- | --- |
| `settings` | Objeto que contiene cualquier configuración que el usuario ha configurado en la vista del tipo de evento. Usted tiene el control final sobre lo que va a este objeto. |
| `trigger` | Una función que el módulo debe llamar cada vez que se debe activar la regla. Existe una relación uno a uno entre un objeto `settings`, una función `trigger` y una regla. En otras palabras, la función desencadenadora que recibió para una regla no se puede usar para activar una regla diferente. |

>[!NOTE]
>
>La función exportada se llamará una vez para cada regla que se haya configurado para usar el tipo de evento.

Con el paso de la actividad de cinco segundos como ejemplo, después de cinco segundos, la actividad se ha realizado y la regla se activará. El módulo tendrá un aspecto similar al de este ejemplo.

```js
module.exports = function(settings, trigger) {
  setTimeout(trigger, 5000);
};
```

Si desea que el usuario de Adobe Experience Platform pueda configurar la duración, se requiere la opción para introducir y guardar una duración en el objeto de configuración. El objeto podría tener este aspecto:

```js
{
  "duration": 25000
}
```

Para poder trabajar con la duración definida por el usuario, el módulo debería actualizarse para incluir esto.

```js
module.exports = function(settings, trigger) {
  setTimeout(trigger, settings.duration);
};
```

## Paso de datos de evento contextual

Cuando se activa una regla, suele ser útil proporcionar detalles adicionales acerca del evento que se ha producido. Los usuarios que crean reglas pueden encontrar útil esta información para lograr un determinado comportamiento. Por ejemplo, si un experto en marketing desea crear una regla en la que se envíe una baliza de análisis cada vez que el usuario desliza la pantalla. La extensión tendría que proporcionar un tipo de evento `swipe` para que el experto en marketing pueda utilizarlo para activar la regla adecuada. Suponiendo que el experto en marketing desee incluir el ángulo en el que se produjo el deslizamiento en la baliza, sería difícil hacerlo sin proporcionar información adicional. Para proporcionar información adicional sobre el evento que se produjo, pase un objeto al llamar a la función `trigger`. Por ejemplo:

```js
trigger({
  swipeAngle: 90 // the value would be the detected angle
});
```

El experto en marketing podría utilizar este valor en una baliza de análisis especificando el valor `%event.swipeAngle%` en un campo de texto. También pueden acceder a `event.swipeAngle` desde otros contextos (como una acción de código personalizado). Es posible incluir otros tipos de información de evento opcional que puedan ser útiles para un experto en marketing de la misma manera.

### [!DNL nativeEvent]

Si el tipo de evento se basa en un evento nativo (por ejemplo, si la extensión proporcionó un tipo de evento `click`), se recomienda configurar la propiedad `nativeEvent` de la siguiente manera.

```js
trigger({
  nativeEvent: nativeEvent // the value would be the underlying native event
});
```

Esto puede resultar útil para los expertos en marketing que intentan acceder a cualquier información del evento nativo, como las coordenadas del cursor.©

### [!DNL element]

Si existe una fuerte relación entre un elemento y el evento que se produjo, se recomienda establecer la propiedad `element` en el nodo DOM del elemento. Por ejemplo: supongamos que la extensión proporciona un tipo de evento `click` y que permite a los expertos en marketing modificar la configuración para que la regla se active únicamente si se selecciona un elemento con el ID de `herobanner`. En este caso, si el usuario selecciona el banner a pantalla completa, se recomienda llamar a `trigger` y establecer `element` en el nodo DOM del banner a pantalla completa.

```js
trigger({
  element: element // the value would be the DOM node
});
```

## Respeto del orden de reglas

Las etiquetas permiten a los usuarios ordenar reglas. Por ejemplo, un usuario puede crear dos reglas que utilicen el tipo de evento de cambio de orientación y personalizar el orden en que se activan las reglas. Suponiendo que el usuario de Adobe Experience Platform especifica un valor de pedido de `2` para el evento de cambio de orientación en la regla A y un valor de pedido de `1` para el evento de cambio de orientación en la regla B. Esto indica que, cuando la orientación cambia en un dispositivo móvil, la Regla B debe activarse antes que la Regla A (las reglas con valores de orden inferior deben activarse primero).

Como se mencionó anteriormente, la función exportada en nuestro módulo de evento se llamará una vez para cada regla que se haya configurado para utilizar nuestro tipo de evento. Cada vez que se llama a la función exportada, se pasa una función `trigger` única vinculada a una regla específica. En el escenario que se acaba de describir, se llamará una vez a nuestra función exportada con una función `trigger` vinculada a la regla B y, a continuación, otra vez con una función `trigger` vinculada a la regla A. La regla B es la primera porque el usuario le ha dado un valor de orden inferior al de la regla A. Cuando nuestro módulo de biblioteca detecta un cambio de orientación, es importante que llamemos a las funciones `trigger` en el mismo orden en que se proporcionaron al módulo de biblioteca.

En el código de ejemplo siguiente, observe que cuando se detecta un cambio de orientación, las funciones desencadenadoras se llaman en el mismo orden en que se proporcionaron a la función exportada:

```js
var triggers = [];

window.addEventListener('orientationchange', function() {
  triggers.forEach(function(trigger) {
    trigger();
  });
});

module.exports = function(settings, trigger) {
  triggers.push(trigger);
};
```

Esto garantiza que se mantenga el orden especificado por el usuario.

Una implementación incorrecta sería aquella que llama a las funciones desencadenadoras en orden diferente:

```js
var triggers = [];

window.addEventListener('orientationchange', function() {
  for (var i = triggers.length - 1; i >= 0; i--) {
    triggers[i]();
  }
});

module.exports = function(settings, trigger) {
  triggers.push(trigger);
};
```

Las prácticas de programación natural suelen mantener el orden adecuado, pero es importante tener en cuenta las consecuencias y desarrollar en consecuencia,
