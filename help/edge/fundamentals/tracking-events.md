---
title: Seguimiento de eventos con el SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo rastrear eventos del SDK web de Adobe Experience Platform.
keywords: sendEvent;xdm;eventType;datasetId;sendBeacon;enviar señalización;documentUnloading;descarga de documento;onBeforeEventSend;
exl-id: 8b221cae-3490-44cb-af06-85be4f8d280a
source-git-commit: a6948e3744aa754eda22831a7e68b847eb904e76
workflow-type: tm+mt
source-wordcount: '1194'
ht-degree: 1%

---

# Seguimiento de eventos

Para enviar datos de evento a Adobe Experience Cloud, use el `sendEvent` comando. La variable `sendEvent` es la forma principal de enviar datos a la variable [!DNL Experience Cloud]y para recuperar contenido personalizado, identidades y destinos de audiencia.

Los datos enviados a Adobe Experience Cloud se dividen en dos categorías:

* Datos XDM
* Datos no XDM

## Envío de datos XDM

Los datos XDM son un objeto cuyo contenido y estructura coinciden con un esquema creado en Adobe Experience Platform. [Obtenga más información sobre cómo crear un esquema.](../../xdm/tutorials/create-schema-ui.md)

Los datos XDM que desee que formen parte de sus análisis, personalización, audiencias o destinos se deben enviar mediante la variable `xdm` .


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

Puede que transcurra un tiempo entre el momento en que se define la variable `sendEvent` se ejecuta y cuando los datos se envían al servidor (por ejemplo, si la biblioteca del SDK web no se ha cargado completamente o aún no se ha recibido el consentimiento). Si tiene intención de modificar cualquier parte de la variable `xdm` después de ejecutar el `sendEvent` es muy recomendable que clone el `xdm` object _before_ ejecución del `sendEvent` comando. Por ejemplo:

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

En este ejemplo, la capa de datos se clona serializándola en JSON y luego deserializándola. A continuación, el resultado clonado se pasa al `sendEvent` comando. Al hacerlo, se garantiza que la variable `sendEvent` tiene una instantánea de la capa de datos tal como existía cuando se utilizaba la variable `sendEvent` se ejecutó para que las modificaciones posteriores en el objeto de capa de datos original no se reflejen en los datos enviados al servidor. Si utiliza una capa de datos impulsada por eventos, es probable que la clonación de los datos ya se haya gestionado automáticamente. Por ejemplo, si está utilizando la variable [Capa de datos del cliente de Adobe](https://github.com/adobe/adobe-client-data-layer/wiki), el `getState()` proporciona una instantánea calculada y clonada de todos los cambios anteriores. Esto también se gestiona automáticamente si utiliza la extensión de etiqueta del SDK web de Adobe Experience Platform.

>[!NOTE]
>
>Los datos que se pueden enviar en cada evento del campo XDM tienen un límite de 32 kB.


## Envío de datos que no sean XDM

Los datos que no coinciden con un esquema XDM deben enviarse utilizando la variable `data` de `sendEvent` comando. Esta función es compatible con las versiones 2.5.0 y posteriores del SDK web.

Esto resulta útil si necesita actualizar un perfil de Adobe Target o enviar atributos de Recommendations de Target. [Obtenga más información sobre estas funciones de Target.](../personalization/adobe-target/target-overview.md#single-profile-update)

En el futuro, podrá enviar la capa de datos completa debajo de la `data` y asígnelo al servidor XDM.

**Envío de atributos de perfil y Recommendations a Adobe Target:**

```javascript
alloy("sendEvent", {
  data: {
    __adobe: {
      target: {
        "profile.gender": "female",
        "profile.age": 30,
        "entity.id": "123",
        "entity.genre": "Drama"
      }
    }
  }
});
```


### Configuración `eventType` {#event-types}

En los esquemas XDM ExperienceEvent, hay una `eventType` campo . Contiene el tipo de evento principal del registro. La configuración de un tipo de evento puede ayudarle a diferenciar entre los diferentes eventos que va a enviar. XDM proporciona varios tipos de eventos predefinidos que puede usar o crear siempre sus propios tipos de eventos personalizados para sus casos de uso. Consulte la documentación de XDM para obtener una [lista de todos los tipos de eventos predefinidos](../../xdm/classes/experienceevent.md#eventType).

Estos tipos de eventos se mostrarán en un menú desplegable si utiliza la extensión de etiqueta o siempre puede pasarlos sin etiquetas. Se pueden pasar como parte del `xdm` .


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

Alternativamente, la variable `eventType` se puede pasar al comando event usando la variable `type` . En segundo plano, esto se añade a los datos XDM. Tener `type` como una opción le permite configurar la variable `eventType` sin tener que modificar la carga útil XDM.


```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.purchases"
});
```

### Anulación del ID del conjunto de datos

>[!IMPORTANT]
>
>La variable `datasetId` que admite la opción `sendEvent` está en desuso. Para anular un ID de conjunto de datos, utilice [anulaciones de configuración](../datastreams/overrides.md) en su lugar.

En algunos casos de uso, es posible que desee enviar un evento a un conjunto de datos que no sea el configurado en la interfaz de usuario de configuración. Para ello, debe configurar la variable `datasetId` en la `sendEvent` comando:



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

Puede ser complicado enviar datos de evento justo antes de que el usuario de la página web haya navegado fuera. Si la solicitud tarda demasiado, el explorador puede cancelar la solicitud. Algunos exploradores han implementado una API estándar web llamada `sendBeacon` para permitir que los datos se recopilen más fácilmente durante este tiempo. Al usar `sendBeacon`, el navegador realiza la solicitud web en el contexto de navegación global. Esto significa que el explorador realiza la solicitud de señalización en segundo plano y no mantiene presionada la navegación de la página. Para decirle a Adobe Experience Platform [!DNL Web SDK] para usar `sendBeacon`, añada la opción `"documentUnloading": true` al comando event.  Vea el siguiente ejemplo:


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

Los navegadores han impuesto límites a la cantidad de datos que se pueden enviar con `sendBeacon` a la vez. En muchos navegadores, el límite es de 64 K. Si el explorador rechaza el evento porque la carga útil es demasiado grande, Adobe Experience Platform [!DNL Web SDK] vuelve a utilizar su método de transporte normal (por ejemplo, fetch).

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
}).then(function(result) {
    // Tracking the event succeeded.
  })
  .catch(function(error) {
    // Tracking the event failed.
  });
```


### La variable `result` object

La variable `sendEvent` devuelve una promesa que se resuelve con un `result` objeto. La variable `result` contiene las siguientes propiedades:

**propuestas**: Ofertas de personalización para las que el visitante se ha clasificado. [Obtenga más información sobre las propuestas.](../personalization/rendering-personalization-content.md#manually-rendering-content)

**decisiones**: Esta propiedad está en desuso. Utilice `propositions` en su lugar.

**destinos**: Segmentos de Adobe Experience Platform que se pueden compartir con plataformas de personalización externas, sistemas de administración de contenido, servidores de publicidad y otras aplicaciones que se ejecutan en sitios web de clientes. [Obtenga más información sobre los destinos.](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/custom-personalization.html?lang=en)

>[!WARNING]
>
>`destinations` está actualmente en versión beta. La documentación y la funcionalidad están sujetas a cambios.

## Modificación global de eventos {#modifying-events-globally}

Si desea agregar, quitar o modificar campos del evento globalmente, puede configurar un `onBeforeEventSend` llamada de retorno.  Esta llamada de retorno se llama cada vez que se envía un evento.  Esta llamada de retorno se pasa en un objeto de evento con un `xdm` campo .  Modificar `content.xdm` para cambiar los datos que se envían con el evento.


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

1. Valores transferidos como opciones al comando de evento `alloy("sendEvent", { xdm: ... });`
2. Valores recopilados automáticamente.  (Consulte [Información automática](../data-collection/automatic-information.md).)
3. Los cambios realizados en la variable `onBeforeEventSend` llamada de retorno.

Algunas notas sobre la `onBeforeEventSend` llamada de retorno:

* Event XDM se puede modificar durante la rellamada. Una vez devuelta la llamada de retorno, los campos y valores modificados de los objetos content.xdm y content.data se envían con el evento .

   ```javascript
   onBeforeEventSend: function(content){
     //sets a query parameter in XDM
     const queryString = window.location.search;
     const urlParams = new URLSearchParams(queryString);
     content.xdm.marketing.trackingCode = urlParams.get('cid')
   }
   ```

* Si la rellamada genera una excepción, el procesamiento del evento se interrumpe y no se envía el evento.
* Si la llamada de retorno devuelve el valor booleano de `false`, el procesamiento de eventos se interrumpe, sin error, y el evento no se envía. Este mecanismo permite ignorar ciertos eventos fácilmente examinando los datos del evento y devolviendo `false` si no se debe enviar el evento.

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

* Los eventos se pueden filtrar examinando el tipo de evento (consulte [Tipos de eventos](#event-types).):

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
