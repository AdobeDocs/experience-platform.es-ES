---
title: sendEvent
description: Envíe datos a Adobe Experience Platform Edge Network.
exl-id: 83de368d-78d4-4e28-aadd-afaea1ca091d
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 0%

---

# `sendEvent`

El comando `sendEvent` es la forma principal de enviar datos a Adobe. Su objeto de respuesta es la forma principal de recuperar contenido, identidades y destinos de audiencia personalizados. Utilice el objeto [`xdm`](xdm.md) para enviar datos que se asignen al esquema de Adobe Experience Platform. Utilice el objeto [`data`](data.md) para enviar datos que no sean XDM. La carga útil al enviar datos a Adobe tiene un límite máximo de 64 KB.

Ejecute el comando `sendEvent` al llamar a la instancia configurada de Web SDK. Asegúrese de llamar al comando [`configure`](../configure/overview.md) antes de llamar al comando `sendEvent`.

```js
alloy("sendEvent", {
  data: dataObject,
  documentUnloading: false,
  edgeConfigOverrides: { datastreamId: "0dada9f4-fa94-4c9c-8aaf-fdbac6c56287" },
  personalization: { decisionScopes: ["hero-banner"]},
  renderDecisions: true,
  type: "commerce.purchases",
  xdm: adobeDataLayer.getState(reference)
});
```

## Objeto Response

Si decide [controlar las respuestas](../command-responses.md) con este comando, las siguientes propiedades están disponibles en el objeto de respuesta:

* **`propositions`**: matriz de propuestas devuelta por Edge Network. Las propuestas que se procesan automáticamente incluyen el indicador `renderAttempted` establecido en `true`.
* **`inferences`**: matriz de objetos de inferencia que contiene información de aprendizaje automático sobre este usuario.
* **`destinations`**: una matriz de objetos de destino devueltos por Edge Network.

## Envío de eventos con la extensión de etiquetas Web SDK

La extensión de etiquetas Web SDK equivalente a este comando es la acción [**[!UICONTROL Send event]**](/help/tags/extensions/client/web-sdk/actions/send-event.md#data-fields).
