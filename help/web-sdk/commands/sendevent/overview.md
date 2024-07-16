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

El comando `sendEvent` es la forma principal de enviar datos al Adobe para recuperar contenido personalizado, identidades y destinos de audiencia. Utilice el objeto [`xdm`](xdm.md) para enviar datos que se asignen al esquema de Adobe Experience Platform. Utilice el objeto [`data`](data.md) para enviar datos que no sean XDM. Puede utilizar el asignador de flujos de datos para alinear los datos de este objeto con los campos de esquema.

## Envío de datos de evento mediante la extensión de etiqueta del SDK web

El envío de datos de evento se realiza como una acción dentro de una regla de la interfaz de etiquetas de recopilación de datos de Adobe Experience Platform.

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Reglas]** y luego seleccione la regla que desee.
1. En [!UICONTROL Acciones], seleccione una acción existente o cree una acción.
1. Establezca el campo desplegable [!UICONTROL Extension] en **[!UICONTROL SDK web de Adobe Experience Platform]** y establezca [!UICONTROL Action Type] en **[!UICONTROL Send event]**.
1. Defina los campos que desee, haga clic en **[!UICONTROL Conservar cambios]** y ejecute el flujo de trabajo de publicación.

## Enviar datos de evento mediante la biblioteca de JavaScript del SDK web

Ejecute el comando `sendEvent` al llamar a la instancia configurada del SDK web. Asegúrese de llamar al comando [`configure`](../configure/overview.md) antes de llamar al comando `sendEvent`.

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

Si decide [controlar las respuestas](../command-responses.md) con este comando, las siguientes propiedades están disponibles en el objeto de respuesta:

* **`propositions`**: matriz de propuestas devuelta por el Edge Network. Las propuestas que se procesan automáticamente incluyen el indicador `renderAttempted` establecido en `true`.
* **`inferences`**: matriz de objetos de inferencia que contiene información de aprendizaje automático sobre este usuario.
* **`destinations`**: una matriz de objetos de destino devueltos por el Edge Network.
