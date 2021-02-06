---
keywords: Experience Platform;inicio;temas populares;Campos de asignación de Analytics;asignación de análisis
solution: Experience Platform
title: Campos de asignación para el conector de origen de Adobe Analytics
topic: overview
description: Adobe Experience Platform permite la ingesta de datos de Adobe Analytics a través del conector de datos de Analytics (ADC). Algunos de los datos ingestados a través de ADC se pueden asignar directamente desde los campos de Analytics a los campos del Modelo de datos de experiencia (XDM), mientras que otros datos requieren transformaciones y funciones específicas para asignarse correctamente.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '3393'
ht-degree: 10%

---


# Asignaciones de campos de Analytics

Adobe Experience Platform permite la ingesta de datos de Adobe Analytics a través del conector de datos de Analytics (ADC). Algunos de los datos ingestados a través de ADC se pueden asignar directamente desde los campos de Analytics a los campos del Modelo de datos de experiencia (XDM), mientras que otros datos requieren transformaciones y funciones específicas para asignarse correctamente.

![](../images/analytics-data-experience-platform.png)

## Campos de asignación directa

Los campos seleccionados se asignan directamente de Adobe Analytics al Modelo de datos de experiencia (XDM).

La siguiente tabla incluye columnas que muestran el nombre del campo Analytics (*campo Analytics*), el campo XDM correspondiente (*campo XDM*) y su tipo (*tipo XDM*), así como una descripción del campo (*Descripción*).

>[!NOTE]
>
>Desplácese hacia la izquierda/derecha para vista del contenido completo de la tabla.

| Campo de Analytics | Campo XDM | Tipo XDM | Descripción |
| --------------- | --------- | -------- | ---------- |
| m_evar1 - m_evar250 | _experience.analytics.customDimensions.eVars.eVar1 - _experience.analytics.customDimensions.eVars.eVar250 | string | Variable personalizada que puede variar entre 1 y 250. Cada organización usará estas eVars personalizadas de manera diferente. |
| m_prop1 - m_prop75 | _experience.analytics.customDimensions.props.prop1 - _experience.analytics.customDimensions.props.prop75 | string | Variables de tráfico personalizadas, que pueden variar entre 1 y 75. |
| m_browser | _experience.analytics.entorno.browserID | integer | ID de número del explorador. |
| m_browser_height | environment.browserDetails.viewportHeight | integer | Altura del explorador, en píxeles. |
| m_browser_width | environment.browserDetails.viewportWidth | integer | Ancho del explorador, en píxeles. |
| m_campaña | marketing.trackingCode | string | Variable utilizada en la dimensión Código de seguimiento. |
| m_canal | web.webPageDetails.siteSection | string | La variable utilizada en la dimensión Secciones del sitio. |
| m_domain | environment.domain | string | La variable utilizada en la dimensión Dominio. Esto se basará en el proveedor de servicio de Internet (ISP) del usuario. |
| m_geo_city | placeContext.geo.city | string | Nombre de la ciudad de la visita. Se basa en la dirección IP de la visita. |
| m_geo_dma | placeContext.geo.dmaID | integer | ID numérico del área demográfica de la visita. Se basa en la dirección IP de la visita. |
| m_geo_region | placeContext.geo.stateProvince | string | Nombre del estado o región de la visita. Se basa en la dirección IP de la visita. |
| m_geo_zip | placeContext.geo.postalCode | string | Código postal de la visita. Se basa en la dirección IP de la visita. |
| m_keywords | search.keywords | string | La variable utilizada en la dimensión Palabra clave. |
| m_os | _experience.analytics.entorno.OperatingSystemID | integer | El ID numérico que representa el sistema operativo del visitante. Esto se basa en la columna user_agent. |
| m_page_url | web.webPageDetails.URL | string | Dirección URL de la visita individual de la página. |
| m_pagename_no_url | web.webPageDetails.</span>name | string | Variable utilizada para rellenar la dimensión Páginas. |
| m_remitente del reenvío | web.webReferrer.URL | string | La dirección URL de la página anterior. |
| m_search_page_num | search.pageDepth | integer | Utilizado por la dimensión Clasificación de todas las páginas de búsqueda. Indica en qué página de resultados de búsqueda apareció el sitio antes de que el usuario hiciera clic en el sitio. |
| m_state | _experience.analytics.customDimensions.stateProvincia | string | Variable de estado. |
| m_user_server | web.webPageDetails.server | string | Variable utilizada en la dimensión Servidor. |
| m_zip | _experience.analytics.customDimensions.postalCode | string | Variable utilizada para rellenar la dimensión Código postal. |
| accept_language | environment.browserDetails.acceptLanguage | string | Lista todos los idiomas aceptados, como se indica en el encabezado HTTP Accept-Language. |
| homepage | web.webPageDetails.isHomePage | Booleano | Ya no se utiliza. Se indica si la dirección URL actual es la página principal del explorador. |
| ipv6 | environment.ipV6 | string |
| j_jscript | environment.browserDetails.javaScriptVersion | string | Versión de JavaScript admitida por el explorador. |
| user_agent | environment.browserDetails.userAgent | string | La cadena del agente de usuario enviada en el encabezado HTTP. |
| mobileappid | application.</span>name | string | El ID de la aplicación móvil, almacenado en el siguiente formato: `[AppName][BundleVersion]`. |
| mobiledevice | device.model | string | Nombre del dispositivo móvil. En iOS, se almacena como una cadena de dos dígitos separada por comas. El primer número representa la generación del dispositivo y el segundo número representa la familia del dispositivo. |
| pointofinterest | placeContext.POIinteraction.POIDetail.</span>name | string | Utilizado por los servicios móviles. Representa el punto de interés. |
| pointofinterestdistance | placeContext.POIinteraction.POIDetail.geoInteractionDetails.distanceToCenter | entero | Utilizado por los servicios móviles. Representa la distancia del punto de interés. |
| mobileplaceaccuracy | placeContext.POIinteraction.POIDetail.geoInteractionDetails.deviceGeoAccuracy | entero | Recopilado desde la variable de datos de contexto a.loc.acc. Indica la precisión del GPS en metros en el momento de la recogida. |
| mobileplacecategory | placeContext.POIinteraction.POIDetail.category | string | Recopilado desde la variable de datos de contexto a.loc.category. Describe la categoría de un lugar específico. |
| mobileplaceid | placeContext.POIinteraction.POIDetail.POIID | string | Recopilado desde la variable de datos de contexto a.loc.id. Identificador de un punto de interés determinado. |
| vídeo | media.mediaTimed.primaryAssetReference._id | string | Nombre del vídeo. |
| videoad | advertising.adAssetReference._id | string | Identificador del recurso de publicidad. |
| videocontenttype | media.mediaTimed.primaryAssetViewDetails.broadcastContentType | string | Tipo de contenido de vídeo. Se establece automáticamente en &quot;Vídeo&quot; para todas las vistas de vídeo. |
| videoadpod | advertising.adAssetViewDetails.adBreak._id | string | El pod en el que se encuentra la publicidad de vídeo. |
| videoadinpod | advertising.adAssetViewDetails.index | integer | Posición en la que se encuentra la publicidad de vídeo en el pod. |
| videoplayername | media.mediaTimed.primaryAssetViewDetails.playerName | string | Nombre del reproductor de vídeo. |
| videochannel | media.mediaTimed.primaryAssetViewDetails.broadcastChannel | string | El canal de vídeo. |
| videoadplayername | advertising.adAssetViewDetails.playerName | string | Nombre del reproductor de anuncios de vídeo. |
| videochapter | media.mediaTimed.mediaChapter.chapterAssetReference._id | string | Nombre del capítulo de vídeo |
| videoname | media.mediaTimed.primaryAssetReference._dc.title | string | El nombre del vídeo. |
| videoadname | advertising.adAssetReference._dc.title | string | Nombre de la publicidad de vídeo. |
| videoshow | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Series._iptc4xmpExt.Name | string | Programa del vídeo. |
| videoseason | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Season._iptc4xmpExt.Name | string | Temporada de video. |
| videoepisode | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Episode._iptc4xmpExt.Name | string | Episodio del vídeo. |
| videonetwork | media.mediaTimed.primaryAssetViewDetails.broadcastNetwork | string | Red del vídeo. |
| videoshowtype | media.mediaTimed.primaryAssetReference.showType | string | Tipo de programa del vídeo. |
| videoadload | media.mediaTimed.primaryAssetViewDetails.adLoadType | string | Cargas del anuncio de vídeo. |
| videofeedtype | media.mediaTimed.primaryAssetViewDetails.sourceFeed | string | Tipo de fuente de vídeo. |
| mobilebeaconmajor | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.beaconMajor | entero | Señalización principal de Mobile Services. |
| mobilebeaconminor | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.beaconMinor | entero | Señalización menor de Mobile Services. |
| mobilebeaconuuid | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.proximityUUID | string | UUID de señalización de Mobile Services. |
| videosessionid | media.mediaTimed.primaryAssetViewDetails._id | string | ID de sesión de vídeo. |
| videogenre | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Genre | array | Género del vídeo. | {title (Objeto), description (Objeto), type (Objeto), meta:xdmType (Objeto), items (cadena), meta:xdmField (Objeto)} |
| mobileinstalls | application.firstLaunches | Objeto | Esto se activa en la primera ejecución después de la instalación o reinstalación | {id (cadena), valor (número)} |
| mobileupgrades | application.upgrades | Objeto | Informa del número de actualizaciones de la aplicación. Déclencheur en la primera ejecución después de la actualización o en cualquier momento en que cambie el número de versión. | {id (cadena), valor (número)} |
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
| videoqoetimetostart | media.mediaTimed.primaryAssetViewDetails.qoe.timeToStart | Objeto | Tiempo de inicio de la calidad del vídeo. | {id (cadena), valor (número)} |
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
| videosecundaria ssincelastcall | media.mediaTimed.primaryAssetViewDetails.sessionTimeout | integer |

## Dividir campos de asignación

Estos campos tienen un único origen, pero se asignan a **varias** ubicaciones XDM.

| Campo de Analytics | Campo XDM | Tipo XDM | Descripción |
| --------------- | --------- | -------- | ---------- |
| s_resolution | device.screenWidth, device.screenHeight | integer | ID numérico que representa la resolución del monitor. |
| mobileosversion | entorno.OperatingSystem, entorno.OperatingSystemVersion | string | Versión del sistema operativo móvil. |
| videoadlength | advertising.adAssetReference._xmpDM.duration | integer | Duración de la publicidad de vídeo. |

## Campos de asignación generados

Es necesario transformar determinados campos procedentes de ADC, lo que requiere lógica más allá de una copia directa de Adobe Analytics para poder generarlos en XDM.

La siguiente tabla incluye columnas que muestran el nombre del campo Analytics (*campo Analytics*), el campo XDM correspondiente (*campo XDM*) y su tipo (*tipo XDM*), así como una descripción del campo (*Descripción*).

>[!NOTE]
>
>Desplácese hacia la izquierda/derecha para vista del contenido completo de la tabla.

| Campo de Analytics | Campo XDM | Tipo XDM | Descripción |
| --------------- | --------- | -------- | ----------- |
| m_prop1 - m_prop75 | _experience.analytics.customDimensions.listprops.prop1 - _experience.analytics.customDimensions.listprops.prop75 | Objeto | Variables de tráfico personalizadas, que varían entre 1 y 75 | {} |
| m_hier1 - m_hier5 | _experience.analytics.customDimensions.hierarchies.hier1 - _experience.analytics.customDimensions.hierarchies.hier5 | Objeto | Utilizado por variables de jerarquía. Contiene un | lista delimitada de valores. | {valores (matriz), delimitador (cadena)} |
| m_mvvar1 - m_mvvar3 | _experience.analytics.customDimensions.listas.lista1.lista[] - _experience.analytics.customDimensions.listas.lista3.lista[] | array | Lista de los valores variables. Contiene una lista delimitada de valores personalizados, según la implementación | {valor (cadena), clave (cadena)} |
| m_color | device.colorDepth | integer | ID de profundidad de color, que se basa en el valor de la columna c_color. |
| m_cookies | environment.browserDetails.cookiesEnabled | Booleano | Variable utilizada en la dimensión Compatibilidad con cookies. |
| m_evento_lista | commerce.purchase, commerce.productViews, commerce.productListOpen, commerce.checkouts, commerce.productListAdd, commerce.productListRemovals, commerce.productListViews | Objeto | Eventos comerciales estándar activados en la visita. | {id (cadena), valor (número)} |
| m_evento_lista | _experience.analytics.evento1to100.evento1 - _experience.analytics.evento1to100.evento100, _experience.analytics.evento101to200.evento101 - _experience.analytics.evento101to20 0.evento200, _experience.analytics.evento201 a 300.evento201 - _experience.analytics.evento201 a 300.evento300, _experience.analytics.evento301 a 400.evento33 01 - _experience.analytics.evento301to400.` 400, _experience.analytics.› 401to500.401 - _experience.analytics.html401to500._experience .analytics.› 501a600.501 - _experience.analytics.` 501a600.600, _experience.analytics.601a700.601 - _experience.analytics. 601to700.html700, _experience.analytics.701to800.html・701 - _experience.analytics.701to800._experience.analytics.801to1 900.› 801 - _experience.analytics.` 801to900.› 900, _experience.analytics.901to1000.› 901 - _experience.analytics.› 901 a 10000 1000 | Objeto | Eventos personalizados activados en la visita. | {id (objeto), valor (objeto)} |
| m_geo_country | placeContext.geo.countryCode | string | Abreviación del país del que procede la visita, que se basa en la IP. |
| m_geo_latitude | placeContext.geo._esquema.latitude | entero | <!-- MISSING --> |
| m_geo_longitude | placeContext.geo._esquema.longitude | entero | <!-- MISSING --> |
| m_java_enabled | environment.browserDetails.javaEnabled | Booleano | Un indicador que indica si Java está habilitado. |
| m_latitude | placeContext.geo._esquema.latitude | entero | <!-- MISSING --> |
| m_longitude | placeContext.geo._esquema.longitude | entero | <!-- MISSING --> |
| m_page_evento_var1 | web.webInteraction.URL | string | Variable que solo se utiliza en solicitudes de imagen de seguimiento de vínculos. Esta variable contiene la dirección URL del vínculo de descarga, de salida o personalizado en el que se hizo clic. |
| m_page_evento_var2 | web.webInteraction.name | string | Variable que solo se utiliza en solicitudes de imagen de seguimiento de vínculos. Esto lista el nombre personalizado del vínculo, si se especifica. |
| m_page_type | web.webPageDetails.isErrorPage | Booleano | Variable que se utiliza para rellenar la dimensión Páginas no encontradas. Esta variable debe estar vacía o contener &quot;ErrorPage&quot;. |
| m_pagename_no_url | web.webPageDetails.pageViews.value | entero | El nombre de la página (si se ha establecido). Si no se especifica ninguna página, este valor se deja vacío. |
| m_paid_search | search.isPaid | Booleano | Un indicador que se establece si la visita coincide con la detección de búsqueda paga. |
| m_product_lista | productListItems[].items | array | La lista del producto, tal como se pasa a través de la variable products. | {SKU (cadena), cantidad (entero), priceTotal (número)} |
| m_ref_type | web.webReferrer.type | string | Una ID numérica que representa el tipo de referente de la visita. 1 significa que dentro del sitio, 2 significa otros sitios web, 3 significa motores de búsqueda, 4 significa disco duro, 5 significa USENET, 6 significa Escrito o marcador (sin remitente del reenvío), 7 significa correo electrónico, 8 significa No JavaScript y 9 significa Redes sociales. |
| m_search_engine | search.searchEngine | string | ID numérica que representa el motor de búsqueda que dirigió el visitante a su sitio. |
| post_currency | commerce.order.currencyCode | string | El código de moneda que se ha utilizado durante la transición. |
| post_cust_hit_time_gmt | timestamp | string | Esto solo se utiliza en conjuntos de datos con marca de tiempo habilitada. Ésta es la marca de tiempo que se envía con ella, en función de la hora Unix. |
| post_cust_visid | identityMap | object | ID de visitante del cliente. |
| post_cust_visid | endUserIDs._experience.aacustomid.primario | Booleano | ID de visitante del cliente. |
| post_cust_visid | endUserIDs._experience.acustomid.Área de nombres.code | string | ID de visitante del cliente. |
| post_visid_high + visid_low | identityMap | object | Identificador único de una visita. |
| post_visid_high + visid_low | endUserIDs._experience.aaid.id | string | Identificador único de una visita. |
| post_visid_high | endUserIDs._experience.aaid.Primary | Booleano | Se utiliza junto con visid_low para identificar de forma exclusiva una visita. |
| post_visid_high | endUserIDs._experience.aaid.Área de nombres.code | string | Se utiliza junto con visid_low para identificar de forma exclusiva una visita. |
| post_visid_low | identityMap | object | Se utiliza junto con visid_high para identificar de forma exclusiva una visita. |
| hit_time_gmt | receivedTimestamp | string | Marca de hora de la visita, basada en tiempo Unix. |
| hitid_high + hitid_low | _id | string | Identificador único para identificar una visita. |
| hitid_low | _id | string | Se utiliza junto con hitid_high para identificar de forma exclusiva una visita. |
| ip | environment.ipV4 | string | Dirección IP, basada en el encabezado HTTP de la solicitud de imagen. |
| j_jscript | environment.browserDetails.javaScriptEnabled | Booleano | Versión de JavaScript utilizada. |
| mcvisid_high + mcvisid_low | identityMap | object | ID del Visitante del Experience Cloud. |
| mcvisid_high + mcvisid_low | endUserIDs._experience.mcid.id | string | ID del Visitante del Experience Cloud. |
| mcvisid_high | endUserIDs._experience.mcid.Primary | Booleano | ID del Visitante del Experience Cloud. |
| mcvisid_high | endUserIDs._experience.mcid.Área de nombres.code | string | ID del Visitante del Experience Cloud. |
| mcvisid_low | identityMap | object | ID del Visitante del Experience Cloud. |
| sdid_high + sdid_low | _experience.destinatario.plementalDataID | string | ID de la configuración de visitas. El campo analytics sdid_high y sdid_low es la identificación de datos suplementaria que se utiliza para unir dos (o más) visitas entrantes. |
| mobilebeaconproximity | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.proximity | string | Proximidad de la señalización de Mobile Services. |
| videochapter | media.mediaTimed.mediaChapter.chapterAssetReference._xmpDM.duration | integer | Nombre del capítulo del vídeo. |
| videolength | media.mediaTimed.primaryAssetReference._xmpDM.duration | integer | Duración del vídeo. |

## Campos de asignación avanzada

Los campos seleccionados (conocidos como &quot;valores postales&quot;) requieren transformaciones más avanzadas para poder asignarlos correctamente desde los campos de Adobe Analytics al Modelo de datos de experiencia (XDM). La realización de estas transformaciones avanzadas implica el uso del servicio de Consulta Adobe Experience Platfrom y funciones prediseñadas (llamadas funciones definidas por Adobe) para la sesionización, atribución y deduplicación.

Para obtener más información sobre cómo realizar estas transformaciones mediante el servicio de Consulta, visite la [documentación de funciones definidas por Adobe](../../../../query-service/sql/adobe-defined-functions.md).

La siguiente tabla incluye columnas que muestran el nombre del campo Analytics (*campo Analytics*), el campo XDM correspondiente (*campo XDM*) y su tipo (*tipo XDM*), así como una descripción del campo (*Descripción*).

>[!NOTE]
>
>Desplácese hacia la izquierda/derecha para vista del contenido completo de la tabla.

| Campo de Analytics | Campo XDM | Tipo XDM | Descripción |
| --------------- | --------- | -------- | ---------- |
| post_evar1 - post_evar250 | _experience.analytics.customDimensions.eVars.eVar1 - _experience.analytics.customDimensions.eVars.eVar250 | string | Variable personalizada que puede variar entre 1 y 250. Cada organización usará estas eVars personalizadas de manera diferente. |
| post_prop1 - post_prop75 | _experience.analytics.customDimensions.props.prop1 - _experience.analytics.customDimensions.props.prop75 | string | Variables de tráfico personalizadas, que pueden variar entre 1 y 75. |
| post_browser_height | environment.browserDetails.viewportHeight | integer | Altura del explorador, en píxeles. |
| post_browser_width | environment.browserDetails.viewportWidth | integer | Ancho del explorador, en píxeles. |
| post_campaña | marketing.trackingCode | string | Variable utilizada en la dimensión Código de seguimiento. |
| post_canal | web.webPageDetails.siteSection | string | La variable utilizada en la dimensión Secciones del sitio. |
| post_cust_visid | endUserIDs._experience.aacustomid.id | string | El ID de visitante personalizado, si se establece. |
| post_first_hit_page_url | _experience.analytics.endUser.firstWeb.webPageDetails.URL | string | Dirección URL de la primera página a la que llega el visitante. |
| post_first_hit_pagename | _experience.analytics.endUser.firstWeb.webPageDetails.name | string | Variable utilizada en la dimensión Página de entrada original. El nombre de la página de entrada del visitante. |
| post_keywords | search.keywords | string | Las palabras clave que se recopilaron para la visita. |
| post_page_url | web.webPageDetails.URL | string | Dirección URL de la visita individual de la página. |
| post_pagename_no_url | web.webPageDetails.name | string | Variable utilizada para rellenar la dimensión Páginas. |
| post_purchaseid | commerce.order.purchaseID | string | Variable que se utiliza para identificar de forma exclusiva las compras. |
| post_remitente del reenvío | web.webReferrer.URL | string | La dirección URL de la página anterior. |
| post_state | _experience.analytics.customDimensions.stateProvincia | string | Variable de estado. |
| post_user_server | web.webPageDetails.server | string | Variable utilizada en la dimensión Servidor. |
| post_zip | _experience.analytics.customDimensions.postalCode | string | Variable utilizada para rellenar la dimensión Código postal. |
| explorador | _experience.analytics.entorno.browserID | integer | ID numérico del explorador. |
| domain | environment.domain | string | La variable utilizada en la dimensión Dominio. Esto se basará en el proveedor de servicio de Internet (ISP) del usuario. |
| first_hit_remitente del reenvío | _experience.analytics.endUser.firstWeb.webReferrer.URL | string | La primera dirección URL de referencia del visitante. |
| geo_city | placeContext.geo.city | string | Nombre de la ciudad de la visita. Se basa en la dirección IP de la visita. |
| geo_dma | placeContext.geo.dmaID | integer | ID numérico del área demográfica de la visita. Se basa en la dirección IP de la visita. |
| geo_region | placeContext.geo.stateProvince | string | Nombre del estado o región de la visita. Se basa en la dirección IP de la visita. |
| geo_zip | placeContext.geo.postalCode | string | Código postal de la visita. Se basa en la dirección IP de la visita. |
| os | _experience.analytics.entorno.OperatingSystemID | integer | El ID numérico que representa el sistema operativo del visitante. Esto se basa en la columna user_agent. |
| search_page_num | search.pageDepth | integer | Esta variable se utiliza en la dimensión Clasificación de todas las páginas de búsqueda e indica la página de resultados de búsqueda del sitio | antes de que el usuario hiciera clic en el sitio. |
| visit_keywords | _experience.analytics.session.search.keywords | string | Variable utilizada en la dimensión Palabras clave de búsqueda. |
| visit_num | _experience.analytics.session.num | integer | Variable utilizada en la dimensión Número de visita. Esto inicio en 1 y aumenta cada vez que se produce un nuevo inicio de visita (por usuario). |
| visit_page_num | _experience.analytics.session.depth | integer | Variable utilizada en la dimensión Profundidad de acierto. Este valor aumenta en 1 por cada visita que genera el usuario y se restablece después de cada visita. |
| visit_remitente del reenvío | _experience.analytics.session.web.webReferrer.URL | string | El primer remitente del reenvío de la visita. |
| visit_search_page_num | _experience.analytics.session.search.pageDepth | integer | El primer nombre de página de la visita. |
| post_prop1 - post_prop75 | _experience.analytics.customDimensions.listprops.prop1 - _experience.analytics.customDimensions.listprops.prop75 | Objeto | Variables de tráfico personalizadas 1-75. |
| post_hier1 - post_hier5 | _experience.analytics.customDimensions.hierarchies.hier1 - _experience.analytics.customDimensions.hierarchies.hier5 | Objeto | Utilizado por variables de jerarquía y contiene una lista delimitada de valores. | {valores (matriz), delimitador (cadena)} |
| post_mvvar1 - post_mvvar3 | _experience.analytics.customDimensions.listas.lista1.lista[] - _experience.analytics.customDimensions.listas.lista3.lista[] | array | Una lista de valores de variables. Contiene una lista delimitada de valores personalizados, según la implementación. | {valor (cadena), clave (cadena)} |
| post_cookies | environment.browserDetails.cookiesEnabled | Booleano | Variable utilizada en la dimensión Compatibilidad con cookies. |
| post_evento_lista | commerce.purchase, commerce.productViews, commerce.productListOpen, commerce.checkouts, commerce.productListAdd, commerce.productListRemovals, commerce.productListViews | Objeto | Eventos comerciales estándar activados en la visita. | {id (cadena), valor (número)} |
| post_evento_lista | _experience.analytics.evento1to100.evento1 - _experience.analytics.evento1to100.evento100, _experience.analytics.evento101to200.evento101 - _experience.analytics.evento101to20 0.evento200, _experience.analytics.evento201 a 300.evento201 - _experience.analytics.evento201 a 300.evento300, _experience.analytics.evento301 a 400.evento33 01 - _experience.analytics.evento301to400.` 400, _experience.analytics.› 401to500.401 - _experience.analytics.html401to500._experience .analytics.› 501a600.501 - _experience.analytics.` 501a600.600, _experience.analytics.601a700.601 - _experience.analytics. 601to700.html700, _experience.analytics.701to800.html・701 - _experience.analytics.701to800._experience.analytics.801to1 900.› 801 - _experience.analytics.` 801to900.› 900, _experience.analytics.901to1000.› 901 - _experience.analytics.› 901 a 10000 1000 | Objeto | Eventos personalizados activados en la visita. | {id (objeto), valor (objeto)} |
| post_java_enabled | environment.browserDetails.javaEnabled | Booleano | Un indicador que indica si Java está habilitado. |
| post_latitude | placeContext.geo._esquema.latitude | entero | <!-- MISSING --> |
| post_longitude | placeContext.geo._esquema.longitude | entero | <!-- MISSING --> |
| post_page_evento | web.webInteraction.type | string | Tipo de visita que se envía en la solicitud de imagen (visita individual estándar, vínculo de descarga, vínculo de salida o vínculo personalizado en el que se hace clic). |
| post_page_evento | web.webInteraction.linkClicks.value | entero | Tipo de visita que se envía en la solicitud de imagen (visita individual estándar, vínculo de descarga, vínculo de salida o vínculo personalizado en el que se hace clic). |
| post_page_evento_var1 | web.webInteraction.URL | string | Esta variable solo se utiliza en solicitudes de imagen de seguimiento de vínculos. Es la dirección URL del vínculo de descarga, de salida o personalizado en el que se hizo clic. |
| post_page_evento_var2 | web.webInteraction.name | string | Esta variable solo se utiliza en solicitudes de imagen de seguimiento de vínculos. Será el nombre personalizado del vínculo. |
| post_page_type | web.webPageDetails.isErrorPage | Booleano | Se utiliza para rellenar la dimensión Páginas no encontradas. Esta variable debe estar vacía o contener &quot;ErrorPage&quot; |
| post_pagename_no_url | web.webPageDetails.pageViews.value | entero | El nombre de la página (si se ha establecido). Si no se especifica ninguna página, este valor se deja vacío. |
| post_product_lista | productListItems[].items | array | La lista del producto, tal como se pasa a través de la variable products. | {SKU (cadena), cantidad (entero), priceTotal (número)} |
| post_search_engine | search.searchEngine | string | ID numérica que representa el motor de búsqueda que dirigió el visitante a su sitio. |
| mvvar1_instance | .lista.items[] | Objeto | Lista de los valores variables. Contiene una lista delimitada de valores personalizados, según la implementación. |
| mvvar2_instance | .lista.items[] | Objeto | Lista de los valores variables. Contiene una lista delimitada de valores personalizados, según la implementación. |
|  | mvvar3_instance | .lista.items[] | Objeto | Lista de los valores variables. Contiene una lista delimitada de valores personalizados, según la implementación. |
| color | device.colorDepth | integer | ID de profundidad de color, según el valor de la columna c_color. |
| first_hit_ref_type | _experience.analytics.endUser.firstWeb.webReferrer.type | string | El ID numérico, que representa el tipo de remitente del reenvío del primer remitente del reenvío del visitante. |
| first_hit_time_gmt | _experience.analytics.endUser.firstTimestamp | integer | Marca de tiempo de la primera visita del visitante en Tiempo Unix. |
| geo_country | placeContext.geo.countryCode | string | Abreviación del país del que procede la visita, basada en la IP. |
| geo_latitude | placeContext.geo._esquema.latitude | entero | <!-- MISSING --> |
| geo_longitude | placeContext.geo._esquema.longitude | entero | <!-- MISSING --> |
| paid_search | search.isPaid | Booleano | Un indicador que se establece si la visita coincide con la detección de búsqueda paga. |
| ref_type | web.webReferrer.type | string | Una ID numérica que representa el tipo de referente de la visita. |
| visit_paid_search | _experience.analytics.session.search.isPaid | Booleano | Un indicador (1=pago, 0=no pagado) que indica si la primera visita individual de la visita fue desde una visita individual de búsqueda paga. |
| visit_ref_type | _experience.analytics.session.web.webReferrer.type | string | ID numérico que representa el tipo de remitente del reenvío del primer remitente del reenvío de la visita. |
| visit_search_engine | _experience.analytics.session.search.searchEngine | string | ID numérica del primer motor de búsqueda de la visita. |
| visit_inicio_time_gmt | _experience.analytics.session.timestamp | integer | Marca de hora de la primera visita individual de la visita en tiempo Unix. |
