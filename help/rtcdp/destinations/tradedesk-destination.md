---
keywords: advertising; the trade desk;
title: Destino de la mesa de operaciones
seo-title: Destino de la mesa de operaciones
description: Trade Desk es una plataforma de autoservicio para que los compradores de publicidad ejecuten campañas digitales de objetivo de redireccionamiento y audiencia en distintas fuentes de inventario de dispositivos móviles, de vídeo y de visualización.
seo-description: Trade Desk es una plataforma de autoservicio para que los compradores de publicidad ejecuten campañas digitales de objetivo de redireccionamiento y audiencia en distintas fuentes de inventario de dispositivos móviles, de vídeo y de visualización.
translation-type: tm+mt
source-git-commit: 4eed145c4ca1a4c1d5c58ba0d0b30cead2dd9af9
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 1%

---


# [!DNL The Trade Desk] destino

## Información general {#overview}

[!DNL The Trade Desk] destination le ayuda a enviar datos de perfil a [!DNL The Trade Desk].

[!DNL The Trade Desk] es una plataforma de autoservicio para que los compradores de publicidad ejecuten campañas digitales de objetivo de redireccionamiento y audiencia en distintas fuentes de inventario móviles, de vídeo y de visualización.

Para enviar datos de perfil a [!DNL The Trade Desk], primero debe conectarse al destino.

## Especificaciones de destino {#destination-specs}

Tenga en cuenta los siguientes detalles específicos del [!DNL The Trade Desk] destino:

* Puede enviar las siguientes [identidades](../../identity-service/namespaces.md) a [!DNL The Trade Desk] destinos: [!DNL The Trade Desk ID], [!DNL IDFA], [!DNL GAID].

## Casos de uso {#use-cases}

Como especialista en marketing, quiero poder usar segmentos creados a partir de [!DNL Trade Desk IDs] o ID de dispositivo para crear campañas digitales con objetivo de redireccionamiento o audiencia.

## Tipo de exportación {#export-type}

**[!DNL Segment export]** - está exportando todos los miembros de un segmento (audiencia) al destino.

## Conectar al destino {#connect-destination}

1. En **[!UICONTROL Conexiones]** > **[!UICONTROL Destinos]**, seleccione [!DNL The Trade Desk]y seleccione **[!UICONTROL Configurar]**.

   ![Configurar El Destino De Escritorio Comercial](assets/tradedesk-destination-configure.png)

   >[!NOTE]
   >
   >Si ya existe una conexión con este destino, puede ver un botón **[!UICONTROL Activar]** en la tarjeta de destino. Para obtener más información sobre la diferencia entre **[!UICONTROL Activar]** y **[!UICONTROL Configurar]**, consulte la sección [Catálogo](../destinations/destinations-workspace.md#catalog) de la documentación del espacio de trabajo de destino.
   >
   >![Activar El Destino Del Escritorio Comercial](assets/tradedesk-destination-activate.png)

1. En el paso [!UICONTROL Autenticación] , debe introducir los detalles [!DNL The Trade Desk] de conexión:

   * **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
   * **[!UICONTROL Descripción]**: Descripción que le ayudará a identificar este destino en el futuro.
   * **[!UICONTROL ID]** de cuenta: Su ID [!DNL Trade Desk] de [!UICONTROL cuenta].
   * **[!UICONTROL Secreto]** del cliente: El `clientSecret` parámetro utilizado en las credenciales del [!DNL OAuth2] cliente.
   * **[!UICONTROL Ubicación]** del servidor: Pregunte a su [!DNL The Trade Desk] representante qué servidor regional debe utilizar. Estos son los servidores regionales disponibles que puede elegir:

      * **[!UICONTROL Europa]**
      * **[!UICONTROL Singapur]**
      * **[!UICONTROL Tokio]**
      * **[!UICONTROL Norteamérica Oriental]**
      * **[!UICONTROL Norteamérica Occidental]**
      * **[!UICONTROL América Latina]**
   * **[!UICONTROL Caso]** de uso de marketing: Los casos de uso de mercadotecnia indican la intención para la cual se exportarán los datos al destino. Puede seleccionar entre los casos de uso de mercadotecnia definidos por el Adobe o puede crear su propio caso de uso de mercadotecnia. Para obtener más información sobre los casos de uso de mercadotecnia, consulte la página Gobierno [de datos en Adobe Experience Platform](../privacy/data-governance-overview.md#destinations) . Para obtener información sobre los casos individuales de uso de mercadotecnia definidos por el Adobe, consulte la descripción general [de las políticas de uso de](../../data-governance/policies/overview.md#core-actions)datos.

   ![Paso de autenticación de asistencia técnica](assets/tradedesk-destination-authentication.png)

1. Haga clic en **[!UICONTROL Crear destino]**. Se ha creado el destino. Puede hacer clic en [!UICONTROL Guardar y salir] si desea activar segmentos más adelante, o bien puede seleccionar [!UICONTROL Siguiente] para continuar el flujo de trabajo y seleccionar los segmentos que desea activar. En cualquier caso, consulte la siguiente sección, [Activar segmentos](#activate-segments), para el resto del flujo de trabajo.

## Activar segmentos {#activate-segments}

Consulte [Activar perfiles y segmentos en un destino](activate-destinations.md#select-attributes) para obtener información sobre el flujo de trabajo de activación de segmentos.

Durante el paso de programación [de](activate-destinations.md#segment-schedule) segmentos, debe asignar manualmente los segmentos a su ID correspondiente o a su nombre descriptivo en el destino.

Al asignar segmentos, le recomendamos que utilice el nombre del [!DNL Platform] segmento o una forma más corta de éste, para facilitar su uso. Sin embargo, el ID o nombre del segmento en el destino no necesita coincidir con el de su [!DNL Platform] cuenta. Cualquier valor que inserte en el campo de asignación se verá reflejado por el destino.

Si está utilizando asignaciones de varios dispositivos (ID de cookies, [!DNL IDFA], [!DNL GAID]), asegúrese de utilizar el mismo valor de asignación para las tres asignaciones. [!DNL The Trade Desk] todos ellos se acumulados en un solo segmento, con un desglose a nivel de dispositivo.

![ID de asignación de segmentos](assets/segment-mapping-id.png)


## Datos exportados {#exported-data}

Para verificar si los datos se han exportado correctamente al [!DNL The Trade Desk] destino, compruebe su [!DNL The Trade Desk] cuenta. Si la activación se ha realizado correctamente, las audiencias se rellenan en su cuenta.
