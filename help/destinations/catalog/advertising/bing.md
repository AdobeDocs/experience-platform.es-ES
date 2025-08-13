---
keywords: publicidad; bing;
title: Conexión de Microsoft Bing
description: Con el destino de conexión de Microsoft Bing, puede ejecutar campañas digitales de retargeting y segmentación de audiencia en toda la red de Advertising de Microsoft, incluida la publicidad de visualización, la búsqueda y la segmentación nativa.
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: 34520b42554a4ff72b05e9254bd923173629d611
workflow-type: tm+mt
source-wordcount: '877'
ht-degree: 8%

---

# [!DNL Microsoft Bing] conexión {#bing-destination}

## Información general {#overview}


>[!IMPORTANT]
>
>Después de una actualización interna al servicio de destinos a partir de agosto de 2025, es posible que experimente una **caída en el número de perfiles activados** en sus flujos de datos a [!DNL Microsoft Bing].
>
> Esta caída se debe a la introducción del **requisito de asignación ECID** para todas las activaciones en esta plataforma de destino. Consulte la sección [asignación obligatoria](#mandatory-mappings) en esta página para obtener información detallada.
>
>**Qué cambió:**
>
>* La asignación ECID (Experience Cloud ID) ahora es **obligatoria** para todas las activaciones de perfil.
>* Los perfiles sin asignación ECID se **eliminarán** de los flujos de datos de activación existentes.
>
>**Lo que debe hacer:**
>
>* Revise los datos de audiencia para confirmar que los perfiles tienen valores ECID válidos.
>* Monitorice las métricas de activación para verificar los recuentos de perfiles esperados.

Use el destino [!DNL Microsoft Bing] para enviar datos de perfil a [!DNL Microsoft Advertising Network] completo, incluidos [!DNL Display Advertising], [!DNL Search] y [!DNL Native].

El destino [!DNL Microsoft Bing] crea *[!DNL Custom Audiences]* en Microsoft. Están disponibles tanto en [!DNL Microsoft Search Network] como en [!DNL Audience Network] ([!DNL Native] /[!DNL Display] /[!DNL Programmatic]) tal como se indica en la [documentación de Microsoft Advertising](https://help.ads.microsoft.com/#apex/ads/en/56892/1-500).

Para enviar datos de perfil a [!DNL Microsoft Bing], primero debe conectarse al destino.

## Casos de uso {#use-cases}

Como especialista en marketing, quiero poder usar audiencias creadas a partir de [!DNL Microsoft Advertising IDs] para segmentar usuarios mediante anuncios de visualización o búsqueda en [!DNL Microsoft Advertising] canales.

## Identidades admitidas {#supported-identities}

[!DNL Microsoft Bing] admite la activación de audiencias en función de las identidades mostradas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidad | Descripción |
|---|---|
| CRIADA | MICROSOFT ADVERTISING ID |
| ECID | ID de Experience Cloud. Esta identidad es obligatoria para que la integración funcione correctamente, pero no se utiliza para la activación de audiencias. |

{style="table-layout:auto"}

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipos de audiencias puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiencias generadas a través del [servicio de segmentación](../../../segmentation/home.md) de Experience Platform. |
| Cargas personalizadas | ✓ | Las audiencias [importadas](../../../segmentation/ui/audience-portal.md#import-audience) en Experience Platform desde archivos CSV. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

**[!DNL Audience Export]**: está exportando todos los miembros de una audiencia al destino [!DNL Microsoft Bing].

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de audiencia]** | Está exportando todos los miembros de una audiencia al destino [!DNL Microsoft Bing]. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform basado en la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Requisitos previos {#prerequisites}

>[!IMPORTANT]
>
>Si desea crear su primer destino con [!DNL Microsoft Bing] y no ha habilitado la [funcionalidad de sincronización de ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) en el servicio de Experience Cloud ID en el pasado (con Adobe Audience Manager u otras aplicaciones), póngase en contacto con Adobe Consulting o con el Servicio de atención al cliente para habilitar las sincronizaciones de ID. Si ya había configurado [!DNL Microsoft Bing] integraciones en Audience Manager, las sincronizaciones de ID que configuró se transfieren a Experience Platform.

Al configurar el destino, debe proporcionar la siguiente información:

* [!UICONTROL ID de cuenta]: este es su [!DNL Bing Ads CID], en formato entero.

## Conectar con el destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita los **[!UICONTROL permisos de control de acceso]** de Ver destinos **[!UICONTROL y]** Administrar destinos[&#128279;](/help/access-control/home.md#permissions)5&rbrace;. Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md).

### Rellenar detalles de destino {#parameters}

Mientras [configura](../../ui/connect-destination.md) este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL ID de cuenta]**: su [!DNL Bing Ads Customer ID] (CID). Su CID es un número entero que se encuentra en la dirección URL cuando inicia sesión en [!DNL Microsoft Advertising].

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando termine de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar públicos en este destino {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_bing_mapping_id"
>title="ID de asignación"
>abstract="Introduzca el ID de público numérico de Bing al que desea asignar el segmento seleccionado. Si el [!UICONTROL ID de asignación] proporcionado no corresponde a un ID de público en el destino de Bing, no verá los datos de público esperados en su cuenta de Bing."

>[!IMPORTANT]
> 
>Para activar los datos, necesita los **[!UICONTROL permisos de control de acceso]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]**&#x200B;[para ](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Consulte [Activar datos de audiencia en destinos de exportación de audiencia de streaming](../../ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

En el paso [Programación de audiencias](../../ui/activate-segment-streaming-destinations.md#scheduling), debe asignar manualmente el nombre de la audiencia en el campo [!UICONTROL Id. de asignación]. Esto garantiza que los metadatos de la audiencia se pasen correctamente a [!DNL Bing].

![Imagen de la interfaz de usuario que muestra la pantalla de programación de audiencias con un ejemplo de cómo asignar el nombre de audiencia al identificador de asignación de Bing.](../../assets/catalog/advertising/bing/mapping-id.png)

### Asignaciones obligatorias {#mandatory-mappings}

Todas las identidades de destino descritas en la sección [identidades admitidas](#supported-identities) son obligatorias y deben asignarse durante el proceso de activación de audiencia. Esto incluye lo siguiente:

* **EMPLEADA DOMÉSTICA** (Microsoft Advertising ID)
* **ECID** (Experience Cloud ID)

Si no se asignan todas las identidades necesarias, no se puede completar el flujo de trabajo de activación. Cada identidad cumple un propósito específico en la integración y todas son necesarias para que el destino funcione correctamente.

## Datos exportados {#exported-data}

Para comprobar si los datos se han exportado correctamente al destino [!DNL Microsoft Bing], compruebe su cuenta de [!DNL Microsoft Bing Ads]. Si la activación se ha realizado correctamente, las audiencias se rellenan en la cuenta.
