---
title: Google AdsDestination
seo-title: Destino de publicidades de Google
description: Google Ads, anteriormente conocido como Google AdWords, es un servicio de publicidad en línea que permite a las empresas pagar por publicidad a través de búsquedas de texto, visualizaciones gráficas, vídeos de YouTube y visualizaciones móviles dentro de la aplicación.
seo-description: Google Ads, anteriormente conocido como Google AdWords, es un servicio de publicidad en línea que permite a las empresas pagar por publicidad a través de búsquedas de texto, visualizaciones gráficas, vídeos de YouTube y visualizaciones móviles dentro de la aplicación.
translation-type: tm+mt
source-git-commit: 7f3df12da5e93c3d0cc53eed1aa603ddbafdb0b2
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 0%

---


# [!DNL Google Ads] Destino

## Información general

[!DNL Google Ads], anteriormente conocido como [!DNL Google AdWords][!DNL YouTube] , es un servicio de publicidad en línea que permite a las empresas pagar por publicidad a través de búsquedas basadas en texto, visualizaciones gráficas, vídeos y visualizaciones móviles dentro de la aplicación.

## Especificaciones de destino

Tenga en cuenta los siguientes detalles específicos de los [!DNL Google Ads] destinos:

* Puede enviar las siguientes [identidades](../../identity-service/namespaces.md) a [!DNL Google Ads] destinos: **ID de cookie de Google, IDFA, GAID, Roku ID, Microsoft ID, Amazon Fire TV ID**.
* Las audiencias activadas se crean mediante programación en la [!DNL Google] plataforma.
* El CDP en tiempo real de Adobe no incluye actualmente una métrica de medición para validar una activación correcta. Consulte los recuentos de audiencias en Google para validar la integración y comprender el tamaño del objetivo de audiencias.

>[!IMPORTANT]
>
>Si desea crear su primer destino con [!DNL Google Ads] y no ha habilitado la funcionalidad [de sincronización de](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) ID en el servicio de ID de Experience Cloud en el pasado (con Audience Manager u otras aplicaciones), póngase en contacto con el servicio de consultoría de Adobe o con el servicio de atención al cliente para habilitar las sincronizaciones de ID. Si anteriormente había configurado integraciones de Google en Audience Manager, las sincronizaciones de ID que había configurado se transfieren a CDP en tiempo real de Adobe.

## Requisitos previos

### Cuenta [!DNL Google Ads] existente

[!DNL Google] ha pausado [!DNL Google Ads] integraciones nuevas con proveedores de terceros. Debe tener una integración existente con [!DNL Google Ads] para poder realizar los pasos de lista de permitidos en la siguiente sección y crear un [!DNL Google Ads] destino en Adobe Real-time CDP.

### Lista de permitidos

>[!NOTE]
>
>La lista de permitidos es obligatoria antes de configurar su primer [!DNL Google Ads] destino en Adobe Real-time CDP. Asegúrese de que el proceso de lista de permitidos que se describe a continuación se haya completado [!DNL Google] antes de crear un destino.

Antes de crear el [!DNL Google Ads] destino en Adobe Real-time CDP, debe ponerse en contacto [!DNL Google] para que el Adobe se ponga en la lista de proveedores de datos permitidos y para que su cuenta se agregue a la lista de permitidos. Póngase en contacto [!DNL Google] y proporcione la siguiente información:

* **ID** de cuenta: es el ID de cuenta de Adobe con [!DNL Google]. Póngase en contacto con el Servicio de atención al cliente de Adobe o con su representante de Adobe para obtener este ID.
* **ID** del cliente: es el ID de cuenta de cliente de Adobe con [!DNL Google]. Póngase en contacto con el Servicio de atención al cliente de Adobe o con su representante de Adobe para obtener este ID.
* El tipo de cuenta: **AdWords**
* **ID** de Google AdWords: Este es su ID con [!DNL Google]. El formato de ID suele ser 123-456-7890.

## Crear destino

1. En **[!UICONTROL Conexiones > Destinos]**, seleccione [!DNL Google Ads]y seleccione **[!UICONTROL Crear destino]**.
   ![Destino de Connect Google Ads](/help/rtcdp/destinations/assets/google-2-destination.png)

2. En el paso **Configuración** del flujo de trabajo de creación de destino, rellene la información  básica del destino. <br>

   ![Información básica de Google Ads](/help/rtcdp/destinations/assets/google-2-destination-setup-step.png)
* **[!UICONTROL Nombre]**: Rellene el nombre preferido para este destino.
* **[!UICONTROL Descripción]**: Opcional. Por ejemplo, puede mencionar para qué campaña utiliza este destino.
* **[!UICONTROL Tipo]** de cuenta: AdWords es la única opción disponible.
* **[!UICONTROL ID]** de cuenta: Rellene su ID de cuenta con [!DNL Google Ads]. El formato de ID suele ser 123-456-7890.
* **[!UICONTROL Caso]** de uso de marketing: Los casos de uso de mercadotecnia indican la intención para la cual se exportarán los datos al destino. Puede seleccionar entre los casos de uso de mercadotecnia definidos por el Adobe o puede crear su propio caso de uso de mercadotecnia. Para obtener más información sobre los casos de uso de mercadotecnia, consulte la página [Administración de datos en tiempo real de CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) . Para obtener información sobre los casos individuales de uso de mercadotecnia definidos por el Adobe, consulte la descripción general [de las políticas de uso de](/help/data-governance/policies/overview.md#core-actions)datos.

## Activar segmentos para [!DNL Google Ads]

Para obtener instrucciones sobre cómo activar segmentos en [!DNL Google Ads], consulte [Activar datos en destinos](/help/rtcdp/destinations/activate-destinations.md).

## Datos exportados

Para verificar si los datos se han exportado correctamente al [!DNL Google Ads] destino, compruebe su [!DNL Google Ads] cuenta. Si la activación se ha realizado correctamente, las audiencias se rellenan en su cuenta.