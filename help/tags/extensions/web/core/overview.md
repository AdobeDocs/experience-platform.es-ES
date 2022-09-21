---
title: Información general de la extensión Core
description: Obtenga información acerca de la extensión de etiquetas de Core en Adobe Experience Platform.
exl-id: 841f32ad-a6a8-49fb-a131-ef4faab47187
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '5482'
ht-degree: 83%

---

# Información general de la extensión Core

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

La extensión de etiquetas Core es la extensión predeterminada lanzada con Adobe Experience Platform.

Este documento proporciona información sobre las opciones disponibles al utilizar la extensión Core para generar una regla.

## Tipos de eventos de la Extensión principal {#core-extension-event-types}

En este tema se describen los tipos de eventos disponibles en la Extensión principal. Para obtener más información sobre las opciones que se pueden configurar para distintos tipos de eventos, consulte la sección [Opciones](#options).

### Eventos basados en el explorador

#### Tab Blur

El evento de desenfoque de pestañas activa la acción cuando una pestaña pierde el enfoque. No hay configuraciones para este tipo de evento.

#### Tab Focus

El evento de enfoque de pestañas activa la acción cuando una pestaña recibe el enfoque. No hay configuraciones para este tipo de evento.

### Form

#### Blur

El evento de desenfoque activa la acción cuando un formulario pierde el enfoque. Consulte la sección [Opciones](#options) para obtener más información sobre la configuración de eventos personalizables.

#### Focus

El evento de enfoque activa la acción cuando un formulario recibe el enfoque. Consulte la sección [Opciones](#options) para obtener más información sobre la configuración de eventos personalizables.

#### Submit

El evento de envío activa la acción cuando se envía un formulario. Consulte la sección [Opciones](#options) para obtener más información sobre la configuración de eventos personalizables.

### Eventos controlados por teclado

#### Key Press

Se activa el evento cuando se pulsa una tecla. Consulte la sección [Opciones](#options) para obtener más información sobre la configuración de eventos personalizables.

### Eventos basados en medios

#### Media Ended

Se activa el evento cuando terminan los medios. Consulte la sección [Opciones](#options) para obtener más información sobre la configuración de eventos personalizables.

#### Datos cargados en medios

Se activa el evento cuando los medios cargan datos. Consulte la sección [Opciones](#options) para obtener más información sobre la configuración de eventos personalizables.

#### Media Pause

Se activa el evento cuando se pausa el medio. Consulte la sección [Opciones](#options) para obtener más información sobre la configuración de eventos personalizables.

#### Media Play

Se activa el evento cuando se reproduce el medio. Consulte la sección [Opciones](#options) para obtener más información sobre la configuración de eventos personalizables.

#### Media Stalled

Se activa el evento si se bloquean los medios. Consulte la sección [Opciones](#options) para obtener más información sobre la configuración de eventos personalizables.

#### Tiempo de medio reproducido

Se activa el evento si el medio se reproduce durante un periodo de tiempo determinado. Debe especificar la duración durante la cual se debe reproducir el medio para activar el evento. Consulte la sección [Opciones](#options) para obtener más información sobre la configuración de eventos personalizables.


#### Volumen del medio cambiado

Se activa el evento si el volumen aumenta o se reduce. Consulte la sección [Opciones](#options) para obtener más información sobre la configuración de eventos personalizables.

### Eventos orientados a dispositivos móviles

#### Orientation Change

El evento se déclencheur si cambia la orientación del dispositivo. Debe especificar la duración durante la cual debe cambiar la orientación para activar del evento. No hay configuraciones para este tipo de evento.

#### Zoom Change

Se activa el evento si el usuario amplía o reduce la imagen. No hay configuraciones para este tipo de evento.

### Eventos controlados con el ratón

#### Click

Se activa el evento si se selecciona el elemento especificado (al hacer clic). También se pueden especificar valores de propiedad que deben tener el valor “True” para el elemento antes de activar el evento.

`<a>`Si el elemento es una etiqueta de anclaje al contenido vinculado, también puede especificar si se retrasará la navegación durante un período de tiempo. Esto puede resultar útil si la regla requiere tiempo adicional para ejecutarse y normalmente no se completaría antes de que se navegue la página.

>[!WARNING]
>
>Esta opción debe utilizarse con extrema precaución debido a las posibles consecuencias negativas que puede tener para la experiencia del usuario si se utiliza incorrectamente.

Cuando se retrasa el vínculo, Platform impide que el explorador salga de la página. A continuación, realiza una redirección de JavaScript al destino original después del tiempo de espera especificado. Esto es especialmente peligroso cuando el marcado de la página tiene etiquetas `<a>` donde la funcionalidad deseada no aleja al usuario de la página. Si no puede resolver el problema de ninguna otra manera, debe ser extremadamente preciso en la definición del selector para que este evento se active exactamente donde lo necesita y no en otro lugar.

El valor de retraso del vínculo predeterminado es 100 milisegundos. Tenga en cuenta que las etiquetas siempre esperarán el tiempo especificado y no están conectadas a la ejecución de las acciones de la regla de ninguna manera. Es posible que el retraso obligue al usuario a esperar más tiempo del necesario y también que el retraso no sea lo suficientemente largo como para que todas las acciones de la regla se completen correctamente. Los retrasos más largos proporcionan más tiempo para la ejecución de reglas, pero también empeoran la experiencia del usuario.

Para corregir el retraso, es necesario proporcionar el elemento seleccionado que activa el evento y la cantidad de tiempo específica antes de activarlo.

Para ver las opciones avanzadas, consulte la sección [Opciones](#options) para obtener más información.

#### Hover

Se activa el evento si el usuario pasa el ratón sobre un elemento especificado. Además, configure si la regla se activa inmediatamente o después de un número determinado de milisegundos. Consulte la sección [Opciones](#options) para obtener más información sobre la configuración de eventos personalizables.

### Otros eventos

#### Custom Event

Se activa el evento si se produce un tipo de evento personalizado. Las funciones de JavaScript con nombre definidas en cualquier otra parte de la base de código pueden utilizarse como tipo de evento personalizado. Especifique el nombre del tipo de evento personalizado y, a continuación, configure las demás opciones como se describe en [Opciones](#options).

#### Data Element Changed

Se activa el evento si cambia un elemento de datos especificado. Debe proporcionar un nombre para el elemento de datos. Puede seleccionar el elemento de datos escribiendo su nombre en el campo de texto o seleccionando el icono de elemento de datos a la derecha del campo de texto y eligiendo de una lista proporcionada dentro del cuadro de diálogo que aparece.

#### Direct Call {#direct-call-event}

Un evento de llamada directa evita los sistemas de detección de eventos y búsqueda. Las reglas de Direct Call son perfectas para situaciones en las que desea decirle al sistema exactamente lo que está ocurriendo. Además, son ideales cuando el sistema no puede detectar un evento en el DOM.

Al definir un evento de llamada directa, debe especificar una cadena que actuará como identificador de este evento. Si [acción de llamada directa de déclencheur](#direct-call-action) que contenga el mismo identificador se activa, todas las reglas de evento de llamada directa que escuchen ese identificador se ejecutarán.

![Captura de pantalla de un evento de llamada directa en la interfaz de usuario de la recopilación de datos](../../../images/extensions/core/direct-call-event.png)

#### Element Exists

Se activa el evento si el elemento especificado existe. Consulte la sección [Opciones](#options) para obtener más información sobre la configuración de eventos personalizables.

#### Enters Viewport

Se activa el evento si el usuario entra en una ventanilla especificada. Debe proporcionar un selector de CSS como criterio para dirigirse a los elementos coincidentes. También debe configurar si la regla se activa inmediatamente o después de un número determinado de milisegundos, y si el evento debe activarse cada vez que se produzca el evento o solo la primera vez.

Consulte la sección [Opciones](#options) para obtener más información sobre la configuración de eventos personalizables.

#### History Change

El evento se activa si se produce un evento pushState o hashchange. No hay configuraciones para este tipo de evento.

#### Tiempo invertido en la página

Se activa el evento si el usuario permanece en la página durante una determinada cantidad de segundos. Especifique la cantidad de segundos que deben transcurrir antes de activar el evento.

### Eventos de carga de página

#### DOM Ready

Se activa el evento cuando el DOM está listo y el usuario puede interactuar con la página. No hay configuraciones para este tipo de evento.

#### Library Loaded (Page Top) {#library-loaded-page-top}

El evento se activa en cuanto se carga la biblioteca de etiquetas. No hay configuraciones para este tipo de evento.

#### Page Bottom {#page-bottom}

Se activa el evento una vez que se realiza la llamada a `_satellite.pageBottom();` Al cargar la biblioteca de etiquetas de forma asíncrona, no se debe utilizar este tipo de evento. No hay configuraciones para este tipo de evento.

#### Window Loaded

Se activa el evento cuando el explorador llama a onLoad y la página termina de cargarse. No hay configuraciones para este tipo de evento.

### Opciones {#options}

Cada uno de los tipos de eventos de formulario utiliza la siguiente configuración:

#### Specific Elements \| Any Element

* Si selecciona **[!UICONTROL Elementos específicos]**, aparecen las opciones para seleccionar los elementos y los valores de propiedad.
* Si selecciona **[!UICONTROL Cualquier elemento]**, no se necesitan más opciones para restringir los elementos.

#### Elements matching the CSS selector

Indique el selector de CSS que identifica los elementos que activan el evento.

#### And having certain property values

Si selecciona esta opción, aparecerán disponibles los siguientes parámetros:

* `property=value`

   Especifique el valor de la propiedad

* Regex

   Habilitar si `property=value` es una expresión regular.

* Add

   Añadir otro par de `property=value`.

#### Advanced options (Bubbling)

* Ejecute esta regla incluso cuando el evento se origine a partir de un elemento descendiente
* Permita que esta regla se ejecute incluso si el evento ya ha activado una regla para un elemento descendientes
* Una vez ejecutada la regla, se impide que el evento active reglas dirigidas a elementos antecesores

## Tipos de condición de la Extensión principal

Esta sección describe los tipos de condición disponibles en la Extensión principal. Estos tipos de condiciones se pueden usar con el tipo de lógica regular o de excepción.

### Datos

#### Cookie

Especifique el nombre y el valor de la cookie que deben darse para activar una acción con un evento.

1. Especifique un nombre de cookie.
1. Escriba el valor que debe darse en la cookie si el evento va a activar una acción.
1. (Opcional) Habilite Regex si es una expresión regular.

#### Custom Code

Especifique cualquier Custom Code que deba darse como condición del evento.

>[!NOTE]
>
>JavaScript ES6+ ahora se admite en código personalizado. Tenga en cuenta que algunos exploradores más antiguos no admiten ES6+. Para comprender el impacto del uso de las funciones ES6+, realice pruebas con todos los exploradores web compatibles.

Utilice el editor de código integrado para introducir el código personalizado:

1. Seleccione **[!UICONTROL Abrir editor]**.
1. Escriba el Custom Code.
1. Seleccione **[!UICONTROL Guardar]**.

Una variable denominada `event` estará disponible automáticamente y podrá hacer referencia a ella desde su Custom Code. El objeto `event` contendrá información útil sobre el evento que activó la regla. La forma más sencilla de determinar qué datos de eventos están disponibles es registrar `event` en la consola desde el código personalizado:

```javascript
console.log(event);
return true;
```

Ejecute la regla en un explorador e inspeccione el objeto de evento registrado en la consola del explorador. Una vez que sepa qué información está disponible, puede utilizarla para la toma de decisiones mediante programación dentro del Custom Code.

*Secuencia de condiciones*

Cuando la opción &quot;Run rule components in sequence&quot; de la configuración de propiedades está activada, puede hacer que los componentes de regla subsiguientes esperen mientras la condición realiza una tarea asincrónica.

Cuando la condición arroja una [promesa](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise), la siguiente condición de la regla no se ejecutará hasta que se resuelva la promesa que se muestra. Si se rechaza la promesa, las etiquetas consideran que la condición ha fallado y que no se ejecutarán más condiciones o acciones de esa regla.

Un ejemplo de una condición que arroja una promesa:

```javascript
return new Promise(function(resolve, reject) {
  setTimeout(function() {
    if (new Date().getDay() === 5) {
      resolve();
    } else {
      reject();
    }
  }, 1000);
});
```

#### Comparación de valor {#value-comparison}

Compara dos valores para determinar si esta condición devuelve el valor “True”.

Si tiene una regla con varias condiciones, es posible que esta condición devuelva el valor “True”, pero la regla no se activará porque las demás condiciones se evalúan como “False” o una de las excepciones como “True”.

1. Proporcione un valor.
1. Seleccione el operador. Consulte la lista de operadores de comparación de valores para obtener más información.
1. (Cuando sea necesario) Seleccione si la comparación debe distinguir entre mayúsculas y minúsculas.
1. Proporcione otro valor para la comparación.

Están disponibles los siguientes operadores de comparación de valores:

**Equal:** La condición devuelve el valor “True” si los dos valores son iguales usando una comparación no estricta (en JavaScript, el operador ==). Los valores pueden ser de cualquier tipo. Al escribir una palabra como _True_, _False_, _Null_ o _Undefined_ en un campo de valor, la palabra se compara como una cadena y no se convierte a su equivalente de JavaScript.

**Does Not Equal:** La condición devuelve el valor “True” si los dos valores no se igualan con una comparación no estricta (en JavaScript,operador !=). Los valores pueden ser de cualquier tipo. Al escribir una palabra como _True_, _False_, _Null_ o _Undefined_ en un campo de valor, la palabra se compara como una cadena y no se convierte a su equivalente de JavaScript.

**Contains:** La condición devuelve el valor “True” si el primer valor contiene el segundo valor. Los números se convierten en cadenas. Cualquier valor que no sea un número o una cadena provocará que la condición devuelva el valor “False”.

**Does Not Contain:** La condición devuelve el valor “True” si el primer valor no contiene el segundo valor. Los números se convierten en cadenas. Cualquier valor que no sea un número o una cadena dará como resultado que la condición devuelva el valor “True”.

**Starts With:** La condición devuelve el valor “True” si el primer valor empieza por el segundo valor. Los números se convierten en cadenas. Cualquier valor que no sea un número o una cadena provocará que la condición devuelva el valor “False”.

**Does Not Start With:** La condición devuelve el valor “True” si el primer valor no comienza con el segundo valor. Los números se convierten en cadenas. Cualquier valor distinto al número o cadena provoca que la condición devuelva el valor “True”.

**Ends With:** La condición devuelve el valor “True” si el primer valor termina con el segundo valor. Los números se convierten en cadenas. Cualquier valor que no sea un número o una cadena provocará que la condición devuelva el valor “False”.

**Does Not End With:** La condición devuelve el valor “True” si el primer valor no termina con el segundo valor. Los números se convierten en cadenas. Cualquier valor distinto al número o cadena provoca que la condición devuelva el valor “True”.

**Matches Regex:** La condición devuelve el valor “True” si el primer valor coincide con la expresión regular. Los números se convierten en cadenas. Cualquier valor que no sea un número o una cadena provocará que la condición devuelva el valor “False”.

**Does Not Match Regex:** La condición devuelve el valor “True” si el primer valor no coincide con la expresión regular. Los números se convierten en cadenas. Cualquier valor distinto al número o cadena provoca que la condición devuelva el valor “True”.

**Is Less Than:** La condición devuelve el valor “True” si el primer valor es menor que el segundo valor. Las cadenas que representan números se convierten en números. Cualquier valor que no sea un número o una cadena convertible provocará que la condición devuelva el valor “False”.

**Is Less Than Or Equal To:** La condición devuelve el valor “True” si el primer valor es menor o igual que el segundo valor. Las cadenas que representan números se convierten en números. Cualquier valor que no sea un número o una cadena convertible provocará que la condición devuelva el valor “False”.

**Is Greater Than:** La condición devuelve el valor “True” si el primer valor es mayor que el segundo valor. Las cadenas que representan números se convierten en números. Cualquier valor que no sea un número o una cadena convertible provocará que la condición devuelva el valor “False”.

**Is Greater Than Or Equal To:** La condición devuelve el valor “True” si el primer valor es mayor o igual que el segundo valor. Las cadenas que representan números se convierten en números. Cualquier valor que no sea un número o una cadena convertible provocará que la condición devuelva el valor “False”.

**Is True:** La condición devuelve el valor “True” si se trata de una condición booleana con el valor “True”. El valor que proporcione no se convierte en booleano si es de cualquier otro tipo. Cualquier valor que no sea booleano con el valor “True” provoca que se devuelva el valor “False”.

**Is Truthy:** La condición devuelve el valor “True” si el valor es “True” después de convertirse en un valor booleano. Consulte la documentación [MDN&#39;s Truthy](https://developer.mozilla.org/es-ES/docs/Glossary/Truthy) de MDN para ver ejemplos de valores “Truthy”.

**Is False:** La condición devuelve el valor “True” si se trata de una condición booleana con el valor “False”. El valor que proporcione no se convierte en booleano si es de cualquier otro tipo. Cualquier valor que no sea booleano con el valor “False” provoca que se devuelva el valor “False”.

**Is Falsy:** La condición devuelve el valor “True” si el valor es “False” después de convertirse en un valor booleano. Consulte la documentación [MDN&#39;s Falsy](https://developer.mozilla.org/es-ES/docs/Glossary/Falsy) para ver ejemplos de valores “Falsy”.

#### Variable

Especifique el nombre y el valor de la variable JavaScript que debe darse para activar una acción con un evento.

1. Especifique el nombre de la variable JavaScript.
1. Especifique el valor de la variable que debe darse como condición para el evento.
1. (Opcional) Habilite Regex si es una expresión regular.

### Participación

#### Landing Page

Especifique la página en la que el usuario debe aterrizar para activar el evento.

1. Especifique la página de aterrizaje.
1. (Opcional) Habilite Regex si es una expresión regular.

#### New/Returning Visitor

Especifique si el visitante debe ser un visitante nuevo o recurrente para que un evento active una acción.

Seleccione una de las siguientes opciones:

* New Visitor
* Returning Visitor

#### Page Views

Configure la cantidad de veces que el visitante debe ver la página antes de activar la acción.

1. Seleccione si el número de vistas de página debe ser mayor, igual o menor que el valor especificado.
1. Especifique la cantidad de vistas de página que determina si se cumple la condición.
1. Configure cuándo se cuentan las vistas de página seleccionando una de las siguientes opciones:
   * Lifetime
   * Current Session

#### Sessions

Se activa la acción si el número de sesiones del usuario cumple los criterios especificados.

1. Seleccione si el número de sesiones debe ser mayor, igual o menor que el valor especificado.
1. Especifique el número de sesiones que determinan si se cumple la condición.

#### Time On Site

Se activa la acción si el número de sesiones del usuario cumple los criterios especificados.

Configure cuánto tiempo debe estar el visitante en el sitio antes de activar la acción.

1. Seleccione si el número de minutos que el visitante está en el sitio debe ser mayor, igual o menor que el valor especificado.
1. Especifique la cantidad de minutos que determina si se cumple la condición.

#### Traffic Source

Se activa la acción si el número de sesiones del usuario cumple los criterios especificados.

Especifique la fuente del tráfico del visitante que debe tener el valor “True” para que se active la acción.

1. Especifique la fuente de tráfico.
1. (Opcional) Habilite Regex si es una expresión regular.

### Tecnología

#### Browser

Seleccione el explorador que el visitante debe utilizar para activar la acción.

Seleccione uno o varios de los siguientes exploradores:

* Chrome
* Firefox
* Internet Explorer/Edge
* Internet Explorer Mobile
* Mobile Safari
* OmniWeb
* Opera
* Opera Mini
* Opera Mobile
* Safari

#### Device Type

Seleccione el tipo de dispositivo que debe utilizar el visitante para que se active la acción.

Seleccione uno o varios de los siguientes tipos de dispositivos:

* Android
* BlackBerry
* Escritorio
* iPad
* iPhone
* iPod
* Nokia
* Windows Phone

#### Operating System

Seleccione el sistema operativo que el visitante debe utilizar para activar la acción.

Seleccione uno o varios de los siguientes sistemas operativos:

* Android
* BlackBerry
* iOS
* Linux
* MacOS
* Maemo
* Symbian OS
* Unix
* Windows

#### Screen Resolution

Seleccione la resolución de pantalla que deben utilizar los visitantes en sus dispositivos para activar la acción.

1. Seleccione si la anchura de resolución de pantalla del dispositivo del visitante debe ser mayor, igual o menor que el valor especificado.
1. Especifique el número de píxeles necesarios para la anchura de resolución de pantalla.
1. Seleccione si la altura de resolución de pantalla del dispositivo del visitante debe ser mayor, igual o menor que el valor especificado.
1. Especifique el número de píxeles necesarios para la altura de resolución de pantalla.

#### Window Size

Seleccione el tamaño de la ventana que deben utilizar los visitantes en sus dispositivos para que se active la acción.

1. Seleccione si el ancho de la ventana del dispositivo del visitante debe ser mayor, igual o menor que el valor especificado.
1. Especifique el número de píxeles necesarios para el ancho de tamaño de la ventana.
1. Seleccione si la altura del tamaño de la ventana del dispositivo del visitante debe ser mayor, igual o menor que el valor especificado.
1. Especifique el número de píxeles necesarios para la altura del tamaño de la ventana.

### URL

#### Domain

Especifique el dominio del visitante.

#### Hash

Especifique uno o varios patrones hash que deben darse en la dirección URL.

>[!NOTE]
>
>Una condición OR permite unir varios patrones hash.

1. Especifique el patrón hash.
1. (Opcional) Habilite Regex si es una expresión regular.
1. Añada cualquier otro patrón hash.

#### Ruta And Query String

Especifique una o más rutas que deben darse en la dirección URL. Esto incluye Path And Query String.

>[!NOTE]
>
>Las rutas múltiples se unen mediante una condición OR.

1. Especifique la ruta.
1. (Opcional) Habilite Regex si es una expresión regular.
1. Añada otras rutas.

#### Path Without Query String

Especifique una o más rutas que deben darse en la dirección URL. Esto incluye la ruta, pero no la cadena de consulta.

>[!NOTE]
>
>Las rutas múltiples se unen mediante una condición OR.

1. Especifique la ruta.
1. (Opcional) Habilite Regex si es una expresión regular.
1. Añada otras rutas.

#### Protocol

Especifique el protocolo utilizado en la dirección URL.

Seleccione una de las siguientes opciones:

* HTTP
* HTTPS

#### Query String Parameter

Especifique el URL Parameter utilizado en la URL.

1. Especifique un nombre de URL Parameter.
1. Especifique el valor utilizado para el URL Parameter.
1. (Opcional) Habilite Regex si es una expresión regular.

#### Subdomain

Especifique uno o varios subdominios que deben darse en la dirección URL.

>[!NOTE]
>
>Los subdominios múltiples se unen mediante una condición OR.

1. Especifique el subdominio.
1. (Opcional) Habilite Regex si es una expresión regular.
1. Añada cualquier otro subdominio.

### Otras

#### Date Range

Especifique un intervalo de fechas. Seleccione la fecha y la hora tras la que se produce el evento, la fecha antes de la que se produce y la zona horaria.

#### Max Frequency

Especifique el número máximo de veces que la condición devuelve el valor “True”. Puede seleccionar las siguientes opciones:

* Page view
* Sesiones
* Visitor
* Seconds
* Minutes
* Days
* Weeks
* Months

Para la frecuencia máxima 1 de condición por sesión, se comparan estos dos elementos `localStorage`. Si `visitorTracking.sessionCount` es mayor que el recuento de `maxFrequency.session`, la condición de muestreo es verdadera. Si son iguales, la condición es falsa.

`sessionCount` es un elemento `visitorTracking`, por lo que la API de visitante debe estar activada para que la condición de muestreo funcione.

#### Sampling

Especifique el porcentaje del tiempo que la condición devuelve true.

## Tipos de acción de Extensión principal

En esta sección se describen los tipos de acción disponibles en la Extensión principal.

### Código personalizado

>[!NOTE]
>
>JavaScript ES6+ ahora se admite en código personalizado. Tenga en cuenta que algunos exploradores más antiguos no admiten ES6+. Para comprender el impacto del uso de las funciones ES6+, realice pruebas con todos los exploradores web compatibles.

Proporcione el código que se ejecuta después de activar el evento y de evaluar las condiciones.

1. Asigne un nombre al código de acción.
1. Seleccione el idioma utilizado para definir la acción:
   * JavaScript
   * HTML
1. Seleccione si desea ejecutar el código de acción globalmente.
1. Seleccione **[!UICONTROL Abrir editor]**.
1. Edite el código y, a continuación, haga clic en **[!UICONTROL Guardar]**.

Cuando se selecciona JavaScript como idioma, estará disponible automáticamente una variable denominada `event` y podrá hacer referencia a ella desde su Custom Code. El objeto `event` contendrá información útil sobre el evento que activó la regla. La forma más sencilla de determinar qué datos de eventos están disponibles es registrar `event` en la consola desde el código personalizado:

```javascript
console.log(event);
```

Ejecute la regla en un explorador e inspeccione el objeto de evento registrado en la consola del explorador. Después de saber qué información está disponible, puede utilizarla para la toma de decisiones mediante programación dentro del código personalizado, el envío de una parte del objeto `event` a un servidor, etc.

### Procesamiento de acciones de Custom Code

La extensión principal, disponible para todos los usuarios de Adobe Experience Platform, contiene una acción de código personalizado para ejecutar JavaScript o HTML proporcionados por el usuario. A menudo, es útil que los usuarios comprendan cómo se procesan las reglas con acciones de Custom Code.

#### Reglas que utilizan los eventos Page Top o Page Bottom

El código de las acciones personalizadas está incrustado en la biblioteca principal de etiquetas. El código se escribe en el documento usando document.write. Si una regla tiene varias acciones Custom Code, el código se escribe en el orden configurado en la regla.

#### Reglas que utilizan cualquier evento distinto a Page Top o Page Bottom

El código de las acciones personalizadas se carga desde el servidor y se escribe en el documento mediante [Postscribe](https://github.com/krux/postscribe). Si una regla tiene varias acciones Custom Code, el código se carga en paralelo desde el servidor, pero se escribe en el orden configurado en la regla.

Cuando se utiliza document.write después de que una página se haya cargado normalmente, no supone un problema para el código proporcionado mediante acciones de Custom Code. Puede utilizar document.write dentro de las acciones de Custom Code independientemente de cuándo se ejecuta el código.

#### Validación de Custom Code

El validador utilizado en el editor de código de etiquetas se ha diseñado para identificar los problemas con el código escrito por el desarrollador. El código que ha pasado por un proceso de reducción (como el código AppMeasurement.js descargado del Administrador de códigos) puede recibir falsas advertencias sobre problemas por el validador que generalmente se pueden ignorar.

#### Secuencia de acciones

Cuando la opción &quot;Run rule components in sequence&quot; de la configuración de propiedades está activada, puede hacer que los componentes de regla subsiguientes esperen mientras la acción realiza una tarea asincrónica.  Esto funciona de forma diferente para un Custom Code JavaScript y HTML.

*JavaScript*

Al crear una acción de Custom Code de JavaScript, puede devolver una [promesa](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) de su acción. La acción siguiente de la regla se ejecutará únicamente cuando se resuelva la promesa proporcionada. Si se rechaza la promesa, no se ejecutarán las siguientes acciones de la regla.

>[!NOTE]
>
>Esto solo funciona cuando JavaScript no está configurado para ejecutarse globalmente. Si está ejecutando la acción de código personalizado en el ámbito global, las etiquetas tratarán la promesa como resuelta inmediatamente y pasará al siguiente elemento de la cola de procesamiento.

Ejemplo de una acción de Custom Code de JavaScript que arroja una promesa:

```javascript
return new Promise(function(resolve, reject) {
  setTimeout(function() {
    if (new Date().getDay() === 5) {
      resolve();
    } else {
      reject();
    }
  }, 1000);
});
```

*HTML*

Al crear una acción de Custom Code HTML, una función denominada `onCustomCodeSuccess()` estará disponible para usar en el Custom Code. Puede llamar a esta función para indicar que el código personalizado se ha completado y que las etiquetas pueden pasar a ejecutar acciones posteriores. Por otro lado, si el Custom Code falla de alguna manera, puede llamar a `onCustomCodeFailure()`. Esto informará a las etiquetas que no ejecuten las acciones posteriores a esa regla.

Ejemplo de una acción de Custom Code HTML que utiliza las llamadas de retorno nuevas:

```html
<script>
setTimeout(function() {
  if (new Date().getDay() === 5) {
    onCustomCodeSuccess();
  } else {
    onCustomCodeFailure();
  }
}, 1000);
</script>
```

### Llamada directa de déclencheur {#direct-call-action}

Esta acción déclencheur todas las reglas que utilizan una [evento de llamada directa](#direct-call-event). Al configurar la acción, debe proporcionar la cadena de identificador para el evento de llamada directa que desee almacenar en déclencheur. De forma opcional, también puede pasar datos al evento de llamada directa a través de un `detail` , que puede contener un conjunto personalizado de pares de clave-valor.

![Captura de pantalla de una acción de llamada directa de Déclencheur en la interfaz de usuario de recopilación de datos](../../../images/extensions/core/direct-call-action.png)

La acción se asigna directamente a la variable [`track` method](../../../ui/client-side/satellite-object.md?lang=en#track) en el `satellite` , a la que se puede acceder mediante código del lado del cliente.

## Tipos de Data Elements de Extensión principal

Los tipos de Data Elements están determinados por la extensión. No hay límite para los tipos que se pueden crear.

Las secciones siguientes describen los tipos de Data Elements disponibles en la Extensión principal. Otras extensiones utilizan tipos de Data Elements diferentes.

### Cookie

Es posible hacer referencia a cualquier cookie de dominio disponible en el campo de nombre de cookie.

#### Ejemplo:

`cookieName`

### Constante

Cualquier valor de cadena constante al que se pueda hacer referencia en acciones o condiciones.

#### Ejemplo:

`string`

### Custom Code

>[!NOTE]
>
>JavaScript ES6+ ahora se admite en código personalizado. Tenga en cuenta que algunos exploradores más antiguos no admiten ES6+. Para comprender el impacto del uso de las funciones ES6+, realice pruebas con todos los exploradores web compatibles.

Puede introducir código JavaScript personalizado en la IU si selecciona la opción Abrir editor e inserta código en la ventana del editor.

Se debe incluir una sentencia de retorno en la ventana del editor para indicar qué valor se tiene que usar como valor del elemento de datos. Si no se incluye una sentencia de retorno o se devuelve el valor `null` o `undefined`, el valor predeterminado del elemento de datos se utilizará como valor del elemento de datos.

**Ejemplo:**

```javascript
var pageType = $('div.page-wrapper').attr('class').split('')[1];
if (window.location.pathname == '/') {
  return 'homepage';
} else {
  return pageType;
}
```

Si se recupera el elemento de datos de Custom Code como parte de una ejecución de regla, estará disponible automáticamente una variable denominada `event` a la que podrá hacer referencia desde el Custom Code. El objeto `event` contendrá información útil sobre el evento que activó la regla. La forma más sencilla de determinar qué datos de eventos están disponibles es registrar `event` en la consola desde el código personalizado:

```javascript
console.log(event);
return true;
```

Ejecute la regla en un explorador e inspeccione el objeto de evento registrado en la consola del explorador. Una vez que sepa qué información está disponible bajo las distintas reglas que pueden utilizar el elemento de datos, puede utilizarla para la toma de decisiones mediante programación dentro del código personalizado o devolver una parte del objeto `event` como valor del elemento de datos.

### Atributo DOM

Es posible recuperar cualquier elemento, como una etiqueta H1 o div.

#### Ejemplo:

Cadena de selector de CSS:

`id#dc logo img`

Obtener el valor de:

`src`

### Variable de JavaScript

Es posible hacer referencia a cualquier objeto JavaScript o variable mediante el campo de ruta.

Los elementos de datos de etiquetas se pueden utilizar para capturar las variables de JavaScript de marcado o las propiedades de objeto. Estos valores se pueden usar dentro de las extensiones o reglas personalizadas haciendo referencia a los elementos de datos de etiquetas. Si la fuente de los datos cambia, solo es necesario actualizar la referencia a la fuente.

En el ejemplo siguiente, el marcado contiene una variable de JavaScript llamada `Page_Name`.

```markup
<script>
  //data layer
  var Page_Name = "Homepage"
</script>
```

Cuando cree el elemento de datos, simplemente proporcione la ruta a esa variable.

Si utiliza un objeto de recopilación de datos como parte de la capa de datos, utilice la notación de puntos en la ruta para hacer referencia al objeto y la propiedad que desea capturar en el elemento de datos, como `_myData.pageName`o `digitalData.pageName`, etc.

#### Ejemplo:

`window.document.title`

### Almacenamiento local

Proporcione el nombre del elemento de almacenamiento local en el campo Local Storage Item Name.

El almacenamiento local proporciona a los exploradores una forma de almacenar información de página a página ([https://www.w3schools.com/html/html5_webstorage.asp](https://www.w3schools.com/html/html5_webstorage.asp)). El almacenamiento local funciona de forma muy similar a las cookies, pero es mucho más amplio y flexible.

Utilice el campo proporcionado para especificar el valor que ha creado para un elemento de almacenamiento local, como `lastProductViewed.`

### Objetos combinados

Seleccione varios elementos de datos que proporcionen un objeto. Estos objetos se combinarán en profundidad (recursivamente) para producir un nuevo objeto. Los objetos de origen no se modificarán. Si se encuentra una propiedad en la misma ubicación de varios objetos de origen, se utilizará el valor del último objeto. Si el valor de la propiedad de origen es `undefined`, no invalidará un valor de un objeto de origen anterior. Si las matrices se encuentran en la misma ubicación en varios objetos de origen, las matrices se concatenarán.

Por ejemplo, supongamos que selecciona un elemento de datos que proporciona el siguiente objeto:

```
{
  "sport": {
    "name": "tennis"
  },
  "dessert": "ice cream",
  "fruits": [
    "apple",
    "banana"
  ]
}
```

Supongamos que también selecciona otro elemento de datos que proporciona el siguiente objeto:

```
{
  "sport": {
    "name": "volleyball"
  },
  "dessert": undefined,
  "pet": "dog",
  "instrument": undefined,
  "fruits": [
    "cherry",
    "duku"
  ]
}
```

El resultado del elemento de datos Objetos combinados sería el siguiente objeto:

```
{
  "sport": {
    "name": "volleyball"
  },
  "dessert": "ice cream",
  "pet": "dog",
  "instrument": undefined,
  "fruits": [
    "apple",
    "banana",
    "cherry",
    "duku"
  ]
}
```

### Información de página

Utilice estos puntos de datos para capturar información de página para usarla en la lógica de regla o para enviar información a Analytics o a sistemas de seguimiento externos.

Puede seleccionar uno de los siguientes atributos de página para usarlos en el elemento de datos:

* URL
* Hostname
* Pathname
* Protocolo
* Referrer
* Title

### Query string Parameter

Especifique un único parámetro de URL en el campo URL Parameter.

Solo es necesaria la sección de nombres y cualquier indicador especial como “?” o &quot;=&quot; debe omitirse.

#### Ejemplo:

`contentType`

### Número aleatorio

Utilice este elemento de datos para generar un número aleatorio. A menudo se utiliza para datos de muestra o para crear ID, como un ID de visita individual. El número aleatorio puede utilizarse para proteger o desproteger datos confidenciales. Algunos ejemplos pueden incluir:

* Generar un ID de visita individual (Hit ID)
* Concatenar el número a un token de usuario o una marca de tiempo para garantizar su exclusividad
* Realizar un hash unidireccional en los datos PII
* Decidir al azar cuándo se muestra una solicitud de encuesta en el sitio

Especifique los valores mínimos y máximos del número aleatorio.

**Valores predeterminados:**

Mínimo: 0

Máximo: 1000000000

### Almacenamiento de sesión

Proporcione el nombre del elemento de almacenamiento de la sesión en el campo Session Storage Item Name.

El almacenamiento de sesión es similar al almacenamiento local, excepto que los datos se descartan después de que finalice la sesión, mientras que el almacenamiento local o una cookie pueden retener los datos.

### Comportamiento de los visitantes

De manera similar a Información de página, este elemento de datos utiliza tipos de comportamiento comunes para enriquecer la lógica dentro de las reglas y otras soluciones de Platform.

Seleccione uno de los siguientes atributos de comportamiento del visitante:

* Landing page
* Traffic source
* Minutes on site
* Session count
* Session page view count
* Lifetime page view count
* Is new visitor

Algunos casos de uso común son:

* Mostrar una encuesta después de que un visitante haya estado en el sitio durante cinco minutos
* Si esta es la página de aterrizaje para la visita, rellenar una métrica de Analytics
* Mostrar una oferta nueva al visitante después de un determinado número de sesiones
* Mostrar una sugerencia de suscripción al boletín en el caso de los visitantes nuevos

### Valor condicional

Un envoltorio para el [Value Comparison](#value-comparison-value-comparison) condición. En función del resultado de la comparación, devolverá uno de los dos valores disponibles en el formulario. De este modo, puede manejar &quot;If... Entonces... Si no...&quot; escenarios sin necesidad de reglas adicionales.

### Entorno de tiempo de ejecución

Permite seleccionar una de las siguientes variables:

* Entorno, etapa - Devuelve `_satellite.environment.stage` para diferenciar entre entornos de desarrollo/ensayo/producción.
* Fecha de compilación de la biblioteca: Devuelve `turbine.buildInfo.buildDate` que contiene el mismo valor que `_satellite.buildInfo.buildDate`.
* Nombre de propiedad - Devuelve `_satellite.property.name` para obtener el nombre de la propiedad de Launch.
* ID de propiedad - Devuelve `_satellite.property.id` para obtener el ID de la propiedad de Launch
* Nombre de regla - Devuelve `event.$rule.name` que contiene el nombre de la regla ejecutada.
* ID de regla - Devuelve `event.$rule.id` que contiene el ID de la regla ejecutada.
* Tipo de evento: Devuelve `event.$type` que contiene el tipo de evento que activó la regla.
* Carga útil de detalles de eventos - Devuelve `event.detail` que contiene la carga útil de un evento personalizado o una regla de llamada directa.
* Identificador de llamada directa: devuelve `event.identifier` que contiene el identificador de una regla de llamada directa.

### Atributos de dispositivo

Devuelve uno de los siguientes atributos de dispositivo de visitante:

* Tamaño de la ventana del explorador
* Tamaño de la pantalla

### Herramientas de JavaScript

Es un envoltorio para operaciones comunes de JavaScript. Recibe un elemento de datos como entrada. Devuelve el resultado de una de las siguientes transformaciones del valor del elemento de datos:

* Manipulación de cadenas básica (reemplazar, subcadena, coincidencia regex, primer y último índice, dividir, fracción)
* Operaciones básicas de matriz (fracción, unión, pop, desplazamiento)
* Operaciones universales básicas (fracción, longitud)