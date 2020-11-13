---
keywords: google ad manager;google ad;doubleclick;DoubleClick AdX;DoubleClick;Google Ad Manager;Google ad manager
title: Destino del administrador de publicidad de Google
seo-title: Destino del administrador de publicidad de Google
description: 'Google Ad Manager, anteriormente conocido como DoubleClick para editores o DoubleClick AdX, es una plataforma de servicio de publicidad de Google que proporciona a los editores los medios para administrar la visualización de anuncios en sus sitios web, a través de vídeos y en aplicaciones móviles. '
seo-description: 'Google Ad Manager, anteriormente conocido como DoubleClick para editores o DoubleClick AdX, es una plataforma de servicio de publicidad de Google que proporciona a los editores los medios para administrar la visualización de anuncios en sus sitios web, a través de vídeos y en aplicaciones móviles. '
translation-type: tm+mt
source-git-commit: 485c4b1c3c68755396da087d4b5864c8a36e64df
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 0%

---


# [!DNL Google Ad Manager Destination]

## Información general

[!DNL Google Ad Manager], anteriormente conocida como [!DNL DoubleClick] para editores o [!DNL DoubleClick AdX], es una plataforma de servicio de publicidad de [!DNL Google] que proporciona a los editores los medios para administrar la visualización de anuncios en sus sitios web, a través de vídeos y en aplicaciones móviles.

## Especificaciones de destino

Tenga en cuenta los siguientes detalles específicos de los [!DNL Google Ad Manager] destinos:

* Puede enviar las siguientes [identidades](../../identity-service/namespaces.md) a [!DNL Google Ad Manager] destinos: **ID de cookie de Google, IDFA, GAID, Roku ID, Microsoft ID, Amazon Fire TV ID**.
* Las audiencias activadas se crean mediante programación en la [!DNL Google] plataforma.
* El CDP en tiempo real de Adobe no incluye actualmente una métrica de medición para validar una activación correcta. Consulte los recuentos de audiencias en Google para validar la integración y comprender el tamaño del objetivo de audiencias.

>[!IMPORTANT]
>
>Si desea crear su primer destino con [!DNL Google Ad Manager] y no ha habilitado la funcionalidad [de sincronización de](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) ID en el servicio de ID de Experience Cloud en el pasado (con Audience Manager u otras aplicaciones), póngase en contacto con el servicio de consultoría de Adobe o con el servicio de atención al cliente para habilitar las sincronizaciones de ID. Si anteriormente había configurado [!DNL Google] integraciones en Audience Manager, las sincronizaciones de ID que había configurado se transfieren a Adobe Real-time CDP.

### Tipo de exportación {#export-type}

**[!DNL Segment Export]** - está exportando todos los miembros de un segmento (audiencia) al destino de Google.

## Requisitos previos 

### Lista de permitidos

>[!NOTE]
>
>La lista de permitidos es obligatoria antes de configurar su primer [!DNL Google Ad Manager] destino en Adobe Real-time CDP. Asegúrese de que el proceso de lista de permitidos que se describe a continuación se haya completado [!DNL Google] antes de crear un destino.

Antes de crear el [!DNL Google Ad Manager] destino en Adobe Real-time CDP, debe ponerse en contacto [!DNL Google] para que el Adobe se ponga en la lista de proveedores de datos permitidos y para que su cuenta se agregue a la lista de permitidos. Póngase en contacto [!DNL Google] y proporcione la siguiente información:

* **ID** de cuenta: es el ID de cuenta de Adobe con [!DNL Google]. Póngase en contacto con el Servicio de atención al cliente de Adobe o con su representante de Adobe para obtener este ID.
* **ID** del cliente: es el ID de cuenta de cliente de Adobe con [!DNL Google]. Póngase en contacto con el Servicio de atención al cliente de Adobe o con su representante de Adobe para obtener este ID.
* **ID** de red: esta es su cuenta con [!DNL Google Ad Manager]
* **ID** del vínculo de audiencia: esta es su cuenta con [!DNL Google Ad Manager]
* El tipo de cuenta. DFP por comprador de Google o AdX.

## Configurar destino

1. En **[!UICONTROL Conexiones]** > **[!UICONTROL Destinos]**, seleccione **[!DNL Google Ad Manager]** y seleccione **[!UICONTROL Configurar]**.
   ![Destino de Connect Google Ad Manager](/help/rtcdp/destinations/assets/google-1-destination.png)

   >[!NOTE]
   >
   >Si ya existe una conexión con este destino, puede ver un botón **[!UICONTROL Activar]** en la tarjeta de destino. Para obtener más información sobre la diferencia entre **[!UICONTROL Activar]** y **[!UICONTROL Configurar]**, consulte la sección [Catálogo](/help/rtcdp/destinations/destinations-workspace.md#catalog) de la documentación del espacio de trabajo de destino.

2. En el paso **Configuración** del flujo de trabajo de creación de destino, rellene la información  básica del destino. <br>

   ![Información básica Google Ad Manager](/help/rtcdp/destinations/assets/google-1-destination-setup-step.png)
* **[!UICONTROL Nombre]**: Rellene el nombre preferido para este destino.
* **[!UICONTROL Descripción]**: Opcional. Por ejemplo, puede mencionar para qué campaña utiliza este destino.
* **[!UICONTROL Tipo]** de cuenta: Seleccione una opción, en función de su cuenta con Google:
   * Usar `DFP by Google` para [!DNL DoubleClick] editores
   * Usar `AdX buyer` para [!DNL Google AdX]
* **[!UICONTROL ID]** de cuenta: Rellene su ID de cuenta con [!DNL Google]. Puede ser su ID de red o su ID de vínculo de Audiencia. Normalmente, se trata de un ID de ocho dígitos.
* **[!UICONTROL Caso]** de uso de marketing: Los casos de uso de mercadotecnia indican la intención para la cual se exportarán los datos al destino. Puede seleccionar entre los casos de uso de mercadotecnia definidos por el Adobe o puede crear su propio caso de uso de mercadotecnia. Para obtener más información sobre los casos de uso de mercadotecnia, consulte la página [Administración de datos en tiempo real de CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) . Para obtener información sobre los casos individuales de uso de mercadotecnia definidos por el Adobe, consulte la descripción general [de las políticas de uso de](/help/data-governance/policies/overview.md#core-actions)datos.

>[!NOTE]
>
> Al configurar un [!DNL Google Ad Manager] destino, trabaje con su representante [!DNL Google Account Manager] o Adobe para saber qué tipo de cuenta tiene.

## Activar segmentos para [!DNL Google Ad Manager]

Para obtener instrucciones sobre cómo activar segmentos en [!DNL Google Ad Manager], consulte [Activar datos en destinos](/help/rtcdp/destinations/activate-destinations.md).

## Datos exportados

Para verificar si los datos se han exportado correctamente al [!DNL Google Ad Manager] destino, compruebe su [!DNL Google Ad Manager] cuenta. Si la activación se ha realizado correctamente, las audiencias se rellenan en su cuenta.