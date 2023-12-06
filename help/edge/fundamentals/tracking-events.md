---
title: Seguimiento de eventos mediante el SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo rastrear eventos de SDK web de Adobe Experience Platform.
source-git-commit: 68174928d3b005d1e5a31b17f3f287e475b5dc86
workflow-type: tm+mt
source-wordcount: '1163'
ht-degree: 0%

---


# Seguimiento de eventos

Para enviar datos de evento a Adobe Experience Cloud, utilice el `sendEvent` comando. El `sendEvent` es la forma principal de enviar datos al [!DNL Experience Cloud]y para recuperar contenido personalizado, identidades y destinos de audiencia.

Los datos enviados a Adobe Experience Cloud se dividen en dos categorías:

* Datos XDM
* Datos que no son XDM

## Envío de datos XDM

Los datos XDM son un objeto cuyo contenido y estructura coinciden con un esquema creado en Adobe Experience Platform. [Más información sobre cómo crear un esquema.](../../xdm/tutorials/create-schema-ui.md)

Los datos XDM que desee que formen parte de sus análisis, personalización, audiencias o destinos deben enviarse mediante el `xdm` opción.


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

Puede pasar algún tiempo entre el momento en que `sendEvent` se ejecuta y cuando los datos se envían al servidor (por ejemplo, si la biblioteca del SDK web no se ha cargado completamente o si aún no se ha recibido el consentimiento). Si tiene intención de modificar cualquier parte de `xdm` después de ejecutar el objeto `sendEvent` , es muy recomendable que clone el comando `xdm` objeto _antes_ ejecución del `sendEvent` comando. Por ejemplo:

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

En este ejemplo, la capa de datos se clona serializándola en JSON y luego deserializándola. A continuación, el resultado clonado se pasa al `sendEvent` comando. Al hacerlo, se asegura de que `sendEvent` tiene una instantánea de la capa de datos tal y como existía cuando se ejecutaba el comando `sendEvent` Este comando se ejecutó para que las modificaciones posteriores al objeto de capa de datos original no se reflejen en los datos enviados al servidor. Si utiliza una capa de datos impulsada por evento, es probable que la clonación de datos ya se haya gestionado automáticamente. Por ejemplo, si está utilizando la variable [Capa de datos del cliente de Adobe](https://github.com/adobe/adobe-client-data-layer/wiki), el `getState()` proporciona una instantánea calculada y clonada de todos los cambios anteriores. Esto también se gestiona automáticamente si utiliza la extensión de etiqueta del SDK web de Adobe Experience Platform.

>[!NOTE]
>
>Hay un límite de 32 KB en los datos que se pueden enviar en cada evento del campo XDM.


## Envío de datos que no son XDM

Los datos que no coinciden con un esquema XDM deben enviarse con el `data` de la opción `sendEvent` comando. Esta función se admite en las versiones 2.5.0 y posteriores del SDK web.

Esto resulta útil si debe actualizar un perfil de Adobe Target o enviar atributos de Recommendations de Target. [Obtenga más información sobre estas funciones de Target.](../personalization/adobe-target/target-overview.md#single-profile-update)

En el futuro, podrá enviar toda la capa de datos en `data` y asignarla al lado del servidor XDM.

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

En los esquemas XDM ExperienceEvent, hay un `eventType` field. Contiene el tipo de evento principal del registro. La configuración de un tipo de evento puede ayudarle a diferenciar entre los diferentes eventos que envía. XDM proporciona varios tipos de eventos predefinidos que puede utilizar o que siempre puede crear sus propios tipos de eventos personalizados para sus casos de uso. Consulte la documentación de XDM para ver un [lista de todos los tipos de eventos predefinidos](../../xdm/classes/experienceevent.md#eventType).

Estos tipos de eventos se muestran en un menú desplegable si utiliza la extensión de etiqueta o siempre puede pasarlos sin etiquetas. Se pueden pasar como parte de la variable `xdm` opción.


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

Alternativamente, la variable `eventType` se puede pasar al comando de evento utilizando el `type` opción. En segundo plano, esto se añade a los datos XDM. Tener el `type` como una opción le permite configurar más fácilmente la variable `eventType` sin tener que modificar la carga útil XDM.


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
>El `datasetId` opción admitida por el `sendEvent` El comando estaba obsoleto. Para anular un ID de conjunto de datos, utilice [invalidaciones de configuración](../../datastreams/overrides.md) en su lugar.

En algunos casos de uso, es posible que desee enviar un evento a un conjunto de datos que no sea el configurado en la interfaz de usuario de configuración. Para ello, debe establecer la variable `datasetId` opción en la `sendEvent` comando:



```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.checkout",
  "datasetId": "YOUR_DATASET_ID"
});
```

### Adición de información de identidad

También se puede añadir información de identidad personalizada al evento. Consulte [Recuperando ID de Experience Cloud](../identity/overview.md).

## Uso de la API sendBeacon

Puede ser complicado enviar datos de evento justo antes de que el usuario de la página web haya salido. Si la solicitud tarda demasiado, el explorador puede cancelarla. Algunos exploradores han implementado una API estándar web llamada `sendBeacon` para permitir que los datos se recopilen más fácilmente durante este tiempo. Al utilizar `sendBeacon`, el explorador realiza la solicitud web en el contexto de navegación global. Esto significa que el explorador realiza la solicitud de señalización en segundo plano y no retrasa la navegación de la página. Para informar a Adobe Experience Platform [!DNL Web SDK] para utilizar `sendBeacon`, agregue la opción `"documentUnloading": true` al comando de evento.

**Ejemplo**

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

Los navegadores han impuesto límites a la cantidad de datos que se pueden enviar con `sendBeacon` al mismo tiempo. En muchos exploradores, el límite es de 64 KB. Si el explorador rechaza el evento porque la carga útil es demasiado grande, Adobe Experience Platform [!DNL Web SDK] vuelve a utilizar su método de transporte normal (por ejemplo, fetch).

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


### El `result` objeto

El `sendEvent` El comando devuelve una promesa que se resuelve con una `result` objeto. El `result` contiene las propiedades siguientes:

| Propiedad | Descripción |
|---------|----------|
| `propositions` | Las ofertas de personalización para las que el visitante cumple los requisitos. [Más información sobre las propuestas.](../personalization/rendering-personalization-content.md#manually-rendering-content) |
| `decisions` | Esta propiedad está obsoleta. Utilice `propositions` en su lugar. |
| `destinations` | Audiencias de Adobe Experience Platform que se pueden compartir con plataformas de personalización externas, sistemas de administración de contenido, servidores de publicidad y otras aplicaciones que se ejecutan en sitios web de clientes. [Más información sobre los destinos.](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/custom-personalization.html) |

>[!WARNING]
>
>El `destinations` La propiedad está en versión beta. La documentación y la funcionalidad están sujetas a cambios.

## Modificación de eventos globalmente {#modifying-events-globally}

Si desea agregar, quitar o modificar campos del evento globalmente, puede configurar un `onBeforeEventSend` devolución de llamada. Se llama a esta devolución de llamada cada vez que se envía un evento. Esta llamada de retorno se pasa en un objeto de evento con un `xdm` field. Para cambiar los datos que se envían con el evento, modifique `content.xdm`.


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

`xdm` los campos se establecen en este orden:

1. Valores pasados como opciones al comando de evento `alloy("sendEvent", { xdm: ... });`.
2. Valores recopilados automáticamente. Consulte [Información automática](../data-collection/automatic-information.md).
3. Los cambios realizados en la `onBeforeEventSend` devolución de llamada.

Algunas notas sobre la `onBeforeEventSend` callback:

* El XDM de evento se puede modificar durante la llamada de retorno. Una vez devuelta la llamada de retorno, los campos y valores modificados de los objetos content.xdm y content.data se envían con el evento.

  ```javascript
  onBeforeEventSend: function(content){
    //sets a query parameter in XDM
    const queryString = window.location.search;
    const urlParams = new URLSearchParams(queryString);
    content.xdm.marketing.trackingCode = urlParams.get('cid')
  }
  ```

* Si la llamada de retorno genera una excepción, el procesamiento del evento se interrumpe y el evento no se envía.
* Si la llamada de retorno devuelve el valor booleano de `false`, el procesamiento de eventos se interrumpe sin errores y el evento no se envía. Este mecanismo permite ignorar fácilmente ciertos eventos examinando los datos del evento y devolviendo `false` si el evento no se debe enviar.

  >[!NOTE]
  >Se debe tener cuidado de evitar devolver false en el primer evento de una página. Devolver false en el primer evento puede afectar negativamente a la personalización.

```javascript
   onBeforeEventSend: function(content) {
     // ignores events from bots
     if (MyBotDetector.isABot()) {
       return false;
     }
   }
```

Cualquier valor devuelto que no sea booleano `false` permitirá que el evento se procese y envíe después de la llamada de retorno.

* Los eventos se pueden filtrar examinando el tipo de evento (Consulte [Tipos de eventos](#event-types).):

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

Al enviar un evento, puede producirse un error si los datos enviados son demasiado grandes (más de 32 KB para la solicitud completa). En este caso, debe reducir la cantidad de datos que se envían.
