---
title: Documente su destino en Adobe Experience Platform
description: Instrucciones paso a paso para crear una página de documentación para su destino en Adobe Experience Platform
exl-id: 6cc9c758-44bb-463b-941a-06b1a22ee8f3
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# Documente su destino en Adobe Experience Platform

>[!IMPORTANT]
>
>El proceso documentado aquí solo es necesario para los socios que envían destinos productizados (públicos). Si está creando un destino privado para su propio uso, no necesita crear y publicar documentación para su destino.

## Información general {#overview}

Bienvenido a Adobe Experience Platform. ¡Encantado de tenerle aquí!
Documentar el destino es el paso final antes de poder configurarlo en Adobe Experience Platform.

Esta sección de documentación incluye:

* Instrucciones paso a paso para crear una página de documentación para el nuevo destino;
* Una plantilla para que la rellene en su destino;
* [Instrucciones generales sobre el uso de Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html);
* [Instrucciones específicas para el sabor del Adobe Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html#custom-markdown-extensions) (el sabor del Adobe Markdown es muy similar al Markdown normal).
* Una [página de prácticas recomendadas](./authoring-best-practices.md) que le ayudará a crear una página de documentación para su página de destino que cumpla los estándares de calidad de Experience Platform.

## Requisitos previos {#prerequisites}

Para crear documentación para el destino según las instrucciones de este artículo, son necesarios los siguientes elementos:

* **Una cuenta de GitHub**. Regístrate en [GitHub](https://github.com/) si aún no tienes una cuenta.
* **Escritorio de GitHub**. Si decide [crear la documentación en su entorno local](./work-in-local-environment.md), debe usar [GitHub Desktop](https://desktop.github.com/).
* La integración con Adobe debe estar en una fase de prueba con el destino implementado en un entorno de ensayo en Adobe Experience Platform.

## Instrucciones generales para crear documentación para su destino en Adobe Experience Platform {#high-level-instructions}

En un nivel superior, para crear documentación para tu destino, necesitas [crear una ramificación](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html#fork-the-repository) del repositorio de documentación de Adobe Experience Platform y editar la [plantilla de documentación proporcionada](./self-service-template.md) en una nueva rama. Utilice la plantilla proporcionada por el Adobe para crear una nueva página de destino. Abra una solicitud de extracción (PR) cuando esté listo. Las instrucciones para hacerlo se encuentran más abajo, en [Pasos para crear la nueva página de destino](./documentation-instructions.md#steps-to-create-docs-page).

<!--

* In the table of contents (TOC.md) `/help/rtcdp/TOC.md`, add a link to your new destination page. Place it within the category where your destination resides in the Adobe Experience Platform user interface (for example: mobile, social, advertising). 
* In the overview page for the respective category, add a link to your new destination page. For example, for cloud storage destinations, you would add a link to [this page](https://docs.adobe.com/content/help/en/experience-platform/rtcdp/destinations/destinations-cat/cloud-storage/cloud-storage-destinations.html). 

-->

## Plantilla de documentación {#documentation-template}

Para ayudarle a crear su página de documentación, Adobe ha rellenado previamente una [plantilla de documentación](./self-service-template.md) para usted. Más adelante, encontrará instrucciones sobre cómo editar la plantilla y abrir una solicitud de extracción. El equipo de documentación de Adobe revisará y publicará la documentación del nuevo destino.

[Descargue la plantilla aquí](../assets/docs-framework/yourdestination-template.zip) y descomprima el archivo para extraer el archivo `yourdestination.md`.

A continuación, se proporcionan instrucciones sobre el uso de la plantilla para crear la página de documentación.

## Pasos para crear la nueva página de destino {#steps-to-create-docs-page}

Puede utilizar la interfaz web de GitHub o el entorno local para crear documentación para el nuevo destino en Adobe Experience Platform. Encuentre instrucciones para ambas opciones en los siguientes vínculos:

* [Utilice la interfaz web de GitHub para crear una página de documentación de destino](./use-github-interface-to-create-documentation.md)
* [Utilice un editor de texto en el entorno local para crear una página de documentación de destino](./work-in-local-environment.md)

## Prácticas recomendadas {#best-practices}

Revise las [prácticas recomendadas de creación](/help/destinations/destination-sdk/docs-framework/authoring-best-practices.md) antes y durante la creación de la página de documentación de destino. Asegúrese de leer también las [instrucciones de escritura para la documentación de Adobe](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html) para obtener más sugerencias de escritura que el equipo de documentación de Adobe usa al crear la documentación.