---
title: Extensión de la capa de datos del cliente de Adobe
description: Obtenga información acerca de la extensión de la etiqueta de capa de datos del cliente de Adobe en Adobe Experience Platform.
exl-id: c4d1b4d3-4b51-4701-be2e-31b08e109bf6
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 95%

---

# Extensión de la capa de datos del cliente de Adobe

Esta documentación proporciona ejemplos y prácticas recomendadas sobre cómo utilizar la extensión de capa de datos del cliente de Adobe.

<!-- (Missing document?)
If you would like to have more details on development consideration, [please reach this page](./dev.md). -->

## Instalación

Para instalar la extensión, vaya al catálogo de extensiones en la interfaz de usuario del Experience Platform o la interfaz de usuario de recopilación de datos y seleccione Capa de datos del cliente de Adobe.

![Vista de extensión ACDL en el catálogo](./images/catalog.png)

<!-- (GitHub link?)
There is also the possibility to fork this project. You can download this github project, realize the change that you deem required for your specific use-case and re-upload it on your Organization as a private extension.
This installation will not be supported on our end.<br>
>[!NOTE]
>
> _Consider renaming the extension name in the extension.json file_ -->

## Vista de extensión

De forma predeterminada, la secuencia de comandos ACDL crea una nueva capa de datos con el nombre de variable `adobeDataLayer`. La vista de extensión le ofrece la posibilidad de cambiar este nombre si lo desea. Se creará una instancia del nombre que haya definido cuando se carguen las etiquetas.

>[!NOTE]
>
>Al cambiar el nombre del objeto, se sigue creando una instancia del objeto `adobeDataLayer` original, que luego se duplica con el nuevo nombre de variable seleccionado.

## Eventos

La extensión permite escuchar eventos en la capa de datos. Los eventos disponibles son los siguientes:

### Escuchar todos los cambios de datos

Si selecciona esta opción, el oyente de eventos escucha cualquier cambio realizado en la capa de datos.

>[!IMPORTANT]
>
>La inserción de eventos no cambia la propia capa de datos.

El oyente rastrearía los siguientes eventos push de ejemplo:

* ` adobeDataLayer.push({"data":"something"})`
* ` adobeDataLayer.push({"event":"myevent","data":"something"})`

El siguiente ejemplo de evento push no sería rastreado por el oyente:

* ` adobeDataLayer.push({"event":"myevent"})`

### Escuchar todos los eventos

Si selecciona esta opción, el oyente de eventos escucha cualquier evento insertado en la capa de datos.

El oyente rastrearía los siguientes eventos push de ejemplo:

* ` adobeDataLayer.push({"event":"myevent"})`
* ` adobeDataLayer.push({"event":"myevent","data":"something"})`

El siguiente ejemplo de evento push no sería rastreado por el oyente:

* ` adobeDataLayer.push({"data":"something"}) `

### Escuchar un evento específico

En el caso de que especifique un evento, el oyente de eventos rastrea cualquier evento que coincida con una cadena específica.

Por ejemplo, si se establece `myEvent` al usar esta configuración, el oyente solo rastreará el siguiente evento push:

* `adobeDataLayer.push({"event":"myEvent"})`

También puede cambiar el ámbito del oyente de eventos. Las diferentes opciones se resumen a continuación:

* `all`: Esta es la opción predeterminada y activa la regla cada vez que la condición seleccionada arriba se ha cumplido en el pasado o se insertará en el futuro. Esta es la opción más segura si utiliza una implementación asincrónica.
* `future`: Esta opción activa la regla solo cuando se envían a la capa de datos nuevos eventos push que coinciden con la condición.
* `past`: Esta opción activa la regla solo para los eventos push antiguos que coinciden con la condición. Los nuevos eventos push que coincidan con la condición se ignorarán y ya no volverán a activar la regla.

## Acciones

Las siguientes secciones describen las acciones que pueden realizarse con la extensión.

### Restablecer capa de datos

La extensión le ofrece una forma de restablecer la longitud de la capa de datos, lo que puede ayudarle a mantener un tamaño limitado para una aplicación de una sola página (SPA).

Sin embargo, actualmente no hay posibilidad de quitar completamente la información establecida con anterioridad durante los métodos push.

La acción **Restablecer y establecer estado calculado** copia el último estado calculado, vacía el objeto de capa de datos y vuelve a insertar el último estado.

### Insertar en la capa de datos

La extensión le proporciona una acción para insertar contenido JSON en la propia capa de datos. Esta acción permite utilizar elementos de datos directamente en el JSON. En el editor JSON, se debe hacer referencia a los elementos de datos mediante notación de porcentaje (por ejemplo, `%dataElementName%`).

```json
{
    "page": {
        "url": "%url%",
        "previous_url": "%previous_url%",
        "concatenated_values": "static string %dataElement%"
    }
}
```

## Elementos de datos

Las secciones siguientes abarcan los tipos de elementos de datos únicos proporcionados por la extensión.

### Estado calculado

El elemento de datos Estado calculado de la capa de datos puede devolver una de estas dos cosas, en función de cómo lo configure:

* Estado completo de la capa de datos: De forma predeterminada, se devuelve el estado calculado de la capa de datos completo.
* Una ruta específica: Puede especificar la ruta que desee devolver en la capa de datos. Las rutas se especifican usando notación de puntos (por ejemplo, `data.foo`).

### Tamaño de la capa de datos

Este elemento de datos devuelve el tamaño de la capa de datos. El tamaño de la capa de datos se representa mediante el número de elementos que se han insertado en este objeto.

Dada la siguiente lista de eventos push, este elemento de datos devolverá el entero `2`:

```js
adobeDataLayer.push({"event":"myEvent"})
adobeDataLayer.push({"data":{"foo":"bar"}})
```
