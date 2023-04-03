---
title: Vista Editor de validación
description: Esta guía detalla información sobre la vista del Editor de validación en Adobe Experience Platform Assurance.
source-git-commit: 5778d4db27d0f57281821dc8e042a31b69745514
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 3%

---


# Vista Editor de validación

El Editor de validación permite administrar rápida y fácilmente las funciones de JavaScript para validar eventos en una sesión de Adobe Experience Platform Assurance. Cada función recibe los eventos en una sesión de Assurance. Puede escribir funciones para validar la configuración del cliente, las condiciones de evento, las pruebas y los casos de uso.

## Introducción al Editor de validación

Después [configuración de Assurance](../tutorials/implement-assurance.md), en el **[!UICONTROL Página principal]** ver, seleccionar **[!UICONTROL Editor de validación]**.

![Validation-Editor-Screen-Shot](https://user-images.githubusercontent.com/6597105/198680074-f548a646-6f2f-4a65-82fd-0f1687d869bf.png)

## Escribir una función de validación

Esta función le permite crear, editar o eliminar funciones de validación para sus sesiones de Adobe Experience Platform Assurance.

1. Select **[!UICONTROL Crear una nueva validación]**.
2. Escriba un **name** para identificar la validación, proporcione una **categoría** y **descripción**.
3. Edite el código en el editor para validar los eventos para la sesión de seguridad.

Una vez completadas las pruebas de función, seleccione **[!UICONTROL Publicación]** para guardar la validación.

### Definición del evento

| Clave | Tipo | Descripción |
| :--- | :--- | :--- |
| `uuid` | Cadena | Identificador único universal para el evento. |
| `timestamp` | Número | Marca de tiempo del cliente cuando el evento se envió a Assurance. |
| `eventNumber` | Número | Se utiliza para solicitar cuándo se envió el evento. Esta clave es útil cuando los eventos tienen la misma marca de tiempo. |
| `vendor` | Cadena | Cadena de identificación del proveedor con el formato de nombre de dominio inverso (por ejemplo, com.adobe.surance). |
| `type` | Cadena | Se utiliza para denotar el tipo de evento. |
| `payload` | Objeto | Define los datos del evento y contiene propiedades únicas y comunes. Algunas propiedades comunes incluyen `ACPExtensionEventSource` y `ACPExtensionEventType`. |
| `annotations` | Matriz | Matriz de objetos de anotación. |

### Definición de anotación

| Clave | Tipo | Descripción |
| :--- | :--- | :--- |
| `uuid` | Cadena | Identificador único universal para la anotación. |
| `type` | Cadena | Se utiliza para denotar el tipo de anotación y suele ser el nombre del complemento (por ejemplo, analytics). |
| `payload` | Objeto | Define los datos que deben complementar el evento. En Adobe Analytics, aquí es donde se incluyen los datos de visitas posprocesados. |

### Resultados de validación

Se espera que la función de validación devuelva un objeto que contenga lo siguiente:

| Clave | Tipo | Descripción |
| :--- | :--- | :--- |
| `message` | Cadena | Mensaje de validación que se mostrará en los resultados del resumen. |
| `events` | Matriz | Matriz de uuids de evento que se notificarán como coincidentes o no coincidentes. |
| `links` | Matriz | Una matriz de `ValidationResultLink` objetos para hacer referencia a documentación y otros recursos `{( type: 'doc'|'product', url: String )}` |
| `result` | Cadena | Este es el resultado de la validación y se espera que sea una de las cadenas enumeradas: &quot;coincidente&quot;, &quot;no coincidente&quot;, &quot;desconocido&quot; |

## Ver los resultados de validación

Los resultados de la función se muestran en la sección de resultados debajo del editor de código. Si el resultado de validación es `unknown` o `not matched` y `events` matriz tiene una o más `uuids`, los eventos se resaltarán en la cronología con los colores siguientes:

* Verde: coincidente
* Naranja - desconocido
* Rojo: no coincide

![Timeling-Validation-Resaltados-Screen-Shot](https://user-images.githubusercontent.com/6597105/198681412-93d10a5a-3212-4e85-850a-aeaf5caf0521.png)

## Resolución de problemas

Puede añadir `console.log()` en la función para imprimir elementos en la consola del desarrollador. Como alternativa, puede utilizar la propiedad message del objeto result para depurar mensajes en el panel de resultados.

Si se produce un error en el editor de código JavaScript, se muestra un estado de error junto con el motivo.

Para obtener más información sobre las validaciones, visite la [Validaciones de Adobe Experience Platform Assurance](https://github.com/adobe/griffon-validation-plugins) GitHub Aquí encontrará ejemplos de validaciones propiedad de Adobe. Consulte la [wiki](https://github.com/adobe/griffon-validation-plugins/wiki) para obtener descripciones más detalladas de las validaciones.
