---
title: Desarrollar una extensión
description: Este documento proporciona una visión general del proceso de desarrollo de la extensión de etiquetas con vínculos a documentación adicional para procesos más detallados.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 43%

---

# Desarrollar una extensión

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

Una extensión de etiqueta debe considerarse como un producto (pequeño) con sus propios requisitos. Determinar cómo un usuario de Adobe Experience Platform querrá utilizar su extensión puede ayudarle a clasificar la funcionalidad según los tipos de evento, los tipos de condición, los tipos de acciones y los tipos de elementos de datos que debe proporcionar su extensión.

Con ese conocimiento, puede planificar qué componentes se deben proporcionar en la extensión.

## Guías

Una vez establecido el plan, las directrices que se muestran a continuación pueden ayudarle a comprender el proceso de desarrollo de la extensión:

* La [guía de introducción](../getting-started.md) y otros documentos en **Extension development** en la navegación izquierda son buenos materiales de referencia para comprender las extensiones. Incluyen detalles sobre qué extensiones pueden hacer, cómo se almacena y pasa la información de usuario entre la extensión y Adobe Experience Platform, cómo se agrupa el código en las bibliotecas y cómo se interpreta y utiliza el código de extensión en el explorador durante la ejecución.
* El [tutorial de extensión video](https://youtu.be/rxjtC9o4rl0) es un lugar bueno para comenzar.
* La lista de reproducción de YouTube [Introducción a las extensiones](https://www.youtube.com/playlist?list=PLOdw8u2F8CIgynzKrPEwCPuDxzHW1WP5m) le guiará por el proceso de creación de paquetes de extensión.
* [Explicación del esquema JSON](https://spacetelescope.github.io/understanding-json-schema/index.html#).
* [JSON Lint/Validator](http://jsonlint.com/).
* Extensión [JSON Viewer](https://chrome.google.com/webstore/detail/json-viewer/gbmdgpbipfallnflgajpaliibnhdgobh) para Chrome para resaltar e imprimir JSON y JSONP.
* Editor [jsonschema.net](https://jsonschema.net/#/editor) para crear esquemas JSON a partir de objetos..
* [JSON Schema Validator](http://www.jsonschemavalidator.net/), que es un validador de esquemas JSON interactivo en línea.

## Herramientas

También encontrará una serie de herramientas npm para ayudarle con el desarrollo de su paquete de extensión:

* [La herramienta de extensión de etiquetas Scaffold ](https://www.npmjs.com/package/@adobe/reactor-scaffold) ayuda a crear fácilmente un proyecto de inicio en el equipo local.
* [Tag Extension ](https://www.npmjs.com/package/@adobe/reactor-sandbox) Sandboxs le ayuda a validar sus vistas de extensión y módulos en el equipo local.
* [Tag Extension ](https://www.npmjs.com/package/@adobe/reactor-packager) Packagerers es una utilidad de línea de comandos para empaquetar una extensión de etiqueta en un archivo zip.
* [Tag Extension ](https://www.npmjs.com/package/@adobe/reactor-uploader) Uploader es una herramienta interactiva de línea de comandos que le ayuda a introducir sus credenciales de cuenta técnica y cargar el paquete de extensión en etiquetas.
* [Tag Extension ](https://www.npmjs.com/package/@adobe/reactor-releaser) Versiones es una herramienta interactiva de línea de comandos que le ayuda a liberar la extensión para que esté disponible en privado.

## Extensiones de ejemplo

Existen extensiones de ejemplo en GitHub que puede revisar o utilizar como proyectos iniciales:

* [Extensión de ejemplo de Hello World](https://github.com/adobe/reactor-helloworld-extension)
* [Extensión de ejemplo de Facebook](https://github.com/Adobe-Marketing-Cloud-Activation/extension-facebookpixel)
* [Extensión de ejemplo de Typekit](https://github.com/jeffchasin/extension-typekit)
* [Extensión de ejemplo de Pinterest](https://github.com/jeffchasin/extension-pinterest)

## Espacio de trabajo de Slack

Puede solicitar acceso al espacio de trabajo de la comunidad de Slack, donde los autores de las extensiones pueden admitirse entre sí mediante este [formulario de solicitud](http://join.launchdevelopers.chat).

**Tenga en cuenta**: aunque hay miembros del Adobe en este espacio de trabajo del Slack, es un recurso de la comunidad que no está patrocinado por el Adobe ni moderado por él.
