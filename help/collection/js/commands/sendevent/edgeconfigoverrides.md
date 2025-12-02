---
title: edgeConfigOverrides
description: Configure las anulaciones de flujos de datos solo para el comando sendEvent.
exl-id: 8e327892-9520-43f5-abf4-d65a5ca34e6d
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---

# `edgeConfigOverrides` (comando `sendEvent`)

El objeto `edgeConfigOverrides` le permite anular los valores de configuración sólo para el comando `sendEvent` actual. Este objeto es útil cuando tiene comandos específicos en la misma página que desea ejecutar con parámetros de configuración diferentes a los del resto de la implementación de Web SDK. Si desea anular las opciones de configuración de todos los comandos de una página determinada, considere la posibilidad de utilizar el objeto [`edgeConfigOverrides` en el comando `configure` &#x200B;](../configure/edgeconfigoverrides.md).

El proceso general de anulación de la configuración del flujo de datos consta de dos pasos principales:

1. En primer lugar, debe definir la anulación de la configuración de la secuencia de datos al [configurar una secuencia de datos](/help/datastreams/configure.md) en la IU de Datastreams. Consulte [Anulaciones de configuración de secuencia de datos](/help/datastreams/overrides.md) en la documentación de flujos de datos para obtener instrucciones sobre cómo configurar las anulaciones.
1. Después de configurar la anulación de la secuencia de datos en la interfaz de usuario de flujos de datos, puede configurar el objeto `edgeConfigOverrides`.

Tenga en cuenta que el comando `configure` también admite un objeto `edgeConfigOverrides`; consulte [`edgeConfigOverrides`](../configure/edgeconfigoverrides.md) en el comando `configure`. El objeto `edgeConfigOverrides` del comando `sendEvent` tiene prioridad sobre el objeto `edgeConfigOverrides` del comando `configure` si ambos están establecidos.

## Ejemplo

Si la configuración del flujo de datos tiene habilitados todos los servicios compatibles, el ejemplo siguiente anula esta configuración y deshabilita todos los servicios (consulte la configuración de `enabled: false` en cada servicio). Este objeto admite las mismas propiedades que el objeto [`edgeConfigOverrides`](../configure/edgeconfigoverrides.md) en el comando `configure`.

```js
alloy("sendEvent", {
  renderDecisions: true,
  edgeConfigOverrides: {
    datastreamId: "bfa8fe21-6157-42d3-b47a-78310920b39d",
    com_adobe_experience_platform: {
      enabled: false,
      datasets: {
        event: {
          datasetId: "64b6f949a8a6891ca8a28911",
        },
      },
      com_adobe_edge_ode: {
        enabled: false,
      },
      com_adobe_edge_segmentation: {
        enabled: false,
      },
      com_adobe_edge_destinations: {
        enabled: false,
      },
      com_adobe_edge_ajo: {
        enabled: false,
      },
    },
    com_adobe_analytics: {
      enabled: false,
      reportSuites: ["examplersid3"],
    },
    com_adobe_identity: {
      idSyncContainerId: 34374,
    },
    com_adobe_target: {
      enabled: false,
      propertyToken: "f3fd55e1-a06d-8650-9aa5-c8356c6e2223",
    },
    com_adobe_audience_manager: {
      enabled: false,
    },
    com_adobe_launch_ssf: {
      enabled: false,
    },
  },
});
```

## Anulaciones de configuración de secuencia de datos mediante la extensión de etiquetas Web SDK

La extensión de etiquetas Web SDK equivalente a este objeto es la sección [Anulaciones de configuración de secuencia de datos](/help/tags/extensions/client/web-sdk/actions/send-event.md#datastream-configuration-overrides) al configurar la acción &#39;[!UICONTROL Send event]&#39;.
