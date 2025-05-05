---
keywords: Experience Platform;inicio;temas populares;fuentes;conectores;conectores de origen;fuentes sdk;sdk;SDK
solution: Experience Platform
title: Documente su Source
description: El paso final antes de que la nueva fuente se pueda activar en Adobe Experience Platform es documentar la nueva fuente.
exl-id: 80daadb1-127f-4f42-8bc9-fb89a7898462
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---

# Documente su origen

El paso final antes de que el nuevo origen se pueda establecer en Adobe Experience Platform es documentar el nuevo origen.

Esta guía de documentación incluye:

* Un tutorial que puede seguir para crear una página de documentación para el nuevo origen;
* Una plantilla de documentación para que la rellene para su nuevo origen;
* [Instrucciones sobre cómo usar Markdown para escribir documentación técnica](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=es);
* [Instrucciones para comprender el sabor de Adobe Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=es#custom-markdown-extensions).

## Requisitos previos

Se requieren los siguientes elementos antes de poder documentar la nueva fuente:

* **Una cuenta de usuario de GitHub válida**: si no tiene una cuenta de GitHub existente, debe crearla a través de la [página de registro de GitHub](https://github.com/);
* **Acceso a GitHub Desktop**: debe usar la [aplicación GitHub Desktop](https://desktop.github.com/) para crear la documentación de origen en su entorno local;
* La integración con Adobe debe estar en una fase de prueba con el origen implementado en un entorno de ensayo en Experience Platform.

## Instrucciones generales para crear documentación para su origen en Experience Platform

En un nivel superior, para crear documentación para el origen, debe crear una ramificación del repositorio de documentación de Experience Platform y editar la plantilla de documentación proporcionada en una nueva rama. Utilice la plantilla proporcionada por Adobe para crear una nueva página de origen y abrir una solicitud de extracción (PR) cuando esté listo. Las instrucciones para hacerlo se encuentran más abajo, en pasos para crear la nueva página de origen.

## Plantilla de documentación

Puede usar una [plantilla de documentación](./template.md) rellenada previamente para ayudar a crear documentación para su origen. Más abajo encontrará instrucciones sobre cómo editar la plantilla y abrir una solicitud de extracción. El equipo de documentación de Adobe revisará y publicará la documentación enviada para el nuevo origen.

También puede descargar las plantillas de documentación a continuación:

* [Plantilla de documentación de API](../assets/api-template.zip)
* [Plantilla de documentación de IU](../assets/ui-template.zip)

## Crear la nueva página de origen

Puede utilizar la interfaz web de GitHub o el entorno local para crear documentación para la nueva fuente en Experience Platform. Encuentre instrucciones para ambas opciones en los siguientes vínculos:

* [Utilice la interfaz web de GitHub para crear una página de documentación de origen](./github.md)
* [Utilice un editor de texto en el entorno local para crear una página de documentación de origen](./text-editor.md)
