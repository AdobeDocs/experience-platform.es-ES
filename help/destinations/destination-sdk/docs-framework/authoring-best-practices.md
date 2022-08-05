---
title: Prácticas recomendadas sobre la creación
description: Conozca qué reglas y sugerencias debe seguir al crear su página de documentación de destino, para asegurarse de que cumple los estándares de calidad de la documentación de Adobe Experience Platform.
exl-id: b12059f1-6635-41cd-acc5-6ff471111164
source-git-commit: 0b9b724c2530e43ce681011d12fc1341148ddbf5
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

---

# Prácticas recomendadas sobre la creación

## Información general {#overview}

Esta página describe las reglas que debe seguir cuando [creación de la documentación de destino](./documentation-instructions.md) para garantizar que cumple los estándares de calidad de la documentación de Adobe Experience Platform.

## Directrices generales {#general-guidance}

* Al rellenar el [plantilla](./self-service-template.md) para la documentación de destino, consulte la guía del colaborador de Adobe para obtener información sobre [vinculación](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en), [tablas](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en#tables), el [sintaxis de markdown admitida](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en), [guía de escritura](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html?lang=en), y más.
* No incluya observaciones y estimaciones en la documentación del producto.
* En la documentación de Experience Platform, los autores de Adobes utilizan **formato negrita** para hacer referencia a los controles de la interfaz de usuario, haga lo siguiente:
   * Vaya a **[!UICONTROL Conexiones]** > **[!UICONTROL Destinos]** y seleccione **[!UICONTROL Catálogo]** pestaña . Ver un ejemplo de cómo se documentan los controles de la interfaz de usuario en un [tutorial de destinos](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en#select-destination).

## Estilo de escritura

>[!IMPORTANT]
>
>Lectura [Guía de escritura para la documentación de Adobe](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html?lang=en) antes de comenzar a crear la página de documentación de destino.

* Mantenga sus frases cortas y llegue al punto rápidamente. Si la oración tiene más de 20 palabras o usa varias comas, considere separarla en oraciones separadas. Las frases de más de 20 palabras pueden ser especialmente desafiantes para los lectores.
* No seas demasiado educado. Evite utilizar &quot;please&quot; (por favor) o &quot;do...&quot; (por favor). en la documentación técnica.

## Vinculación {#linking}

Siga la plantilla de documentación proporcionada y no edite los vínculos existentes en la plantilla. Cuando se incluyan vínculos nuevos, lea [uso de vínculos en la documentación](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en) en la guía del colaborador.

## Directrices de personalización {#branding}

* AEP no es un término público aprobado. Utilice Adobe Experience Platform en primer uso, luego Experience Platform y, por último, Platform.
   * **No use**: Antes de exportar datos de AEP a YourDestination, asegúrese de leer y completar estos requisitos previos.
   * **Uso**: Antes de exportar datos de Adobe Experience Platform a su destino, asegúrese de leer y completar estos requisitos previos.

## Imágenes y capturas de pantalla {#images-and-screenshots}

* Para obtener información sobre [cómo vincular a imágenes](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en#images), consulte la guía del colaborador.
* Cuando utilice capturas de pantalla, asegúrese de que la captura de pantalla captura toda la pantalla de la interfaz de usuario de Platform.
* Al marcar las imágenes para resaltar un determinado control o etiqueta en la página, intente seguir el estilo de marcado utilizado por el equipo de documentación del Experience Platform. Observe cómo se resalta la función basada en perfiles en [esta captura de pantalla](/help/destinations/catalog/cloud-storage/amazon-s3.md#export-type-frequency).
* Utilice `png` formatear imágenes.
* No utilice capturas de pantalla numeradas como nombres de archivo. Los nombres de archivo de imagen deben ser descriptivos.
   * **No use**: `1.png`, `2.png`, `3.png`
   * **Uso de**: `yourdestination-authentication-details.png`, `yourdestination-destination-details.png`
* Utilice texto alternativo para cualquier imagen que agregue a la documentación y utilice la gramática adecuada en el texto alternativo.
   * **No use**: Detalles de conexión de destino
   * **Uso**: Imagen de la interfaz de usuario de Platform que muestra los detalles de conexión de destino completados.

## Proceso {#process}

* La variable [plantilla de documentación](./self-service-template.md) se actualiza con poca frecuencia, en función de los comentarios de los socios. Antes de empezar a crear documentación para su destino, asegúrese de haber descargado la variable [versión más reciente de la plantilla](/help/destinations/destination-sdk/docs-framework/assets/yourdestination-template.zip).
* Cree la documentación y la solicitud de extracción (PR) de documentación desde una rama de su ramificación *distinto de la rama principal*. Consulte la sección Enviar destino para revisión al crear en la sección [Interfaz de GitHub](./use-github-interface-to-create-documentation.md#submit-review) o [su entorno local](./work-in-local-environment.md#submit-review).
