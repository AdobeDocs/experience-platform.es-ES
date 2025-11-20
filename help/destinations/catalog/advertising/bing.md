---
keywords: publicidad; Bing;
title: Conexión de Microsoft Bing
description: Con el destino de conexión de Microsoft Bing, puede ejecutar campañas digitales de retargeting y segmentación de audiencia en toda la red de Advertising de Microsoft, incluida la publicidad de visualización, la búsqueda y la segmentación nativa.
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '851'
ht-degree: 5%

---

# [!DNL Microsoft Bing] conexión {#bing-destination}

## Información general {#overview}


>[!IMPORTANT]
>
>Tras una actualización interna del servicio de destinos a partir de agosto de 2025, es posible que experiencia una **caída en el número de perfiles** activados en los flujos de datos a [!DNL Microsoft Bing].
>
> Esta caída se debe a la introducción del **requisito** de asignación de ECID para todas las activaciones en esta plataforma de destino. Consulte la sección de [asignación](#mandatory-mappings) obligatoria de este Página para obtener información detallada.
>
>**Qué ha cambiado:**
>
>* La asignación de ECID (ID Experience Cloud) es ahora **obligatoria** para todas las activaciones perfil.
>* Los perfiles sin asignación ECID se **eliminarán** de los flujos de datos activación existentes.
>
>**Lo que debe hacer:**
>
>* Revise los datos de su audiencia para confirmar que los perfiles tienen valores ECID válidos.
>* Supervise las métricas de activación para verificar los recuentos de perfil esperados.

Use el destino [!DNL Microsoft Bing] para enviar datos de perfil a [!DNL Microsoft Advertising Network] completo, incluidos [!DNL Display Advertising], [!DNL Search] y [!DNL Native].

El destino [!DNL Microsoft Bing] crea *[!DNL Custom Audiences]* en Microsoft. Están disponibles tanto en [!DNL Microsoft Search Network] como en [!DNL Audience Network] ([!DNL Native] /[!DNL Display] /[!DNL Programmatic]) tal como se indica en la [documentación de Microsoft Advertising](https://help.ads.microsoft.com/#apex/ads/en/56892/1-500).

Para enviar datos de perfil a [!DNL Microsoft Bing], primero debe conectarse al destino.

## Casos de uso {#use-cases}

Como experto en marketing, quiero poder utilizar audiencias creadas a partir de destino a los usuarios a través de [!DNL Microsoft Advertising IDs] publicidad gráfica o búsqueda en todos [!DNL Microsoft Advertising] los canales.

## Identidades admitidas {#supported-identities}

[!DNL Microsoft Bing] Admite el activación de audiencias en función de las identidades que se muestran en la tabla siguiente. Obtenga más información sobre [las identidades](/help/identity-service/features/namespaces.md).

| Identidad | Descripción |
|---|---|
| CRIADA | Microsoft Advertising ID |
| ECID | Experience Cloud ID. Esta identidad es obligatoria para que la integración funcione correctamente, pero no se utiliza para audiencia activación. |

{style="table-layout:auto"}

## Audiencias admitidas {#supported-audiences}

En esta sección se describen los tipos de audiencias que se pueden exportar a este destino.

| origen de audiencia | Admitido | Descripción |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiences generan a través del servicio[&#x200B; de segmentación Experience Platform](../../../segmentation/home.md). |
| Cargas personalizadas | ✓ | [Audiences importados](../../../segmentation/ui/audience-portal.md#import-audience) a Experience Platform desde CSV archivos. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

**[!DNL Audience Export]**: está exportando todos los miembros de una audiencia al destino [!DNL Microsoft Bing].

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
|---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Audience export]** | Está exportando todos los miembros de una audiencia al [!DNL Microsoft Bing] destino. |
| Frecuencia de exportación | **[!UICONTROL Streaming]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform basado en la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Requisitos previos {#prerequisites}

>[!IMPORTANT]
>
>Si desea crear su primer destino y [!DNL Microsoft Bing] no ha habilitado el [funcionalidad de sincronizar de ID en Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) servicio de ID en el pasado (con Adobe Audience Manager u otras aplicaciones), póngase en contacto con Adobe Systems asesor o con el Servicio de atención al cliente para habilitar las sincronizaciones de ID. Si anteriormente había configurado [!DNL Microsoft Bing] integraciones en Audience Manager, las sincronizaciones de ID que había configurado se transfieren a Experience Platform.

Al configurar el destino, debe proporcionar la siguiente información:

* [!UICONTROL Account ID]: este es su [!DNL Bing Ads CID], en entero formato.

## Conectar con el destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita los **[!UICONTROL View Destinations]** y **[!UICONTROL Manage Destinations]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md).

### Rellenar detalles de destino {#parameters}

Mientras [configura](../../ui/connect-destination.md) este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Name]**: un nombre con el cual reconocerá este destino en el futuro.
* **[!UICONTROL Description]**: una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL Account ID]**: Su [!DNL Bing Ads Customer ID] (CID). Su CID es un número entero que se encuentra en la URL al iniciar sesión en [!DNL Microsoft Advertising].

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos hacia su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Next]**.

## Activar públicos en este destino {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_bing_mapping_id"
>title="ID de asignación"
>abstract="Introduzca el ID de público numérico de Bing al que desea asignar el segmento seleccionado. Si lo proporcionado [!UICONTROL Mapping ID] no corresponde a un identificador de audiencia en el destino de Bing, no verá los datos de audiencia esperados en su cuenta de Bing."

>[!IMPORTANT]
> 
>Para activar los datos, necesita los **[!UICONTROL View Destinations]** permisos **[!UICONTROL Activate Destinations]** , **[!UICONTROL View Profiles]**, **[!UICONTROL View Segments]**, y [&#x200B; &#x200B;](/help/access-control/home.md#permissions)control de acceso. Lea la control de acceso descripción general[&#x200B; o póngase en contacto con el &#x200B;](/help/access-control/ui/overview.md)administrador del producto para obtener los permisos necesarios.

Consulte [Activar datos de audiencia en destinos](../../ui/activate-segment-streaming-destinations.md) de flujo continuo audiencia exportación para obtener instrucciones sobre cómo activar audiencias en este destino.

En el paso de programación[&#x200B; de &#x200B;](../../ui/activate-segment-streaming-destinations.md#scheduling)audiencia, debe asignar manualmente el nombre del audiencia en el [!UICONTROL Mapping ID] campo. Esto garantiza que audiencia metadatos se transmita correctamente a [!DNL Bing].

![IU imagen que muestra la pantalla de programación de audiencia con un ejemplo de cómo asignar el nombre de audiencia al ID de Asignación de Bing.](../../assets/catalog/advertising/bing/mapping-id.png)

### Asignaciones obligatorias {#mandatory-mappings}

Todas las identidades de destino descritas en la sección [identidades admitidas](#supported-identities) son obligatorias y deben asignarse durante el proceso de activación de audiencia. Esto incluye lo siguiente:

* **EMPLEADA DOMÉSTICA** (Microsoft Advertising ID)
* **ECID** (Experience Cloud ID)

Si no se asignan todas las identidades necesarias, no se puede completar el flujo de trabajo de activación. Cada identidad cumple un propósito específico en la integración y todas son necesarias para que el destino funcione correctamente.

## Datos exportados {#exported-data}

Para verificar si los datos se han exportado correctamente al destino, compruebe su [!DNL Microsoft Bing] [!DNL Microsoft Bing Ads] cuenta. Si activación ha tenido éxito, las audiencias se rellenan en su cuenta.
