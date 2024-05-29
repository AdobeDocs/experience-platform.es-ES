---
title: mediaCollection
description: Configure el SDK web para recopilar datos relacionados con el uso de medios en las propiedades web.
source-git-commit: 1d1bb754769defd122faaa2160e06671bf02c974
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 6%

---


# `streamingMedia`

El `streamingMedia` Este componente le ayuda a recopilar datos relacionados con las sesiones de contenido del sitio web.

Los datos recopilados pueden incluir información sobre reproducciones de contenido, pausas, finalizaciones y otros eventos relacionados. Una vez recopilados, puede enviar estos datos a Adobe Experience Platform o Adobe Analytics para generar informes. Esta función proporciona una solución completa para realizar el seguimiento y comprender el comportamiento del consumo de medios en el sitio web.

## Requisitos previos {#prerequisites}

Para usar la variable `streamingMedia` del SDK web, debe cumplir los siguientes requisitos previos:

* Asegúrese de que tiene acceso a Adobe Experience Platform o Adobe Analytics.
* Debe utilizar la versión 2.20.0 o posterior del SDK web. Consulte la [Información general sobre la instalación del SDK web](../../install/overview.md) para obtener información sobre cómo instalar la versión más reciente.
* Habilite la **[[!UICONTROL Media Analytics]](../../../datastreams/configure.md#advanced-options)** para la secuencia de datos que está utilizando.
* Asegúrese de que el esquema utilizado por el conjunto de datos incluya los campos de esquema de recopilación de contenido.
* Configure la función Streaming Media en la configuración del SDK web, como se muestra en esta página, a través del [extensión de etiqueta](#tag-extension) o a través de [Biblioteca JavaScript](#library).

## Configuración de medios de streaming mediante la extensión de etiqueta del SDK web {#tag-extension}

Para configurar los medios de streaming en la extensión de etiqueta del SDK web, siga los pasos a continuación.

1. Iniciar sesión en [experience.adobe.com](https://experience.adobe.com) usando sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensiones]**, luego haga clic en **[!UICONTROL Configurar]** en el [!UICONTROL SDK web de Adobe Experience Platform] Tarjeta de.
1. Configure las variables **[!UICONTROL Medios de streaming]** configuración tal como se describe en [Página de configuración de extensión de etiqueta de SDK web](../../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#media-collection).

## Configurar los medios de streaming mediante la biblioteca JavaScript del SDK web {#library}

Para configurar los medios de streaming en el SDK web, utilice las propiedades que se describen a continuación.

Al llamar a `configure` , añada el comando `streamingMedia` objeto.

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
| `mainPingInterval` | Entero | No | Frecuencia de pings para el contenido principal, en segundos. El valor predeterminado es `10`. Los valores pueden variar desde `10` hasta `50` segundos.  Si no se especifica ningún valor, se utiliza el valor predeterminado al utilizar [sesiones rastreadas automáticamente](../createmediasession.md#automatic). |
| `adPingInterval` | Entero | No | Frecuencia de pings para el contenido del anuncio, en segundos. El valor predeterminado es `10`. Los valores pueden variar desde `1` hasta `10` segundos. Si no se especifica ningún valor, se utiliza el valor predeterminado al utilizar [sesiones rastreadas automáticamente](../createmediasession.md#automatic). |
