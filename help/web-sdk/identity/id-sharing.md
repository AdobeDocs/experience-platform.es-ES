---
title: Uso compartido de ID de móviles a web y entre dominios
description: Obtenga información sobre cómo mantener los ID de visitante de propiedades móviles a web y entre dominios
keywords: identidad;móvil;id;compartir;dominio;entre dominios;sdk;plataforma;
exl-id: b9bb236f-52cf-4615-96d8-1137d957de8c
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# Uso compartido de ID de móviles a web y entre dominios

## Información general

El SDK web de Adobe Experience Platform admite funciones de uso compartido de ID de visitante que permiten a los clientes ofrecer experiencias personalizadas de forma más precisa, entre aplicaciones móviles y contenido web móvil, así como entre dominios.

## Casos de uso {#use-cases}

### Ofrezca una personalización coherente entre las aplicaciones móviles y los sitios web móviles

Una compañía de ropa quiere personalizar la experiencia de sus clientes en función de sus intereses y mantener la personalización precisa en una aplicación móvil que también cargue WebViews. Al utilizar la función de uso compartido de ID de móvil a web, se pueden asegurar de que se presenten las ofertas más precisas a los clientes, utilizando el mismo identificador de visitante en la aplicación y el contenido de la web móvil pasando [!DNL ECID] a la URL de la web móvil.

### Ofrezca una personalización coherente entre dominios

Un minorista con varias tiendas en línea quiere personalizar la experiencia del comprador en sus dominios según los intereses de los clientes. Con la función de uso compartido de ID entre dominios del SDK web, el minorista puede ofrecer ofertas precisas basadas en los intereses de los clientes en todos sus dominios.

### Mejore los informes de actividad del visitante

Un minorista de tecnología quiere mejorar sus informes de actividad de visitantes con información sobre cuándo sus visitantes pasan de la aplicación móvil al sitio web móvil o a sus otros dominios. Con la función de uso compartido de ID entre dominios del SDK web, el equipo de marketing puede realizar un seguimiento preciso de los visitantes en sus propiedades web y generar informes de actividad.

## Requisitos previos {#prerequisites}

Para usar el uso compartido de ID de móviles a web y entre dominios, debe usar [!DNL Web SDK] versión 2.11.0 o posterior.

Para implementaciones móviles de Edge Network, esta característica es compatible con la extensión [Identity for Edge Network](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/) a partir de la versión 1.1.0 (iOS y Android).

Esta característica también es compatible con [!DNL VisitorAPI.js] versión 1.7.0 o posterior.

## Uso compartido de ID de móvil a web {#mobile-to-web}

Utilice la API `getUrlVariables` de la extensión [Identity for Edge Network](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#geturlvariables) para recuperar los identificadores como parámetros de consulta y adjuntarlos a la dirección URL al abrir [!DNL webViews].

No se requiere ninguna configuración adicional para que el SDK web acepte `ECID` valores en la cadena de consulta.

El parámetro de cadena de consulta incluye:

* `MCID`: Id. de Experience Cloud (`ECID`)
* `MCORGID`: el Experience Cloud `orgID` que debe coincidir con el `orgID` configurado en el [!DNL Web SDK].
* `TS`: parámetro de marca de tiempo que no puede ser anterior a cinco minutos.


El uso compartido de ID de móvil a web usa el parámetro `adobe_mc`. Cuando el parámetro `adobe_mc` está presente y es válido, el elemento `ECID` de la cadena de consulta se agrega automáticamente al mapa de identidad en la primera solicitud realizada al Edge Network. Todas las interacciones de Edge Network subsiguientes utilizarán ese(a) `ECID`.

Para obtener más información sobre cómo pasar ID de visitantes de una aplicación móvil a un WebView, consulte la documentación sobre [administración de WebViews](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/app-implementation/web-views.html?lang=es#implementation).

## Implementación del uso compartido de ID entre dominios {#cross-domain-sharing}

Consulte el comando [`appendIdentityToUrl`](../commands/appendidentitytourl.md) para obtener instrucciones de implementación mediante la extensión de etiquetas del SDK web y la biblioteca de JavaScript del SDK web.
