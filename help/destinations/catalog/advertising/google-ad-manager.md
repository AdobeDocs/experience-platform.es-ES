---
keywords: Google Ad Manager;Google Ad;doubleclick;DoubleClick AdX;DoubleClick;Google Ad Manager;Google Ad Manager; DFP
title: Conexión de Google Ad Manager
description: Google Ad Manager, anteriormente conocido como DoubleClick for Publishers o DoubleClick AdX, es una plataforma de servicio de anuncios de Google que ofrece a los editores los medios para administrar la visualización de anuncios en sus sitios web, a través de vídeo y en aplicaciones móviles.
exl-id: e93f1bd5-9d29-43a1-a9a6-8933f9d85150
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1121'
ht-degree: 7%

---

# [!DNL Google Ad Manager] conexión

>[!IMPORTANT]
>
> Google está publicando cambios en la [API de Google Ads](https://developers.google.com/google-ads/api/docs/start), [Customer Match](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html) y la [API de Display &amp; Video 360](https://developers.google.com/display-video/api/guides/getting-started/overview) para admitir los requisitos relacionados con el cumplimiento y el consentimiento definidos en la [Ley de Mercados Digitales](https://digital-markets-act.ec.europa.eu/index_es) (DMA) de la Unión Europea ([Política de consentimiento del Usuario de la UE](https://www.google.com/about/company/user-consent-policy/)). La aplicación de estos cambios en los requisitos de consentimiento está activa desde el 6 de marzo de 2024.
><br/>
>Para adherirse a la política de consentimiento de usuario de la UE y seguir creando listas de audiencia para usuarios en el Espacio Económico Europeo (EEE), los anunciantes y socios deben asegurarse de que están pasando el consentimiento del usuario final al cargar datos de audiencia. Como socio de Google, Adobe le proporciona las herramientas necesarias para cumplir con estos requisitos de consentimiento según la DMA en la Unión Europea.
><br/>
>Los clientes que hayan adquirido Adobe Privacy &amp; Security Shield y hayan configurado una [política de consentimiento](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) para filtrar los perfiles no consentidos no tienen que realizar ninguna acción.
><br/>
>Los clientes que no hayan adquirido Adobe Privacy &amp; Security Shield deben utilizar las funciones de [definición de segmento](../../../segmentation/home.md#segment-definitions) de [Generador de segmentos](../../../segmentation/ui/segment-builder.md) para filtrar los perfiles no consentidos y así poder seguir utilizando los destinos de Real-Time CDP Google existentes sin interrupción.


[!DNL Google Ad Manager], anteriormente conocido como [!DNL DoubleClick for Publishers] (DFP) o [!DNL DoubleClick AdX], es una plataforma de servicio de anuncios de [!DNL Google] que proporciona a los editores los medios para administrar la visualización de anuncios en sus sitios web, a través de vídeo y en aplicaciones móviles.

## Detalles del destino {#specifics}

Tenga en cuenta los siguientes detalles que son específicos de [!DNL Google Ad Manager] destinos:

* Las audiencias activadas se crean mediante programación en la plataforma [!DNL Google].
* [!DNL Experience Platform] no incluye actualmente una métrica de medición para validar la activación correcta. Consulte los recuentos de audiencias en Google para validar la integración y comprender el tamaño de la segmentación de audiencia.
* Después de asignar una audiencia a un destino [!DNL Google Ad Manager], el nombre de la audiencia aparece inmediatamente en la interfaz de usuario [!DNL Google Ad Manager].
* La población del segmento necesita entre 24 y 48 horas para aparecer en [!DNL Google Ad Manager]. Además, las audiencias deben tener un tamaño de audiencia de al menos 50 perfiles para poder mostrarse en [!DNL Google Ad Manager]. Las audiencias con tamaños menores a 50 perfiles no se rellenarán en [!DNL Google Ad Manager].

## Identidades admitidas {#supported-identities}

[!DNL Google Ad Manager] admite la activación de audiencias en función de las identidades mostradas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidad | Descripción | Consideraciones |
|---|---|---|
| GAID | [!DNL Google Advertising ID] |  |
| IDFA | [!DNL Apple ID for Advertisers] |  |
| UUID DE AAM | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html), también conocido como [!DNL Device ID]. Un ID de dispositivo numérico de 38 dígitos que Audience Manager asocia a cada dispositivo con el que interactúa. | Google usa [UUID de AAM](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html) para segmentar usuarios en California y el ID de cookie de Google para todos los demás usuarios. |
| ID de cookie [!DNL Google] | ID de cookie [!DNL Google] | [!DNL Google] usa este identificador para dirigirse a usuarios fuera de California. |
| RIDA | ID de Roku para Advertising. Este ID identifica de forma exclusiva los dispositivos Roku. |  |
| CRIADA | ID de Microsoft Advertising. Este ID identifica de forma exclusiva los dispositivos que ejecutan Windows 10. |  |
| ID de Amazon Fire TV | Este ID identifica de forma exclusiva los Amazon Fire TV. |  |

{style="table-layout:auto"}

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipos de audiencias puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiencias generadas a través del [servicio de segmentación](../../../segmentation/home.md) de Experience Platform. |
| Cargas personalizadas | ✓ | Las audiencias [importadas](../../../segmentation/ui/audience-portal.md#import-audience) en Experience Platform desde archivos CSV. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de audiencia]** | Va a exportar todos los miembros de una audiencia al destino de Google. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform basado en la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Requisitos previos {#prerequisites}

Si desea crear su primer destino con [!DNL Google Ad Manager] y no ha habilitado la [funcionalidad de sincronización de ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) en el servicio de Experience Cloud ID en el pasado (con Audience Manager u otras aplicaciones), póngase en contacto con Adobe Consulting o con el Servicio de atención al cliente para habilitar las sincronizaciones de ID. Si ya había configurado [!DNL Google] integraciones en Audience Manager, las sincronizaciones de ID que configuró se transfieren a Experience Platform.

### Lista de permitidos {#allow-listing}

La inclusión en la lista de permitidos es obligatoria antes de configurar su primer destino de [!DNL Google Ad Manager] en Experience Platform. Asegúrese de completar el proceso de inclusión en la lista de permitidos que se describe a continuación antes de crear su destino.

1. Siga los pasos descritos en la [documentación de Google Ad Manager](https://support.google.com/admanager/answer/3289669?hl=en) para agregar Adobe como plataforma de administración de datos vinculada (DMP).
2. En la interfaz de [!DNL Google Ad Manager], vaya a **[!UICONTROL Administración]** > **[!UICONTROL Configuración global]** > **[!UICONTROL Configuración de red]** y habilite el control deslizante **[!UICONTROL Acceso a la API]**.

## Conexión al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita los **[!UICONTROL permisos de control de acceso](/help/access-control/home.md#permissions) de Ver destinos]** y **[!UICONTROL Administrar destinos]**[5}. Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_gam_appendSegmentID"
>title="Anexar el ID de público al nombre de público"
>abstract="Seleccione esta opción para que el nombre de público en Google Ad Manager incluya el ID de público de Experience Platform, de esta manera: `Audience Name (Audience ID)`"

Mientras [configura](../../ui/connect-destination.md) este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Nombre]**: rellene el nombre preferido para este destino.
* **[!UICONTROL Descripción]**: Opcional. Por ejemplo, puede mencionar para qué campaña está usando este destino.
* **[!UICONTROL ID de cuenta]**: escribe tu [!DNL Audience Link ID] desde tu cuenta de [!DNL Google]. Este es un identificador específico asociado con su red [!DNL Google Ad Manager] (no con su [!DNL Network code]). Puede encontrar esto en **[!UICONTROL Administración > Configuración global]** en la interfaz de [!DNL Google Ad Manager].
* **[!UICONTROL Tipo de cuenta]**: selecciona una opción, según tu cuenta con Google:
   * Usar `DFP by Google` para [!DNL DoubleClick] para editores
   * Usar `AdX buyer` para [!DNL Google AdX]
* **[!UICONTROL Anexar ID de audiencia al nombre de audiencia]**: seleccione esta opción para que el nombre de audiencia en Google Ad Manager incluya el ID de audiencia de Experience Platform, así: `Audience Name (Audience ID)`.

>[!NOTE]
>
>Al configurar un destino de [!DNL Google Ad Manager], colabore con su representante de [!DNL Google Account Manager] o Adobe para saber qué tipo de cuenta tiene.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando termine de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita los **[!UICONTROL permisos de control de acceso]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]**[para ](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Consulte [Activar datos de audiencia en destinos de exportación de audiencia de streaming](../../ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

## Datos exportados {#exported-data}

Para comprobar si los datos se han exportado correctamente al destino [!DNL Google Ad Manager], compruebe su cuenta de [!DNL Google Ad Manager]. Si la activación se ha realizado correctamente, las audiencias se rellenan en la cuenta.

## Resolución de problemas {#troubleshooting}

Si encuentra algún error al utilizar este destino y necesita ponerse en contacto con Adobe o Google, mantenga los siguientes ID a mano.

Estos son los ID de cuenta de Google de Adobe:

* **[!UICONTROL Id. de cuenta]**: 87933855
* **[!UICONTROL ID de cliente]**: 89690775