---
title: Prácticas recomendadas de creación
description: Descubra qué reglas y sugerencias debe seguir al crear la página de documentación de destino para asegurarse de que cumple los estándares de calidad de la documentación de Adobe Experience Platform.
exl-id: b12059f1-6635-41cd-acc5-6ff471111164
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# Prácticas recomendadas de creación

## Información general {#overview}

En esta página se describen las reglas que debe seguir al [crear su página de ](./documentation-instructions.md) documentación de destino para asegurarse de que cumple los estándares de calidad de la documentación de Adobe Experience Platform.

## Directrices generales {#general-guidance}

* Al rellenar la [plantilla](./self-service-template.md) para la documentación de destino, consulte la guía del colaborador de Adobe para obtener información sobre la [vinculación](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=es), las [tablas](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=es#tables), la [sintaxis de markdown admitida](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=es), la [guía de escritura](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html?lang=es) y más.
* No incluya observaciones y estimaciones en la documentación del producto.
* En la documentación de Experience Platform, los redactores de Adobe usan **formato de negrita** para hacer referencia a los controles de la interfaz de usuario, de esta manera:
   * Vaya a **[!UICONTROL Conexiones]** > **[!UICONTROL Destinos]** y seleccione la ficha **[!UICONTROL Catálogo]**. Vea un ejemplo de cómo se documentan los controles de la interfaz de usuario en un [tutorial de destinos](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=es#select-destination).

## Estilo de escritura

>[!IMPORTANT]
>
>Lea [Guía de escritura para la documentación de Adobe](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html?lang=es) antes de empezar a crear la página de documentación de destino.

* Mantén tus frases cortas y ve al grano rápidamente. Si tu frase tiene más de 20 palabras o usa múltiples comas, considera separarla en oraciones separadas. Las frases de más de 20 palabras pueden ser especialmente difíciles para los lectores.
* No seas excesivamente educado. Evite utilizar &quot;por favor&quot; o &quot;amablemente haga...&quot; en la documentación técnica.

## Vinculación {#linking}

Siga la plantilla de documentación proporcionada y no edite los vínculos existentes en la plantilla. Cuando incluya nuevos vínculos, lea [usando vínculos en la documentación](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=es) de la guía del colaborador.

## Directrices de marca {#branding}

* AEP no es un término público aprobado. Utilice Adobe Experience Platform en el primer uso, luego Experience Platform y después Experience Platform.
   * **No uses**: Para poder exportar datos de AEP a tu destino, asegúrate de leer y completar estos requisitos previos.
   * **Usar**: para poder exportar datos de Adobe Experience Platform a tu destino, asegúrate de leer y completar estos requisitos previos.

## Imágenes y capturas de pantalla {#images-and-screenshots}

* Para obtener información sobre [cómo vincular a imágenes](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=es#images), consulte la guía del colaborador.
* Cuando utilice capturas de pantalla, asegúrese de que la captura de pantalla capture toda la pantalla de la interfaz de usuario de Experience Platform.
* Al marcar imágenes para resaltar un control o una etiqueta determinados en la página, intente seguir el estilo de marcado utilizado por el equipo de documentación de Experience Platform. Observe cómo Basado en perfiles se resalta en [esta captura de pantalla](/help/destinations/catalog/cloud-storage/amazon-s3.md#export-type-frequency).
* Utilice `png` imágenes de formato.
* No utilice capturas de pantalla numeradas como nombres de archivo. Los nombres de archivo de imagen deben ser descriptivos.
   * **No use**: `1.png`, `2.png`, `3.png`
   * **Usar**: `yourdestination-authentication-details.png`, `yourdestination-destination-details.png`
* Utilice texto alternativo para cualquier imagen que agregue a la documentación y utilice la gramática adecuada en el texto alternativo.
   * **No usar**: detalles de conexión de destino
   * **Usar**: imagen de la interfaz de usuario de Experience Platform que muestra los detalles de conexión de destino rellenados.

## Proceso {#process}

* La [plantilla de documentación](./self-service-template.md) se actualiza con poca frecuencia, según los comentarios del socio. Antes de empezar a crear documentación para tu destino, asegúrate de haber descargado la [última versión de la plantilla](../assets/docs-framework/yourdestination-template.zip).
* Cree la documentación y la solicitud de extracción de documentación (PR) a partir de una rama de su ramificación *distinta de la rama principal*. Consulte la sección enviar destino para revisión cuando cree en la [interfaz de GitHub](./use-github-interface-to-create-documentation.md#submit-review) o en [su entorno local](./work-in-local-environment.md#submit-review).
