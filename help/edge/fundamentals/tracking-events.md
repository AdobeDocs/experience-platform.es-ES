---
title: Seguimiento de eventos con el SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo rastrear eventos del SDK web de Adobe Experience Platform.
keywords: sendEvent;xdm;eventType;datasetId;sendBeacon;enviar señalización;documentUnloading;descarga de documento;onBeforeEventSend;
exl-id: 8b221cae-3490-44cb-af06-85be4f8d280a
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '1451'
ht-degree: 0%

---

# Seguimiento de eventos

Para enviar datos de evento a Adobe Experience Cloud, utilice el comando `sendEvent`. El comando `sendEvent` es la forma principal de enviar datos a [!DNL Experience Cloud] y recuperar contenido personalizado, identidades y destinos de audiencia.

Los datos enviados a Adobe Experience Cloud se dividen en dos categorías:

* Datos XDM
* Datos no XDM

## Envío de datos XDM

Los datos XDM son un objeto cuyo contenido y estructura coinciden con un esquema creado en Adobe Experience Platform. [Obtenga más información sobre cómo crear un esquema.](../../xdm/tutorials/create-schema-ui.md)

Los datos XDM que desee que formen parte de su análisis, personalización, audiencias o destinos se deben enviar mediante la opción `xdm` .


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
});
```

Puede pasar algún tiempo entre el momento en que se ejecuta el comando `sendEvent` y el momento en que se envían los datos al servidor (por ejemplo, si la biblioteca del SDK web no se ha cargado completamente o aún no se ha recibido el consentimiento). Si tiene intención de modificar cualquier parte del objeto `xdm` después de ejecutar el comando `sendEvent`, es muy recomendable clonar el objeto `xdm` _antes de_ ejecutar el comando `sendEvent`. Por ejemplo:

```javascript
var clone = function(value) {
  return JSON.parse(JSON.stringify(value));
};

var dataLayer = {
  "commerce": {
    "order": {
      "purchaseID": "a8g784hjq1mnp3",
      "purchaseOrderNumber": "VAU3123",
      "currencyCode": "USD",
      "priceTotal": 999.98
    }
  }
};

alloy("sendEvent", {
  "xdm": clone(dataLayer)
});

// This change will not be reflected in the data sent to the 
// server for the prior sendEvent command.
dataLayer.commerce = null;
```

En este ejemplo, la capa de datos se clona serializándola en JSON y luego deserializándola. A continuación, el resultado clonado se pasa al comando `sendEvent`. Esto garantiza que el comando `sendEvent` tenga una instantánea de la capa de datos tal como existía cuando se ejecutó el comando `sendEvent` para que las modificaciones posteriores en el objeto de capa de datos original no se reflejen en los datos enviados al servidor. Si utiliza una capa de datos impulsada por eventos, es probable que la clonación de los datos ya se haya gestionado automáticamente. Por ejemplo, si utiliza la [capa de datos del cliente de Adobe](https://github.com/adobe/adobe-client-data-layer/wiki), el método `getState()` proporciona una instantánea calculada y clonada de todos los cambios anteriores. Esto también se gestiona automáticamente si utiliza la extensión de etiqueta del SDK web de Adobe Experience Platform.

>[!NOTE]
>
>Los datos que se pueden enviar en cada evento del campo XDM tienen un límite de 32 kB.


## Envío de datos que no sean XDM

Los datos que no coinciden con un esquema XDM deben enviarse utilizando la opción `data` del comando `sendEvent`. Esta función es compatible con las versiones 2.5.0 y posteriores del SDK web.

Esto resulta útil si necesita actualizar un perfil de Adobe Target o enviar atributos de Recommendations de Target. [Obtenga más información sobre estas funciones de Target.](../personalization/adobe-target/target-overview.md#single-profile-update)

En el futuro, podrá enviar toda la capa de datos en la opción `data` y asignarla al servidor XDM.

**Envío de atributos de perfil y Recommendations a Adobe Target:**

```javascript
alloy("sendEvent", {
  data: {
    __adobe: {
      target: {
        "profile.gender": "female",
        "profile.age": 30,
        "entity.id" : "123",
        "entity.genre" : "Drama"
      }
    }
  }
});
```


### Configuración `eventType` {#event-types}

En un evento de experiencia XDM, hay un campo opcional `eventType`. Contiene el tipo de evento principal del registro. La configuración de un tipo de evento puede ayudarle a diferenciar entre los diferentes eventos que va a enviar. XDM proporciona varios tipos de eventos predefinidos que puede usar o crear siempre sus propios tipos de eventos personalizados para sus casos de uso. A continuación se muestra una lista de todos los tipos de eventos predefinidos proporcionados por XDM. [Obtenga más información en el repositorio público XDM](https://github.com/adobe/xdm/blob/master/docs/reference/behaviors/time-series.schema.md#xdmeventtype-known-values).


| **Tipo de evento:** | **Definición:** |
| ---------------------------------- | ------------ |
| advertising.completes | Indica si se ha visto hasta el final un recurso de medios temporizados, lo que no significa necesariamente que el usuario haya visto todo el vídeo; el visor podría haber omitido |
| advertising.timePlayed | Describe la cantidad de tiempo que un usuario emplea en un recurso de medios temporizados específico |
| advertising.federated | Indica si se creó un evento de experiencia mediante una federación de datos (uso compartido de datos entre clientes) |
| advertising.clicks | Acciones de clic en un anuncio |
| advertising.conversions | Una acción o acciones predefinidas por el cliente que déclencheur un evento para la evaluación del rendimiento |
| advertising.firstQuartiles | Un anuncio de vídeo digital se ha reproducido a una velocidad normal del 25% de su duración |
| advertising.impressions | Impresión o impresiones de un anuncio a un usuario final con el potencial de ser visto |
| advertising.midpoints | Un anuncio de vídeo digital se ha reproducido a una velocidad normal durante el 50% de su duración |
| advertising.starts | Se ha empezado a reproducir un anuncio de vídeo digital |
| advertising.thirdQuartiles | Un anuncio de vídeo digital se ha reproducido a la velocidad normal durante el 75% de su duración |
| web.webpagedetails.pageViews | Se han producido vistas de una página web |
| web.webinteraction.linkClicks | Se ha hecho clic en un vínculo web |
| commerce.checkouts | Una acción durante un proceso de cierre de compra de una lista de productos, puede haber más de un evento de cierre de compra si hay varios pasos en un proceso de cierre de compra. Si hay varios pasos, la información de tiempo del evento y la página o experiencia a las que se hace referencia se utilizan para identificar el paso que representan los eventos individuales |
| commerce.productListAdds | Adición de un producto a la lista de productos. Ejemplo de un producto agregado a un carro de compras |
| commerce.productListOpens | Inicializaciones de una nueva lista de productos. Ejemplo de creación de un carro de compras |
| commerce.productListRemovals | Eliminación de una entrada de producto de una lista de productos. Ejemplo en el que se elimina un producto de un carro de compras |
| commerce.productListReopens | El usuario ha reactivado una lista de productos que ya no era accesible (abandonada). Ejemplo a través de una actividad de remarketing |
| commerce.productListViews | Se han producido vistas de una lista de productos |
| commerce.productViews | Se han producido vistas de un producto |
| commerce.purchases | Se ha aceptado una solicitud. La compra es la única acción requerida en una conversión de comercio. La compra debe tener una lista de productos referenciada |
| commerce.saveForLaters | La lista de productos se guarda para su uso futuro. Ejemplo de lista de deseos de producto |
| delivery.feedback | Eventos de comentarios de una entrega. Ejemplos de eventos de comentarios de un envío de correo electrónico |


Estos tipos de eventos se mostrarán en un menú desplegable si utiliza la extensión de etiqueta o siempre puede pasarlos sin etiquetas. Se pueden pasar como parte de la opción `xdm`.


```javascript
alloy("sendEvent", {
  "xdm": {
    "eventType": "commerce.purchases",
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

Alternativamente, el `eventType` se puede pasar al comando event usando la opción `type`. En segundo plano, esto se añade a los datos XDM. Tener el `type` como opción le permite configurar el `eventType` con mayor facilidad sin tener que modificar la carga útil XDM.


```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.purchases"
});
```

### Anulación del ID del conjunto de datos

En algunos casos de uso, es posible que desee enviar un evento a un conjunto de datos que no sea el configurado en la interfaz de usuario de configuración. Para ello, debe configurar la opción `datasetId` en el comando `sendEvent`:


```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.checkout",
  "datasetId": "YOUR_DATASET_ID"
});
```

### Adición de información de identidad

La información de identidad personalizada también se puede agregar al evento. Consulte [Recuperación del ID de Experience Cloud](../identity/overview.md).

## Uso de la API sendBeacon

Puede ser complicado enviar datos de evento justo antes de que el usuario de la página web haya navegado fuera. Si la solicitud tarda demasiado, el explorador puede cancelar la solicitud. Algunos exploradores han implementado una API estándar web llamada `sendBeacon` para permitir que los datos se recopilen más fácilmente durante este tiempo. Al utilizar `sendBeacon`, el explorador realiza la solicitud web en el contexto de navegación global. Esto significa que el explorador realiza la solicitud de señalización en segundo plano y no mantiene presionada la navegación de la página. Para indicar a Adobe Experience Platform [!DNL Web SDK] que utilice `sendBeacon`, añada la opción `"documentUnloading": true` al comando event.  Vea el siguiente ejemplo:


```javascript
alloy("sendEvent", {
  "documentUnloading": true,
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

Los navegadores han impuesto límites a la cantidad de datos que se pueden enviar con `sendBeacon` al mismo tiempo. En muchos navegadores, el límite es de 64 K. Si el explorador rechaza el evento porque la carga útil es demasiado grande, Adobe Experience Platform [!DNL Web SDK] vuelve a utilizar su método de transporte normal (por ejemplo, recuperación).

## Gestión de respuestas de eventos

Si desea gestionar una respuesta de un evento, se le puede notificar un éxito o error de la siguiente manera:


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
}).then(function(results) {
    // Tracking the event succeeded.
  })
  .catch(function(error) {
    // Tracking the event failed.
  });
```

## Modificación global de eventos {#modifying-events-globally}

Si desea agregar, quitar o modificar campos del evento globalmente, puede configurar una llamada de retorno `onBeforeEventSend`.  Esta llamada de retorno se llama cada vez que se envía un evento.  Esta llamada de retorno se pasa en un objeto de evento con un campo `xdm`.  Modifique `content.xdm` para cambiar los datos que se envían con el evento.


```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeEventSend": function(content) {
    // Change existing values
    content.xdm.web.webPageDetails.URL = xdm.web.webPageDetails.URL.toLowerCase();
    // Remove existing values
    delete content.xdm.web.webReferrer.URL;
    // Or add new values
    content.xdm._adb3lettersandnumbers.mycustomkey = "value";
  }
});
```

`xdm` los campos se definen en este orden:

1. Valores pasados como opciones al comando de evento `alloy("sendEvent", { xdm: ... });`
2. Valores recopilados automáticamente.  (Consulte [Información automática](../data-collection/automatic-information.md)).
3. Los cambios realizados en la llamada de retorno `onBeforeEventSend`.

Algunas notas de la llamada de retorno `onBeforeEventSend`:

* Event XDM se puede modificar durante la rellamada. Una vez devuelta la llamada de retorno, los campos y valores modificados de
los objetos content.xdm y content.data se envían con el evento .

   ```javascript
   onBeforeEventSend: function(content){
     //sets a query parameter in XDM
     const queryString = window.location.search;
     const urlParams = new URLSearchParams(queryString);
     content.xdm.marketing.trackingCode = urlParams.get('cid')
   }
   ```

* Si la rellamada genera una excepción, el procesamiento del evento se interrumpe y no se envía el evento.
* Si la rellamada devuelve el valor booleano `false`, el procesamiento de eventos interrumpe.
sin error y el evento no se envía. Este mecanismo permite que ciertos eventos se ignoren fácilmente en
examinar los datos del evento y devolver `false` si no se debe enviar el evento.

   >[!NOTE]
   >Se debe tener cuidado de evitar devolver false en el primer evento de una página. Devolver el valor false en el primer evento puede afectar negativamente a la personalización.

```javascript
   onBeforeEventSend: function(content) {
     // ignores events from bots
     if (MyBotDetector.isABot()) {
       return false;
     }
   }
```

Cualquier valor devuelto que no sea el booleano `false` permitirá que el evento se procese y envíe después de la llamada de retorno.

* Los eventos se pueden filtrar examinando el tipo de evento (consulte [Tipos de eventos](#event-types)):

```javascript
    onBeforeEventSend: function(content) {  
      // augments XDM if link click event is to a partner website
      if (
        content.xdm.eventType === "web.webinteraction.linkClicks" &&
        content.xdm.web.webInteraction.URL ===
          "http://example.com/partner-page.html"
      ) {
        content.xdm.partnerWebsiteClick = true;
      }
   }
```

## Posibles errores procesables

Al enviar un evento, se puede generar un error si los datos que se envían son demasiado grandes (más de 32 KB para la solicitud completa). En este caso, debe reducir la cantidad de datos que se envían.
