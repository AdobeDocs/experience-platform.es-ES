---
title: Anulaciones de configuración de secuencia de datos
description: Obtenga información sobre cómo configurar las anulaciones de flujos de datos mediante el SDK web.
exl-id: 8e327892-9520-43f5-abf4-d65a5ca34e6d
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 14%

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
   * Mediante los comandos del SDK web `sendEvent` o `configure`.
   * Mediante el comando del SDK móvil `sendEvent`.

Si establece invalidaciones tanto en la configuración del SDK web como en un comando específico (como [`sendEvent`](sendevent/overview.md)), las invalidaciones del comando específico tienen prioridad.

## Propiedades del objeto

Las siguientes propiedades están disponibles en este objeto:

* **Anulación de secuencia de datos**: Envíe llamadas a una secuencia de datos diferente. Si establece este valor, otras invalidaciones que requieran la configuración de la secuencia de datos deben configurarse en la secuencia de datos establecida aquí.
* **Contenedor de sincronización de ID de terceros**: El ID del contenedor de sincronización de ID de terceros de destino en Adobe Audience Manager. Antes de utilizar este campo, es necesario configurar una anulación del contenedor de ID de terceros en la configuración del conjunto de datos.
* **Token de propiedad de destino**: El token para la propiedad de destino en Adobe Target. Antes de utilizar este campo, es necesario configurar una anulación de token de propiedad de Target en la configuración del conjunto de datos.
* **Grupos de informes**: Los ID de los grupos de informes que se anularán en Adobe Analytics. Antes de utilizar este campo, es necesario configurar las anulaciones de grupos de informes en la configuración del conjunto de datos.

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

El ejemplo siguiente muestra el aspecto que podría tener una anulación de la configuración en un comando `sendEvent`.

```js {line-numbers="true" highlight="5-25"}
alloy("sendEvent", {
  xdm: {
    /* ... */
  },
  edgeConfigOverrides: {
    datastreamId: "{DATASTREAM_ID}"
    com_adobe_experience_platform: {
      datasets: {
        event: {
          datasetId: "SampleEventDatasetIdOverride"
        }
      }
    },
    com_adobe_analytics: {
      reportSuites: [
        "MyFirstOverrideReportSuite",
        "MySecondOverrideReportSuite",
        "MyThirdOverrideReportSuite"
        ]
    },
    com_adobe_identity: {
      idSyncContainerId: "1234567"
    },
    com_adobe_target: {
      propertyToken: "63a46bbc-26cb-7cc3-def0-9ae1b51b6c62"
    }
  }
});
```

| Parámetro | Descripción |
|---|---|
| `edgeConfigOverrides.datastreamId` | Utilice este parámetro para permitir que una sola solicitud vaya a una secuencia de datos diferente a la definida por el comando `configure`. |
| `com_adobe_analytics.reportSuites[]` | Matriz de cadenas que determina a qué grupos de informes desean enviar datos de Analytics. |
| `com_adobe_identity.idSyncContainerId` | El contenedor de sincronización de ID de terceros que desea utilizar en Audience Manager. |
| `com_adobe_target.propertyToken` | El token para la propiedad de destino de Adobe Target. |

### Enviar invalidaciones de configuración mediante el comando `configure` del SDK web {#send-configure}

El ejemplo siguiente muestra el aspecto que podría tener una anulación de la configuración en un comando `configure`.

```js {line-numbers="true" highlight="8-30"}
alloy("configure", {
  defaultConsent: "in",
  edgeDomain: "etc",
  edgeBasePath: "ee",
  datastreamId: "{DATASTREAM_ID}",
  orgId: "org",
  debugEnabled: true,
  edgeConfigOverrides: {
    "com_adobe_experience_platform": {
      "datasets": {
        "event": {
          datasetId: "SampleProfileDatasetIdOverride"
        }
      }
    },
    "com_adobe_analytics": {
      "reportSuites": [
        "MyFirstOverrideReportSuite",
        "MySecondOverrideReportSuite",
        "MyThirdOverrideReportSuite"
      ]
    },
    "com_adobe_identity": {
      "idSyncContainerId": "1234567"
    },
    "com_adobe_target": {
      "propertyToken": "63a46bbc-26cb-7cc3-def0-9ae1b51b6c62"
    }
  },
  onBeforeEventSend: function() { /* … */ });
};
```

| Parámetro | Descripción |
|---|---|
| `edgeConfigOverrides.datastreamId` | Utilice este parámetro para permitir que una sola solicitud vaya a una secuencia de datos diferente a la definida por el comando `configure`. |
| `com_adobe_analytics.reportSuites[]` | Matriz de cadenas que determina a qué grupos de informes desean enviar datos de Analytics. |
| `com_adobe_identity.idSyncContainerId` | El contenedor de sincronización de ID de terceros que desea utilizar en Audience Manager. |
| `com_adobe_target.propertyToken` | El token para la propiedad de destino de Adobe Target. |
