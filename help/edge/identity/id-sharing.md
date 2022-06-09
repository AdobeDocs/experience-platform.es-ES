---
title: Uso compartido de ID de dominio cruzado y de móvil a web
description: Obtenga información sobre cómo mantener los ID de visitante de las propiedades móviles a las web y entre dominios
keywords: Identidad;móvil;id;uso compartido;dominio;dominio cruzado;sdk;plataforma;
source-git-commit: 55e28f749741c653a230b42fabf5a047ba8c7d01
workflow-type: tm+mt
source-wordcount: '893'
ht-degree: 0%

---


# Uso compartido de ID de dominio cruzado y de móvil a web

## Información general

El SDK web de Adobe Experience Platform admite las funciones de uso compartido de ID de visitante que permiten a los clientes ofrecer experiencias personalizadas con mayor precisión, entre aplicaciones móviles y contenido web móvil, así como entre dominios.

## Casos de uso {#use-cases}

### Ofrecer una personalización coherente entre aplicaciones móviles y sitios web móviles

Una empresa de ropa quiere personalizar la experiencia de sus clientes según sus intereses y mantener la personalización precisa en una aplicación móvil que también carga WebViews. Al utilizar la función de uso compartido de ID de móvil a web, se pueden asegurar de que las ofertas más precisas se presenten a los clientes, utilizando el mismo identificador de visitante en la aplicación y el contenido de la web móvil al pasar la variable [!DNL ECID] a la URL de la web móvil.

### Ofrecer una personalización coherente en todos los dominios

Un minorista con varias tiendas en línea quiere personalizar la experiencia del comprador en sus dominios, según los intereses del cliente. Gracias a la función de uso compartido de ID entre dominios del SDK web, el minorista puede ofrecer ofertas precisas basadas en los intereses de los clientes en todos sus dominios.

### Mejorar los informes de actividad de los visitantes

Un comerciante de tecnología desea mejorar los informes de actividad de los visitantes con información sobre cuándo los visitantes pasan de la aplicación móvil a su sitio web móvil o a sus otros dominios. Con la función de uso compartido de ID entre dominios del SDK web, el equipo de marketing puede realizar un seguimiento exacto de los visitantes en sus propiedades web y generar informes de actividad.

## Requisitos previos {#prerequisites}

Para usar el uso compartido de ID de móviles a la web y entre dominios, debe actualizar a [!DNL Web SDK] versión 2.11.0 o posterior.

Para implementaciones móviles de red perimetral, esta función se admite en la variable [Identidad para la red perimetral](https://aep-sdks.gitbook.io/docs/foundation-extensions/identity-for-edge-network) a partir de la versión 1.1.0 (iOS y Android).

## Uso compartido de ID de Mobile a Web {#mobile-to-web}

Utilice la variable `getUrlVariables` API de [Identidad para la red perimetral](https://aep-sdks.gitbook.io/docs/foundation-extensions/identity-for-edge-network/api-reference#geturlvariables) extensión para recuperar los identificadores como parámetros de consulta y adjuntarlos a la URL al abrir [!DNL webViews].

No se requiere ninguna configuración adicional para que el SDK web acepte `ECID` valores de la cadena de consulta.

El parámetro de cadena de consulta incluye:

* `MCID`: El ID de Experience Cloud (`ECID`)
* `MCORGID`: El Experience Cloud `orgID` que debe coincidir con la variable `orgID` configurado en la variable [!DNL Web SDK].
* `TS`: Parámetro de marca de tiempo que no puede ser anterior a cinco minutos.


El uso compartido de ID de móvil a web utiliza la variable `adobe_mc` parámetro. Cuando la variable `adobe_mc` está presente y es válido, la variable `ECID` de la cadena de consulta se agrega automáticamente al mapa de identidad en la primera solicitud realizada a la red perimetral. Todas las interacciones de red perimetral subsiguientes utilizarán que `ECID`.

Para obtener más información sobre cómo pasar ID de visitantes de una aplicación móvil a WebView, consulte la documentación de [gestión de WebViews](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/app-implementation/web-views.html#implementation).

## Uso compartido de ID entre dominios {#cross-domain-sharing}

Para el uso compartido de ID entre dominios, la versión 2.11.0 del SDK web agrega compatibilidad con el `appendIdentityToUrl` comando. Cuando se utiliza, este comando genera la variable `adobe_mc` parámetro de cadena de consulta.

El comando acepta un objeto con una propiedad, `url`y devuelve un objeto con la propiedad `url`.

Este comando no espera ninguna actualización de consentimiento. Si no se ha dado el consentimiento, la dirección URL se devuelve sin cambios.

Si una `ECID` no se proporciona, la variable `/acquire` se llamará al extremo para generar un `ECID`.

A continuación se muestra un ejemplo de cómo un cliente puede implementar el uso compartido de ID entre dominios en su sitio web.

Este código agrega un detector de eventos para todos los clics en la página y si el clic estaba en un vínculo a un dominio coincidente (en este caso `adobe.com` o `behance.com`), añade la identidad a la dirección URL y redirige al usuario allí.

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

Similar al uso de la variable [!DNL Web SDK], no se requiere ninguna configuración adicional en el [!DNL Tags] para utilizar las identidades pasadas a través de la URL.

Para utilizar el uso compartido de ID de móviles a la web y entre dominios a través de la extensión Etiquetas, debe utilizar la versión 2.12.0 o posterior de la extensión Etiquetas.

Para compartir identidades de la página actual con otros dominios, hay una nueva acción disponible en la variable [!DNL Web SDK] [!DNL Tags] extensión. Esta acción está diseñada para utilizarse con un **[!UICONTROL Core - Haga clic]** tipo de evento y una condición de comparación de valores.

Siga los pasos descritos [here](../../tags/ui/managing-resources/rules.md) para crear una regla con la siguiente configuración:

* [!UICONTROL Configuración de eventos]:
   * **[!UICONTROL Extensión: Core]**
   * **[!UICONTROL Tipo de evento: Haga clic en]**
   * Select **[!UICONTROL Cuando el usuario hace clic en > elementos específicos]**
   * Escriba en la **[!UICONTROL Selector]**: `a[href]`. Este evento se déclencheur cada vez que se haga clic en una etiqueta delimitadora de la página con un `href` propiedad.

      ![Imagen de la interfaz de usuario que muestra la configuración del evento con los ajustes descritos anteriormente](assets/id-sharing-event-configuration.png)

* [!UICONTROL Configuración de condición]
   * **[!UICONTROL Tipo de lógica]**: [!UICONTROL Regular]
   * **[!UICONTROL Extensión]**: [!UICONTROL Principal]
   * **[!UICONTROL Tipo de condición]**: [!UICONTROL Value Comparison]
   * **[!UICONTROL Operador izquierdo]**: [!UICONTROL `%this.hostname%`]. Este es un elemento de datos especial que funciona con [!UICONTROL Core - Haga clic] y responde al nombre de host del vínculo en el que se hizo clic.
   * **[!UICONTROL Operador]**: [!UICONTROL Matches Regex]
   * **[!UICONTROL Operador derecho]**: Escriba una expresión regular que coincida con los dominios con los que desea compartir identidades. Por ejemplo, para buscar coincidencias entre vínculos con nombres de host que terminen con `adobe.com` o `behance.com`, utilice esta expresión regular: `behance.com$|adobe.com$`. La página vinculada debe tener la variable [!DNL Web SDK] o [!DNL Visitor ID] instalado para aceptar la identidad.

      ![Imagen de la interfaz de usuario que muestra la configuración de la condición con los ajustes descritos anteriormente](assets/id-sharing-condition-configuration.png)

* [!UICONTROL Configuración de la acción]
   * **[!UICONTROL Extensión]**: [!UICONTROL SDK web de Adobe Experience Platform]
   * **[!UICONTROL Tipo de acción]**: [!UICONTROL Redireccionar con identidad]
   * **[!UICONTROL Instancia]**: Seleccione la instancia. En la mayoría de los casos, solo se configurará una instancia. Si tiene varias instancias, seleccione la que tenga la identidad que desea compartir.

      ![Imagen de la interfaz de usuario que muestra la configuración de la acción con los ajustes descritos anteriormente](assets/id-sharing-action-configuration.png)

La variable **[!UICONTROL Redireccionar con identidad]** evitará que el explorador navegue hasta el vínculo. A continuación, llamará a la función `appendIdentityToUrl` en el [!DNL Web SDK] instancia.

Finalmente, redirige al usuario al [!DNL URL] con la variable `adobe_mc` parámetro de cadena de consulta anexado.
