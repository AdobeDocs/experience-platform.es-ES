---
title: Administrar eventos de visualización en Web SDK
description: Explica qué son los eventos de visualización y cómo se pueden utilizar en Web SDK.
exl-id: 7150ad6e-7693-4f4d-917e-8d08a39a0b41
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# Administrar eventos de visualización en Web SDK

Web SDK utiliza los eventos de visualización para informar al servicio de personalización o análisis cuando se muestra un contenido de personalización específico en una página. El envío de eventos de visualización mejora la precisión de las métricas de personalización y le ofrece una visión general precisa de lo que los usuarios ven en la página.

>[!NOTE]
>
>Los eventos de visualización no se envían automáticamente al llamar a la función `applyPropositions`.

## Enviar eventos de visualización automáticamente

El envío de eventos de visualización proporciona automáticamente métricas de análisis más precisas, ya que el evento se envía inmediatamente después de que se cargue la personalización. Esta implementación también tiene un método de implementación más simplificado.

Para enviar eventos de visualización automáticamente después de que se procese el contenido personalizado en la página, debe configurar los siguientes parámetros:

* `renderDecisions: true`
* `personalization.sendDisplayEvent: true` o no especificado

Web SDK envía los eventos de visualización inmediatamente después de que se procese cualquier personalización como resultado de una llamada a `sendEvent`.

## Envío de eventos de visualización en llamadas subsiguientes a sendEvent

En comparación con el envío automático de eventos de visualización, cuando los incluye en las llamadas a `sendEvent` subsiguientes, también tiene la oportunidad de incluir más información sobre la carga de página en la llamada. Puede tratarse de información adicional, que no estaba disponible al solicitar el contenido personalizado.

Además, el envío de eventos de visualización en llamadas de `sendEvent` minimiza los errores de tasa de devolución al utilizar Adobe Analytics.

>[!IMPORTANT]
>
>Cuando se utilizan propuestas procesadas manualmente, los eventos de visualización solo se admiten a través de llamadas a `sendEvent`. En este caso, no se pueden enviar eventos de visualización automáticamente.

### Enviar eventos de visualización para propuestas procesadas automáticamente

Para enviar eventos de visualización para propuestas procesadas automáticamente, debe configurar los siguientes parámetros en la llamada `sendEvent`:

* `renderDecisions: true`
* `personalization.sendDisplayEvent: false` para la parte superior de la visita de página

Para enviar los eventos de visualización, llame a `sendEvent` con `personalization.includeRenderedPropositions: true`

### Envío de eventos de visualización para propuestas procesadas manualmente

Para enviar eventos de visualización para propuestas procesadas manualmente, debe incluirlas en el campo XDM `_experience.decisioning.propositions`, incluidos los campos `id`, `scope` y `scopeDetails` de las propuestas.

Además, establezca el campo `include _experience.decisioning.propositionEventType.display` en `1`.
