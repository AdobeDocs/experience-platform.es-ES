---
title: Gestión de respuestas de comandos
description: Administre las respuestas de los comandos utilizando promesas de JavaScript.
exl-id: dda98b3e-3e37-48ac-afd7-d8852b785b83
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---

# Gestión de respuestas de comandos

Algunos comandos del SDK web pueden devolver un objeto que contenga datos potencialmente útiles para su organización. Si lo desea, puede elegir qué hacer con esos datos. Las respuestas de comandos son valiosas para las propuestas y los destinos, ya que requieren datos Edge Network para funcionar de forma eficaz.

Las respuestas de comandos utilizan JavaScript [promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise), que actúa como un proxy para un valor que no se conoce cuando se crea la promesa. Una vez conocido el valor, la promesa se &quot;resuelve&quot; con el valor.

## Administrar respuestas de comandos mediante la extensión de etiqueta del SDK web

Cree una regla que se suscriba al evento **[!UICONTROL Enviar evento completado]** como parte de una regla.

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Reglas]** y luego seleccione la regla que desee.
1. En [!UICONTROL Eventos], seleccione un evento existente o cree un evento.
1. Establezca el campo desplegable [!UICONTROL Extensión] en **[!UICONTROL SDK web de Adobe Experience Platform]** y establezca el [!UICONTROL Tipo de evento] en **[!UICONTROL Enviar evento completado]**.
1. Haga clic en **[!UICONTROL Conservar cambios]** y, a continuación, ejecute el flujo de trabajo de publicación.

A continuación, puede incluir las acciones **[!UICONTROL Aplicar propuestas]** o **[!UICONTROL Aplicar respuesta]** a esta regla.

1. Al ver la regla creada o editada anteriormente, seleccione una acción existente o cree una acción.
1. Establezca el campo desplegable [!UICONTROL Extension] en **[!UICONTROL Adobe Experience Platform Web SDK]** y establezca [!UICONTROL Action Type] en **[!UICONTROL Apply propositions]** o **[!UICONTROL Apply response]**, según el comportamiento deseado.
1. Defina los campos deseados de la acción y luego haga clic en **[!UICONTROL Conservar cambios]**.

## Administrar respuestas de comandos mediante la biblioteca JavaScript del SDK web

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
