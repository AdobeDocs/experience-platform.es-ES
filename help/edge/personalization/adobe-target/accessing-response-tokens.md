---
title: Acceso a tokens de respuesta mediante el SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo acceder a los tokens de respuesta con el SDK web de Adobe Experience Platform.
keywords: personalización;target;adobe target;renderdecisions;sendEvent;decisionScopes;result.decisions,tokens de respuesta;
source-git-commit: 4bddd9f23ae885468148d1592af219290d6fafd9
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---


# Acceso a tokens de respuesta

El contenido de personalización que Adobe Target devuelve incluye [tokens de respuesta](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html), que son detalles sobre la actividad, la oferta, la experiencia, el perfil de usuario, la información geográfica y mucho más. Estos detalles se pueden compartir con herramientas de terceros o utilizar para la depuración. Los tokens de respuesta se pueden configurar en la interfaz de usuario de Adobe Target.

Para acceder a cualquier contenido de personalización, proporcione una función de llamada de retorno al enviar un evento. Se llamará a esta rellamada después de que el SDK reciba una respuesta correcta del servidor. Se proporcionará a la rellamada un objeto `result` , que puede contener una propiedad `propositions` que contenga cualquier contenido de personalización devuelto. A continuación se muestra un ejemplo de cómo proporcionar una función de llamada de retorno.

```javascript
alloy("sendEvent", {
    renderDecisions: true,
    xdm: {}
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions
    }
  });
```

En este ejemplo, `result.propositions`, si existe, es una matriz que contiene propuestas de personalización relacionadas con el evento. Consulte [Rendering personalization content](../rendering-personalization-content.md) para obtener más información sobre el contenido de `result.propositions`.

Supongamos que desea recopilar todos los nombres de actividad de todas las propuestas que el SDK web ha procesado automáticamente y colocarlos en una única matriz. Luego puede enviar la matriz única a un tercero. En este caso:

1. Extraiga propuestas del objeto `result`.
1. Bucle por cada propuesta.
1. Determine si el SDK procesó la propuesta.
1. Si es así, realice un bucle por cada elemento de la propuesta.
1. Recupere el nombre de la actividad desde la propiedad `meta` , que es un objeto que contiene tokens de respuesta.
1. Inserte el nombre de la actividad en una matriz.
1. Envíe los nombres de la actividad a un tercero.

El código tendría el siguiente aspecto:

```javascript
alloy("sendEvent", {
    renderDecisions: true,
    xdm: {}
  }).then(function(result) {
    var activityNames = [];
    propositions.forEach(function(proposition) {
      if (proposition.renderAttempted) {
        proposition.items.forEach(function(item) {
          if (item.meta) {
            // item.meta contains the response tokens.
            var activityName = item.meta["activity.name"];
            // Ignore duplicates
            if (activityNames.indexOf(activityName) === -1) {
              activityNames.push(activityName);
            }
          }
        });
      }
    });
    // Now that activity names are in an array,
    // you can send them to a third party or use
    // them in some other way.
  });
```


