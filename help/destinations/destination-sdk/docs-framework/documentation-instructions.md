---
title: Documentar el destino en Adobe Experience Platform
description: Instrucciones paso a paso para crear una página de documentación para su destino en Adobe Experience Platform
exl-id: 6cc9c758-44bb-463b-941a-06b1a22ee8f3
source-git-commit: ffd87573b93d642202e51e5299250a05112b6058
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 1%

---

# Documentar el destino en Adobe Experience Platform

>[!IMPORTANT]
>
>El proceso documentado aquí solo es necesario para socios que envían destinos productizados (públicos). Si está creando un destino privado para su propio uso, no necesita crear y publicar documentación para su destino.

## Información general {#overview}

Bienvenido a Adobe Experience Platform, bueno de tenerte aquí!
La documentación del destino es el último paso para que se pueda establecer en Adobe Experience Platform.

Esta sección de documentación incluye:

* Instrucciones paso a paso para crear una página de documentación para el nuevo destino;
* Una plantilla que puede rellenar para su destino;
* [Instrucciones generales sobre el uso de Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en);
* [Instrucciones específicas para el sabor de Markdown del Adobe](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en#custom-markdown-extensions) (el sabor del Adobe Markdown es muy similar al de Markdown normal).
* A [página prácticas recomendadas](./authoring-best-practices.md) para ayudarle a crear una página de documentación para su página de destino, que cumpla los estándares de calidad de la documentación del Experience Platform.

## Requisitos previos {#prerequisites}

Para crear documentación para el destino según las instrucciones de este artículo, son necesarios los siguientes elementos:

* **Una cuenta de GitHub**. Regístrese para [GitHub](https://github.com/) si todavía no tiene una cuenta.
* **Escritorio de GitHub**. Si selecciona [cree la documentación en el entorno local](./work-in-local-environment.md), debe usar [Escritorio de GitHub](https://desktop.github.com/).
* La integración con Adobe debe estar en una fase de prueba con el destino implementado en un entorno de ensayo en Adobe Experience Platform.

## Instrucciones de alto nivel para crear documentación para su destino en Adobe Experience Platform {#high-level-instructions}

En un nivel superior, para crear documentación para el destino, debe [crear una ramificación](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#fork-the-repository) del repositorio de documentación de Adobe Experience Platform y edite el [plantilla de documentación proporcionada](./self-service-template.md) en una rama nueva. Utilice la plantilla proporcionada por el Adobe para crear una nueva página de destino. Abra una solicitud de extracción (PR) cuando esté listo. Las instrucciones para hacerlo se detallan a continuación, en [Pasos para crear la nueva página de destino](./documentation-instructions.md#steps-to-create-docs-page).

<!--

* In the table of contents (TOC.md) `/help/rtcdp/TOC.md`, add a link to your new destination page. Place it within the category where your destination resides in the Adobe Experience Platform user interface (for example: mobile, social, advertising). 
* In the overview page for the respective category, add a link to your new destination page. For example, for cloud storage destinations, you would add a link to [this page](https://docs.adobe.com/content/help/en/experience-platform/rtcdp/destinations/destinations-cat/cloud-storage/cloud-storage-destinations.html). 

-->

## Plantilla de documentación {#documentation-template}

Para ayudarle a crear su página de documentación, Adobe ha rellenado previamente un [plantilla de documentación](./self-service-template.md) para usted. Más abajo, puede encontrar instrucciones para editar la plantilla y abrir una solicitud de extracción. El equipo de documentación de Adobe revisará y publicará la documentación de su nuevo destino.

[Descargue la plantilla aquí](../assets/docs-framework/yourdestination-template.zip) y descomprima el archivo para extraer el `yourdestination.md` archivo.

A continuación se ofrecen instrucciones sobre el uso de la plantilla para crear la página de documentación.

## Pasos para crear la nueva página de destino {#steps-to-create-docs-page}

Puede utilizar la interfaz web de GitHub o el entorno local para crear documentación para el nuevo destino en Adobe Experience Platform. Busque instrucciones para ambas opciones en los vínculos siguientes:

* [Utilice la interfaz web de GitHub para crear una página de documentación de destino](./use-github-interface-to-create-documentation.md)
* [Utilice un editor de texto en el entorno local para crear una página de documentación de destino](./work-in-local-environment.md)

## Prácticas recomendadas {#best-practices}

Consulte la [prácticas recomendadas de creación](/help/destinations/destination-sdk/docs-framework/authoring-best-practices.md) antes y mientras crea la página de documentación de destino. Asegúrese de leer también el [guía de escritura para la documentación de Adobe](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html?lang=en) para obtener más sugerencias de escritura que utiliza el equipo de documentación de Adobe al crear la documentación.