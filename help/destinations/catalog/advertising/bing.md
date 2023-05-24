---
keywords: publicidad; bing;
title: Conexión de Microsoft Bing
description: Con el destino de conexión de Microsoft Bing, puede ejecutar campañas digitales de retargeting y segmentación de audiencia en toda la publicidad en pantalla de Microsoft.
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: aec9708680c2a4cb3c70af12f95c67ec37b2e129
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 8%

---

# [!DNL Microsoft Bing] conexión {#bing-destination}

## Información general {#overview}

El [!DNL Microsoft Bing] El destino le ayuda a enviar datos de perfil a [!DNL Microsoft Display Advertising].

Para enviar datos de perfil a [!DNL Microsoft Bing], primero debe conectarse al destino.

## Casos de uso {#use-cases}

Como experto en marketing, quiero poder utilizar segmentos creados a partir de [!DNL Microsoft Advertising IDs] para dirigirse a los usuarios mediante la publicidad de display en [!DNL Microsoft Advertising] canales.

## Identidades admitidas {#supported-identities}

[!DNL Microsoft Bing] admite la activación de identidades descritas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/namespaces.md).

| Identidad de destino | Descripción |
|---|---|
| CRIADA | ID de publicidad de Microsoft |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

**[!DNL Segment Export]** - está exportando todos los miembros de un segmento (audiencia) a [!DNL Microsoft Bing] destino.

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de segmentos]** | Va a exportar todos los miembros de un segmento (audiencia) a [!DNL Microsoft Bing] destino. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform según la evaluación de segmentos, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Requisitos previos {#prerequisites}

>[!IMPORTANT]
>
>Si quiere crear su primer destino con [!DNL Microsoft Bing] y no han habilitado el [Funcionalidad de sincronización de ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) en el Servicio de ID de Experience Cloud en el pasado (con Adobe Audience Manager u otras aplicaciones), póngase en contacto con el Servicio de consultoría de Adobe o con el Servicio de atención al cliente para habilitar las sincronizaciones de ID. Si había configurado anteriormente [!DNL Microsoft Bing] integraciones en Audience Manager, las sincronizaciones de ID que había configurado se transfieren a Platform.

Al configurar el destino, debe proporcionar la siguiente información:

* [!UICONTROL ID de cuenta]: este es su [!DNL Bing Ads CID], en formato entero.

## Conectar con el destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

While [configuración](../../ui/connect-destination.md) Para este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Nombre]**: Un nombre con el que reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL ID de cuenta]**: su [!DNL Bing Ads Customer ID] (CID). El CID es un número entero que se encuentra en la dirección URL cuando inicia sesión en [!DNL Microsoft Advertising].

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la IU](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar segmentos en este destino {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_bing_mapping_id"
>title="ID de asignación"
>abstract="Introduzca el ID de segmento numérico de Bing al que desea asignar el segmento seleccionado. Si el [!UICONTROL ID de asignación] proporcionado no corresponde a un ID de segmento en el destino de Bing, no verá los datos de audiencia esperados en su cuenta de Bing."

>[!IMPORTANT]
> 
>Para activar los datos, necesita el **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Consulte [Activar datos de audiencia en destinos de exportación de segmentos de flujo continuo](../../ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar segmentos de audiencia en este destino.

En el [Programación de segmentos](../../ui/activate-segment-streaming-destinations.md#scheduling) paso, debe asignar manualmente el nombre del segmento en la [!UICONTROL ID de asignación] field. Esto garantiza que los metadatos del segmento se pasen correctamente a [!DNL Bing].

![Imagen de la interfaz de usuario que muestra la pantalla de programación de segmentos con un ejemplo de cómo asignar el nombre del segmento al ID de asignación de Bing.](../../assets/catalog/advertising/bing/mapping-id.png)

## Datos exportados {#exported-data}

Para comprobar si los datos se han exportado correctamente a [!DNL Microsoft Bing] destino, compruebe su [!DNL Microsoft Bing Ads] cuenta. Si la activación se ha realizado correctamente, las audiencias se rellenan en la cuenta.
