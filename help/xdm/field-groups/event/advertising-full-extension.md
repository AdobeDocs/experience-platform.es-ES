---
title: Grupo de campos de esquema de extensión completa de Adobe Advertising Cloud ExperienceEvent
description: Obtenga información acerca del grupo de campos de esquema Extensión completa de ExperienceEvent de Adobe Advertising Cloud.
badgeBeta: label="Beta" type="Informative"
source-git-commit: adfd0220b8bc53c44abc76a711b148a7e03edb7a
workflow-type: tm+mt
source-wordcount: '1581'
ht-degree: 7%

---

# [!UICONTROL Extensión completa de Adobe Advertising Cloud ExperienceEvent] grupo de campos de esquema

>[!AVAILABILITY]
>
>El grupo de campos [!UICONTROL Extensión completa de ExperienceEvent de Adobe Advertising Cloud] está actualmente en la versión beta. La documentación y las funcionalidades están sujetas a cambios.

[!UICONTROL Adobe Advertising Cloud ExperienceEvent Full Extension] es un grupo de campos de esquema estándar para la [[!DNL XDM ExperienceEvent] clase](../../classes/experienceevent.md), que captura métricas comunes recopiladas por Adobe Advertising (anteriormente denominadas &quot;[!DNL Advertising Cloud]&quot;).

Este documento describe la estructura y el caso de uso del grupo de campos de extensión [!DNL Advertising Cloud].

>[!NOTE]
>
>También puede buscar este grupo de campos [en la interfaz de usuario de Experience Platform](../../ui/explore.md) o ver el esquema completo en el [repositorio XDM público](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json).

## Estructura del grupo de campos

El grupo de campos proporciona un único objeto `_experience` a un esquema, que a su vez contiene un único objeto `adcloud`.

![Campos de nivel superior para el grupo de campos [!DNL Advertising Cloud]](../../images/field-groups/advertising-full-extension/full-schema.png "Campos de nivel superior para el [!DNL Advertising Cloud] grupo de campos")

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `adDeliveryDetails` | Objeto | Detalles de envío del anuncio. Consulte la [subsección siguiente sobre el objeto `adDeliveryDetails`](#adDeliveryDetails) para obtener más información sobre el contenido de este objeto. |
| `advertisement` | Objeto | Detalles del anuncio digital. Consulte la [subsección siguiente del objeto de anuncio](#advertisement) para obtener más información sobre el contenido de este objeto. |
| `campaign` | Objeto | Detalles de jerarquía de campaña. Consulte la [subsección siguiente sobre el objeto de campaña](#campaign-campaign) para obtener más información sobre el contenido de este objeto. |
| `conversionDetails` | Objeto | Detalles de conversión de un anuncio. Vea la [subsección debajo de](#conversionDetails) para obtener más información sobre el contenido de este objeto. |
| `eventType` | Cadena | El tipo de evento de Adobe Advertising. |
| `fees` | Objeto | Detalles de tarifas de Advertising. Consulte la [subsección siguiente sobre el objeto de tarifas](#fees) para obtener más información sobre el contenido de este objeto. |
| `inventory` | Objeto | Detalles de inventario. Vea la [subsección debajo de](#inventory) para obtener más información sobre el contenido de este objeto. |
| `productDetails` | Objeto | Detalles del anuncio del producto. Consulte la [subsección siguiente del objeto productDetails](#productDetails) para obtener más información sobre el contenido de este objeto. |
| `stitchId` | Cadena | ID de los servidores de publicidad de Adobe Advertising para rastrear las conversiones de clics en exploradores que bloquean cookies de terceros. |

## `adDeliveryDetails` {#adDeliveryDetails}

El objeto adDeliveryDetails proporciona información sobre dónde y cómo se entregó el anuncio, incluidos los sitios web de colocación y los identificadores de ubicación.

![Diagrama de esquema que muestra el objeto `adDeliveryDetails` y sus campos.](../../images/field-groups/advertising-full-extension/adDeliveryDetails.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `placementWebsite` | Cadena | El sitio web donde se mostró el anuncio. |
| `siteLinkText` | Cadena | Vínculo de sitio real seleccionado en el anuncio. |
| `interestLocationID` | Cadena | La ubicación deducida de la consulta de búsqueda. Por ejemplo, la consulta &quot;Hotel en Goa&quot; devuelve el ID de Goa, independientemente de la ubicación de navegación real del usuario. |
| `physicalLocationID` | Cadena | La ubicación de exploración del usuario, representada por un ID de referencia de la red de publicidad. Este ID no es un nombre de ubicación legible (como una ciudad o un país), sino un código asignado por la red de publicidad para identificar un objetivo geográfico. |

## `advertisement` {#advertisement}

El objeto de anuncio describe detalles sobre el anuncio digital, como sus identificadores, tipo, creativo, objetivo y palabras clave asociadas.

![Diagrama de esquema que muestra el objeto `advertisement` y sus campos.](../../images/field-groups/advertising-full-extension/advertisement.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `adId` | Cadena | El identificador del anuncio asociado con este evento. Este ID no está relacionado con el estándar del sector de Ad-ID. |
| `runtime` | Cadena | El tiempo de ejecución de la unidad de publicidad, distinto del tiempo de ejecución del explorador o del sistema operativo. Los valores posibles incluyen: `unknown` y `HTML5`. |
| `adClass` | Cadena | La clase de anuncio del evento de conducción: `display`, `video` o `social`. |
| `adUnitType` | Cadena | El identificador del código que procesa el anuncio en un explorador o dispositivo. Entre los posibles valores están:<ul><li>`linearVideo`: vídeo lineal</li><li>`interactiveVideo`: vídeo interactivo</li><li>`banner`: titular,</li><li>`richMediaBanner`: titular de medios enriquecidos,</li><li>`newsFeedVideo`: vídeo de fuente de noticias,</li><li>`newsFeedDisplay`: visualización de fuente de noticias,</li><li>`HTML5`: HTML5,</li><li>`inPageVideo`: en el vídeo de la página,</li><li>`inPageDisplay`: en la visualización de la página,</li><li>`facebook`: Facebook,</li><li>`twitter`: Twitter,</li><li>`linearTv`: TV lineal,</li><li>`vod`: vídeo bajo demanda</li></ul> |
| `promotedAssetId` | Cadena | El identificador del recurso promocionado en el anuncio asociado con este evento. |
| `creativeID` | Cadena | El identificador del creativo de publicidad (como un titular, un vídeo o un anuncio social) asociado con este evento. |
| `keywordID` | Cadena | El identificador de la palabra clave introducida por el usuario en una consulta de búsqueda que activó este evento. |
| `keyword` | Cadena | La palabra clave de anuncio por la que pujó el cliente. |
| `isDynamicSearchAd` | Booleano | Indica si el evento procede de un anuncio de búsqueda dinámica. |
| `audienceID` | Cadena | El identificador del segmento de audiencia al que se dirige el anuncio. |
| `adGroupID` | Cadena | El identificador del grupo de publicidad asociado con el anuncio que activó este evento. |
| `campaignID` | Cadena | El identificador de la campaña asociada con el anuncio que activó este evento. |
| `networkType` | Cadena | El tipo de red donde ocurrió el evento. Entre los posibles valores están: <ul><li>`search`: el anuncio se mostró en la red de búsqueda.</li><li>`content`: el anuncio se mostró en la red de contenido.</li></ul> |
| `matchType` | Cadena | El tipo de coincidencia de palabra clave. Entre los posibles valores están: <ul><li>`exact`: coincidencia exacta de la palabra clave</li><li>`broad`: coincidencia amplia de la palabra clave</li><li>`phrase`: coincidencia de frase de la palabra clave</li></ul> |

## `campaign` {#campaign}

El objeto de campaña define la jerarquía de campañas de publicidad, incluidos los identificadores de cuenta, anunciante, ubicación y paquete, junto con los detalles de moneda.

![Diagrama de esquema que muestra el objeto `campaign` y sus campos.](../../images/field-groups/advertising-full-extension/campaign.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `accountId` | Cadena | El identificador de la cuenta. |
| `dspId` | Cadena | El identificador de la Demand Side Platform (DSP) en la que se define la campaña. Normalmente, este identificador es el ID de Adobe Advertising Cloud DSP. |
| `campaignId` | Cadena | El identificador de la campaña. |
| `placementId` | Cadena | El identificador de la ubicación. |
| `packageId` | Cadena | El identificador del paquete de Advertising DSP. |
| `advertiserId` | Cadena | El identificador del anunciante. |
| `experimentId` | Cadena | El identificador del experimento. |
| `sampleGroupId` | Cadena | El identificador del grupo de muestra. |
| `currency` | Cadena | El código de divisa de facturación en formato ISO 4217 de la cuenta. Utiliza el patrón de expresión regular ^[A-Z]{3}$ (tres letras mayúsculas). Por ejemplo: USD, EUR. |

## `conversionDetails` {#conversionDetails}

El objeto conversionDetails captura información de seguimiento para las conversiones de anuncios, incluidos códigos de seguimiento, identidades y propiedades de conversión.

![Diagrama de esquema que muestra el objeto `conversionDetails` y sus campos.](../../images/field-groups/advertising-full-extension/conversionDetails.png "campo conversionDetails")

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `trackingCode` | Cadena | El código de seguimiento de conversión del evento. Para obtener una lista de posibles formatos, consulte [Formatos de ID de AMO](https://experienceleague.adobe.com/es/docs/advertising/integrations/customer-journey-analytics/ids#amo-id-formats). |
| `trackingIdentities` | Cadena | El EF ID o los detalles de identidad de seguimiento de un evento. Para obtener una lista de los posibles formatos, vea [Formatos EF ID](https://experienceleague.adobe.com/es/docs/advertising/integrations/customer-journey-analytics/ids#ef-id-formats). |
| `conversionProperties` | Objeto | Mapa de propiedades de conversión, representadas como una matriz de cadenas de pares clave-valor (como `subscriptions=253`). |

## `fees` {#fees}

El objeto de tarifas captura los medios, los datos y otros costes de publicidad, desglosados por Advertising DSP, cuenta y anunciante.

![Diagrama de esquema que muestra el objeto `fees` y sus campos.](../../images/field-groups/advertising-full-extension/fees.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `DSPMediaFees` | Número | Las tarifas de medios facturables por Advertising DSP. |
| `DSPDataFees` | Número | Las tarifas de datos facturables por Advertising DSP. |
| `DSPOtherFees` | Número | Otras tarifas facturables por Advertising DSP. |
| `accountMediaFees` | Número | Las tarifas de medios para la cuenta, pero no facturables por Advertising DSP. |
| `accountDataFees` | Número | Las tarifas de datos de la cuenta, pero no facturables por Advertising DSP. |
| `accountOtherFees` | Número | Otras tarifas de la cuenta pero no facturables por Advertising DSP. |
| `advertiserMediaFees` | Número | Las tarifas del anunciante de medios se cobran al anunciante desde la cuenta. |
| `advertiserDataFees` | Número | Otros cargos del anunciante cargados al anunciante desde la cuenta. |
| `advertiserOtherFees` | Número | Otros cargos del anunciante cargados al anunciante desde la cuenta. |
| `billableMediaNetSpend` | Número | Gasto neto facturable en publicidad en medios de comunicación. |
| `totalMediaNetSpend` | Número | Gasto neto total en publicidad en medios. |
| `billableDataNetSpend` | Número | Gasto neto facturable por publicidad de datos. |
| `billableOtherNetSpend` | Número | El gasto neto facturable por otros tipos de publicidad. |
| `totalBillableNetSpend` | Número | Gasto neto total facturable. |
| `totalNonBillableNetSpend` | Número | El gasto neto total no facturable. |
| `totalNetSpend` | Número | El gasto neto total. |

## `inventory` {#inventory}

El objeto de inventario registra detalles sobre la oportunidad de inventario de anuncios, incluidos los datos de sesión, los códigos de socio, los ID de sitio, la moneda de coste y las reglas de segmentación.

![Diagrama de esquema que muestra el objeto `inventory` y sus campos.](../../images/field-groups/advertising-full-extension/inventory.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `sessionId` | Cadena | El ID de sesión asociado a un evento de experiencia, que se utiliza para vincular eventos independientes que se produjeron en la misma sesión. |
| `feedID` | Cadena | Un ID compuesto del editor, el intercambio de anuncios y otras funciones. |
| `sspPartnerCode` | Cadena | El socio (intercambio) a través del cual Adobe Advertising Cloud recibe la oportunidad de inventario. |
| `siteID` | Cadena | El identificador del sitio web en el que se proporcionó la impresión publicitaria. |
| `costCurrency` | Cadena | El código de divisa en formato ISO 4217 usado para pagar a un socio por una oportunidad publicitaria. El valor debe seguir el patrón de expresión regular ^[A-Z]{3}$ (tres letras mayúsculas). Por ejemplo: USD, EUR. |
| `inventorySourceId` | Cadena | El ID del origen del inventario de Adobe Advertising Cloud en el que se entregó esta oportunidad. |
| `segment` | Objeto | Detalles asociados con las reglas de segmentación de usuarios. Entre sus propiedades se incluyen:<ul><li>`attributablePartnerId` (cadena): Identificador del proveedor del segmento propietario de attributeSegmentId.</li><li>`attributableSegmentId` (cadena): segmento acreditado por la segmentación de usuarios en la regla de segmentación de la ubicación. Esto se utiliza para los fines de seguimiento de costes y pago a socios.</li><li>`segments` (cadena): la intersección de los segmentos de usuario (a\) a los que pertenecía el usuario y (b\) a los que se dirigía el anuncio. Esta no es la lista completa de segmentos a los que pertenecía el usuario en el momento de la subasta.</li></ul> |
| `optimizationTag` | Cadena | La etiqueta relacionada con la optimización. |
| `attributableDeviceGraphId` | Cadena | El identificador del gráfico del dispositivo atribuido a un evento de conversión. |

## `productDetails` {#productDetails}

El objeto `productDetails` contiene información sobre los productos que aparecen en los anuncios de compra de [!DNL Adobe Advertising Search, Social, & Commerce], incluidos los identificadores de producto, el país, el idioma, la partición, el título y el tipo de anuncio.

![Diagrama de esquema que muestra el objeto `productDetails` y sus campos.](../../images/field-groups/advertising-full-extension/productDetails.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `productID` | Cadena | El identificador del producto que aparece en el anuncio asociado con este evento. |
| `country` | Cadena | El país de venta del producto que aparece en el anuncio asociado con el evento. |
| `language` | Cadena | El idioma de la información del producto, tal como se indica en la fuente de datos del Centro de comerciantes del cliente. |
| `partitionID` | Cadena | El identificador del grupo de productos asociado con el anuncio en este evento. |
| `title` | Cadena | El título del producto mostrado en el anuncio. |
| `adType` | Cadena | Tipo de anuncio del producto utilizado en [!DNL Google] campañas de compra. Entre los posibles valores están:<ul><li>`pla_with_pog`: cuando el evento provino de una compra a través de un anuncio de compra</li><li>`pla`: cuando el evento provino de un anuncio de compras.</li><li>`pla_multichannel`: cuando el evento de un anuncio de compra incluyó opciones para canales de compra &quot;en línea&quot; y &quot;locales&quot;.</li><li>`pla_with_promotion`: cuando el evento de un anuncio de compra mostraba una promoción de comerciante.</li></ul> |

## Próximos pasos

Este documento cubre la estructura y el caso de uso del grupo de campos de extensión [!DNL Advertising Cloud]. Para obtener más información sobre el propio grupo de campos, consulte el [repositorio XDM público](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/adcloud/experienceevent-all.schema.json).

Si utiliza este grupo de campos para recopilar datos de [!DNL Advertising] mediante Adobe Experience Platform Web SDK, consulte la guía sobre [configuración de una secuencia de datos](../../../datastreams/overview.md) para obtener información sobre cómo asignar datos a XDM en el servidor.
