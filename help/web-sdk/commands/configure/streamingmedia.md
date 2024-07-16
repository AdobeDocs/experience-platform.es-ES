---
title: streamingMedia
description: Configure el SDK web para recopilar datos relacionados con el uso de medios en las propiedades web.
exl-id: f7733619-d35e-43eb-ac90-052717310c39
source-git-commit: 57d42d88ec9a93744450a2a352590ab57d9e5bb7
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 6%

---

# `streamingMedia`

El componente `streamingMedia` le ayuda a recopilar datos relacionados con las sesiones de contenido del sitio web.

Los datos recopilados pueden incluir información sobre reproducciones de contenido, pausas, finalizaciones y otros eventos relacionados. Una vez recopilados, puede enviar estos datos a Adobe Experience Platform o Adobe Analytics para generar informes. Esta función proporciona una solución completa para realizar el seguimiento y comprender el comportamiento del consumo de medios en el sitio web.

## Requisitos previos {#prerequisites}

Para utilizar el componente `streamingMedia` del SDK web, debe cumplir los siguientes requisitos previos:

* Asegúrese de que tiene acceso a Adobe Experience Platform o Adobe Analytics.
* Debe utilizar la versión 2.20.0 o posterior del SDK web. Consulte la [descripción general de la instalación del SDK web](../../install/overview.md) para obtener información sobre cómo instalar la versión más reciente.
* Habilite la opción **[[!UICONTROL Media Analytics]](../../../datastreams/configure.md#advanced-options)** para el conjunto de datos que esté usando.
* Asegúrese de que el esquema utilizado por el conjunto de datos incluya los campos de esquema de recopilación de contenido.
* Configure la función Streaming Media en la configuración del SDK web, como se muestra en esta página, ya sea mediante la [extensión de etiqueta](#tag-extension) o a través de la [biblioteca de JavaScript](#library).

## Configuración de medios de streaming mediante la extensión de etiqueta del SDK web {#tag-extension}

Para configurar los medios de streaming en la extensión de etiqueta del SDK web, siga los pasos a continuación.

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensions]** y, a continuación, haga clic en **[!UICONTROL Configure]** en la tarjeta de [!UICONTROL Adobe Experience Platform Web SDK].
1. Configure las opciones de **[!UICONTROL Streaming Media]** tal como se describe en la [página de configuración de la extensión de etiquetas del SDK web](../../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#media-collection).

## Configuración de medios de streaming mediante la biblioteca JavaScript del SDK web {#library}

Para configurar los medios de streaming en el SDK web, utilice las propiedades que se describen a continuación.

Al llamar al comando `configure`, agregue el objeto `streamingMedia`.

```js
alloy("configure", {
    streamingMedia: {
        channel: "video channel",
        playerName: "test player",
        appVersion: "Media Analytics with Web SDK 2.20.0",
        mainPingInterval: 10,
        adPingInterval: 10
    }
});
```

| Propiedad | Tipo | Requerido | Descripción |
|---------|----------|---------|---------|
| `channel` | Cadena | Sí | Nombre del canal en el que se produce la recopilación de medios de streaming. Ejemplo: `Video channel`. |
| `playerName` | Cadena | Sí | Nombre del reproductor de contenidos. |
| `appVersion` | Cadena | No | La versión de la aplicación del reproductor de contenidos. |
| `mainPingInterval` | Entero | No | Frecuencia de pings para el contenido principal, en segundos. El valor predeterminado es `10`. Los valores pueden oscilar entre `10` y `50` segundos.  Si no se especifica ningún valor, se usa el valor predeterminado al usar [sesiones con seguimiento automático](../createmediasession.md#automatic). |
| `adPingInterval` | Entero | No | Frecuencia de pings para el contenido del anuncio, en segundos. El valor predeterminado es `10`. Los valores pueden oscilar entre `1` y `10` segundos. Si no se especifica ningún valor, se usa el valor predeterminado al usar [sesiones con seguimiento automático](../createmediasession.md#automatic). |
