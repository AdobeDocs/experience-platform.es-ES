---
title: Ajustes de configuración de recopilación de datos
description: Configure las opciones de recopilación de datos en la extensión de etiquetas Web SDK.
source-git-commit: 46c8748e9ab972705b8283c174c285e571acb2ed
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 0%

---

# Ajustes de configuración de recopilación de datos

Esta sección de configuración le permite determinar cómo se recopilan los datos en la extensión.

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensions]** y, a continuación, seleccione **[!UICONTROL Configure]** en la tarjeta [!UICONTROL Adobe Experience Platform Web SDK].
1. Vaya a la sección **[!UICONTROL Data collection]**.

![Imagen que muestra la configuración de recopilación de datos de la extensión de etiquetas Web SDK en la interfaz de usuario de etiquetas.](../assets/web-sdk-ext-collection.png)

Las opciones disponibles son las siguientes:

## [!UICONTROL On before event send callback]

Una función de llamada de retorno para evaluar y modificar la carga útil enviada a Adobe. En el editor de código, tiene acceso a las siguientes variables:

* **`content.xdm`**: la carga útil XDM para el evento.
* **`content.data`**: la carga del objeto de datos para el evento.
* **`return true`**: salga inmediatamente de la llamada de retorno y envíe datos a Adobe con los valores actuales en el objeto `content`.
* **`return false`**: salga inmediatamente de la llamada de retorno y anule el envío de datos a Adobe.

Se puede usar cualquier variable definida fuera de `content`, pero no se incluye en la carga útil enviada a Adobe.

>[!WARNING]
>
>Esta llamada de retorno permite el uso de código personalizado. Si algún código que incluya en la llamada de retorno genera una excepción no detectada, se detendrá el procesamiento del evento. **No se han enviado los datos a Adobe.**

```js
// Use nullish coalescing assignments to add objects if they don't yet exist
content.xdm.commerce ??= {};
content.xdm.commerce.order ??= {};

// Then add the purchase ID
content.xdm.commerce.order.purchaseID = "12345";

// Use optional chaining to prevent undefined errors when setting tracking code to lower case
if(content.xdm.marketing?.trackingCode) content.xdm.marketing.trackingCode = content.xdm.marketing.trackingCode.toLowerCase();

// Delete operating system version
if(content.xdm.environment) delete content.xdm.environment.operatingSystemVersion;

// Immediately end onBeforeEventSend logic and send the data to Adobe for this event type
if (content.xdm.eventType === "web.webInteraction.linkClicks") {
  return true;
}

// Cancel sending data if it is a known bot
if (myBotDetector.isABot()) {
  return false;
}
```

>[!TIP]
>Evite devolver `false` en el primer evento de una página. Devolver `false` en el primer evento puede afectar negativamente a la personalización.

Esta llamada de retorno es la etiqueta equivalente a [`onBeforeEventSend`](/help/collection/js/commands/configure/onbeforeeventsend.md) en la biblioteca de JavaScript.

## [!UICONTROL Collect internal link clicks]

Casilla de verificación que permite recopilar datos de seguimiento de vínculos internos del sitio o de la propiedad. Esta casilla de verificación equivale a [`clickCollection.internalLinkEnabled`](/help/collection/js/commands/configure/clickcollection.md) en la biblioteca de JavaScript. Al activar esta casilla de verificación, aparecen las opciones de agrupación de eventos:

* **[!UICONTROL No event grouping]**: los datos de seguimiento de vínculos se envían a Adobe en eventos independientes. Los clics en vínculos enviados en eventos independientes pueden aumentar el uso contractual de los datos enviados a Adobe Experience Platform.
* **[!UICONTROL Event grouping using session storage]**: almacena los datos de seguimiento de vínculos en el almacenamiento de la sesión hasta el siguiente evento de &quot;vista de página&quot;. En el siguiente evento que se considere una &quot;vista de página&quot;, los datos de seguimiento de vínculos almacenados se combinan con la carga útil del evento de &quot;vista de página&quot;. Adobe recomienda habilitar esta configuración al realizar el seguimiento de vínculos internos.
* **[!UICONTROL Event grouping using local object]**: almacena los datos de seguimiento de vínculos en un objeto local hasta el siguiente evento de &quot;vista de página&quot;. Si un visitante navega a una nueva página del explorador, se pierden los datos de seguimiento de vínculos. Esta configuración es más beneficiosa en el contexto de aplicaciones de una sola página.

La biblioteca de etiquetas considera un evento determinado como una &quot;vista de página&quot; cuando los siguientes elementos están incluidos en la carga útil:

* `xdm.web.webPageDetails.name` contiene un valor de cadena
* `xdm.web.webPageDetails.pageViews.value` es mayor que `0`

## [!UICONTROL Collect external link clicks]

Casilla de verificación que habilita la recopilación de vínculos externos. Esta casilla de verificación equivale a [`clickCollection.externalLinkEnabled`](/help/collection/js/commands/configure/clickcollection.md) en la biblioteca de JavaScript.

## [!UICONTROL Collect download link clicks]

Casilla de verificación que habilita la colección de vínculos de descarga. Esta casilla de verificación equivale a [`clickCollection.downloadLinkEnabled`](/help/collection/js/commands/configure/clickcollection.md) en la biblioteca de JavaScript.

## [!UICONTROL Download link qualifier]

Expresión regular que califica una dirección URL de vínculo como vínculo de descarga. Esta cadena es la etiqueta equivalente a [`downloadLinkQualifier`](/help/collection/js/commands/configure/downloadlinkqualifier.md) en la biblioteca de JavaScript.

## [!UICONTROL Filter click properties]

Una función de llamada de retorno para evaluar y modificar las propiedades relacionadas con los clics antes de la colección. Esta función se ejecuta antes que [!UICONTROL On before event send callback] y es la etiqueta equivalente a [`clickCollection.filterClickDetails`](/help/collection/js/commands/configure/clickcollection.md) en la biblioteca de JavaScript. En el editor de código, tiene acceso a las siguientes variables:

* **`content.clickedElement`**: el elemento DOM donde se hizo clic.
* **`content.pageName`**: nombre de página cuando se produjo el clic.
* **`content.linkName`**: nombre del vínculo donde se hizo clic.
* **`content.linkRegion`**: región del vínculo donde se hizo clic.
* **`content.linkType`**: tipo de vínculo (de salida, de descarga, etc.).
* **`content.linkURL`**: dirección URL de destino del vínculo donde se hizo clic.
* **`return true`**: salga inmediatamente de la llamada de retorno con los valores de las variables actuales.
* **`return false`**: salga inmediatamente de la llamada de retorno y anule la recopilación de datos.
* Se puede usar cualquier variable definida fuera de `content`, pero no se incluye en la carga útil enviada a Adobe.

>[!TIP]
>
>El campo **[!UICONTROL On before link click send]** es una llamada de retorno obsoleta que solo está visible para las propiedades que ya lo tienen configurado. Es la etiqueta equivalente a [`onBeforeLinkClickSend`](/help/collection/js/commands/configure/onbeforelinkclicksend.md) en la biblioteca de JavaScript. Use la llamada de retorno **[!UICONTROL Filter click properties]** para filtrar o ajustar los datos de clics, o use **[!UICONTROL On before event send callback]** para filtrar o ajustar la carga útil general enviada a Adobe. Si se establecen tanto la devolución de llamada **[!UICONTROL Filter click properties]** como la devolución de llamada **[!UICONTROL On before link click send]**, solo se ejecutará la devolución de llamada **[!UICONTROL Filter click properties]**.

## Configuración de contexto

Recopile automáticamente información del visitante, que rellena automáticamente campos XDM específicos. Puede elegir **[!UICONTROL All default context information]** o **[!UICONTROL Specific context information]**. Es la etiqueta equivalente a [`context`](/help/collection/js/commands/configure/context.md) en la biblioteca de JavaScript.

* **[!UICONTROL Web]**: recopila información sobre la página actual.
* **[!UICONTROL Device]**: recopila información sobre el dispositivo del usuario.
* **[!UICONTROL Environment]**: recopila información acerca del explorador del usuario.
* **[!UICONTROL Place context]**: recopila información sobre la ubicación del usuario.
* **[!UICONTROL High entropy user-agent hints]**: recopila información más detallada acerca del dispositivo del usuario.
