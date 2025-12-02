---
title: edgeConfigOverrides
description: Configure las anulaciones de flujos de datos para la implementación.
source-git-commit: f4a2778c71ad6a48621212f3ece1776d1b3ac643
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---

# `edgeConfigOverrides` (comando `configure`)

El objeto `edgeConfigOverrides` le permite anular los valores de configuración de los comandos que se ejecutan en la página actual. Este objeto es útil cuando tiene diferentes sitios web o subdominios para diferentes países o si tiene varios entornos limitados de Experience Platform para almacenar datos específicos de diferentes unidades comerciales. Si desea anular las opciones de configuración para un solo comando de la página, considere la posibilidad de utilizar el objeto [`edgeConfigOverrides` en el comando `sendEvent` ](../sendevent/edgeconfigoverrides.md).

El proceso de anulación de la configuración del conjunto de datos consta de dos pasos principales:

1. En primer lugar, debe definir la anulación de la configuración de la secuencia de datos al [configurar una secuencia de datos](/help/datastreams/configure.md) en la IU de Datastreams. Consulte [Anulaciones de configuración de secuencia de datos](/help/datastreams/overrides.md) en la documentación de flujos de datos para obtener instrucciones sobre cómo configurar las anulaciones.
1. Después de configurar la anulación de la secuencia de datos en la interfaz de usuario de flujos de datos, puede configurar el objeto `edgeConfigOverrides`.

Cuando establece el objeto `edgeConfigOverrides` en el comando `configure`, se aplica a todos los datos enviados a Adobe. Los siguientes comandos _also_ admiten el objeto `edgeConfigOverrides`:

* [sendEvent](../sendevent/edgeconfigoverrides.md)
* [&quot;setConsent&quot;](../setconsent.md)
* [getIdentity.](../getidentity.md)
* [&quot;appendIdentityToUrl&quot;](../appendidentitytourl.md)

La configuración de `edgeConfigOverrides` en cualquiera de los comandos anteriores tiene prioridad sobre el objeto `edgeConfigOverrides` del comando `configure` si ambos están establecidos. Si alguno de estos comandos no contiene un objeto `edgeConfigOverrides`, se utilizará el objeto `edgeConfigOverrides` del comando `configure`.

## Ejemplo

Si la configuración del flujo de datos tiene habilitados todos los servicios compatibles, el ejemplo siguiente anula esta configuración y deshabilita todos los servicios.

```js
alloy("configure", {
  orgId: "97D1F3F459CE0AD80A495CBE@AdobeOrg",
  datastreamId: "db9c70a1-6f11-4563-b0e9-b5964ab3a858",
  edgeConfigOverrides: {
    com_adobe_experience_platform: {
      enabled: false,
      datasets: {
        event: {
          datasetId: "64b6f930753dd41ca8d4fd77"
        }
      },
      com_adobe_edge_ode: {
        enabled: false
      },
      com_adobe_edge_segmentation: {
        enabled: false
      },
      com_adobe_edge_destinations: {
        enabled: false
      },
      com_adobe_edge_ajo: {
        enabled: false
      },
    },
    com_adobe_analytics: {
      enabled: false,
      reportSuites: ["exampleoverridersid","exampleoverridersid2"]
    },
    com_adobe_identity: {
      idSyncContainerId: 34373
    },
    com_adobe_target: {
      enabled: false,
      propertyToken: "01dbc634-07c1-d8f9-ca69-b489a5ac5e94"
    },
    com_adobe_audience_manager: {
      enabled: false
    },
    com_adobe_launch_ssf: {
      enabled: false
    }
  }
});
```

| Parámetro | Tipo | Descripción |
| --- | --- | --- |
| **`orgId`** | `string` | ID de organización de IMS de su empresa. |
| **`datastreamId`** | `string` | ID del conjunto de datos al que se enviarán los datos. |
| **`com_adobe_experience_platform`** | `object` | Define la configuración del flujo de datos dinámico para los servicios de Adobe Experience Platform. |
| **`com_adobe_experience_platform.enabled`** | `boolean` | Determina si el evento se envía a Adobe Experience Platform. |
| **`com_adobe_experience_platform.datasets`** | `object` | Define los conjuntos de datos utilizados para el evento. |
| **`com_adobe_experience_platform.com_adobe_edge_ode.enabled`** | `boolean` | Determina si el evento se envía a Offer Decisioning. |
| **`com_adobe_experience_platform.com_adobe_edge_segmentation.enabled`** | `boolean` | Determina si el evento se envía a la segmentación de Edge. |
| **`com_adobe_experience_platform.com_adobe_edge_destinations.enabled`** | `boolean` | Determina si el evento se envía a los destinos de Edge. |
| **`com_adobe_experience_platform.com_adobe_edge_ajo.enabled`** | `boolean` | Determina si el evento se envía a Adobe Journey Optimizer. |
| **`com_adobe_analytics.enabled`** | `boolean` | Determina si el evento se envía a Adobe Analytics. |
| **`com_adobe_analytics.reportSuites[]`** | `string[]` | Matriz de cadenas que determina a qué grupos de informes enviar datos de Analytics. |
| **`com_adobe_audience_manager.enabled`** | `boolean` | Determina si el evento se envía a Adobe Audience Manager. |
| **`com_adobe_identity.idSyncContainerId`** | `integer` | El contenedor de sincronización de ID de terceros que desea utilizar en Audience Manager. Requiere que `com_adobe_audience_manager.enabled` se establezca en `true`. De lo contrario, el servicio Audience Manager está deshabilitado. |
| **`com_adobe_target.enabled`** | `boolean` | Determina si el evento se envía a Adobe Target. |
| **`com_adobe_target.propertyToken`** | `string` | El token para la propiedad de destino de Adobe Target. |
| **`com_adobe_launch_ssf`** | `boolean` | Determina si el evento se envía al reenvío del lado del servidor. |

## Anulaciones de configuración mediante la extensión de etiquetas Web SDK

El equivalente de la extensión de etiquetas Web SDK de este campo se encuentra en [Invalidaciones de configuración](/help/tags/extensions/client/web-sdk/configure/configuration-overrides.md) al configurar la extensión de etiquetas.
