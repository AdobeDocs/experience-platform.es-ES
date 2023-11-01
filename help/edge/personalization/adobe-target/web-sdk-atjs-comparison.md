---
title: Comparación de at.js con el SDK web de Experience Platform
description: Descubra cómo se comparan las funciones de at.js con el SDK web de Experience Platform
keywords: target;adobe target;activity.id;experience.id;renderDecisions;decisionScopes;preocultando fragmento;vec;Compositor de experiencias basadas en formularios;xdm;audiencias;decisiones;ámbito;esquema;diagrama del sistema;diagrama
exl-id: b63fe47d-856a-4cae-9057-51917b3e58dd
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '2257'
ht-degree: 6%

---

# Comparación de la biblioteca at.js con el SDK web

## Información general

Este artículo ofrece una descripción general de las diferencias entre las variables `at.js` y el SDK web de Experience Platform.

## Instalación de las bibliotecas

### Instalación de at.js

Permitimos a nuestros clientes descargar la biblioteca directamente desde Adobe Experience Cloud, pestaña Implementación. La biblioteca at.js se personaliza con opciones que el cliente tiene como: clientCode, imsOrgId, etc.

### Instalación del SDK web

La versión prediseñada está disponible en una CDN. Puede hacer referencia a la biblioteca en la CDN directamente en la página o descargarla y alojarla en su propia infraestructura. Está disponible en formatos minificado y no minificado. La versión no minificada es útil para la depuración.

Estructura de la URL: https://cdn1.adoberesources.net/alloy/[VERSIÓN]/alloy.min.js o alloy.js para la versión no minificada.

Por ejemplo:

* Minificado: [https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js](https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js)
* No minificado: [https://cdn1.adoberesources.net/alloy/2.14.0/alloy.js](https://cdn1.adoberesources.net/alloy/2.14.0/alloy.js)

[Más información](../../fundamentals/installing-the-sdk.md)

## Configuración de las bibliotecas

### Configuración de at.js

Al final de cada archivo at.js encontrará una sección en la que creamos una instancia y pasamos un objeto de configuración. Es personalizable, en la descarga rellenamos esa sección con la configuración actual del cliente.

```javascript
window.adobe.target.init(window, document, {
  "clientCode": "demo",
  "imsOrgId": "",
  "serverDomain": "localhost:5000",
  "timeout": 2000,
  "globalMboxName": "target-global-mbox",
  "version": "2.0.0",
  "defaultContentHiddenStyle": "visibility: hidden;",
  "defaultContentVisibleStyle": "visibility: visible;",
  "bodyHiddenStyle": "body {opacity: 0 !important}",
  "bodyHidingEnabled": true,
  "deviceIdLifetime": 63244800000,
  "sessionIdLifetime": 1860000,
  "selectorsPollingTimeout": 5000,
  "visitorApiTimeout": 2000,
  "overrideMboxEdgeServer": false,
  "overrideMboxEdgeServerTimeout": 1860000,
  "optoutEnabled": false,
  "optinEnabled": false,
  "secureOnly": false,
  "supplementalDataIdParamTimeout": 30,
  "authoringScriptUrl": "//cdn.tt.omtrdc.net/cdn/target-vec.js",
  "urlSizeLimit": 2048,
  "endpoint": "/rest/v1/delivery",
  "pageLoadEnabled": true,
  "viewsEnabled": true,
  "analyticsLogging": "server_side",
  "serverState": {},
  "decisioningMethod": "server-side",
  "legacyBrowserSupport":  false
});
```

[Más información](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetgobalsettings.html)


### Configuración del SDK web

La configuración del SDK se realiza con `configure` comando.

>[!IMPORTANT]
>
>`configure` es *siempre* el primer comando llamado.

Por ejemplo:

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

Hay muchas opciones que se pueden configurar durante la configuración. Todas las opciones se encuentran a continuación, agrupadas por categoría.

[Más información](../../fundamentals/configuring-the-sdk.md)


## Cómo solicitar y procesar automáticamente ofertas de Page Load Target

### Uso de at.js

Con at.js 2.x, si activa la configuración `pageLoadEnabled`, la biblioteca almacenará en déclencheur una llamada a Target Edge con `execute -> pageLoad`. Si todos los ajustes se establecen en los valores predeterminados, no es necesaria ninguna codificación personalizada. Una vez que at.js se añade a la página y el explorador lo carga, se ejecuta una llamada de Target Edge.

### Uso del SDK web

Contenido creado en el de Adobe Target [Compositor de experiencias visuales](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) El SDK puede recuperarlo y procesarlo automáticamente.

Para solicitar y procesar automáticamente ofertas de Target, utilice el `sendEvent` y establezca el `renderDecisions` opción para `true`. Esto obliga al SDK a procesar automáticamente cualquier contenido personalizado que sea apto para el procesamiento automático.

Por ejemplo:

```javascript
alloy("sendEvent", {
  "renderDecisions": true,
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
});
```

El SDK web de Experience Platform envía automáticamente una notificación con las ofertas ejecutadas por el SDK web. Este es un ejemplo del aspecto de una carga útil de solicitud de notificación:

```json
{
  "events": [{
      "xdm": {
        "_experience": {
          "decisioning": {
            "propositions": [
              {
                "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
                "scope": "cart",
                "scopeDetails": {
                  "decisionProvider": "TGT",
                  "activity": {
                    "id": "127019"
                  },
                  "experience": {
                    "id": "0"
                  },
                  "strategies": [
                    {
                      "step": "entry",
                      "algorithmID": "0",
                      "trafficType": "0"
                    },
                    {
                      "step": "display",
                      "algorithmID": "0",
                      "trafficType": "0"
                    }
                  ],
                  "characteristics": {
                    "eventToken": "bKMxJ8dCR1XlPfDCx+2vSGqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="
                  }
                }
              }
            ]
          }
        },
        "eventType": "display",
        "web": {
          "webPageDetails": {
            "viewName": "cart",
            "URL": "https://alloyio.com/personalizationSpa/cart"
          },
          "webReferrer": {
            "URL": ""
          }
        },
        "device": {
          "screenHeight": 800,
          "screenWidth": 1280,
          "screenOrientation": "landscape"
        },
        "environment": {
          "type": "browser",
          "browserDetails": {
            "viewportWidth": 1280,
            "viewportHeight": 284
          }
        },
        "placeContext": {
          "localTime": "2021-12-10T15:50:34.467+02:00",
          "localTimezoneOffset": -120
        },
        "timestamp": "2021-12-10T13:50:34.467Z",
        "implementationDetails": {
          "name": "https://ns.adobe.com/experience/alloy",
          "version": "2.6.2",
          "environment": "browser"
        }
      }
    }
  ]
}
```

[Más información](../rendering-personalization-content.md)

## Cómo solicitar y NO procesar automáticamente ofertas de Page Load Target

### Uso de at.js

Hay dos maneras de activar una llamada a Target Edge que recuperará ofertas para la carga de página.

Ejemplo 1:

```javascript
adobe.target.getOffer({
   mbox: "target-global-mbox", 
   success: console.log,
   error: console.error
});
```

Ejemplo 2:

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        pageLoad: {}
    }
  }
})
.then(console.log)
.catch(console.error);
```

[Más información](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/cmp-atjs-functions.html)

### Uso del SDK web

Ejecutar un `sendEvent` comando con un ámbito especial en `decisionScopes`: `__view__`. Utilizamos este ámbito como señal para recuperar todas las actividades de carga de página de Target y recuperar previamente todas las vistas. El SDK web también intentará evaluar todas las actividades basadas en vistas del VEC. Actualmente, el SDK web no admite la desactivación de la recuperación previa de vistas.

Para acceder a cualquier contenido de personalización, puede proporcionar una función de llamada de retorno a la que se llamará después de que el SDK reciba una respuesta correcta del servidor. La llamada de retorno se proporciona como un objeto result, que puede contener la propiedad propositions que contiene cualquier contenido de personalización devuelto.

Por ejemplo:

```javascript
alloy("sendEvent", {
    xdm: {...},
    decisionScopes: ["__view__"]
  }).then(function(result) {
    if (result.propositions) {
      result.propositions.forEach(proposition => {
        proposition.items.forEach(item => {
          if (item.schema === HTML_SCHEMA) {
            // manually apply offer
            document.getElementById("form-based-offer-container").innerHTML =
              item.data.content;
            const executedPropositions = [
              {
                id: proposition.id,
                scope: proposition.scope,
                scopeDetails: proposition.scopeDetails
              }
            ];
          // manually send the display notification event, so that Target/Analytics impressions aare increased
            alloy("sendEvent",{
              "xdm": {
                "eventType": "decisioning.propositionDisplay",
                "_experience": {
                  "decisioning": {
                    "propositions": executedPropositions
                  }
                }
              }
            });
          }
        });
      });
    }
  });
```

[Más información](../rendering-personalization-content.md#manually-rendering-content)


## Cómo solicitar mboxes específicos de Form Based Target


### Uso de at.js

Puede recuperar actividades del Compositor basado en formularios utilizando `getOffer` función:

Ejemplo 1:

```javascript
adobe.target.getOffer({
   mbox: "hero-banner", 
   success: console.log,
   error: console.error
});
```

Ejemplo 2:

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        mboxes: [
        {
          index: 0,
          name: "hero-banner"
        }]
    }
  }
})
.then(console.log)
.catch(console.error);
```

[Más información](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/cmp-atjs-functions.html)


### Uso del SDK web

Puede recuperar actividades basadas en el Compositor basado en formularios utilizando `sendEvent` y pasando los nombres de mbox bajo el comando `decisionScopes` opción. El `sendEvent` El comando devolverá una promesa que se resuelve con un objeto que contiene las actividades/propuestas solicitadas: así es como se define la variable `propositions` la matriz tiene este aspecto:

```javascript
[
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "hero-banner",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434689"
      },
      "experience": {
        "id": "0"
      },
      "strategies": [
        {
          "algorithmID": "0",
          "trafficType": "0"
        }
      ],
      "characteristics": {
        "eventToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw=="
      }
    },
    "items": [
      {
        "id": "1184844",
        "schema": "https://ns.adobe.com/personalization/html-content-item",
        "meta": {
          "geo.state": "bucuresti",
          "activity.id": "434689",
          "experience.id": "0",
          "activity.name": "a4t test form based activity",
          "offer.id": "1184844",
          "profile.tntId": "04608610399599289452943468926942466370-pybgfJ"
        },
        "data": {
          "id": "1184844",
          "format": "text/html",
          "content": "<div> analytics impressions </div>"
        }
      }
    ]
  },
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "hero-banner",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434689"
      },
      "characteristics": {
        "eventToken": "E0gb6q1+WyFW3FMbbQJmrg=="
      }
    },
    "items": [
      {
        "id": "434689",
        "schema": "https://ns.adobe.com/personalization/measurement",
        "data": {
          "type": "click",
          "format": "application/vnd.adobe.target.metric"
        }
      }
    ]
  }
]
```

Por ejemplo:

```javascript
alloy("sendEvent", {
  xdm: { ...},
  decisionScopes: ["hero-banner"]
}).then(function (result) {
  var propositions = result.propositions;

  if (propositions) {
    // Find the discount proposition, if it exists.
    for (var i = 0; i < propositions.length; i++) {
      var proposition = propositions[i];
      for (var j = 0; j < proposition.items; j++) {
        var item = proposition.items[j];
        if (item.schema === HTML_SCHEMA) {
          // apply offer
          document.getElementById("form-based-offer-container").innerHTML =
            item.data.content;
          const executedPropositions = [
            {
              id: proposition.id,
              scope: proposition.scope,
              scopeDetails: proposition.scopeDetails
            }
          ];

          alloy("sendEvent", {
            "xdm": {
              "eventType": "decisioning.propositionDisplay",
              "_experience": {
                "decisioning": {
                  "propositions": executedPropositions
                }
              }
            }
          });
        }
      }
    }
  }
});
```

[Más información](../rendering-personalization-content.md#manually-rendering-content)

## Aplicación de las actividades de Target

### Uso de at.js

Puede aplicar las actividades de Target usando la variable `applyOffers` función: `adobe.target.applyOffer(options)`

Por ejemplo:

```javascript
adobe.target.getOffers({...})
  .then(response => adobe.target.applyOffers({ response: response }))
  .then(() => console.log("Success"))
  .catch(error => console.log("Error", error));
```

Obtenga más información acerca de `applyOffers` desde el [documentación dedicada](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-applyoffers-atjs-2.html).


### Uso del SDK web

Puede aplicar las actividades de Target usando la variable `applyPropositions` comando.

Por ejemplo:

```javascript
alloy("applyPropositions", {
    propositions: [...]
});
```

Obtenga más información acerca de `applyPropositions` desde el [documentación dedicada](../../personalization/rendering-personalization-content.md#applypropositions).

## Seguimiento de eventos

### Uso de at.js

Puede realizar un seguimiento de eventos utilizando `trackEvent` función o uso `sendNotifications`.

Esta función activa una solicitud para informar de las acciones del usuario, como clics y conversiones. No ofrece actividades en la respuesta.


**Ejemplo 1**

```javascript
adobe.target.trackEvent({ 
    "type": "click",
    "mbox": "some-mbox"
});
```

**Ejemplo 2**

```javascript
adobe.target.sendNotifications({ 
    request: {
       notifications: [{
          ...,
          mbox: {
            name: "some-mbox"
          },
          type: "click",
          ...
       }]
    }
});
```

[Más información](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-trackevent.html)

### Uso del SDK web

Puede realizar un seguimiento de eventos y acciones del usuario llamando a la función `sendEvent` , rellenando el `_experience.decisioning.propositions` grupo de campos XDM y configuración de `eventType` a uno de los dos valores:

* `decisioning.propositionDisplay`: indica la renderización de la actividad de Target.
* `decisioning.propositionInteract`: indica la interacción de un usuario con la actividad, como un clic del ratón.

El `_experience.decisioning.propositions` El grupo de campos XDM es una matriz de objetos. Las propiedades de cada objeto se derivan del `result.propositions` que se devuelve en el `sendEvent` comando: `{ id, scope, scopeDetails }`

**Ejemplo 1 - Pista a `decisioning.propositionDisplay` evento después de procesar una actividad**

```javascript
alloy("sendEvent", {
  xdm: {},
  decisionScopes: ['discount']
}).then(function(result) {
  var propositions = result.propositions;

  var discountProposition;
  if (propositions) {
    // Find the discount proposition, if it exists.
    for (var i = 0; i < propositions.length; i++) {
      var proposition = propositions[i];
      if (proposition.scope === "discount") {
        discountProposition = proposition;
        break;
      }
    }
  }

  if (discountProposition) {
    // Find the item from proposition that should be rendered.
    // Rather than assuming there a single item that has HTML
    // content, find the first item whose schema indicates
    // it contains HTML content.
    for (var j = 0; j < discountProposition.items.length; j++) {
      var discountPropositionItem = discountProposition.items[i];
      if (discountPropositionItem.schema === "https://ns.adobe.com/personalization/html-content-item") {
        var discountHtml = discountPropositionItem.data.content;
        // Render the content
        var dailySpecialElement = document.getElementById("daily-special");
        dailySpecialElement.innerHTML = discountHtml;
        
        // For this example, we assume there is only a single place to update in the HTML.
        break;  
      }
    }
      // Send a "decisioning.propositionDisplay" event signaling that the proposition has been rendered.
    alloy("sendEvent", {
      xdm: {
        eventType: "decisioning.propositionDisplay",
        _experience: {
          decisioning: {
            propositions: [
              {
                id: discountProposition.id,
                scope: discountProposition.scope,
                scopeDetails: discountProposition.scopeDetails
              }
            ]
          }
        }
      }
    });
  }
});
```

**Ejemplo 2 - Pista a `decisioning.propositionInteract` evento después de que se produzca una métrica de clic**

```javascript
alloy("sendEvent", {
  xdm: { ...},
  decisionScopes: ["hero-banner"]
}).then(function (result) {
  var propositions = result.propositions;

  if (propositions) {
    // Find the discount proposition, if it exists.
    for (var i = 0; i < propositions.length; i++) {
      var proposition = propositions[i];
      for (var j = 0; j < proposition.items.length; j++) {
        var item = proposition.items[j];

        if (item.schema === "https://ns.adobe.com/personalization/measurement") {
          // add metric to the DOM element
          const button = document.getElementById("form-based-click-metric");

          button.addEventListener("click", event => {
            const executedPropositions = [
              {
                id: proposition.id,
                scope: proposition.scope,
                scopeDetails: proposition.scopeDetails
              }
            ];
            // send the click track event
            alloy("sendEvent", {
              "xdm": {
                "eventType": "decisioning.propositionInteract",
                "_experience": {
                  "decisioning": {
                    "propositions": executedPropositions
                  }
                }
              }
            });
          });
        }
      }
    }
  }
});
```

[Más información](../rendering-personalization-content.md#manually-rendering-content)

## Cómo almacenar en déclencheur un cambio de vista en una aplicación de una sola página

### Uso de at.js

Utilice el `adobe.target.triggerView` función. Se puede llamar a esta función cada vez que se carga una página nueva o cuando se vuelve a procesar un componente de una página. SPA adobe.target.triggerView() debe implementarse para aplicaciones de una sola página () a fin de utilizar el Compositor de experiencias visuales (VEC) para crear pruebas A/B y actividades de segmentación de experiencias (XT). SPA Si adobe.target.triggerView() no se implementa en el sitio, el VEC no se puede utilizar para la segmentación de datos (VEC) en el sitio de.

**Ejemplo**

```javascript
adobe.target.triggerView("homeView")
```

[Más información](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-triggerview-atjs-2.html)


### Uso del SDK web

Para almacenar en déclencheur o señalar un cambio de vista de aplicación de una sola página, establezca el `web.webPageDetails.viewName` propiedad bajo el `xdm` de la opción `sendEvent` comando. El SDK web comprobará la caché de vistas si hay ofertas para `viewName` especificado en `sendEvent` los ejecutará y enviará un evento de notificación de visualización.

**Ejemplo**

```javascript
alloy("sendEvent", {
  renderDecisions: true,
  xdm:{
    web:{
      webPageDetails:{
        viewName: "homeView"
      }
    }
  }
});
```

[Más información](./spa-implementation.md#implementing-xdm-views)

## Cómo aprovechar los tokens de respuesta

El contenido de personalización devuelto desde Adobe Target incluye [tokens de respuesta](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html), que son detalles sobre la actividad, oferta, experiencia, perfil de usuario, información geográfica y más. Estos detalles se pueden compartir con herramientas de terceros o utilizar para la depuración. Los tokens de respuesta se pueden configurar en la interfaz de usuario de Adobe Target.

### Uso de at.js

Utilice eventos personalizados de at.js para detectar la respuesta de Target y leer los tokens de respuesta.

**Ejemplo**

```javascript
document.addEventListener(adobe.target.event.REQUEST_SUCCEEDED, function(e) { 
  console.log("Request succeeded", e.detail); 
}); 
```

[Más información](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html)


### Uso del SDK web

>[!IMPORTANT]
>
>Compruebe que está utilizando la versión 2.6.0 o posterior del SDK web de Platform.

Los tokens de respuesta se devuelven como parte de `propositions` que se exponen en el resultado de la `sendEvent` comando. Cada propuesta contiene una matriz de `items`y cada elemento tendrá un `meta` objeto rellenado con tokens de respuesta si están habilitados en la interfaz de usuario de administración de Target. [Más información](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html)

**Ejemplo**

```javascript
alloy("sendEvent", {
    renderDecisions: true,
    xdm: {}
  }).then(function(result) {
    if (result.propositions) {
      // Format of result.propositions:
      /*
        [
            {
                "id": "",
                "scope": "",
                "items": [
                    {
                        "id": "",
                        "schema": "",
                        "data": {},
                        "meta": { // RESPONSE TOKENS
                            "activity.name": ...,
                            "offer.id": ...,
                            "profile.activeActivities": ...
                        }
                    }
                ],
                "scopeDetails": {}
                "renderAttempted": false
            }
        ]
      */
    }
  });
```

[Más información](./accessing-response-tokens.md)

## Cómo administrar el parpadeo

### Uso de at.js

Con at.js puede administrar el parpadeo configurando `bodyHidingEnabled: true` de modo que at.js es el que se encargaría de ocultar previamente los contenedores personalizados antes de recuperar y aplicar los cambios del DOM.
Las secciones de la página que contienen contenido personalizado se pueden ocultar previamente anulando at.js `bodyHiddenStyle`.
De forma predeterminada `bodyHiddenStyle` oculta todo el HTML `body`.
Ambas configuraciones se pueden sobrescribir mediante `window.targetGlobalSettings`. `window.targetGlobalSettings` antes de cargar at.js.

### Uso del SDK web

Mediante el SDK web, el cliente puede configurar su estilo de ocultamiento previo en el comando configure, como en el ejemplo siguiente:

```javascript
alloy("configure", {
  edgeConfigId: "configurationId",
  orgId: "orgId@AdobeOrg",
  debugEnabled: true,
  prehidingStyle: "body { opacity: 0 !important }"
});
```

Al cargar el SDK web de forma asíncrona, se recomienda que el siguiente fragmento se inserte en la página antes de que se inserte el SDK web:

```html
<script>
  !function(e,a,n,t){
  if (a) return;
  var i=e.head;if(i){
  var o=e.createElement("style");
  o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),
  setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
  (document, document.location.href.indexOf("adobe_authoring_enabled") !== -1, "body { opacity: 0 !important }", 3000);
</script>
```

## Cómo se gestiona A4T

### Uso de at.js

Existen dos tipos de registro de A4T compatibles con at.js:

* Registro del lado del cliente de Analytics
* Registro en el servidor de Analytics

#### Registro del lado del cliente de Analytics

**Ejemplo 1: Uso de la configuración global de Target**

El registro en el lado del cliente de Analytics se puede habilitar configurando `analyticsLogging: client_side` en la configuración de at.js o anulando el `window.targetglobalSettings` objeto.
Cuando se configura esta opción, el formato de la carga útil que se devuelve es el siguiente:

```json
{
  "analytics": {
    "payload": {
      "pe": "tnt",
      "tnta": "167169:0:0|0|100,167169:0:0|2|100,167169:0:0|1|100"
    }
  }
}
```

La carga útil se puede reenviar a Analytics mediante la API de inserción de datos.

Ejemplo 2: configurarlo en cada `getOffers` función:

```javascript
adobe.target.getOffers({
      request: {
        experienceCloud: {
          analytics: {
            logging: "client_side"
          }
        },
        prefetch: {
          mboxes: [{
            index: 0,
            name: "a1-serverside-xt"
          }]
        }
      }
    })
    .then(console.log)
```

Este es el aspecto de la carga útil de respuesta:

```json
{
  "prefetch": {
    "mboxes": [{
      "index": 0,
      "name": "a1-serverside-xt",
      "options": [{
        "content": "<img src=\"http://s7d2.scene7.com/is/image/TargetAdobeTargetMobile/L4242-xt-usa?tm=1490025518668&fit=constrain&hei=491&wid=980&fmt=png-alpha\"/>",
        "type": "html",
        "eventToken": "n/K05qdH0MxsiyH4gX05/2qipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
        "responseTokens": {
          "profile.memberlevel": "0",
          "geo.city": "bucharest",
          "activity.id": "167169",
          "experience.name": "USA Experience",
          "geo.country": "romania"
        }
      }],
      "analytics": {
        "payload": {
          "pe": "tnt",
          "tnta": "167169:0:0|0|100,167169:0:0|2|100,167169:0:0|1|100"
        }
      }
    }]
  }
}
```

La carga útil de Analytics (`tnta` token) debe incluirse en la visita de Analytics mediante [API de inserción de datos](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md).

#### Registro en el servidor de Analytics

El registro en el lado del servidor de Analytics se puede habilitar configurando `analyticsLogging: server_side` en la configuración de at.js o anulando el `window.targetglobalSettings` objeto.
A continuación, los datos fluyen de la siguiente manera:

![](assets/a4t-server-side-atjs.png)

[Más información](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4timplementation.html)

### Uso del SDK web

El SDK web también admite:

* Registro en el lado del cliente de Analytics
* Registro en el servidor de Analytics

#### Registro del lado del cliente de Analytics

El registro del lado del cliente de Analytics está habilitado cuando Adobe Analytics está deshabilitado para esa configuración de DataStream.

![](assets/analytics-disabled-datastream-config.png)

El cliente tiene acceso al token de Analytics (`tnta`) que debe compartirse con Analytics mediante [API de inserción de datos](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md)
en encadenando el `sendEvent` e iterar a través de la matriz de propuestas resultante.

**Ejemplo**

```javascript
alloy("sendEvent", {
    "renderDecisions": true,
    "xdm": {
      "web": {
        "webPageDetails": {
          "name": "Home Page"
        }
      }
    }
  }
).then(function (results) {
  var analyticsPayloads = new Set();
  for (var i = 0; i < results.propositions.length; i++) {
    var proposition = results.propositions[i];
    var renderAttempted = proposition.renderAttempted;

    if (renderAttempted === true) {
      var analyticsPayload = getAnalyticsPayload(proposition);
      if (analyticsPayload !== undefined) {
        analyticsPayloads.add(analyticsPayload);
      }
    }
  }
  var analyticsPayloadsToken = concatenateAnalyticsPayloads(analyticsPayloads);
  // send the page view Analytics hit with collected Analytics payload using Data Insertion API
});
```

Este diagrama muestra cómo fluyen los datos cuando Analytics Client Side está habilitado:

![](assets/analytics-client-side-logging.png)

#### Registro en el servidor de Analytics

El registro del lado del servidor de Analytics está habilitado cuando Analytics está habilitado para esa configuración de DataStream.

![](assets/analytics-enabled-datastream-config.png)

Cuando el registro de Analytics del lado del servidor está habilitado, la carga útil de A4T que debe compartirse con Analytics para que los informes de Analytics muestren impresiones y conversiones correctas se compartan en el nivel de red perimetral, de modo que el cliente no tenga que realizar ningún procesamiento adicional.

Así es como los datos fluyen a nuestros sistemas cuando el registro de Analytics en el servidor está habilitado:

![](assets/analytics-server-side-logging.png)

## Cómo establecer la configuración global de Target

### Uso de at.js

En lugar de definir la configuración en la interfaz de usuario de Target Standard/Premium, puede anular la configuración de la biblioteca at.js mediante `window.targetGlobalSettings` o usar las API de REST.

La anulación debe definirse antes de que se cargue at.js o en Administración > Implementación > Editar la configuración de at.js > Configuración del código > Encabezado de la biblioteca.

Por ejemplo:

```javascript
window.targetGlobalSettings = {  
   timeout: 200, // using custom timeout  
   visitorApiTimeout: 500, // using custom API timeout  
   enabled: document.location.href.indexOf('https://www.adobe.com') >= 0 // enabled ONLY on adobe.com  
};
```

[Más información](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetgobalsettings.html)

### Uso del SDK web

Esta función no se admite en el SDK web.

## Actualización de los atributos de perfil de Target

### Uso de at.js

**Ejemplo 1**

```javascript
adobe.target.getOffer({
   mbox: "target-global-mbox",
   params: {
     "profile.name": "test",
     "profile.gender": "female"
   },
   success: console.log,
   error: console.error
});
```

**Ejemplo 2**

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        pageLoad: {
          profileParameters: {
            name: "test",
            gender: "female"
          }
        }
    }
  }
})
.then(console.log)
.catch(console.error);
```

### Uso del SDK web

Para actualizar un perfil de Target, utilice el `sendEvent` y establezca el `data.__adobe.target` , prefijando los nombres de clave mediante `profile`.

**Ejemplo**

```javascript
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "profile.gender": "female",
        "profile.age": 30
      }
    }
  }
});
```

## ¿Cómo utilizo Target Recommendations?

### Uso de at.js

**Ejemplo 1**

```javascript
adobe.target.getOffer({
   mbox: "target-global-mbox",
   params: {
     "entity.name": "T-shirt",
     "entity.id": "1234"
   },
   success: console.log,
   error: console.error
});
```

**Ejemplo 2**

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        pageLoad: {
          parameters: {
            "entity.name": "T-shirt",
            "entity.id": "1234"
          }
        }
    }
  }
})
.then(console.log)
.catch(console.error);
```

[Más información](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-getoffers-atjs-2.html)


### Uso del SDK web

Para enviar datos de Recommendations, utilice el `sendEvent` y establezca el `data.__adobe.target` , prefijando los nombres de clave mediante `entity`.

**Ejemplo**

```javascript
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "entity.name": "T-shirt",
        "entity.id": "1234"
      }
    }
  }
});
```

## ¿Cómo utilizo ID de terceros?

### Uso de at.js

Con at.js hay varias formas de enviar `mbox3rdPartyId`, usando `getOffer` o `getOffers`:

**Ejemplo 1**

```javascript
adobe.target.getOffer({
  mbox:"test",
  params:{
    "mbox3rdPartyId": "1234"
  },
  success: console.log,
  error: console.error
});
```

**Ejemplo 2**

```javascript
adobe.target.getOffers({
    request: {
      id:{
        thirdPartyId: "1234"
      },
      execute: {
        pageLoad: {}
    }
  }
})
.then(console.log)
.catch(console.error);
```

O existe una forma de configurar el `mbox3rdPartyId` en `targetPageParams` o `targetPageParamsAll`.
Al establecerlo en `targetPageParams`, se enviará en las solicitudes de `target-global-mbox` también conocido como `pag-lLoad`.
La recomendación se debe establecer utilizando `targetPageParamsAll` ya que se envía en cada solicitud de target.
La ventaja de utilizar `targetPageParamsAll` es que puede definir el `mbox3rdPartyId` en la página una vez, lo que garantiza que todas las solicitudes de target tengan el derecho de `mbox3rdPartyId`.

```javascript
window.targetPageParamsAll = function() {
      return {
        "mbox3rdPartyId": "1234"
      };
    };
```

```javascript
window.targetPageParams = function() {
  return {
    "mbox3rdPartyId": "1234"
  };
};
```

[Más información](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetpageparams.html)

### Uso del SDK web

El SDK web admite el ID de terceros de Target. Sin embargo, se requieren algunos pasos más. Antes de sumergirse en la solución, deberíamos hablar un poco sobre `identityMap`.
El mapa de identidad permite a los clientes enviar varias identidades. Todas las identidades tienen un espacio de nombres. Cada área de nombres puede tener una o más identidades. Una identidad en particular se puede marcar como principal.
Con este conocimiento en mente, podemos ver cuáles son los pasos necesarios para configurar el sdk web para utilizar el ID de terceros de Target.

1. Configure el área de nombres que contendrá el ID de terceros de Target en la vista Configuración del flujo de datos:

![](assets/mbox-3-party-id-setup.png)

1. Envíe ese área de nombres de identidad en cada comando sendEvent como se muestra a continuación:

```javascript
alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
    "identityMap": {
      "TGT3PID": [
        {
          "id": "1234",
          "primary": true
        }
      ]
    }
  }
});
```

## ¿Cómo se establecen los tokens de propiedad?

### Uso de at.js

Con at.js, hay dos formas de configurar los tokens de propiedad: mediante `targetPageParams` o `targetPageParamsAll`. Uso de `targetPageParams` agrega el token de propiedad a `target-global-mbox` llamada a, pero con `targetPageParamsAll` añade el token a todas las llamadas de target:

**Ejemplo 1**

```javascript
   window.targetPageParamsAll = function() {
      return {
        "at_property": "1234"
      };
    };
```

**Ejemplo 2**

```javascript
window.targetPageParams = function() {
      return {
        "at_property": "1234"
      };
    };
```

### Uso del SDK web

Mediante el SDK web, los clientes pueden configurar la propiedad en un nivel superior, al configurar la secuencia de datos, en el área de nombres de Adobe Target:
![](assets/at-property-setup.png)
Esto significa que cada llamada de Target para esa configuración de flujo de datos específica va a contener ese token de propiedad.

## ¿Cómo puedo recuperar previamente los mboxes?

### Uso de at.js

Esta funcionalidad solo está disponible en at.js 2.x. at.js 2.x tiene una nueva función denominada `getOffers`. `getOffers` permite a los clientes recuperar previamente contenido para uno o más mboxes. Vea el siguiente ejemplo:

```javascript
adobe.target.getOffers({
    request: {
      prefetch: {
        mboxes: [{
          index: 0,
          name: "test-mbox",
          parameters: {
            ...
          },
          profileParameters: {
            ...
          }
        }]
    }
  }
})
.then(console.log)
.catch(console.error);
```

NOTA: Se recomienda encarecidamente asegurarse de que cada `mbox` en el `mboxes` la matriz tiene su propio índice. Normalmente, el primer mbox tiene `index=0`, el siguiente `index=1`, etc.

### Uso del SDK web

Actualmente, esta funcionalidad no se admite en el SDK web.

## Cómo depuro mi implementación de Target

### Uso de at.js

At.js expone estas funciones de depuración:

* Deshabilitar mbox: deshabilitar Target para que no recupere ni procese para comprobar si la página está rota sin interacciones de Target
* Depuración de mbox: at.js registra todas las acciones
* Seguimiento de Target: Con un token de seguimiento de mbox generado en Bullseye, hay disponible un objeto de seguimiento con detalles que participaron en el proceso de toma de decisiones en `window.___target_trace` objeto

Nota: Todas estas funciones de depuración están disponibles con funciones mejoradas en [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

### Uso del SDK web

Dispone de varias funciones de depuración al utilizar el SDK web:

* Uso de [Assurance](../../../assurance/home.md)
* [Depuración del SDK web habilitada](../../../edge/fundamentals/debugging.md)
* Uso [Enlaces de monitorización del SDK web](https://github.com/adobe/alloy/wiki/Monitoring-Hooks)
* Uso [Adobe Experience Platform Debugger](../../../debugger/home.md)
* Seguimiento de destino
