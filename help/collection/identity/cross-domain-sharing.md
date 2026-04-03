---
title: Compartir la identidad entre dominios
description: Mantenga la continuidad de identidad entre los dominios de su organización para mejorar la personalización y la creación de informes.
source-git-commit: bf0bb72777cacd822fd6e887ac3ef71764784214
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# Compartir la identidad entre dominios

Cuando los visitantes se desplazan entre los dominios de su organización, cada dominio mantiene su propia identidad de visitante de forma predeterminada. Sin un traspaso explícito, un visitante que hace clic de uno de sus dominios a otro se trata como una persona nueva y desconocida en el sitio de destino. Este tipo de implementación fragmenta la creación de informes y reinicia la personalización.

El uso compartido de identidades entre dominios resuelve este problema adjuntando un parámetro de cadena de consulta `adobe_mc` a la dirección URL de destino cuando un visitante hace clic en un vínculo o es redirigido. Este parámetro contiene la [Experience Cloud ID (ECID)](./overview.md) del visitante, su ID de organización y una marca de tiempo. Cuando la página de destino se carga con un parámetro `adobe_mc` válido, Web SDK lo lee automáticamente y aplica la identidad entregada en su primera solicitud de Edge Network, de modo que ambos dominios comparten el mismo visitante. El parámetro `adobe_mc` caduca a los cinco minutos, por lo que la página de destino debe cargarse inmediatamente después de la redirección.

Este caso de uso abarca el uso compartido de identidades entre sitios web de diferentes dominios. Si desea pasar la identidad de una aplicación móvil a una página web móvil o WebView, use [uso compartido de identidad de móvil a web](./mobile-to-web.md).

## Requisitos previos

Antes de empezar, asegúrese de que la implementación cumple los siguientes requisitos:

* **Web SDK**: [Web SDK](/help/collection/js/js-overview.md) versión **2.11.0 o posterior**, o la extensión de etiquetas Web SDK, está instalada tanto en el dominio de origen como en el de destino.
* **Configuración coincidente**: Todos los dominios participantes utilizan el mismo [`orgId`](../js/commands/configure/orgid.md) al configurar Web SDK.
* **Control de URL**: tu código controla los vínculos o redirecciones entre dominios para que puedas anexar parámetros de cadena de consulta a la URL de destino.

## Implementación del uso compartido entre dominios

Debe configurar el uso compartido de identidades en todos los dominios que actúen como origen en un traspaso entre dominios. Si los visitantes pueden navegar en ambas direcciones entre dos dominios, configure ambos dominios como fuentes.

>[!BEGINTABS]

>[!TAB Biblioteca de JavaScript]

Utilice el comando [`appendIdentityToUrl`](/help/collection/js/commands/appendidentitytourl.md) para anexar el parámetro `adobe_mc` a los vínculos de salida. El siguiente ejemplo escucha clics en elementos de anclaje y anexa la identidad a cualquier vínculo que apunte a un dominio deseado:

```js
document.addEventListener("click", event => {
  // Check if the click was a link
  const anchor = event.target.closest("a");
  if (!anchor || !anchor.href) return;

  // Check if the link points to a domain you want to share identity with
  const url = new URL(anchor.href);
  if (!url.hostname.endsWith(".example.com") && !url.hostname.endsWith(".example.org")) return;

  // Append the identity to the URL, then navigate
  event.preventDefault();
  alloy("appendIdentityToUrl", { url: anchor.href }).then(result => {
    window.open(result.url, anchor.target || "_self");
  });
});
```

>[!TAB Extensión de etiqueta Web SDK]

Utilice la acción [**[!UICONTROL Redirect with identity]**](/help/tags/extensions/client/web-sdk/actions/redirect-with-identity.md) para anexar el parámetro `adobe_mc` a los vínculos de salida. Puede crear una regla con las siguientes condiciones para lograr el comportamiento deseado:

1. **Evento**: establezca la extensión en **[!UICONTROL Core]** y el tipo de evento en **[!UICONTROL Click]**. En **[!UICONTROL Elements matching the CSS selector]**, escriba `a[href]`.
2. **Condición**: establezca la extensión en **[!UICONTROL Core]** y el tipo de condición en **[!UICONTROL Value Comparison]**. Establezca **[!UICONTROL Left Operand]** en `%this.hostname%`, **[!UICONTROL Operator]** en **[!UICONTROL Matches Regex]** y **[!UICONTROL Right Operand]** en una expresión regular que coincida con sus dominios de destino (por ejemplo, `example\.com$|example\.org$`).
3. **Acción**: establezca la extensión en **[!UICONTROL Adobe Experience Platform Web SDK]** y el tipo de acción en **[!UICONTROL Redirect with identity]**.

>[!ENDTABS]

## Identidad de recepción en el dominio de destino

No se requiere código adicional en el dominio de destino. Cuando Web SDK está presente en la página y la dirección URL contiene un parámetro `adobe_mc` válido, SDK extrae automáticamente el ECID y lo aplica al mapa de identidad del visitante en su primera solicitud Edge Network.

Asegúrese de que el dominio de destino cumpla las siguientes condiciones:

* La extensión de etiquetas Web SDK o Web SDK se instala y configura con el mismo [`orgId`](../js/commands/configure/orgid.md) que el dominio de origen. Puede usar la biblioteca JavaScript y la extensión de etiquetas Web SDK de forma intercambiable entre dominios, siempre que compartan el mismo(a) `orgId`.
* La página carga y envía su primera solicitud de Edge Network en los **cinco minutos** posteriores a la redirección, antes de que caduque el parámetro `adobe_mc`.
