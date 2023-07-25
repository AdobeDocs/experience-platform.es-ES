---
title: Vista del editor de validación
description: Esta guía detalla información acerca de la vista Editor de validación en Adobe Experience Platform Assurance.
exl-id: 09be531c-8dc3-48b8-814f-b7a06adf1da3
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: ht
source-wordcount: '527'
ht-degree: 100%

---

# Vista del Editor de validación

El Editor de validación permite administrar rápida y fácilmente las funciones JavaScript para validar eventos en una sesión de Adobe Experience Platform Assurance. Cada función recibe los eventos en una sesión de Assurance. Puede escribir funciones para validar la configuración del cliente, las condiciones de evento, las pruebas y los casos de uso.

## Introducción al Editor de validación

Después de [configurar Assurance](../tutorials/implement-assurance.md), en la vista **[!UICONTROL Inicio]**, seleccione **[!UICONTROL Editor de validación]**.

![Validation-Editor-Screen-Shot](https://user-images.githubusercontent.com/6597105/198680074-f548a646-6f2f-4a65-82fd-0f1687d869bf.png)

## Escritura de una función de validación

Esta función le permite crear, editar o eliminar funciones de validación para sus sesiones de Adobe Experience Platform Assurance.

1. Seleccione **[!UICONTROL Crear una nueva validación]**.
2. Introduzca un **nombre** para identificar la validación, proporcione una **categoría** y una **descripción**.
3. Edite el código en el editor para validar los eventos de la sesión de Assurance.

Una vez completadas las pruebas de función, seleccione **[!UICONTROL Publish]** para guardar la validación.

### Definición del evento

| Clave | Tipo | Descripción |
| :--- | :--- | :--- |
| `uuid` | Cadena | Identificador único universal del evento. |
| `timestamp` | Número | Marca de tiempo del cliente cuando el evento se envió a Assurance. |
| `eventNumber` | Número | Se utiliza para ordenar cuando se envió el evento. Esta clave es útil cuando los eventos tienen la misma marca de tiempo. |
| `vendor` | Cadena | Cadena de identificación del proveedor en el formato de nombre de dominio inverso (por ejemplo, com.adobe.assurance). |
| `type` | Cadena | Se utiliza para indicar el tipo de evento. |
| `payload` | Objeto | Define los datos del evento y contiene propiedades únicas y comunes. Algunas propiedades comunes incluyen `ACPExtensionEventSource` y `ACPExtensionEventType`. |
| `annotations` | Matriz | Una matriz de objetos de anotación. |

### Definición de anotación

| Clave | Tipo | Descripción |
| :--- | :--- | :--- |
| `uuid` | Cadena | Identificador único universal de la anotación. |
| `type` | Cadena | Se utiliza para denotar el tipo de anotación y suele ser el nombre del complemento (por ejemplo, análisis). |
| `payload` | Objeto | Define los datos que deben complementar el evento. En Adobe Analytics, aquí es donde se incluyen los datos de visitas posprocesados. |

### Resultados de validación

Se espera que la función de validación devuelva un objeto que contenga lo siguiente:

| Clave | Tipo | Descripción |
| :--- | :--- | :--- |
| `message` | Cadena | El mensaje de validación que se mostrará en los resultados del resumen. |
| `events` | Matriz | Una matriz de uuid de evento para registrar como coincidentes o no coincidentes. |
| `links` | Matriz | Una matriz de objetos de `ValidationResultLink` para hacer referencia a documentación y otros recursos `{( type: 'doc'|'product', url: String )}` |
| `result` | Cadena | Este es el resultado de validación y se espera que sea una de las cadenas enumeradas: “coincidente”, “no coincidente”, “desconocido” |

## Vista de los resultados de validación

Los resultados de la función se muestran en la sección de resultados, debajo del editor de código. Si el resultado de la validación es `unknown` o `not matched` y la matriz `events` tiene uno o más `uuids`, los eventos se resaltarán en la cronología con los colores siguientes:

* Verde: coincidente
* Naranja: desconocido
* Rojo: no coincidente

![Timeling-Validation-Highlights-Screen-Shot](https://user-images.githubusercontent.com/6597105/198681412-93d10a5a-3212-4e85-850a-aeaf5caf0521.png)

## Resolución de problemas

Puede añadir `console.log()` en la función para imprimir elementos en Developer Console. Como alternativa, puede utilizar la propiedad mensaje del objeto resultado para depurar los mensajes en el panel de resultados.

Si se produce un error en el editor de código JavaScript, se muestra un estado de error junto con el motivo.

Para obtener más información sobre las validaciones, visite el GitHub de [Validaciones de Adobe Experience Platform Assurance](https://github.com/adobe/griffon-validation-plugins). Aquí encontrará ejemplos de validaciones propiedad de Adobe. Consulte la [wiki](https://github.com/adobe/griffon-validation-plugins/wiki) para obtener descripciones más detalladas de las validaciones.
