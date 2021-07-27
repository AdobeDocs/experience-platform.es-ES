---
title: Información general sobre el desarrollo de extensiones
description: Obtenga información sobre los componentes principales de diferentes tipos de extensión de etiquetas y el proceso de desarrollo de extensiones en Adobe Experience Platform.
source-git-commit: a165f0c254885b17db734ab09bf6523175a11dfb
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 21%

---

# Información general sobre el desarrollo de extensiones

>[!NOTE]
>
>Adobe Experience Platform Launch se está convirtiendo en un conjunto de tecnologías de recopilación de datos en Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

Uno de los objetivos principales de las etiquetas en Adobe Experience Platform es crear un ecosistema abierto en el que los ingenieros fuera del Adobe puedan exponer funcionalidades adicionales en sus sitios web y aplicaciones móviles. Esto se logra mediante extensiones de etiqueta. Una vez que se ha instalado una extensión en una propiedad de etiqueta, la funcionalidad de esa extensión está disponible para que la utilicen todos los usuarios de la propiedad.

Este documento describe los componentes principales de una extensión y proporciona vínculos a documentación adicional para ayudarle a guiarle en el proceso de desarrollo de la extensión.

## Estructura de las extensiones

Una extensión consiste en un directorio de archivos. Concretamente, una extensión consiste en un archivo de manifiesto, módulos de biblioteca y vistas.

### Archivo de manifiesto

Debe existir un archivo de manifiesto ([`extension.json`](./manifest.md)) en la raíz del directorio. Este archivo describe la composición de la extensión y dónde se encuentran ciertos archivos dentro del directorio. El manifiesto funciona de forma similar a un archivo [`package.json`](https://docs.npmjs.com/files/package.json) en un proyecto [npm](https://www.npmjs.com/).

### Módulos de biblioteca

Los módulos de biblioteca son los archivos que describen los diferentes [componentes](#components) que proporciona una extensión (es decir, la lógica que se emitirá dentro de la biblioteca de tiempo de ejecución de etiquetas). El contenido de cada archivo de módulo de biblioteca debe seguir el [Módulo CommonJS estándar](http://wiki.commonjs.org/wiki/Modules/1.1.1).

Por ejemplo, si está creando un tipo de acción denominado &quot;send beacon&quot;, debe tener un archivo que contenga la lógica que envía la señalización. Si utiliza JavaScript, el archivo podría llamarse `sendBeacon.js`. El contenido de este archivo se emitirá en la biblioteca de tiempo de ejecución de etiquetas.

Puede colocar archivos de módulo de biblioteca en cualquier lugar que desee dentro del directorio de extensión, siempre que describa sus ubicaciones en `extension.json`.

### Vistas

Una vista es un archivo HTML que puede cargarse en un elemento [`iframe`](https://developer.mozilla.org/es-ES/docs/Web/HTML/Element/iframe) dentro de la aplicación de etiquetas, específicamente a través de la interfaz de usuario de la recopilación de datos. La vista debe incluir una secuencia de comandos proporcionada por la extensión y ajustarse a una pequeña API para comunicarse con la aplicación.

El archivo de vista más importante para cualquier extensión es su configuración. Consulte la sección sobre [configuraciones de extensión](#configuration) para obtener más información.

No hay restricciones en cuanto a las bibliotecas que se utilizan en sus vistas. En otras palabras, puede utilizar jQuery, Guión bajo, Reacción, Angular, Bootstrap u otros. Sin embargo, se recomienda que la extensión tenga un aspecto similar al de la interfaz de usuario de recopilación de datos.

Se recomienda colocar todos los archivos relacionados con la vista (HTML, CSS, JavaScript) en un único subdirectorio aislado de los archivos del módulo de biblioteca. En `extension.json`, puede describir dónde se encuentra este subdirectorio de vista. Platform servirá este subdirectorio (y solo este subdirectorio) desde sus servidores web.

## Componentes de biblioteca {#components}

Cada extensión define un conjunto de funcionalidades. Estas funcionalidades se implementan al incluirse en una [biblioteca](../ui/publishing/libraries.md) que se implementa en el sitio web o la aplicación. Las bibliotecas son una colección de componentes individuales, que incluyen condiciones, acciones, elementos de datos y mucho más. Cada componente de biblioteca es un fragmento de código reutilizable (proporcionado por una extensión) que se emite dentro del tiempo de ejecución de etiquetas.

Dependiendo de si está desarrollando una extensión web o una extensión edge, los tipos de componentes disponibles y sus casos de uso difieren. Consulte las subsecciones siguientes para obtener una descripción general de los componentes disponibles para cada tipo de extensión.

### Componentes para extensiones web {#web}

En las extensiones web, las reglas se activan mediante eventos que pueden ejecutar acciones específicas si se cumple un conjunto determinado de condiciones. Consulte la descripción general del [flujo de módulos en extensiones web](./web/flow.md) para obtener más información.

Además de los [módulos principales](./web/core.md) proporcionados por Adobe, puede definir los siguientes componentes de biblioteca en sus extensiones web:

* [Eventos](./web/event-types.md)
* [Condiciones](./web/condition-types.md)
* [Acciones](./web/action-types.md)
* [Elementos de datos](./web/data-element-types.md)
* [Módulos compartidos](./web/shared.md)

>[!NOTE]
>
>Para obtener más información sobre el formato necesario para implementar componentes de biblioteca en extensiones web, consulte la [descripción general del formato del módulo](./web/format.md).

### Componentes para extensiones de borde {#edge}

En las extensiones de Edge, las reglas se activan mediante comprobaciones de condiciones que luego ejecutan acciones específicas si se superan dichas comprobaciones. Consulte la descripción general del [flujo de extensión de Edge](./edge/flow.md) para obtener más información.

Puede definir los siguientes componentes de biblioteca en las extensiones Edge:

* [Condiciones](./edge/condition-types.md)
* [Acciones](./edge/action-types.md)
* [Elementos de datos](./edge/data-element-types.md)

>[!NOTE]
>
>Para obtener más información sobre el formato requerido para implementar módulos de biblioteca en extensiones de Edge, consulte la [descripción general del formato de los módulos](./edge/format.md).

## Configuración de extensión {#configuration}

La configuración de una extensión hace referencia a la manera en que recopila la configuración global de un usuario. La configuración consiste en un componente de vista que exporta y emite la configuración dentro de la biblioteca de tiempo de ejecución de etiquetas como un objeto sin formato.

Por ejemplo, imaginemos una extensión que permite al usuario enviar una señalización mediante una acción &quot;Send Beacon&quot; y que la señalización siempre debe contener un ID de cuenta. En lugar de solicitar a los usuarios un ID de cuenta cada vez que configuran una acción &quot;Send Beacon&quot;, la extensión debe solicitar el ID de cuenta una vez desde la vista de configuración de la extensión. Cada vez que se envía una señalización, la acción &quot;Send Beacon&quot; puede extraer el ID de cuenta de la configuración de la extensión y añadirlo a la señalización.

Cuando los usuarios instalan una extensión en una propiedad en la interfaz de usuario, se les muestra la vista de configuración de la extensión, que deben completar para finalizar la instalación.

Para obtener más información, consulte la guía sobre [configuraciones de extensión](./configuration.md).

## Envío de extensiones

Una vez que haya terminado de crear la extensión, puede enviarla para que aparezca en el catálogo de extensiones en Platform. Consulte la [descripción general del proceso de envío de extensión](./submit/overview.md) para obtener más información.