---
keywords: 'publicidad; bing; '
title: Conexión de Microsoft Bing
description: Con el destino de la conexión de Microsoft Bing, puede ejecutar campañas digitales con objetivo de audiencia y redireccionamiento en toda la publicidad de presentación de Microsoft.
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: 15ea3ab9370541c35b874414a8753e8812eea9c6
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 1%

---

# [!DNL Microsoft Bing] connection {#bing-destination}

## Información general {#overview}

El destino [!DNL Microsoft Bing] le ayuda a enviar datos de perfil a [!DNL Microsoft Display Advertising].

Para enviar datos de perfil a [!DNL Microsoft Bing], primero debe conectarse al destino.

## Casos de uso {#use-cases}

Como especialista en marketing, quiero poder usar segmentos creados a partir de [!DNL Microsoft Advertising IDs] para dirigirme a los usuarios a través de la publicidad de display en los canales [!DNL Microsoft Advertising].

## Identidades compatibles {#supported-identities}

[!DNL Microsoft Bing] admite la activación de identidades descritas en la tabla siguiente. Obtenga más información sobre [identities](/help/identity-service/namespaces.md).

| Identidad de Target | Descripción |
|---|---|
| MAID | Microsoft Advertising ID |

## Tipo de exportación {#export-type}

**[!DNL Segment Export]** : exporta todos los miembros de un segmento (audiencia) al  [!DNL Microsoft Bing] destino.

## Requisitos previos {#prerequisites}

Si desea crear su primer destino con [!DNL Microsoft Bing] y no ha habilitado la [funcionalidad de sincronización de ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) en el servicio de ID de Experience Cloud en el pasado (con Adobe Audience Manager u otras aplicaciones), póngase en contacto con el servicio de consultoría de Adobe o con el servicio de atención al cliente para habilitar las sincronizaciones de ID. Si anteriormente había configurado [!DNL Microsoft Bing] integraciones en Audience Manager, las sincronizaciones de ID que había configurado se transfieren a Platform.

Al configurar el destino, debe proporcionar la siguiente información:

* [!UICONTROL ID de cuenta]: este es su  [!DNL Bing Ads CID], en formato entero.

## Conectarse al destino {#connect}

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

Mientras [configura](../../ui/connect-destination.md) este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL ID de cuenta]**: Su  [!DNL Bing Ads CID].

## Activar segmentos en este destino {#activate}

Consulte [Activar perfiles y segmentos en un destino](../../ui/activate-destinations.md) para obtener instrucciones sobre cómo activar segmentos de audiencia en destinos.

En el paso [Programación de segmentos](../../ui/activate-destinations.md#segment-schedule), debe asignar manualmente los segmentos a su ID correspondiente o nombre descriptivo en el destino.

Al asignar segmentos, le recomendamos que utilice el nombre del segmento [!DNL Platform] o una forma más corta de él, para facilitar su uso. Sin embargo, el ID de segmento o el nombre de su destino no necesitan coincidir con el de su cuenta [!DNL Platform]. El destino reflejará cualquier valor que inserte en el campo de asignación.

## Datos exportados {#exported-data}

Para verificar si los datos se han exportado correctamente al destino [!DNL Microsoft Bing] , compruebe su cuenta [!DNL Microsoft Bing Ads]. Si la activación se ha realizado correctamente, las audiencias se rellenan en la cuenta.
