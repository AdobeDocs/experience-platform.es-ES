---
title: applyResponse
description: Utilice una respuesta del Edge Network para inicializar el SDK web.
exl-id: 0653b8f7-33f0-43a1-97f5-59a51270f660
source-git-commit: 74725546163f0807d3188aff5b5ffda9b8d6350b
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# `applyResponse`

El `applyResponse` El comando permite realizar varias acciones en función de la respuesta del Edge Network. Normalmente se utiliza en implementaciones híbridas en las que el servidor realiza una llamada inicial al Edge Network. Este comando toma la respuesta de esa llamada e inicializa el SDK web en el explorador.

## Aplicar respuesta mediante la extensión de etiqueta del SDK web

La aplicación de respuestas se realiza como una acción dentro de una regla de la interfaz de etiquetas de recopilación de datos de Adobe Experience Platform.

1. Iniciar sesión en [experience.adobe.com](https://experience.adobe.com) usando sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Reglas]**, luego seleccione la regla que desee.
1. En [!UICONTROL Acciones], seleccione una acción existente o cree una acción.
1. Configure las variables [!UICONTROL Extensión] campo desplegable a **[!UICONTROL SDK web de Adobe Experience Platform]** y configure el [!UICONTROL Tipo de acción] hasta **[!UICONTROL Aplicar respuesta]**.
1. Defina los campos deseados a la derecha.
1. Clic **[!UICONTROL Conservar cambios]**, luego ejecute el flujo de trabajo de publicación.

## Aplicar respuesta mediante la biblioteca JavaScript del SDK web

Ejecute el `applyResponse` al llamar a la instancia configurada del SDK web. El objeto que contiene las opciones de configuración admite los siguientes campos:

* **`renderDecisions`**: Un booleano que fuerza al SDK web a procesar cualquier contenido personalizado que sea apto para el procesamiento automático. Idéntico a [`renderDecisions`](sendevent/renderdecisions.md) en el [`sendEvent`](sendevent/overview.md) comando.
* **`responseHeaders`**: mapa de nombres de encabezados de cadena a valores de encabezados de cadena.
* **`responseBody`**: obligatorio. Un cuerpo de respuesta JSON desde la llamada al servidor al Edge Network.
* **`personalization.sendDisplayEvent`**: Un booleano que funciona de forma idéntica a [`personalization.sendDisplayEvent`](sendevent/personalization.md) en el `sendEvent` comando.

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

Si decide hacerlo [gestionar respuestas](command-responses.md) con este comando, están disponibles las siguientes propiedades en el objeto response:

* **`propositions`**: matriz de propuestas que devuelve el Edge Network. Las propuestas que se procesan automáticamente incluyen el indicador `renderAttempted` establezca en `true`.
* **`inferences`**: matriz de objetos de inferencia que contienen información de aprendizaje automático sobre este usuario.
* **`destinations`**: matriz de objetos de destino devueltos por el Edge Network.
