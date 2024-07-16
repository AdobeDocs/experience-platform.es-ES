---
title: Documente su Source (Streaming SDK)
description: El paso final antes de que la nueva fuente se pueda activar en Adobe Experience Platform es documentar la nueva fuente.
exl-id: 65ca7a4d-3e02-4f54-bf07-ea2c92b8dbf1
badge: Beta
source-git-commit: 256857103b4037b2cd7b5b52d6c5385121af5a9f
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---

# Documente su origen (Streaming SDK)

>[!NOTE]
>
>El SDK de flujo de fuentes de autoservicio está en versión beta. Lea [información general de orígenes](../../home.md#terms-and-conditions) para obtener más información sobre el uso de orígenes etiquetados como beta.

El paso final antes de que el nuevo origen se pueda establecer en Adobe Experience Platform es documentar el nuevo origen.

Esta guía de documentación incluye:

* Un tutorial que puede seguir para crear una página de documentación para el nuevo origen;
* Una plantilla de documentación para que la rellene para su nuevo origen;
* [Instrucciones sobre cómo usar Markdown para escribir documentación técnica](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html);
* [Instrucciones para comprender el sabor de Markdown de Adobe](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html#custom-markdown-extensions).

## Requisitos previos

Se requieren los siguientes elementos antes de poder documentar la nueva fuente:

* **Una cuenta de usuario de GitHub válida**: si no tiene una cuenta de GitHub existente, debe crearla a través de la [página de registro de GitHub](https://github.com/);
* **Acceso a GitHub Desktop**: debe usar la [aplicación GitHub Desktop](https://desktop.github.com/) para crear la documentación de origen en su entorno local;
* La integración con Adobe debe estar en una fase de prueba con el origen implementado en un entorno de ensayo en Platform.

## Instrucciones de alto nivel para crear documentación para su origen en Platform

En un nivel superior, para crear documentación para el origen, debe crear una ramificación del repositorio de documentación de Platform y editar la plantilla de documentación proporcionada en una nueva rama. Utilice la plantilla proporcionada por el Adobe para crear una nueva página de origen y abrir una solicitud de extracción (PR) cuando esté listo. Las instrucciones para hacerlo se encuentran más abajo, en pasos para crear la nueva página de origen.

## Plantilla de documentación

Puede usar una [plantilla de documentación de API](streaming-template-api.md) rellenada previamente o la [plantilla de documentación de IU](streaming-template-ui.md) para ayudar a crear documentación para su origen. Más abajo encontrará instrucciones sobre cómo editar la plantilla y abrir una solicitud de extracción. El equipo de documentación del Adobe revisará y publicará la documentación enviada para la nueva fuente.

También puede descargar las plantillas de documentación a continuación:

* [Plantilla de documentación de API](../assets/streaming/streaming-template-api.zip)
* [Plantilla de documentación de IU](../assets/streaming/streaming-template-ui.zip)

## Crear la nueva página de origen

Puede utilizar la interfaz web de GitHub o el entorno local para crear documentación para la nueva fuente en Platform. Encuentre instrucciones para ambas opciones en los siguientes vínculos:

* [Utilice la interfaz web de GitHub para crear una página de documentación de origen](../documentation/github.md)
* [Utilice un editor de texto en el entorno local para crear una página de documentación de origen](../documentation/text-editor.md)
