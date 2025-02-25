---
keywords: campos de asignación de Analytics;asignación de Analytics
solution: Experience Platform
title: Asignación de campos para el conector de Adobe Analytics Source
description: Asigne campos de Adobe Analytics a campos XDM mediante el conector de Source de Analytics.
exl-id: 15dc1368-5cf1-42e1-9683-d5158f8aa2db
source-git-commit: 15d63db308ea9d2daf7660b463785d04ff94e296
workflow-type: tm+mt
source-wordcount: '2415'
ht-degree: 8%

---

# Asignaciones de campos de Analytics

Adobe Experience Platform le permite introducir datos de Adobe Analytics a través de la fuente de Analytics. Algunos de los datos introducidos a través de ADC se pueden asignar directamente desde campos de Analytics a campos del modelo de datos de experiencia (XDM), mientras que otros datos requieren transformaciones y funciones específicas para asignarse correctamente.

![](../images/analytics-data-experience-platform.png)

## Campos de asignación directa

Los campos seleccionados se asignan directamente de Adobe Analytics al modelo de datos de experiencia (XDM).

| Campo de Analytics | Campo XDM | Tipo de XDM | Descripción |
| --------------- | --------- | -------- | ---------- |
| `m_evar1`<br/>`[...]`<br/>`m_evar250` | `_experience.analytics.customDimensions.`<br/>`eVars.eVar1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`eVars.eVar250` | cadena | eVars de Analytics personalizadas. Cada organización puede utilizar eVars de forma diferente. |
| `m_prop1`<br/>`[...]`<br/>`m_prop75` | `_experience.analytics.customDimensions.`<br/>`props.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`props.prop75` | cadena | Propiedades personalizadas de Analytics. Cada organización puede utilizar props de forma diferente. |
| `m_browser` | `_experience.analytics.environment.`<br/>`browserID` | entero | El ID de número del explorador. |
| `m_browser_height` | `environment.browserDetails.viewportHeight` | entero | Altura del explorador, en píxeles. |
| `m_browser_width` | `environment.browserDetails.viewportWidth` | entero | Anchura del explorador, en píxeles. |
| `m_campaign` | `marketing.trackingCode` | cadena | La variable utilizada en la dimensión Código de seguimiento. |
| `m_channel` | `web.webPageDetails.siteSection` | cadena | La variable utilizada en la dimensión Secciones del sitio. |
| `m_domain` | `environment.domain` | cadena | La variable utilizada en la dimensión Dominio. Se basa en el proveedor de servicios de Internet (ISP) del usuario. |
| `m_geo_city` | `placeContext.geo.city` | cadena | El nombre de la ciudad de la visita. Se basa en la dirección IP de la visita. |
| `m_geo_dma` | `placeContext.geo.dmaID` | entero | El ID numérico del área demográfica de la visita. Se basa en la dirección IP de la visita. |
| `m_geo_region` | `placeContext.geo.stateProvince` | cadena | El nombre del estado o la región de la visita. Se basa en la dirección IP de la visita. |
| `m_geo_zip` | `placeContext.geo.postalCode` | cadena | El código postal de la visita. Se basa en la dirección IP de la visita. |
| `m_keywords` | `search.keywords` | cadena | La variable utilizada en la dimensión Palabra clave. |
| `m_os` | `_experience.analytics.environment.`<br/>`operatingSystemID` | entero | ID numérica que representa el sistema operativo del visitante. Se basa en la columna user_agent. |
| `m_page_url` | `web.webPageDetails.URL` | cadena | La URL de la visita individual a la página. |
| `m_pagename` | `web.webPageDetails.pageViews.value` | cadena | Es igual a 1 en visitas que tienen un nombre de página. Esto es similar a la métrica Vistas de página de Adobe Analytics. |
| `m_referrer` | `web.webReferrer.URL` | cadena | Dirección URL de la página anterior. |
| `m_search_page_num` | `search.pageDepth` | entero | Lo utiliza la dimensión Rango de todas las páginas de búsqueda. Indica en qué página de resultados de búsqueda apareció su sitio antes de que el usuario hiciera clic para acceder a su sitio. |
| `m_state` | `_experience.analytics.customDimensions.`<br/>`stateProvince` | cadena | Variable de estado. |
| `m_user_server` | `web.webPageDetails.server` | cadena | Variable utilizada en la dimensión Servidor. |
| `m_zip` | `_experience.analytics.customDimensions.`<br/>`postalCode` | cadena | Variable utilizada para rellenar la dimensión Código postal. |
| `accept_language` | `environment.browserDetails.acceptLanguage` | cadena | Enumera todos los idiomas aceptados, tal como se indica en la cabecera Accept-Language-HTTP. |
| `homepage` | `web.webPageDetails.isHomePage` | Booleano | Ya no se utiliza. Se indica si la dirección URL actual es la página principal del explorador. |
| `ipv6` | `environment.ipV6` | cadena |
| `j_jscript` | `environment.browserDetails.javaScriptVersion` | cadena | La versión de JavaScript admitida por el explorador. |
| `user_agent` | `environment.browserDetails.userAgent` | cadena | La cadena del agente de usuario enviada en el encabezado HTTP. |
| `mobileappid` | `application.name` | cadena | El id. de la aplicación móvil, almacenado en el siguiente formato: `[AppName][BundleVersion]`. |
| `mobiledevice` | `device.model` | cadena | Nombre del dispositivo móvil. En iOS, se almacena como una cadena de 2 dígitos separados por comas. El primer número representa la generación del dispositivo y el segundo número representa la familia del dispositivo. |
| `pointofinterest` | `placeContext.POIinteraction.POIDetail.`<br/>`name` | cadena | Utilizado por Mobile Services. Representa el punto de interés. |
| `pointofinterestdistance` | `placeContext.POIinteraction.POIDetail.`<br/>`geoInteractionDetails.distanceToCenter` | número | Utilizado por Mobile Services. Representa la distancia del punto de interés. |
| `mobileplaceaccuracy` | `placeContext.POIinteraction.POIDetail.`<br/>`geoInteractionDetails.deviceGeoAccuracy` | número | Recopilado desde la variable de datos de contexto a.loc.acc. Indica la precisión del GPS en metros en el momento de la recogida. |
| `mobileplacecategory` | `placeContext.POIinteraction.POIDetail.`<br/>`category` | cadena | Recopilado desde la variable de datos de contexto a.loc.category. Describe la categoría de un lugar específico. |
| `mobileplaceid` | `placeContext.POIinteraction.POIDetail.`<br/>`POIID` | cadena | Recopilado desde la variable de datos de contexto a.loc.id. Identificador de un punto de interés determinado. |
| `video` | `media.mediaTimed.primaryAssetReference.`<br/>`_id` | cadena | Nombre del vídeo. |
| `videoad` | `advertising.adAssetReference._id` | cadena | Identificador del recurso publicitario. |
| `videocontenttype` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`broadcastContentType` | cadena | El Tipo De Contenido Del Vídeo. Se establece automáticamente como &quot;Vídeo&quot; para todas las vistas de vídeo. |
| `videoadpod` | `advertising.adAssetViewDetails.adBreak._id` | cadena | El pod en el que se encuentra el anuncio de vídeo. |
| `videoadinpod` | `advertising.adAssetViewDetails.index` | entero | La posición en la que se encuentra el anuncio de vídeo en la secuencia. |
| `videoplayername` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`playerName` | cadena | Nombre del reproductor de vídeo. |
| `videochannel` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`broadcastChannel` | cadena | El canal de vídeo. |
| `videoadplayername` | `advertising.adAssetViewDetails.playerName` | cadena | Nombre del reproductor del anuncio de vídeo. |
| `videochapter` | `media.mediaTimed.mediaChapter.`<br/>`chapterAssetReference._id` | cadena | Nombre del capítulo del vídeo |
| `videoname` | `media.mediaTimed.primaryAssetReference.`<br/>`_dc.title` | cadena | Nombre del vídeo. |
| `videoadname` | `advertising.adAssetReference._dc.title` | cadena | Nombre del anuncio de vídeo. |
| `videoshow` | `media.mediaTimed.primaryAssetReference.`<br/>`_iptc4xmpExt.Series._iptc4xmpExt.Name` | cadena | Muestra de vídeo. |
| `videoseason` | `media.mediaTimed.primaryAssetReference.`<br/>`_iptc4xmpExt.Season._iptc4xmpExt.Name` | cadena | Temporada de vídeos. |
| `videoepisode` | `media.mediaTimed.primaryAssetReference.`<br/>`_iptc4xmpExt.Episode._iptc4xmpExt.Name` | cadena | Episodio de vídeo. |
| `videonetwork` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`broadcastNetwork` | cadena | Red de vídeo. |
| `videoshowtype` | `media.mediaTimed.primaryAssetReference.`<br/>`showType` | cadena | Tipo de programa de vídeo. |
| `videoadload` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`adLoadType` | cadena | Se carga el anuncio de vídeo. |
| `videofeedtype` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`sourceFeed` | cadena | Tipo de fuente de vídeo. |
| `mobilebeaconmajor` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.beaconMajor` | número | Señalización principal de Mobile Services. |
| `mobilebeaconminor` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.beaconMinor` | número | Señalización menor de Mobile Services. |
| `mobilebeaconuuid` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.proximityUUID` | cadena | UUID de señalización de Mobile Services. |
| `videosessionid` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`_id` | cadena | ID de sesión de vídeo. |
| `videogenre` | `media.mediaTimed.primaryAssetReference.`<br/>`_iptc4xmpExt.Genre` | matriz | Género de vídeo. | {title (objeto), description (objeto), type (objeto), meta:xdmType (objeto), items (cadena), meta:xdmField (objeto)} |
| `mobileinstalls` | `application.firstLaunches` | Objeto | Se activa la primera vez que se ejecuta después de la instalación o reinstalación | {id (cadena), value (número)} |
| `mobileupgrades` | `application.upgrades` | Objeto | Notifica el número de actualizaciones de aplicaciones. Los déclencheur se ejecutan por primera vez después de la actualización o cada vez que cambia el número de versión. | {id (cadena), value (número)} |
| `mobilelaunches` | `application.launches` | Objeto | El número de veces que se ha iniciado la aplicación. | {id (cadena), value (número)} |
| `mobilecrashes` | `application.crashes` | Objeto | <!-- MISSING --> | {id (cadena), value (número)} |
| `mobilemessageclicks` | `directMarketing.clicks` | Objeto | <!-- MISSING --> | {id (cadena), value (número)} |
| `mobileplaceentry` | `placeContext.POIinteraction.poiEntries` | Objeto | <!-- MISSING --> | {id (cadena), value (número)} |
| `mobileplaceexit` | `placeContext.POIinteraction.poiExits` | Objeto | <!-- MISSING --> | {id (cadena), value (número)} |
| `videotime` | `media.mediaTimed.timePlayed` | Objeto | <!-- MISSING --> | {id (cadena), value (número)} |
| `videostart` | `media.mediaTimed.impressions` | Objeto | <!-- MISSING --> | {id (cadena), value (número)} |
| `videocomplete` | `media.mediaTimed.completes` | Objeto | <!-- MISSING --> | {id (cadena), value (número)} |
| `videosegmentviews` | `media.mediaTimed.mediaSegmentViews` | Objeto | <!-- MISSING --> | {id (cadena), value (número)} |
| `videoadstart` | `advertising.impressions` | Objeto | <!-- MISSING --> | {id (cadena), value (número)} |
| `videoadcomplete` | `advertising.completes` | Objeto | <!-- MISSING --> | {id (cadena), value (número)} |
| `videoadtime` | `advertising.timePlayed` | Objeto | <!-- MISSING --> | {id (cadena), value (número)} |
| `videochapterstart` | `media.mediaTimed.mediaChapter.`<br/>`impressions` | Objeto | <!-- MISSING --> | {id (cadena), value (número)} |
| `videochaptercomplete` | `media.mediaTimed.mediaChapter.`<br/>`completes` | Objeto | <!-- MISSING --> | {id (cadena), value (número)} |
| `videochaptertime` | `media.mediaTimed.mediaChapter.`<br/>`timePlayed` | Objeto | <!-- MISSING --> | {id (cadena), value (número)} |
| `videoplay` | `media.mediaTimed.starts` | Objeto | <!-- MISSING --> | {id (cadena), value (número)} |
| `videototaltime` | `media.mediaTimed.totalTimePlayed` | Objeto | <!-- MISSING --> | {id (cadena), value (número)} |
| `videoqoetimetostart` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.timeToStart` | Objeto | Hora de inicio de la calidad de vídeo. | {id (cadena), value (número)} |
| `videoqoedropbeforestart` | `media.mediaTimed.dropBeforeStarts` | Objeto | <!-- MISSING --> | {id (cadena), value (número)} |
| `videoqoebuffercount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.buffers` | Objeto | Recuento de búfer de calidad de vídeo | {id (cadena), value (número)} |
| `videoqoebuffertime` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bufferTime` | Objeto | Tiempo de búfer de calidad de vídeo | {id (cadena), value (número)} |
| `videoqoebitratechangecount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bitrateChanges` | Objeto | Recuento de cambios de calidad de vídeo | {id (cadena), value (número)} |
| `videoqoebitrateaverage` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bitrateAverage` | Objeto | Velocidad de bits promedio de calidad de vídeo | {id (cadena), value (número)} |
| `videoqoeerrorcount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.errors` | Objeto | Recuento de errores de calidad de vídeo | {id (cadena), value (número)} |
| `videoqoedroppedframecount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.droppedFrames` | Objeto | <!-- MISSING --> | {id (cadena), value (número)} |
| `videoprogress10` | `media.mediaTimed.progress10` | Objeto | <!-- MISSING --> | {id (cadena), value (número)} |
| `videoprogress25` | `media.mediaTimed.progress25` | Objeto | <!-- MISSING --> | {id (cadena), value (número)} |
| `videoprogress50` | `media.mediaTimed.progress50` | Objeto | <!-- MISSING --> | {id (cadena), value (número)} |
| `videoprogress75` | `media.mediaTimed.progress75` | Objeto | <!-- MISSING --> | {id (cadena), value (número)} |
| `videoprogress95` | `media.mediaTimed.progress95` | Objeto | <!-- MISSING --> | {id (cadena), value (número)} |
| `videoresume` | `media.mediaTimed.resumes` | Objeto | <!-- MISSING --> | {id (cadena), value (número)} |
| `videopausecount` | `media.mediaTimed.pauses` | Objeto | <!-- MISSING --> | {id (cadena), value (número)} |
| `videopausetime` | `media.mediaTimed.pauseTime` | Objeto | <!-- MISSING --> | {id (cadena), value (número)} |
| `videosecondssincelastcall` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`sessionTimeout` | entero |

{style="table-layout:auto"}

## Campos de asignación dividida

Estos campos tienen un solo origen, pero se asignan a **varias** ubicaciones XDM.

| Campo de Analytics | Campo XDM | Tipo de XDM | Descripción |
| --------------- | --------- | -------- | ---------- |
| `s_resolution` | `device.screenWidth`,<br/>`device.screenHeight` | entero | ID numérica que representa la resolución del monitor. |
| `mobileosversion` | `environment.operatingSystem`,<br/>`environment.operatingSystemVersion` | cadena | Versión del sistema operativo móvil. |
| `videoadlength` | `advertising.adAssetReference._xmpDM.duration` | entero | Duración del anuncio de vídeo. |

{style="table-layout:auto"}

## Campos de asignación generados

Los campos seleccionados procedentes de ADC deben transformarse, lo que requiere que la lógica más allá de una copia directa de Adobe Analytics se genere en XDM.

| Campo de Analytics | Campo XDM | Tipo de XDM | Descripción |
| --------------- | --------- | -------- | ----------- |
| `m_prop1`<br/>`[...]`<br/>`m_prop75` | `_experience.analytics.customDimensions`<br/>`.listprops.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`listprops.prop75` | Objeto | Propiedades personalizadas de Analytics, configuradas para ser props de lista. Contiene una lista delimitada de valores. | {} |
| `m_hier1`<br/>`[...]`<br/>`m_hier5` | `_experience.analytics.customDimensions.`<br/>`hierarchies.hier1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`hierarchies.hier5` | Objeto | Utilizado por variables de jerarquía. Contiene una lista delimitada de valores. | {values (array), delimiter (string)} |
| `m_mvvar1`<br/>`[...]`<br/>`m_mvvar3` | `_experience.analytics.customDimensions.`<br/>`lists.list1.list[]`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`lists.list3.list[]` | matriz | Variables de lista personalizadas de Analytics. Contiene una lista delimitada de valores. | {value (string), key (string)} |
| `m_color` | `device.colorDepth` | entero | El ID de profundidad de color, que se basa en el valor de la columna c_color. |
| `m_cookies` | `environment.browserDetails.cookiesEnabled` | Booleano | Variable utilizada en la dimensión Compatibilidad con cookies. |
| `m_event_list` | `commerce.purchases`,<br/>`commerce.productViews`,<br/>`commerce.productListOpens`,<br/>`commerce.checkouts`,<br/>`commerce.productListAdds`,<br/>`commerce.productListRemovals`,<br/>`commerce.productListViews` | Objeto | Eventos de comercio estándar activados en la visita. | {id (cadena), value (número)} |
| `m_event_list` | `_experience.analytics.event1to100.event1`<br/>`[...]`<br/>`_experience.analytics.event901to1000.event1000` | Objeto | Eventos personalizados activados en la visita. | {id (objeto), value (objeto)} |
| `m_geo_country` | `placeContext.geo.countryCode` | cadena | Abreviatura del país del que provino la visita basada en la dirección IP. |
| `m_geo_latitude` | `placeContext.geo._schema.latitude` | número | <!-- MISSING --> |
| `m_geo_longitude` | `placeContext.geo._schema.longitude` | número | <!-- MISSING --> |
| `m_java_enabled` | `environment.browserDetails.javaEnabled` | Booleano | Un indicador que indica si Java™ está habilitado. |
| `m_latitude` | `placeContext.geo._schema.latitude` | número | <!-- MISSING --> |
| `m_longitude` | `placeContext.geo._schema.longitude` | número | <!-- MISSING --> |
| `m_page_event_var1` | `web.webInteraction.URL` | cadena | Variable que solo se utiliza en las solicitudes de imagen de seguimiento de vínculos. Esta variable contiene la dirección URL del vínculo de descarga, de salida o personalizado en el que se hizo clic. |
| `m_page_event_var2` | `web.webInteraction.name` | cadena | Variable que solo se utiliza en las solicitudes de imagen de seguimiento de vínculos. Muestra el nombre personalizado del vínculo, si se especifica. |
| `m_page_type` | `web.webPageDetails.isErrorPage` | Booleano | Variable que se utiliza para rellenar la dimensión Páginas no encontradas. Esta variable debe estar vacía o debe contener &quot;ErrorPage&quot;. |
| `m_pagename_no_url` | `web.webPageDetails.name` | número | El nombre de la página (si está configurado). Si no se especifica ninguna página, este valor se deja vacío. |
| `m_paid_search` | `search.isPaid` | Booleano | Un indicador que se establece si la visita coincide con la detección de búsquedas de pago. |
| `m_product_list` | `productListItems[].items` | matriz | La lista de productos, tal como se transmite mediante la variable products. | {SKU (cadena), cantidad (entero), priceTotal (número)} |
| `m_ref_type` | `web.webReferrer.type` | cadena | ID numérica que representa el tipo de referente de la visita.<br/>`1`: Dentro del sitio<br/>`2`: Otros sitios web<br/>`3`: Motores de búsqueda<br/>`4`: Disco duro<br/>`5`: USENET<br/>`6`: Escritos o marcadores (sin referente)<br/>`7`: correo electrónico<br/>`8`: Sin JavaScript<br/>`9`: Redes sociales |
| `m_search_engine` | `search.searchEngine` | cadena | El ID numérico que representa el motor de búsqueda que refirió al visitante a su sitio. |
| `post_currency` | `commerce.order.currencyCode` | cadena | El código de moneda que se utilizó durante la transacción. |
| `post_cust_hit_time_gmt` | `timestamp` | cadena | Esto solo se utiliza en conjuntos de datos con marca de tiempo habilitada. Es la marca de tiempo que se envía con la visita en función de la hora de UNIX®. |
| `post_cust_visid` | `identityMap` | objeto | El ID de visitante de cliente. |
| `post_cust_visid` | `endUserIDs._experience.aacustomid.primary` | Booleano | El ID de visitante de cliente. |
| `post_cust_visid` | `endUserIDs._experience.aacustomid.namespace.code` | cadena | El ID de visitante de cliente. |
| `post_visid_high` + `visid_low` | `identityMap` | objeto | Un identificador único de una visita. |
| `post_visid_high` + `visid_low` | `endUserIDs._experience.aaid.id` | cadena | Un identificador único de una visita. |
| `post_visid_high` | `endUserIDs._experience.aaid.primary` | Booleano | Se usa con `visid_low` para identificar una visita de forma exclusiva. |
| `post_visid_high` | `endUserIDs._experience.aaid.namespace.code` | cadena | Se usa con `visid_low` para identificar una visita de forma exclusiva. |
| `post_visid_low` | `identityMap` | objeto | Se utiliza con visid_high para identificar una visita de forma exclusiva. |
| `hit_time_gmt` | `receivedTimestamp` | cadena | La marca de tiempo de la visita basada en la hora de UNIX®. |
| `hitid_high` + `hitid_low` | `_id` | cadena | Un identificador único para identificar una visita. |
| `hitid_low` | `_id` | cadena | Se utiliza con hitid_high para identificar una visita de forma exclusiva. |
| `ip` | `environment.ipV4` | cadena | La dirección IP, basada en el encabezado HTTP de la solicitud de imagen. |
| `j_jscript` | `environment.browserDetails.javaScriptEnabled` | Booleano | La versión de JavaScript utilizada. |
| `mcvisid_high` + `mcvisid_low` | identityMap | objeto | El ID de visitante de Experience Cloud. |
| `mcvisid_high` + `mcvisid_low` | endUserID._experience.mcid.id | cadena | El Experience Cloud ID (ECID) también se conoce como MCID y a veces se utiliza en áreas de nombres. |
| `mcvisid_high` | `endUserIDs._experience.mcid.primary` | Booleano | El Experience Cloud ID (ECID) también se conoce como MCID y a veces se utiliza en áreas de nombres. |
| `mcvisid_high` | `endUserIDs._experience.mcid.namespace.code` | cadena | El Experience Cloud ID (ECID) también se conoce como MCID y a veces se utiliza en áreas de nombres. |
| `mcvisid_low` | `identityMap` | objeto | El ID de visitante de Experience Cloud. |
| `sdid_high` + `sdid_low` | `_experience.target.supplementalDataID` | cadena | ID de vinculación de visita. El campo de análisis sdid_high y sdid_low es el ID de datos suplementario que se utiliza para unir dos (o más) visitas entrantes. |
| `mobilebeaconproximity` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.proximity` | cadena | Proximidad de señalización de Mobile Services. |
| `videochapter` | `media.mediaTimed.mediaChapter.`<br/>`chapterAssetReference._xmpDM.duration` | entero | Nombre del capítulo del vídeo. |
| `videolength` | `media.mediaTimed.primaryAssetReference.`<br/>`_xmpDM.duration` | entero | La duración del vídeo. |

{style="table-layout:auto"}

## Campos de asignación avanzados

Los campos seleccionados (conocidos como &quot;valores posteriores&quot;) contienen datos después de que Adobe haya ajustado sus valores mediante Reglas de procesamiento, Reglas de VISTA y Tablas de búsqueda. La mayoría de los valores de publicación tienen un homólogo preprocesado.

El conector de origen de Analytics envía datos preprocesados a un conjunto de datos en Experience Platform. Puede transformar estos datos en su homólogo posprocesado mediante transformaciones. Para obtener más información sobre cómo realizar estas transformaciones mediante el servicio de consultas, consulte [Funciones definidas por Adobe](/help/query-service/sql/adobe-defined-functions.md) en la guía del usuario del servicio de consultas.

Para obtener más información sobre cómo realizar estas transformaciones mediante el servicio de consultas, consulte [Funciones definidas por Adobe](/help/query-service/sql/adobe-defined-functions.md) en la guía del usuario del servicio de consultas.

| Campo de Analytics | Campo XDM | Tipo de XDM | Descripción |
| --------------- | --------- | -------- | ---------- |
| `post_evar1`<br/>`[...]`<br/>`post_evar250` | `_experience.analytics.customDimensions.`<br/>`eVars.eVar1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`eVars.eVar250` | cadena | eVars de Analytics personalizadas. Cada organización puede utilizar eVars de forma diferente. |
| `post_prop1`<br/>`[...]`<br/>`post_prop75` | `_experience.analytics.customDimensions.`<br/>`props.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`props.prop75` | cadena | Propiedades personalizadas de Analytics. Cada organización puede utilizar props de forma diferente. |
| `post_browser_height` | `environment.browserDetails.viewportHeight` | entero | Altura del explorador, en píxeles. |
| `post_browser_width` | `environment.browserDetails.viewportWidth` | entero | Anchura del explorador, en píxeles. |
| `post_campaign` | `marketing.trackingCode` | cadena | La variable utilizada en la dimensión Código de seguimiento. |
| `post_channel` | `web.webPageDetails.siteSection` | cadena | La variable utilizada en la dimensión Secciones del sitio. |
| `post_cust_visid` | `endUserIDs._experience.aacustomid.id` | cadena | El ID de visitante personalizado, si está establecido. |
| `post_first_hit_page_url` | `_experience.analytics.endUser.`<br/>`firstWeb.webPageDetails.URL` | cadena | La URL de la primera página a la que llega el visitante. |
| `post_first_hit_pagename` | `_experience.analytics.endUser.`<br/>`firstWeb.webPageDetails.name` | cadena | Variable utilizada en la dimensión Página de entrada original. El nombre de página de la página de entrada del visitante. |
| `post_keywords` | `search.keywords` | cadena | Las palabras clave que se recopilaron para la visita. |
| `post_page_url` | `web.webPageDetails.URL` | cadena | La URL de la visita individual a la página. |
| `post_pagename` | `web.webPageDetails.pageViews.value` | cadena | Es igual a 1 en visitas que tienen un nombre de página. Esto es similar a la métrica Vistas de página de Adobe Analytics. |
| `post_purchaseid` | `commerce.order.purchaseID` | cadena | Variable que se utiliza para identificar compras de forma exclusiva. |
| `post_referrer` | `web.webReferrer.URL` | cadena | Dirección URL de la página anterior. |
| `post_state` | `_experience.analytics.customDimensions.`<br/>`stateProvince` | cadena | Variable de estado. |
| `post_user_server` | `web.webPageDetails.server` | cadena | Variable utilizada en la dimensión Servidor. |
| `post_zip` | `_experience.analytics.customDimensions.`<br/>`postalCode` | cadena | Variable utilizada para rellenar la dimensión Código postal. |
| `browser` | `_experience.analytics.environment.`<br/>`browserID` | entero | El ID numérico del explorador. |
| `domain` | `environment.domain` | cadena | La variable utilizada en la dimensión Dominio. Se basa en el proveedor de servicios de Internet (ISP) del usuario. |
| `first_hit_referrer` | `_experience.analytics.endUser.`<br/>`firstWeb.webReferrer.URL` | cadena | La primera URL de referencia del visitante. |
| `geo_city` | `placeContext.geo.city` | cadena | El nombre de la ciudad de la visita. Se basa en la dirección IP de la visita. |
| `geo_dma` | `placeContext.geo.dmaID` | entero | El ID numérico del área demográfica de la visita. Se basa en la dirección IP de la visita. |
| `geo_region` | `placeContext.geo.stateProvince` | cadena | El nombre del estado o la región de la visita. Se basa en la dirección IP de la visita. |
| `geo_zip` | `placeContext.geo.postalCode` | cadena | El código postal de la visita. Se basa en la dirección IP de la visita. |
| `os` | `_experience.analytics.environment.`<br/>`operatingSystemID` | entero | ID numérica que representa el sistema operativo del visitante. Se basa en la columna user_agent. |
| `search_page_num` | `search.pageDepth` | entero | Esta variable la utiliza la dimensión Clasificación de todas las páginas de búsqueda e indica en qué página de resultados de búsqueda se encuentra el sitio | apareció en antes de que el usuario hiciera clic en el sitio. |
| `visit_keywords` | `_experience.analytics.session.`<br/>`search.keywords` | cadena | Variable utilizada en la dimensión Palabras clave de búsqueda. |
| `visit_num` | `_experience.analytics.session.`<br/>`num` | entero | Variable utilizada en la dimensión Número de visita. Comienza en 1 y aumenta cada vez que se inicia una nueva visita (por usuario). |
| `visit_page_num` | `_experience.analytics.session.`<br/>`depth` | entero | Variable utilizada en la dimensión Profundidad de visita. Este valor aumenta en 1 por cada visita que genera el usuario y se restablece después de cada visita. |
| `visit_referrer` | `_experience.analytics.session.`<br/>`web.webReferrer.URL` | cadena | El primer referente de la visita. |
| `visit_search_page_num` | `_experience.analytics.session.`<br/>`search.pageDepth` | entero | El primer nombre de página de la visita. |
| `post_prop1`<br/>`[...]`<br/>`post_prop75` | `_experience.analytics.customDimensions.`<br/>`listprops.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`listprops.prop75` | Objeto | Propiedades personalizadas de Analytics, configuradas para ser props de lista. Contiene una lista delimitada de valores. |
| `post_hier1`<br/>`[...]`<br/>`post_hier5` | `_experience.analytics.customDimensions.`<br/>`hierarchies.hier1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`hierarchies.hier5` | Objeto | Lo utilizan las variables de jerarquía y contiene una lista delimitada de valores. | {values (array), delimiter (string)} |
| `post_mvvar1`<br/>`[...]`<br/>`post_mvvar3` | `_experience.analytics.customDimensions.`<br/>`lists.list1.list[]`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`lists.list3.list[]` | matriz | Una lista de valores de variables. Contiene una lista delimitada de valores personalizados, según la implementación. | {value (string), key (string)} |
| `post_cookies` | `environment.browserDetails.cookiesEnabled` | Booleano | Variable utilizada en la dimensión Compatibilidad con cookies. |
| `post_event_list` | `commerce.purchases`,<br/>`commerce.productViews`,<br/>`commerce.productListOpens`,<br/>`commerce.checkouts`,<br/>`commerce.productListAdds`,<br/>`commerce.productListRemovals`,<br/>`commerce.productListViews` | Objeto | Eventos de comercio estándar activados en la visita. | {id (cadena), value (número)} |
| `post_event_list` | `_experience.analytics.event1to100.event1`<br/>`[...]`<br/>`_experience.analytics.event901to1000.event1000` | Objeto | Eventos personalizados activados en la visita. | {id (objeto), value (objeto)} |
| `post_java_enabled` | `environment.browserDetails.javaEnabled` | Booleano | Un indicador que indica si Java™ está habilitado. |
| `post_latitude` | `placeContext.geo._schema.latitude` | número | <!-- MISSING --> |
| `post_longitude` | `placeContext.geo._schema.longitude` | número | <!-- MISSING --> |
| `post_page_event` | `web.webInteraction.type` | cadena | El tipo de visita que se envía en la solicitud de imagen (visita estándar, vínculo de descarga, vínculo de salida o vínculo personalizado en el que se hace clic). |
| `post_page_event` | `web.webInteraction.linkClicks.value` | número | Es igual a 1 si la visita es un clic en vínculo. Esto es similar a la métrica Eventos de página de Adobe Analytics. |
| `post_page_event_var1` | `web.webInteraction.URL` | cadena | Esta variable solo se utiliza en solicitudes de imagen de seguimiento de vínculos. Es la dirección URL del vínculo de descarga, de salida o personalizado en el que se hizo clic. |
| `post_page_event_var2` | `web.webInteraction.name` | cadena | Esta variable solo se utiliza en solicitudes de imagen de seguimiento de vínculos. Es el nombre personalizado del vínculo. |
| `post_page_type` | `web.webPageDetails.isErrorPage` | Booleano | Se utiliza para rellenar la dimensión Páginas no encontradas. Esta variable debe estar vacía o debe contener &quot;ErrorPage&quot; |
| `post_pagename_no_url` | `web.webPageDetails.name` | número | El nombre de la página (si está configurado). Si no se especifica ninguna página, este valor se deja vacío. |
| `post_product_list` | `productListItems[].items` | matriz | La lista de productos, tal como se transmite mediante la variable products. | {SKU (cadena), cantidad (entero), priceTotal (número)} |
| `post_search_engine` | `search.searchEngine` | cadena | El ID numérico que representa el motor de búsqueda que refirió al visitante a su sitio. |
| `mvvar1_instances` | `.list.items[]` | Objeto | Lista de valores de variables. Contiene una lista delimitada de valores personalizados, según la implementación. |
| `mvvar2_instances` | `.list.items[]` | Objeto | Lista de valores de variables. Contiene una lista delimitada de valores personalizados, según la implementación. |
| `mvvar3_instances` | `.list.items[]` | Objeto | Lista de valores de variables. Contiene una lista delimitada de valores personalizados, según la implementación. |
| `color` | `device.colorDepth` | entero | ID de profundidad de color, basada en el valor de la columna c_color. |
| `first_hit_ref_type` | `_experience.analytics.endUser.`<br/>`firstWeb.webReferrer.type` | cadena | El ID numérico, que representa el tipo de referente del primer referente del visitante. |
| `first_hit_time_gmt` | `_experience.analytics.endUser.`<br/>`firstTimestamp` | entero | Marca de tiempo de la primera visita del visitante en tiempo UNIX®. |
| `geo_country` | `placeContext.geo.countryCode` | cadena | Abreviatura del país del que provino la visita basada en la dirección IP. |
| `geo_latitude` | `placeContext.geo._schema.latitude` | número | <!-- MISSING --> |
| `geo_longitude` | `placeContext.geo._schema.longitude` | número | <!-- MISSING --> |
| `paid_search` | `search.isPaid` | Booleano | Un indicador que se establece si la visita coincide con la detección de búsquedas de pago. |
| `ref_type` | `web.webReferrer.type` | cadena | ID numérica que representa el tipo de referente de la visita. |
| `visit_paid_search` | `_experience.analytics.session.`<br/>`search.isPaid` | Booleano | Un indicador (1=de pago, 0=no pagado) que indica si la primera visita se produjo a partir de una visita de búsqueda de pago. |
| `visit_ref_type` | `_experience.analytics.session.`<br/>`web.webReferrer.type` | cadena | ID numérica que representa el tipo de referente del primer referente de la visita. |
| `visit_search_engine` | `_experience.analytics.session.`<br/>`search.searchEngine` | cadena | ID numérica del primer motor de búsqueda de la visita. |
| `visit_start_time_gmt` | `_experience.analytics.session.`<br/>`timestamp` | entero | Marca de tiempo de la primera visita individual de la visita en tiempo UNIX®. |

{style="table-layout:auto"}