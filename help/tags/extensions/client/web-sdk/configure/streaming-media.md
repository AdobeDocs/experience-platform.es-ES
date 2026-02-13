---
title: Ajustes de configuración de medios de streaming
description: Personalice el modo en que la extensión de etiquetas Web SDK recopila datos de medios de streaming.
exl-id: f486d729-b7ad-4720-8399-71495cb9c57e
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 3%

---

# Ajustes de configuración de medios de streaming {#streaming-media}

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_streamingmedia"
>title="Medios de streaming"
>abstract="Determina cómo se recopilan los datos de medios de streaming durante las sesiones de reproducción de medios."

La función de recopilación de contenido le ayuda a recopilar datos relacionados con las sesiones de contenido, como reproducciones de contenido, pausas, finalizaciones y otros eventos relacionados. Una vez recopilados, puede enviar estos datos a Adobe Experience Platform o Adobe Analytics para generar informes. Esta función proporciona una solución completa para realizar el seguimiento y comprender el comportamiento del consumo de medios en el sitio web.

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensions]** y, a continuación, seleccione **[!UICONTROL Configure]** en la tarjeta [!UICONTROL Adobe Experience Platform Web SDK].
1. Vaya a la sección **[!UICONTROL Streaming media]**.

![Imagen que muestra la configuración de recopilación de medios de la extensión de etiquetas Web SDK en la interfaz de usuario de etiquetas](../assets/media-collection.png)

## Requisitos previos

Para utilizar el componente de medios de streaming de Web SDK, debe cumplir los siguientes requisitos previos:

* Asegúrese de tener acceso a Adobe Experience Platform o Adobe Analytics.
* Habilite la opción **[[!UICONTROL Media Analytics]](/help/datastreams/configure.md#advanced-options)** para el conjunto de datos que esté utilizando.
* Asegúrese de que el esquema utilizado por el conjunto de datos incluya los campos de esquema de recopilación de contenido.
* Configure la función Streaming Media en la extensión de etiquetas Web SDK, como se muestra en esta página.

## [!UICONTROL Channel]

Nombre del canal en el que se produce la recopilación de medios. Por ejemplo, `Video channel`. Cualquier valor de cadena es válido.

## [!UICONTROL Player Name]

Nombre del reproductor de contenidos que utiliza su propiedad para la reproducción de contenidos.

## [!UICONTROL Application Version]

La versión de la aplicación de reproducción de contenido que su propiedad utiliza para la reproducción de contenido.

## [!UICONTROL Main ping interval]

Frecuencia de pings para el contenido principal, en segundos. El valor predeterminado es `10`. Los valores pueden oscilar entre `10` y `50` segundos. Si no se especifica ningún valor, se usa el valor predeterminado al usar [sesiones con seguimiento automático](/help/collection/js/commands/createmediasession.md#automatic).

## [!UICONTROL Ad ping interval]

La frecuencia de pings para el contenido del anuncio, en segundos. El valor predeterminado es `10`. Los valores pueden oscilar entre `1` y `10` segundos. Si no se especifica ningún valor, se usa el valor predeterminado al usar [sesiones con seguimiento automático](/help/collection/js/commands/createmediasession.md#automatic).
