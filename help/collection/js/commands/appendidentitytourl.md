---
title: appendIdentityToUrl
description: Ofrezca experiencias personalizadas con mayor precisión entre aplicaciones, sitios web y dominios cruzados.
exl-id: 09dd03bd-66d8-4d53-bda8-84fc4caadea6
source-git-commit: c2564f1b9ff036a49c9fa4b9e9ffbdbc598a07a8
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# `appendIdentityToUrl`

El comando `appendIdentityToUrl` le permite agregar un identificador de usuario a la dirección URL como una cadena de consulta. Esta acción le permite transferir la identidad de un visitante entre dominios, lo que evita recuentos de visitantes duplicados para conjuntos de datos que incluyen dominios o canales. Está disponible en las versiones 2.11.0 o posteriores de Web SDK.

La cadena de consulta generada y anexada a la dirección URL es `adobe_mc`. Si Web SDK no encuentra un ECID, llama al extremo `/acquire` para generar uno.

>[!NOTE]
>
>Si no se ha proporcionado el consentimiento, la dirección URL de este método se devuelve sin cambios. Este comando se ejecuta inmediatamente; no espera una actualización de consentimiento.

Ejecute el comando `appendIdentityToUrl` con una dirección URL como parámetro. El método devuelve una dirección URL con el identificador anexado como cadena de consulta.

```js
alloy("appendIdentityToUrl",
  {
    url: document.location.href
  }
);
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
  alloy("appendIdentityToUrl", {url: anchor.href}).then(result => { window.open(result.url, anchor.target || "_self"); });
});
```

Este comando admite el objeto [`edgeConfigOverrides`](configure/edgeconfigoverrides.md).

## Objeto Response

Cuando [administra respuestas](command-responses.md) con este comando, el objeto de respuesta contiene **`url`**, la nueva dirección URL con información de identidad agregada como parámetro de cadena de consulta.

## Anexar la identidad a la URL mediante la extensión de etiquetas Web SDK

La extensión de etiquetas Web SDK equivalente a este comando es la acción [Redirigir con identidad](/help/tags/extensions/client/web-sdk/actions/redirect-with-identity.md).
