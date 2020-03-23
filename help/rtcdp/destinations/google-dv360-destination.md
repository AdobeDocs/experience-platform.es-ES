---
title: Destino de Google Display y Video 360
seo-title: Destino de Google Display y Video 360
description: Display & Video 360, anteriormente conocido como DoubleClick Bid Manager, es una herramienta que se utiliza para ejecutar campañas digitales de resegmentación y dirigidas a la audiencia en las fuentes de inventario de dispositivos móviles, vídeo y visualización.
seo-description: 'Display & Video 360, anteriormente conocido como DoubleClick Bid Manager, es una herramienta que se utiliza para ejecutar campañas digitales de resegmentación y dirigidas a la audiencia en las fuentes de inventario de dispositivos móviles, vídeo y visualización. '
translation-type: tm+mt
source-git-commit: 810028edc662a7f52484e37cf0fbdfafe5db650f

---


# Destino de Google Display y Video 360

## Información general

Display &amp; Video 360, anteriormente conocido como DoubleClick Bid Manager, es una herramienta que se utiliza para ejecutar campañas digitales de resegmentación y dirigidas a la audiencia en las fuentes de inventario de dispositivos móviles, de vídeo y de visualización.

## Especificaciones de destino

Tenga en cuenta los siguientes detalles específicos de destinos de Google Display &amp; Video 360:

* Puede enviar las siguientes [identidades](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/identity_namespace_overview/identity_namespace_overview.md) a los destinos de Google Display &amp; Video 360: ID de cookie de **Google, IDFA, GAID, Roku ID, Microsoft ID, Amazon Fire TV ID**.
* Las audiencias activadas se crean mediante programación en la plataforma Google.
* Actualmente, CDP en tiempo real de Adobe no incluye una métrica de medición para validar la activación correcta. Consulte los recuentos de audiencias en Google para validar la integración y comprender el tamaño de la segmentación de audiencia.

>[!IMPORTANT]
>
>Si desea crear su primer destino con Google Display &amp; Video 360 y no ha habilitado la funcionalidad [de sincronización de](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) ID en el servicio Experience Cloud ID en el pasado (con Adobe Audience Manager u otras aplicaciones), póngase en contacto con el servicio de consultoría de Adobe o con el servicio de atención al cliente para habilitar la sincronización de ID. Si anteriormente había configurado integraciones de Google en Audience Manager, las sincronizaciones de ID que había configurado se transfieren a CDP en tiempo real de Adobe.

## Requisitos previos

### Lista blanca

>[!NOTE]
>
>Es obligatorio incluir la lista blanca antes de configurar el primer destino de Google Display &amp; Video 360 en Adobe Real-time CDP. Asegúrese de que Google haya completado el proceso de lista de direcciones permitidas que se describe a continuación antes de crear un destino.

Antes de crear el destino de Google Display &amp; Video 360 en Adobe Real-time CDP, debe ponerse en contacto con Google para solicitar que Adobe aparezca en la lista de direcciones permitidas como proveedor de datos y que se incluya su cuenta en la lista de direcciones permitidas. Póngase en contacto con Google y proporcione la siguiente información:

* **ID** de cuenta: este es el ID de cuenta de Adobe con Google. Póngase en contacto con el Servicio de atención al cliente de Adobe o con su representante de Adobe para obtener este ID.
* **ID** del cliente: es el ID de cuenta de cliente de Adobe con Google. Póngase en contacto con el Servicio de atención al cliente de Adobe o con su representante de Adobe para obtener este ID.
* **Tipo** de cuenta: use **[!DNL Invite advertiser]** para permitir que las audiencias se compartan solo con una marca específica de su cuenta de Display &amp; Video 360 o **[!DNL Invite partner]** para permitir que las audiencias se compartan con todas las marcas de su cuenta de Display &amp; Video 360.

## Crear destino

1. En **[!UICONTROL Conexiones > Destinos]**, seleccione Google Display &amp; Video 360 y, a continuación, **[!UICONTROL Crear destino]**.
   ![Destino de Connect Google Display y Video 360](/help/rtcdp/destinations/assets/google-dv360-destination.png)

2. En el asistente Crear destino, rellene la información básica del destino.
   ![Información básica Google Display &amp; Video 360](/help/rtcdp/destinations/assets/google-dv360-basic-information.png)
* **Nombre**: Rellene el nombre preferido para este destino.
* **Descripción**: Opcional. Por ejemplo, puede mencionar para qué campaña utiliza este destino.
* **Tipo** de cuenta: Seleccione una opción, en función de su cuenta con Google:
   * Utilícelo `Invite Advertiser` para permitir que las audiencias solo se compartan con una marca específica de su cuenta de Display &amp; Video 360.
   * Utilícelo `Invite Partner` para permitir que las audiencias se compartan con todas las marcas de su cuenta de Display &amp; Video 360.
* **ID** de cuenta: Rellene su ID **[!DNL Invite partner]** o **[!DNL Invite advertiser]** de cuenta con Google. Normalmente, se trata de un ID de seis o siete dígitos.

>[!NOTE]
>
>Al configurar un destino de Google Display &amp; Video 360, trabaje con el administrador de cuentas de Google o con un representante de Adobe para comprender qué tipo de cuenta tiene.

## Activar segmentos en Google Display &amp; Video 360

Para obtener instrucciones sobre cómo activar segmentos en Google Display &amp; Video 360, consulte [Activar datos en destinos](/help/rtcdp/destinations/activate-destinations.md).