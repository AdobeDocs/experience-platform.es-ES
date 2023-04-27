---
title: Configurar anulaciones del almacén de datos
description: Obtenga información sobre cómo configurar las anulaciones del almacén de datos en la interfaz de usuario de Datastreams y activarlas mediante el SDK web.
source-git-commit: ce2e80a7ea7385be98bbcda6a0704cd0814c62b2
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 0%

---


# Configurar anulaciones del almacén de datos

Las anulaciones del almacén de datos le permiten definir configuraciones adicionales para sus conjuntos de datos, que se pasan a la red perimetral mediante el SDK web.

Esto le ayuda a almacenar en déclencheur diferentes comportamientos del conjunto de datos que los predeterminados, sin necesidad de crear un nuevo conjunto de datos ni modificar la configuración existente.

La anulación de la configuración del almacén de datos es un proceso de dos pasos:

1. En primer lugar, debe definir las anulaciones de configuración del conjunto de datos en la variable [página de configuración del almacén de datos](configure.md).
2. A continuación, debe enviar las anulaciones a la red perimetral a través de un comando Web SDK o utilizando el SDK web [extensión de etiqueta](../extension/web-sdk-extension-configuration.md).

Este artículo explica el proceso de anulación de la configuración del conjunto de datos de extremo a extremo para cada tipo de anulación admitida.

## Configurar anulaciones del almacén de datos en la interfaz de usuario de Datastreams {#configure-overrides}

Las anulaciones en la configuración del almacén de datos le permiten modificar las siguientes configuraciones del conjunto de datos:

* conjuntos de datos de eventos del Experience Platform
* Tokens de propiedad de Adobe Target
* Contenedores de sincronización de ID de Audience Manager
* Grupos de informes de Adobe Analytics

### Anulaciones del almacén de datos para Adobe Target {#target-overrides}

Para configurar las anulaciones del conjunto de datos para un conjunto de datos de Adobe Target, primero debe tener creado un conjunto de datos de Adobe Target. Siga las instrucciones para [configurar un conjunto de datos](configure.md) con la variable [Adobe Target](configure.md#target) servicio.

Una vez creado el conjunto de datos, edite el [Adobe Target](configure.md#target) que ha agregado y use el **[!UICONTROL Anulaciones de tokens de propiedad]** para agregar las anulaciones del conjunto de datos deseadas, como se muestra en la imagen siguiente. Agregue un token de propiedad por línea.

![Captura de pantalla de la interfaz de usuario de Datastreams que muestra la configuración del servicio Adobe Target, con las anulaciones de token de propiedad resaltadas.](../assets/datastreams/overrides/override-target.png)

Después de agregar las anulaciones deseadas, guarde la configuración del conjunto de datos.

Ahora debería tener configuradas las anulaciones del almacén de datos de Adobe Target. Ahora puede [enviar las anulaciones a la red perimetral mediante el SDK web](#send-overrides).

### Anulaciones del almacén de datos para Adobe Analytics {#analytics-overrides}

Para configurar las anulaciones del almacén de datos para un conjunto de datos de Adobe Analytics, primero debe tener un [Adobe Analytics](configure.md#analytics) datastream creado. Siga las instrucciones para [configurar un conjunto de datos](configure.md) con la variable [Adobe Analytics](configure.md#analytics) servicio.

Una vez creado el conjunto de datos, edite el [Adobe Analytics](configure.md#target) que ha agregado y use el **[!UICONTROL Anulaciones de grupos de informes]** para agregar las anulaciones del conjunto de datos deseadas, como se muestra en la imagen siguiente.

Select **[!UICONTROL Mostrar modo de lote]** para habilitar la edición por lotes de las anulaciones de grupos de informes. Puede copiar y pegar una lista de anulaciones de grupos de informes, introduciendo un grupo de informes por línea.

![Captura de pantalla de la interfaz de usuario de Datastreams que muestra la configuración del servicio Adobe Analytics, con las anulaciones del grupo de informes resaltadas.](../assets/datastreams/overrides/override-analytics.png)

Después de agregar las anulaciones deseadas, guarde la configuración del conjunto de datos.

Ahora debería tener configuradas las anulaciones del almacén de datos de Adobe Analytics. Ahora puede [enviar las anulaciones a la red perimetral mediante el SDK web](#send-overrides).

### Anulaciones de almacén de datos para conjuntos de datos de eventos de Experience Platform {#event-dataset-overrides}

Para configurar las anulaciones del almacén de datos para los conjuntos de datos de eventos de Experience Platform, primero debe tener un [Adobe Experience Platform](configure.md#aep) datastream creado. Siga las instrucciones para [configurar un conjunto de datos](configure.md) con la variable [Adobe Experience Platform](configure.md#aep) servicio.

Una vez creado el conjunto de datos, edite el [Adobe Experience Platform](configure.md#aep) que ha agregado y seleccione el **[!UICONTROL Agregar conjunto de datos de evento]** para agregar uno o más conjuntos de datos de evento anulados, como se muestra en la imagen siguiente.

![Captura de pantalla de la interfaz de usuario de Datastreams que muestra la configuración del servicio Adobe Experience Platform, con las anulaciones del conjunto de datos de evento resaltadas.](../assets/datastreams/overrides/override-aep.png)

Después de agregar las anulaciones deseadas, guarde la configuración del conjunto de datos.

Ahora debería tener configuradas las anulaciones del almacén de datos de Adobe Experience Platform. Ahora puede [enviar las anulaciones a la red perimetral mediante el SDK web](#send-overrides).

### Anulaciones de almacén de datos para contenedores de sincronización de ID de terceros {#container-overrides}

Para configurar las anulaciones del almacén de datos para los contenedores de sincronización de ID de terceros, primero debe crear un conjunto de datos. Siga las instrucciones para [configurar un conjunto de datos](configure.md) para crear uno.

Una vez creado el conjunto de datos, vaya a **[!UICONTROL Opciones avanzadas]** y habilite **[!UICONTROL Sincronización de ID de terceros]** .

A continuación, utilice el **[!UICONTROL Anulaciones de ID de contenedor]** para agregar los ID de contenedor que desea que anulen la configuración predeterminada, como se muestra en la imagen siguiente.

>[!IMPORTANT]
>
>Los ID de contenedor deben ser valores numéricos, como `1234567`y no cadenas, como `"1234567"`. Si envía un valor de cadena a través del SDK web como anulación de ID de contenedor, recibirá un error.

![Captura de pantalla de la interfaz de usuario de Datastreams que muestra la configuración del conjunto de datos, con las anulaciones del contenedor de sincronización de ID de terceros resaltadas.](../assets/datastreams/overrides/override-container.png)

Después de agregar las anulaciones deseadas, guarde la configuración del conjunto de datos.

Ahora debería tener configuradas las anulaciones del contenedor de sincronización de ID. Ahora puede [enviar las anulaciones a la red perimetral mediante el SDK web](#send-overrides).

## Envío de las anulaciones a la red perimetral mediante el SDK web {#send-overrides}

>[!NOTE]
>
>Como alternativa al envío de las anulaciones de configuración mediante comandos del SDK web, puede añadir las anulaciones de configuración al SDK web [extensión de etiqueta](../extension/web-sdk-extension-configuration.md).

Después [configuración de las anulaciones del almacén de datos](#configure-overrides) en la interfaz de usuario de recopilación de datos, ahora puede enviar las anulaciones a la red perimetral a través del SDK web.

El envío de las anulaciones a la red perimetral mediante el SDK web es el segundo y último paso para activar las anulaciones de configuración del conjunto de datos.

Las anulaciones de la configuración del conjunto de datos se envían a la red perimetral a través del `edgeConfigOverrides` SDK web. Este comando crea anulaciones del conjunto de datos que se pasan al [!DNL Edge Network] en el siguiente comando o, en el caso de la variable `configure` para cada solicitud.

La variable `edgeConfigOverrides` crea anulaciones del conjunto de datos que se pasan al [!DNL Edge Network] en el siguiente comando o, en el caso de `configure`, para cada solicitud.

Cuando se envía una anulación de configuración con la variable `configure` , se incluye en los siguientes comandos admitidos.

* [sendEvent](../fundamentals/tracking-events.md)
* [setConsent](../consent/iab-tcf/overview.md)
* [getIdentity](../identity/overview.md)
* [appendIdentityToUrl](../identity/id-sharing.md#cross-domain-sharing)
* [configure](../fundamentals/configuring-the-sdk.md)

Las opciones especificadas globalmente se pueden anular mediante la opción de configuración de comandos individuales.

### Envío de anulaciones de configuración a través del `sendEvent` command {#send-event}

El ejemplo siguiente muestra cómo podría verse una anulación de configuración en una `sendEvent` comando.

```js {line-numbers="true" highlight="5-25"}
alloy("sendEvent", {
  xdm: {
    /* ... */
  },
  edgeConfigOverrides: {
    com_adobe_experience_platform: {
      datasets: {
        event: {
          datasetId: "MyOverrideDataset"
        },
        profile: {
          datasetId: "www"
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

### Envío de anulaciones de configuración a través del `configure` command {#send-configure}

El ejemplo siguiente muestra cómo podría verse una anulación de configuración en una `configure` comando.

```js {line-numbers="true" highlight="8-30"}
alloy("configure", {
  defaultConsent: "in",
  edgeDomain: "etc",
  edgeBasePath: "ee",
  edgeConfigId: "etc",
  orgId: "org",
  debugEnabled: true,
  edgeConfigOverrides: {
    "com_adobe_experience_platform": {
      "datasets": {
        "event": { 
          datasetId: "MyOverrideDataset"
        },
        "profile": { 
          datasetId: "www"
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

### Ejemplo de carga útil {#payload-example}

Los ejemplos anteriores generan un [!DNL Edge Network] carga útil similar a esta:

```json
{
  "meta": {
    "configOverrides": {
      "com_adobe_experience_platform": {
        "datasets": {
          "event": {
            "datasetId": "MyOverrideDataset"
          },
          "profile": {
            "datasetId": "www"
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
    "state": {  }
  },
  "events": [  ],
  "query": {
    "identity": {
      "fetch": [
        "ECID"
      ]
    }
  }
}
```

