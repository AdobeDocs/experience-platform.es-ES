---
keywords: Experience Platform;inicio;temas populares;fuentes;conectores;conectores de origen;sdk de fuentes;sdk;SDK
solution: Experience Platform
title: Documentar el origen
description: El paso final antes de que la nueva fuente se pueda activar en Adobe Experience Platform es documentar la nueva fuente.
exl-id: 80daadb1-127f-4f42-8bc9-fb89a7898462
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 0%

---

# Documente su origen

El paso final antes de que el nuevo origen se pueda establecer en Adobe Experience Platform es documentar el nuevo origen.

Esta guía de documentación incluye:

* Un tutorial que puede seguir para crear una página de documentación para el nuevo origen;
* Una plantilla de documentación para que la rellene para su nuevo origen;
* [Instrucciones sobre cómo utilizar Markdown para escribir documentación técnica](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html);
* [Instrucciones para comprender el sabor de Adobe Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html#custom-markdown-extensions).

## Requisitos previos

Se requieren los siguientes elementos antes de poder documentar la nueva fuente:

* **Una cuenta de usuario de GitHub válida**: Si no tiene una cuenta de GitHub existente, debe crearla mediante la variable [Página de registro de GitHub](https://github.com/);
* **Acceso a GitHub Desktop**: debe utilizar el [Aplicación de escritorio de GitHub](https://desktop.github.com/) para crear la documentación de origen en el entorno local;
* La integración con Adobe debe estar en una fase de prueba con el origen implementado en un entorno de ensayo en Platform.

## Instrucciones de alto nivel para crear documentación para su origen en Platform

En un nivel superior, para crear documentación para el origen, debe crear una ramificación del repositorio de documentación de Platform y editar la plantilla de documentación proporcionada en una nueva rama. Utilice la plantilla proporcionada por el Adobe para crear una nueva página de origen y abrir una solicitud de extracción (PR) cuando esté listo. Las instrucciones para hacerlo se encuentran más abajo, en pasos para crear la nueva página de origen.

## Plantilla de documentación

Puede usar una etiqueta precargada [plantilla de documentación](./template.md) para ayudarle a crear la documentación de su origen. Más abajo encontrará instrucciones sobre cómo editar la plantilla y abrir una solicitud de extracción. El equipo de documentación del Adobe revisará y publicará la documentación enviada para la nueva fuente.

También puede descargar las plantillas de documentación a continuación:

* [Plantilla de documentación de API](../assets/api-template.zip)
* [Plantilla de documentación de IU](../assets/ui-template.zip)

## Crear la nueva página de origen

Puede utilizar la interfaz web de GitHub o el entorno local para crear documentación para la nueva fuente en Platform. Encuentre instrucciones para ambas opciones en los siguientes vínculos:

* [Utilice la interfaz web de GitHub para crear una página de documentación de origen](./github.md)
* [Utilice un editor de texto en el entorno local para crear una página de documentación de origen](./text-editor.md)
