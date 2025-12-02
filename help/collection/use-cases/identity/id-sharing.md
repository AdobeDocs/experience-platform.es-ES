---
title: Uso compartido de ID de móviles a web y entre dominios
description: Obtenga información sobre cómo mantener los ID de visitante de propiedades móviles a web y entre dominios
keywords: identidad;móvil;id;compartir;dominio;entre dominios;sdk;plataforma;
exl-id: b9bb236f-52cf-4615-96d8-1137d957de8c
source-git-commit: 217282135bcd750740f4d3f8c6e17a0b8f9578bd
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 0%

---

# Uso compartido de ID de móviles a web y entre dominios

## Información general

Adobe Experience Platform Web SDK admite funciones de uso compartido de ID de visitante que permiten a los clientes ofrecer experiencias personalizadas de forma más precisa, entre aplicaciones móviles y contenido web móvil, así como entre dominios.

## Casos de uso {#use-cases}

### Ofrezca una personalización coherente entre las aplicaciones móviles y los sitios web móviles

Una compañía de ropa quiere personalizar la experiencia de sus clientes en función de sus intereses y mantener la personalización precisa en una aplicación móvil que también cargue WebViews. Al utilizar la función de uso compartido de ID de móvil a web, se pueden asegurar de que se presenten las ofertas más precisas a los clientes, utilizando el mismo identificador de visitante en la aplicación y el contenido de la web móvil pasando [!DNL ECID] a la URL de la web móvil.

### Ofrezca una personalización coherente entre dominios

Una retailer con varias tiendas en línea quiere personalizar la experiencia del comprador en sus dominios según los intereses de los clientes. Con la función de uso compartido de ID entre dominios de Web SDK, retailer puede ofrecer ofertas precisas basadas en los intereses de los clientes en todos sus dominios.

### Mejore los informes de actividad del visitante

Una tecnología con la que retailer desea mejorar sus informes de actividad del visitante con información sobre cuándo sus visitantes pasan de la aplicación móvil al sitio web móvil o a sus otros dominios. Con la función de uso compartido de ID entre dominios de Web SDK, el equipo de marketing puede realizar un seguimiento preciso de los visitantes en sus propiedades web y generar informes de actividad.

## Requisitos previos {#prerequisites}

Para usar el uso compartido de ID de móviles a web y entre dominios, debe usar [!DNL Web SDK] versión 2.11.0 o posterior.

En implementaciones móviles de Edge Network, esta característica es compatible con la extensión [Identity for Edge Network](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/) a partir de la versión 1.1.0 (iOS y Android).

Esta característica también es compatible con [!DNL VisitorAPI.js] versión 1.7.0 o posterior.

## Uso compartido de ID de móvil a web {#mobile-to-web}

Utilice la API `getUrlVariables` de la extensión [Identity for Edge Network](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#geturlvariables) para recuperar los identificadores como parámetros de consulta y adjuntarlos a la dirección URL al abrir [!DNL webViews].

No se requiere ninguna configuración adicional para que Web SDK acepte `ECID` valores en la cadena de consulta.

El parámetro de cadena de consulta incluye:

* `MCID`: Experience Cloud ID (`ECID`)
* `MCORGID`: Experience Cloud `orgID` que debe coincidir con `orgID` configurado en [!DNL Web SDK].
* `TS`: parámetro de marca de tiempo que no puede ser anterior a cinco minutos.


El uso compartido de ID de móvil a web usa el parámetro `adobe_mc`. Cuando el parámetro `adobe_mc` está presente y es válido, el elemento `ECID` de la cadena de consulta se agrega automáticamente al mapa de identidad en la primera solicitud realizada a Edge Network. Todas las interacciones subsiguientes de Edge Network usarán ese(a) `ECID`.

Para obtener más información sobre cómo pasar ID de visitantes de una aplicación móvil a un WebView, consulte la documentación sobre [administración de WebViews](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/app-implementation/web-views.html#implementation).

## Implementación del uso compartido de ID entre dominios {#cross-domain-sharing}

Consulte los siguientes vínculos, según la configuración de Web SDK:

* **Biblioteca JavaScript**: [`appendIdentityToUrl`](../../js/commands/appendidentitytourl.md) comando
* **Extensión de etiqueta**: [Redireccionar con acción de identidad](/help/tags/extensions/client/web-sdk/actions/redirect-with-identity.md)
