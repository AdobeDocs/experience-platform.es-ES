---
keywords: 'publicidad; bing; '
title: Conexión de Microsoft Bing
description: Con el destino de la conexión de Microsoft Bing, puede ejecutar campañas digitales de redireccionamiento y segmentación de audiencia en toda la publicidad de presentación de Microsoft.
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: 0006c498cd33d9deb66f1d052b4771ec7504457d
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 3%

---

# [!DNL Microsoft Bing] connection {#bing-destination}

## Información general {#overview}

La variable [!DNL Microsoft Bing] destination le ayuda a enviar datos de perfil a [!DNL Microsoft Display Advertising].

Para enviar datos de perfil a [!DNL Microsoft Bing], primero debe conectarse al destino.

## Casos de uso {#use-cases}

Como especialista en marketing, quiero poder usar segmentos creados a partir de [!DNL Microsoft Advertising IDs] para dirigirse a los usuarios mediante la publicidad de display en [!DNL Microsoft Advertising] canales.

## Identidades compatibles {#supported-identities}

[!DNL Microsoft Bing] admite la activación de identidades descritas en la tabla siguiente. Más información sobre [identidades](/help/identity-service/namespaces.md).

| Identidad de Target | Descripción |
|---|---|
| MAID | Microsoft Advertising ID |

{style=&quot;table-layout:auto&quot;}

## Tipo de exportación y frecuencia {#export-type-frequency}

**[!DNL Segment Export]** - está exportando todos los miembros de un segmento (audiencia) a la [!DNL Microsoft Bing] destino.

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de segmentos]** | Está exportando todos los miembros de un segmento (audiencia) al [!DNL Microsoft Bing] destino. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de flujo continuo son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como un perfil se actualiza en el Experience Platform en función de la evaluación de segmentos, el conector envía la actualización descendente a la plataforma de destino. Más información sobre [destinos de flujo continuo](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Requisitos previos {#prerequisites}

>[!IMPORTANT]
>
>Si desea crear su primer destino con [!DNL Microsoft Bing] y no han habilitado [Funcionalidad de sincronización de ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) en el servicio de ID de Experience Cloud en el pasado (con Adobe Audience Manager u otras aplicaciones), póngase en contacto con el servicio de consultoría de Adobe o el servicio de atención al cliente para habilitar las sincronizaciones de ID. Si ha configurado anteriormente [!DNL Microsoft Bing] integraciones en Audience Manager, las sincronizaciones de ID que ha configurado se transfieren a Platform.

Al configurar el destino, debe proporcionar la siguiente información:

* [!UICONTROL ID de cuenta]: este es su [!DNL Bing Ads CID], en formato entero.

## Conectarse al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita la variable **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

While [configuración](../../ui/connect-destination.md) Para este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL ID de cuenta]**: Su [!DNL Bing Ads CID].

## Activar segmentos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita la variable **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Consulte [Activar datos de audiencia en destinos de exportación de segmentos de flujo continuo](../../ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre la activación de segmentos de audiencia en este destino.

En el [Programación de segmentos](../../ui/activate-segment-streaming-destinations.md#scheduling) , debe asignar manualmente los segmentos a su ID correspondiente o a su nombre descriptivo en el destino.

Al asignar segmentos, le recomendamos que utilice el [!DNL Platform] nombre del segmento o una forma más corta de él, para facilitar su uso. Sin embargo, el ID de segmento o el nombre de su destino no necesitan coincidir con el de su [!DNL Platform] cuenta. El destino reflejará cualquier valor que inserte en el campo de asignación.

## Datos exportados {#exported-data}

Para verificar si los datos se han exportado correctamente a la variable [!DNL Microsoft Bing] destino, compruebe su [!DNL Microsoft Bing Ads] cuenta. Si la activación se ha realizado correctamente, las audiencias se rellenan en la cuenta.
