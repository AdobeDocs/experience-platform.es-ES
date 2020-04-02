---
title: Google AdsDestination
seo-title: Destino de publicidades de Google
description: Google Ads, anteriormente conocido como Google AdWords, es un servicio de publicidad en línea que permite a las empresas pagar por publicidad a través de búsquedas de texto, visualizaciones gráficas, vídeos de YouTube y visualizaciones móviles dentro de la aplicación.
seo-description: Google Ads, anteriormente conocido como Google AdWords, es un servicio de publicidad en línea que permite a las empresas pagar por publicidad a través de búsquedas de texto, visualizaciones gráficas, vídeos de YouTube y visualizaciones móviles dentro de la aplicación.
translation-type: tm+mt
source-git-commit: 50e6b39c1eb0bda4f3b30991515fb1c13fa9ff87

---


# Destino de publicidades de Google

## Información general

Google Ads, anteriormente conocido como Google AdWords, es un servicio de publicidad en línea que permite a las empresas pagar por publicidad a través de búsquedas de texto, visualizaciones gráficas, vídeos de YouTube y visualizaciones móviles dentro de la aplicación.

## Especificaciones de destino

Tenga en cuenta los siguientes detalles que son específicos de los destinos de Google Ads:

* Puede enviar las siguientes [identidades](../../identity-service/namespaces.md) a los destinos de Google Ads: ID de cookie de **Google, IDFA, GAID, Roku ID, Microsoft ID, Amazon Fire TV ID**.
* Las audiencias activadas se crean mediante programación en la plataforma Google.
* Actualmente, CDP en tiempo real de Adobe no incluye una métrica de medición para validar una activación correcta. Consulte los recuentos de audiencias en Google para validar la integración y comprender el tamaño del objetivo de audiencias.

>[!IMPORTANT]
>
>Si desea crear su primer destino con Google Ads y no ha habilitado la funcionalidad [de sincronización de](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) ID en el servicio Experience Cloud ID en el pasado (con el administrador de Audiencias u otras aplicaciones), póngase en contacto con el servicio de consultoría de Adobe o con el servicio de atención al cliente para activar las sincronizaciones de ID. Si anteriormente había configurado integraciones de Google en el Administrador de Audiencias, las sincronizaciones de ID configuradas se transfieren a CDP en tiempo real de Adobe.

## Requisitos previos

### Cuenta existente de Google Ads

Google ha pausado todas las integraciones nuevas de Google Ads con proveedores de terceros. Debe tener una integración existente con Google Ads para poder realizar los pasos de la lista blanca en la siguiente sección y crear un destino de Google Ads en Adobe Real-time CDP.

### Lista blanca

>[!NOTE]
>
>Es obligatorio incluir en la lista blanca antes de configurar el primer destino de Google Ads en Adobe Real-time CDP. Asegúrese de que Google haya completado el proceso de lista de direcciones permitidas que se describe a continuación antes de crear un destino.

Antes de crear el destino de Google Ads en Adobe Real-time CDP, debe ponerse en contacto con Google para solicitar que Adobe aparezca en la lista de direcciones permitidas como proveedor de datos y que su cuenta se incluya en la lista de direcciones permitidas. Póngase en contacto con Google y proporcione la siguiente información:

* **ID** de cuenta: este es el ID de cuenta de Adobe con Google. Póngase en contacto con el Servicio de atención al cliente de Adobe o con su representante de Adobe para obtener este ID.
* **ID** del cliente: es el ID de cuenta de cliente de Adobe con Google. Póngase en contacto con el Servicio de atención al cliente de Adobe o con su representante de Adobe para obtener este ID.
* El tipo de cuenta: **AdWords**
* **ID** de Google AdWords: Este es su ID con Google. El formato de ID suele ser 123-456-7890.

## Crear destino

1. En **[!UICONTROL Connections > Destinations]**, seleccione Publicidades de Google y, a continuación, **[!UICONTROL Create destination]**.
   ![Destino de Connect Google Ads](/help/rtcdp/destinations/assets/google-2-destination.png)

2. En el flujo de trabajo Crear destino, rellene el [!UICONTROL Basic Information] para el destino.
   ![Información básica de Google Ads](/help/rtcdp/destinations/assets/google-2-basic-information.png)
* **[!UICONTROL Name]**:: Rellene el nombre preferido para este destino.
* **[!UICONTROL Description]**: Opcional. Por ejemplo, puede mencionar para qué campaña utiliza este destino.
* **[!UICONTROL Account Type]**:: AdWords es la única opción disponible.
* **[!UICONTROL Account ID]**:: Rellene su ID de cuenta con Google Ads. El formato de ID suele ser 123-456-7890.

## Activar segmentos en anuncios de Google

Para obtener instrucciones sobre cómo activar segmentos en publicidades de Google, consulte [Activar datos en destinos](/help/rtcdp/destinations/activate-destinations.md).

