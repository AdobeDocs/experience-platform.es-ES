---
title: Anulaciones de configuración de secuencia de datos
description: Obtenga información sobre cómo configurar las anulaciones de flujos de datos mediante el SDK web.
source-git-commit: 9cb46957a1c9755dcad6279aae5f5cc04eb6b305
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 14%

---


# Configurar anulaciones de secuencia de datos

El `edgeConfigOverrides` permite anular los valores de configuración de los comandos que se ejecutan en la página actual. Este objeto override no es un comando, sino un objeto que se puede incluir en la mayoría de los comandos del SDK web.

Este objeto es útil cuando tiene diferentes sitios web o subdominios para diferentes países o si tiene varios entornos limitados de Experience Platform para almacenar datos específicos de diferentes unidades de negocio.

>[!IMPORTANT]
>
>Para obtener instrucciones de configuración detalladas e integrales sobre las anulaciones de flujos de datos, consulte la [anulaciones de configuración de secuencia de datos](../../datastreams/overrides.md#configure-overrides) documentación.

La anulación de la configuración del flujo de datos es un proceso de dos pasos:

1. En primer lugar, debe definir la anulación de la configuración de la secuencia de datos en [página configuración de secuencia de datos](../../datastreams/configure.md), en la interfaz de usuario de flujos de datos. Consulte la [anulaciones de configuración de secuencia de datos](../../datastreams/overrides.md#configure-overrides) para obtener instrucciones sobre cómo configurar las invalidaciones.
2. Después de configurar la anulación de la secuencia de datos en la interfaz de usuario de, debe enviar las invalidaciones a la red perimetral de una de las siguientes maneras:
   * A través del SDK web [extensión de etiqueta](#tag-extension).
   * A través de `sendEvent` o `configure` Comandos del SDK web.
   * A través del SDK móvil `sendEvent` comando.

Si establece invalidaciones tanto en la configuración del SDK web como en un comando específico (por ejemplo, [`sendEvent`](sendevent/overview.md)), las invalidaciones del comando específico tienen prioridad.

## Propiedades del objeto

Las siguientes propiedades están disponibles en este objeto:

* **Anulación de flujo de datos**: envía llamadas a un conjunto de datos diferente. Si establece este valor, otras invalidaciones que requieran la configuración de la secuencia de datos deben configurarse en la secuencia de datos establecida aquí.
* **Contenedor de sincronización de ID de terceros**: ID del contenedor de sincronización de ID de terceros de destino en Adobe Audience Manager. Antes de utilizar este campo, es necesario configurar una anulación del contenedor de ID de terceros en la configuración del conjunto de datos.
* **Token de propiedad de destino**: el token para la propiedad de destino en Adobe Target. Antes de utilizar este campo, es necesario configurar una anulación de token de propiedad de Target en la configuración del conjunto de datos.
* **Grupos de informes**: Los ID del grupo de informes que se anularán en Adobe Analytics. Antes de utilizar este campo, es necesario configurar las anulaciones de grupos de informes en la configuración del conjunto de datos.

## Envíe invalidaciones de flujo de datos a la red perimetral a través de la extensión de etiqueta del SDK web {#tag-extension}

Consulte la documentación sobre [configuración de anulaciones de flujos de datos](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#datastrea-overrides) en la extensión de etiquetas del SDK web para obtener instrucciones de configuración detalladas.

Si desea configurar las anulaciones de secuencia de datos desde la extensión de etiqueta del SDK web, establezca cada campo deseado en **[!UICONTROL Anulaciones de configuración de secuencia de datos]** cuando [configuración de la extensión de etiqueta](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Iniciar sesión en [experience.adobe.com](https://experience.adobe.com) usando sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensiones]**, luego haga clic en **[!UICONTROL Configurar]** en el [!UICONTROL SDK web de Adobe Experience Platform] Tarjeta de.
1. Desplácese hacia abajo hasta el **[!UICONTROL Anulaciones de configuración de secuencia de datos]** sección. Establezca cada valor de anulación deseado.
1. Clic **[!UICONTROL Guardar]** y, a continuación, publique los cambios.

Si desea establecer invalidaciones solo para un comando específico, establezca cada campo deseado dentro de las acciones de una regla de etiqueta.

1. Iniciar sesión en [experience.adobe.com](https://experience.adobe.com) usando sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Reglas]**, luego seleccione la regla que desee.
1. En [!UICONTROL Acciones], seleccione una acción existente o cree una acción.
1. Configure las variables [!UICONTROL Extensión] campo desplegable a **[!UICONTROL SDK web de Adobe Experience Platform]** y configure el [!UICONTROL Tipo de acción] hasta **[!UICONTROL Enviar evento]**.
1. Desplácese hacia abajo hasta la sección denominada **[!UICONTROL Anulaciones de configuración de secuencia de datos]**.
1. Establezca cada campo de esta sección en el valor de anulación deseado.
1. Clic **[!UICONTROL Conservar cambios]**, luego ejecute el flujo de trabajo de publicación.

Se proporcionan campos independientes para [!UICONTROL Desarrollo], [!UICONTROL Ensayo], y [!UICONTROL Producción] entornos. Asegúrese de rellenar cada campo deseado para cada entorno.

## Envíe las invalidaciones a la red perimetral mediante la biblioteca JavaScript del SDK web {#library}

Después [configuración de las anulaciones de secuencia de datos](../../datastreams/overrides.md) en la IU de recopilación de datos, ahora puede enviar las invalidaciones a la red perimetral a través de la biblioteca JavaScript del SDK web.

Si utiliza el SDK web, el envío de las invalidaciones a la red perimetral mediante la variable `edgeConfigOverrides` El comando es el segundo y último paso de activar las anulaciones de configuración de secuencia de datos.

Las anulaciones de configuración de la secuencia de datos se envían a Edge Network a través del comando `edgeConfigOverrides` del SDK web. Este comando crea invalidaciones de secuencia de datos que se pasan al [!DNL Edge Network] en el siguiente comando. Si utiliza el complemento `configure` , las anulaciones se pasan para cada solicitud.

El `edgeConfigOverrides` El comando crea anulaciones de secuencia de datos que se pasan al [!DNL Edge Network] en el siguiente comando.

Cuando se envía una anulación de la configuración con el comando `configure`, se incluye en los siguientes comandos del SDK web.

* [sendEvent](../commands/sendevent/overview.md)
* [setConsent](../commands/setconsent.md)
* [getIdentity](../commands/getidentity.md)
* [appendIdentityToUrl](../commands/appendidentitytourl.md)
* [configurar](../commands/configure/overview.md)

Las opciones especificadas globalmente pueden ser anuladas por la opción de configuración en comandos individuales.

### Envío de invalidaciones de configuración mediante el SDK web `sendEvent` mando {#send-event}

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

### Envío de invalidaciones de configuración mediante el SDK web `configure` mando {#send-configure}

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