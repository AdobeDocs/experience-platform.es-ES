---
keywords: Experience Platform;inicio;temas populares;orígenes;conectores;conectores de origen;sdk de fuentes;sdk;SDK
solution: Experience Platform
title: Documentar el origen
description: El paso final antes de que la nueva fuente se pueda publicar en Adobe Experience Platform es documentar la nueva fuente.
exl-id: 80daadb1-127f-4f42-8bc9-fb89a7898462
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# Documentar el origen

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

Puede utilizar un [plantilla de documentación](./template.md) para ayudarle a crear documentación para su origen. A continuación, encontrará instrucciones sobre cómo editar la plantilla y abrir una solicitud de extracción. La documentación enviada para su nueva fuente será revisada y publicada por el equipo de documentación de Adobe.

También puede descargar las plantillas de documentación siguientes:

* [Plantilla de documentación de API](../assets/api-template.zip)
* [Plantilla de documentación de la interfaz de usuario](../assets/ui-template.zip)

## Crear la nueva página de origen

Puede utilizar la interfaz web de GitHub o el entorno local para crear documentación para la nueva fuente en Platform. Busque instrucciones para ambas opciones en los vínculos siguientes:

* [Utilice la interfaz web de GitHub para crear una página de documentación de origen](./github.md)
* [Utilice un editor de texto en el entorno local para crear una página de documentación de origen](./text-editor.md)
