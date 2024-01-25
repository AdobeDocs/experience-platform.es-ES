---
keywords: Google Ad Manager;Google Ad;doubleclick;DoubleClick AdX;DoubleClick;Google Ad Manager;Google Ad Manager; DFP
title: Conexión de Google Ad Manager
description: Google Ad Manager, anteriormente conocido como DoubleClick for Publishers o DoubleClick AdX, es una plataforma de servicio de anuncios de Google que ofrece a los editores los medios para administrar la visualización de anuncios en sus sitios web, a través de vídeo y en aplicaciones móviles.
exl-id: e93f1bd5-9d29-43a1-a9a6-8933f9d85150
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 5%

---

# [!DNL Google Ad Manager] conexión

## Información general {#overview}

[!DNL Google Ad Manager], anteriormente conocido como [!DNL DoubleClick for Publishers] (DFP) o [!DNL DoubleClick AdX], es una plataforma de servicio de anuncios de [!DNL Google] que proporciona a los editores los medios para administrar la visualización de anuncios en sus sitios web, a través de vídeo y en aplicaciones móviles.

## Detalles del destino {#specifics}

Tenga en cuenta los siguientes detalles específicos de [!DNL Google Ad Manager] destinos:

* Las audiencias activadas se crean mediante programación en [!DNL Google] plataforma.
* [!DNL Platform] actualmente no incluye una métrica de medición para validar que la activación se haya realizado correctamente. Consulte los recuentos de audiencias en Google para validar la integración y comprender el tamaño de la segmentación de audiencia.
* Después de asignar una audiencia a una [!DNL Google Ad Manager] destino, el nombre de la audiencia aparece inmediatamente en el [!DNL Google Ad Manager] interfaz de usuario.
* La población de segmentos necesita entre 24 y 48 horas para aparecer en [!DNL Google Ad Manager]. Además, las audiencias deben tener un tamaño de audiencia de al menos 50 perfiles para poder mostrarse en [!DNL Google Ad Manager]. Las audiencias con tamaños inferiores a 50 perfiles no se rellenarán en [!DNL Google Ad Manager].

## Identidades admitidas {#supported-identities}

[!DNL Google Ad Manager] admite la activación de audiencias en función de las identidades mostradas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidad | Descripción | Consideraciones |
|---|---|---|
| GAID | [!DNL Google Advertising ID] |  |
| IDFA | [!DNL Apple ID for Advertisers] |  |
| AAM UUID DE USUARIO | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html), también conocido como [!DNL Device ID]. Un ID de dispositivo numérico de 38 dígitos que el Audience Manager asocia a cada dispositivo con el que interactúa. | Google utiliza [AAM UUID DE USUARIO](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html) para dirigirse a los usuarios de California y el ID de cookie de Google para todos los demás usuarios. |
| [!DNL Google] ID de cookie | [!DNL Google] ID de cookie | [!DNL Google] utiliza este ID para dirigirse a usuarios fuera de California. |
| RIDA | ID de Roku para publicidad. Este ID identifica de forma exclusiva los dispositivos Roku. |  |
| CRIADA | ID de publicidad de Microsoft. Este ID identifica de forma exclusiva los dispositivos que ejecutan Windows 10. |  |
| ID de Amazon Fire TV | Este ID identifica de forma exclusiva los Amazon Fire TV. |  |

{style="table-layout:auto"}

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipos de audiencias puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiencias generadas mediante el Experience Platform [Servicio de segmentación](../../../segmentation/home.md). |
| Cargas personalizadas | ✓ | Audiencias [importado](../../../segmentation/ui/overview.md#import-audience) en el Experience Platform desde archivos CSV. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de audiencia]** | Va a exportar todos los miembros de una audiencia al destino de Google. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform según la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Requisitos previos {#prerequisites}

Si quiere crear su primer destino con [!DNL Google Ad Manager] y no han habilitado el [Funcionalidad de sincronización de ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) en el Servicio de ID de Experience Cloud en el pasado (con Audience Manager u otras aplicaciones), póngase en contacto con el Servicio de consultoría de Adobe o con el Servicio de atención al cliente para habilitar las sincronizaciones de ID. Si había configurado anteriormente [!DNL Google] integraciones en Audience Manager, las sincronizaciones de ID que había configurado se transfieren a Platform.

### Lista de permitidos {#allow-listing}

La inclusión en la lista de permitidos es obligatoria antes de configurar la primera [!DNL Google Ad Manager] en Platform. Asegúrese de completar el proceso de inclusión en la lista de permitidos que se describe a continuación antes de crear su destino.

1. Siga los pasos descritos en la sección [Documentación de Google Ad Manager](https://support.google.com/admanager/answer/3289669?hl=en) para agregar Adobe como plataforma de administración de datos (DMP) vinculada.
2. En el [!DNL Google Ad Manager] interfaz, vaya a **[!UICONTROL Administrador]** > **[!UICONTROL Configuración global]** > **[!UICONTROL Configuración de red]** y habilite la opción **[!UICONTROL Acceso a API]** deslizador.

## Conexión al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el **[!UICONTROL Ver destinos]** y **[!UICONTROL Administrar destinos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_gam_appendSegmentID"
>title="Anexar el ID de público al nombre de público"
>abstract="Seleccione esta opción para que el nombre de público en Google Ad Manager incluya el ID de público de Experience Platform, de esta manera: `Audience Name (Audience ID)`"

While [configuración](../../ui/connect-destination.md) Para este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Nombre]**: complete el nombre preferido para este destino.
* **[!UICONTROL Descripción]**: Opcional. Por ejemplo, puede mencionar para qué campaña está usando este destino.
* **[!UICONTROL ID de cuenta]**: introduzca su [!DNL Audience Link ID] de su [!DNL Google] cuenta. Se trata de un identificador específico asociado con su [!DNL Google Ad Manager] red (no su [!DNL Network code]). Puede encontrar esto en **[!UICONTROL Administración > Configuración global]** en el [!DNL Google Ad Manager] interfaz.
* **[!UICONTROL Tipo de cuenta]**: Seleccione una opción, en función de su cuenta con Google:
   * Uso `DFP by Google` para [!DNL DoubleClick] para editores
   * Uso `AdX buyer` para [!DNL Google AdX]
* **[!UICONTROL Anexar ID de audiencia al nombre de audiencia]**: seleccione esta opción para que el nombre de la audiencia en Google Ad Manager incluya el ID de audiencia de Experience Platform, de esta manera: `Audience Name (Audience ID)`.

>[!NOTE]
>
>Al configurar un [!DNL Google Ad Manager] destino, trabaje con su [!DNL Google Account Manager] o un representante del Adobe para comprender qué tipo de cuenta tiene.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la IU](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita el **[!UICONTROL Ver destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Consulte [Activar datos de audiencia en destinos de exportación de audiencia de flujo continuo](../../ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

## Datos exportados {#exported-data}

Para comprobar si los datos se han exportado correctamente a [!DNL Google Ad Manager] destino, compruebe su [!DNL Google Ad Manager] cuenta. Si la activación se ha realizado correctamente, las audiencias se rellenan en la cuenta.

## Resolución de problemas {#troubleshooting}

Si encuentra algún error al utilizar este destino y necesita ponerse en contacto con Adobe o Google, mantenga los siguientes ID a mano.

Estos son los ID de cuenta de Google de Adobe:

* **[!UICONTROL ID de cuenta]**: 87933855
* **[!UICONTROL ID de cliente]**: 89690775