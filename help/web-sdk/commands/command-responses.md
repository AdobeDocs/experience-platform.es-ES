---
title: Gestión de respuestas de comandos
description: Gestionar las respuestas de los comandos utilizando promesas de JavaScript.
exl-id: dda98b3e-3e37-48ac-afd7-d8852b785b83
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---

# Gestión de respuestas de comandos

Algunos comandos del SDK web pueden devolver un objeto que contenga datos potencialmente útiles para su organización. Si lo desea, puede elegir qué hacer con esos datos. Las respuestas de comando son valiosas para propuestas y destinos, ya que requieren datos de red perimetral para funcionar de forma eficaz.

Las respuestas de comando utilizan JavaScript [promesas](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise), actuando como proxy para un valor que no se conoce cuando se crea la promesa. Una vez conocido el valor, la promesa se &quot;resuelve&quot; con el valor.

## Administrar respuestas de comandos mediante la extensión de etiqueta del SDK web

Cree una regla que se suscriba a **[!UICONTROL Enviar evento completado]** como parte de una regla.

1. Iniciar sesión en [experience.adobe.com](https://experience.adobe.com) usando sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Reglas]**, luego seleccione la regla que desee.
1. En [!UICONTROL Eventos], seleccione un evento existente o cree un evento.
1. Configure las variables [!UICONTROL Extensión] campo desplegable a **[!UICONTROL SDK web de Adobe Experience Platform]** y configure el [!UICONTROL Tipo de evento] hasta **[!UICONTROL Enviar evento completado]**.
1. Clic **[!UICONTROL Conservar cambios]**, luego ejecute el flujo de trabajo de publicación.

Luego puede incluir las acciones **[!UICONTROL Aplicar propuestas]** o **[!UICONTROL Aplicar respuesta]** a esta regla.

1. Al ver la regla creada o editada anteriormente, seleccione una acción existente o cree una acción.
1. Configure las variables [!UICONTROL Extensión] campo desplegable a **[!UICONTROL SDK web de Adobe Experience Platform]** y configure el [!UICONTROL Tipo de acción] hasta **[!UICONTROL Aplicar propuestas]** o **[!UICONTROL Aplicar respuesta]**, según el comportamiento deseado.
1. Defina los campos deseados de la acción y haga clic en **[!UICONTROL Conservar cambios]**.

## Administrar respuestas de comandos mediante la biblioteca JavaScript del SDK web

Utilice el `then` y `catch` métodos para determinar cuándo un comando tiene éxito o falla. Puede omitir cualquiera de las siguientes opciones `then` o `catch` si sus fines no son importantes para la implementación.

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

Todas las promesas devueltas por los comandos utilizan un `result` objeto. Por ejemplo, puede obtener información de biblioteca del `result` objeto que utiliza el [`getLibraryInfo`](getlibraryinfo.md) comando:

```js
alloy("getLibraryInfo")
  .then(function(result) {
    console.log(result.libraryInfo.version);
    console.log(result.libraryInfo.commands);
    console.log(result.libraryInfo.configs);
  });
```

El contenido de esta `result` depende de una combinación del comando que utilice y del consentimiento del usuario. Si un usuario no ha dado su consentimiento para un fin determinado, el objeto de respuesta solo contiene información que se puede proporcionar en el contexto de lo que el usuario ha consentido.
