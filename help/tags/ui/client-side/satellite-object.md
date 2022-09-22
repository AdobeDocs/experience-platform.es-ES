---
title: Referencia de objeto satelital
description: Obtenga información sobre el objeto _satellite del lado del cliente y las diversas funciones que puede realizar con él en las etiquetas.
exl-id: f8b31c23-409b-471e-bbbc-b8f24d254761
source-git-commit: 0c2ee3bbb4d85bd755b4847a509fc7bd50ba67bc
workflow-type: tm+mt
source-wordcount: '1291'
ht-degree: 79%

---

# Referencia de objeto satélite

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

Este documento sirve como referencia para el objeto `_satellite` del lado del cliente y las diversas funciones que puede realizar con él.

## `track`

**Código**

```javascript
_satellite.track(identifier: string [, detail: *] )
```

**Ejemplo**

```javascript
_satellite.track('contact_submit', { name: 'John Doe' });
```

`track` activa todas las reglas utilizando el tipo de evento Direct Call que se ha configurado con el identificador dado de la extensión de etiqueta Core. El ejemplo anterior activa todas las reglas utilizando un tipo de evento Direct Call en el que el identificador configurado es `contact_submit`. También se transmite un objeto opcional que contiene información relacionada. Se puede acceder al objeto de detalle introduciendo `%event.detail%` en un campo de texto en una condición o acción o `event.detail` dentro del editor de código en una condición o acción Custom Code.

## `getVar`

**Código**

```javascript
_satellite.getVar(name: string) => *
```

**Ejemplo**

```javascript
var product = _satellite.getVar('product');
```

En el ejemplo proporcionado, si existe un elemento de datos con un nombre que coincida, se devuelve el valor del elemento de datos. Si no existe ningún elemento de datos que coincida, se verifica si se ha establecido previamente una variable personalizada con un nombre que coincida usando `_satellite.setVar()`. Si se encuentra una variable personalizada que coincida, se devuelve su valor.

>[!NOTE]
>
>Puede utilizar el porcentaje (`%`) para hacer referencia a variables para muchos campos de formulario en la interfaz de usuario de la recopilación de datos, lo que reduce la necesidad de llamar a `_satellite.getVar()`. Por ejemplo, al usar `%product%` accederá al valor del elemento de datos del producto o de la variable personalizada.

Cuando un evento déclencheur una regla, puede pasar la regla correspondiente `event` a `_satellite.getVar()` así:

```javascript
// event refers to the calling rule's event
var rule = _satellite.getVar('return event rule', event);
```

## `setVar`

**Código**

```javascript
_satellite.setVar(name: string, value: *)
```

**Ejemplo**

```javascript
_satellite.setVar('product', 'Circuit Pro');
```

`setVar()` establece una variable personalizada con un nombre y un valor determinados. Más adelante se puede acceder al valor de la variable mediante `_satellite.getVar()`.

Si lo desea, puede configurar varias variables a la vez transmitiendo un objeto donde las claves sean nombres de variable y los valores sean los valores de variable correspondientes.

```javascript
_satellite.setVar({ 'product': 'Circuit Pro', 'category': 'hobby' });
```

## `getVisitorId`

**Código**

```javascript
_satellite.getVisitorId() => Object
```

**Ejemplo**

```javascript
var visitorIdInstance = _satellite.getVisitorId();
```

Si la extensión [!DNL Adobe Experience Cloud ID] está instalada en la propiedad, este método devuelve la instancia de ID de visitante. Consulte la documentación [del servicio de Experience Cloud ID](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=es) para obtener más información.

## `logger`

**Código**

```javascript
_satellite.logger.log(message: string)
```

```javascript
_satellite.logger.info(message: string)
```

```javascript
_satellite.logger.warn(message: string)
```

```javascript
_satellite.logger.error(message: string)
```

**Ejemplo**

```javascript
_satellite.logger.error('No product ID found.');
```

El objeto `logger` permite registrar un mensaje en la consola del explorador. El mensaje se muestra únicamente si el usuario habilita la depuración de etiquetas (llamando a `_satellite.setDebug(true)` o utilizando una extensión adecuada del explorador).

### Registro de advertencias de obsolescencia

```javascript
_satellite.logger.deprecation(message: string)
```

**Ejemplo**

```javascript
_satellite.logger.deprecation('This method is no longer supported, please use [new example] instead.');
```

Registra una advertencia en la consola del explorador. El mensaje aparece independientemente de si el usuario ha habilitado o no la depuración de etiquetas.

## `cookie` {#cookie}

`_satellite.cookie` contiene funciones para leer y escribir cookies. Es una copia expuesta de la biblioteca de terceros js-cookie. Para obtener más información sobre el uso avanzado de esta biblioteca, consulte la [documentación de js-cookie](https://www.npmjs.com/package/js-cookie#basic-usage).

### Configurar una cookie {#cookie-set}

Para configurar una cookie, use `_satellite.cookie.set()`.

**Código**

```javascript
_satellite.cookie.set(name: string, value: string[, attributes: Object])
```

>[!NOTE]
>
>En el [`setCookie`](#setCookie) para configurar cookies, el tercer argumento (opcional) de esta llamada a la función era un entero que indicaba el tiempo de vida (TTL) de la cookie en días. En este nuevo método, se acepta un objeto &quot;attributes&quot; como tercer argumento. Para configurar un TTL para una cookie mediante el nuevo método, debe proporcionar una variable `expires` en el objeto attributes y establézcalo en el valor deseado. Esto se muestra en el siguiente ejemplo.

**Ejemplo**

La siguiente llamada de función escribe una cookie que caduca en una semana.

```javascript
_satellite.cookie.set('product', 'Circuit Pro', { expires: 7 });
```

### Recuperar una cookie {#cookie-get}

Para recuperar una cookie, utilice `_satellite.cookie.get()`.

**Código**

```javascript
_satellite.cookie.get(name: string) => string
```

**Ejemplo**

La siguiente llamada de función lee una cookie previamente establecida.

```javascript
var product = _satellite.cookie.get('product');
```

### Eliminar una cookie {#cookie-remove}

Para eliminar una cookie, utilice `_satellite.cookie.remove()`.

**Código**

```javascript
_satellite.cookie.remove(name: string)
```

**Ejemplo**

La siguiente llamada de función elimina una cookie previamente establecida.

```javascript
_satellite.cookie.remove('product');
```

## `buildInfo`

**Código**

```javascript
_satellite.buildInfo
```

Este objeto contiene información acerca de la compilación de la biblioteca de tiempo de ejecución de etiquetas actual. El objeto contiene las siguientes propiedades:

### `turbineVersion`

Proporciona la versión de [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine) utilizada dentro de la biblioteca actual.

### `turbineBuildDate`

La fecha ISO 8601 en que se creó la versión de [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine) utilizada dentro del contenedor.

### `buildDate`

La fecha ISO 8601 en que se creó la biblioteca actual.

Este ejemplo muestra los valores de los objetos:

```javascript
{
  turbineVersion: "14.0.0",
  turbineBuildDate: "2016-07-01T18:10:34Z",
  buildDate: "2016-03-30T16:27:10Z"
}
```

## `environment`

Este objeto contiene información sobre el entorno en el que se implementa la biblioteca de tiempo de ejecución de etiquetas actual.

**Código**

```javascript
_satellite.environment
```

El objeto contiene las siguientes propiedades:

```javascript
{
  id: "ENbe322acb4fc64dfdb603254ffe98b5d3",
  stage: "development"
}
```

| Propiedad | Descripción |
| --- | --- |
| `id` | ID del entorno. |
| `stage` | El entorno para el que se creó esta biblioteca. Los valores posibles son `development`, `staging`y `production`. |

## `notify`

>[!NOTE]
>
>Este método se ha desaprobado. Utilice `_satellite.logger.log()` en su lugar.

**Código**

```javascript
_satellite.notify(message: string[, level: number])
```

**Ejemplo**

```javascript
_satellite.notify('Hello world!');
```

`notify` registra un mensaje en la consola del explorador. El mensaje se muestra únicamente si el usuario habilita la depuración de etiquetas (llamando a `_satellite.setDebug(true)` o utilizando una extensión adecuada del explorador).

Se puede transmitir un nivel de registro opcional que afecte al diseño y al filtrado del mensaje que se registra. Estos son los niveles compatibles:

3 - Mensajes informativos.

4 - Mensajes de advertencia.

5 - Mensajes de error.

Si no proporciona un nivel de registro ni transmite ningún otro valor de nivel, el mensaje se registra como mensaje normal.

## `setCookie` {#setCookie}

>[!IMPORTANT]
>
>Este método se ha desaprobado. Utilice [`_satellite.cookie.set()`](#cookie-set) en su lugar.

**Código**

```javascript
_satellite.setCookie(name: string, value: string, days: number)
```

**Ejemplo**

```javascript
_satellite.setCookie('product', 'Circuit Pro', 3);
```

Establece una cookie en el explorador del usuario. La cookie persistirá durante el número de días especificado.

## `readCookie`

>[!IMPORTANT]
>
>Este método se ha desaprobado. Utilice [`_satellite.cookie.get()`](#cookie-get) en su lugar.

**Código**

```javascript
_satellite.readCookie(name: string) => string
```

**Ejemplo**

```javascript
var product = _satellite.readCookie('product');
```

Lee una cookie desde el explorador del usuario.

## `removeCookie`

>[!NOTE]
>
>Este método se ha desaprobado. Utilice [`_satellite.cookie.remove()`](#cookie-remove) en su lugar.

**Código**

```javascript
_satellite.removeCookie(name: string)
```

**Ejemplo**

```javascript
_satellite.removeCookie('product');
```

Quita una cookie del explorador del usuario.

## Funciones de depuración

No se debe acceder a las siguientes funciones desde el código de producción. Se han diseñado únicamente con fines de depuración y cambian con el tiempo según sea necesario.

### `container`

**Código**

```javascript
_satellite._container
```

**Ejemplo**

>[!IMPORTANT]
>
>No se debe acceder a esta función desde el código de producción. Se ha diseñado únicamente con fines de depuración y cambia con el tiempo según sea necesario.

### `monitor`

**Código**

```javascript
_satellite._monitors
```

**Ejemplo**

>[!IMPORTANT]
>
>No se debe acceder a esta función desde el código de producción. Se ha diseñado únicamente con fines de depuración y cambia con el tiempo según sea necesario.

**Muestra**

En la página web que ejecuta una biblioteca de etiquetas, añada un fragmento de código al HTML. Normalmente, el código se inserta en el elemento `<head>` antes del elemento `<script>` que carga la biblioteca de etiquetas. Esto permite al monitor capturar los primeros eventos del sistema que se producen en la biblioteca de etiquetas. Por ejemplo:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <script>
    window._satellite = window._satellite || {};
    window._satellite._monitors = window._satellite._monitors || [];
    window._satellite._monitors.push({
      ruleTriggered: function (event) {
        console.log(
          'rule triggered',
          event.rule
        );
      },
      ruleCompleted: function (event) {
        console.log(
          'rule completed',
          event.rule
        );
      },
      ruleConditionFailed: function (event) {
        console.log(
          'rule condition failed',
          event.rule,
          event.condition
        );
      }
    });
  </script>
  <script src="//assets.adobedtm.com/launch-EN5bfa516febde4b22b3e7c6f96f6b439f.min.js"
          async></script>
</head>
<body>
  <h1>Click me!</h1>
</body>
</html>
```

En el primer elemento de script, ya que la biblioteca de etiquetas aún no se ha cargado, se crea el objeto `_satellite` inicial y se inicia una matriz en `_satellite._monitors`. A continuación, el script añade un objeto de monitor a esa matriz. El objeto de monitor puede especificar los siguientes métodos a los que la biblioteca de etiquetas llama posteriormente:

### `ruleTriggered`

Se llama a esta función después de que un evento desencadene una regla, pero antes de que se hayan procesado las condiciones y acciones de la regla. El objeto de evento transmitido a `ruleTriggered` contiene información sobre la regla activada.

### `ruleCompleted`

Se llama a esta función después de que una regla se haya procesado completamente. En otras palabras, el evento se ha producido, todas las condiciones se han transmitido y todas las acciones se han ejecutado. El objeto de evento enviado a `ruleCompleted` contiene información acerca de la regla que se ha completado.

### `ruleConditionFailed`

Se llama a esta función después de activar una regla y de que haya fallado una de sus condiciones. El objeto de evento transmitido a `ruleConditionFailed` contiene información sobre la regla activada y la condición que ha fallado.

Si se llama a `ruleTriggered`, se llama a `ruleCompleted` o `ruleConditionFailed` poco después.

>[!NOTE]
>
>Un monitor no tiene que especificar los tres métodos (`ruleTriggered`, `ruleCompleted` y `ruleConditionFailed`). Las etiquetas de Adobe Experience Platform funcionan con los métodos compatibles proporcionados por el monitor.

### Prueba del monitor

El ejemplo anterior especifica los tres métodos del monitor. Cuando se los llama, el monitor cierra la información relevante. Para probar esto, configure dos reglas en la biblioteca de etiquetas:

1. Una regla que tenga un evento de clic y una condición del explorador que se transmita únicamente si el explorador es [!DNL Chrome].
1. Una regla que tenga un evento de clic y una condición del explorador que se transmita únicamente si el explorador es [!DNL Firefox].

Si abre la página en [!DNL Chrome], abre la consola del explorador y selecciona la página, aparecerá lo siguiente en la consola:

![](../../images/debug.png)

Se pueden añadir nuevos enlaces o información adicional a estos controladores según sea necesario.
