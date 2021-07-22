---
title: Información general sobre el desarrollo de extensiones
description: Obtenga información sobre los componentes principales de diferentes tipos de extensión de etiquetas y el proceso de desarrollo de extensiones en Adobe Experience Platform.
source-git-commit: 421d1d0660c4c9c7280974f8a812a8f0e4f7cbea
workflow-type: tm+mt
source-wordcount: '1888'
ht-degree: 68%

---

# Información general sobre el desarrollo de extensiones

>[!NOTE]
>
>Adobe Experience Platform Launch se está convirtiendo en un conjunto de tecnologías de recopilación de datos en Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

Uno de los objetivos principales de Adobe Experience Platform es crear un ecosistema abierto en el que los ingenieros fuera del equipo de ingeniería principal puedan exponer funcionalidades adicionales mediante etiquetas. Esto se realiza mediante extensiones de etiqueta. Una vez que un usuario ha instalado una extensión en una propiedad de etiqueta, la funcionalidad de esa extensión está disponible para su uso por todos los usuarios de la propiedad.

Este documento describe los componentes principales de diferentes tipos de extensiones y proporciona vínculos para obtener más documentación que le guíe en el proceso de desarrollo de extensiones.

## Módulos de biblioteca

Los módulos de biblioteca son fragmentos de código reutilizable proporcionados por una extensión que se emiten dentro de la biblioteca de tiempo de ejecución de etiquetas. Dependiendo de si está desarrollando una extensión web o una extensión Edge, los tipos de módulos disponibles y sus casos de uso variarán. Consulte las siguientes subsecciones para obtener una descripción general acerca de los módulos de cada tipo de extensión:

* [Módulos para extensiones web](#web-modules)
* [Módulos para extensiones de Edge](#edge-modules)

### Módulos para extensiones web {#web-modules}

En las extensiones web, las reglas se activan mediante eventos que pueden ejecutar acciones específicas si se cumple un conjunto determinado de condiciones. Consulte la descripción general del [flujo de módulos en extensiones web](./web/flow.md) para obtener más información.

Además de los [módulos principales](./web/core.md) que proporciona Adobe, puede definir sus propios módulos de biblioteca en sus extensiones web:

* [Tipos de eventos](#web-event)
* [Tipos de condición](#web-condition)
* [Tipos de acción](#web-action)
* [Tipos de elementos de datos](#web-data-element)
* [Módulos compartidos](#shared)

>[!NOTE]
>
>Para obtener más información sobre el formato requerido para implementar los módulos de biblioteca en las extensiones web, consulte la [descripción general sobre el formato de los módulos](./web/format.md).

#### Tipos de eventos {#web-event}

Un evento de regla es una actividad que debe producirse antes de que se active una regla.

Por ejemplo, una extensión podría proporcionar un tipo de evento de &quot;gesto&quot; que supervise la producción de un determinado gesto táctil o movimiento del ratón. Una vez que se produce el gesto, la lógica de evento activaría la regla.

Los tipos de eventos suelen consistir en (1) una vista mostrada dentro de la interfaz de usuario de la recopilación de datos que permite a los usuarios modificar la configuración del evento y (2) un módulo de biblioteca emitido dentro de la biblioteca de tiempo de ejecución de etiquetas para interpretar la configuración y observar si se produce una determinada actividad.

[Más información](./web/event-types.md)

#### Tipos de condición {#web-condition}

Las condiciones de regla siempre se evalúan después de que se haya producido un evento de regla. Todas las condiciones deben devolver el valor verdadero para que la regla pueda continuar el procesamiento. La excepción se produce cuando los usuarios colocan explícitamente condiciones en un bloque de &quot;excepción&quot;, en cuyo caso todas las condiciones del bloque deben arrojar un valor falso para que la regla se pueda seguir procesando.

Por ejemplo, una extensión podría proporcionar un tipo de condición &quot;la ventanilla contiene&quot; en la que el usuario de podría especificar un selector CSS. Cuando la condición se evalúa en el sitio web del cliente, la extensión puede encontrar elementos que coincidan con el selector de CSS y devolver si alguno de ellos se incluye en la ventanilla del usuario.

Los tipos de condición suelen consistir en (1) una vista mostrada dentro de la interfaz de usuario de recopilación de datos que permite a los usuarios modificar la configuración de la condición y (2) un módulo de biblioteca emitido dentro de la biblioteca de tiempo de ejecución de etiquetas para interpretar la configuración y evaluar una condición.

[Más información](./web/condition-types.md)

#### Tipos de acción {#web-action}

Una acción de regla es algo que se realiza después de que se haya producido el evento de la regla y de que las condiciones hayan superado la evaluación.

Por ejemplo, una extensión podría proporcionar un tipo de acción &quot;mostrar chat de asistencia&quot; que puede mostrar un cuadro de diálogo de chat de asistencia técnica para ayudar a los usuarios con problemas para efectuar sus pagos.

Los tipos de acción suelen consistir en (1) una vista mostrada dentro de la interfaz de usuario de la recopilación de datos que permite a los usuarios modificar la configuración de la acción y (2) un módulo de biblioteca emitido dentro de la biblioteca de tiempo de ejecución de etiquetas para interpretar la configuración y realizar una acción.

[Más información](./web/action-types.md)

#### Tipos de elementos de datos {#web-data-element}

Los elementos de datos son esencialmente alias de datos de una página, sin importar si dichos datos se encuentran en parámetros de cadenas de consulta, cookies, elementos DOM o en algún otro lugar. Las reglas pueden hacer referencia a un elemento de datos y este puede actuar como una abstracción para acceder a estos fragmentos de datos. Cuando la ubicación de los datos cambie en el futuro (por ejemplo, de `innerHTML` de un elemento DOM al valor de una variable de JavaScript), se puede volver a configurar un único elemento de datos y mantener sin cambios a todas las reglas que hacen referencia a dicho elemento de datos.

Un tipo de elemento de datos permite a los usuarios configurar los elementos de datos para acceder a un fragmento de datos de una manera determinada. Por ejemplo, una extensión podría proporcionar un tipo de elemento de datos &quot;elemento de almacenamiento local&quot; en el que el usuario de podría especificar un nombre de elemento de almacenamiento local. Cuando una regla hace referencia al elemento de datos, la extensión puede buscar el valor del elemento de almacenamiento local utilizando el nombre del elemento de almacenamiento local que el usuario proporcionó al configurar el elemento de datos.

Los tipos de elementos de datos suelen consistir en (1) una vista mostrada dentro de la interfaz de usuario de recopilación de datos que permite a los usuarios modificar la configuración del elemento de datos y (2) un módulo de biblioteca emitido dentro de la biblioteca de tiempo de ejecución de etiquetas para interpretar la configuración y recuperar fragmentos de datos.

[Más información](./web/data-element-types.md)

#### Módulos compartidos {#shared}

Un módulo compartido es un módulo que expone una extensión para que otra pueda acceder a él. Este puede ser un mecanismo muy útil para la comunicación entre extensiones. Por ejemplo, la extensión A puede cargar un fragmento de datos asincrónicamente y ponerlo a disposición de la extensión B mediante una [promesa](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise).

Los módulos compartidos se incluyen en la biblioteca incluso si nunca se les llama desde otras extensiones. Para no incrementar el tamaño de la biblioteca de manera innecesaria, debe tener cuidado con lo que expone como módulo compartido.

Los módulos compartidos no tienen componente de vista.

[Más información](./web/shared.md)

### Módulos para extensiones de Edge {#edge-modules}

En las extensiones de Edge, las reglas se activan mediante comprobaciones de condiciones que luego ejecutan acciones específicas si se superan dichas comprobaciones. Consulte la descripción general del [flujo de módulos en extensiones de Edge](./edge/flow.md) para obtener más información.

Puede definir sus propios módulos de biblioteca en las extensiones de Edge. Se pueden clasificar en los tipos siguientes:

* [Tipos de condición](#condition)
* [Tipos de acción](#action)
* [Tipos de elementos de datos](#data-element)

>[!NOTE]
>
>Para obtener más información sobre el formato requerido para implementar módulos de biblioteca en extensiones de Edge, consulte la [descripción general del formato de los módulos](./edge/format.md).

#### Tipos de condición {#condition}

Las condiciones de regla siempre se evalúan después de que se haya producido un evento de regla. Todas las condiciones deben devolver el valor verdadero para que la regla pueda continuar el procesamiento. La excepción se produce cuando los usuarios colocan explícitamente condiciones en un bloque de &quot;excepción&quot;, en cuyo caso todas las condiciones del bloque deben arrojar un valor falso para que la regla se pueda seguir procesando.

Por ejemplo, una extensión podría proporcionar un tipo de condición &quot;la ventanilla contiene&quot; en la que el usuario de podría especificar un selector CSS. Cuando la condición se evalúa en el sitio web del cliente, la extensión puede encontrar elementos que coincidan con el selector de CSS y devolver si alguno de ellos se incluye en la ventanilla del usuario.

Los tipos de condición suelen consistir en (1) una vista mostrada dentro de la interfaz de usuario de recopilación de datos que permite a los usuarios modificar la configuración de la condición y (2) un módulo de biblioteca emitido dentro de la biblioteca de tiempo de ejecución de etiquetas para interpretar la configuración y evaluar una condición.

[Más información](./web/condition-types.md)

#### Tipos de acción {#action}

Una acción de regla es algo que se realiza después de que las condiciones de las reglas hayan superado la evaluación.

Por ejemplo, una extensión podría proporcionar un tipo de acción &quot;mostrar chat de asistencia&quot; que puede mostrar un cuadro de diálogo de chat de asistencia técnica para ayudar a los usuarios con problemas para efectuar sus pagos.

Los tipos de acción suelen consistir en (1) una vista mostrada dentro de la interfaz de usuario de la recopilación de datos que permite a los usuarios modificar la configuración de la acción y (2) un módulo de biblioteca emitido dentro de la biblioteca de tiempo de ejecución de etiquetas para interpretar la configuración y realizar una acción.

[Más información](./web/action-types.md)

#### Tipos de elementos de datos {#data-element}

Los elementos de datos son esencialmente alias de datos de una página, independientemente de dónde se encuentren dichos datos dentro del evento que recibe el servidor. Las reglas pueden hacer referencia a un elemento de datos y este puede actuar como una abstracción para acceder a estos fragmentos de datos. Cuando la ubicación de los datos cambie en el futuro (por ejemplo, al cambiar la clave del evento que contiene el valor), se puede volver a configurar un único elemento de datos y mantener sin cambios a todas las reglas que hacen referencia a dicho elemento de datos.

Los tipos de elementos de datos suelen consistir en (1) una vista mostrada dentro de la interfaz de usuario de recopilación de datos que permite a los usuarios modificar la configuración del elemento de datos y (2) un módulo de biblioteca emitido dentro de la biblioteca de tiempo de ejecución de etiquetas para interpretar la configuración y recuperar fragmentos de datos.

[Más información](./web/data-element-types.md)

## Configuración de extensión

La configuración de una extensión hace referencia a la manera en que recopila la configuración global de un usuario. Por ejemplo, considere una extensión que permita al usuario enviar una señalización mediante la acción Enviar señalización y tenga en cuenta que la señalización siempre debe contener un ID de cuenta. No queremos molestar a los usuarios pidiéndoles el ID de cuenta cada vez que configuren una acción Enviar señalización. En su lugar, la extensión debe solicitar el ID de la cuenta una vez desde la vista de configuración de la extensión. De este modo, cada vez que se envíe una señalización, el módulo de biblioteca de acciones Enviar señalización podrá extraer el ID de cuenta de la configuración de la extensión y añadirlo a la señalización.

Cuando los usuarios instalan una extensión en una propiedad de etiqueta, se les mostrará la vista de configuración de la extensión. No pueden completar la instalación de la extensión sin completar la configuración de la extensión.

La configuración de la extensión consiste en un componente de vista que exportará los ajustes que luego se emiten dentro de la biblioteca de tiempo de ejecución de etiquetas como un objeto sin formato.

[Más información](./configuration.md)

## Estructura de las extensiones

Una extensión consiste en un directorio de archivos. A continuación se ofrece información general de cómo se deben estructurar estos archivos. Encontrará detalles sobre el contenido del archivo en otras secciones.

Debe existir un archivo [`extension.json`](./manifest.md) en la raíz del directorio. Dicho archivo, entre otras cosas, describirá la composición de la extensión y la ubicación de ciertos archivos en el directorio. Este archivo se parece al archivo [`package.json`](https://docs.npmjs.com/files/package.json) de [npm](https://www.npmjs.com/).

Cada módulo de biblioteca (la lógica que se emitirá dentro de la biblioteca de tiempo de ejecución de etiquetas) debe ser su propio archivo cuyo contenido siga el [CommonJS module standard](http://wiki.commonjs.org/wiki/Modules/1.1.1). Por ejemplo, si estamos generando un tipo de acción &quot;enviar señalización&quot;, debemos disponer de un archivo que contenga la lógica que envía la señalización. El contenido de este archivo se emitirá en la biblioteca de tiempo de ejecución de etiquetas. Puede llamarlo `sendBeacon.js`. La ubicación del archivo en el directorio no es importante, ya que `extension.json` describirá dónde se encuentra.

Cada vista debe ser un archivo HTML que se pueda cargar en un iframe dentro de la aplicación de etiquetas. La vista debe incluir una secuencia de comandos proporcionada por etiquetas y ajustarse a una pequeña API para comunicarse con la aplicación. No hay restricciones en cuanto a las bibliotecas que se utilizan en sus vistas. En otras palabras, puede utilizar jQuery, Guión bajo, Reacción, Angular, Bootstrap u otras bibliotecas. Sin embargo, esperamos que su extensión tenga una apariencia similar a la de la aplicación.

Se recomienda colocar todos los archivos relacionados con la vista (HTML, CSS, JavaScript) en un único subdirectorio aislado de los archivos del módulo de biblioteca. En el archivo `extension.json` describirá dónde se encuentra este subdirectorio de vista. Platform servirá este subdirectorio (y solo este subdirectorio) desde sus servidores web.
