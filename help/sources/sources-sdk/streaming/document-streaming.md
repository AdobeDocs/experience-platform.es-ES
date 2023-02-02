---
title: Documento de origen (SDK de transmisión)
description: El paso final antes de que la nueva fuente se pueda publicar en Adobe Experience Platform es documentar la nueva fuente.
hide: true
hidefromtoc: true
source-git-commit: a9879530a8911d77dfc4cde3824834e03fa5e0a9
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Documentar el origen (Streaming SDK)

El paso final antes de que el nuevo origen se pueda configurar en Adobe Experience Platform es documentar el nuevo origen.

Esta guía de documentación incluye:

* Un tutorial que puede seguir para crear una página de documentación para el nuevo origen;
* Una plantilla de documentación que puede rellenar para la nueva fuente;
* [Instrucciones sobre cómo utilizar Markdown para escribir documentación técnica](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en);
* [Instrucciones para comprender el sabor de Adobe Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en#custom-markdown-extensions).

## Requisitos previos

Los siguientes elementos son necesarios para poder empezar a documentar la nueva fuente:

* **Una cuenta de usuario de GitHub válida**: Si no tiene una cuenta de GitHub existente, debe crearla a través de la [Página de registro de GitHub](https://github.com/);
* **Acceso a GitHub Desktop**: Debe usar la variable [Aplicación de escritorio de GitHub](https://desktop.github.com/) para crear la documentación de origen en el entorno local;
* La integración con Adobe debe estar en una fase de prueba con el origen implementado en un entorno de ensayo en Platform.

## Instrucciones de alto nivel para crear documentación para la fuente en Platform

En un nivel superior, para crear documentación para la fuente, debe crear una ramificación del repositorio de documentación de Platform y editar la plantilla de documentación proporcionada en una nueva rama. Utilice la plantilla proporcionada por el Adobe para crear una nueva página de origen y abrir una solicitud de extracción (PR) cuando esté listo. Las instrucciones para ello se detallan a continuación, en los pasos para crear la nueva página de origen.

## Plantilla de documentación

Puede utilizar un [Plantilla de documentación de API](streaming-template-api.md) o [Plantilla de documentación de la interfaz de usuario](streaming-template-ui.md) para ayudarle a crear documentación para su origen. A continuación, encontrará instrucciones sobre cómo editar la plantilla y abrir una solicitud de extracción. La documentación enviada para su nueva fuente será revisada y publicada por el equipo de documentación de Adobe.

También puede descargar las plantillas de documentación siguientes:

* [Plantilla de documentación de API](../assets/streaming/streaming-template-api.zip)
* [Plantilla de documentación de la interfaz de usuario](../assets/streaming/streaming-template-ui.zip)

## Crear la nueva página de origen

Puede utilizar la interfaz web de GitHub o el entorno local para crear documentación para la nueva fuente en Platform. Busque instrucciones para ambas opciones en los vínculos siguientes:

* [Utilice la interfaz web de GitHub para crear una página de documentación de origen](../documentation/github.md)
* [Utilice un editor de texto en el entorno local para crear una página de documentación de origen](../documentation/text-editor.md)
