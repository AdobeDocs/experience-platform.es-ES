---
title: 'Adobe Destinatario y el SDK web de Adobe Experience Platform. '
seo-title: SDK web de Adobe Experience Platform y uso de Adobe Destinatario
description: Obtenga información sobre cómo procesar contenido personalizado con el SDK web de la plataforma de experiencia mediante Adobe Destinatario
seo-description: Obtenga información sobre cómo procesar contenido personalizado con el SDK web de la plataforma de experiencia mediante Adobe Destinatario
translation-type: tm+mt
source-git-commit: db4bfec04a1116ce2b6a0be7ca0e8cb2f9639ad6

---


# Información general de Destinatario

El SDK web de Adobe Experience Platform está integrado con Adobe Destinatario mediante esa función [de](../../fundamentals/rendering-personalization-content.md) personalización y le permite ofrecer contenido y decisiones personalizados de forma sencilla.

## Activación de Adobe Destinatario

Para habilitar Destinatario, deberá hacer lo siguiente:

- Habilite el destinatario en la configuración [de](../../fundamentals/edge-configuration.md) Edge con el código de cliente adecuado.
- Añada la `renderDecisions` opción a sus eventos.

De forma opcional, también puede:

- Añada `scopes` a sus eventos para recuperar actividades específicas (útil para actividades creadas con el compositor basado en formularios).
- Añada el [fragmento](../../fundamentals/managing-flicker.md) de ocultamiento previo para ocultar solo determinadas partes de la página.

## Uso del VEC

Con el SDK puede utilizar el VEC normalmente con una excepción, necesitará la extensión [auxiliar de VEC de](https://docs.adobe.com/content/help/en/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) destinatario instalada y activa.

## Uso del Compositor basado en formularios

El compositor basado en formularios se puede utilizar también para devolver contenido. Los ámbitos aparecerán como ubicaciones (mBoxes) en la interfaz de usuario de Destinatario. También debe asegurarse de que el desarrollador está buscando las respuestas si decide utilizar ámbitos.

## Audiencias en XDM

Dentro de Destinatario, los datos XDM se mostrarán en el Generador de Audiencias como un parámetro personalizado. El XDM se serializa mediante notación de puntos (p. ej. `web.webPageDetails.name`)

## Terminología

__Decisiones__ : En Destinatario, se correlacionan con la experiencia seleccionada de una Actividad.

__Ámbito__ : el ámbito de aplicación de la decisión. En Destinatario, este es el mBox. El mbox global es el `__view__` ámbito.

__Esquema__ - El esquema de una decisión es el tipo de oferta en el Destinatario.

__XDM__ : el XDM se serializa en notación de puntos y luego se coloca en Destinatario como parámetros mBox.