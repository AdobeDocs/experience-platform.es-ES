---
title: Vistas en extensiones web
description: Obtenga información sobre cómo definir vistas para módulos de biblioteca en las extensiones web de Adobe Experience Platform
exl-id: 4471df3e-75e2-4257-84c0-dd7b708be417
source-git-commit: 41efcb14df44524b58be2293d2b943bd890c1621
workflow-type: tm+mt
source-wordcount: '2083'
ht-degree: 98%

---

# Vistas en extensiones web

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

Cada tipo de evento, condición, acción o elemento de datos puede proporcionar una vista que permita al usuario proporcionar la configuración. La extensión también puede tener una [vista de configuración de extensión](../configuration.md) de nivel superior que permita a los usuarios proporcionar la configuración global de toda la extensión. El proceso de creación de una vista es idéntico en todos los tipos de vistas.

## Inclusión de un tipo de documento

Asegúrese de incluir una etiqueta `doctype` en el archivo HTML. Normalmente, esto implica que el archivo HTML comience como se indica a continuación:

```xml
<!DOCTYPE html>
```

## Inclusión de las etiquetas de la secuencia de scripts de iframe

Incluya el script iframe de las etiquetas en el código HTML de su vista:

```html
<script src="https://assets.adobedtm.com/activation/reactor/extensionbridge/extensionbridge.min.js"></script>
```

Este script proporciona una API de comunicación que permite a la vista comunicarse con la aplicación de las etiquetas.

## Registro con la API de comunicación de puente de extensión

Una vez que se haya cargado el script de iframe, deberá proporcionar a las etiquetas algunos métodos que utilizará para la comunicación. Llame a `window.extensionBridge.register` y pase un objeto como se indica a continuación:

```js
window.extensionBridge.register({
  init: function(info) {
    // Populate view with info.settings which will exist if the user is editing something
    // that was previously saved.
    if (info.settings) {
      document.getElementById('name').value = info.settings.name;
    }
  },
  validate: function() {
    // Return whether the view is valid.
    return document.getElementById('name').value.length > 0;
  },
  getSettings: function() {
    // Return user-provided settings.
    return {
      name: document.getElementById('name').value
    };
  }
});
```

Deberá modificar el contenido de cada uno de los métodos para adaptarlo a los requisitos particulares de su vista.

### [!DNL init]

Las etiquetas llamárán al método `init` en cuanto la vista se haya cargado en el iframe. Se pasará un solo argumento (`info`) que debe ser un objeto que contenga las propiedades siguientes:

| Propiedad | Descripción |
| --- | --- |
| `settings` | Objeto que contiene opciones de configuración que se guardaron anteriormente desde esta vista. Si `settings` es `null`, quiere decir que el usuario está creando la configuración inicial en lugar de cargar una versión guardada. Si `settings` es un objeto, debe utilizarlo para rellenar la vista, ya que el usuario está optando por editar la configuración mantenida anteriormente. |
| `extensionSettings` | Configuración guardada desde la vista de configuración de la extensión. Esto puede resultar útil para acceder a las opciones de configuración de extensión de vistas que no son la vista de configuración de extensión. Si la vista actual es la vista de configuración de la extensión, utilice `settings`. |
| `propertySettings` | Objeto que contiene la configuración de la propiedad. Consulte la [guía del objeto turbine](../turbine.md#property-settings) para obtener más información sobre el contenido de este objeto. |
| `tokens` | Objeto que contiene tokens de API. Para acceder a las API de Adobe desde la vista, normalmente deberá utilizar un token IMS en `tokens.imsAccess`. Este token solo estará disponible para las extensiones desarrolladas por Adobe. Si es usted un empleado de Adobe que representa una extensión creada por Adobe, [envíe un correo electrónico al equipo de ingenería de recopilación de datos](mailto:reactor@adobe.com) y proporcione el nombre de la extensión para que podamos añadirla a la lista de permitidos. |
| `company` | Objeto que contiene una sola propiedad, `orgId`, que representa su Adobe Experience Cloud ID (cadena alfanumérica de 24 caracteres). |
| `schema` | Objeto con el formato [Esquema JSON](https://json-schema.org/). Este objeto provendrá del [manifiesto de extensión](../manifest.md) y puede resultar útil para validar el formulario. |

La vista debe utilizar esta información para procesar y administrar su formulario. Es probable que solo necesite tratar con `info.settings`, aunque también se proporciona la otra información por si es necesario.

### [!DNL validate]

Se llamará al método `validate` después de que el usuario pulse el botón Guardar. Debe devolver uno de los elementos siguientes:

* Un valor booleano que indica si la entrada del usuario es válida.
* Una promesa de resolución posterior con un valor booleano que indica si la entrada del usuario es válida.

Depende de usted, como desarrollador de la extensión, determinar qué constituye una entrada válida, ya que el módulo de biblioteca actuará en función de dicha entrada.

Si los datos introducidos por el usuario no son válidos, esto es algo que debe indicarse en la vista para que los usuarios sepan qué es lo que se debe corregir.

### [!DNL getSettings]

Se llamará al método `getSettings` después de que el usuario pulse el botón Guardar y valide la vista. La función debe devolver uno de los elementos siguientes:

* Un objeto que contenga la configuración en función de la entrada del usuario.
* Una promesa de resolución posterior con un objeto que contenga la configuración basada en los datos introducidos por el usuario.

Este objeto de configuración se emitirá más adelante en la biblioteca de tiempo de ejecución de etiquetas. El contenido de este objeto está a su discreción. El objeto debe ser serializable y deserializable desde y hacia JSON. Los valores como las funciones o las instancias de [RegExp](https://developer.mozilla.org/es-ES/docs/Web/JavaScript/Reference/Global_Objects/RegExp) no cumplen estos criterios y, por lo tanto, no están permitidos.

## Utilización de las vistas compartidas

El objeto `window.extensionBridge` tiene varios métodos que le permiten aprovechar las ventajas que ofrecen las vistas existentes disponibles mediante las etiquetas para que no tenga que reproducirlas en su vista. Los métodos disponibles son los siguientes:

### [!DNL openCodeEditor]

```js
window.extensionBridge.openCodeEditor().then(function(code) { 
  console.log(code);
});
```

Al llamar a este método se mostrará un modal que permite al usuario editar un fragmento de código. Cuando el usuario haya terminado de editar el código, la promesa se resolverá con el código actualizado. Si el usuario cierra el editor de código sin guardar los cambios, la promesa nunca se resolverá. El objeto `options` debe estructurarse de la manera siguiente:

| Propiedad | Descripción |
| --- | --- |
| `code` | Código que debe mostrarse en el editor. Esto generalmente se proporciona cuando el usuario está editando el código existente. Si no se proporciona, el editor de código estará vacío cuando se abra. |
| `language` | Idioma del código que se editará. Las opciones válidas son `javascript`, `html`, `css`, `json` y `plaintext`. Si no se proporciona esto, se tomará el valor `javascript`. |

### [!DNL openRegexTester]

```js
window.extensionBridge.openRegexTester().then(function(pattern) { 
  console.log(pattern);
});
```

Al llamar a este método, se mostrará un modal que permite al usuario probar y modificar un patrón de expresión regular. Cuando el usuario haya terminado de editar la expresión regular, la promesa se resolverá con el patrón de expresión regular actualizado. Si el usuario cierra el comprobador de Regex sin guardar los cambios, la promesa nunca se resolverá. El objeto `options` debe contener las propiedades siguientes:

| Propiedad | Descripción |
| --- | --- |
| `pattern` | Patrón de expresión regular que debe utilizarse como valor inicial del campo de patrón dentro del comprobador. Normalmente, esto se proporciona cuando el usuario está editando una expresión regular existente. Si no se proporciona, el campo de patrón estará vacío inicialmente. |
| `flags` | Indicadores de expresión regular que debe utilizar el probador. Como ejemplo, `gi` indicaría el indicador de coincidencia global y el indicador de omisión de mayúsculas y minúsculas. Estos indicadores no son modificables por el usuario dentro del comprobador, pero se utilizan para mostrar los indicadores específicos que la extensión utilizará al ejecutar la expresión regular. Si no se proporciona, no se utilizarán indicadores dentro del comprobador. Consulte la [documentación de RegExp de MDN](https://developer.mozilla.org/es-ES/docs/Web/JavaScript/Reference/Global_Objects/RegExp) para obtener más información sobre los indicadores de expresiones regulares.<br><br>Un escenario común es una extensión que permite a los usuarios alternar entre mayúsculas y minúsculas para una expresión regular. Para admitir esto, la extensión suele incluir una casilla de verificación dentro de su vista de extensión que, al activarse, no hace distinción entre mayúsculas y minúsculas (representada por el indicador `i`). El objeto de configuración guardado por la vista tendría que representar si la casilla de verificación se marcó para que el módulo de biblioteca que ejecuta la expresión regular pueda saber si debe utilizar el indicador `i`. Además, cuando la vista de extensión desee abrir el comprobador de expresión regular, deberá pasar el indicador `i` si se marca la casilla de verificación para no hacer distinción entre mayúsculas y minúsculas. Esto permite al usuario probar correctamente la expresión regular con la omisión de distinción entre mayúsculas y minúsculas habilitada. |

### [!DNL openDataElementSelector] {#open-data-element}

```js
window.extensionBridge.openDataElementSelector().then(function(dataElement) { 
  console.log(dataElement);
});
```

Al llamar a este método se mostrará un modal que permite al usuario seleccionar un elemento de datos. Cuando el usuario haya terminado de seleccionar un elemento de datos, la promesa se resolverá con el nombre del elemento de datos seleccionado (de forma predeterminada, el nombre se incluirá entre símbolos de porcentaje). Si el usuario cierra el selector de elementos sin guardar los cambios, la promesa nunca se resolverá.

El objeto `options` debe contener una sola propiedad booleana, `tokenize`. Esta propiedad indica si el nombre del elemento de datos seleccionado debe incluirse entre símbolos de porcentaje antes de resolver la promesa. Consulte la sección sobre [elementos de datos de soporte](#supporting-data-elements) para ver por qué esto puede resultar de utilidad. Esta opción toma el valor predeterminado `true`.

## Elementos de datos complementarios {#supporting-data-elements}

Es probable que sus vistas tengan campos de formulario en los que los usuarios deseen utilizar elementos de datos. Por ejemplo, si la vista tiene un campo de texto en el que el usuario debe introducir un nombre de producto, puede que no tenga sentido que el usuario escriba un valor incrustado en el campo. En su lugar, es posible que deseen que el valor del campo sea dinámico (determinado en tiempo de ejecución) y utilizar un elemento de datos para ello.

Como ejemplo, supongamos que vamos a crear una extensión que envía una señalización para rastrear una conversión. Supongamos también que uno de los datos que envía nuestra señalización es un nombre de producto. Es probable que nuestra vista de extensión que permite al usuario configurar la señalización tenga un campo de texto para el nombre del producto. Normalmente, no tendría mucho sentido que el usuario de Platform escribiese un nombre de producto estático como &quot;Calzone Oven XL&quot;, puesto que el nombre del producto probablemente dependa de la página desde la que se enviará la señalización. Este es un excelente caso para utilizar un elemento de datos.

Si un usuario desea utilizar el elemento de datos denominado `productname` para el valor del nombre del producto, puede escribir el nombre del elemento de datos con símbolos de porcentaje a ambos lados (`%productname%`). Nos referimos al nombre del elemento de datos acortado con signos de porcentaje como un “token de elemento de datos”. Los usuarios de Platform suelen estar familiarizados con esta construcción. La extensión, a su vez, guardaría el token del elemento de datos dentro del objeto `settings` que exporta. El objeto de configuración puede tener el aspecto siguiente:

```js
{
  productName: '%productname%'
}
```

En tiempo de ejecución, antes de pasar el objeto de configuración al módulo de biblioteca, se analiza el objeto de configuración y se reemplazan los tokens de elemento de datos por sus valores respectivos. Si en el tiempo de ejecución, el valor del elemento de datos `productname` fuese `Ceiling Medallion Pro 2000`, el objeto de configuración que se pasaría al módulo de biblioteca sería el siguiente:

```js
{
  productName: 'Ceiling Medallion Pro 2000'
}
```

Para indicar a los dónde puede resultar útil utilizar elementos de datos y facilitar la introducción de un elemento de datos, se recomienda añadir un botón de icono junto a dichos campos, tal como se muestra a continuación:

![Campo de elemento de datos](../images/data-element-field.png)

>[!NOTE]
>
>Para descargar el icono correspondiente, vaya a la página [página iconos en el Espectro de Adobe](https://spectrum.adobe.com/page/icons/) y busque &quot;[!DNL Data]&quot;.

Cuando un usuario selecciona el botón que se encuentra junto al campo de texto, se realiza una llamada a `window.extensionBridge.openDataElementSelector`, tal como se ha [descrito anteriormente](#open-data-element). Esto mostrará una lista de los elementos de datos del usuario entre los que el usuario puede elegir en lugar de obligarlos a recordar el nombre y los símbolos de porcentaje. Una vez que el usuario haya seleccionado un elemento de datos, recibirá el nombre del elemento de datos seleccionado escrito entre símbolos de porcentaje (a menos que haya configurado la opción `tokenize` como `false`). Se recomienda rellenar el campo de texto con el resultado.

### Sustitución de tokens de elementos de datos

Como se ha descrito anteriormente, si un objeto de configuración persistente consta de lo siguiente:

```js
{
  productName: '%productname%'
}
```

Y, en tiempo de ejecución, el valor del elemento de datos `productname` fuese `Ceiling Medallion Pro 2000`, el objeto de configuración que se pasaría al módulo de biblioteca sería el siguiente:

```js
{
  productName: 'Ceiling Medallion Pro 2000'
}
```

Siempre que se encuentra un valor dentro de un objeto de configuración compuesto por un símbolo de porcentaje, una cadena y un símbolo de porcentaje, _y nada más_, este reemplaza por el valor del elemento de datos _sin cambiar el tipo del valor del elemento de datos_.

Por ejemplo, si el valor de `productname` en tiempo de ejecución fuese en su lugar el número `538` (no una cadena), el objeto de configuración que se pasaría al módulo de biblioteca sería el siguiente:

```js
{
  productName: 538
}
```

Tenga en cuenta que el `538` resultante es un número y no una cadena. Del mismo modo, si el valor del elemento de datos en tiempo de ejecución fuese una función (un caso de uso poco frecuente pero posible), el objeto de configuración resultante sería el siguiente:

```js
{
  productName: function() { … }
}
```

Por otro lado, supongamos que el objeto de configuración persistente fuese el siguiente:

```js
{
  productName: '%productname% - %modelnumber%'
}
```

En este caso, como el valor de `productName` es más que un token de elemento de datos único, el resultado siempre será una cadena. Cada token de elemento de datos se reemplazará por su valor respectivo tras convertirse en cadena. Si, en el tiempo de ejecución, el valor de `productname` fuese `Ceiling Medallion Pro` (una cadena) y `modelnumber` fuese `2000` (un número), el objeto de configuración resultante pasado al módulo de la biblioteca sería el siguiente:

```js
{
  productName: 'Ceiling Medallion Pro - 2000'
}
```

## Evitar la navegación

La comunicación entre la vista de extensión y la interfaz de usuario de recopilación de datos contenedora depende de que no se produzca navegación dentro de la vista de extensión. Por lo tanto, evite añadir contenido a la vista de extensión que permita al usuario navegar fuera de la página HTML de la vista de la extensión. Por ejemplo, si proporciona un vínculo en la vista de extensión, asegúrese de que abra una nueva ventana del explorador (esto se consigue añadiendo `target="_blank"` a la etiqueta de anclaje). Si decide utilizar un elemento `form` dentro de la vista de extensión, asegúrese de que el formulario nunca se envíe. El envío del formulario puede producirse accidentalmente si tiene un elemento `button` dentro del formulario y no se añade `type="button"`. Si se envía un formulario dentro de la vista de extensión, el documento HTML se actualizará, lo que provocará que se interrumpa la experiencia del usuario.
