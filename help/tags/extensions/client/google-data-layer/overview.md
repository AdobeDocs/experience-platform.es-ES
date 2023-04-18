---
title: Extensión de la capa de datos de Google
description: Obtenga información sobre la extensión de la etiqueta de capa de datos del cliente de Google en Adobe Experience Platform.
exl-id: 7990351d-8669-432b-94a9-4f9db1c2b3fe
source-git-commit: 9c608f69f6ba219f9cb4e938a77bd4838158d42c
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 13%

---

# Extensión de la capa de datos de Google

La extensión de capa de datos de Google le permite utilizar una capa de datos de Google en la implementación de etiquetas. La extensión se puede utilizar de forma independiente o simultánea con las soluciones de Google y con el código abierto de Google [Biblioteca de ayuda de capa de datos](https://github.com/google/data-layer-helper).

La biblioteca Helper proporciona una funcionalidad similar impulsada por eventos al Adobe Client Data Dayer (ACDL). Los elementos de datos, las reglas y las acciones de la extensión de capa de datos de Google proporcionan una funcionalidad similar a la de la [Extensión ACDL](../client-data-layer/overview.md).

## Vencimiento

La versión 1.2.x es una versión beta tardía que se está utilizando en la producción.

## Instalación

Para instalar la extensión, vaya al catálogo de extensiones en la interfaz de usuario de la recopilación de datos y seleccione **[!UICONTROL Capa de datos de Google]**.

Una vez instalada, la extensión crea o accede a una capa de datos en cada carga de la biblioteca de etiquetas de Adobe Experience Platform.

## Vista de extensión

La configuración de la extensión se puede utilizar para definir el nombre de la capa de datos que consume la extensión. Si no hay ninguna capa de datos con el nombre configurado cuando se cargan las etiquetas de Adobe Experience Platform, la extensión crea una.

El nombre predeterminado de la capa de datos es el nombre predeterminado de Google `dataLayer`.

>[!NOTE]
>
>No importa si Google o el código de Adobe se cargan primero y crean la capa de datos. Ambos sistemas se comportan del mismo modo: cree la capa de datos si no está presente o utilice la capa de datos existente.

## Eventos

>[!NOTE]
>
>La palabra _evento_ se sobrecarga cuando se utiliza una capa de datos basada en eventos en Adobe Experience Platform Tags. _Eventos_ puede ser:
> - Eventos de Adobe Experience Platform Tags (biblioteca cargada, etc.).
> - Eventos de JavaScript.
> - Datos insertados en la capa de datos con la variable _evento_ palabra clave.


La extensión le ofrece la posibilidad de detectar cambios en la capa de datos.

>[!NOTE]
>
>Es importante comprender el uso de la variable _evento_ palabra clave cuando se insertan datos en una capa de datos de Google, de forma similar a la capa de datos del cliente de Adobe. La variable _evento_ palabra clave cambia el comportamiento de la capa de datos de Google y, por lo tanto, esta extensión.\
> Lea la documentación de Google o realice una investigación si no está seguro sobre este punto.

### Escuche todos los empujones a la capa de datos

Si selecciona esta opción, el oyente de eventos escucha cualquier cambio realizado en la capa de datos.

### Escuchar pulsaciones excluyendo eventos

Si selecciona esta opción, el detector de eventos escucha cualquier inserción de datos en la capa de datos, excluyendo eventos.

El oyente rastrearía los siguientes eventos push de ejemplo:

```js
dataLayer.push({"data":"something"})
```

El oyente no rastrearía los siguientes eventos push de ejemplo:

```js
dataLayer.push({"event":"myevent"})
dataLayer.push({"event":"myevent","data":"something"})
```

### Escuchar todos los eventos

Si selecciona esta opción, el oyente de eventos escucha cualquier evento insertado en la capa de datos.

El oyente rastrearía los siguientes eventos push de ejemplo:

```js
dataLayer.push({"event":"myevent"})
dataLayer.push({"event":"myevent","data":"something"})
```

El siguiente ejemplo de evento push no sería rastreado por el oyente:

```js
dataLayer.push({"data":"something"})
```

### Escuchar un evento específico

En el caso de que especifique un evento, el oyente de eventos rastrea cualquier evento que coincida con una cadena específica.

Por ejemplo, si se establece `myEvent` al usar esta configuración, el oyente solo rastreará el siguiente evento push:

```js
dataLayer.push({"event":"myEvent"})
```

Se puede utilizar una regex (ECMAScript / JavaScript) para hacer coincidir los nombres de evento.

Por ejemplo, configurar &#39;myEvent\d&#39; rastrearía `myEvent` con un dígito (\d):

```js
dataLayer.push({"event":"myEvent1"})
dataLayer.push({"event":"myEvent2"})
```

## Acciones

### Insertar en la capa de datos {#push-to-data-layer}

La extensión de le proporciona dos acciones para insertar JSON en la capa de datos. un campo de texto libre para crear manualmente el JSON que se va a insertar y, a partir de la versión 1.2.0, un cuadro de diálogo multicampo de valor clave.

#### Texto libre JSON

La acción de texto libre permite utilizar elementos de datos directamente en el JSON. Dentro del editor JSON, se debe hacer referencia a los elementos de datos mediante la notación de porcentaje. Por ejemplo, `%dataElementName%`.

```json
{
    "page": {
        "url": "%url%",
        "previous_url": "%previous_url%",
        "concatenated_values": "static string %dataElement%"
    }
}
```

#### Campo múltiple Clave-Valor

El nuevo cuadro de diálogo multicampo clave-valor es una interfaz más fácil de usar que permite configurar una notificación push sin escribir JSON manualmente.

### Restablecimiento de Google DL a estado calculado

La extensión proporciona una acción para restablecer la capa de datos. Si se utiliza en una regla que procesa un cambio en la capa de datos de Google, la capa de datos se restablece al estado calculado de la capa de datos en el momento en que se activó la regla. Si la acción se utiliza en una regla que no procesa un cambio en la capa de datos de Google, la acción vacía la capa de datos.

## Elementos de datos

El elemento de datos proporcionado se puede utilizar durante la ejecución de una regla activada por un cambio en la capa de datos de Google (evento push) o en una regla no relacionada como Library Loaded. En el primer caso, el elemento de datos devuelve un valor tomado del estado calculado en el momento del cambio de la capa de datos. En este último caso, se utiliza el estado calculado en el momento de la ejecución de la regla.

Un conmutador le permite seleccionar si el elemento de datos debe devolver valores del estado calculado completo o solo a partir de la información de evento (si se utiliza en una regla activada por un cambio en la capa de datos).

Por lo tanto, el elemento de datos puede devolver:

- Campo vacío: estado calculado de la capa de datos.
- Campo con clave (como page.previous_url en el ejemplo anterior): valor de la clave en el objeto de evento o en el estado calculado.

## Información adicional

Los cuadros de diálogo de evento y elemento de datos de la extensión contienen información de uso detallada y ejemplos.

La información general adicional se encuentra en la sección [README DEL PROYECTO](https://github.com/adobe/reactor-extension-googledatalayer/blob/main/README.md)
