---
title: sendEvent
description: Envíe datos al Edge Network de Adobe Experience Platform.
exl-id: 83de368d-78d4-4e28-aadd-afaea1ca091d
source-git-commit: 9ea7b678f5cfa19c7fd1e3ba6633cdeed4084b18
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---

# `sendEvent`

El `sendEvent` es la forma principal de enviar datos al Adobe para recuperar contenido personalizado, identidades y destinos de audiencia. Utilice el [`xdm`](xdm.md) para enviar datos que se asignen al esquema de Adobe Experience Platform. Utilice el [`data`](data.md) para enviar datos que no sean XDM. Puede utilizar el asignador de flujos de datos para alinear los datos de este objeto con los campos de esquema.

## Envío de datos de evento mediante la extensión de etiqueta del SDK web

El envío de datos de evento se realiza como una acción dentro de una regla de la interfaz de etiquetas de recopilación de datos de Adobe Experience Platform.

1. Iniciar sesión en [experience.adobe.com](https://experience.adobe.com) usando sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Reglas]**, luego seleccione la regla que desee.
1. En [!UICONTROL Acciones], seleccione una acción existente o cree una acción.
1. Configure las variables [!UICONTROL Extensión] campo desplegable a **[!UICONTROL SDK web de Adobe Experience Platform]** y configure el [!UICONTROL Tipo de acción] hasta **[!UICONTROL Enviar evento]**.
1. Defina los campos deseados y haga clic en **[!UICONTROL Conservar cambios]**, luego ejecute el flujo de trabajo de publicación.

## Envío de datos de evento mediante la biblioteca JavaScript del SDK web

Ejecute el `sendEvent` al llamar a la instancia configurada del SDK web. Asegúrese de llamar al [`configure`](../configure/overview.md) antes de llamar a `sendEvent` comando.

```js
alloy("sendEvent", {
  "data": dataObject,
  "documentUnloading": false,
  "edgeConfigOverrides": { "datastreamId": "0dada9f4-fa94-4c9c-8aaf-fdbac6c56287" },
  "renderDecisions": true,
  "type": "commerce.purchases",
  "xdm": adobeDataLayer.getState(reference)
});
```

## Objeto Response

Si decide hacerlo [gestionar respuestas](../command-responses.md) con este comando, están disponibles las siguientes propiedades en el objeto response:

* **`propositions`**: matriz de propuestas que devuelve el Edge Network. Las propuestas que se procesan automáticamente incluyen el indicador `renderAttempted` establezca en `true`.
* **`inferences`**: matriz de objetos de inferencia que contienen información de aprendizaje automático sobre este usuario.
* **`destinations`**: matriz de objetos de destino devueltos por el Edge Network.
