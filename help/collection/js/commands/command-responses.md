---
title: Gestión de respuestas de comandos
description: Administre las respuestas de los comandos utilizando promesas de JavaScript.
exl-id: dda98b3e-3e37-48ac-afd7-d8852b785b83
source-git-commit: 8abdd206f5fcff0e1cec7bb6ecd25c5eb9354286
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---

# Gestión de respuestas de comandos

Algunos comandos de Web SDK pueden devolver un objeto que contenga datos potencialmente útiles para su organización. Si lo desea, puede elegir qué hacer con esos datos. Las respuestas de comandos son valiosas para propuestas y destinos, ya que requieren datos de Edge Network para funcionar de forma eficaz.

Las respuestas de comandos utilizan JavaScript [promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise), que actúa como un proxy para un valor que no se conoce cuando se crea la promesa. Una vez conocido el valor, la promesa se &quot;resuelve&quot; con el valor.

Utilice los métodos `then` y `catch` para determinar si un comando tiene éxito o falla. Puede omitir `then` o `catch` si sus propósitos no son importantes para la implementación.

```javascript
alloy("sendEvent", {
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
}).then(function(result) {
    console.log("The sendEvent command succeeded.");
  })
  .catch(function(error) {
    console.log("The sendEvent command failed.");
  });
```

Todas las promesas devueltas por los comandos utilizan un objeto `result`. Por ejemplo, puede obtener información de biblioteca del objeto `result` mediante el comando [`getLibraryInfo`](getlibraryinfo.md):

```js
alloy("getLibraryInfo")
  .then(function(result) {
    console.log(result.libraryInfo.version);
    console.log(result.libraryInfo.commands);
    console.log(result.libraryInfo.configs);
  });
```

El contenido de este objeto `result` depende de una combinación del comando que utilice y del consentimiento del usuario. Si un usuario no ha dado su consentimiento para un fin determinado, el objeto de respuesta solo contiene información que se puede proporcionar en el contexto de lo que el usuario ha consentido.

## Respuestas de comandos mediante la extensión de etiquetas Web SDK

La extensión de etiquetas Web SDK equivalente a respuestas de comandos es una regla que se suscribe al evento [**[!UICONTROL Send event complete]**](/help/tags/extensions/client/web-sdk/event-types.md#send-event-complete). A continuación, puede incluir acciones como [**[!UICONTROL Apply propositions]**](/help/tags/extensions/client/web-sdk/actions/apply-propositions.md) o [**[!UICONTROL Apply response]**](/help/tags/extensions/client/web-sdk/actions/apply-response.md) en esta regla.
