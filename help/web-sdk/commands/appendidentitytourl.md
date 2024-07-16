---
title: appendIdentityToUrl
description: Ofrezca experiencias personalizadas con mayor precisión entre aplicaciones, sitios web y dominios cruzados.
exl-id: 09dd03bd-66d8-4d53-bda8-84fc4caadea6
source-git-commit: 153c5bae42c027c25a38a8b63070249d1b1a8f01
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---

# `appendIdentityToUrl`

El comando `appendIdentityToUrl` le permite agregar un identificador de usuario a la dirección URL como una cadena de consulta. Esta acción le permite transferir la identidad de un visitante entre dominios, lo que evita recuentos de visitantes duplicados para conjuntos de datos que incluyen dominios o canales. Está disponible en las versiones 2.11.0 o posteriores del SDK web.

La cadena de consulta generada y anexada a la dirección URL es `adobe_mc`. Si el SDK web no encuentra un ECID, llama al extremo `/acquire` para generar uno.

>[!NOTE]
>
>Si no se ha proporcionado el consentimiento, la dirección URL de este método se devuelve sin cambios. Este comando se ejecuta inmediatamente; no espera una actualización de consentimiento.

## Anexar identidad a una URL mediante la extensión del SDK web {#extension}

La adición de una identidad a una dirección URL se realiza como una acción dentro de una regla de la interfaz de etiquetas de recopilación de datos de Adobe Experience Platform.

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Reglas]** y luego seleccione la regla que desee.
1. En [!UICONTROL Acciones], seleccione una acción existente o cree una acción.
1. Establezca el campo desplegable [!UICONTROL Extension] en **[!UICONTROL SDK web de Adobe Experience Platform]** y establezca [!UICONTROL Action Type] en **[!UICONTROL Redirect with identity]**.
1. Haga clic en **[!UICONTROL Conservar cambios]** y, a continuación, ejecute el flujo de trabajo de publicación.

Este comando suele utilizarse con una regla específica que escucha clics y comprueba los dominios deseados.

+++Criterios de evento de regla

Déclencheur cuando se hace clic en una etiqueta delimitadora con una propiedad `href`.

* **[!UICONTROL Extensión]**: Principal
* **[!UICONTROL Tipo de evento]**: haga clic en
* **[!UICONTROL Cuando el usuario hace clic en]**: Elementos específicos
* **[!UICONTROL Elementos que coinciden con el selector de CSS]**: `a[href]`

![Evento de regla](../assets/id-sharing-event-configuration.png)

+++

+++Condición de regla

Déclencheur solo en los dominios deseados.

* **[!UICONTROL Tipo de lógica]**: Normal
* **[!UICONTROL Extensión]**: Principal
* **[!UICONTROL Tipo de condición]**: Comparación de valor
* **[!UICONTROL Operando Izquierdo]**: `%this.hostname%`
* **[!UICONTROL Operador]**: coincide con la expresión regular
* **[!UICONTROL Operando derecho]**: Una expresión regular que coincide con los dominios deseados. Por ejemplo, `adobe.com$|behance.com$`

![Condición de regla](../assets/id-sharing-condition-configuration.png)

+++

+++Acción de regla

Anexe la identidad a la dirección URL.

* **[!UICONTROL Extensión]**: SDK web de Adobe Experience Platform
* **[!UICONTROL Tipo de acción]**: redireccionar con identidad

![Acción de regla](../assets/id-sharing-action-configuration.png)

+++

## Anexar la identidad a una URL mediante la biblioteca JavaScript del SDK web

Ejecute el comando `appendIdentityToUrl` con una dirección URL como parámetro. El método devuelve una dirección URL con el identificador anexado como cadena de consulta.

```js
alloy("appendIdentityToUrl",document.location);
```

Puede agregar un detector de eventos para todos los clics recibidos en la página y comprobar si la dirección URL coincide con algún dominio deseado. En caso afirmativo, anexe la identidad a la dirección URL y redirija al usuario.

```js
document.addEventListener("click", event => {
  // Check if the click was a link
  const anchor = event.target.closest("a");
  if (!anchor || !anchor.href) return;

  // Check if the link points to the desired domain
  const url = new URL(anchor.href);
  if (!url.hostname.endsWith(".adobe.com") && !url.hostname.endsWith(".behance.com")) return;

  // Append the identity to the URL, then direct the user to the URL
  event.preventDefault();
  alloy("appendIdentityToUrl", {url: anchor.href}).then(result => {document.location = result.url;});
});
```

## Objeto Response

Si decide [controlar las respuestas](command-responses.md) con este comando, el objeto response contiene **`url`**, la nueva dirección URL con información de identidad agregada como parámetro de cadena de consulta.
