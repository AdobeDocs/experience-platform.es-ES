---
title: Tipos de evento para extensiones web
description: Obtenga información sobre cómo definir un módulo de biblioteca de tipo evento para una extensión web en Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '1048'
ht-degree: 31%

---

# Tipos de eventos para extensiones web

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

En una regla de etiqueta, un evento es una actividad que debe producirse para que una regla se active. Por ejemplo, una extensión web podría proporcionar un tipo de evento de &quot;gesto&quot; que observe si se produce un determinado gesto de ratón o contacto. Una vez que se produce el gesto, la lógica de evento activaría la regla.

Un módulo de biblioteca de tipo de evento está diseñado para detectar cuándo se produce una actividad y, a continuación, llamar a una función para activar una regla asociada. El evento que se está detectando se puede personalizar. Por ejemplo, podría detectar cuándo un usuario realiza un gesto determinado, se desplaza rápidamente o interactúa con algo.

Este documento explica cómo definir tipos de eventos para una extensión web en Adobe Experience Platform.

>[!NOTE]
>
>Este documento supone que está familiarizado con los módulos de biblioteca y cómo se integran en las extensiones web. Consulte la información general sobre el [formato del módulo de biblioteca](./format.md) para obtener una introducción a su implementación antes de volver a esta guía.

Los tipos de eventos se definen mediante extensiones y suelen consistir en lo siguiente:

1. Se muestra una [vista](./views.md) en la interfaz de usuario de la recopilación de datos que permite a los usuarios modificar la configuración del evento.
2. Un módulo de biblioteca emitido dentro de la biblioteca de tiempo de ejecución de etiquetas para interpretar la configuración y observar que se produzca una determinada actividad.

`module.exports` acepte los  `settings` parámetros  `trigger` y . Esto permite la personalización del tipo de evento.

```js
module.exports = function(settings, trigger) { … };
```

| Parámetro | Descripción |
| --- | --- |
| `settings` | Objeto que contiene cualquier configuración que el usuario ha configurado en la vista del tipo de evento. Usted tiene el control final sobre lo que va a este objeto. |
| `trigger` | Una función que el módulo debe llamar cada vez que se debe activar la regla. Existe una relación uno a uno entre un objeto `settings`, una función `trigger` y una regla. Esto significa que la función de déclencheur que recibió para una regla no se puede usar para activar una regla diferente. |

>[!NOTE]
>
>La función exportada se llamará una vez para cada regla que se haya configurado para usar el tipo de evento.

Con la actividad de cinco segundos pasando como ejemplo, después de cinco segundos, la actividad se ha realizado y la regla se activará. El módulo tendrá un aspecto similar al de este ejemplo.

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

Para poder operar en la duración definida por el usuario, sería necesario actualizar el módulo para incluirlo.

```js
module.exports = function(settings, trigger) {
  setTimeout(trigger, settings.duration);
};
```

## Pasar datos de evento contextual

Cuando se activa una regla, suele ser útil proporcionar detalles adicionales sobre el evento que se ha producido. Los usuarios que crean reglas pueden encontrar útil esta información para lograr un determinado comportamiento. Por ejemplo, si un especialista en marketing desea crear una regla en la que se envíe una señalización de análisis cada vez que el usuario desliza la pantalla. La extensión tendría que proporcionar un tipo de evento `swipe` para que el especialista en marketing pueda utilizar este tipo de evento para almacenar en déclencheur la regla adecuada. Suponiendo que el especialista en marketing desee incluir el ángulo en el que se produjo el desliz en la señalización, sería difícil hacerlo sin proporcionar información adicional. Para proporcionar información adicional sobre el evento que se produjo, pase un objeto al llamar a la función `trigger`. Por ejemplo:

```js
trigger({
  swipeAngle: 90 // the value would be the detected angle
});
```

El experto en marketing podría utilizar este valor en una baliza de análisis especificando el valor `%event.swipeAngle%` en un campo de texto. También pueden acceder a `event.swipeAngle` desde otros contextos (como una acción de código personalizado). Es posible incluir otros tipos de información de evento opcional que puedan ser útiles para un especialista en marketing de la misma manera.

### [!DNL nativeEvent]

Si el tipo de evento se basa en un evento nativo (por ejemplo, si la extensión ha proporcionado un tipo de evento `click`), se recomienda establecer la propiedad `nativeEvent` de la siguiente manera.

```js
trigger({
  nativeEvent: nativeEvent // the value would be the underlying native event
});
```

Esto puede resultar útil para los expertos en marketing que intentan acceder a cualquier información del evento nativo, como las coordenadas del cursor.©

### [!DNL element]

Si existe una fuerte relación entre un elemento y el evento que se produjo, se recomienda establecer la propiedad `element` en el nodo DOM del elemento. Por ejemplo, si la extensión proporciona un tipo de evento `click` y permite que los especialistas en marketing lo configuren, la regla se activará únicamente si se selecciona un elemento con el ID `herobanner` . En este caso, si el usuario selecciona el banner a pantalla completa, se recomienda llamar a `trigger` y establecer `element` en el nodo DOM del banner a pantalla completa.

```js
trigger({
  element: element // the value would be the DOM node
});
```

## Respeto del orden de reglas

Las etiquetas permiten a los usuarios solicitar reglas. Por ejemplo, un usuario puede crear dos reglas que utilicen el tipo de evento de cambio de orientación y para personalizar el orden en que se activan las reglas. Suponiendo que el usuario de Adobe Experience Platform especifique un valor de orden de `2` para el evento de cambio de orientación en la Regla A y un valor de orden de `1` para el evento de cambio de orientación en la Regla B. Esto indica que cuando la orientación cambia en un dispositivo móvil, la Regla B debe activarse antes de la Regla A (las reglas con valores de orden inferior se activan primero).

Como se mencionó anteriormente, la función exportada en nuestro módulo de evento se llamará una vez para cada regla que se haya configurado para utilizar nuestro tipo de evento. Cada vez que se llama a la función exportada, se pasa una función `trigger` única vinculada a una regla específica. En el escenario que se acaba de describir, se llama una vez a nuestra función exportada con una función `trigger` vinculada a la regla B y otra con una función `trigger` vinculada a la regla A. La regla B va primero porque el usuario le ha dado un valor de orden inferior al de la regla A. Cuando nuestro módulo de biblioteca detecta un cambio de orientación, es importante que llamemos a las funciones `trigger` en el mismo orden en que se proporcionaron al módulo de biblioteca.

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
