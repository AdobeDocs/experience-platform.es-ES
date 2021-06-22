---
keywords: 'publicidad; bing; '
title: Conexión de Microsoft Bing
description: Con el destino de la conexión de Microsoft Bing, puede ejecutar campañas digitales con objetivo de audiencia y redireccionamiento en toda la publicidad de presentación de Microsoft.
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: 2931efa6f67a042255fb1d31c0683f73d817b55b
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 0%

---

# [!DNL Microsoft Bing] connection  {#bing-destination}

## Información general {#overview}

El destino [!DNL Microsoft Bing] le ayuda a enviar datos de perfil a [!DNL Microsoft Display Advertising].

Para enviar datos de perfil a [!DNL Microsoft Bing], primero debe conectarse al destino.

## Casos de uso {#use-cases}

Como especialista en marketing, quiero poder usar segmentos creados a partir de [!DNL Microsoft Advertising IDs] para dirigirme a los usuarios a través de la publicidad de display en los canales [!DNL Microsoft Advertising].

## Identidades admitidas {#supported-identities}

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

## Conectarse al destino {#connect-destination}

En **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, seleccione [!DNL Microsoft Bing] y seleccione **[!UICONTROL Configure]**.

![Configuración del destino de Microsoft Bing](../../assets/catalog/advertising/bing/configure.png)

Si ya existe una conexión con este destino, puede ver un botón **[!UICONTROL Activate]** en la tarjeta de destino. Para obtener más información sobre la diferencia entre **[!UICONTROL Activate]** y **[!UICONTROL Configure]**, consulte la sección [Catalog](../../ui/destinations-workspace.md#catalog) de la documentación del espacio de trabajo de destino.

![Activar destino de Microsoft Bing](../../assets/catalog/advertising/bing/activate.png)

## Paso de autenticación {#authentication}

En el paso **[!UICONTROL Authentication]** debe introducir los detalles de conexión de destino:

* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL ID de cuenta]**: Su  [!DNL Bing Ads CID].
* **[!UICONTROL Acción de marketing]**: Las acciones de marketing indican la intención para la que se exportarán los datos al destino. Puede seleccionar entre las acciones de marketing definidas por el Adobe o crear su propia acción de marketing. Para obtener más información sobre las acciones de marketing, consulte la página [Control de datos en Adobe Experience Platform](../../../data-governance/policies/overview.md). Para obtener información sobre las acciones de marketing definidas por el Adobe, consulte la [Información general sobre las políticas de uso de datos](../../../data-governance/policies/overview.md).

![Autenticación de destino de Microsoft Bing](../../assets/catalog/advertising/bing/authentication.png)

Haga clic en **[!UICONTROL Crear destino]**. Se ha creado el destino. Puede hacer clic en [!UICONTROL Guardar y salir] si desea activar los segmentos más adelante, o puede hacer clic en [!UICONTROL Siguiente] para continuar con el flujo de trabajo y seleccionar los segmentos que desea activar. En cualquier caso, consulte la siguiente sección, [Activar segmentos](#activate-segments), para el resto del flujo de trabajo.

## Activar segmentos {#activate-segments}

Consulte [Activar perfiles y segmentos en un destino](../../ui/activate-destinations.md#select-attributes) para obtener información sobre el flujo de trabajo de activación de segmentos.

En el paso [Programación de segmentos](../../ui/activate-destinations.md#segment-schedule), debe asignar manualmente los segmentos a su ID correspondiente o nombre descriptivo en el destino.

Al asignar segmentos, le recomendamos que utilice el nombre del segmento [!DNL Platform] o una forma más corta de él, para facilitar su uso. Sin embargo, el ID de segmento o el nombre de su destino no necesitan coincidir con el de su cuenta [!DNL Platform]. El destino reflejará cualquier valor que inserte en el campo de asignación.

![ID de asignación de segmentos](../../assets/common/segment-mapping-id.png)

## Datos exportados {#exported-data}

Para verificar si los datos se han exportado correctamente al destino [!DNL Microsoft Bing] , compruebe su cuenta [!DNL Microsoft Bing Ads]. Si la activación se ha realizado correctamente, las audiencias se rellenan en la cuenta.
