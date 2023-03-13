---
title: Variables de Adobe Analytics asignadas automáticamente en el SDK web de Adobe Experience Platform
description: Descubra qué variables se asignan automáticamente en Adobe Analytics con el SDK web de Experience Platform
seo-description: Learn which variables are automatically mapped in Adobe Analytics with the Adobe Experience Platform Web SDK
keywords: adobe analytics;variables;analytics;asignación automática;asignada automáticamente;
exl-id: 856fada7-b62c-4fd2-9372-a19ae1cdec33
source-git-commit: dcbe4c1b5a085878562990ed2db8e5cb27b93e28
workflow-type: tm+mt
source-wordcount: '915'
ht-degree: 6%

---

# Variables asignadas automáticamente en [!DNL Analytics]

A continuación se muestra una lista de variables que Adobe Experience Platform Edge Network asigna automáticamente a Adobe Analytics. Encontrará información detallada sobre los parámetros de consulta de recopilación de datos de Adobe Analytics en la [Guía de implementación de Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/validate/query-parameters.html?lang=es).

>[!NOTE]
>La información de esta página también se aplica al SDK de Adobe Mobile.

| Ruta de campo XDM | [!DNL Analytics Query String] / Encabezado HTTP | Descripción |
| ---------- | ------------------------- | ----------------------------------------- |
| application.id | c.a.appid | Datos de contexto de AppMeasurement `c.a.appid` asignación. |
| application.launches.value | c.a.launches | Datos de contexto de AppMeasurement `c.a.launches` asignación. |
| commerce.checkouts.id | de reacción | `scCheckout` Serialización de eventos. Si se excluye este campo (es decir, para eventos no serializados), el sistema genera y asigna su propio valor de ID a la entidad. |
| commerce.checkouts.value | de reacción | Asignación del parámetro de consulta EVENT_LIST_FULL de AppMeasurement con conversión COMMERCE_SC_CHECKOUT, con delimitador `,`. |
| commerce.order.currencyCode | cc | Asignación de MONEDA del parámetro de consulta AppMeasurement. |
| commerce.order.purchaseID | pi | Asignación del parámetro de consulta PURCHASEID de AppMeasurement. |
| commerce.productListAdds.id | de reacción | `scAdd` Serialización de eventos. Si se excluye este campo (es decir, para eventos no serializados), el sistema genera y asigna su propio valor de ID a la entidad. |
| commerce.productListAdds.value | de reacción | Asignación del parámetro de consulta EVENT_LIST_FULL de AppMeasurement con conversión COMMERCE_SC_ADD, con delimitador `,`. |
| commerce.productListOpens.id | de reacción | `scOpen` Serialización de eventos. Si se excluye este campo (es decir, para eventos no serializados), el sistema genera y asigna su propio valor de ID a la entidad. |
| commerce.productListOpens.value | de reacción | Asignación del parámetro de consulta EVENT_LIST_FULL de AppMeasurement con conversión COMMERCE_SC_OPEN, con delimitador `,`. |
| commerce.productListRemovals.id | de reacción | `scRemove` Serialización de eventos. Si se excluye este campo (es decir, para eventos no serializados), el sistema genera y asigna su propio valor de ID a la entidad. |
| commerce.productListRemovals.value | de reacción | Asignación del parámetro de consulta EVENT_LIST_FULL de AppMeasurement con conversión COMMERCE_SC_REMOVE, con delimitador `,`. |
| commerce.productListViews.id | de reacción | `scView` Serialización de eventos. Si se excluye este campo (es decir, para eventos no serializados), el sistema genera y asigna su propio valor de ID a la entidad. |
| commerce.productListViews.value | de reacción | Asignación del parámetro de consulta EVENT_LIST_FULL de AppMeasurement con conversión COMMERCE_SC_VIEW, con delimitador `,`. |
| commerce.productViews.id | de reacción | `prodView` Serialización de eventos. Si se excluye este campo (es decir, para eventos no serializados), el sistema genera y asigna su propio valor de ID a la entidad. |
| commerce.productViews.value | de reacción | Asignación del parámetro de consulta EVENT_LIST_FULL de AppMeasurement con la conversión COMMERCE_PROD_VIEW, con delimitador `,`. |
| commerce.purchases.value | de reacción | Asignación del parámetro de consulta EVENT_LIST_FULL de AppMeasurement con conversión COMMERCE_PURCHASE, con delimitador `,`. |
| device.colorDepth | c | Asignación del parámetro de consulta C_COLOR de AppMeasurement. |
| device.screenHeight | s | Asignación de resolución de pantalla del parámetro de consulta AppMeasurement. |
| device.screenWidth | s | Asignación de resolución de pantalla del parámetro de consulta AppMeasurement. |
| environment.browserDetails.acceptLanguage | Accept-Language | Es una asignación de encabezado HTTP, HEADER_ACCEPT_LANGUAGE. |
| environment.browserDetails.cookiesEnabled | k | Asignación de COOKIES del parámetro de consulta de AppMeasurement con la conversión BOOLEAN_TO_YN. |
| environment.browserDetails.javaEnabled | Versión  | Asignación del parámetro de consulta JAVA_ENABLED de AppMeasurement con la conversión BOOLEAN_TO_YN. |
| environment.browserDetails.javaScriptVersion | j | Asignación de J_JSCRIPT del parámetro de consulta de AppMeasurement. |
| environment.browserDetails.userAgent | User-Agent | Es una asignación de encabezado HTTP, HEADER_USER_AGENT. |
| environment.browserDetails.viewportHeight | bh | Asignación del parámetro de consulta BROWSER_HEIGHT de AppMeasurement. |
| environment.browserDetails.viewportWidth | pc | Asignación del parámetro de consulta BROWSER_WIDTH de AppMeasurement. |
| environment.connectionType | ct | Asignación del parámetro de consulta CT_CONNECT_TYPE de AppMeasurement. |
| environment.ipV4 | X-Forwarded-For | Esta es una asignación de encabezado HTTP, X-FORWARDED-FOR. |
| identityMap.ECID[0].id | mid | Asignación de MID del parámetro de consulta de AppMeasurement. |
| marketing.trackingCode | Versión 0 | Asignación del parámetro de consulta CAMPAIGN de AppMeasurement. |
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
| placeContext.geo.latitude | lat | Asignación de LATITUDE del parámetro de consulta de AppMeasurement. |
| placeContext.geo.longitude | lon | Asignación de LONGITUDE del parámetro de consulta de AppMeasurement. |
| placeContext.geo.postalCode | zip | Asignación ZIP del parámetro de consulta de AppMeasurement. |
| placeContext.geo.stateProvince | estado | Asignación STATE del parámetro de consulta de AppMeasurement. |
| productListItems[N].lineItemId | productos | Asignación de categoría de productos del parámetro de consulta de AppMeasurement. |
| productlistitems[N].name | productos | Asignación de nombres de productos del parámetro de consulta AppMeasurement. |
| productlistitems[N].priceTotal | productos | Parámetro de consulta AppMeasurement Productos Asignación de precios. |
| productlistitems[N].quantity | productos | Parámetro de consulta AppMeasurement Productos Asignación de cantidad. |
| web.webInteraction.URL | pev1 | Asignación del parámetro de consulta PAGE_EVENT_VAR1 de AppMeasurement. |
| web.webInteraction.name | pev2 | Asignación del parámetro de consulta PAGE_EVENT_VAR2 de AppMeasurement. |
| web.webInteraction.type | pe | `web.webInteraction.type=other` hasta `pe=lnk_o`; `web.webInteraction.type=download` hasta `pe=lnk_d`; `web.webInteraction.type=exit` hasta `pe=lnk_e` |
| web.webPageDetails.URL | g | Asignación PAGE_URL del parámetro de consulta de AppMeasurement. |
| web.webPageDetails.errorPage | pageType | Asignación del parámetro de consulta PAGE_TYPE_FULL de AppMeasurement con conversión ERROR_PAGE_TYPE. |
| web.webPageDetails.homePage | hp | Asignación del parámetro de consulta HOMEPAGE de AppMeasurement con la conversión BOOLEAN_TO_YN. |
| web.webPageDetails.name | gn | Asignación del parámetro de consulta PAGENAME de AppMeasurement. |
| web.webPageDetails.server | sv | Asignación del parámetro de consulta USER_SERVER de AppMeasurement. |
| web.webPageDetails.siteSection | ch | Asignación de CANAL del parámetro de consulta de AppMeasurement. |
| web.webReferrer.URL | r | Asignación del REFERENTE del parámetro de consulta de AppMeasurement. |

{style="table-layout:auto"}
