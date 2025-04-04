---
title: Activar audiencias de Audience Manager mediante la activación expandida
description: Aprenda a activar audiencias de Audience Manager en destinos sociales y publicitarios mediante la activación expandida de Audience Manager.
exl-id: 4105f5c5-db69-414f-9ee4-8630b0a86da7
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# Activar audiencias mediante la activación expandida de Audience Manager

En esta página se describe el flujo de trabajo completo que debe seguir para activar audiencias de Audience Manager en las plataformas de destino admitidas por la activación expandida.

## Antes de empezar {#before-you-begin}

Los pasos descritos en esta guía suponen que ha leído la [página de información general de activación expandida](overview.md) y que ha confirmado que cumple los requisitos previos para la activación de audiencia.

>[!IMPORTANT]
>
>Para activar audiencias a través de [!DNL Expanded Activation], asegúrese de que las audiencias de Audience Manager estén basadas en **direcciones de correo electrónico con hash**. Consulte los [requisitos previos](overview.md#prerequisites) para obtener más información.

## Paso 1: Configuración de la conexión de origen de Audience Manager {#configure-source}

El [conector de origen de Audience Manager](../sources/connectors/adobe-applications/audience-manager.md) envía los datos de audiencia recopilados en Adobe Audience Manager para su activación en las plataformas de destino admitidas por la activación expandida.

Siga la guía sobre cómo [crear una conexión de origen de Audience Manager](../sources/tutorials/ui/create/adobe-applications/audience-manager.md) para configurar el conector de origen.

![Imagen de la interfaz de usuario de Experience Platform que muestra la ficha Orígenes con la conexión de origen de Audience Manager.](assets/sources-tab.png)

>[!TIP]
>
>El conector de origen de Adobe Audience Manager es el único conector de origen disponible en la activación expandida.
>
>Si desea introducir audiencias basadas en identificadores adicionales, debe adquirir una edición de [Real-Time CDP](../rtcdp/overview.md). Póngase en contacto con su representante de Adobe para obtener más información.

### Visualización y monitorización de audiencias ingeridas {#view-audiences}

Las audiencias que introduce en la activación expandida desde Audience Manager están disponibles para que las vea en el panel **[!UICONTROL Audiencias]**.

Para ver tus audiencias, ve a **[!UICONTROL Cliente]** -> **[!UICONTROL Audiencias]** -> **[!UICONTROL Examinar]**.

![Imagen de la interfaz de usuario de Experience Platform que muestra la página Audiencias.](assets/audiences-browse.png)

>[!IMPORTANT]
>
>* Las audiencias pueden tardar hasta 48 horas en rellenarse completamente en la activación expandida. Esto también se aplica a las actualizaciones de audiencias de Audience Manager existentes.
>* Las audiencias de Audience Manager recién creadas no aparecen automáticamente en la activación expandida. Para introducir nuevos segmentos en la activación expandida, debe añadirlos a través del conector de origen de Audience Manager.

Una vez que haya configurado el conector de origen de Audience Manager, vaya al [paso 2](#create-destination-connection).

## Paso 2: Crear una nueva conexión de destino {#create-destination-connection}

Para poder enviar las audiencias de Audience Manager a la plataforma de destino que elija, primero debe crear una conexión con una plataforma de destino.

En la barra lateral izquierda, vaya a **[!UICONTROL Conexiones]** -> **[!UICONTROL Destinos]** -> **[!UICONTROL Catálogo]**.

Las categorías de destino disponibles para [!DNL Expanded Activation] son [publicidad](../destinations/catalog/advertising/overview.md) y [medios sociales](../destinations/catalog/social/overview.md).

![Imagen de la interfaz de usuario de Experience Platform que muestra el catálogo de destino para la activación expandida.](assets/destination-catalog.png)

Para crear una nueva conexión a una plataforma de destino, siga la guía de [cómo crear una nueva conexión de destino](../destinations/ui/connect-destination.md). A continuación, pase al [paso 3](#activate-audiences).

## Paso 3: Activación de audiencias en el destino {#activate-audiences}

Después de [ingerir audiencias de Audience Manager](#configure-source) correctamente y de [crear una nueva conexión de destino](#create-destination-connection), ahora puede activar las audiencias en la plataforma de destino que elija.

![Imagen de la interfaz de usuario de Experience Platform que muestra el catálogo de destino para la activación expandida.](assets/activate-audiences.png)

Para activar audiencias en tu destino, sigue la guía de [cómo activar audiencias en los destinos de streaming](../destinations/ui/activate-segment-streaming-destinations.md).

## Verificar activación de audiencia {#verify}

Consulte la [documentación de supervisión de destino](../dataflows/ui/monitor-destinations.md) para obtener información detallada sobre cómo supervisar el flujo de datos a sus destinos.
