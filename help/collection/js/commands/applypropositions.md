---
title: applyPropositions
description: Volver a procesar propuestas que ya se hayan procesado con sendEvent.
exl-id: 6b79f334-4ea6-4ba4-8640-d35b7f90df98
source-git-commit: e150fa51953edbb0e21de962e066deedaf8bd2d7
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---

# `applyPropositions`

El comando `applyPropositions` le permite volver a procesar propuestas que ya se representaron con el comando [`sendEvent`](sendevent/overview.md). Este comando resulta útil cuando se trabaja con aplicaciones de una sola página en las que se vuelven a procesar partes de la página, sobrescribiendo potencialmente las personalizaciones ya aplicadas a la página.

Este comando admite los campos siguientes:

* **Propositions**: matriz de objetos de propuesta que desea volver a procesar.
* **Nombre de vista**: Nombre de la vista que se va a procesar. Las notificaciones de visualización para estas decisiones se almacenan en caché y se pueden incluir en un comando `sendEvent` posterior usando la opción `personalization.includeRenderedPropositions`.
* **Datos de Meta**: Un objeto que determina cómo se pueden aplicar las ofertas de HTML. Contiene las siguientes propiedades:
   * Ámbito
   * Selector
   * Tipo de acción

>[!NOTE]
>
>El comando `applyPropositions` no envía automáticamente eventos de visualización. Si desea grabar las pantallas, utilice el comando `sendEvent` tal como se describe en [Administrar eventos de visualización](/help/collection/use-cases/personalization/display-events.md).

Ejecute el comando `applyPropositions` al llamar a la instancia configurada de Web SDK. El objeto que contiene las opciones de configuración admite los siguientes campos:

* **`propositions`**: matriz de objetos de propuesta que desea volver a procesar. Este objeto no suele utilizarse, ya que el campo `propositionScopes` suele determinar qué ámbitos o superficies desea volver a procesar.
* **`metadata`**: Determina cómo se aplican las ofertas de HTML. Es un mapa donde la clave es un ámbito o una superficie y el valor es un objeto que contiene las claves `selector` y `actionType`.
   * `selector`: cadena que contiene un selector CSS de dónde aplicar HTML.
   * `actionType`: la acción que se realizará con HTML. Los valores válidos incluyen `setHtml`, `replaceHtml` y `appendHtml`.
* **`viewName`**: nombre de la vista que se va a procesar en una aplicación de una sola página. Las notificaciones de visualización para estas decisiones se almacenan en caché y se pueden incluir en un comando `sendEvent` posterior con `personalization.includeRenderedPropositions`.

```js
alloy("applyPropositions",{
  "propositions": [],
  "metadata": {},
  "viewName": ""
});
```

## Aplicación de propuestas mediante la extensión de etiquetas Web SDK

La extensión de etiquetas Web SDK equivalente a este comando es la acción [**[!UICONTROL Apply propositions]**](/help/tags/extensions/client/web-sdk/actions/apply-propositions.md).
