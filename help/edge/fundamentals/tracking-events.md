---
title: eventos de seguimiento
seo-title: Seguimiento de los eventos del SDK web de la plataforma Adobe Experience Platform
description: Obtenga información sobre cómo rastrear los eventos del SDK web de la plataforma de experiencia
seo-description: Obtenga información sobre cómo rastrear los eventos del SDK web de la plataforma de experiencia
translation-type: tm+mt
source-git-commit: 3c6f9663ef5b83ceeb93539171017e2b282a613f

---


# eventos de seguimiento

>[!IMPORTANT]
>
>El SDK web de la plataforma de experiencia de Adobe se encuentra en fase beta y no está disponible para todos los usuarios. La documentación y las funciones están sujetas a cambios.

Para enviar datos de evento a Adobe Experience Cloud, utilice el `event` comando. El `event` comando es la forma principal de enviar datos a Experience Cloud y recuperar contenido personalizado, identidades y destinos de audiencia.

Los datos enviados a Adobe Experience Cloud se dividen en dos categorías:

* Datos XDM
* Datos no XDM (actualmente no compatibles)

## Envío de datos XDM

Los datos XDM son un objeto cuyo contenido y estructura coinciden con un esquema creado en Adobe Experience Platform. [Obtenga más información sobre cómo crear un esquema.](../../xdm/tutorials/create-schema-ui.md)

Los datos XDM que desee incluir en el análisis, la personalización, las audiencias o los destinos deben enviarse mediante la `xdm` opción .

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
});
```

>[!Note]
>Hay un límite de 32 KB en los datos que se pueden enviar en cada evento del campo XDM.

### Envío de datos que no son XDM

Actualmente, no se admite el envío de datos que no coinciden con un esquema XDM. La asistencia técnica está prevista para una fecha futura.

### Configuración `eventType`

En un evento de experiencia XDM, hay un `eventType` campo. Esto contiene el tipo de evento principal del registro. Esto se puede pasar como parte de la `xdm` opción.

```javascript
alloy("event", {
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

alloy("event", {
  "xdm": myXDMData,
  "type": "commerce.purchases"
});
```

### Inicio de una vista

Cuando se inicie una vista, es importante notificar al SDK estableciendo `viewStart` en `true` el comando `event` . Esto indica, entre otras cosas, que el SDK debe recuperar y procesar contenido personalizado. Aunque no utilice la personalización en este momento, simplifica en gran medida la activación de la personalización u otras funciones más adelante, ya que no será necesario modificar el código en la página. Además, el seguimiento de vistas resulta útil cuando se ven informes de análisis después de recopilar los datos.

La definición de una vista puede depender del contexto.

* En un sitio web normal, cada página web suele considerarse una vista única. En este caso, un evento con `viewStart` configurado para `true` se debe ejecutar lo antes posible en la parte superior de la página.
* En una aplicación de una sola página \(SPA\), una vista está menos definida. Normalmente significa que el usuario ha navegado dentro de la aplicación y que la mayor parte del contenido ha cambiado. Para aquellos familiarizados con los fundamentos técnicos de las aplicaciones de una sola página, esto suele suceder cuando la aplicación carga una nueva ruta. Siempre que un usuario se desplaza a una nueva vista, sin importar cómo decida definir una _vista_, se debe ejecutar un evento con `viewStart` el estado configurado en `true` .

El evento con `viewStart` el valor `true` es el mecanismo principal para enviar datos a Adobe Experience Cloud y solicitar contenido de Adobe Experience Cloud. Así es como inicio una vista:

```javascript
alloy("event", {
  "viewStart": true,
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

Después de enviar los datos, el servidor responde con contenido personalizado, entre otras cosas. Este contenido personalizado se procesa automáticamente en la vista. Los controladores de vínculos también se adjuntan automáticamente al contenido de la nueva vista.

## Uso de la API sendBeacon

Puede ser complicado enviar datos de evento justo antes de que el usuario haya navegado fuera de la página web. Si la solicitud tarda demasiado, el explorador podría cancelarla. Algunos exploradores han implementado una API estándar web llamada `sendBeacon` para permitir que los datos se recopilen más fácilmente durante este tiempo. Cuando se utiliza `sendBeacon`, el navegador realiza la solicitud web en el contexto de navegación global. Esto significa que el explorador realiza la solicitud de señalización en segundo plano y no mantiene presionada la navegación de la página. Para indicar a Adobe Experience Platform Web SDK que utilice `sendBeacon`, agregue la opción `"documentUnloading": true` al comando evento.  Vea el siguiente ejemplo:

```javascript
alloy("event", {
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

Los exploradores han impuesto límites a la cantidad de datos que se pueden enviar `sendBeacon` al mismo tiempo. En muchos exploradores, el límite es de 64 K. Si el navegador rechaza el evento porque la carga útil es demasiado grande, el SDK web de la plataforma Adobe Experience Platform vuelve a utilizar su método de transporte normal (por ejemplo, la búsqueda).

## Gestión de respuestas de eventos

Si desea gestionar una respuesta desde un evento, se le puede notificar un éxito o un error de la siguiente manera:

```javascript
alloy("event", {
  "viewStart": true,
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
}).then(function() {
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
  "configId": "ebebf826-a01f-4458-8cec-ef61de241c93",
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

1. Valores pasados como opciones al comando evento `alloy("event", { xdm: ... });`
2. Valores recopilados automáticamente.  (Consulte Información [](../reference/automatic-information.md)automática).
3. Los cambios realizados en la `onBeforeEventSend` llamada de retorno.

Si la `onBeforeEventSend` llamada de retorno emite una excepción, se seguirá enviando el evento; sin embargo, ninguno de los cambios realizados dentro de la llamada de retorno se aplica al evento final.

## Posibles errores procesables

Al enviar un evento, se puede generar un error si los datos que se envían son demasiado grandes (más de 32 KB para la solicitud completa). En este caso, debe reducir la cantidad de datos que se envían.

Cuando la depuración está habilitada, el servidor valida sincrónicamente los datos de evento que se envían con el esquema XDM configurado. Si los datos no coinciden con el esquema, el servidor devuelve los detalles sobre la discrepancia y se genera un error. En este caso, modifique los datos para que coincidan con el esquema. Cuando la depuración no está habilitada, el servidor valida los datos asincrónicamente y, por lo tanto, no se genera ningún error correspondiente.
