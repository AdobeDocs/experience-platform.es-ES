---
keywords: Experience Platform;inicio;temas populares;campos de asignación de Analytics;asignación de analytics
solution: Experience Platform
title: Asignación de campos para el conector de origen de Adobe Analytics
topic-legacy: overview
description: Adobe Experience Platform le permite introducir datos de Adobe Analytics a través de la fuente de Analytics. Algunos de los datos introducidos a través de ADC pueden asignarse directamente de los campos de Analytics a los campos del Modelo de datos de experiencia (XDM), mientras que otros datos requieren transformaciones y funciones específicas para poder asignarse correctamente.
exl-id: 15dc1368-5cf1-42e1-9683-d5158f8aa2db
source-git-commit: efe36904b0dce94a8b1f5e7a3d3f38da1038d49c
workflow-type: tm+mt
source-wordcount: '3401'
ht-degree: 13%

---

# Asignaciones de campos de Analytics

Adobe Experience Platform le permite introducir datos de Adobe Analytics a través de la fuente de Analytics. Algunos de los datos introducidos a través de ADC pueden asignarse directamente de los campos de Analytics a los campos del Modelo de datos de experiencia (XDM), mientras que otros datos requieren transformaciones y funciones específicas para poder asignarse correctamente.

![](../images/analytics-data-experience-platform.png)

## Campos de asignación directa

Los campos seleccionados se asignan directamente de Adobe Analytics al modelo de datos de Experience (XDM).

La tabla siguiente incluye columnas que muestran el nombre del campo Analytics (*Campo de Analytics*), el campo XDM correspondiente (*Campo XDM*) y su tipo (*Tipo XDM*), así como una descripción del campo (*Descripción*).

>[!NOTE]
>
>Desplácese a la izquierda/derecha para ver todo el contenido de la tabla.

| Campo de Analytics | Campo XDM | Tipo XDM | Descripción |
| --------------- | --------- | -------- | ---------- |
| m_evar1 - m_evar250 | _experience.analytics.customDimensions.eVars.eVar1 - _experience.analytics.customDimensions.eVars.eVar250 | string | Variable personalizada, que puede oscilar entre 1 y 250. Cada organización utilizará estas eVars personalizadas de forma diferente. |
| m_prop1 - m_prop75 | _experience.analytics.customDimensions.props.prop1 - _experience.analytics.customDimensions.props.prop75 | string | Variables de tráfico personalizadas, que pueden oscilar entre 1 y 75. |
| m_browser | _experience.analytics.environment.browserID | integer | El ID de número del explorador. |
| m_browser_height | environment.browserDetails.viewportHeight | integer | Altura del explorador, en píxeles. |
| m_browser_width | environment.browserDetails.viewportWidth | integer | Anchura del explorador, en píxeles. |
| m_campaign | marketing.trackingCode | string | La variable utilizada en la dimensión Código de seguimiento . |
| m_channel | web.webPageDetails.siteSection | string | La variable utilizada en la dimensión Secciones del sitio. |
| m_domain | environment.domain | string | La variable utilizada en la dimensión Dominio . Esto se basa en el proveedor de servicios de Internet (ISP) del usuario. |
| m_geo_city | placeContext.geo.city | string | Nombre de la ciudad de la visita. Se basa en la dirección IP de la visita. |
| m_geo_dma | placeContext.geo.dmaID | integer | ID numérico del área demográfica de la visita. Se basa en la dirección IP de la visita. |
| m_geo_region | placeContext.geo.stateProvince | string | Nombre del estado o región de la visita. Se basa en la dirección IP de la visita. |
| m_geo_zip | placeContext.geo.postalCode | string | El código postal de la visita. Se basa en la dirección IP de la visita. |
| m_keywords | search.keywords | string | La variable utilizada en la dimensión Palabra clave. |
| m_os | _experience.analytics.environment.OperatingSystemID | integer | ID numérica que representa el sistema operativo del visitante. Esto se basa en la columna user_agent . |
| m_page_url | web.webPageDetails.URL | string | Dirección URL de la visita individual a la página. |
| m_pagename_no_url | web.webPageDetails.</span>name | string | Variable utilizada para rellenar la dimensión Páginas . |
| m_referrer | web.webReferrer.URL | string | La dirección URL de la página anterior. |
| m_search_page_num | search.pageDepth | integer | Lo utiliza la dimensión Rango de todas las páginas de búsqueda. Indica en qué página de resultados de búsqueda apareció su sitio antes de que el usuario hiciera clic para acceder a su sitio. |
| m_state | _experience.analytics.customDimensions.stateProvincia | string | Variable de estado. |
| m_user_server | web.webPageDetails.server | string | Variable utilizada en la dimensión Servidor . |
| m_zip | _experience.analytics.customDimensions.postalCode | string | Variable utilizada para rellenar la dimensión Código postal . |
| accept_language | environment.browserDetails.acceptLanguage | string | Enumera todos los idiomas aceptados, tal como se indica en el encabezado Accept-Language-HTTP. |
| homepage | web.webPageDetails.isHomePage | Booleano | Ya no se utiliza. Se indica si la dirección URL actual es la página principal del explorador. |
| ipv6 | environment.ipV6 | string |
| j_jscript | environment.browserDetails.javaScriptVersion | string | Versión de JavaScript admitida por el explorador. |
| user_agent | environment.browserDetails.userAgent | string | La cadena del agente de usuario enviada en el encabezado HTTP. |
| mobileappid | aplicación.</span>name | string | El ID de la aplicación móvil, almacenado en el siguiente formato: `[AppName][BundleVersion]`. |
| mobiledevice | device.model | string | Nombre del dispositivo móvil. En iOS, se almacena como una cadena de dos dígitos separados por comas. El primer número representa la generación del dispositivo y el segundo representa la familia del dispositivo. |
| pointofinterest | placeContext.POIinteraction.POIDetail.</span>name | string | Utilizado por los servicios móviles. Representa el punto de interés. |
| pointofinterestdistance | placeContext.POIinteraction.POIDetail.geoInteractionDetails.distanceToCenter | entero | Utilizado por los servicios móviles. Representa la distancia del punto de interés. |
| mobileplaceaccuracy | placeContext.POIinteraction.POIDetail.geoInteractionDetails.deviceGeoAccuracy | entero | Recopilado desde la variable de datos de contexto a.loc.acc. Indica la precisión del GPS en metros en el momento de la recogida. |
| mobileplacecategory | placeContext.POIinteraction.POIDetail.category | string | Recopilado desde la variable de datos de contexto a.loc.category. Describe la categoría de un lugar específico. |
| mobileplaceid | placeContext.POIinteraction.POIDetail.POIID | string | Recopilado desde la variable de datos de contexto a.loc.id. Identificador de un punto de interés determinado. |
| vídeo | media.mediaTimed.primaryAssetReference._id | string | Nombre del vídeo. |
| videoad | advertising.adAssetReference._id | string | Identificador del recurso publicitario. |
| videocontenttype | media.mediaTimed.primaryAssetViewDetails.broadcastContentType | string | El Tipo De Contenido Del Vídeo. Se establece automáticamente como &quot;Vídeo&quot; para todas las vistas de vídeo. |
| videoadpod | advertising.adAssetViewDetails.adBreak._id | string | El pod en el que se encuentra el anuncio de vídeo. |
| videoadinpod | advertising.adAssetViewDetails.index | integer | Posición en la que se encuentra el anuncio de vídeo en el pod. |
| videoplayername | media.mediaTimed.primaryAssetViewDetails.playerName | string | Nombre del reproductor de vídeo. |
| videochannel | media.mediaTimed.primaryAssetViewDetails.broadcastChannel | string | El canal de vídeo. |
| videoadplayername | advertising.adAssetViewDetails.playerName | string | Nombre del reproductor del anuncio de vídeo. |
| videochapter | media.mediaTimed.mediaChapter.chapterAssetReference._id | string | El nombre del capítulo del vídeo |
| videoname | media.mediaTimed.primaryAssetReference._dc.title | string | El nombre del vídeo. |
| videoadname | advertising.adAssetReference._dc.title | string | Nombre del anuncio de vídeo. |
| videoshow | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Series._iptc4xmpExt.Name | string | Programa del vídeo. |
| videoseason | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Season._iptc4xmpExt.Name | string | Temporada del vídeo. |
| videoepisode | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Episode._iptc4xmpExt.Name | string | Episodio del vídeo. |
| videonetwork | media.mediaTimed.primaryAssetViewDetails.broadcastNetwork | string | Red del vídeo. |
| videoshowtype | media.mediaTimed.primaryAssetReference.showType | string | Tipo de programa del vídeo. |
| videoadload | media.mediaTimed.primaryAssetViewDetails.adLoadType | string | Cargas del anuncio de vídeo. |
| videofeedtype | media.mediaTimed.primaryAssetViewDetails.sourceFeed | string | Tipo de fuente de vídeo. |
| mobilebeaconmajor | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.beaconMajor | entero | Señalización principal de Mobile Services. |
| mobilebeaconminor | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.beaconMinor | entero | Señalización menor de Mobile Services. |
| mobilebeaconuuid | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.proximityUUID | string | UUID de señalización de Mobile Services. |
| videosessionid | media.mediaTimed.primaryAssetViewDetails._id | string | ID de sesión de vídeo. |
| videogenre | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Genre | matriz | Género del vídeo. | {title (Object), description (Object), type (Object), meta:xdmType (Object), items (string), meta:xdmField (Object)} |
| mobileinstalls | application.firstLaunches | Objeto | Esto se activa en la primera ejecución después de la instalación o reinstalación | {id (cadena), valor (número)} |
| mobileupgrades | application.upgrades | Objeto | Notifica el número de actualizaciones de aplicaciones. Déclencheur en la primera ejecución después de la actualización o cada vez que cambie el número de versión. | {id (cadena), valor (número)} |
| mobilelaunches | application.launches | Objeto | Número de veces que se ha iniciado la aplicación. | {id (cadena), valor (número)} |
| mobilecrashes | application.crashes | Objeto | <!-- MISSING --> | {id (cadena), valor (número)} |
| mobilemessageclicks | directMarketing.clicks | Objeto | <!-- MISSING --> | {id (cadena), valor (número)} |
| mobileplaceentry | placeContext.POIinteraction.poiEntries | Objeto | <!-- MISSING --> | {id (cadena), valor (número)} |
| mobileplaceexit | placeContext.POIinteraction.poiExits | Objeto | <!-- MISSING --> | {id (cadena), valor (número)} |
| videotime | media.mediaTimed.timePlayed | Objeto | <!-- MISSING --> | {id (cadena), valor (número)} |
| videostart | media.mediaTimed.impressions | Objeto | <!-- MISSING --> | {id (cadena), valor (número)} |
| videocomplete | media.mediaTimed.completes | Objeto | <!-- MISSING --> | {id (cadena), valor (número)} |
| videosegmentviews | media.mediaTimed.mediaSegmentViews | Objeto | <!-- MISSING --> | {id (cadena), valor (número)} |
| videoadstart | advertising.impressions | Objeto | <!-- MISSING --> | {id (cadena), valor (número)} |
| videoadcomplete | advertising.completes | Objeto | <!-- MISSING --> | {id (cadena), valor (número)} |
| videoadtime | advertising.timePlayed | Objeto | <!-- MISSING --> | {id (cadena), valor (número)} |
| videochapterstart | media.mediaTimed.mediaChapter.impressions | Objeto | <!-- MISSING --> | {id (cadena), valor (número)} |
| videochaptercomplete | media.mediaTimed.mediaChapter.completes | Objeto | <!-- MISSING --> | {id (cadena), valor (número)} |
| videochaptertime | media.mediaTimed.mediaChapter.timePlayed | Objeto | <!-- MISSING --> | {id (cadena), valor (número)} |
| videoplay | media.mediaTimed.starts | Objeto | <!-- MISSING --> | {id (cadena), valor (número)} |
| videototaltime | media.mediaTimed.totalTimePlayed | Objeto | <!-- MISSING --> | {id (cadena), valor (número)} |
| videoqoetimetostart | media.mediaTimed.primaryAssetViewDetails.qoe.timeToStart | Objeto | El tiempo de calidad de vídeo para el inicio. | {id (cadena), valor (número)} |
| videoqoedropbeforestart | media.mediaTimed.dropBeforeStarts | Objeto | <!-- MISSING --> | {id (cadena), valor (número)} |
| videoqoebuffercount | media.mediaTimed.primaryAssetViewDetails.qoe.buffers | Objeto | Recuento de búferes en la calidad de vídeo | {id (cadena), valor (número)} |
| videoqoebuffertime | media.mediaTimed.primaryAssetViewDetails.qoe.bufferTime | Objeto | Hora de búfer de la calidad de vídeo | {id (cadena), valor (número)} |
| videoqoebitratechangecount | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateChanges | Objeto | Recuento de cambios en la calidad de vídeo | {id (cadena), valor (número)} |
| videoqoebitrateaverage | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateAverage | Objeto | Tasa de bits promedio de la calidad de vídeo | {id (cadena), valor (número)} |
| videoqoeerrorcount | media.mediaTimed.primaryAssetViewDetails.qoe.errors | Objeto | Recuento de errores de calidad de vídeo | {id (cadena), valor (número)} |
| videoqoedroppedframecount | media.mediaTimed.primaryAssetViewDetails.qoe.droppedFrames | Objeto | <!-- MISSING --> | {id (cadena), valor (número)} |
| videoprogress10 | media.mediaTimed.progress10 | Objeto | <!-- MISSING --> | {id (cadena), valor (número)} |
| videoprogress25 | media.mediaTimed.progress25 | Objeto | <!-- MISSING --> | {id (cadena), valor (número)} |
| videoprogress50 | media.mediaTimed.progress50 | Objeto | <!-- MISSING --> | {id (cadena), valor (número)} |
| videoprogress75 | media.mediaTimed.progress75 | Objeto | <!-- MISSING --> | {id (cadena), valor (número)} |
| videoprogress95 | media.mediaTimed.progress95 | Objeto | <!-- MISSING --> | {id (cadena), valor (número)} |
| videoresume | media.mediaTimed.resumes | Objeto | <!-- MISSING --> | {id (cadena), valor (número)} |
| videopausecount | media.mediaTimed.pauses | Objeto | <!-- MISSING --> | {id (cadena), valor (número)} |
| videopausetime | media.mediaTimed.pauseTime | Objeto | <!-- MISSING --> | {id (cadena), valor (número)} |
| videoSecondssincelastcall | media.mediaTimed.primaryAssetViewDetails.sessionTimeout | integer |

{style=&quot;table-layout:auto&quot;}

## Dividir campos de asignación

Estos campos tienen un único origen, pero se asignan a **múltiple** Ubicaciones XDM.

| Campo de Analytics | Campo XDM | Tipo XDM | Descripción |
| --------------- | --------- | -------- | ---------- |
| s_resolution | device.screenWidth, device.screenHeight | integer | ID numérico que representa la resolución del monitor. |
| mobileosversion | environment.operationSystem, environment.operationSystemVersion | string | Versión del sistema operativo del dispositivo móvil. |
| videoadlength | advertising.adAssetReference._xmpDM.duration | integer | Duración del anuncio de vídeo. |

{style=&quot;table-layout:auto&quot;}

## Campos de asignación generados

Los campos seleccionados procedentes de ADC deben transformarse, lo que requiere lógica más allá de una copia directa de Adobe Analytics para que se genere en XDM.

La tabla siguiente incluye columnas que muestran el nombre del campo Analytics (*Campo de Analytics*), el campo XDM correspondiente (*Campo XDM*) y su tipo (*Tipo XDM*), así como una descripción del campo (*Descripción*).

>[!NOTE]
>
>Desplácese a la izquierda/derecha para ver todo el contenido de la tabla.

| Campo de Analytics | Campo XDM | Tipo XDM | Descripción |
| --------------- | --------- | -------- | ----------- |
| m_prop1 - m_prop75 | _experience.analytics.customDimensions.listprops.prop1 - _experience.analytics.customDimensions.listprops.prop75 | Objeto | Variables de tráfico personalizadas que varían de 1 a 75 | {} |
| m_hier1 - m_hier5 | _experience.analytics.customDimensions.hierarchy.hier1 - _experience.analytics.customDimensions.hierarchy.hier5 | Objeto | Utilizado por variables de jerarquía. Contiene un | lista delimitada de valores. | {valores (matriz), delimitador (cadena)} |
| m_mvvar1 - m_mvvar3 | _experience.analytics.customDimensions.lists.list1.list[] - _experience.analytics.customDimensions.lists.list3.list[] | matriz | Lista de valores de variables. Contiene una lista delimitada de valores personalizados, según la implementación | {valor (cadena), clave (cadena)} |
| m_color | device.colorDepth | integer | El ID de profundidad de color, que se basa en el valor de la columna c_color. |
| m_cookies | environment.browserDetails.cookiesEnabled | Booleano | Variable utilizada en la dimensión Compatibilidad con cookies . |
| m_event_list | commerce.purchases, commerce.productViews, commerce.productListOpens, commerce.checkouts, commerce.productListAdd, commerce.productListRemovals, commerce.productListViews | Objeto | Eventos comerciales estándar activados en la visita. | {id (cadena), valor (número)} |
| m_event_list | _experience.analytics.event1to100.event1 - _experience.analytics.event1to100.event100, _experience.analytics.event101to200.event101 - _experience.analytics.event101to200.event200 , _experience.analytics.event201to300.event201 - _experience.analytics.event201to300.event300, _experience.analytics.event301to400.event301 - _experience.analytics.event30 1to400.event400, _experience.analytics.event401to500.event401 - _experience.analytics.event401to500.event500, _experience.analytics.event501to600.event5 01 - _experience.analytics.event501to600.event600, _experience.analytics.event601to700.event601 - _experience.analytics.event601to700.event700, _experience.analytics.event7 01to800.event701 - _experience.analytics.event701to800.event800, _experience.analytics.event801to900.event801 - _experience.analytics.event801to900.event 900, _experience.analytics.event901to1000.event901 - _experience.analytics.event901to1000.event1000 | Objeto | Eventos personalizados activados en la visita. | {id (objeto), valor (objeto)} |
| m_geo_country | placeContext.geo.countryCode | string | Abreviación del país de donde provino la visita, que se basa en la dirección IP. |
| m_geo_latitude | placeContext.geo._schema.latitude | entero | <!-- MISSING --> |
| m_geo_longitude | placeContext.geo._schema.longitude | entero | <!-- MISSING --> |
| m_java_enabled | environment.browserDetails.javaEnabled | Booleano | Un indicador que indica si Java está habilitado. |
| m_latitude | placeContext.geo._schema.latitude | entero | <!-- MISSING --> |
| m_longitude | placeContext.geo._schema.longitude | entero | <!-- MISSING --> |
| m_page_event_var1 | web.webInteraction.URL | string | Variable que solo se utiliza en solicitudes de imagen de seguimiento de vínculos. Esta variable contiene la dirección URL del vínculo de descarga, de salida o personalizado en el que se hizo clic. |
| m_page_event_var2 | web.webInteraction.name | string | Variable que solo se utiliza en solicitudes de imagen de seguimiento de vínculos. Muestra el nombre personalizado del vínculo, si se especifica. |
| m_page_type | web.webPageDetails.isErrorPage | Booleano | Variable que se utiliza para rellenar la dimensión Páginas no encontradas . Esta variable debe estar vacía o contener &quot;ErrorPage&quot;. |
| m_pagename_no_url | web.webPageDetails.pageViews.value | entero | El nombre de la página (si está configurado). Si no se especifica ninguna página, este valor se deja vacío. |
| m_paid_search | search.isPaid | Booleano | Un indicador que se establece si la visita coincide con la detección de búsquedas de pago. |
| m_product_list | productListItems[].items | matriz | La lista de productos, tal como se transfiere a través de la variable products . | {SKU (cadena), cantidad (total), priceTotal (número)} |
| m_ref_type | web.webReferrer.type | string | Una ID numérica que representa el tipo de referente de la visita. 1 significa que dentro del sitio, 2 significa otros sitios web, 3 significa motores de búsqueda, 4 significa disco duro, 5 significa USENET, 6 significa Escritos o marcadores (sin referente), 7 significa correo electrónico, 8 significa Sin JavaScript y 9 significa Redes sociales. |
| m_search_engine | search.searchEngine | string | ID numérica que representa el motor de búsqueda que ha llevado al visitante a su sitio. |
| post_currency | commerce.order.currencyCode | string | El código de moneda que se ha utilizado durante la transición. |
| post_cust_hit_time_gmt | timestamp | string | Esto solo se utiliza en conjuntos de datos con marca de tiempo habilitada. Esta es la marca de tiempo que se envía con ella, en función de la hora Unix. |
| post_cust_visid | identityMap | object | El ID de visitante del cliente. |
| post_cust_visid | endUserIDs._experience.aacustomid.primary | Booleano | El ID de visitante del cliente. |
| post_cust_visid | endUserIDs._experience.aacustomid.namespace.code | string | El ID de visitante del cliente. |
| post_visid_high + visid_low | identityMap | object | Identificador único de una visita. |
| post_visid_high + visid_low | endUserIDs._experience.aaid.id | string | Identificador único de una visita. |
| post_visid_high | endUserIDs._experience.aaid.primary | Booleano | Se utiliza junto con visid_low para identificar una visita de forma exclusiva. |
| post_visid_high | endUserIDs._experience.aaid.namespace.code | string | Se utiliza junto con visid_low para identificar una visita de forma exclusiva. |
| post_visid_low | identityMap | object | Se utiliza junto con visid_high para identificar una visita de forma exclusiva. |
| hit_time_gmt | receivedTimestamp | string | La marca de tiempo de la visita, basada en el tiempo Unix. |
| hitid_high + hitid_low | _id | string | Identificador único para identificar una visita. |
| hitid_low | _id | string | Se utiliza junto con hitid_high para identificar una visita de forma exclusiva. |
| ip | environment.ipV4 | string | La dirección IP, basada en el encabezado HTTP de la solicitud de imagen. |
| j_jscript | environment.browserDetails.javaScriptEnabled | Booleano | Versión de JavaScript utilizada. |
| mcvisid_high + mcvisid_low | identityMap | object | El ID de visitante del Experience Cloud. |
| mcvisid_high + mcvisid_low | endUserIDs._experience.mcid.id | string | El ID de visitante del Experience Cloud. |
| mcvisid_high | endUserIDs._experience.mcid.primary | Booleano | El ID de visitante del Experience Cloud. |
| mcvisid_high | endUserIDs._experience.mcid.namespace.code | string | El ID de visitante del Experience Cloud. |
| mcvisid_low | identityMap | object | El ID de visitante del Experience Cloud. |
| sdid_high + sdid_low | _experience.target.complementDataID | string | ID de vinculación de visitas. El campo de análisis sdid_high y sdid_low es el id de datos suplementario que se utiliza para unir dos o más visitas entrantes. |
| mobilebeaconproximity | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.proximity | string | Proximidad de la señalización de Mobile Services. |
| videochapter | media.mediaTimed.mediaChapter.chapterAssetReference._xmpDM.duration | integer | Nombre del capítulo del vídeo. |
| videolength | media.mediaTimed.primaryAssetReference._xmpDM.duration | integer | Duración del vídeo. |

{style=&quot;table-layout:auto&quot;}

## Campos de asignación avanzados

Los campos seleccionados (conocidos como &quot;postvalues&quot;) requieren transformaciones más avanzadas para poder asignarlos correctamente de los campos de Adobe Analytics al Modelo de datos de experiencia (XDM). Para realizar estas transformaciones avanzadas es necesario utilizar el servicio de consulta de Adobe Experience Platform y las funciones prediseñadas (denominadas funciones definidas por Adobe) para la sesionización, atribución y deduplicación.

Para obtener más información sobre cómo realizar estas transformaciones mediante el servicio de consulta, visite la [Funciones definidas por Adobe](../../../../query-service/sql/adobe-defined-functions.md) documentación.

La tabla siguiente incluye columnas que muestran el nombre del campo Analytics (*Campo de Analytics*), el campo XDM correspondiente (*Campo XDM*) y su tipo (*Tipo XDM*), así como una descripción del campo (*Descripción*).

>[!NOTE]
>
>Desplácese a la izquierda/derecha para ver todo el contenido de la tabla.

| Campo de Analytics | Campo XDM | Tipo XDM | Descripción |
| --------------- | --------- | -------- | ---------- |
| post_evar1 - post_evar250 | _experience.analytics.customDimensions.eVars.eVar1 - _experience.analytics.customDimensions.eVars.eVar250 | string | Variable personalizada, que puede oscilar entre 1 y 250. Cada organización utilizará estas eVars personalizadas de forma diferente. |
| post_prop1 - post_prop75 | _experience.analytics.customDimensions.props.prop1 - _experience.analytics.customDimensions.props.prop75 | string | Variables de tráfico personalizadas, que pueden oscilar entre 1 y 75. |
| post_browser_height | environment.browserDetails.viewportHeight | integer | Altura del explorador, en píxeles. |
| post_browser_width | environment.browserDetails.viewportWidth | integer | Anchura del explorador, en píxeles. |
| post_campaign | marketing.trackingCode | string | La variable utilizada en la dimensión Código de seguimiento . |
| post_channel | web.webPageDetails.siteSection | string | La variable utilizada en la dimensión Secciones del sitio. |
| post_cust_visid | endUserIDs._experience.aacustomid.id | string | El ID de visitante personalizado, si está establecido. |
| post_first_hit_page_url | _experience.analytics.endUser.firstWeb.webPageDetails.URL | string | Dirección URL de la primera página a la que llega el visitante. |
| post_first_hit_pagename | _experience.analytics.endUser.firstWeb.webPageDetails.name | string | Variable utilizada en la dimensión Página de entrada original . El nombre de la página de entrada del visitante. |
| post_keywords | search.keywords | string | Las palabras clave que se recopilaron para la visita. |
| post_page_url | web.webPageDetails.URL | string | Dirección URL de la visita individual a la página. |
| post_pagename_no_url | web.webPageDetails.name | string | Variable utilizada para rellenar la dimensión Páginas . |
| post_purchaseid | commerce.order.purchaseID | string | Variable que se utiliza para identificar compras de forma única. |
| post_referrer | web.webReferrer.URL | string | La dirección URL de la página anterior. |
| post_state | _experience.analytics.customDimensions.stateProvincia | string | Variable de estado. |
| post_user_server | web.webPageDetails.server | string | Variable utilizada en la dimensión Servidor . |
| post_zip | _experience.analytics.customDimensions.postalCode | string | Variable utilizada para rellenar la dimensión Código postal . |
| explorador | _experience.analytics.environment.browserID | integer | El ID numérico del explorador. |
| domain | environment.domain | string | La variable utilizada en la dimensión Dominio . Esto se basa en el proveedor de servicios de Internet (ISP) del usuario. |
| first_hit_referrer | _experience.analytics.endUser.firstWeb.webReferrer.URL | string | La primera URL de referencia para el visitante. |
| geo_city | placeContext.geo.city | string | Nombre de la ciudad de la visita. Se basa en la dirección IP de la visita. |
| geo_dma | placeContext.geo.dmaID | integer | ID numérico del área demográfica de la visita. Se basa en la dirección IP de la visita. |
| geo_region | placeContext.geo.stateProvince | string | Nombre del estado o región de la visita. Se basa en la dirección IP de la visita. |
| geo_zip | placeContext.geo.postalCode | string | El código postal de la visita. Se basa en la dirección IP de la visita. |
| os | _experience.analytics.environment.OperatingSystemID | integer | ID numérica que representa el sistema operativo del visitante. Esto se basa en la columna user_agent . |
| search_page_num | search.pageDepth | integer | Esta variable la utiliza la dimensión Clasificación de todas las páginas de búsqueda e indica qué página de resultados de búsqueda tiene su sitio | aparecía antes de que el usuario hiciera clic en el sitio. |
| visit_keywords | _experience.analytics.session.search.keywords | string | Variable utilizada en la dimensión Palabras clave de búsqueda. |
| visit_num | _experience.analytics.session.num | integer | Variable utilizada en la dimensión Número de visita. Esto comienza en 1 y aumenta cada vez que se inicia una nueva visita (por usuario). |
| visit_page_num | _experience.analytics.session.depth | integer | Variable utilizada en la dimensión Profundidad de visita . Este valor aumenta en 1 por cada visita que genera el usuario y se restablece después de cada visita. |
| visit_referrer | _experience.analytics.session.web.webReferrer.URL | string | El primer referente de la visita. |
| visit_search_page_num | _experience.analytics.session.search.pageDepth | integer | El primer nombre de página de la visita. |
| post_prop1 - post_prop75 | _experience.analytics.customDimensions.listprops.prop1 - _experience.analytics.customDimensions.listprops.prop75 | Objeto | Variables de tráfico personalizadas 1-75. |
| post_hier1 - post_hier5 | _experience.analytics.customDimensions.hierarchy.hier1 - _experience.analytics.customDimensions.hierarchy.hier5 | Objeto | Lo utilizan las variables de jerarquía y contiene una lista delimitada de valores. | {valores (matriz), delimitador (cadena)} |
| post_mvvar1 - post_mvvar3 | _experience.analytics.customDimensions.lists.list1.list[] - _experience.analytics.customDimensions.lists.list3.list[] | matriz | Una lista de valores de variables. Contiene una lista delimitada de valores personalizados, según la implementación. | {valor (cadena), clave (cadena)} |
| post_cookies | environment.browserDetails.cookiesEnabled | Booleano | Variable utilizada en la dimensión Compatibilidad con cookies. |
| post_event_list | commerce.purchases, commerce.productViews, commerce.productListOpens, commerce.checkouts, commerce.productListAdd, commerce.productListRemovals, commerce.productListViews | Objeto | Eventos comerciales estándar activados en la visita. | {id (cadena), valor (número)} |
| post_event_list | _experience.analytics.event1to100.event1 - _experience.analytics.event1to100.event100, _experience.analytics.event101to200.event101 - _experience.analytics.event101to200.event200 , _experience.analytics.event201to300.event201 - _experience.analytics.event201to300.event300, _experience.analytics.event301to400.event301 - _experience.analytics.event30 1to400.event400, _experience.analytics.event401to500.event401 - _experience.analytics.event401to500.event500, _experience.analytics.event501to600.event5 01 - _experience.analytics.event501to600.event600, _experience.analytics.event601to700.event601 - _experience.analytics.event601to700.event700, _experience.analytics.event7 01to800.event701 - _experience.analytics.event701to800.event800, _experience.analytics.event801to900.event801 - _experience.analytics.event801to900.event 900, _experience.analytics.event901to1000.event901 - _experience.analytics.event901to1000.event1000 | Objeto | Eventos personalizados activados en la visita. | {id (objeto), valor (objeto)} |
| post_java_enabled | environment.browserDetails.javaEnabled | Booleano | Un indicador que indica si Java está habilitado. |
| post_latitude | placeContext.geo._schema.latitude | entero | <!-- MISSING --> |
| post_longitude | placeContext.geo._schema.longitude | entero | <!-- MISSING --> |
| post_page_event | web.webInteraction.type | string | El tipo de visita que se envía en la solicitud de imagen (visita estándar, vínculo de descarga, vínculo de salida o vínculo personalizado en el que se hizo clic). |
| post_page_event | web.webInteraction.linkClicks.value | entero | El tipo de visita que se envía en la solicitud de imagen (visita estándar, vínculo de descarga, vínculo de salida o vínculo personalizado en el que se hizo clic). |
| post_page_event_var1 | web.webInteraction.URL | string | Esta variable solo se utiliza en solicitudes de imagen de seguimiento de vínculos. Esta es la dirección URL del vínculo de descarga, de salida o personalizado en el que se hizo clic. |
| post_page_event_var2 | web.webInteraction.name | string | Esta variable solo se utiliza en solicitudes de imagen de seguimiento de vínculos. Será el nombre personalizado del vínculo. |
| post_page_type | web.webPageDetails.isErrorPage | Booleano | Se utiliza para rellenar la dimensión Páginas no encontradas . Esta variable debe estar vacía o contener &quot;ErrorPage&quot; |
| post_pagename_no_url | web.webPageDetails.pageViews.value | entero | El nombre de la página (si está configurado). Si no se especifica ninguna página, este valor se deja vacío. |
| post_product_list | productListItems[].items | matriz | La lista de productos, tal como se transfiere a través de la variable products . | {SKU (cadena), cantidad (total), priceTotal (número)} |
| post_search_engine | search.searchEngine | string | ID numérica que representa el motor de búsqueda que ha llevado al visitante a su sitio. |
| mvvar1_instances | .list.items[] | Objeto | Lista de valores de variables. Contiene una lista delimitada de valores personalizados, según la implementación. |
| mvvar2_instances | .list.items[] | Objeto | Lista de valores de variables. Contiene una lista delimitada de valores personalizados, según la implementación. |
|  | mvvar3_instances | .list.items[] | Objeto | Lista de valores de variables. Contiene una lista delimitada de valores personalizados, según la implementación. |
| color | device.colorDepth | integer | ID de profundidad de color, según el valor de la columna c_color. |
| first_hit_ref_type | _experience.analytics.endUser.firstWeb.webReferrer.type | string | El ID numérico, que representa el tipo de referente del primer referente del visitante. |
| first_hit_time_gmt | _experience.analytics.endUser.firstTimestamp | integer | Marca de tiempo de la primera visita del visitante en Tiempo Unix. |
| geo_country | placeContext.geo.countryCode | string | Abreviatura del país del que provino la visita basada en la dirección IP. |
| geo_latitude | placeContext.geo._schema.latitude | entero | <!-- MISSING --> |
| geo_longitude | placeContext.geo._schema.longitude | entero | <!-- MISSING --> |
| paid_search | search.isPaid | Booleano | Un indicador que se establece si la visita coincide con la detección de búsquedas de pago. |
| ref_type | web.webReferrer.type | string | Una ID numérica que representa el tipo de referente de la visita. |
| visit_paid_search | _experience.analytics.session.search.isPaid | Booleano | Un indicador (1=pagado, 0=no pagado) que indica si la primera visita individual de la visita procede de una visita de búsqueda paga. |
| visit_ref_type | _experience.analytics.session.web.web.webReferrer.type | string | ID numérica que representa el tipo de referente del primer referente de la visita. |
| visit_search_engine | _experience.analytics.session.search.searchEngine | string | ID numérica del primer motor de búsqueda de la visita. |
| visit_start_time_gmt | _experience.analytics.session.timestamp | integer | Marca de tiempo de la primera visita individual de la visita en Tiempo Unix. |

{style=&quot;table-layout:auto&quot;}