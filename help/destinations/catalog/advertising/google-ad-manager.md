---
keywords: administrador de publicidad de Google;publicidad de Google;doble clic;DoubleClick AdX;DoubleClick;Administrador de publicidad de Google;Administrador de publicidad de Google
title: Destino de conexión de Google Ad Manager
description: 'Google Ad Manager, anteriormente conocido como DoubleClick para editores o DoubleClick AdX, es una plataforma de servicio de publicidad de Google que proporciona a los editores los medios para administrar la visualización de anuncios en sus sitios web, a través de vídeos y en aplicaciones móviles.  '
translation-type: tm+mt
source-git-commit: 6655714d4b57d9c414cd40529bcee48c7bcd862d
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 0%

---


# [!DNL Google Ad Manager] connection

[!DNL Google Ad Manager], anteriormente conocida como  [!DNL DoubleClick] para editores o  [!DNL DoubleClick AdX], es una plataforma de servicio de publicidad de la  [!DNL Google] que proporciona a los editores los medios para administrar la visualización de anuncios en sus sitios web, a través de vídeos y en aplicaciones móviles.

## Especificaciones de destino

Tenga en cuenta los siguientes detalles específicos de destinos [!DNL Google Ad Manager]:

* Puede enviar las [identidades](../../../identity-service/namespaces.md) siguientes a [!DNL Google Ads] destinos: [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en), ID de cookie de Google, IDFA, GAID, ID de Roku, ID de Microsoft e ID de Amazon Fire TV.
   * Google utilizará [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en) para los usuarios de destinatario en California y el ID de cookie de Google para todos los demás usuarios.
* Las audiencias activadas se crean mediante programación en la plataforma [!DNL Google].
* La plataforma no incluye actualmente una métrica de medición para validar una activación correcta. Consulte los recuentos de audiencias en Google para validar la integración y comprender el tamaño del objetivo de audiencias.

>[!IMPORTANT]
>
>Si desea crear su primer destino con [!DNL Google Ad Manager] y no ha habilitado la [funcionalidad de sincronización de ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) en el servicio de ID de Experience Cloud en el pasado (con Audience Manager u otras aplicaciones), póngase en contacto con el Servicio de consultoría de Adobe o con el Servicio de atención al cliente para habilitar la sincronización de ID. Si anteriormente había configurado [!DNL Google] integraciones en Audience Manager, las sincronizaciones de ID que había configurado continuarán con Platform.

### Tipo de exportación {#export-type}

**Exportación**  de segmentos: está exportando todos los miembros de un segmento (audiencia) al destino de Google.

## Requisitos previos

### Lista de permitidos

>[!NOTE]
>
>La lista de permitidos es obligatoria antes de configurar su primer [!DNL Google Ad Manager] destino en Platform. Asegúrese de que el proceso de lista de permitidos que se describe a continuación haya sido completado por [!DNL Google] antes de crear un destino.

Antes de crear el [!DNL Google Ad Manager] destino en Platform, debe ponerse en contacto con [!DNL Google] para que el Adobe se ponga en la lista de proveedores de datos permitidos y para que su cuenta se agregue a la lista de permitidos. Póngase en contacto con [!DNL Google] y proporcione la siguiente información:

* **ID**  de cuenta: es el ID de cuenta de Adobe con  [!DNL Google]. Póngase en contacto con el Servicio de atención al cliente de Adobe o con su representante de Adobe para obtener este ID.
* **ID**  del cliente: es el ID de cuenta de cliente de Adobe con  [!DNL Google]. Póngase en contacto con el Servicio de atención al cliente de Adobe o con su representante de Adobe para obtener este ID.
* **ID**  de red: esta es su cuenta con  [!DNL Google Ad Manager]
* **ID**  del vínculo de audiencia: esta es su cuenta con  [!DNL Google Ad Manager]
* El tipo de cuenta. DFP por comprador de Google o AdX.

## Configurar destino

En **[!UICONTROL Conexiones]** > **[!UICONTROL Destinos]**, seleccione **[!DNL Google Ad Manager]** y seleccione **[!UICONTROL Configurar]**.

![Destino de Connect Google Ad Manager](../../assets/catalog/advertising/google-ad-manager/catalog.png)

>[!NOTE]
>
>Si ya existe una conexión con este destino, puede ver un botón **[!UICONTROL Activar]** en la tarjeta de destino. Para obtener más información sobre la diferencia entre **[!UICONTROL Activar]** y **[!UICONTROL Configurar]**, consulte la sección [Catálogo](../../ui/destinations-workspace.md#catalog) de la documentación del espacio de trabajo de destino.

En el paso **Configuración** del flujo de trabajo de creación de destino, rellene la [!UICONTROL Información básica] para el destino.

![Información básica Google Ad Manager](../../assets/catalog/advertising/google-ad-manager/setup.png)

* **[!UICONTROL Nombre]**: Rellene el nombre preferido para este destino.
* **[!UICONTROL Descripción]**: Opcional. Por ejemplo, puede mencionar para qué campaña utiliza este destino.
* **[!UICONTROL Tipo]** de cuenta: Seleccione una opción, en función de su cuenta con Google:
   * Use `DFP by Google` para [!DNL DoubleClick] Publicadores
   * Use `AdX buyer` para [!DNL Google AdX]
* **[!UICONTROL ID]** de cuenta: Rellene su ID de cuenta con  [!DNL Google]. Puede ser su ID de red o su ID de vínculo de Audiencia. Normalmente, se trata de un ID de ocho dígitos.
* **[!UICONTROL Caso]** de uso de marketing: Los casos de uso de mercadotecnia indican la intención para la cual se exportarán los datos al destino. Puede seleccionar entre los casos de uso de mercadotecnia definidos por el Adobe o puede crear su propio caso de uso de mercadotecnia. Para obtener más información acerca de los casos de uso de mercadotecnia, consulte la [información general de las directivas de uso de datos](../../../data-governance/policies/overview.md).

>[!NOTE]
>
>Al configurar un [!DNL Google Ad Manager] destino, trabaje con su [!DNL Google Account Manager] o representante de Adobe para comprender qué tipo de cuenta tiene.

## Activar segmentos a [!DNL Google Ad Manager]

Para obtener instrucciones sobre cómo activar segmentos en [!DNL Google Ad Manager], consulte [Activar datos en destinos](../../ui/activate-destinations.md).

## Datos exportados

Para verificar si los datos se han exportado correctamente al destino [!DNL Google Ad Manager], compruebe su cuenta [!DNL Google Ad Manager]. Si la activación se ha realizado correctamente, las audiencias se rellenan en su cuenta.