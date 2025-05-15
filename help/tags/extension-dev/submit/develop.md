---
title: Desarrollar una extensión
description: Este documento proporciona una visión general del proceso de desarrollo de extensiones de etiquetas, con vínculos a documentación adicional para ver procesos más detallados.
exl-id: fb2f7275-a5da-4a41-b915-822c71c02e5c
source-git-commit: cfcc70d66a34fa51bf0e21525539ba88de7fc367
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 96%

---

# Desarrollar una extensión

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un grupo de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

Una extensión de etiqueta debe considerarse como un producto (pequeño) con sus propios requisitos. Determinar cómo un usuario de Adobe Experience Platform querrá utilizar su extensión puede ayudarle a clasificar la funcionalidad según los tipos de evento, los tipos de condición, los tipos de acciones y los tipos de elementos de datos que debe proporcionar su extensión.

Con esos conocimientos puede planificar los componentes que se deben proporcionar en la extensión.

## Guías

Una vez establecido el plan, las directrices que se muestran a continuación pueden ayudarle a comprender el proceso de desarrollo de la extensión:

* La [guía de introducción](../getting-started.md) y otros documentos de **desarrollo de extensiones** en la navegación izquierda son buenos materiales de referencia para comprender las extensiones. Incluyen detalles sobre qué pueden hacer las extensiones, cómo se almacena y pasa la información de usuario entre su extensión y Adobe Experience Platform, cómo se agrupa el código en las bibliotecas, y cómo se interpreta y utiliza el código de extensión en el explorador durante la ejecución.
<!-- * The [extension tutorial video](https://youtu.be/rxjtC9o4rl0) is a great place to start. -->
* La lista de reproducción de YouTube [Introducción a las extensiones](https://www.youtube.com/playlist?list=PLOdw8u2F8CIgynzKrPEwCPuDxzHW1WP5m) le guiará por el proceso de creación de paquetes de extensión.
* [Explicación del esquema JSON](https://spacetelescope.github.io/understanding-json-schema/index.html#).
* [JSON Lint/Validator](https://jsonlint.com/).
* Extensión [JSON Viewer](https://chrome.google.com/webstore/detail/json-viewer/gbmdgpbipfallnflgajpaliibnhdgobh) para Chrome para resaltar e imprimir JSON y JSONP.
* Editor [jsonschema.net](https://jsonschema.net/#/editor) para ayudar a crear el esquema JSON a partir de su objeto.
* [JSON Schema Validator](https://www.jsonschemavalidator.net), que es un validador de esquemas JSON interactivo en línea.

## Herramientas

También encontrará una serie de herramientas npm para ayudarle con el desarrollo de su paquete de extensión:

* La [herramienta de andamiaje de extensiones](https://www.npmjs.com/package/@adobe/reactor-scaffold) le ayuda a crear con facilidad un proyecto de inicio en su equipo.
* La [zona protegida de extensiones de etiquetas](https://www.npmjs.com/package/@adobe/reactor-sandbox) le ayuda a validar sus módulos y vistas de extensión en su equipo local.
* El [empaquetador de extensiones](https://www.npmjs.com/package/@adobe/reactor-packager) es una utilidad de línea de comandos que permite empaquetar extensiones de etiqueta en archivos zip.
* El [cargador de extensiones de etiquetas](https://www.npmjs.com/package/@adobe/reactor-uploader) es una herramienta interactiva de línea de comandos que le ayudará a introducir las credenciales de su cuenta técnica y a cargar el paquete de extensión en las etiquetas.
* La [herramienta de lanzamiento de etiquetas](https://www.npmjs.com/package/@adobe/reactor-releaser) es una herramienta interactiva de línea de comandos que le ayudará con el lanzamiento privado de su extensión.

## Extensiones de ejemplo

Existen extensiones de ejemplo en GitHub que puede revisar o utilizar como proyectos iniciales:

* [Extensión de ejemplo de Hello World](https://github.com/adobe/reactor-helloworld-extension)
* [Extensión de ejemplo de Facebook](https://github.com/Adobe-Marketing-Cloud-Activation/extension-facebookpixel)
* [Extensión de ejemplo de Typekit](https://github.com/jeffchasin/extension-typekit)
* [Extensión de ejemplo de Pinterest](https://github.com/jeffchasin/extension-pinterest)

## Espacio de trabajo de Slack

Puede solicitar acceso al espacio de trabajo de la comunidad de Slack, donde los autores de las extensiones pueden ayudarse, mediante este [formulario de solicitud](https://docs.google.com/forms/d/e/1FAIpQLScq1m63YkDrRpvPLhzUqtfoleWiDDTTXZsSivIXRfFdlSMzpQ/viewform).

**Tenga en cuenta lo siguiente**: aunque hay miembros de Adobe en este espacio de trabajo de Slack, se trata de un recurso de la comunidad no patrocinado ni moderado por Adobe.
