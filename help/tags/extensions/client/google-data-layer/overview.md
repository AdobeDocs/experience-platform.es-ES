---
title: Extensión de capa de datos de Google
description: Obtenga información acerca de la extensión de etiqueta de capa de datos del cliente de Google en Adobe Experience Platform.
exl-id: 7990351d-8669-432b-94a9-4f9db1c2b3fe
source-git-commit: c61afdc2c3df98a0ef815d7cb034ba2907c52908
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 12%

---

# Extensión de capa de datos Google

La extensión de capa de datos de Google le permite utilizar una capa de datos de Google en la implementación de etiquetas. La extensión se puede usar de forma independiente o simultánea con las soluciones de Google y con la biblioteca de código abierto [Data Layer Helper Library](https://github.com/google/data-layer-helper) de Google.

La biblioteca de ayuda proporciona una funcionalidad impulsada por eventos similar a la capa de datos del cliente de Adobe (ACDL). Los elementos de datos, las reglas y las acciones de la extensión de capa de datos de Google proporcionan una funcionalidad similar a las de la [extensión ACDL](../client-data-layer/overview.md).

## Instalación

Para instalar la extensión, vaya al catálogo de extensiones en la interfaz de usuario de recopilación de datos y seleccione **[!UICONTROL Capa de datos de Google]**.

Una vez instalada, la extensión crea o accede a una capa de datos en cada carga de la biblioteca de etiquetas de Adobe Experience Platform.

## Vista de extensión

La configuración de la extensión se puede utilizar para definir el nombre de la capa de datos que consume la extensión. Si no hay ninguna capa de datos con el nombre configurado cuando se carga Adobe Experience Platform Tags, la extensión crea una.

El nombre predeterminado de la capa de datos es el nombre predeterminado de Google `dataLayer`.

>[!NOTE]
>
>No importa si el código de Adobe o Google se carga primero y crea la capa de datos. Ambos sistemas se comportan del mismo modo: cree la capa de datos si no está presente o utilice la capa de datos existente.

## Eventos

>[!NOTE]
>
>La palabra _event_ se sobrecarga cuando se utiliza una capa de datos controlada por evento en las etiquetas de Adobe Experience Platform. _Los eventos_ pueden ser:
> - Eventos de etiquetas de Adobe Experience Platform (biblioteca cargada, etc.).
> - Eventos de JavaScript.
> - Datos insertados en la capa de datos con la palabra clave _event_.

La extensión le ofrece la posibilidad de escuchar cambios en la capa de datos.

>[!NOTE]
>
>Es importante comprender el uso de la palabra clave _event_ cuando los datos se insertan en una capa de datos de Google, de manera similar a la capa de datos del cliente de Adobe. La palabra clave _event_ cambia el comportamiento de la capa de datos de Google y, por lo tanto, de esta extensión.\
> Lea la documentación de Google o investigue si no está seguro sobre este punto.

### Tipos de eventos de Google

Google admite dos métodos para insertar eventos: Google Tag Manager, con el método `push()`, y Google Analytics 4, con el método `gtag()`.

Las versiones de la extensión de capa de datos de Google anteriores a 1.2.1 solo admitían eventos creados por `push()`, como se muestra en los ejemplos de código de esta página.

Las versiones 1.2.1 y superiores admiten eventos creados con `gtag()`.  Esto es opcional y se puede habilitar en el cuadro de diálogo Configuración de la extensión.

Para obtener más información acerca de `push()` y `gtag()` eventos, consulte la [documentación de Google](https://developers.google.com/analytics/devguides/collection/ga4/reference/events?client_type=gtag).  También se proporciona información en los cuadros de diálogo de configuración y reglas de la extensión.

### Escuchar todas las inserciones en la capa de datos

Si selecciona esta opción, el oyente de eventos escucha cualquier cambio realizado en la capa de datos.

### Escuchar eventos push excluyendo eventos

Si selecciona esta opción, el oyente de eventos escucha cualquier inserción de datos en la capa de datos, excluyendo los eventos.

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

Por ejemplo, si se configura &#39;myEvent\d&#39;, se rastreará `myEvent` con un dígito (\d):

```js
dataLayer.push({"event":"myEvent1"})
dataLayer.push({"event":"myEvent2"})
```

## Acciones

### Insertar en la capa de datos {#push-to-data-layer}

La extensión le proporciona dos acciones para insertar el JSON en la capa de datos; un campo de texto libre para crear manualmente el JSON que se va a insertar y, a partir de la versión 1.2.0, un cuadro de diálogo de varios campos con valor clave.

#### Texto libre JSON

La acción de texto libre permite utilizar elementos de datos directamente en el JSON. En el editor JSON, se debe hacer referencia a los elementos de datos mediante notación de porcentaje. Por ejemplo, `%dataElementName%`.

```json
{
  "page": {
    "url": "%url%",
    "previous_url": "%previous_url%",
    "concatenated_values": "static string %dataElement%"
  }
}
```

#### Multicampo clave-valor

El nuevo cuadro de diálogo multicampo clave-valor es una interfaz más fácil de usar que permite configurar una notificación push sin escribir manualmente JSON.

### Restablecimiento del estado calculado de Google DL

La extensión le proporciona una acción para restablecer la capa de datos. Si se utiliza en una regla que procesa un cambio de capa de datos de Google, la capa de datos se restablece al estado calculado de la capa de datos en el momento en que se activó la regla. Si la acción se utiliza en una regla que no procesa un cambio en la capa de datos de Google, la acción vacía la capa de datos.

## Elementos de datos

El elemento de datos proporcionado se puede utilizar durante la ejecución de una regla activada por un cambio de capa de datos de Google (evento push) o en una regla no relacionada como Library Loaded. En el primer caso, el elemento de datos devuelve un valor tomado del estado calculado en el momento del cambio de la capa de datos. En este último caso, se utiliza el estado calculado en el momento de la ejecución de la regla.

Un conmutador le permite seleccionar si el elemento de datos debe devolver valores de todo el estado calculado o solo de la información de evento (si se utiliza en una regla activada por un cambio de capa de datos).

Por lo tanto, el elemento de datos puede devolver:

- Empty field: estado calculado de la capa de datos.
- Campo con clave (como page.previous_url en el ejemplo anterior): valor de la clave en el objeto de evento o estado calculado.

## Información adicional

Los cuadros de diálogo de elementos de datos y eventos de la extensión contienen información de uso detallada y ejemplos.

Encontrará información general adicional en el [archivo LÉAME del proyecto](https://github.com/adobe/reactor-extension-googledatalayer/blob/main/README.md)
