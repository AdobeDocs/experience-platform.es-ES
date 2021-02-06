---
keywords: 'publicidad; bing; '
title: Destino de la conexión de Microsoft Bing
description: Con el destino de conexión de Microsoft Bing, puede ejecutar campañas digitales de objetivo de redireccionamiento y audiencia en toda la publicidad de presentación de Microsoft.
translation-type: tm+mt
source-git-commit: 6655714d4b57d9c414cd40529bcee48c7bcd862d
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 0%

---


# [!DNL Microsoft Bing] connection

El destino [!DNL Microsoft Bing] le ayuda a enviar datos de perfil a [!DNL Microsoft Display Advertising].

Para enviar datos de perfil a [!DNL Microsoft Bing], primero debe conectarse al destino.

## Especificaciones de destino {#destination-specs}

Tenga en cuenta los siguientes detalles específicos del destino [!DNL Microsoft Bing]:

* Puede enviar las [identidades](../../../identity-service/namespaces.md) siguientes a [!DNL Microsoft Bing] destinos: [!DNL Microsoft ID].

## Casos de uso {#use-cases}

Como especialista en mercadotecnia, quiero poder usar segmentos creados a partir de [!DNL Microsoft Advertising IDs] para destinatario de usuarios a través de la publicidad en pantalla en canales [!DNL Microsoft Advertising].

## Tipo de exportación {#export-type}

**[!DNL Segment Export]** - está exportando todos los miembros de un segmento (audiencia) al  [!DNL Microsoft Bing] destino.

## Requisitos previos {#prerequisites}

Al configurar el destino, se le pedirá que proporcione la siguiente información:

* [!UICONTROL ID] de cuenta: este es su  [!DNL Bing Ads CID]formato entero.

## Conectar al destino {#connect-destination}

En **[!UICONTROL Conexiones]** > **[!UICONTROL Destinos]**, seleccione [!DNL Microsoft Bing] y seleccione **[!UICONTROL Configurar]**.

![Configurar destino de Microsoft Bing](../../assets/catalog/advertising/bing/configure.png)

>[!NOTE]
>
>Si ya existe una conexión con este destino, puede ver un botón **[!UICONTROL Activar]** en la tarjeta de destino. Para obtener más información sobre la diferencia entre **[!UICONTROL Activar]** y **[!UICONTROL Configurar]**, consulte la sección [Catálogo](../../ui/destinations-workspace.md#catalog) de la documentación del espacio de trabajo de destino.
>
>![Activar destino de Microsoft Bing](../../assets/catalog/advertising/bing/activate.png)

En el paso [!UICONTROL Autenticación], debe introducir los detalles de conexión de destino:

* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL ID]** de cuenta: Tu  [!DNL Bing Ads CID].
* **[!UICONTROL Caso]** de uso de marketing: Los casos de uso de mercadotecnia indican la intención para la cual se exportarán los datos al destino. Puede seleccionar entre los casos de uso de mercadotecnia definidos por el Adobe o puede crear su propio caso de uso de mercadotecnia. Para obtener más información sobre los casos de uso de mercadotecnia, consulte la página [Administración de datos en Adobe Experience Platform](../../../data-governance/policies/overview.md). Para obtener información sobre los casos de uso de mercadotecnia definidos por el Adobe, consulte la [información general sobre las directivas de uso de datos](../../../data-governance/policies/overview.md).

![Autenticación de destino de Microsoft Bing](../../assets/catalog/advertising/bing/authentication.png)

Haga clic en **[!UICONTROL Crear destino]**. Se ha creado el destino. Puede hacer clic en [!UICONTROL Guardar y salir] si desea activar segmentos más adelante, o puede hacer clic en [!UICONTROL Siguiente] para continuar el flujo de trabajo y seleccionar los segmentos que desea activar. En cualquier caso, consulte la siguiente sección, [Activar segmentos](#activate-segments), para el resto del flujo de trabajo.

## Activar segmentos {#activate-segments}

Consulte [Activar perfiles y segmentos en un destino](../../ui/activate-destinations.md#select-attributes) para obtener información sobre el flujo de trabajo de activación de segmentos.

En el paso [Programación de segmentos](../../ui/activate-destinations.md#segment-schedule), debe asignar manualmente los segmentos a su ID correspondiente o nombre práctico en el destino.

Al asignar segmentos, le recomendamos que utilice el nombre del segmento [!DNL Platform] o una forma más corta de éste, para facilitar su uso. Sin embargo, el ID o nombre del segmento en el destino no necesita coincidir con el de su cuenta [!DNL Platform]. Cualquier valor que inserte en el campo de asignación se verá reflejado por el destino.

![ID de asignación de segmentos](../../assets/common/segment-mapping-id.png)

## Datos exportados {#exported-data}

Para verificar si los datos se han exportado correctamente al destino [!DNL Microsoft Bing], compruebe su cuenta [!DNL Microsoft Bing Ads]. Si la activación se ha realizado correctamente, las audiencias se rellenan en su cuenta.