---
title: Combinar datos de Evento en el SDK web de Adobe Experience Platform
description: Aprenda a combinar datos de evento del SDK web Experience Platform
keywords: combinar;datos de evento;eventMergeId;createEventMergeId;sendEvent;mergeId;id de combinación;eventMergeIdPromise; Promesa De Id De Combinación;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 0%

---


# Combinar datos de evento

>[!IMPORTANT]
>
>Esta función aún está en desarrollo. No todas las soluciones podrán combinar datos de evento como se describe en esta página.

A veces, no todos los datos están disponibles cuando se produce un evento. Es posible que desee capturar los datos que tiene para que no se pierdan si, por ejemplo, el usuario cierra el explorador. Por otro lado, también puede incluir cualquier dato que esté disponible más adelante.

En estos casos, puede combinar datos con eventos anteriores pasando `mergeId` como opción a los comandos `event` de la siguiente manera:

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
  },
  "mergeId": "ABC123"
});

// Time passes and more data becomes available

alloy("sendEvent", {
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
  },
  "mergeId": "ABC123"
});
```

Al pasar el mismo valor para la opción `mergeId` a ambos comandos de evento en este ejemplo, los datos del segundo comando de evento se incrementan a los datos enviados anteriormente en el primer comando de evento. En [!DNL Experience Data Platform] se crea un registro para cada comando evento, pero durante el sistema de informes los registros se unen mediante el ID de combinación de eventos y aparecen como un solo evento.

Si envía datos sobre un evento concreto a proveedores de terceros, puede incluir también el mismo ID de combinación de eventos con esos datos. Más adelante, si decide importar los datos de terceros en Adobe Experience Platform, el ID de combinación de eventos se utilizará para combinar todos los datos recopilados como resultado del evento discreto que se produjo en la página web.

## Generación de un ID de combinación de eventos

El ID de combinación de eventos puede ser cualquier cadena que elija, pero recuerde que todos los eventos enviados con el mismo ID se notifican como un solo evento, por lo que tenga cuidado de imponer la exclusividad cuando no se deban combinar eventos. Si desea que el SDK genere un ID de combinación de eventos único en su nombre (siguiendo la especificación [UUID v4 ampliamente adoptada](https://www.ietf.org/rfc/rfc4122.txt)), puede utilizar el comando `createEventMergeId` para hacerlo.

Como con todos los comandos, se devuelve una promesa porque puede ejecutar el comando antes de que el SDK haya terminado de cargarse. La promesa se resolverá con un ID de combinación de eventos único lo antes posible. Puede esperar a que se resuelva la promesa antes de enviar datos al servidor de la siguiente manera:

```javascript
var eventMergeIdPromise = alloy("createEventMergeId");

eventMergeIdPromise.then(function(results) {
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
    },
    "mergeId": results.eventMergeId
  });
});

// Time passes and more data becomes available

eventMergeIdPromise.then(function(results) {
  alloy("sendEvent", {
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
    },
    "mergeId": results.eventMergeId
  });
});
```

Siga este mismo patrón si desea acceder al ID de combinación de eventos por otros motivos (por ejemplo, para enviarlo a un proveedor de terceros):

```javascript
var eventMergeIdPromise = alloy("createEventMergeId");

eventMergeIdPromise.then(function(results) {
  // send event merge ID to a third-party provider
  console.log(results.eventMergeId);
});
```

## Nota sobre el formato XDM

Dentro del comando evento, el ID de combinación de eventos se agrega a la carga útil `xdm` en la ubicación correcta de su nombre.  Si lo desea, el ID de combinación de eventos se puede enviar como parte de la opción `xdm`, como se muestra a continuación:

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
    },
    "eventMergeId": "ABC123"
  }
});
```

Al agregar el ID de combinación de eventos al objeto `xdm` directamente, observe que se utiliza el nombre `eventMergeID` en lugar de `mergeId`.
