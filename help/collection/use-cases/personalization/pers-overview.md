---
title: Información general sobre casos de uso de Personalization
description: Aprenda a implementar casos de uso de personalización mediante Adobe Experience Platform Web SDK, incluidos patrones para representar contenido y rastrear la visualización.
keywords: personalización;sendEvent;renderDecisions;applyPropositions;decisionScopes;mostrar eventos;parpadeo;
exl-id: 6beccbfd-fddb-4e19-8a56-caba276e1643
source-git-commit: caaf5cad7276d6429fbbf35585fd4845de6ff60c
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 0%

---

# Información general sobre casos de uso de Personalization

Adobe Experience Platform Web SDK permite una amplia variedad de casos de uso de personalización para propiedades web. Admite arquitecturas flexibles (del lado del cliente, del lado del servidor e híbridas) para que pueda solicitar decisiones y procesar contenido de formas que coincidan con las necesidades del sitio.

## Procesar contenido personalizado

Web SDK puede recuperar decisiones de personalización (también conocidas como _propositions_) y ayudarle a procesarlas en la página. La renderización es asíncrona, por lo que evite suponer un tiempo específico para cuando se aplique el contenido.

Elija el patrón que coincida con los elementos de la propuesta que recibe:

1. **Procesar automáticamente propuestas de acción DOM**: úselo cuando las propuestas incluyan `dom-action` elementos con selectores y tipos de acción que Web SDK puede aplicar automáticamente. Ver [Procesar automáticamente propuestas de acción DOM](render-auto-pers-content.md).
1. **Procesar ofertas de HTML sin selectores mediante applyPropositions**: úselo cuando reciba contenido de HTML, pero debe proporcionar dónde y cómo aplicarlo (selector + tipo de acción) mediante metadatos. Ver [Procesar ofertas de HTML sin selectores](render-html-offers.md).
1. **Procesar proposiciones manualmente**: úselo cuando necesite control total sobre la lógica de procesamiento (por ejemplo, componer la interfaz de usuario de JSON o aplicar reglas de negocio personalizadas). Ver [Procesar proposiciones manualmente](render-manual-propositions.md).

>[!TIP]
>
>Estos patrones se pueden combinar. Por ejemplo, puede habilitar la representación automática de acciones DOM al mismo tiempo que procesa manualmente el contenido de ámbitos de decisión específicos.

## Temas complementarios comunes

La mayoría de las implementaciones de personalización tratan estos temas comunes:

* **Impedir el parpadeo** (opcional): ocultar y mostrar contenedores durante la personalización. Ver [Administrar parpadeo](manage-flicker.md).
* **Rastrear lo que se mostró**: Registrar eventos de visualización para contenido procesado. Ver [Administrar eventos de visualización](display-events.md).
* **Métricas de búsqueda de la parte superior de la página/final de la página**: Solicite decisiones antes de tiempo y luego incluya la medición más tarde. Ver [Configurar eventos de página superiores e inferiores](top-bottom-page-events.md).

## Ejemplos de Web SDK

Además de las páginas de documento de esta carpeta, Adobe mantiene un repositorio de aplicaciones de ejemplo a las que puede hacer referencia. Consulte [Muestras de Web SDK](https://github.com/adobe/alloy-samples/) en GitHub para escenarios de personalización adicionales, entre ellos:

* Personalización del lado del cliente
* Personalización del lado del servidor
* Personalización híbrida
* Personalization en aplicaciones de una sola página
