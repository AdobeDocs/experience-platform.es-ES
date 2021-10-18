---
title: Variables de Adobe Analytics asignadas automáticamente en el SDK web de Adobe Experience Platform
description: Descubra qué variables se asignan automáticamente en Adobe Analytics con el SDK web de Experience Platform
seo-description: Learn which variables are automatically mapped in Adobe Analytics with the Adobe Experience Platform Web SDK
keywords: adobe analytics;variables;analytics;asignación automática;asignación automática;
exl-id: 856fada7-b62c-4fd2-9372-a19ae1cdec33
source-git-commit: dcbe4c1b5a085878562990ed2db8e5cb27b93e28
workflow-type: tm+mt
source-wordcount: '918'
ht-degree: 5%

---

# Variables asignadas automáticamente en [!DNL Analytics]

A continuación se muestra una lista de variables que Adobe Experience Platform Edge Network asigna automáticamente a Adobe Analytics. Encontrará información detallada sobre los parámetros de consulta de recopilación de datos de Adobe Analytics en la [Guía de implementación de Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/validate/query-parameters.html).

>[!NOTE]
>La información de esta página también se aplica al SDK de Adobe Mobile.

| Ruta de campo XDM | [!DNL Analytics Query String] / Encabezado HTTP | Descripción |
| ---------- | ------------------------- | ----------------------------------------- |
| application.id | c.a.appid | Datos de contexto de AppMeasurement `c.a.appid` asignación. |
| application.launches.value | c.a.launches | Datos de contexto de AppMeasurement `c.a.launches` asignación. |
| commerce.checkouts.id | de reacción | `scCheckout` serialización de eventos. Si este campo se excluye (es decir, para eventos sin serializar), el sistema genera y asigna su propio valor de ID a la entidad. |
| commerce.checkouts.value | de reacción | Asignación del parámetro de consulta AppMeasurement EVENT_LIST_FULL con la conversión COMMERCE_SC_CHECKOUT, con delimitador `,`. |
| commerce.order.currencyCode | cc | Asignación de CURRENCY del parámetro de consulta AppMeasurement. |
| commerce.order.purchaseID | pi | Asignación del parámetro de consulta AppMeasurement PURCHASEID . |
| commerce.productListAdds.id | de reacción | `scAdd` serialización de eventos. Si este campo se excluye (es decir, para eventos sin serializar), el sistema genera y asigna su propio valor de ID a la entidad. |
| commerce.productListAdds.value | de reacción | Asignación del parámetro de consulta AppMeasurement EVENT_LIST_FULL con la conversión COMMERCE_SC_ADD, con delimitador `,`. |
| commerce.productListOpens.id | de reacción | `scOpen` serialización de eventos. Si este campo se excluye (es decir, para eventos sin serializar), el sistema genera y asigna su propio valor de ID a la entidad. |
| commerce.productListOpens.value | de reacción | Asignación del parámetro de consulta AppMeasurement EVENT_LIST_FULL con la conversión COMMERCE_SC_OPEN, con delimitador `,`. |
| commerce.productListRemovals.id | de reacción | `scRemove` serialización de eventos. Si este campo se excluye (es decir, para eventos sin serializar), el sistema genera y asigna su propio valor de ID a la entidad. |
| commerce.productListRemovals.value | de reacción | Asignación del parámetro de consulta AppMeasurement EVENT_LIST_FULL con la conversión COMMERCE_SC_REMOVE, con delimitador `,`. |
| commerce.productListViews.id | de reacción | `scView` serialización de eventos. Si este campo se excluye (es decir, para eventos sin serializar), el sistema genera y asigna su propio valor de ID a la entidad. |
| commerce.productListViews.value | de reacción | Asignación del parámetro de consulta AppMeasurement EVENT_LIST_FULL con la conversión COMMERCE_SC_VIEW, con delimitador `,`. |
| commerce.productViews.id | de reacción | `prodView` serialización de eventos. Si este campo se excluye (es decir, para eventos sin serializar), el sistema genera y asigna su propio valor de ID a la entidad. |
| commerce.productViews.value | de reacción | Asignación del parámetro de consulta AppMeasurement EVENT_LIST_FULL con la conversión COMMERCE_PROD_VIEW, mediante delimitador `,`. |
| commerce.purchases.value | de reacción | Asignación del parámetro de consulta AppMeasurement EVENT_LIST_FULL con la conversión COMMERCE_PURCHASE, con delimitador `,`. |
| device.colorDepth | c | Asignación del parámetro de consulta AppMeasurement C_COLOR. |
| device.screenHeight | s | Parámetro de consulta AppMeasurement Asignación de resolución de pantalla. |
| device.screenWidth | s | Parámetro de consulta AppMeasurement Asignación de resolución de pantalla. |
| environment.browserDetails.acceptLanguage | Accept-Language | Esto es una asignación de encabezados HTTP, HEADER_ACCEPT_LANGUAGE. |
| environment.browserDetails.cookiesEnabled | k | Parámetro de consulta AppMeasurement COOKIES asignación con conversión BOOLEAN_TO_YN. |
| environment.browserDetails.javaEnabled | Versión  | El parámetro de consulta AppMeasurement JAVA_ENABLED se asigna con la conversión BOOLEAN_TO_YN. |
| environment.browserDetails.javaScriptVersion | j | Asignación del parámetro de consulta AppMeasurement J_JSCRIPT. |
| environment.browserDetails.userAgent | User-Agent | Se trata de una asignación de encabezados HTTP, HEADER_USER_AGENT. |
| environment.browserDetails.viewportHeight | bh | Asignación del parámetro de consulta AppMeasurement para BROWSER_HEIGHT. |
| environment.browserDetails.viewportWidth | bw | Asignación del parámetro de consulta AppMeasurement para BROWSER_WIDTH . |
| environment.connectionType | ct | Asignación del parámetro de consulta AppMeasurement CT_CONNECT_TYPE. |
| environment.ipV4 | X-Forwarded-For | Esta es una asignación de encabezados HTTP, X-FORWARDED-FOR. |
| identityMap.ECID[0].id | mid | Asignación de MID del parámetro de consulta AppMeasurement. |
| marketing.trackingCode | Versión 0 | Asignación del parámetro de consulta AppMeasurement en CAMPAIGN. |
| media.mediaTimed.completes.value | c.a.media.complete | Datos de contexto de AppMeasurement. |
| media.mediaTimed.dropBeforeStart.value | c.a.media.view, c.a.media.timePlayed, c.a.media.play | Datos de contexto de AppMeasurement. |
| media.mediaTimed.federated.value | c.a.media.federated | Datos de contexto de AppMeasurement `c.a.media.federated` asignación. |
| media.mediaTimed.firstQuartiles.value | c.a.media.progress25 | Datos de contexto de AppMeasurement. |
| media.mediaTimed.mediaSegmentView.value | c.a.media.segmentView | Datos de contexto de AppMeasurement. |
| media.mediaTimed.midpoints.value | c.a.media.progress50 | Datos de contexto de AppMeasurement. |
| media.mediaTimed.pauseTime.value | c.a.media.pauseTime | Datos de contexto de AppMeasurement `c.a.media.pauseTime` asignación. |
| media.mediaTimed.pauses.value | c.a.media.pauseCount | Datos de contexto de AppMeasurement `c.a.media.pauseCount` asignación. |
| media.mediaTimed.primaryAssetReference.@id | c.a.media.asset | Datos de contexto de AppMeasurement. |
| media.mediaTimed.primaryAssetReference.dc:title | c.a.media.friendlyName | Datos de contexto de AppMeasurement `c.a.media.friendlyName` asignación. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Creator[N].iptc4xmpExt:Name | c.a.media.originator | Datos de contexto de AppMeasurement. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Episode.iptc4xmpExt:Number | c.a.media.episode | Datos de contexto de AppMeasurement `c.a.media.episode` asignación. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Genre | c.a.media.genre | Datos de contexto de AppMeasurement. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Rating[N].iptc4xmpExt:RatingValue | c.a.media.rating | Datos de contexto de AppMeasurement. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Season.iptc4xmpExt:Number | c.a.media.season | Datos de contexto de AppMeasurement `c.a.media.season` asignación. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Identifier | a.media.name | Datos de contexto de AppMeasurement `a.media.name` asignación. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Name | c.a.media.show | Datos de contexto de AppMeasurement `c.a.media.show` asignación. |
| media.mediaTimed.primaryAssetReference.showType | c.a.media.type | Datos de contexto de AppMeasurement `c.a.media.type` asignación con conversión VEDIO_SHOW_TYPE. |
| media.mediaTimed.primaryAssetReference.showType | c.a.media.type | Datos de contexto de AppMeasurement `c.a.media.type` asignación con conversión VIDEO_SHOW_TYPE. |
| media.mediaTimed.primaryAssetReference.xmpDM:duration | c.a.media.length | Datos de contexto de AppMeasurement `c.a.media.length` asignación. |
| media.mediaTimed.primaryAssetViewDetails.@id | c.a.media.vsid | Datos de contexto de AppMeasurement. |
| media.mediaTimed.primaryAssetViewDetails.broadcastChannel | c.a.media.channel | Datos de contexto de AppMeasurement `c.a.media.channel` asignación. |
| media.mediaTimed.primaryAssetViewDetails.broadcastContentType | c.a.contentType | Datos de contexto de AppMeasurement `c.a.contentType` asignación. |
| media.mediaTimed.primaryAssetViewDetails.broadcastNetwork | c.a.media.network | Datos de contexto de AppMeasurement `c.a.media.network` asignación. |
| media.mediaTimed.primaryAssetViewDetails.mediaSegmentView.value | c.a.media.segment | Datos de contexto de AppMeasurement `c.a.media.segment` asignación. |
| media.mediaTimed.primaryAssetViewDetails.playerName | c.a.media.playerName | Datos de contexto de AppMeasurement `c.a.media.playerName` asignación. |
| media.mediaTimed.primaryAssetViewDetails.playerSDKVersion.version | c.a.media.sdkVersion | Datos de contexto de AppMeasurement `c.a.media.sdkVersion` asignación. |
| media.mediaTimed.primaryAssetViewDetails.sourceFeed | c.a.media.feed | Datos de contexto de AppMeasurement `c.a.media.feed` asignación. |
| media.mediaTimed.primaryAssetViewDetails.streamFormat | c.a.media.format | Datos de contexto de AppMeasurement `c.a.media.format` asignación. |
| media.mediaTimed.progress10.value | c.a.media.progress10 | Datos de contexto de AppMeasurement. |
| media.mediaTimed.progress95.value | c.a.media.progress95 | Datos de contexto de AppMeasurement. |
| media.mediaTimed.resumes.value | c.a.media.resume | Datos de contexto de AppMeasurement `c.a.media.resume` asignación. |
| media.mediaTimed.starts.value | c.a.media.view | Datos de contexto de AppMeasurement. |
| media.mediaTimed.thirdQuartiles.value | c.a.media.progress75 | Datos de contexto de AppMeasurement. |
| media.mediaTimed.timePlayed.value | c.a.media.timePlayed | Datos de contexto de AppMeasurement `c.a.media.timePlayed` asignación. |
| media.mediaTimed.totalTimePlayed.value | c.a.media.totalTimePlayed | Datos de contexto de AppMeasurement `c.a.media.totalTimePlayed` asignación. |
| placeContext.geo.latitude | lat | Parámetro de consulta AppMeasurement asignación LATITUDE. |
| placeContext.geo.longitude | lon | Asignación del parámetro de consulta AppMeasurement en LONGITUDE. |
| placeContext.geo.postalCode | zip | Asignación ZIP del parámetro de consulta AppMeasurement. |
| placeContext.geo.stateProvince | estado | Asignación STATE del parámetro de consulta AppMeasurement. |
| productListItems[N].lineItemId | Productos | Parámetro de consulta AppMeasurement Productos Asignación de categorías. |
| productlistiitems[N].name | Productos | Parámetro de consulta AppMeasurement Asignación de nombres de productos. |
| productlistiitems[N].priceTotal | Productos | Parámetro de consulta AppMeasurement Asignación de precios de productos. |
| productlistiitems[N].quantity | Productos | Parámetro de consulta AppMeasurement Asignación de cantidad de productos. |
| web.webInteraction.URL | pev1 | Asignación del parámetro de consulta AppMeasurement PAGE_EVENT_VAR1 . |
| web.webInteraction.name | pev2 | Asignación del parámetro de consulta AppMeasurement PAGE_EVENT_VAR2 . |
| web.webInteraction.type | pe | `web.webInteraction.type=other` a `pe=lnk_o`; `web.webInteraction.type=download` a `pe=lnk_d`; `web.webInteraction.type=exit` a `pe=lnk_e` |
| web.webPageDetails.URL | g | Parámetro de consulta AppMeasurement asignación PAGE_URL. |
| web.webPageDetails.errorPage | pageType | Parámetro de consulta AppMeasurement PAGE_TYPE_FULL asignación con conversión ERROR_PAGE_TYPE. |
| web.webPageDetails.homePage | hp | Asignación del parámetro de consulta AppMeasurement HOMEPAGE con la conversión BOOLEAN_TO_YN. |
| web.webPageDetails.name | gn | Asignación del parámetro de consulta AppMeasurement PAGENAME. |
| web.webPageDetails.server | sv | Asignación del parámetro de consulta AppMeasurement USER_SERVER . |
| web.webPageDetails.siteSection | ch | Parámetro de consulta AppMeasurement Asignación de CANAL. |
| web.webReferrer.URL | r | Asignación del parámetro de consulta AppMeasurement REFERRER. |

{style=&quot;table-layout:auto&quot;}
