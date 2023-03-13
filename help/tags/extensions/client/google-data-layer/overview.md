---
title: Extensión de capa de datos de Google
description: Obtenga información acerca de la extensión de etiqueta de capa de datos del cliente de Google en Adobe Experience Platform.
exl-id: 7990351d-8669-432b-94a9-4f9db1c2b3fe
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '823'
ht-degree: 6%

---

# Extensión de la capa de datos de Google (Beta)

>[!IMPORTANT]
>
>Esta extensión se encuentra actualmente en fase beta y no se ha probado completamente en producción.

La extensión de capa de datos de Google le permite utilizar una capa de datos de Google en la implementación de etiquetas. La extensión se puede utilizar de forma independiente o simultánea con las soluciones de Google y con el código abierto de Google [Biblioteca auxiliar de capa de datos](https://github.com/google/data-layer-helper).

La biblioteca de ayuda proporciona una funcionalidad impulsada por eventos similar a la del Adobe de datos del cliente (ACDL). Los elementos de datos, las reglas y las acciones de la extensión de capa de datos de Google proporcionan una funcionalidad similar a las del [Extensión ACDL](../client-data-layer/overview.md).

## Vencimiento

La versión 1.0.x de la extensión es una versión beta. Esta extensión no se ha probado completamente en producción.

## Instalación

Para instalar la extensión, vaya al catálogo de extensiones en la interfaz de usuario de Experience Platform o en la interfaz de usuario de recopilación de datos y seleccione **Capa de datos de Google**.

Una vez instalada, la extensión crea o accede a una capa de datos cada vez que la biblioteca de etiquetas se carga en el sitio web.

## Vista de extensión

Al configurar la extensión de (durante la instalación de la extensión o al seleccionar **[!UICONTROL Configurar]** en el catálogo de extensiones) debe definir el nombre de la capa de datos que consume la extensión. Si no hay ninguna capa de datos con el nombre configurado cuando se carga la biblioteca, la extensión crea una en su lugar.

>[!NOTE]
>
>No importa si el código de Adobe o Google se carga primero y crea la capa de datos. Ambos sistemas crearán la capa de datos si no está presente, o utilizarán la capa de datos existente.

De forma predeterminada, la capa de datos utiliza el nombre predeterminado de Google `dataLayer`.

## Eventos

La extensión de permite escuchar cambios (eventos) dentro de la capa de datos. Un evento puede ser cualquiera de los siguientes:

* Etiquetar eventos (como una biblioteca que se está cargando)
* Eventos de JavaScript
* Datos insertados en la capa de datos con el `event` palabra clave.

Es importante comprender el uso del complemento [`event` palabra clave](https://developers.google.com/tag-platform/devguides/datalayer#use_a_data_layer_with_event_handlers) al insertar datos en una capa de datos de Google, de forma similar a la capa de datos del cliente de Adobe. El `event` La palabra clave cambia el comportamiento de la capa de datos de Google y, por lo tanto, el comportamiento de la extensión se actualiza en consecuencia.

Las secciones siguientes describen los diferentes tipos de eventos que la extensión puede detectar.

### Escuchar todas las inserciones en la capa de datos

Si selecciona esta opción, la extensión escucha cualquier cambio realizado en la capa de datos.

### Escuchar eventos push excluyendo eventos

Si selecciona esta opción, la extensión escucha todo lo que se inserte en la capa de datos, excepto los eventos.

El siguiente ejemplo de evento push lo rastrearía el oyente:

```js
dataLayer.push({"data":"something"})
```

El oyente no rastrearía los siguientes eventos push de ejemplo:

```js
dataLayer.push({"event":"myevent"})
dataLayer.push({"event":"myevent","data":"something"})
```

### Escuchar todos los eventos

Si selecciona esta opción, la extensión escucha cualquier evento insertado en la capa de datos.

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

Si desea detectar un evento específico, seleccione esta opción para que el detector de eventos rastree cualquier evento que coincida con una cadena específica.

Por ejemplo, si se establece `myEvent` al usar esta configuración, el oyente solo rastreará el siguiente evento push:

```js
dataLayer.push({"event":"myEvent"})
```

También puede utilizar una cadena regex para hacer coincidir los nombres de evento. Por ejemplo, configurar `myEvent\d` rastrearía eventos que comienzan por `myEvent` seguido de un dígito:

```js
dataLayer.push({"event":"myEvent1"})
dataLayer.push({"event":"myEvent2"})
```

## Acciones

Las secciones siguientes describen las diferentes acciones que la extensión puede realizar cuando se incluye en una [regla](../../../ui/managing-resources/rules.md).

### Insertar en la capa de datos {#push-to-data-layer}

Esta acción inserta contenido JSON en la propia capa de datos, lo que permite utilizar elementos de datos directamente en cargas JSON. En el editor JSON proporcionado, puede hacer referencia a elementos de datos usando notación de porcentaje (por ejemplo, `%dataElementName%`).

```json
{
    "page": {
        "url": "%url%",
        "previous_url": "%previous_url%",
        "concatenated_values": "static string %dataElement%"
    }
}
```

### Restablecimiento del estado calculado de Google DL

>[!NOTE]
>
>Esta acción está disponible a partir de la versión 1.0.5.

Esta acción restablece la capa de datos. Si se utiliza en una regla que procesa un cambio de capa de datos de Google, la capa de datos se restablece al estado calculado de la capa de datos en el momento en que se activó la regla. Si la acción se utiliza en una regla que no procesa un cambio en la capa de datos de Google, la acción vacía la capa de datos.

## Elementos de datos

La extensión proporciona un elemento de datos único que accede a la capa de datos mediante una clave (por ejemplo, `page.url` en el [fragmento superior](#push-to-data-layer)).

El elemento de datos puede proporcionar cualquiera de las siguientes opciones:

* Un valor específico de la capa de datos (por ejemplo, `page.url`)
* Toda la matriz de capas de datos (campo de clave vacío)
* Valores de un evento de capa de datos utilizando la clave (si la variable `event` palabra clave utilizada)
* Todo el objeto de evento (campo de clave vacío)

La extensión de siempre da prioridad a la información de evento. Si una capa de datos `event` se está procesando, los valores siempre se leen desde ese evento. Si un `event` no está presente, los valores se leen directamente desde la capa de datos.

## Información adicional

Encontrará más información en la [LÉAME del proyecto](https://github.com/adobe/reactor-extension-googledatalayer/blob/main/README.md) y en los cuadros de diálogo de elementos de datos y eventos de la extensión.
