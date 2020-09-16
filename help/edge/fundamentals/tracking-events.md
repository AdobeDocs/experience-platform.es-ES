---
title: Eventos de seguimiento
seo-title: Seguimiento de eventos del SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo rastrear los eventos del SDK web Experience Platform
seo-description: Obtenga información sobre cómo rastrear los eventos del SDK web Experience Platform
keywords: sendEvent;xdm;eventType;datasetId;sendBeacon;send Beacon;documentUnloading;document Unloading;onBeforeEventSend;
translation-type: tm+mt
source-git-commit: 69ddfca041624123b03eb01d0f10a5bdb36cd119
workflow-type: tm+mt
source-wordcount: '1116'
ht-degree: 0%

---


# Eventos de seguimiento

Para enviar datos de evento al Adobe Experience Cloud, utilice el `sendEvent` comando . El `sendEvent` comando es la forma principal de enviar datos al [!DNL Experience Cloud]sitio y recuperar contenido personalizado, identidades y destinos de audiencia.

Los datos enviados a Adobe Experience Cloud se dividen en dos categorías:

* Datos XDM
* Datos no XDM (actualmente no compatibles)

## Envío de datos XDM

Los datos XDM son un objeto cuyo contenido y estructura coinciden con un esquema creado en Adobe Experience Platform. [Obtenga más información sobre cómo crear un esquema.](../../xdm/tutorials/create-schema-ui.md)

Los datos XDM que desee que formen parte de sus análisis, personalización, audiencias o destinos deben enviarse mediante la `xdm` opción .


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

>[!NOTE]
>
>Hay un límite de 32 KB en los datos que se pueden enviar en cada evento del campo XDM.

### Envío de datos que no son XDM

Actualmente, no se admite el envío de datos que no coinciden con un esquema XDM. La asistencia técnica está prevista para una fecha futura.

### Configuración `eventType`

En un evento de experiencia XDM, hay un `eventType` campo opcional. Esto contiene el tipo de evento principal del registro. La configuración de un tipo de evento puede ayudarle a diferenciar entre los diferentes eventos que va a enviar. XDM proporciona varios tipos de evento predefinidos que puede utilizar o que siempre crea sus propios tipos de evento personalizados para los casos de uso. A continuación se presenta una lista de todos los tipos de evento predefinidos proporcionados por XDM.


| **Tipo de evento:** | **Definición:** |
| ---------------------------------- | ------------ |
| advertising.completes | Indica si un recurso de medios temporizados se ha visto hasta la finalización; esto no significa necesariamente que el visor haya visto todo el vídeo; el visor podría haber omitido |
| advertising.timePlayed | Describe la cantidad de tiempo que un usuario emplea en un recurso de medios temporizados específico |
| advertising.federated | Indica si se creó un evento de experiencia mediante la federación de datos (uso compartido de datos entre clientes) |
| advertising.clicks | Acciones de clic en un anuncio |
| advertising.conversions | Una acción o acciones predefinidas por el cliente que desencadena un evento para la evaluación del rendimiento |
| advertising.firstQuartiles | Un anuncio de vídeo digital se ha reproducido a una velocidad normal durante el 25 % de su duración |
| advertising.impressions | Impresión(s) de un anuncio a un usuario final con el potencial de ser visto |
| advertising.midpoints | Un anuncio de vídeo digital se ha reproducido a una velocidad normal durante el 50 % de su duración |
| advertising.starts | Se ha empezado a reproducir un anuncio de vídeo digital |
| advertising.thirdQuartiles | Un anuncio de vídeo digital se ha reproducido a una velocidad normal durante el 75 % de su duración |
| web.webpagedetails.pageViews | Vistas de una página web |
| web.webinteraction.linkClicks | Se ha producido un clic en un vínculo web |
| commerce.checkouts | Una acción durante un proceso de cierre de compra de una lista de producto, puede haber más de un evento de cierre de compra si hay varios pasos en un proceso de cierre de compra. Si hay varios pasos, la información de tiempo de evento y la página o experiencia a la que se hace referencia se utilizan para identificar el paso que representan los eventos individuales en orden |
| commerce.productListAdds | Adición de un producto a la lista del producto. Ejemplo de un producto agregado a un carro de compras |
| commerce.productListOpens | Inicializaciones de una nueva lista de producto. Ejemplo de creación de un carro de compras |
| commerce.productListRemovals | Eliminación de una entrada de producto de una lista de producto. Ejemplo de eliminación de un producto de un carro de compras |
| commerce.productListReopens | El usuario ha reactivado una lista de producto que ya no era accesible (abandonada). Ejemplo mediante una actividad de remercadotecnia |
| commerce.productListViews | Vista(s) de una lista de producto |
| commerce.productViews | Se han producido vistas de un producto |
| commerce.purchases | Se ha aceptado una orden. La compra es la única acción requerida en una conversión de comercio. La compra debe tener una lista de producto referenciada |
| commerce.saveForLaters | La lista del producto se guarda para su uso futuro. Ejemplo de una lista de deseo de producto |
| delivery.feedback | Eventos de comentarios para un envío. Ejemplo de eventos de comentarios para un envío de correo electrónico |


Estos tipos de evento se mostrarán en una lista desplegable si utiliza la extensión Launch o si siempre puede pasarlos sin Launch. Se pueden pasar como parte de la `xdm` opción.


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

Como alternativa, el `eventType` se puede pasar al comando evento mediante la `type` opción . En segundo plano, esto se agrega a los datos XDM. Tener la `type` opción como opción le permite establecer el `eventType` sin tener que modificar la carga útil XDM.


```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.purchases"
});
```

### Anulación del ID del conjunto de datos

En algunos casos de uso, es posible que desee enviar un evento a un conjunto de datos que no sea el configurado en la interfaz de usuario de configuración. Para ello, debe definir la `datasetId` opción en el `sendEvent` comando:


```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.checkout",
  "datasetId": "YOUR_DATASET_ID"
});
```

### Añadir información de identidad

La información de identidad personalizada también se puede agregar al evento. Consulte [Recuperación de ID de Experience Cloud](./identity.md)

## Uso de la API sendBeacon

Puede ser complicado enviar datos de evento justo antes de que el usuario haya navegado fuera de la página web. Si la solicitud tarda demasiado, el explorador podría cancelarla. Algunos exploradores han implementado una API estándar web llamada `sendBeacon` para permitir que los datos se recopilen más fácilmente durante este tiempo. Cuando se utiliza `sendBeacon`, el navegador realiza la solicitud web en el contexto de navegación global. Esto significa que el explorador realiza la solicitud de señalización en segundo plano y no mantiene presionada la navegación de la página. Para indicar a Adobe Experience Platform [!DNL Web SDK] que lo utilice `sendBeacon`, agregue la opción `"documentUnloading": true` al comando evento.  Vea el siguiente ejemplo:


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

Los exploradores han impuesto límites a la cantidad de datos que se pueden enviar `sendBeacon` al mismo tiempo. En muchos exploradores, el límite es de 64 K. Si el explorador rechaza el evento porque la carga útil es demasiado grande, Adobe Experience Platform [!DNL Web SDK] vuelve a utilizar su método de transporte normal (por ejemplo, recuperar).

## Gestión de respuestas de eventos

Si desea gestionar una respuesta desde un evento, se le puede notificar un éxito o un error de la siguiente manera:


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

Si desea agregar, quitar o modificar campos del evento de forma global, puede configurar una `onBeforeEventSend` llamada de retorno.  Esta llamada de retorno se llama cada vez que se envía un evento.  Esta llamada de retorno se pasa a un objeto evento con un `xdm` campo.  Modifique `event.xdm` para cambiar los datos que se envían en el evento.


```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeEventSend": function(event) {
    // Change existing values
    event.xdm.web.webPageDetails.URL = xdm.web.webPageDetails.URL.toLowerCase();
    // Remove existing values
    delete event.xdm.web.webReferrer.URL;
    // Or add new values
    event.xdm._adb3lettersandnumbers.mycustomkey = "value";
  }
});
```

`xdm` los campos se definen en este orden:

1. Valores pasados como opciones al comando evento `alloy("sendEvent", { xdm: ... });`
2. Valores recopilados automáticamente.  (Consulte Información [](../reference/automatic-information.md)automática).
3. Los cambios realizados en la `onBeforeEventSend` llamada de retorno.

Si la `onBeforeEventSend` llamada de retorno emite una excepción, se seguirá enviando el evento; sin embargo, ninguno de los cambios realizados dentro de la llamada de retorno se aplica al evento final.

## Posibles errores procesables

Al enviar un evento, se puede generar un error si los datos que se envían son demasiado grandes (más de 32 KB para la solicitud completa). En este caso, debe reducir la cantidad de datos que se envían.

Cuando la depuración está habilitada, el servidor valida sincrónicamente los datos de evento que se envían con el esquema XDM configurado. Si los datos no coinciden con el esquema, el servidor devuelve los detalles sobre la discrepancia y se genera un error. En este caso, modifique los datos para que coincidan con el esquema. Cuando la depuración no está habilitada, el servidor valida los datos asincrónicamente y, por lo tanto, no se genera ningún error correspondiente.
