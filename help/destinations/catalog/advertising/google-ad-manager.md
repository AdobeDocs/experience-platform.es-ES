---
keywords: google ad manager;google ad;doubleclick;DoubleClick AdX;DoubleClick;Google Ad Manager;Google ad manager; DFP
title: Conexión de Google Ad Manager
description: Google Ad Manager, anteriormente conocido como DoubleClick for Publishers o DoubleClick AdX, es una plataforma de servicio de publicidad de Google que proporciona a los editores los medios para administrar la visualización de anuncios en sus sitios web, a través de vídeo y en aplicaciones móviles.
exl-id: e93f1bd5-9d29-43a1-a9a6-8933f9d85150
source-git-commit: 4df2e7ce9c7e94da4ea0be50ba21232c639e2587
workflow-type: tm+mt
source-wordcount: '754'
ht-degree: 0%

---

# [!DNL Google Ad Manager] connection

## Información general {#overview}

[!DNL Google Ad Manager], anteriormente conocido como  [!DNL DoubleClick for Publishers] (DFP) o  [!DNL DoubleClick AdX], es una plataforma de servicio de publicidad de  [!DNL Google] que proporciona a los editores los medios para administrar la visualización de anuncios en sus sitios web, a través de vídeo y en aplicaciones móviles.

## Detalles de destino {#specifics}

Tenga en cuenta los siguientes detalles que son específicos de destinos [!DNL Google Ad Manager]:

* Las audiencias activadas se crean mediante programación en la plataforma [!DNL Google].
* [!DNL Platform] no incluye actualmente una métrica de medición para validar la activación correcta. Consulte los recuentos de audiencias en Google para validar la integración y comprender el tamaño de la segmentación de audiencia.

## Identidades admitidas {#supported-identities}

[!DNL Google Ad Manager] admite la activación de identidades descritas en la tabla siguiente.

| Identidad de Target | Descripción | Consideraciones |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Seleccione esta identidad de destino cuando la identidad de origen sea un área de nombres GAID. |
| IDFA | [!DNL Apple ID for Advertisers] | Seleccione esta identidad de destino cuando la identidad de origen sea un área de nombres IDFA. |
| UUID de AAM | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html), también conocido como  [!DNL Device ID]. ID de dispositivo numérico de 38 dígitos que el Audience Manager asocia a cada dispositivo con el que interactúa. | Google utiliza [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en) para dirigirse a los usuarios de California, y el ID de cookie de Google para el resto de los usuarios. |
| [!DNL Google] ID de cookie | [!DNL Google] ID de cookie | [!DNL Google] utiliza este ID para dirigirse a usuarios fuera de California. |
| RIDA | ID de Roku para publicidad. Este ID identifica de forma exclusiva los dispositivos Roku. |  |
| MAID | Microsoft Advertising ID. Este ID identifica de forma exclusiva los dispositivos que ejecutan Windows 10. |  |
| ID de Amazon Fire TV | Este ID identifica de forma exclusiva los Amazon Fire TV. |  |

## Tipo de exportación {#export-type}

**Exportación de segmentos** : está exportando todos los miembros de un segmento (audiencia) al destino de Google.

## Requisitos previos

Si desea crear su primer destino con [!DNL Google Ad Manager] y no ha habilitado la [funcionalidad de sincronización de ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) en el servicio de ID de Experience Cloud en el pasado (con el Audience Manager u otras aplicaciones), póngase en contacto con el servicio de consultoría de Adobe o con el servicio de atención al cliente para habilitar las sincronizaciones de ID. Si anteriormente había configurado [!DNL Google] integraciones en Audience Manager, las sincronizaciones de ID que había configurado se transfieren a Platform.

## Lista de permitidos

>[!NOTE]
>
>La lista de permitidos es obligatoria antes de configurar el primer destino [!DNL Google Ad Manager] en Platform. Asegúrese de que el proceso de lista de permitidos que se describe a continuación se haya completado por [!DNL Google] antes de crear un destino.

Antes de crear el [!DNL Google Ad Manager] destino en Platform, debe ponerse en contacto con [!DNL Google] para que el Adobe se incluya en la lista de proveedores de datos permitidos y para que su cuenta se agregue a la lista de permitidos . Póngase en contacto con [!DNL Google] y proporcione la siguiente información:

* **ID de cuenta** : es el ID de cuenta de Adobe con  [!DNL Google]. Póngase en contacto con el Servicio de atención al cliente de Adobe o con su representante de Adobe para obtener este ID.
* **ID**  de cliente: es el ID de cuenta de cliente de Adobe con  [!DNL Google]. Póngase en contacto con el Servicio de atención al cliente de Adobe o con su representante de Adobe para obtener este ID.
* **ID**  de red: esta es su cuenta con  [!DNL Google Ad Manager]
* **ID del vínculo de audiencia** : esta es su cuenta con  [!DNL Google Ad Manager]
* El tipo de cuenta. DFP de un comprador de Google o AdX.

## Configurar destino

En **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, seleccione **[!DNL Google Ad Manager]** y seleccione **[!UICONTROL Configure]**.

![Conectar destino de Google Ad Manager](../../assets/catalog/advertising/google-ad-manager/catalog.png)

>[!NOTE]
>
>Si ya existe una conexión con este destino, puede ver un botón **[!UICONTROL Activate]** en la tarjeta de destino. Para obtener más información sobre la diferencia entre **[!UICONTROL Activate]** y **[!UICONTROL Configure]**, consulte la sección [Catalog](../../ui/destinations-workspace.md#catalog) de la documentación del espacio de trabajo de destino.

En el paso **Configuración** del flujo de trabajo de creación de destino, rellene la [!UICONTROL Información básica] para el destino.

![Información básica Google Ad Manager](../../assets/catalog/advertising/google-ad-manager/setup.png)

* **[!UICONTROL Nombre]**: Rellene el nombre preferido para este destino.
* **[!UICONTROL Descripción]**: Opcional. Por ejemplo, puede mencionar para qué campaña utiliza este destino.
* **[!UICONTROL Tipo]** de cuenta: Seleccione una opción, en función de su cuenta con Google:
   * Usar `DFP by Google` para [!DNL DoubleClick] para editores
   * Usar `AdX buyer` para [!DNL Google AdX]
* **[!UICONTROL ID de cuenta]**: Rellene su ID de cuenta con  [!DNL Google]. Puede ser su ID de red o su ID de vínculo de audiencia. Normalmente, se trata de un ID de ocho dígitos.
* **[!UICONTROL Acción de marketing]**: Las acciones de marketing indican la intención para la que se exportarán los datos al destino. Puede seleccionar entre las acciones de marketing definidas por el Adobe o crear su propia acción de marketing. Para obtener más información sobre las acciones de marketing, consulte [Información general sobre las políticas de uso de datos](../../../data-governance/policies/overview.md).

>[!NOTE]
>
>Al configurar un destino [!DNL Google Ad Manager], trabaje con su [!DNL Google Account Manager] o representante de Adobe para comprender qué tipo de cuenta tiene.

## Activar segmentos en [!DNL Google Ad Manager]

Para obtener instrucciones sobre cómo activar segmentos en [!DNL Google Ad Manager], consulte [Activar datos en destinos](../../ui/activate-destinations.md).

## Datos exportados

Para verificar si los datos se han exportado correctamente al destino [!DNL Google Ad Manager] , compruebe su cuenta [!DNL Google Ad Manager]. Si la activación se ha realizado correctamente, las audiencias se rellenan en la cuenta.
