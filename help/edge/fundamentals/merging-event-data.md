---
title: Combinación de datos de evento
seo-title: Combinación de datos de evento del SDK web de Adobe Experience Platform
description: Aprenda a combinar datos de evento del SDK web Experience Platform
seo-description: Aprenda a combinar datos de evento del SDK web Experience Platform
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---


# Combinación de datos de evento

>[!IMPORTANT]
>
>Esta función aún está en desarrollo. No todas las soluciones podrán combinar datos de evento como se describe en esta página.

A veces, no todos los datos están disponibles cuando se produce un evento. Es posible que desee capturar los datos que _sí_ tiene para que no se pierda si, por ejemplo, el usuario cierra el explorador. Por otro lado, también puede incluir cualquier dato que esté disponible más adelante.

En estos casos, puede combinar datos con eventos anteriores pasando `eventMergeId` como opción a los `event` comandos de la siguiente manera:

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
  "eventMergeId": "ABC123"
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
  }
  "eventMergeId": "ABC123"
});
```

Al pasar el mismo `eventMergeID` valor a ambos comandos de evento en este ejemplo, los datos del segundo comando de evento se incrementan a los datos enviados anteriormente en el primer comando de evento. Se crea un registro para cada comando de evento en el [!DNL Experience Data Platform], pero durante el sistema de informes los registros se unen mediante el `eventMergeID` y aparecen como un solo evento.

Si está enviando datos sobre un evento concreto a proveedores de terceros, también puede incluir lo mismo `eventMergeID` con esos datos. Más adelante, si decide importar los datos de terceros en el Adobe Experience Platform, `eventMergeID` se utilizarán para combinar todos los datos recopilados como resultado del evento discreto que se produjo en la página web.

## Generación de un `eventMergeID`

El `eventMergeID` valor puede ser cualquier cadena que elija, pero recuerde que todos los eventos enviados con el mismo ID se notifican como un solo evento, por lo que tenga cuidado de imponer la exclusividad cuando no se deban combinar eventos. Si desea que el SDK genere un único `eventMergeID` en su nombre (siguiendo la especificación [ampliamente adoptada](https://www.ietf.org/rfc/rfc4122.txt)UUID v4), puede utilizar el `createEventMergeId` comando para hacerlo.

Como con todos los comandos, se devuelve una promesa porque puede ejecutar el comando antes de que el SDK haya terminado de cargarse. La promesa se resolverá con un único `eventMergeID` tiempo. Puede esperar a que se resuelva la promesa antes de enviar datos al servidor de la siguiente manera:

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
    }
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
    }
    "mergeId": results.eventMergeId
  });
});
```

Siga este mismo patrón si desea acceder a la página `eventMergeID` por otros motivos (por ejemplo, para enviarla a un proveedor de terceros):

```javascript
var eventMergeIdPromise = alloy("createEventMergeId");

eventMergeIdPromise.then(function(results) {
  // send event merge ID to a third-party provider
  console.log(results.eventMergeId);
});
```

## Nota sobre el formato XDM

Dentro del comando evento, el `mergeId` se agrega a la `xdm` carga útil.  Si lo desea, la opción `mergeId` se puede enviar como parte de la opción xdm, como se muestra a continuación:

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
