---
title: Variables asignadas automáticamente en Adobe Analytics
seo-title: Variables asignadas automáticamente en Adobe Analytics con Adobe Experience Platform Web SDK
description: Aprenda qué variables se asignan automáticamente en Adobe Analytics con el SDK web de Experience Platform
seo-description: Aprenda qué variables se asignan automáticamente en Adobe Analytics con el SDK web de Experience Platform
keywords: adobe analytics;variables;analytics;automatic map;automatically mapped;
translation-type: tm+mt
source-git-commit: 8e3bef77b84e40c836a6279a9a3e3901565c9920
workflow-type: tm+mt
source-wordcount: '681'
ht-degree: 0%

---


# Variables asignadas automáticamente en [!DNL Analytics]

A continuación se muestra una lista de variables a las que Adobe Experience Platform [!DNL Edge Network] asigna automáticamente [!DNL Analytics].

| Ruta de campo XDM | [!DNL Analytics Query String] / Encabezado HTTP | Descripción |
| ---------- | ------------------------- | ----------------------------------------- |
| `commerce.order.purchaseID` | `pi` | Asignación del parámetro de consulta de AppMeasurement PURCHASEID. |
| `commerce.order.currencyCode` | `cc` | Asignación de CURRENCY, parámetro de consulta de AppMeasurement. |
| `commerce.purchases.value` | `events` | Asignación del parámetro de consulta de AppMeasurement EVENTO_LISTA_FULL con conversion COMMERCE_PURCHASE, mediante delimitador `,`. |
| `commerce.productViews.value` | `events` | Asignación del parámetro de consulta de AppMeasurement EVENTO_LISTA_FULL con la VISTA COMMERCE_PROD_, mediante delimitador `,`. |
| `commerce.productListOpens.value` | `events` | Asignación del parámetro de consulta de AppMeasurement EVENTO_LISTA_FULL con conversion COMMERCE_SC_OPEN, mediante delimitador `,`. |
| `commerce.productListViews.value` | `events` | Asignación del parámetro de consulta de AppMeasurement EVENTO_LISTA_FULL con la VISTA COMMERCE_SC_mediante delimitador `,`. |
| `commerce.checkouts.value` | `events` | Asignación del parámetro de consulta de AppMeasurement EVENTO_LISTA_FULL con conversion COMMERCE_SC_CHECKOUT, mediante delimitador `,`. |
| `commerce.productListAdds.value` | `events` | Asignación del parámetro de consulta de AppMeasurement EVENTO_LISTA_FULL con conversion COMMERCE_SC_AÑADA, mediante delimitador `,`. |
| `commerce.productListRemovals.value` | `events` | Asignación del parámetro de consulta de AppMeasurement EVENTO_LISTA_FULL con conversion COMMERCE_SC_REMOVE, mediante delimitador `,`. |
| `commerce.productViews.id` | `events` | (Opcional) `prodView` serialización de evento. Si se excluye este campo (es decir, para eventos sin serializar), el sistema genera y asigna su propio valor de ID a la entidad. |
| `commerce.productListOpens.id` | `events` | (Opcional) `scOpen` serialización de evento. Si se excluye este campo (es decir, para eventos sin serializar), el sistema genera y asigna su propio valor de ID a la entidad. |
| `commerce.productListViews.id` | `events` | (Opcional) `scView` serialización de evento. Si se excluye este campo (es decir, para eventos sin serializar), el sistema genera y asigna su propio valor de ID a la entidad. |
| `commerce.productListAdds.id` | `events` | (Opcional) `scAdd` serialización de evento. Si se excluye este campo (es decir, para eventos sin serializar), el sistema genera y asigna su propio valor de ID a la entidad. |
| `commerce.productListRemovals.id` | `events` | (Opcional) `scRemove` serialización de evento. Si se excluye este campo (es decir, para eventos sin serializar), el sistema genera y asigna su propio valor de ID a la entidad. |
| `commerce.checkouts.id` | `events` | (Opcional) `scCheckout` serialización de evento. Si se excluye este campo (es decir, para eventos sin serializar), el sistema genera y asigna su propio valor de ID a la entidad. |
| `commerce.checkouts.id` | `events` | `scCheckout` Serialización de eventos. |
| `device.screenHeight` | `s` | Parámetro de consulta de AppMeasurement Asignación de resolución de pantalla. |
| `device.screenWidth` | `s` | Parámetro de consulta de AppMeasurement Asignación de resolución de pantalla. |
| `productlistitems.[N].lineitemid` | `products` | Parámetro de consulta de AppMeasurement Asignación de Categoría de productos. |
| `productlistitems.[N].name` | `products` | Parámetro de consulta de AppMeasurement Asignación de nombres de productos. |
| `productlistitems.[N].quantity` | `products` | Parámetro de consulta de AppMeasurement Asignación de cantidad de productos. |
| `productlistitems.[N].pricetotal` | `products` | Parámetro de consulta de AppMeasurement Asignación de precios de productos. |
| `media.mediaTimed.primaryAssetViewDetails.@id` | `c.a.media.vsid` | Datos de contexto de AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.@id` | `c.a.media.asset` | Datos de contexto de AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Rating.[N].iptc4xmpExt:RatingValue` | `c.a.media.rating` | Datos de contexto de AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Genre` | `c.a.media.genre` | Datos de contexto de AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Creator.[N].iptc4xmpExt:Name` | `c.a.media.originator` | Datos de contexto de AppMeasurement. |
| `media.mediaTimed.starts.value` | `c.a.media.view` | Datos de contexto de AppMeasurement. |
| `media.mediaTimed.progress10.value` | `c.a.media.progress10` | Datos de contexto de AppMeasurement. |
| `media.mediaTimed.firstQuartiles.value` | `c.a.media.progress25` | Datos de contexto de AppMeasurement. |
| `media.mediaTimed.midpoints.value` | `c.a.media.progress50` | Datos de contexto de AppMeasurement. |
| `media.mediaTimed.thirdQuartiles.value` | `c.a.media.progress75` | Datos de contexto de AppMeasurement. |
| `media.mediaTimed.progress95.value` | `c.a.media.progress95` | Datos de contexto de AppMeasurement. |
| `media.mediaTimed.completes.value` | `c.a.media.complete` | Datos de contexto de AppMeasurement. |
| `media.mediaTimed.mediaSegmentView.value` | `c.a.media.segmentView` | Datos de contexto de AppMeasurement. |
| `media.mediaTimed.dropBeforeStart.value` | `c.a.media.view`, `c.a.media.timePlayed`, `c.a.media.play` | Datos de contexto de AppMeasurement. |
| `environment.browserDetails.userAgent` | `User-Agent` | Es una asignación de encabezado HTTP, HEADER_USER_AGENT. |
| `environment.browserDetails.acceptLanguage` | `Accept-Language` | Es una asignación de encabezado HTTP, HEADER_ACCEPT_LANGUAGE. |
| `environment.browserDetails.cookiesEnabled` | `k` | Asignación COOKIES del parámetro de consulta de AppMeasurement con la conversión BOOLEAN_TO_YN. |
| `environment.browserDetails.javaScriptVersion` | `j` | Asignación del parámetro de consulta AppMeasurement J_JSCRIPT. |
| `environment.browserDetails.javaEnabled` | `v` | Asignación del parámetro de consulta de AppMeasurement JAVA_ENABLED con BOOLEAN_TO_YN de conversión. |
| `environment.browserDetails.viewportHeight` | `bh` | Asignación del parámetro de consulta de AppMeasurement para BROWSER_HEIGHT. |
| `environment.browserDetails.viewportWidth` | `bw` | Asignación del parámetro de consulta de AppMeasurement para BROWSER_WIDTH. |
| `environment.connectionType` | `ct` | Asignación del parámetro de consulta AppMeasurement CT_CONNECT_TYPE. |
| `device.colorDepth` | `c` | Asignación del parámetro de consulta de AppMeasurement C_COLOR. |
| `placeContext.geo.stateProvince` | `state` | Asignación STATE del parámetro de consulta de AppMeasurement. |
| `placeContext.geo.postalCode` | `zip` | Asignación ZIP del parámetro de consulta de AppMeasurement. |
| `placeContext.geo.latitude` | `lat` | Asignación LATITUDE del parámetro de consulta de AppMeasurement. |
| `placeContext.geo.longitude` | `lon` | Asignación del parámetro de consulta AppMeasurement en LONGITUDE. |
| `web.webPageDetails.server` | `sv` | Asignación del parámetro de consulta de AppMeasurement USER_SERVER. |
| `web.webPageDetails.name` | `gn` | Asignación del parámetro de consulta de AppMeasurement para PAGENAME. |
| `web.webPageDetails.URL` | `g` | Asignación del parámetro de consulta de AppMeasurement PAGE_URL. |
| `web.webPageDetails.homePage` | `hp` | Parámetro de consulta de AppMeasurement Asignación HOMEPAGE con conversión BOOLEAN_TO_YN. |
| `web.webReferrer.URL` | `r` | Asignación de REMITENTES DEL REENVÍO de parámetros de consulta de AppMeasurement. |
| `web.webInteraction.type` | `pe` | Parámetro de consulta de AppMeasurement Asignación PAGE_EVENTO con conversión CLICK_MAP_TYPE. |
| `web.webInteraction.URL` | `pev1` | Asignación del parámetro de consulta de AppMeasurement PAGE_EVENTO_VAR1. |
| `web.webInteraction.name` | `pev2` | Asignación del parámetro de consulta de AppMeasurement PAGE_EVENTO_VAR2. |
| `web.webPageDetails.siteSection` | `ch` | Asignación de CANALES de parámetros de consulta de AppMeasurement. |
| `web.webPageDetails.errorPage` | `pageType` | El parámetro de consulta de AppMeasurement PAGE_TYPE_FULL se asigna con la conversión ERROR_PAGE_TYPE. |
| `application.id` | `c.a.appid` | Asignación `c.a.appid` de datos de contexto de AppMeasurement. |
| `application.launches.value` | `c.a.launches` | Asignación `c.a.launches` de datos de contexto de AppMeasurement. |
| `marketing.trackingCode` | `v0` | Asignación de CAMPAÑA de parámetros de consulta de AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Identifier` | `a.media.name` | Asignación `a.media.name` de datos de contexto de AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.xmpDM:duration` | `c.a.media.length` | Asignación `c.a.media.length` de datos de contexto de AppMeasurement. |
| `media.mediaTimed.primaryAssetViewDetails.broadcastContentType` | `c.a.contentType` | Asignación `c.a.contentType` de datos de contexto de AppMeasurement. |
| `media.mediaTimed.primaryAssetViewDetails.playerName` | `c.a.media.playerName` | Asignación `c.a.media.playerName` de datos de contexto de AppMeasurement. |
| `media.mediaTimed.primaryAssetViewDetails.broadcastChannel` | `c.a.media.channel` | Asignación `c.a.media.channel` de datos de contexto de AppMeasurement. |
| `media.mediaTimed.primaryAssetViewDetails.mediaSegmentView.value` | `c.a.media.segment` | Asignación `c.a.media.segment` de datos de contexto de AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.dc:title` | `c.a.media.friendlyName` | Asignación `c.a.media.friendlyName` de datos de contexto de AppMeasurement. |
| `media.mediaTimed.primaryAssetViewDetails.playerSDKVersion.version` | `c.a.media.sdkVersion` | Asignación `c.a.media.sdkVersion` de datos de contexto de AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Name` | `c.a.media.show` | Asignación `c.a.media.show` de datos de contexto de AppMeasurement. |
| `media.mediaTimed.primaryAssetViewDetails.streamFormat` | `c.a.media.format` | Asignación `c.a.media.format` de datos de contexto de AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Season.iptc4xmpExt:Number` | `c.a.media.season` | Asignación `c.a.media.season` de datos de contexto de AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Episode.iptc4xmpExt:Number` | `c.a.media.episode` | Asignación `c.a.media.episode` de datos de contexto de AppMeasurement. |
| `media.mediaTimed.primaryAssetViewDetails.broadcastNetwork` | `c.a.media.network` | Asignación `c.a.media.network` de datos de contexto de AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.showType` | `c.a.media.type` | Asignación `c.a.media.type` de datos de contexto de AppMeasurement con conversión VEDIO_SHOW_TYPE. |
| `media.mediaTimed.primaryAssetViewDetails.sourceFeed` | `c.a.media.feed` | Asignación `c.a.media.feed` de datos de contexto de AppMeasurement. |
| `media.mediaTimed.timePlayed.value` | `c.a.media.timePlayed` | Asignación `c.a.media.timePlayed` de datos de contexto de AppMeasurement. |
| `media.mediaTimed.totalTimePlayed.value` | `c.a.media.totalTimePlayed` | Asignación `c.a.media.totalTimePlayed` de datos de contexto de AppMeasurement. |
| `media.mediaTimed.federated.value` | `c.a.media.federated` | Asignación `c.a.media.federated` de datos de contexto de AppMeasurement. |
| `media.mediaTimed.pauses.value` | `c.a.media.pauseCount` | Asignación `c.a.media.pauseCount` de datos de contexto de AppMeasurement. |
| `media.mediaTimed.pauseTime.value` | `c.a.media.pauseTime` | Asignación `c.a.media.pauseTime` de datos de contexto de AppMeasurement. |
| `media.mediaTimed.resumes.value` | `c.a.media.resume` | Asignación `c.a.media.resume` de datos de contexto de AppMeasurement. |
| `media.mediaTimed.primaryAssetReference.showType` | `c.a.media.type` | Asignación `c.a.media.type` de datos de contexto de AppMeasurement con conversión VIDEO_SHOW_TYPE. |
| `identityMap.ECID.[0].id` | `mid` | Asignación MID del parámetro de consulta de AppMeasurement. |
