---
keywords: publicidad; la oficina de comercio; oficina de publicidad
title: La conexión con el mostrador de comercio
description: Trade Desk es una plataforma de autoservicio para que los compradores de publicidad ejecuten campañas digitales de redireccionamiento y segmentación de audiencia en distintas fuentes de inventario de dispositivos móviles, vídeo y visualización.
exl-id: b8f638e8-dc45-4aeb-8b4b-b3fa2906816d
source-git-commit: 802b1844bec1e577e978da5d5a69de87278c04b9
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 2%

---

# [!DNL The Trade Desk] connection

## Información general {#overview}

[!DNL The Trade Desk] destination le ayuda a enviar datos de perfil a  [!DNL The Trade Desk].

[!DNL The Trade Desk] es una plataforma de autoservicio para que los compradores de publicidades ejecuten campañas digitales con objetivo de audiencia y redireccionamiento a través de las fuentes de inventario de dispositivos móviles, vídeo y visualización.

Para enviar datos de perfil a [!DNL Trade Desk], primero debe conectarse al destino.

## Casos de uso {#use-cases}

Como especialista en marketing, quiero poder usar segmentos creados a partir de [!DNL Trade Desk IDs] o ID de dispositivo para crear campañas digitales con objetivo de audiencia o retargeting.

## Identidades compatibles {#supported-identities}

[!DNL The Trade Desk] admite la activación de identidades descritas en la tabla siguiente. Obtenga más información sobre [identities](/help/identity-service/namespaces.md).

| Identidad de Target | Descripción |
|---|---|
| GAID | [!DNL Google Advertising ID] |
| IDFA | [!DNL Apple ID for Advertisers] |
| El identificador del servicio de asistencia al cliente | ID del anunciante en la plataforma de asistencia técnica |

## Tipo de exportación {#export-type}

**[!DNL Segment export]** : exporta todos los miembros de un segmento (audiencia) al destino.

## Requisitos previos {#prerequisites}

Si desea crear su primer destino con [!DNL The Trade Desk] y no ha habilitado la [funcionalidad de sincronización de ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) en el servicio de ID de Experience Cloud en el pasado (con Adobe Audience Manager u otras aplicaciones), póngase en contacto con el servicio de consultoría de Adobe o con el servicio de atención al cliente para habilitar las sincronizaciones de ID. Si anteriormente había configurado [!DNL The Trade Desk] integraciones en Audience Manager, las sincronizaciones de ID que había configurado se transfieren a Platform.

## Conectarse al destino {#connect}

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

Mientras [configura](../../ui/connect-destination.md) este destino, debe proporcionar la siguiente información:

* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL ID de cuenta]**: Su  [!DNL Trade Desk] [!UICONTROL ID de cuenta].
* **[!UICONTROL Ubicación]** del servidor: Pregunte a su  [!DNL Trade Desk] representante qué servidor regional debe utilizar. Estos son los servidores regionales disponibles entre los que puede elegir:
   * **[!UICONTROL Europa]**
   * **[!UICONTROL Singapur]**
   * **[!UICONTROL Tokio]**
   * **[!UICONTROL Norteamérica Oriental]**
   * **[!UICONTROL Norteamérica oeste]**
   * **[!UICONTROL América Latina]**

## Activar segmentos en este destino {#activate}

Consulte [Activar perfiles y segmentos en un destino](../../ui/activate-destinations.md) para obtener instrucciones sobre cómo activar segmentos de audiencia en destinos.

En el paso [Programación de segmentos](../../ui/activate-destinations.md#segment-schedule), debe asignar manualmente los segmentos a su ID correspondiente o nombre descriptivo en la plataforma de destino.

Al asignar segmentos, le recomendamos que utilice el nombre del segmento de Platform o una forma más corta de él, para facilitar su uso. Sin embargo, el ID de segmento o el nombre de su destino no necesitan coincidir con el de su cuenta de Platform. El destino reflejará cualquier valor que inserte en el campo de asignación.

Si utiliza varias asignaciones de dispositivo (ID de cookie, [!DNL IDFA], [!DNL GAID]), asegúrese de utilizar el mismo valor de asignación para las tres asignaciones. [!DNL The Trade Desk] agregarán todos ellos en un solo segmento, con un desglose a nivel de dispositivo.

![ID de asignación de segmentos](../../assets/common/segment-mapping-id.png)

## Datos exportados {#exported-data}

Para verificar si los datos se han exportado correctamente al destino [!DNL The Trade Desk] , compruebe su cuenta [!DNL Trade Desk]. Si la activación se ha realizado correctamente, las audiencias se rellenan en la cuenta.
