---
title: Variables de Adobe Analytics asignadas automáticamente en el SDK web de Adobe Experience Platform
description: Aprenda qué variables se asignan automáticamente en Adobe Analytics con el SDK web de Experience Platform
seo-description: Descubra qué variables se asignan automáticamente en Adobe Analytics con el SDK web de Adobe Experience Platform
keywords: adobe analytics;variables;analytics;asignación automática;asignación automática;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '681'
ht-degree: 0%

---


# Variables asignadas automáticamente en [!DNL Analytics]

A continuación se muestra una lista de variables que Adobe Experience Platform Edge Network asigna automáticamente a Adobe Analytics.

| Ruta de campo XDM | [!DNL Analytics Query String] / Encabezado HTTP | Descripción |
| ---------- | ------------------------- | ----------------------------------------- |
| `application.id` | `c.a.appid` | Asignación de datos de contexto de AppMeasurement `c.a.appid`. |
| `application.launches.value` | `c.a.launches` | Asignación de datos de contexto de AppMeasurement `c.a.launches`. |
| `commerce.checkouts.id` | `events` | `scCheckout` serialización de eventos. Si se excluye este campo (es decir, para eventos sin serializar), el sistema genera y asigna su propio valor de ID a la entidad. |
| `commerce.checkouts.value` | `events` | Asignación del parámetro de consulta de AppMeasurement EVENTO_LISTA_FULL con conversion COMMERCE_SC_CHECKOUT, utilizando el delimitador `,`. |
| `commerce.order.currencyCode` | `cc` | Asignación de CURRENCY, parámetro de consulta de AppMeasurement. |
| `commerce.order.purchaseID` | `pi` | Asignación del parámetro de consulta de AppMeasurement PURCHASEID. |
| `commerce.productListAdds.id` | `events` | `scAdd` serialización de eventos. Si se excluye este campo (es decir, para eventos sin serializar), el sistema genera y asigna su propio valor de ID a la entidad. |
| `commerce.productListAdds.value` | `events` | Asignación del parámetro de consulta de AppMeasurement EVENTO_LISTA_FULL con conversion COMMERCE_SC_AÑADA, utilizando el delimitador `,`. |
| `commerce.productListOpens.id` | `events` | `scOpen` serialización de eventos. Si se excluye este campo (es decir, para eventos sin serializar), el sistema genera y asigna su propio valor de ID a la entidad. |
| `commerce.productListOpens.value` | `events` | Asignación del parámetro de consulta de AppMeasurement EVENTO_LISTA_FULL con conversion COMMERCE_SC_OPEN, utilizando el delimitador `,`. |
| `commerce.productListRemovals.id` | `events` | `scRemove` serialización de eventos. Si se excluye este campo (es decir, para eventos sin serializar), el sistema genera y asigna su propio valor de ID a la entidad. |
| `commerce.productListRemovals.value` | `events` | Asignación del parámetro de consulta de AppMeasurement EVENTO_LISTA_FULL con conversion COMMERCE_SC_REMOVE, utilizando el delimitador `,`. |
| `commerce.productListViews.id` | `events` | `scView` serialización de eventos. Si se excluye este campo (es decir, para eventos sin serializar), el sistema genera y asigna su propio valor de ID a la entidad. |
| `commerce.productListViews.value` | `events` | Asignación del parámetro de consulta de AppMeasurement EVENTO_LISTA_FULL con la VISTA COMMERCE_SC_, utilizando el delimitador `,`. |
| `commerce.productViews.id` | `events` | `prodView` serialización de eventos. Si se excluye este campo (es decir, para eventos sin serializar), el sistema genera y asigna su propio valor de ID a la entidad. |
| `commerce.productViews.value` | `events` | Asignación del parámetro de consulta de AppMeasurement EVENTO_LISTA_FULL con la VISTA COMMERCE_PROD_, mediante el uso del delimitador `,`. |
| `commerce.purchases.value` | `events` | Asignación del parámetro de consulta de AppMeasurement EVENTO_LISTA_FULL con conversion COMMERCE_PURCHASE, utilizando el delimitador `,`. |
| `device.colorDepth` | `c` | Asignación del parámetro de consulta de AppMeasurement C_COLOR. |
| `device.screenHeight` | `s` | Parámetro de consulta de AppMeasurement Asignación de resolución de pantalla. |
| `device.screenWidth` | `s` | Parámetro de consulta de AppMeasurement Asignación de resolución de pantalla. |
| `environment.browserDetails.acceptLanguage` | `Accept-Language` | Es una asignación de encabezado HTTP, HEADER_ACCEPT_LANGUAGE. |
| `environment.browserDetails.cookiesEnabled` | `k` | Asignación COOKIES del parámetro de consulta de AppMeasurement con la conversión BOOLEAN_TO_YN. |
| `environment.browserDetails.javaEnabled` | `v` | Asignación del parámetro de consulta de AppMeasurement JAVA_ENABLED con BOOLEAN_TO_YN de conversión. |
| `environment.browserDetails.javaScriptVersion` | `j` | Asignación del parámetro de consulta AppMeasurement J_JSCRIPT. |
| `environment.browserDetails.userAgent` | `User-Agent` | Es una asignación de encabezado HTTP, HEADER_USER_AGENT. |
| `environment.browserDetails.viewportHeight` | `bh` | Asignación del parámetro de consulta de AppMeasurement para BROWSER_HEIGHT. |
| `environment.browserDetails.viewportWidth` | `bw` | Asignación del parámetro de consulta de AppMeasurement para BROWSER_WIDTH. |
| `environment.connectionType` | `ct` | Asignación del parámetro de consulta AppMeasurement CT_CONNECT_TYPE. |
| `environment.ipV4` | `X-Forwarded-For` | Es una asignación de encabezado HTTP, X-FORWARDED-FOR. |
| `identityMap.ECID.[0].id` | `mid` | Asignación MID del parámetro de consulta de AppMeasurement. |
| `marketing.trackingCode` | `v0` | Asignación de CAMPAÑA de parámetros de consulta de AppMeasurement. |
| `media.mediaTimed.completes.value` | `c.a.media.complete` | Datos de contexto de AppMeasurement. |
| `media.mediaTimed.dropBeforeStart.value` | `c.a.media.view`, `c.a.media.timePlayed`, `c.a.media.play` | Datos de contexto de AppMeasurement. |
| `media.mediaTimed.federated.value` | `c.a.media.federated` | Asignación de datos de contexto de AppMeasurement `c.a.media.federated`. |
| `media.mediaTimed.firstQuartiles.value` | `c.a.media.progress25` | Datos de contexto de AppMeasurement. |
| `media.mediaTimed.mediaSegmentView.value` | `c.a.media.segmentView` | Datos de contexto de AppMeasurement. |
| `media.mediaTimed.midpoints.value` | `c.a.media.progress50` | Datos de contexto de AppMeasurement. |
| `media.mediaTimed.pauseTime.value` | `c.a.media.pauseTime` | Asignación de datos de contexto de AppMeasurement `c.a.media.pauseTime`. |
| `media.mediaTimed.pauses.value` | `c.a.media.pauseCount` | Asignación de datos de contexto de AppMeasurement `c.a.media.pauseCount`. |
| `media.mediaTimed.primaryAssetReference.@id` | `c.a.media.asset` | Datos de contexto de AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.dc:title` | `c.a.media.friendlyName` | Asignación de datos de contexto de AppMeasurement `c.a.media.friendlyName`. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Creator.[N].iptc4xmpExt:Name` | `c.a.media.originator` | Datos de contexto de AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Episode.iptc4xmpExt:Number` | `c.a.media.episode` | Asignación de datos de contexto de AppMeasurement `c.a.media.episode`. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Genre` | `c.a.media.genre` | Datos de contexto de AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Rating.[N].iptc4xmpExt:RatingValue` | `c.a.media.rating` | Datos de contexto de AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Season.iptc4xmpExt:Number` | `c.a.media.season` | Asignación de datos de contexto de AppMeasurement `c.a.media.season`. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Identifier` | `a.media.name` | Asignación de datos de contexto de AppMeasurement `a.media.name`. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Name` | `c.a.media.show` | Asignación de datos de contexto de AppMeasurement `c.a.media.show`. |
| `media.mediaTimed.primaryAssetReference.showType` | `c.a.media.type` | Asignación de datos de contexto de AppMeasurement `c.a.media.type` con la conversión VEDIO_SHOW_TYPE. |
| `media.mediaTimed.primaryAssetReference.showType` | `c.a.media.type` | Asignación de datos de contexto de AppMeasurement `c.a.media.type` con conversión VIDEO_SHOW_TYPE. |
| `media.mediaTimed.primaryAssetReference.xmpDM:duration` | `c.a.media.length` | Asignación de datos de contexto de AppMeasurement `c.a.media.length`. |
| `media.mediaTimed.primaryAssetViewDetails.@id` | `c.a.media.vsid` | Datos de contexto de AppMeasurement. |
| `media.mediaTimed.primaryAssetViewDetails.broadcastChannel` | `c.a.media.channel` | Asignación de datos de contexto de AppMeasurement `c.a.media.channel`. |
| `media.mediaTimed.primaryAssetViewDetails.broadcastContentType` | `c.a.contentType` | Asignación de datos de contexto de AppMeasurement `c.a.contentType`. |
| `media.mediaTimed.primaryAssetViewDetails.broadcastNetwork` | `c.a.media.network` | Asignación de datos de contexto de AppMeasurement `c.a.media.network`. |
| `media.mediaTimed.primaryAssetViewDetails.mediaSegmentView.value` | `c.a.media.segment` | Asignación de datos de contexto de AppMeasurement `c.a.media.segment`. |
| `media.mediaTimed.primaryAssetViewDetails.playerName` | `c.a.media.playerName` | Asignación de datos de contexto de AppMeasurement `c.a.media.playerName`. |
| `media.mediaTimed.primaryAssetViewDetails.playerSDKVersion.version` | `c.a.media.sdkVersion` | Asignación de datos de contexto de AppMeasurement `c.a.media.sdkVersion`. |
| `media.mediaTimed.primaryAssetViewDetails.sourceFeed` | `c.a.media.feed` | Asignación de datos de contexto de AppMeasurement `c.a.media.feed`. |
| `media.mediaTimed.primaryAssetViewDetails.streamFormat` | `c.a.media.format` | Asignación de datos de contexto de AppMeasurement `c.a.media.format`. |
| `media.mediaTimed.progress10.value` | `c.a.media.progress10` | Datos de contexto de AppMeasurement. |
| `media.mediaTimed.progress95.value` | `c.a.media.progress95` | Datos de contexto de AppMeasurement. |
| `media.mediaTimed.resumes.value` | `c.a.media.resume` | Asignación de datos de contexto de AppMeasurement `c.a.media.resume`. |
| `media.mediaTimed.starts.value` | `c.a.media.view` | Datos de contexto de AppMeasurement. |
| `media.mediaTimed.thirdQuartiles.value` | `c.a.media.progress75` | Datos de contexto de AppMeasurement. |
| `media.mediaTimed.timePlayed.value` | `c.a.media.timePlayed` | Asignación de datos de contexto de AppMeasurement `c.a.media.timePlayed`. |
| `media.mediaTimed.totalTimePlayed.value` | `c.a.media.totalTimePlayed` | Asignación de datos de contexto de AppMeasurement `c.a.media.totalTimePlayed`. |
| `placeContext.geo.latitude` | `lat` | Asignación LATITUDE del parámetro de consulta de AppMeasurement. |
| `placeContext.geo.longitude` | `lon` | Asignación del parámetro de consulta AppMeasurement en LONGITUDE. |
| `placeContext.geo.postalCode` | `zip` | Asignación ZIP del parámetro de consulta de AppMeasurement. |
| `placeContext.geo.stateProvince` | `state` | Asignación STATE del parámetro de consulta de AppMeasurement. |
| `productlistitems.[N]._[NAME_SPACE].*` | `products` | Parámetro de consulta de AppMeasurement Productos Eventos de mercancías / Asignación de Evars. |
| `productlistitems.[N].name` | `products` | Parámetro de consulta de AppMeasurement Asignación de nombres de productos. |
| `productlistitems.[N].priceTotal` | `products` | Parámetro de consulta de AppMeasurement Asignación de precios de productos. |
| `productlistitems.[N].quantity` | `products` | Parámetro de consulta de AppMeasurement Asignación de cantidad de productos. |
| `web.webInteraction.URL` | `pev1` | Asignación del parámetro de consulta de AppMeasurement PAGE_EVENTO_VAR1. |
| `web.webInteraction.name` | `pev2` | Asignación del parámetro de consulta de AppMeasurement PAGE_EVENTO_VAR2. |
| `web.webInteraction.type` | `pe` | `web.webInteraction.type=other` a  `pe=lnk_o`;  `web.webInteraction.type=download` a  `pe=lnk_d`;  `web.webInteraction.type=exit` to  `pe=lnk_e` |
| `web.webPageDetails.URL` | `g` | Asignación del parámetro de consulta de AppMeasurement PAGE_URL. |
| `web.webPageDetails.errorPage` | `pageType` | El parámetro de consulta de AppMeasurement PAGE_TYPE_FULL se asigna con la conversión ERROR_PAGE_TYPE. |
| `web.webPageDetails.homePage` | `hp` | Parámetro de consulta de AppMeasurement Asignación HOMEPAGE con conversión BOOLEAN_TO_YN. |
| `web.webPageDetails.name` | `gn` | Asignación del parámetro de consulta de AppMeasurement para PAGENAME. |
| `web.webPageDetails.server` | `sv` | Asignación del parámetro de consulta de AppMeasurement USER_SERVER. |
| `web.webPageDetails.siteSection` | `ch` | Asignación de CANALES de parámetros de consulta de AppMeasurement. |
| `web.webReferrer.URL` | `r` | Asignación de REMITENTES DEL REENVÍO de parámetros de consulta de AppMeasurement. |
