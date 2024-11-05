---
title: Anulaciones de configuración de secuencia de datos
description: Obtenga información sobre cómo configurar las anulaciones de flujos de datos mediante el SDK web.
exl-id: 8e327892-9520-43f5-abf4-d65a5ca34e6d
source-git-commit: 2b8ca4bc1d5cf896820a5de95dcdfcd15edc2392
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Configurar anulaciones de secuencia de datos

El objeto `edgeConfigOverrides` le permite anular los valores de configuración de los comandos que se ejecutan en la página actual. Este objeto override no es un comando, sino un objeto que se puede incluir en la mayoría de los comandos del SDK web.

Este objeto es útil cuando tiene diferentes sitios web o subdominios para diferentes países o si tiene varios entornos limitados de Experience Platform para almacenar datos específicos de diferentes unidades de negocio.

>[!IMPORTANT]
>
>Para obtener instrucciones de configuración detalladas e integrales sobre las anulaciones de flujos de datos, consulte la documentación [anulaciones de configuración de flujos de datos](../../datastreams/overrides.md#configure-overrides).

La anulación de la configuración del flujo de datos es un proceso de dos pasos:

1. En primer lugar, debe definir la anulación de la configuración de la secuencia de datos en la [página de configuración de la secuencia de datos](../../datastreams/configure.md), dentro de la interfaz de usuario de Datastreams. Consulte la documentación de [anulaciones de configuración de secuencia de datos](../../datastreams/overrides.md#configure-overrides) para obtener instrucciones sobre cómo configurar las anulaciones.
2. Después de configurar la anulación de la secuencia de datos en la interfaz de usuario de, debe enviar las invalidaciones al Edge Network de una de las siguientes maneras:
   * A través del SDK web [extensión de etiqueta](#tag-extension).
   * Mediante los comandos del SDK web [`sendEvent`](../commands/sendevent/overview.md) o [`configure`](../commands/configure/overview.md).
   * Mediante el comando del SDK móvil [`sendEvent`](https://developer.adobe.com/client-sdks/home/getting-started/track-events/#send-events-to-edge-network).

Si establece invalidaciones tanto en la configuración del SDK web como en un comando específico (como [`sendEvent`](sendevent/overview.md)), las invalidaciones del comando específico tienen prioridad.

>[!NOTE]
>
>Si desea que una anulación de la configuración *deshabilite* un servicio de Experience Cloud, debe asegurarse de que el servicio esté primero *habilitado* en la configuración de la secuencia de datos. Consulte la documentación sobre cómo [configurar flujos de datos](../../datastreams/configure.md#add-services) para obtener detalles sobre cómo agregar servicios a un flujo de datos.

## Envíe invalidaciones de secuencia de datos al Edge Network a través de la extensión de etiquetas del SDK web {#tag-extension}

Consulte la documentación sobre [configuración de anulaciones de secuencia de datos](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#datastrea-overrides) desde la extensión de etiqueta del SDK web para obtener instrucciones de configuración detalladas.

Si desea configurar las invalidaciones de secuencia de datos desde la extensión de etiqueta del SDK web, establezca cada campo deseado en **[!UICONTROL Invalidaciones de configuración de secuencia de datos]** al [configurar la extensión de etiqueta](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensions]** y, a continuación, haga clic en **[!UICONTROL Configure]** en la tarjeta de [!UICONTROL Adobe Experience Platform Web SDK].
1. Desplácese hacia abajo hasta la sección **[!UICONTROL Anulaciones de configuración de secuencia de datos]**. Establezca cada valor de anulación deseado.
1. Haz clic en **[!UICONTROL Guardar]** y después publica los cambios.

Si desea establecer invalidaciones solo para un comando específico, establezca cada campo deseado dentro de las acciones de una regla de etiqueta.

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Reglas]** y luego seleccione la regla que desee.
1. En [!UICONTROL Acciones], seleccione una acción existente o cree una acción.
1. Establezca el campo desplegable [!UICONTROL Extension] en **[!UICONTROL SDK web de Adobe Experience Platform]** y establezca [!UICONTROL Action Type] en **[!UICONTROL Send event]**.
1. Desplácese hacia abajo hasta la sección denominada **[!UICONTROL Anulaciones de configuración de secuencia de datos]**.
1. Establezca cada campo de esta sección en el valor de anulación deseado.
1. Haga clic en **[!UICONTROL Conservar cambios]** y, a continuación, ejecute el flujo de trabajo de publicación.

Se proporcionan campos independientes para los entornos [!UICONTROL Development], [!UICONTROL Staging] y [!UICONTROL Production]. Asegúrese de rellenar cada campo deseado para cada entorno.

## Envíe las invalidaciones al Edge Network a través de la biblioteca JavaScript del SDK web {#library}

Después de [configurar las invalidaciones de la secuencia de datos](../../datastreams/overrides.md) en la IU de recopilación de datos, ahora puede enviar las invalidaciones al Edge Network a través de la biblioteca JavaScript del SDK web.

Si utiliza el SDK web, el envío de las invalidaciones al Edge Network mediante el comando `edgeConfigOverrides` es el segundo y último paso de activar las invalidaciones de configuración de la secuencia de datos.

Las anulaciones de configuración de la secuencia de datos se envían a Edge Network a través del comando `edgeConfigOverrides` del SDK web. Este comando crea invalidaciones de secuencia de datos que se pasan al [!DNL Edge Network] en el siguiente comando. Si usa el comando `configure`, las invalidaciones se pasan para cada solicitud.

El comando `edgeConfigOverrides` crea invalidaciones de secuencia de datos que se pasan al [!DNL Edge Network] en el siguiente comando.

Cuando se envía una anulación de la configuración con el comando `configure`, se incluye en los siguientes comandos del SDK web.

* [sendEvent](../commands/sendevent/overview.md)
* [setConsent](../commands/setconsent.md)
* [getIdentity](../commands/getidentity.md)
* [appendIdentityToUrl](../commands/appendidentitytourl.md)
* [configurar](../commands/configure/overview.md)

Las opciones especificadas globalmente pueden ser anuladas por la opción de configuración en comandos individuales.

### Enviar invalidaciones de configuración mediante el comando `sendEvent` del SDK web {#send-event}

El ejemplo siguiente muestra todas las opciones de configuración de secuencia de datos dinámica admitidas en una llamada a `sendEvent`.

Si la configuración del flujo de datos tiene habilitados todos los servicios compatibles, el ejemplo siguiente anulará esta configuración y deshabilitará todos los servicios (consulte la configuración de `enabled: false` en cada servicio).

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
      reportSuites: ["ujslconfigoverrides3"],
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

| Parámetro | Descripción |
|---|---|
| `renderDecisions` |  |
| `edgeConfigOverrides.datastreamId` | Utilice este parámetro para permitir que una sola solicitud vaya a una secuencia de datos diferente a la definida por el comando `configure`. |
| `edgeConfigOverrides.com_adobe_experience_platform` | Define la configuración del flujo de datos dinámico para el servicio de Experience Platform. |
| `edgeConfigOverrides.com_adobe_experience_platform.enabled` | Define si el evento se enviará al servicio Experience Platform o no. |
| `edgeConfigOverrides.com_adobe_experience_platform.datasets` | Define los conjuntos de datos utilizados para el evento. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_ode.enabled` | Define si el evento se envía al servicio Offer decisioning o no. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_segmentation.enabled` | Define si el evento se envía al servicio de segmentación de Edge o no. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_destinations.enabled` | Define si los datos de evento se envían o no a los destinos Edge. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_ajo.enabled` | Define si los datos de evento se envían al servicio de Adobe Journey Optimizer o no. |
| `com_adobe_analytics.enabled` | Define si los datos de evento se envían o no a Adobe Analytics. |
| `com_adobe_analytics.reportSuites[]` | Matriz de cadenas que determina a qué grupos de informes desea enviar datos de Analytics. |
| `com_adobe_identity.idSyncContainerId` | El contenedor de sincronización de ID de terceros que desea utilizar en Audience Manager. Para que este contenedor de sincronización de ID funcione, debe establecer `com_adobe_audience_manager.enabled` en `true`. De lo contrario, el servicio Audience Manager está deshabilitado. |
| `com_adobe_target.enabled` | Define si los datos de evento se envían a Adobe Target. |
| `com_adobe_target.propertyToken` | El token para la propiedad de destino de Adobe Target. |
| `com_adobe_audience_manager.enabled` | Define si los datos de evento se envían al servicio Audience Manager. |
| `com_adobe_launch_ssf` | Define si los datos de evento se envían al reenvío del lado del servidor. |

### Enviar invalidaciones de configuración mediante el comando `configure` del SDK web {#send-configure}

El ejemplo siguiente muestra el aspecto que podría tener una anulación de la configuración en un comando `configure`.

Si la configuración del flujo de datos tiene habilitados todos los servicios compatibles, el ejemplo siguiente anulará esta configuración y deshabilitará todos los servicios (consulte la configuración de `enabled: false` en cada servicio).

```js
alloy("configure", {
  orgId: "97D1F3F459CE0AD80A495CBE@AdobeOrg",
  datastreamId: "db9c70a1-6f11-4563-b0e9-b5964ab3a858",
  edgeConfigOverrides: {
    com_adobe_experience_platform: {
      enabled: false,
      datasets: {
        event: {
          datasetId: "64b6f930753dd41ca8d4fd77",
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
      reportSuites: ["ujslconfigoverrides2"],
    },
    com_adobe_identity: {
      idSyncContainerId: 34373,
    },
    com_adobe_target: {
      enabled: false,
      propertyToken: "01dbc634-07c1-d8f9-ca69-b489a5ac5e94",
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

| Parámetro | Descripción |
|---|---|
| `orgId` | El ID de organización de IMS correspondiente a su cuenta de Adobe. |
| `edgeConfigOverrides.datastreamId` | Utilice este parámetro para permitir que una sola solicitud vaya a una secuencia de datos diferente a la definida por el comando `configure`. |
| `edgeConfigOverrides.com_adobe_experience_platform` | Define la configuración del flujo de datos dinámico para el servicio de Experience Platform. |
| `edgeConfigOverrides.com_adobe_experience_platform.enabled` | Define si el evento se enviará al servicio Experience Platform o no. |
| `edgeConfigOverrides.com_adobe_experience_platform.datasets` | Define los conjuntos de datos utilizados para el evento. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_ode.enabled` | Define si el evento se envía al servicio Offer decisioning o no. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_segmentation.enabled` | Define si el evento se envía al servicio de segmentación de Edge o no. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_destinations.enabled` | Define si los datos de evento se envían o no a los destinos Edge. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_ajo.enabled` | Define si los datos de evento se envían al servicio de Adobe Journey Optimizer o no. |
| `com_adobe_analytics.enabled` | Define si los datos de evento se envían o no a Adobe Analytics. |
| `com_adobe_analytics.reportSuites[]` | Matriz de cadenas que determina a qué grupos de informes desea enviar datos de Analytics. |
| `com_adobe_identity.idSyncContainerId` | El contenedor de sincronización de ID de terceros que desea utilizar en Audience Manager. Para que este contenedor de sincronización de ID funcione, debe establecer `com_adobe_audience_manager.enabled` en `true`. De lo contrario, el servicio Audience Manager está deshabilitado. |
| `com_adobe_target.enabled` | Define si los datos de evento se envían a Adobe Target. |
| `com_adobe_target.propertyToken` | El token para la propiedad de destino de Adobe Target. |
| `com_adobe_audience_manager.enabled` | Define si los datos de evento se envían al servicio Audience Manager. |
| `com_adobe_launch_ssf` | Define si los datos de evento se envían al reenvío del lado del servidor. |

