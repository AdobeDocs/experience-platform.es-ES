---
keywords: google ad manager;google ad;doubleclick;DoubleClick AdX;DoubleClick;Google Ad Manager;Google ad manager; DFP
title: Conexión de Google Ad Manager
description: Google Ad Manager, anteriormente conocido como DoubleClick for Publishers o DoubleClick AdX, es una plataforma de servicio de publicidad de Google que proporciona a los editores los medios para administrar la visualización de anuncios en sus sitios web, a través de vídeo y en aplicaciones móviles.
exl-id: e93f1bd5-9d29-43a1-a9a6-8933f9d85150
source-git-commit: f163b1e3c60953192b2ddf543eb4f3e8df88799b
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 3%

---

# [!DNL Google Ad Manager] connection

## Información general {#overview}

[!DNL Google Ad Manager], anteriormente conocido como [!DNL DoubleClick for Publishers] (DFP) o [!DNL DoubleClick AdX], es una plataforma de servicio de publicidad de [!DNL Google] que proporciona a los editores los medios para administrar la visualización de anuncios en sus sitios web, a través de vídeo y en aplicaciones móviles.

## Detalles de destino {#specifics}

Tenga en cuenta los siguientes detalles que son específicos de [!DNL Google Ad Manager] destinos:

* Las audiencias activadas se crean mediante programación en la variable [!DNL Google] plataforma.
* [!DNL Platform] no incluye actualmente una métrica de medición para validar la activación correcta. Consulte los recuentos de audiencias en Google para validar la integración y comprender el tamaño de la segmentación de audiencia.

## Identidades admitidas {#supported-identities}

[!DNL Google Ad Manager] admite la activación de identidades descritas en la tabla siguiente.

| Identidad de Target | Descripción | Consideraciones |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Seleccione esta identidad de destino cuando la identidad de origen sea un área de nombres GAID. |
| IDFA | [!DNL Apple ID for Advertisers] | Seleccione esta identidad de destino cuando la identidad de origen sea un área de nombres IDFA. |
| UUID de AAM | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html), también conocido como [!DNL Device ID]. ID de dispositivo numérico de 38 dígitos que el Audience Manager asocia a cada dispositivo con el que interactúa. | Uso de Google [UUID de AAM](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en) para dirigirse a usuarios de California y al ID de cookie de Google para el resto de usuarios. |
| [!DNL Google] ID de cookie | [!DNL Google] ID de cookie | [!DNL Google] utiliza este ID para dirigirse a usuarios fuera de California. |
| RIDA | ID de Roku para publicidad. Este ID identifica de forma exclusiva los dispositivos Roku. |  |
| MAID | ID de publicidad de Microsoft. Este ID identifica de forma exclusiva los dispositivos que ejecutan Windows 10. |  |
| ID de Amazon Fire TV | Este ID identifica de forma exclusiva los Amazon Fire TV. |  |

{style=&quot;table-layout:auto&quot;}

## Tipo de exportación y frecuencia {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de segmentos]** | Está exportando todos los miembros de un segmento (audiencia) al destino de Google. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de flujo continuo son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como un perfil se actualiza en el Experience Platform en función de la evaluación de segmentos, el conector envía la actualización descendente a la plataforma de destino. Más información sobre [destinos de flujo continuo](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Requisitos previos {#prerequisites}

Si desea crear su primer destino con [!DNL Google Ad Manager] y no han habilitado [Funcionalidad de sincronización de ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) en el servicio de ID de Experience Cloud en el pasado (con Audience Manager u otras aplicaciones), póngase en contacto con el servicio de consultoría de Adobe o con el servicio de atención al cliente para habilitar las sincronizaciones de ID. Si ha configurado anteriormente [!DNL Google] integraciones en Audience Manager, las sincronizaciones de ID que ha configurado se transfieren a Platform.

### Permitir inclusión en la lista {#allow-listing}

>[!NOTE]
>
>La lista de permitidos es obligatoria antes de configurar la primera [!DNL Google Ad Manager] destino en Platform. Asegúrese de que el proceso de lista de permitidos que se describe a continuación se haya completado en [!DNL Google] antes de crear un destino.

Antes de crear la variable [!DNL Google Ad Manager] destino en Platform, debe ponerse en contacto con [!DNL Google] para que el Adobe se incluya en la lista de proveedores de datos permitidos y para que su cuenta se agregue a la lista de permitidos . Contacto [!DNL Google] y proporcione la siguiente información:

* **ID de cuenta**: ID de cuenta de Adobe con Google. ID de cuenta: 87933855.
* **ID de cliente**: ID de cuenta de cliente de Adobe con Google. ID de cliente: 89690775.
* **Código de red**: Esta es su [!DNL Google Ad Manager] identificador de red, encontrado en **[!UICONTROL Administración > Configuración global]** en la interfaz de Google, así como en la URL.
* **ID del vínculo de audiencia**: Este es un identificador específico asociado con su [!DNL Google Ad Manager] red (no su [!DNL Network code]), también se encuentra en **[!UICONTROL Administración > Configuración global]** en la interfaz de Google.
* El tipo de cuenta. DFP de Google o del comprador de AdX.

## Conectarse al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita la variable **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

While [configuración](../../ui/connect-destination.md) Para este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Nombre]**: Rellene el nombre preferido para este destino.
* **[!UICONTROL Descripción]**: Opcional. Por ejemplo, puede mencionar para qué campaña utiliza este destino.
* **[!UICONTROL Tipo de cuenta]**: Seleccione una opción, en función de su cuenta con Google:
   * Uso `DFP by Google` para [!DNL DoubleClick] para editores
   * Uso `AdX buyer` para [!DNL Google AdX]
* **[!UICONTROL ID de cuenta]**: Complete el ID del vínculo de audiencia con [!DNL Google].

>[!NOTE]
>
>Al configurar un [!DNL Google Ad Manager] destino, trabaje con su [!DNL Google Account Manager] o representante de Adobes para comprender qué tipo de cuenta tiene.

### Habilitar alertas {#enable-alerts}

Puede activar las alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista para suscribirse y recibir notificaciones sobre el estado de su flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar segmentos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita la variable **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Consulte [Activar datos de audiencia en destinos de exportación de segmentos de flujo continuo](../../ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre la activación de segmentos de audiencia en este destino.

## Datos exportados {#exported-data}

Para verificar si los datos se han exportado correctamente a la variable [!DNL Google Ad Manager] destino, compruebe su [!DNL Google Ad Manager] cuenta. Si la activación se ha realizado correctamente, las audiencias se rellenan en la cuenta.
