---
title: Administrar eventos de visualización en el SDK web
description: Este artículo explica qué son los eventos de visualización y cómo puede utilizarlos en el SDK web.
exl-id: 7150ad6e-7693-4f4d-917e-8d08a39a0b41
source-git-commit: c2e308b5e743f07062be9a34e23c4bc700b27463
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---

# Administrar eventos de visualización en el SDK web

El SDK web utiliza eventos de visualización para informar al servicio de personalización o análisis cuando se muestra un contenido de personalización específico en una página.

El envío de eventos de visualización mejora la precisión de las métricas de personalización y le ofrece una visión general precisa de lo que los usuarios ven en la página.

El SDK web permite enviar eventos de visualización de dos formas:

* [Automáticamente](#send-automatically), inmediatamente después de que se procese el contenido personalizado en la página. Consulte la documentación sobre cómo [representación de contenido personalizado](rendering-personalization-content.md) para obtener más información.
* [Manualmente](#send-sendEvent-calls), a través de subsiguientes `sendEvent` llamadas.

>[!NOTE]
>
>Los eventos de visualización no se envían automáticamente al llamar a `applyPropositions` función.

## Enviar eventos de visualización automáticamente {#send-automatically}

El envío de eventos de visualización proporciona automáticamente métricas de análisis más precisas, ya que el evento se envía inmediatamente después de que se cargue la personalización. Esta implementación también tiene un método de implementación más simplificado.

Para enviar eventos de visualización automáticamente después de que se procese el contenido personalizado en la página, debe configurar los siguientes parámetros:

* `renderDecisions: true`
* `personalization.sendDisplayNotifications: true` o no especificado

El SDK web envía los eventos de visualización inmediatamente después de que se procese cualquier personalización como resultado de una `sendEvent` llamada.

## Envío de eventos de visualización en llamadas subsiguientes a sendEvent {#send-sendEvent-calls}

Comparado con [automáticamente](#send-automatically) envío de eventos de visualización, cuando se incluyen en las siguientes `sendEvent` llamadas de también tiene la oportunidad de incluir más información sobre la carga de página en la llamada de. Puede tratarse de información adicional, que no estaba disponible al solicitar el contenido personalizado.

Además, el envío de eventos de visualización en `sendEvent` Las llamadas de minimizan los errores de tasa de devolución al utilizar Adobe Analytics.

>[!IMPORTANT]
>
>Cuando se utilizan propuestas procesadas manualmente, los eventos de visualización solo se admiten mediante `sendEvent` llamadas. En este caso, no se pueden enviar eventos de visualización automáticamente.

### Enviar eventos de visualización para propuestas procesadas automáticamente {#auto-rendered-propositions}

Para enviar eventos de visualización para propuestas procesadas automáticamente, debe configurar los siguientes parámetros en la variable `sendEvent` llamada:

* `renderDecisions: true`
* `personalization.sendDisplayNotifications: false` para la parte superior de la visita individual a la página

Para enviar los eventos de visualización, llame a `sendEvent` con `personalization.includePendingDisplayNotifications: true`

### Envío de eventos de visualización para propuestas procesadas manualmente {#manually-rendered-propositions}

Para enviar eventos de visualización para propuestas procesadas manualmente, debe incluirlos en la `_experience.decisioning.propositions` Campo XDM, incluido el `id`, `scope`, y `scopeDetails` campos de las propuestas.

Además, configure el `include _experience.decisioning.propositionEventType.display` field a `1`.
