---
title: Información general sobre la extensión del reenvío de eventos principal
description: Obtenga información acerca de la extensión de reenvío de eventos principal en Adobe Experience Platform.
feature: Event Forwarding
exl-id: b5ee4ccf-6fa5-4472-be04-782930f07e20
source-git-commit: c7344d0ac5b65c6abae6a040304f27dc7cd77cbb
workflow-type: tm+mt
source-wordcount: '1724'
ht-degree: 98%

---

# Información general sobre la extensión del reenvío de eventos principal

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

La extensión de reenvío de eventos principal proporciona los eventos, condiciones y tipos de datos predeterminados para el reenvío de eventos en Adobe Experience Platform.

Utilice esta referencia para obtener información sobre las opciones disponibles al utilizar esta extensión para generar una regla.

## Tipos de condición de la Extensión principal

Esta sección describe los tipos de condición disponibles en la Extensión principal. Estos tipos de condiciones se pueden usar con el tipo de lógica regular o de excepción.

### Código personalizado

Especifique cualquier Custom Code que deba darse como condición del evento. Utilice el editor de código integrado para introducir el código personalizado. El reenvío de eventos en Adobe Experience Platform es compatible con ES6.

1. Seleccione **[!UICONTROL Abrir editor]**.
1. Escriba el Custom Code.
1. Seleccione **[!UICONTROL Guardar]**.

Para acceder al valor de un elemento de datos en el código personalizado, utilice el método `getDataElementValue`. Por ejemplo, para recuperar el valor de un elemento de datos denominado `productName`, escriba lo siguiente: 

```javascript
getDataElementValue('productName') 
```

#### ruleStash, objeto

En el código personalizado, también puede utilizar el objeto `ruleStash`.

```javascript
utils.logger.log(context.arc.ruleStash);
```

`ruleStash` es un objeto que recopila todos los resultados de los módulos de acción.

Cada extensión tiene su propia área de nombres. Por ejemplo, si la extensión tiene el nombre `send-beacon`, todos los resultados de las acciones `send-beacon` se almacenan en el área de nombres `ruleStash['send-beacon']`.

```javascript
utils.logger.log(context.arc.ruleStash['adobe-cloud-connector']);
```

El área de nombres es única para cada extensión y tiene el valor `undefined` al principio.

El área de nombres se sobrescribirá con el resultado devuelto por cada acción. No hay área de nombres en que se produzca algo excepcional. Por ejemplo, si tiene una extensión `transform` que contiene dos acciones: `generate-fullname` y `generate-fulladdress`, añada las dos acciones a una regla.

Si el resultado de la acción `generate-fullname` es `Firstname Lastname`, la cadena de reglas aparece de la siguiente manera una vez completada la acción:

```js
{
  transform: 'Firstname Lastname`
}
```

Si el resultado de la acción `generate-address` es `3900 Adobe Way`, la pila de reglas aparece de la siguiente manera una vez completada la acción:

```js
{
  transform: '3900 Adobe Way`
}
```

Observe que `Firstname Lastname` ya no existe dentro de la pila de reglas. Esto se debe a que la acción `generate-address` la sobrescribió con la dirección.

Si desea almacenar los resultados de ambas acciones dentro del área de nombres `transform` en `ruleStash`, puede escribir el módulo de acción de manera similar al siguiente ejemplo:

```javascript
module.exports = (context) => {
  let transformRuleStash = context.arc.ruleStash.transform;
  if (!transformRuleStash) {
    transformRuleStash = {};
  }
  transformRuleStash.fullName = 'Firstname Lastname';
  return transformRuleStash;
}
```

La primera vez que se ejecuta esta acción, `ruleStash` es `undefined` y se inicializa con un objeto vacío. La próxima vez que se ejecuta la acción, la acción arroja `ruleStash` cuando se invocó anteriormente. El uso de un objeto como `ruleStash` le permite añadir nuevos datos sin perder datos previamente establecidos por otras acciones de la extensión.

En este caso, debe tener cuidado de devolver siempre la pila de reglas de extensión completa. Si solo devolviera un valor (por ejemplo, 5), la pila de reglas tendría el siguiente aspecto:

```js
{
  transform: 5
}
```

### Comparación de valor {#value-comparison}

Compara dos valores para determinar si esta condición devuelve el valor “True”.

Si tiene una regla con varias condiciones, es posible que esta condición devuelva el valor “True”, pero la regla no se activará porque las demás condiciones se evalúan como “False” o una de las excepciones como “True”.

1. Proporcione un valor.
1. Seleccione el operador. Consulte la lista de operadores de comparación de valores para obtener más información.
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

**Is Truthy:** La condición devuelve el valor “True” si el valor es “True” después de convertirse en un valor booleano. Consulte la [documentación sobre Truthy de MDN](https://developer.mozilla.org/es-ES/docs/Glossary/Truthy) para ver ejemplos de valores “Truthy”.

**Is False:** La condición devuelve el valor “True” si se trata de una condición booleana con el valor “False”. El valor que proporcione no se convierte en booleano si es de cualquier otro tipo. Cualquier valor que no sea booleano con el valor “False” provoca que se devuelva el valor “False”.

**Is Falsy:** La condición devuelve el valor “True” si el valor es “False” después de convertirse en un valor booleano. Consulte la [documentación sobre Falsy de MDN](https://developer.mozilla.org/es-ES/docs/Glossary/Falsy) para ver ejemplos de valores “falsy”.



## Tipos de acción de Extensión principal

En esta sección se describen los tipos de acción disponibles en la Extensión principal.

### Código personalizado

Proporcione el código que se ejecuta después de activar el evento y de evaluar las condiciones. El reenvío de eventos en Adobe Experience Platform es compatible con ES6.

1. Asigne un nombre al código de acción.
1. Seleccione **[!UICONTROL Abrir editor]**.
1. Edite el código y, a continuación, haga clic en **[!UICONTROL Guardar]**.

Para acceder al valor de un elemento de datos en el código personalizado, utilice el método `getDataElementValue`. Por ejemplo, para recuperar el valor de un elemento de datos denominado `productName`, escriba lo siguiente: 

```javascript
getDataElementValue('productName') 
```

Las acciones de reenvío de eventos se ejecutan secuencialmente. También es posible que el código personalizado de una acción arroje un valor que se pueda utilizar en una acción posterior. El valor devuelto puede provenir del código dentro de esa acción o del cuerpo de respuesta de una llamada realizada a un origen externo. Para hacer referencia a datos de una acción ejecutada anteriormente en una sola regla en la que se utiliza la extensión Core, cree un elemento de datos de tipo `Path` y utilice la siguiente ruta para hacer referencia al valor de una variable denominada `productCategory` definida en el código personalizado dentro de la extensión Core:

```javascript
arc.ruleStash.[Extension-Name].[key-as-defined-by-action] 

arc.ruleStash.core.productCategory  
```

## Tipos de Data Elements de Extensión principal

Los tipos de Data Elements están determinados por la extensión. No hay límite para los tipos que se pueden crear.

Las secciones siguientes describen los tipos de Data Elements disponibles en la Extensión principal. Otras extensiones utilizan tipos de Data Elements diferentes.

### Código personalizado

Puede introducir código JavaScript personalizado en la IU si selecciona la opción **[!UICONTROL Abrir editor]** e inserta código en la ventana del editor.

Se debe incluir una sentencia de retorno en la ventana del editor para indicar qué valor se tiene que usar como valor del elemento de datos. Si no se incluye una sentencia de retorno o se devuelve el valor `null` o `undefined`, el valor predeterminado del elemento de datos refleja `null` o `undefined`.

Para acceder al valor de un elemento de datos en código personalizado, utilice el método `getDataElementValue`. Por ejemplo, para recuperar el valor de un elemento de datos denominado `productName`, escriba lo siguiente: 

```javascript
getDataElementValue('productName') 
```

**Ejemplo:**

```javascript
return getDataElementValue('section').concat(getDataElementValue('pName')); 
```

#### Ruta

Se puede hacer referencia a una ruta a un par clave-valor en un evento enviado a Adobe Experience Platform Edge Network mediante el tipo de elemento de datos Ruta.

Para hacer referencia al objeto completo de un evento, escriba `arc` como ruta. La sigla `arc` significa Contexto de recursos de Adobe y es la ruta de nivel superior para un evento enviado a Adobe Experience Platform Edge Network.

Por ejemplo, dado que la llamada `interact` del cliente a Edge Network tiene la siguiente solicitud, como se ve desde la consola del explorador:

```javascript
"events": [ 
        { 
             "xdm": { 
                    "page": { 
                            "btnHover": false, 
                            "pageName": "We Travel Home Page", 
                            "siteSection": "Landing Page" 
                     }] 
```

Para introducir una ruta que haga referencia a `pageName`, introduzca lo siguiente en el campo de ruta:

```javascript
arc.event.xdm.page.pageName 
```

>[!NOTE]
>
>La llamada `interact` del cliente tiene `events`, pero para el reenvío de eventos necesita `event`. Esto se debe a que el reenvío de eventos inspecciona cada evento individualmente y no como un lote de varios eventos, como se muestra en el cliente.
