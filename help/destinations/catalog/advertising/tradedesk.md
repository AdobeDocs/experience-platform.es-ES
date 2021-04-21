---
keywords: publicidad; la oficina de comercio; oficina de publicidad
title: La conexión con el mostrador de comercio
description: Trade Desk es una plataforma de autoservicio para que los compradores de publicidad ejecuten campañas digitales de redireccionamiento y segmentación de audiencia en distintas fuentes de inventario de dispositivos móviles, vídeo y visualización.
exl-id: b8f638e8-dc45-4aeb-8b4b-b3fa2906816d
translation-type: tm+mt
source-git-commit: 5b72433fcf2318f98538278c6d2650b366e391a2
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 1%

---

# [!DNL The Trade Desk] connection

## Información general {#overview}

[!DNL The Trade Desk] destination le ayuda a enviar datos de perfil a  [!DNL The Trade Desk].

[!DNL The Trade Desk] es una plataforma de autoservicio para que los compradores de publicidades ejecuten campañas digitales con objetivo de audiencia y redireccionamiento a través de las fuentes de inventario de dispositivos móviles, vídeo y visualización.

Para enviar datos de perfil a [!DNL Trade Desk], primero debe conectarse al destino.

## Casos de uso {#use-cases}

Como especialista en marketing, quiero poder usar segmentos creados a partir de [!DNL Trade Desk IDs] o ID de dispositivo para crear campañas digitales con objetivo de audiencia o retargeting.

## Identidades admitidas {#supported-identities}

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

## Conectarse al destino {#connect-destination}

En **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, seleccione [!DNL The Trade Desk] y seleccione **[!UICONTROL Configure]**.

![Configuración Del Destino Del Escritorio Comercial](../../assets/catalog/advertising/tradedesk/configure.png)

Si ya existe una conexión con este destino, puede ver un botón **[!UICONTROL Activate]** en la tarjeta de destino. Para obtener más información sobre la diferencia entre **[!UICONTROL Activate]** y **[!UICONTROL Configure]**, consulte la sección [Catalog](../../ui/destinations-workspace.md#catalog) de la documentación del espacio de trabajo de destino.

![Activar El Destino De La Mesa De Comercio](../../assets/catalog/advertising/tradedesk/activate.png)

## Paso de autenticación {#authentication}

En el paso **[!UICONTROL Authentication]**, debe introducir los detalles de conexión [!DNL The Trade Desk]:

* **[!UICONTROL Name]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Description]**: Descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL Account ID]**: Su  [!DNL Trade Desk] [!UICONTROL Account ID].
* **[!UICONTROL Server Location]**: Pregunte a su  [!DNL Trade Desk] representante qué servidor regional debe utilizar. Estos son los servidores regionales disponibles entre los que puede elegir:

   * **[!UICONTROL Europe]**
   * **[!UICONTROL Singapore]**
   * **[!UICONTROL Tokyo]**
   * **[!UICONTROL North America East]**
   * **[!UICONTROL North America West]**
   * **[!UICONTROL Latin America]**

* **[!UICONTROL Marketing action]**: Las acciones de marketing indican la intención para la que se exportarán los datos al destino. Puede seleccionar entre las acciones de marketing definidas por el Adobe o crear su propia acción de marketing. Para obtener más información sobre las acciones de marketing, consulte la página [Control de datos en Adobe Experience Platform](../../../data-governance/policies/overview.md). Para obtener información sobre las acciones de marketing definidas por el Adobe, consulte la [Información general sobre las políticas de uso de datos](../../../data-governance/policies/overview.md).

![La etapa de autenticación de los servicios de asistencia técnica](../../assets/catalog/advertising/tradedesk/authenticate.png)

Haga clic en **[!UICONTROL Create destination]**. Se ha creado el destino. Puede hacer clic en [!UICONTROL Save & Exit] si desea activar segmentos más adelante, o puede seleccionar [!UICONTROL Next] para continuar con el flujo de trabajo y seleccionar segmentos para activarlos. En cualquier caso, consulte la siguiente sección, [Activar segmentos](#activate-segments), para el resto del flujo de trabajo.

## Activar segmentos {#activate-segments}

Consulte [Activar perfiles y segmentos en un destino](../../ui/activate-destinations.md#select-attributes) para obtener información sobre el flujo de trabajo de activación de segmentos.

En el paso [Programación de segmentos](../../ui/activate-destinations.md#segment-schedule), debe asignar manualmente los segmentos a su ID correspondiente o nombre descriptivo en el destino.

Al asignar segmentos, le recomendamos que utilice el nombre del segmento [!DNL Platform] o una forma más corta de él, para facilitar su uso. Sin embargo, el ID de segmento o el nombre de su destino no necesitan coincidir con el de su cuenta [!DNL Platform]. El destino reflejará cualquier valor que inserte en el campo de asignación.

Si utiliza varias asignaciones de dispositivo (ID de cookie, [!DNL IDFA], [!DNL GAID]), asegúrese de utilizar el mismo valor de asignación para las tres asignaciones. [!DNL The Trade Desk] agregarán todos ellos en un solo segmento, con un desglose a nivel de dispositivo.

![ID de asignación de segmentos](../../assets/common/segment-mapping-id.png)

## Datos exportados {#exported-data}

Para verificar si los datos se han exportado correctamente al destino [!DNL The Trade Desk] , compruebe su cuenta [!DNL Trade Desk]. Si la activación se ha realizado correctamente, las audiencias se rellenan en la cuenta.
