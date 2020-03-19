---
title: Combinación de datos de eventos
seo-title: Combinación de datos de eventos del SDK web de Adobe Experience Platform
description: Aprenda a combinar los datos de eventos del SDK web de la plataforma de experiencia
seo-description: Aprenda a combinar los datos de eventos del SDK web de la plataforma de experiencia
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (Beta) Combinación de datos de eventos

>[!IMPORTANT]
>
>El SDK web de la plataforma de experiencia de Adobe se encuentra en fase beta y no está disponible para todos los usuarios. La documentación y la funcionalidad están sujetas a cambios.

En ocasiones, no todos los datos están disponibles cuando se produce un evento. Es posible que desee capturar los datos que _sí_ tiene para que no se pierda si, por ejemplo, el usuario cierra el explorador. Por otro lado, también puede incluir cualquier dato que esté disponible más adelante.

En estos casos, puede combinar datos con eventos anteriores pasando `eventMergeId` como una opción a los `event` comandos de la siguiente manera:

```javascript
alloy("event", {
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
  "eventMergeId": "ABC123"
});

// Time passes and more data becomes available

alloy("event", {
  "xdm": {
    "commerce": {
      "order": {
        "payments": [
          {
            "transactionID": "TR426941",
            "paymentAmount": 999.98,
            "paymentType": "credit_card",
            "currencyCode": "USD"
          }
        ]
      }
    }
  }
  "eventMergeId": "ABC123"
});
```

Al pasar el mismo valor de ID de combinación de eventos a ambos comandos de evento en este ejemplo, los datos del segundo comando de evento se incrementan a los datos enviados anteriormente en el primer comando de evento. En la plataforma de datos de experiencia se crea un registro para cada comando de evento, pero durante el informe los registros se unen mediante el ID de combinación de eventos y aparecen como un solo evento.

Si envía datos sobre un evento concreto a proveedores de terceros, también puede incluir el mismo ID de combinación de eventos con esos datos. Más adelante, si decide importar los datos de terceros en Adobe Experience Platform, el ID de combinación de eventos se utilizará para combinar todos los datos recopilados como resultado del evento discreto que se produjo en la página web.

## Generación de un ID de combinación de eventos

El valor de ID de combinación de eventos puede ser cualquier cadena que elija, pero recuerde que todos los eventos enviados con el mismo ID se notifican como un evento único, por lo que tenga cuidado de imponer la exclusividad cuando los eventos no se deban combinar. Si desea que el SDK genere un ID de combinación de eventos único en su nombre (siguiendo la especificación [](https://www.ietf.org/rfc/rfc4122.txt)UUID v4 ampliamente adoptada), puede utilizar el `createEventMergeId` comando para hacerlo.

Como con todos los comandos, se devuelve una promesa porque puede ejecutar el comando antes de que el SDK haya terminado de cargarse. La promesa se resolverá con una ID única de combinación de eventos lo antes posible. Puede esperar a que se resuelva la promesa antes de enviar datos al servidor de la siguiente manera:

```javascript
var eventMergeIdPromise = alloy("createEventMergeId");

eventMergeIdPromise.then(function(eventMergeId) {
  alloy("event", {
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
    "mergeId": eventMergeId
  });
});

// Time passes and more data becomes available

eventMergeIdPromise.then(function(eventMergeId) {
  alloy("event", {
    "xdm": {
      "commerce": {
        "order": {
          "payments": [
            {
              "transactionID": "TR426941",
              "paymentAmount": 999.98,
              "paymentType": "credit_card",
              "currencyCode": "USD"
            }
          ]
        }
      }
    }
    "mergeId": eventMergeId
  });
});
```

Siga este mismo patrón si desea acceder al ID de combinación de eventos por otros motivos (por ejemplo, para enviarlo a un proveedor de terceros):

```javascript
var eventMergeIdPromise = alloy("createEventMergeId");

eventMergeIdPromise.then(function(eventMergeId) {
  // send event merge ID to a third-party provider
  console.log(eventMergeId);
});
```

## Nota sobre el formato XDM

Dentro del comando event, el `mergeId` se agrega a la `xdm` carga útil.  Si lo desea, la opción `mergeId` se puede enviar como parte de la opción xdm, como se muestra a continuación:

```javascript
alloy("event", {
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    },
    "eventMergeId": "ABC123"
  }
});
```
