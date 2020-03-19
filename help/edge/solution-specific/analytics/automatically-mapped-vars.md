---
title: Variables asignadas automáticamente en Analytics
seo-title: Variables asignadas automáticamente en Analytics con el SDK web de la plataforma Adobe Experience Platform
description: Descubra qué variables se asignan automáticamente en Analytics con el SDK web de la plataforma de experiencia
seo-description: Descubra qué variables se asignan automáticamente en Analytics con el SDK web de la plataforma de experiencia
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# Variables asignadas automáticamente en Analytics

>[!IMPORTANT]
>
>El SDK web de la plataforma de experiencia de Adobe se encuentra en fase beta y no está disponible para todos los usuarios. La documentación y la funcionalidad están sujetas a cambios.

A continuación se muestra una lista de variables que Adobe Experience Platform Edge Network asigna automáticamente a Analytics.

| Ruta de campo XDM | Cadena de consulta de Analytics/Encabezado HTTP | Descripción |
| ---------- | ------------------------- | -------- |
| `environment.browserDetails.userAgent` | `User-Agent` | Es una asignación de encabezado HTTP, HEADER_USER_AGENT. |
| `environment.browserDetails.acceptLanguage` | `Accept-Language` | Es una asignación de encabezado HTTP, HEADER_ACCEPT_LANGUAGE. |
| `environment.browserDetails.cookiesEnabled` | `k` | Asignación COOKIES del parámetro de consulta AppMeasurement con la conversión BOOLEAN_TO_YN. |
| `environment.browserDetails.javaScriptVersion` | `j` | Asignación del parámetro de consulta AppMeasurement J_JSCRIPT. |
| `environment.browserDetails.javaEnabled` | `v` | Asignación del parámetro de consulta AppMeasurement JAVA_ENABLED con la conversión BOOLEAN_TO_YN. |
| `environment.browserDetails.viewportHeight` | `bh` | Asignación del parámetro de consulta AppMeasurement para BROWSER_HEIGHT. |
| `environment.browserDetails.viewportWidth` | `bw` | Asignación del parámetro de consulta AppMeasurement para BROWSER_WIDTH. |
| `environment.connectionType` | `ct` | Asignación del parámetro de consulta AppMeasurement CT_CONNECT_TYPE. |
| `device.colorDepth` | `c` | Asignación del parámetro de consulta de AppMeasurement C_COLOR. |
| `placeContext.geo.stateProvince` | `state` | Asignación STATE del parámetro de consulta AppMeasurement. |
| `placeContext.geo.postalCode` | `zip` | Asignación ZIP del parámetro de consulta AppMeasurement. |
| `placeContext.geo.latitude` | `lat` | Asignación LATITUDE del parámetro de consulta AppMeasurement. |
| `placeContext.geo.longitude` | `lon` | Asignación del parámetro de consulta AppMeasurement en LONGITUDE. |
| `web.webPageDetails.server` | `sv` | Asignación del parámetro de consulta AppMeasurement USER_SERVER. |
| `web.webPageDetails.name` | `gn` | Asignación del parámetro de consulta AppMeasurement para PAGENAME. |
| `web.webPageDetails.URL` | `g` | Asignación del parámetro de consulta AppMeasurement PAGE_URL. |
| `web.webPageDetails.homePage` | `hp` | Asignación del parámetro de consulta AppMeasurement HOMEPAGE con la conversión BOOLEAN_TO_YN. |
| `web.webReferrer.URL` | `r` | Asignación de REFERRER del parámetro de consulta AppMeasurement. |
| `application.id` | `c.a.appid` | Asignación `c.a.appid` de datos de contexto de AppMeasurement. |
| `application.launches.value` | `c.a.launches` | Asignación `c.a.launches` de datos de contexto de AppMeasurement. |
| `marketing.trackingCode` | `v0` | Asignación del parámetro de consulta AppMeasurement en CAMPAIGN. |
| `commerce.purchaseID` | `pi` | Asignación del parámetro de consulta AppMeasurement PURCHASEID. |
| `commerce.currencyCode` | `cc` | Asignación de CURRENCY del parámetro de consulta AppMeasurement. |
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
| `identitymap.ecid.[0].id` | `mid` | Asignación MID del parámetro de consulta AppMeasurement. |
