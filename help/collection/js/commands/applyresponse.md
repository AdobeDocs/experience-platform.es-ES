---
title: applyResponse
description: Utilice una respuesta de Edge Network para inicializar Web SDK.
exl-id: 0653b8f7-33f0-43a1-97f5-59a51270f660
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---

# `applyResponse`

El comando `applyResponse` le permite realizar diversas acciones en función de una respuesta de Edge Network. Normalmente se utiliza en implementaciones híbridas en las que el servidor realiza una llamada inicial a Edge Network. Este comando toma la respuesta de esa llamada e inicializa Web SDK en el explorador.

Ejecute el comando `applyResponse` al llamar a la instancia configurada de Web SDK. El objeto que contiene las opciones de configuración admite los siguientes campos:

* **`renderDecisions`**: un booleano que fuerza a Web SDK a procesar cualquier contenido personalizado que sea apto para el procesamiento automático. Idéntico a [`renderDecisions`](sendevent/renderdecisions.md) en el comando [`sendEvent`](sendevent/overview.md).
* **`responseHeaders`**: asignación de nombres de encabezado de cadena a valores de encabezado de cadena.
* **`responseBody`**: obligatorio. Un cuerpo de respuesta JSON desde la llamada al servidor a Edge Network.
* **`personalization.sendDisplayEvent`**: un booleano que funciona de manera idéntica a [`personalization.sendDisplayEvent`](sendevent/personalization.md) en el comando `sendEvent`.

```js
alloy("applyResponse",{
  "renderDecisions": true,
  "responseHeaders": {},
  "responseBody": {},
  "personalization": {
    "sendDisplayEvent": true
  }
});
```

## Objeto Response

Si decide [controlar las respuestas](command-responses.md) con este comando, las siguientes propiedades están disponibles en el objeto de respuesta:

* **`propositions`**: matriz de propuestas devuelta por Edge Network. Las propuestas que se procesan automáticamente incluyen el indicador `renderAttempted` establecido en `true`.
* **`inferences`**: matriz de objetos de inferencia que contiene información de aprendizaje automático sobre este usuario.
* **`destinations`**: una matriz de objetos de destino devueltos por Edge Network.

## Aplicar respuesta mediante la extensión de etiquetas Web SDK

La extensión de etiquetas Web SDK equivalente a este comando es la acción [**[!UICONTROL Apply response]**](/help/tags/extensions/client/web-sdk/actions/apply-response.md).
