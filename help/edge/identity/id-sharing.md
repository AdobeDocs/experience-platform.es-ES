---
title: Uso compartido de ID de móviles a web y entre dominios
description: Obtenga información sobre cómo mantener los ID de visitante de propiedades móviles a web y entre dominios
keywords: identidad;móvil;id;compartir;dominio;entre dominios;sdk;plataforma;
exl-id: b9bb236f-52cf-4615-96d8-1137d957de8c
source-git-commit: 3b65143e33804b251f888dbe2a69d238b3f4cda3
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 1%

---

# Uso compartido de ID de móviles a web y entre dominios

## Información general

El SDK web de Adobe Experience Platform admite funciones de uso compartido de ID de visitante que permiten a los clientes ofrecer experiencias personalizadas de forma más precisa, entre aplicaciones móviles y contenido web móvil, así como entre dominios.

## Casos de uso {#use-cases}

### Ofrezca una personalización coherente entre las aplicaciones móviles y los sitios web móviles

Una compañía de ropa quiere personalizar la experiencia de sus clientes en función de sus intereses y mantener la personalización precisa en una aplicación móvil que también cargue WebViews. Al utilizar la función de uso compartido de ID de móvil a web, se pueden asegurar de que se presenten las ofertas más precisas a los clientes, utilizando el mismo identificador de visitante en la aplicación y el contenido de la web móvil, al pasar el valor de [!DNL ECID] a la URL de la web móvil.

### Ofrezca una personalización coherente entre dominios

Un minorista con varias tiendas en línea quiere personalizar la experiencia del comprador en sus dominios según los intereses de los clientes. Con la función de uso compartido de ID entre dominios del SDK web, el minorista puede ofrecer ofertas precisas basadas en los intereses de los clientes en todos sus dominios.

### Mejore los informes de actividad del visitante

Un minorista de tecnología quiere mejorar sus informes de actividad de visitantes con información sobre cuándo sus visitantes pasan de la aplicación móvil al sitio web móvil o a sus otros dominios. Con la función de uso compartido de ID entre dominios del SDK web, el equipo de marketing puede realizar un seguimiento preciso de los visitantes en sus propiedades web y generar informes de actividad.

## Requisitos previos {#prerequisites}

Para utilizar el uso compartido de ID de móviles a web y entre dominios, debe utilizar [!DNL Web SDK] versión 2.11.0 o posterior.

Para implementaciones móviles de Edge Network, esta función es compatible con [Identidad para la red perimetral](https://aep-sdks.gitbook.io/docs/foundation-extensions/identity-for-edge-network) extensión a partir de la versión 1.1.0 (iOS y Android).

Esta función también es compatible con [!DNL VisitorAPI.js] versión 1.7.0 o posterior de.

## Uso compartido de ID de móvil a web {#mobile-to-web}

Utilice el `getUrlVariables` API de desde [Identidad para la red perimetral](https://aep-sdks.gitbook.io/docs/foundation-extensions/identity-for-edge-network/api-reference#geturlvariables) para recuperar los identificadores como parámetros de consulta y adjuntarlos a la URL al abrir [!DNL webViews].

No se requiere ninguna configuración adicional para que el SDK web acepte `ECID` valores en la cadena de consulta.

El parámetro de cadena de consulta incluye:

* `MCID`: El ID del Experience Cloud (`ECID`)
* `MCORGID`: el Experience Cloud `orgID` que debe coincidir con el `orgID` configurado en la [!DNL Web SDK].
* `TS`: parámetro de marca de tiempo que no puede ser anterior a cinco minutos.


El uso compartido de ID de móvil a web utiliza `adobe_mc` parámetro. Si la variable `adobe_mc` el parámetro está presente y es válido, el parámetro `ECID` de la cadena de consulta se agrega automáticamente al mapa de identidad en la primera solicitud realizada a Edge Network. Todas las interacciones de red perimetral subsiguientes utilizarán eso `ECID`.

Para obtener más información sobre cómo pasar los ID de visitante de una aplicación móvil a un WebView, consulte la documentación sobre [administrar WebViews](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/app-implementation/web-views.html#implementation).

## Uso compartido de ID entre dominios {#cross-domain-sharing}

Para el uso compartido de ID entre dominios, la versión 2.11.0 del SDK web agrega compatibilidad con `appendIdentityToUrl` comando. Cuando se utiliza, este comando genera el `adobe_mc` parámetro de cadena de consulta.

El comando acepta un objeto con una propiedad, `url`y devuelve un objeto con la propiedad `url`.

Este comando no espera ninguna actualización de consentimiento. Si no se ha proporcionado el consentimiento, la dirección URL se devuelve sin cambios.

Si un `ECID` no se proporciona, la variable `/acquire` se llamará al extremo para generar un `ECID`.

A continuación se muestra un ejemplo de cómo un cliente puede implementar el uso compartido de ID entre dominios en su sitio web.

Este código añade un detector de eventos para todos los clics en la página y si el clic estaba en un vínculo a un dominio coincidente (en este caso `adobe.com` o `behance.com`), añade la identidad a la dirección URL y redirige al usuario allí.

```js
document.addEventListener("click", event => {
  const anchor = event.target.closest("a");
  if (!anchor || !anchor.href) {
    return;
  }
  const url = new URL(anchor.href);
  if (!url.hostname.endsWith("adobe.com") && !url.hostname.endsWith("behance.com")) {
    return;
  }
  event.preventDefault();
  alloy("appendIdentityToUrl", { url: anchor.href }).then(result => {
    document.location = result.url;
  });
});
```

## Uso de la extensión Etiquetas {#tags-extension}

Similar al uso de [!DNL Web SDK], no se requiere ninguna configuración adicional en el [!DNL Tags] para utilizar identidades pasadas a través de la dirección URL.

Para utilizar el uso compartido de ID de móviles a web y entre dominios a través de la extensión de etiquetas, debe utilizar la versión 2.12.0 o posterior de la extensión de etiquetas.

Para compartir identidades de la página actual con otros dominios, hay una nueva acción disponible en [!DNL Web SDK] [!DNL Tags] extensión. Esta acción está diseñada para utilizarse con un **[!UICONTROL Núcleo: clic]** tipo de evento y una condición de comparación de valores.

Siga los pasos descritos [aquí](../../tags/ui/managing-resources/rules.md) para crear una regla con la configuración siguiente:

* [!UICONTROL Configuración de eventos]:
   * **[!UICONTROL Extensión: Core]**
   * **[!UICONTROL Tipo de evento: clic]**
   * Seleccionar **[!UICONTROL Cuando el usuario haga clic en > Elementos específicos]**
   * Escriba en **[!UICONTROL Selector]**: `a[href]`. Este evento entrará en déclencheur cada vez que se haga clic en una etiqueta delimitadora de la página con un `href` propiedad.

      ![Imagen de la interfaz de usuario que muestra la configuración del evento con la configuración descrita anteriormente](assets/id-sharing-event-configuration.png)

* [!UICONTROL Configuración de condición]
   * **[!UICONTROL Tipo de lógica]**: [!UICONTROL Normal]
   * **[!UICONTROL Extensión]**: [!UICONTROL Núcleo]
   * **[!UICONTROL Tipo de condición]**: [!UICONTROL Value Comparison]
   * **[!UICONTROL Operando izquierdo]**: [!UICONTROL `%this.hostname%`]. Este es un elemento de datos especial que funciona con [!UICONTROL Núcleo: clic] y se resuelve en el nombre de host del vínculo en el que se hizo clic.
   * **[!UICONTROL Operador]**: [!UICONTROL Matches Regex]
   * **[!UICONTROL Operando derecho]**: escriba una expresión regular que coincida con los dominios con los que desea compartir identidades. Por ejemplo, para hacer coincidir vínculos con nombres de host que terminen por `adobe.com` o `behance.com`, utilice esta expresión regular: `behance.com$|adobe.com$`. La página vinculada debe tener [!DNL Web SDK] o [!DNL Visitor ID] instalado para aceptar la identidad.

      ![Imagen de la interfaz de usuario que muestra la configuración de la condición con la configuración descrita anteriormente](assets/id-sharing-condition-configuration.png)

* [!UICONTROL Configuración de la acción]
   * **[!UICONTROL Extensión]**: [!UICONTROL SDK web de Adobe Experience Platform]
   * **[!UICONTROL Tipo de acción]**: [!UICONTROL Redirigir con identidad]
   * **[!UICONTROL Instancia]**: Seleccione la instancia. En la mayoría de los casos, solo tendrá configurada una instancia. Si tiene varias instancias, seleccione la que tenga la identidad que desee compartir.

      ![Imagen de la interfaz de usuario que muestra la configuración de la acción con la configuración descrita anteriormente](assets/id-sharing-action-configuration.png)

El **[!UICONTROL Redirigir con identidad]** Esta acción impedirá que el explorador navegue hasta el vínculo. A continuación, llamará al `appendIdentityToUrl` en el [!DNL Web SDK] ejemplo.

Finalmente, redirige al usuario a [!DNL URL] con el `adobe_mc` parámetro de cadena de consulta anexado.
