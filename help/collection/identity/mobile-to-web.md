---
title: Compartir la identidad de aplicaciones móviles en web/WebViews móviles
description: Pase la identidad de una aplicación móvil al contenido de la web móvil o a un WebView para que la creación de informes y la personalización puedan continuar en el contexto web.
source-git-commit: bf0bb72777cacd822fd6e887ac3ef71764784214
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 0%

---

# Compartir la identidad de aplicaciones móviles en web/WebViews móviles

Cuando un visitante pasa de una aplicación móvil a una página web WebView o móvil, la aplicación y los contextos web mantienen cada uno su propia identidad. Sin un traspaso explícito, la experiencia web trata al visitante como una persona nueva y desconocida, lo que fragmenta el sistema de informes y reinicia la personalización.

El uso compartido de identidades de móvil a web soluciona esto al pasar el [Experience Cloud ID (ECID)](./overview.md) del visitante de la aplicación móvil al destino web mediante un parámetro de cadena de consulta `adobe_mc`. El parámetro lleva el ECID, el ID de organización de Experience Cloud y una marca de tiempo. Cuando el destino web se carga con un parámetro `adobe_mc` válido, Web SDK lo lee automáticamente y aplica la identidad entregada en su primera solicitud de Edge Network, de modo que ambos contextos comparten el mismo visitante.

Utilice este patrón cuando su aplicación móvil abra una página web WebView o móvil que su organización controle y cuando desee que la actividad de la aplicación y la actividad web permanezcan vinculadas al mismo visitante. Si su objetivo es la continuidad de identidad entre sitios web de dominios diferentes, use [uso compartido entre dominios](cross-domain-sharing.md) en su lugar.

## Requisitos previos

Antes de empezar, asegúrese de que la implementación cumple los siguientes requisitos:

* **Aplicación móvil**: Adobe Experience Platform Mobile SDK con la extensión [Identity for Edge Network](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/) versión **1.1.0 o posterior** (iOS y Android).
* **Destino web**: la versión [Web SDK](/help/collection/js/js-overview.md) **2.11.0 o posterior**, o la extensión de etiquetas Web SDK.
* **Control de URL**: Su código controla la dirección URL que la aplicación pasa al explorador o al WebView para que pueda agregarle parámetros de cadena de consulta.
* **Configuración coincidente**: el mismo ID de organización de Experience Cloud se ha configurado en las implementaciones web y móvil.

## Recuperar identidad de la aplicación móvil {#retrieve-identity}

Utilice la API [`getUrlVariables`](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/api-reference/#geturlvariables) de la extensión Identity for Edge Network para recuperar la identidad del visitante como cadena de consulta. A continuación, puede anexar esa cadena a la dirección URL antes de abrir WebView o el explorador.

La cadena devuelta contiene los siguientes parámetros con codificación URL:

| Parámetro | Descripción |
| --- | --- |
| `MCID` | El Experience Cloud ID (ECID). |
| `MCORGID` | Su ID de organización de Experience Cloud. Este parámetro debe coincidir con la organización configurada en Web SDK en la página de destino. |
| `TS` | Una marca de tiempo. El destino debe recibir este valor en **cinco minutos** o se rechazará el traspaso. |

Los siguientes ejemplos de código muestran el aspecto que podría tener un envío en su aplicación móvil:

>[!BEGINTABS]

>[!TAB Swift (iOS)]

```swift
Identity.getUrlVariables { (urlVariables, error) in
    if let error = error {
        // Handle the error
        return
    }

    guard let urlVariables = urlVariables else { return }

    // Construct the full URL by appending the identity query string
    if let url = URL(string: "https://example.com/webapp?\(urlVariables)") {
        // Open the URL in a WebView or browser
        let request = URLRequest(url: url)
        webView.load(request)
    }
}
```

>[!TAB Kotlin (Android)]

```kotlin
Identity.getUrlVariables { urlVariables ->
    if (urlVariables != null) {
        // Construct the full URL by appending the identity query string
        val url = "https://example.com/webapp?$urlVariables"

        // Open the URL in a WebView or browser
        webView.loadUrl(url)
    }
}
```

>[!ENDTABS]

## Recibir identidad en el lado web {#receive-identity}

No se requiere código adicional en el destino web. Cuando Web SDK está presente en la página y la dirección URL contiene un parámetro `adobe_mc` válido, SDK extrae automáticamente el ECID y lo aplica al mapa de identidad del visitante en la primera solicitud de Edge Network.

Si el destino web usa la extensión de etiquetas Web SDK y necesita redirigir al visitante a otra página preservando al mismo tiempo la identidad, use la acción [Redirigir con identidad](/help/tags/extensions/client/web-sdk/actions/redirect-with-identity.md) para reenviar el parámetro `adobe_mc` a la página siguiente.

>[!NOTE]
>
>El parámetro `adobe_mc` caduca después de **cinco minutos**. Asegúrese de que el destino web se carga y envía su primera solicitud de Edge Network inmediatamente después de abrir la dirección URL.
