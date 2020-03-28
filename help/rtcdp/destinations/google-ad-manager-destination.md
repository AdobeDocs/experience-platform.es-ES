---
title: Destino del administrador de publicidad de Google
seo-title: Destino del administrador de publicidad de Google
description: 'Google Ad Manager, anteriormente conocido como DoubleClick para editores o DoubleClick AdX, es una plataforma de servicio de publicidad de Google que proporciona a los editores los medios para administrar la visualización de anuncios en sus sitios web, a través de vídeos y en aplicaciones móviles. '
seo-description: 'Google Ad Manager, anteriormente conocido como DoubleClick para editores o DoubleClick AdX, es una plataforma de servicio de publicidad de Google que proporciona a los editores los medios para administrar la visualización de anuncios en sus sitios web, a través de vídeos y en aplicaciones móviles. '
translation-type: tm+mt
source-git-commit: 336aa90cf1e059a92a36dd0ef3222ef6a6f5123b

---


# Destino del administrador de publicidad de Google

## Información general

Google Ad Manager, anteriormente conocido como DoubleClick para editores o DoubleClick AdX, es una plataforma de servicio de publicidad de Google que proporciona a los editores los medios para administrar la visualización de anuncios en sus sitios web, a través de vídeos y en aplicaciones móviles.

## Especificaciones de destino

Tenga en cuenta los siguientes detalles específicos de los destinos del Administrador de publicidad de Google:

* Puede enviar las siguientes [identidades](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/identity_namespace_overview/identity_namespace_overview.md) a los destinos del Administrador de publicidad de Google: ID de cookie de **Google, IDFA, GAID, Roku ID, Microsoft ID, Amazon Fire TV ID**.
* Las audiencias activadas se crean mediante programación en la plataforma Google.
* Actualmente, CDP en tiempo real de Adobe no incluye una métrica de medición para validar una activación correcta. Consulte los recuentos de audiencias en Google para validar la integración y comprender el tamaño del objetivo de audiencias.

>[!IMPORTANT]
>
>Si desea crear su primer destino con Google Ad Manager y no ha habilitado la funcionalidad [de sincronización de](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) ID en el servicio Experience Cloud ID en el pasado (con el administrador de Audiencias u otras aplicaciones), póngase en contacto con el servicio de consultoría de Adobe o con el servicio de atención al cliente para activar las sincronizaciones de ID. Si anteriormente había configurado integraciones de Google en el Administrador de Audiencias, las sincronizaciones de ID configuradas se transfieren a CDP en tiempo real de Adobe.

## Requisitos previos

### Lista blanca

>[!NOTE]
>
>Es obligatorio incluir una lista blanca antes de configurar el primer destino de Google Ad Manager en CDP en tiempo real de Adobe. Asegúrese de que Google haya completado el proceso de lista de direcciones permitidas que se describe a continuación antes de crear un destino.

Antes de crear el destino de Google Ad Manager en Adobe Real-time CDP, debe ponerse en contacto con Google para solicitar que Adobe aparezca en la lista de direcciones permitidas como proveedor de datos y que su cuenta se incluya en la lista de direcciones permitidas. Póngase en contacto con Google y proporcione la siguiente información:

* **ID** de cuenta: este es el ID de cuenta de Adobe con Google. Póngase en contacto con el Servicio de atención al cliente de Adobe o con su representante de Adobe para obtener este ID.
* **ID** del cliente: es el ID de cuenta de cliente de Adobe con Google. Póngase en contacto con el Servicio de atención al cliente de Adobe o con su representante de Adobe para obtener este ID.
* **ID** de red: esta es su cuenta con Google Ad Manager
* **ID** del vínculo de Audiencia: esta es su cuenta con Google Ad Manager
* El tipo de cuenta. **DFP por comprador** de Google **o** AdX.

## Crear destino

1. En **[!UICONTROL Connections > Destinations]**, seleccione Administrador de publicidad de Google y, a continuación, **[!UICONTROL Create destination]**.
   ![Destino de Connect Google Ad Manager](/help/rtcdp/destinations/assets/google-1-destination.png)

2. En el flujo de trabajo Crear destino, rellene el [!UICONTROL Basic Information] para el destino.
   ![Información básica Google Ad Manager](/help/rtcdp/destinations/assets/google-1-basic-information.png)
* **[!UICONTROL Name]**:: Rellene el nombre preferido para este destino.
* **[!UICONTROL Description]**: Opcional. Por ejemplo, puede mencionar para qué campaña utiliza este destino.
* **[!UICONTROL Account Type]**:: Seleccione una opción, en función de su cuenta con Google:
   * Usar `DFP by Google` para DoubleClick para editores
   * Usar `AdX buyer` para Google AdX
* **[!UICONTROL Account ID]**:: Rellene su ID de cuenta con Google. Puede ser su ID de red o su ID de vínculo de Audiencia. Normalmente, se trata de un ID de ocho dígitos.

>[!NOTE]
>
>Al configurar un destino de Google Ad Manager, trabaje con su administrador de cuentas de Google o con un representante de Adobe para comprender qué tipo de cuenta tiene.

## Activar segmentos en Google Ad Manager

Para obtener instrucciones sobre cómo activar segmentos en el Administrador de publicidad de Google, consulte [Activar datos en destinos](/help/rtcdp/destinations/activate-destinations.md).