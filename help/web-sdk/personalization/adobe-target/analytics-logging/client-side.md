---
title: Registro del lado del cliente para datos de A4T en Experience Platform Web SDK
description: Obtenga información sobre cómo habilitar el registro en el lado del cliente para Adobe Analytics for Target (A4T) mediante Experience Platform Web SDK.
seo-title: Client-side logging for A4T data in the Experience Platform Web SDK
seo-description: Learn how to enable client-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: target;a4t;registro;sdk web;experiencia;plataforma;
exl-id: 7071d7e4-66e0-4ab5-a51a-1387bbff1a6d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1090'
ht-degree: 0%

---

# Registro del lado del cliente para datos de A4T en Experience Platform Web SDK

## Información general {#overview}

Adobe Experience Platform Web SDK le permite recopilar datos de [Adobe Analytics for Target (A4T)](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=es) en el lado del cliente de la aplicación web.

El registro en el lado del cliente significa que se devuelven datos relevantes de [!DNL Target] en el lado del cliente, lo que le permite recopilarlos y compartirlos con Analytics. Esta opción debería habilitarse si desea enviar manualmente datos a Analytics mediante la [API de inserción de datos](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html?lang=es).

>[!NOTE]
>
>Actualmente se está desarrollando un método para realizar esto usando [AppMeasurement.js](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=es), que estará disponible en un futuro próximo.

Este documento describe los pasos para configurar el registro de A4T del lado del cliente para Web SDK y proporciona algunos ejemplos de implementación para casos de uso comunes.

## Requisitos previos {#prerequisites}

En este tutorial se da por hecho que está familiarizado con los conceptos y procesos fundamentales relacionados con el uso de Web SDK con fines de personalización. Consulte la siguiente documentación si necesita una introducción:

* [Configuración de Web SDK](/help/web-sdk/commands/configure/overview.md)
* [Envío de eventos](/help/web-sdk/commands/sendevent/overview.md)
* [Representación de contenido de personalización](../../rendering-personalization-content.md)

## Configuración del registro en el lado del cliente de Analytics {#set-up-client-side-logging}

Las siguientes subsecciones describen cómo habilitar el registro en el lado del cliente de Analytics para la implementación de Web SDK.

### Habilitar el registro en el lado del cliente de Analytics {#enable-analytics-client-side-logging}

Para considerar el registro del lado del cliente de Analytics habilitado para la implementación, debe deshabilitar la configuración de Adobe Analytics en su [secuencia de datos](../../../../datastreams/overview.md).

![Configuración del flujo de datos de Analytics deshabilitada](../assets/disable-analytics-datastream.png)

### Recuperar [!DNL A4T] datos de SDK y enviarlos a Analytics {#a4t-to-analytics}

Para que este método de generación de informes funcione correctamente, debe enviar los datos relacionados con [!DNL A4T] recuperados del comando [`sendEvent`](/help/web-sdk/commands/sendevent/overview.md) en la visita de Analytics.

Cuando Target Edge calcula una respuesta de propuestas, comprueba si el registro del lado del cliente de Analytics está habilitado (es decir, si Analytics está deshabilitado en la secuencia de datos). Si el registro en el lado del cliente está habilitado, el sistema agrega un token de Analytics a cada propuesta en la respuesta.

El flujo tiene un aspecto similar al siguiente:

![Flujo de registro del lado del cliente](../assets/analytics-client-side-logging.png)

El siguiente es un ejemplo de una respuesta `interact` cuando el registro del lado del cliente de Analytics está habilitado. Si la propuesta es para una actividad que tiene informes de Analytics, tendrá una propiedad `scopeDetails.characteristics.analyticsToken`.

```json
{
  "requestId": "1234",
  "handle": [
    {
      "payload": [
        {
          "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
          "scope": "a4t-test",
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
              "eventToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw==",
              "analyticsToken": "434689:0:0|2,434689:0:0|1"
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
          "scope": "a4t-test",
          "scopeDetails": {
            "decisionProvider": "TGT",
            "activity": {
              "id": "434689"
            },
            "characteristics": {
              "eventToken": "E0gb6q1+WyFW3FMbbQJmrg==",
              "analyticsToken": "434689:0:0|32767"
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
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

Las propuestas para actividades del Compositor de experiencias basadas en formularios pueden contener contenido y elementos de métricas de clic en la misma propuesta. Por lo tanto, en lugar de tener un solo token de análisis para la visualización de contenido en la propiedad `scopeDetails.characteristics.analyticsToken`, pueden tener un token de análisis de clic y visualización especificado en las propiedades `scopeDetails.characteristics.analyticsDisplayToken` y `scopeDetails.characteristics.analyticsClickToken`, según corresponda.

```json
{
  "requestId": "1234",
  "handle": [
    {
      "payload": [
        {
          "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
          "scope": "a4t-test",
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
               "displayToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw==",
               "clickToken": "E0gb6q1+WyFW3FMbbQJmrg==",
               "analyticsDisplayToken": "434689:0:0|2,434689:0:0|1", 
               "analyticsClickToken": "434689:0:0|32767"
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
            },
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
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

Todos los valores de `scopeDetails.characteristics.analyticsToken`, así como `scopeDetails.characteristics.analyticsDisplayToken` (para el contenido mostrado) y `scopeDetails.characteristics.analyticsClickToken` (para las métricas de clics) son las cargas útiles de A4T que deben recopilarse e incluirse como etiqueta `tnta` en la llamada de la API de inserción de datos [Data Insertion](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md).

>[!IMPORTANT]
>
>Las propiedades `analyticsToken`, `analyticsDisplayToken`, `analyticsClickToken` pueden contener varios tokens, concatenados como una sola cadena delimitada por comas.
>
>En los ejemplos de implementación que se proporcionan en la siguiente sección, se recopilan varios tokens de Analytics de forma iterativa. Para concatenar una matriz de tokens de Analytics, utilice una función similar a esta:
>
>```javascript
>var concatenateAnalyticsPayloads = function concatenateAnalyticsPayloads(analyticsPayloads) {
>   if (analyticsPayloads.size > 1) {
>       return [].concat(analyticsPayloads).join(',');
>   }
>   return [].concat(analyticsPayloads).join();
>};
>```

## Ejemplos de implementación {#implementation-examples}

Las siguientes subsecciones muestran cómo implementar el registro del lado del cliente de Analytics para casos de uso comunes.

### Actividades del Compositor de experiencias basadas en formularios {#form-based-composer}

Puede usar Web SDK para controlar la ejecución de propuestas desde las actividades de [Adobe Target Form-Based Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=es).

Cuando se solicitan propuestas para un ámbito de decisión específico, la propuesta devuelta contiene el token de Analytics correspondiente. La práctica recomendada es encadenar el comando `sendEvent` de Experience Platform Web SDK e iterar por las propuestas devueltas para ejecutarlas mientras se recopilan los tokens de Analytics al mismo tiempo.

Puede almacenar en déclencheur un comando `sendEvent` para un ámbito de actividad del Compositor de experiencias basadas en formularios de esta manera:

```javascript
alloy("sendEvent", {
    "decisionScopes": ["a4t-test"],
    "xdm": {
      "web": {
        "webPageDetails": {
          "name": "Home Page"
        }
      }
    }
  }
).then(function(results) {
  for (var i = 0; i < results.propositions.length; i++) {
    //Execute the propositions and collect the Analytics payload
  }
});
```

Desde aquí, debe implementar código para ejecutar las propuestas y construir una carga útil que finalmente se enviará a Analytics. Este es un ejemplo de lo que `results.propositions` podría contener:

```json
[
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "a4t-test",
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
        "eventToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw==",
        "analyticsToken": "434689:0:0|2,434689:0:0|1"
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
    "scope": "a4t-test",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434689"
      },
      "characteristics": {
        "eventToken": "E0gb6q1+WyFW3FMbbQJmrg==",
        "analyticsToken": "434689:0:0|32767"
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
  },
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "a4t-test",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434688"
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
          "displayToken": "91TS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqgEt==",
          "clickToken": "Tagb6q1+WyFW3FMbbQJrtg==",
          "analyticsDisplayTokens": "434688:0:0|2,434688:0:0|1",
          "analyticsClickTokens": "434688:0:0|32767"
        }
      }
    },
    "items": [
      {
        "id": "1184845",
        "schema": "https://ns.adobe.com/personalization/html-content-item",
        "meta": {
          "geo.state": "bucuresti",
          "activity.id": "434688",
          "experience.id": "0",
          "activity.name": "a4t test form based activity 1",
          "offer.id": "1184845"
        },
        "data": {
          "id": "1184845",
          "format": "text/html",
          "content": "<div> analytics impressions 1</div>"
        }
      },
      {
        "id": "434688",
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

Para extraer el token de Analytics de una propuesta con elementos de contenido, puede implementar una función similar a la siguiente:

```javascript
function getDisplayAnalyticsPayload(proposition) {
  if (!proposition || !proposition.scopeDetails || !proposition.scopeDetails.characteristics) {
    return;
  }
  var characteristics = proposition.scopeDetails.characteristics;
  if (characteristics.analyticsDisplayToken) {
    return characteristics.analyticsDisplayToken;
  }
  return characteristics.analyticsToken;
}
```

Una propuesta puede tener diferentes tipos de elementos, tal como indica la propiedad `schema` del elemento en cuestión. Hay cuatro esquemas de elementos de propuesta compatibles con las actividades del Compositor de experiencias basadas en formularios:

```javascript
var HTML_SCHEMA = "https://ns.adobe.com/personalization/html-content-item";
var MEASUREMENT_SCHEMA = "https://ns.adobe.com/personalization/measurement";
var JSON_SCHEMA = "https://ns.adobe.com/personalization/json-content-item";
var REDIRECT_SCHEMA = "https://ns.adobe.com/personalization/redirect-item";
```

`HTML_SCHEMA` y `JSON_SCHEMA` son los esquemas que reflejan el tipo de oferta, mientras que `MEASUREMENT_SCHEMA` refleja las métricas que deben adjuntarse a un elemento DOM.

Las cargas útiles de Analytics para métricas de clics deben recopilarse y enviarse a Analytics por separado de los elementos de contenido en el momento en que el visitante hace clic en el contenido mostrado anteriormente.

La siguiente función de ayuda para obtener la métrica de clics de cargas útiles de A4T será útil en este caso:

```javascript
function getClickAnalyticsPayload(proposition) {
  if (!proposition || !proposition.scopeDetails || !proposition.scopeDetails.characteristics) {
    return;
  }
  var characteristics = proposition.scopeDetails.characteristics;
  if (characteristics.analyticsClickToken) {
    return characteristics.analyticsClickToken;
  }
  return characteristics.analyticsToken;
}
```

#### Resumen de implementación {#implementation-summary}

En resumen, los siguientes pasos deben ejecutarse al aplicar actividades del Compositor de experiencias basadas en formularios con Experience Platform Web SDK:

1. Envíe un evento que obtenga ofertas de actividad del Compositor de experiencias basadas en formularios;
1. Aplicar los cambios de contenido a la página;
1. Enviar el evento de notificación `decisioning.propositionDisplay`;
1. Recopile los tokens de visualización de Analytics de la respuesta de SDK y construya una carga útil para la visita de Analytics;
1. Enviar la carga útil a Analytics mediante la [API de inserción de datos](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md);
1. Si hay métricas de clics en las propuestas enviadas, los oyentes de clics deben configurarse para que cuando se realice un clic, envíe el evento de notificación `decisioning.propositionInteract`. El controlador `onBeforeEventSend` debe configurarse para que al interceptar `decisioning.propositionInteract` eventos, se produzcan las siguientes acciones:
   1. Recopilando los tokens de Click Analytics de `xdm._experience.decisioning.propositions`
   1. Enviando la visita de Click Analytics con la carga útil recopilada de Analytics a través de [API de inserción de datos](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md);

```javascript
alloy("sendEvent", {
    "decisionScopes": ["a4t-test"],
    "xdm": {
      "web": {
        "webPageDetails": {
          "name": "Home Page"
        }
      }
    }
  }
).then(function(results) {
  var analyticsPayload = new Set();
  results.propositions.forEach(function (proposition) {
    proposition.items.forEach(function (item) {
      if (item.schema === HTML_SCHEMA) {
        // 1. Apply offer
        // 2. Collect executed propositions and send the decisioning.propositionDisplay notification event
        // 3. Collect the display Analytics tokens
      }
      if (item.schema === MEASUREMENT_SCHEMA) {
        // Setup click listener, so that when clicked:
        // 1. Collect clicked propositions and send the decisioning.propositionInteract notification event
        // Note: onBeforeEventSend handler should be configured, so that when intercepting decisioning.propositionInteract events:
        //   1. Collect the click Analytics tokens from xdm._experience.decisioning.propositions
        //   2. Send the click Analytics hit with the collected Analytics payload via Data Insertion API
      }
    });
  });
  // Send the page view Analytics hit with the collected display Analytics payload via Data Insertion API
});
```

### Actividades del Compositor de experiencias visuales {#visual-experience-composer-acitivties}

Web SDK le permite gestionar ofertas creadas con [Compositor de experiencias visuales (VEC)](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=es).

>[!NOTE]
>
>Los pasos para implementar este caso de uso son muy similares a los pasos para [actividades del Compositor de experiencias basadas en formularios](#form-based-composer). Consulte la sección anterior para obtener más información.

Cuando se habilita el procesamiento automático, puede recopilar los tokens de Analytics de las propuestas que se ejecutaron en la página. La práctica recomendada es encadenar el comando `sendEvent` de Experience Platform Web SDK e iterar en las propuestas devueltas para filtrar las que Web SDK ha intentado procesar.

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
  
    var proposition = propositions[i];
    var renderAttempted = proposition.renderAttempted;

    if (renderAttempted === true) {
      var analyticsPayload = getDisplayAnalyticsPayload(proposition);
      
      if (analyticsPayload !== undefined) {
        analyticsPayloads.add(analyticsPayload);
      }
    }
  }
  var analyticsPayloadsToken = concatenateAnalyticsPayloads(analyticsPayloads);
  // Send the page view Analytics hit with collected Analytics payload via Data Insertion API
});
```

### Usar `onBeforeEventSend` para controlar las métricas de página {#using-onbeforeeventsend}

Con las actividades de Adobe Target, puede configurar diferentes métricas en la página, ya sea manualmente adjuntas al DOM o automáticamente adjuntas al DOM (actividades creadas por VEC). Ambos tipos son una interacción retrasada del usuario final en la página web.

Para tener en cuenta esto, la práctica recomendada es recopilar cargas útiles de Analytics mediante el vínculo `onBeforeEventSend` de Adobe Experience Platform Web SDK. El vínculo `onBeforeEventSend` debe configurarse con el comando `configure` y se reflejará en todos los eventos que se envíen a través de la secuencia de datos.

A continuación se muestra un ejemplo de cómo se puede configurar `onBeforeEventSent` para almacenar en déclencheur las visitas de Analytics:

```javascript
alloy("configure", {
  datastreamId: "datastream configuration ID",
  orgId: "adobe ORG ID",
  onBeforeEventSend: function(options) {
    const xdm = options.xdm;
    const eventType = xdm.eventType;
    if (eventType === "decisioning.propositionInteract") {
      const analyticsPayloads = new Set();
      const propositions = xdm._experience.decisioning.propositions;

      for (var i = 0; i < propositions.length; i++) {
        var proposition = propositions[i];
        analyticsPayloads.add(getClickAnalyticsPayload(proposition));
      }
      // Trigger the Analytics hit
    }
  }
});
```

## Pasos siguientes {#next-steps}

En esta guía se describe el registro en el lado del cliente de datos de A4T en Web SDK. Consulte la guía sobre [registro en el lado del servidor](server-side.md) para obtener más información sobre cómo administrar los datos de A4T en Edge Network.
