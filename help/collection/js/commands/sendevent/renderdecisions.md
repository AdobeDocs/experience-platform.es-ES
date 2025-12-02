---
title: renderDecisions
description: Procesar contenido personalizado que pueda procesarse automáticamente.
exl-id: 6f7a3531-c2b6-4e90-a7ad-9f0fe4dc39e9
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# `renderDecisions`

La propiedad `renderDecisions` le permite forzar a Web SDK a procesar cualquier contenido personalizado que sea apto para el procesamiento automático.

Establezca el booleano `renderDecisions` al ejecutar el comando `sendEvent`. Si se omite, el valor predeterminado de esta propiedad es `false`. Establezca esta propiedad en `true` si desea procesar automáticamente el contenido personalizado.

>[!IMPORTANT]
>
>La propiedad `renderDecisions` no es compatible con la propiedad [`documentUnloading`](documentunloading.md). Evite establecer ambas propiedades en `true` simultáneamente.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "renderDecisions": true
});
```

Asegúrese de que, al establecer esta propiedad en `true`, también incluya ámbitos o superficies asociados. Estos ámbitos o superficies se pueden solicitar automáticamente (como en el primer comando `sendEvent` de una página) o explícitamente (mediante [`personalization.decisionScopes`](personalization.md#personalizationdecisionscopes) o [`personalization.surfaces`](personalization.md#personalizationsurfaces)). Un problema común al procesar la personalización es el siguiente escenario:

1. Un comando `sendEvent` se ejecuta al principio de la página que solicita la personalización predeterminada con `renderDecisions` sin establecer (el valor predeterminado es `false`). Las propuestas se recuperan, pero no se procesan.
1. Más adelante en la página, otro(a) `sendEvent` déclencheur(a) con `renderDecisions` establecido(a) en `true`, pero no incluye ámbitos o superficies. Dado que no hay ámbitos ni superficies en esta segunda llamada, no se procesa nada.

Puede evitar este problema haciendo lo siguiente:

* Estableciendo `renderDecisions` en `true` en la primera llamada de `sendEvent`; o
* Estableciendo explícitamente `decisionScopes` o `surfaces` en una llamada posterior de `sendEvent` al establecer `renderDecisions` en `true`.

## Procesar decisiones mediante la extensión de etiquetas Web SDK

El equivalente de la extensión de etiquetas Web SDK de esta propiedad es la casilla de verificación [**Procesar decisiones de personalización visuales**](/help/tags/extensions/client/web-sdk/actions/send-event.md#personalization-fields) dentro de la acción &#39;[!UICONTROL Send event]&#39;.
