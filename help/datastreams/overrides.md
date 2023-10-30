---
title: Configurar anulaciones de secuencia de datos
description: Obtenga información sobre cómo configurar las anulaciones de secuencias de datos en la interfaz de usuario de secuencias de datos y activarlas mediante el SDK web.
exl-id: 3f17a83a-dbea-467b-ac67-5462c07c884c
source-git-commit: 5effb8a514100c28ef138ba1fc443cf29a64319a
workflow-type: tm+mt
source-wordcount: '1464'
ht-degree: 78%

---

# Configurar anulaciones de secuencia de datos

Las anulaciones de las secuencias de datos permiten definir configuraciones adicionales para las secuencias de datos, que pasan a la red perimetral mediante el SDK web.

Esto le ayuda a activar comportamientos de secuencias de datos diferentes de los predeterminados, sin crear una nueva secuencia de datos ni modificar la configuración existente.

La anulación de la configuración de la secuencia de datos es un proceso de dos pasos:

1. En primer lugar, debe definir las anulaciones de configuración de la secuencia de datos en la [página de configuración de secuencia de datos](configure.md).
2. A continuación, debe enviar las invalidaciones a la red perimetral de una de las siguientes maneras:
   * A través de `sendEvent` o `configure` [SDK web](#send-overrides-web-sdk) comandos.
   * A través del SDK web [extensión de etiqueta](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).
   * A través del SDK móvil [API sendEvent](#send-overrides-mobile-sdk) llamada.

Este artículo explica el proceso de anulación de la configuración de la secuencia de datos de extremo a extremo para cada tipo de anulación admitida.

>[!IMPORTANT]
>
>Las anulaciones de flujos de datos solo se admiten para [SDK web](../edge/home.md) y [Mobile SDK](https://developer.adobe.com/client-sdks/documentation/) integraciones. [API de servidor](../server-api/overview.md) en este momento, las integraciones no admiten invalidaciones de conjuntos de datos.
><br>
>Las anulaciones de secuencias de datos deben utilizarse cuando necesite enviar datos diferentes a secuencias de datos diferentes. No debe utilizar las anulaciones de secuencias de datos para casos de uso de personalización o datos de consentimiento.

## Casos de uso {#use-cases}

Para comprender mejor cómo y cuándo utilizar las anulaciones de secuencias de datos, estos son algunos casos de uso que los clientes de Adobe Experience Platform pueden solucionar mediante esta función.

**Recopilación de datos de varias regiones**

Una compañía tiene diferentes sitios web o subdominios para diferentes países en los que opera. Han [configurado](configure.md) secuencias de datos independientes con los grupos de informes específicos de Analytics correspondientes, los tókenes de propiedad de Adobe Target específicos del país, los esquemas específicos del país, los conjuntos de datos, las configuraciones de Journey Optimizer, etc. La compañía también tiene un conjunto global de configuraciones en las que se agregan todos los datos específicos de países.

Al utilizar las anulaciones de secuencias de datos, la empresa puede cambiar dinámicamente el flujo de datos a diferentes secuencias de datos, en lugar del comportamiento predeterminado de enviar datos a una secuencia de datos.

Un caso de uso común podría ser enviar datos a una secuencia de datos específica de un país y también enviar datos a una secuencia de datos global en la que los clientes realicen una acción importante, como realizar un pedido o actualizar su perfil de usuario.

**Diferenciación de perfiles e identidades para diferentes unidades de negocio**

Una compañía con varias unidades de negocio desea utilizar varias zonas protegidas de Experience Platform para almacenar datos específicos de cada unidad de negocio.

En lugar de enviar datos a una secuencia de datos predeterminada, la compañía puede usar las anulaciones de secuencias de datos para asegurarse de que cada unidad comercial tenga su propia secuencia de datos para recibir datos.

## Configuración de anulaciones de secuencia de datos en la IU de secuencias de datos {#configure-overrides}

Las anulaciones de configuración de secuencia de datos permiten modificar las siguientes configuraciones de secuencia de datos:

* Conjuntos de datos de evento de Experience Platform
* Tókenes de propiedad de Adobe Target
* Contenedores de sincronización de ID de Audience Manager
* Grupos de informes de Adobe Analytics

### Anulaciones de secuencia de datos para Adobe Target {#target-overrides}

Para configurar las anulaciones de secuencia de datos para una secuencia de datos de Adobe Target, primero debe tener creada una secuencia de datos de Adobe Target. Siga las instrucciones para [configurar una secuencia de datos](configure.md) con el servicio [Adobe Target](configure.md#target).

Una vez creada la secuencia de datos, edite el servicio [Adobe Target](configure.md#target) que ha añadido y utilice la sección **[!UICONTROL Anulaciones de token de propiedad]** para añadir las anulaciones de secuencia de datos deseadas, como se muestra en la siguiente imagen. Agregue un token de propiedad por línea.

![Captura de pantalla de la IU de secuencias de datos que muestra la configuración del servicio Adobe Target, con las anulaciones del token de propiedad resaltadas.](assets/overrides/override-target.png)

Después de agregar las anulaciones deseadas, guarde la configuración de la secuencia de datos.

Ahora debe tener configuradas las anulaciones de la secuencia de datos de Adobe Target. Ahora puede [enviar las anulaciones a Edge Network mediante el SDK web](#send-overrides).

### Anulaciones de secuencias de datos para Adobe Analytics {#analytics-overrides}

Para configurar las anulaciones de secuencias de datos para una secuencia de datos de Adobe Analytics, primero debe tener una secuencia de datos de [Adobe Analytics](configure.md#analytics) creada. Siga las instrucciones de [configuración de una secuencia de datos](configure.md) con el servicio [Adobe Analytics](configure.md#analytics).

Una vez creada la secuencia de datos, edite el servicio de [Adobe Analytics](configure.md#target) que ha añadido y utilice la sección **[!UICONTROL Anulaciones de grupo de informes]** para añadir las anulaciones de secuencia de datos deseadas, como se muestra en la siguiente imagen.

Seleccione **[!UICONTROL Mostrar modo por lotes]** para habilitar la edición por lotes de las anulaciones del grupo de informes. Puede copiar y pegar una lista de anulaciones de grupos de informes introduciendo un grupo de informes por línea.

![Captura de pantalla de la IU de secuencias de datos que muestra la configuración del servicio de Adobe Analytics, con las anulaciones del grupo de informes resaltadas.](assets/overrides/override-analytics.png)

Después de agregar las anulaciones deseadas, guarde la configuración de la secuencia de datos.

Ahora debe tener configuradas las anulaciones de la secuencia de datos de Adobe Analytics. Ahora puede [enviar las anulaciones a Edge Network mediante el SDK web](#send-overrides).

### Anulaciones de secuencia de datos para conjuntos de datos de eventos de Experience Platform {#event-dataset-overrides}

Para configurar las anulaciones de secuencias de datos para conjuntos de datos de evento de Experience Platform, primero debe tener una secuencia de datos de [Adobe Experience Platform](configure.md#aep) creada. Siga las instrucciones de [configuración de una secuencia de datos](configure.md) con el servicio [Adobe Experience Platform](configure.md#aep).

Una vez creada la secuencia de datos, edite el servicio [Adobe Experience Platform](configure.md#aep) que ha añadido y seleccione la opción **[!UICONTROL Agregar conjunto de datos de evento]** para añadir uno o más conjuntos de datos de evento de anulación, como se muestra en la siguiente imagen.

![Captura de pantalla de la IU de secuencias de datos que muestra la configuración del servicio Adobe Experience Platform, con las anulaciones del conjunto de datos de evento resaltadas.](assets/overrides/override-aep.png)

Después de agregar las anulaciones deseadas, guarde la configuración de la secuencia de datos.

Ahora debe tener configuradas las anulaciones de la secuencia de datos de Adobe Experience Platform. Ahora puede [enviar las anulaciones a la red perimetral mediante el SDK web](#send-overrides).

### Anulaciones de secuencia de datos para contenedores de sincronización de ID de terceros {#container-overrides}

Para configurar las anulaciones de secuencias de datos para los contenedores de sincronización de ID de terceros, primero debe haber creado una secuencia de datos. Siga las instrucciones de [configuración de una secuencia de datos](configure.md) para crear una.

Una vez creada la secuencia de datos, vaya a **[!UICONTROL Opciones avanzadas]** y habilite la opción **[!UICONTROL Sincronización de ID de terceros]**.

A continuación, utilice la sección **[!UICONTROL Anulaciones de ID de contenedor]** para añadir los ID de contenedor que desea que anulen la configuración predeterminada, como se muestra en la siguiente imagen.

>[!IMPORTANT]
>
>Los ID de contenedor deben ser valores numéricos, como `1234567`, y no cadenas, como `"1234567"`. Si envía un valor de cadena mediante el SDK web como una anulación de ID de contenedor, recibirá un error.

![Captura de pantalla de la IU de flujos de datos que muestra la configuración de secuencias de datos, con las anulaciones del contenedor de sincronización de ID de terceros resaltadas.](assets/overrides/override-container.png)

Después de agregar las anulaciones deseadas, guarde la configuración de la secuencia de datos.

Ahora debería tener configuradas las anulaciones del contenedor de sincronización de ID. Ahora puede [enviar las anulaciones a Edge Network mediante el SDK web](#send-overrides).

## Envíe las anulaciones a Edge Network mediante el SDK web {#send-overrides-web-sdk}

>[!NOTE]
>
>Como alternativa al envío de las anulaciones de configuración mediante comandos del SDK web, puede agregar las anulaciones de configuración a la [extensión de etiqueta](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md) del SDK web.

Después de [configurar las anulaciones de secuencias de datos](#configure-overrides) en la IU de recopilación de datos, ahora puede enviar las anulaciones a Edge Network, mediante el SDK web.

Si utiliza el SDK web, el envío de las invalidaciones a la red perimetral mediante la variable `edgeConfigOverrides` El comando es el segundo y último paso de activar las anulaciones de configuración de secuencia de datos.

Las anulaciones de configuración de la secuencia de datos se envían a Edge Network a través del comando `edgeConfigOverrides` del SDK web. Este comando crea anulaciones de secuencia de datos que se pasan al [!DNL Edge Network] en el siguiente comando, o, en el caso del comando `configure`, para cada solicitud.

El comando `edgeConfigOverrides` crea anulaciones de secuencia de datos que se pasan al [!DNL Edge Network] en el siguiente comando, o, en el caso de `configure`, para cada solicitud.

Cuando se envía una anulación de la configuración con el comando `configure`, se incluye en los siguientes comandos del SDK web.

* [sendEvent](../edge/fundamentals/tracking-events.md)
* [setConsent](../edge/consent/iab-tcf/overview.md)
* [getIdentity](../edge/identity/overview.md)
* [appendIdentityToUrl](../edge/identity/id-sharing.md#cross-domain-sharing)
* [configurar](../edge/fundamentals/configuring-the-sdk.md)

Las opciones especificadas globalmente pueden ser anuladas por la opción de configuración en comandos individuales.

### Envío de anulaciones de configuración mediante el SDK web `sendEvent` mando {#send-event}

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

| Parámetro | Descripción |
|---|---|
| `edgeConfigOverrides.datastreamId` | Utilice este parámetro para permitir que una sola solicitud vaya a una secuencia de datos diferente a la definida por el comando `configure`. |

### Envío de anulaciones de configuración mediante el comando `configure` {#send-configure}

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

## Envíe las invalidaciones a la red perimetral mediante el SDK móvil {#send-overrides-mobile-sdk}

Después [configuración de las anulaciones de secuencia de datos](#configure-overrides) en la IU de recopilación de datos, ahora puede enviar las invalidaciones a la red perimetral mediante el SDK para móviles.

Si utiliza el SDK móvil, el envío de las invalidaciones a la red perimetral mediante la variable `sendEvent` La API es el segundo y último paso de activar las anulaciones de configuración del flujo de datos.

Para obtener más información sobre el SDK de Experience Platform Mobile, consulte la [Documentación del SDK móvil](https://developer.adobe.com/client-sdks/edge/edge-network/).

### Anulación de ID de flujo de datos mediante SDK móvil {#id-override-mobile}

Los ejemplos siguientes muestran el aspecto que podría tener la anulación de ID de un conjunto de datos en una integración de SDK móvil. Seleccione las pestañas a continuación para ver las [!DNL iOS] y [!DNL Android] ejemplos.

>[!BEGINTABS]

>[!TAB iOS (Swift)]

Este ejemplo muestra el aspecto de la anulación de ID de un conjunto de datos en un SDK móvil [!DNL iOS] integración.

```swift
// Create Experience event from dictionary
var xdmData: [String: Any] = [
  "eventType": "SampleXDMEvent",
  "sample": "data",
]
let experienceEvent = ExperienceEvent(xdm: xdmData, datastreamIdOverride: "SampleDatastreamId")

Edge.sendEvent(experienceEvent: experienceEvent) { (handles: [EdgeEventHandle]) in
  // Handle the Edge Network response
}
```

>[!TAB Android (Kotlin)]

Este ejemplo muestra el aspecto de la anulación de ID de un conjunto de datos en un SDK móvil [!DNL Android] integración.

```kotlin
// Create experience event from Map
val xdmData = mutableMapOf < String, Any > ()
xdmData["eventType"] = "SampleXDMEvent"
xdmData["sample"] = "data"

val experienceEvent = ExperienceEvent.Builder()
    .setXdmSchema(xdmData)
    .setDatastreamIdOverride("SampleDatastreamId")
    .build()

Edge.sendEvent(experienceEvent) {
    // Handle the Edge Network response
}
```

>[!ENDTABS]

### Anulación de configuración de flujo de datos mediante SDK móvil {#config-override-mobile}

Los ejemplos siguientes muestran el aspecto que podría tener una anulación de la configuración de un conjunto de datos en una integración de SDK móvil. Seleccione las pestañas a continuación para ver las [!DNL iOS] y [!DNL Android] ejemplos.

>[!BEGINTABS]

>[!TAB iOS (Swift)]

Este ejemplo muestra el aspecto de la anulación de la configuración de una secuencia de datos en un SDK móvil [!DNL iOS] integración.

```swift
// Create Experience event from dictionary
var xdmData: [String: Any] = [
  "eventType": "SampleXDMEvent",
  "sample": "data",
]

let configOverrides: [String: Any] = [
  "com_adobe_experience_platform": [
    "datasets": [
      "event": [
        "datasetId": "SampleEventDatasetIdOverride"
      ],
      "profile": [
        "datasetId": "SampleProfileDatasetIdOverride"
      ],
    ]
  ],
  "com_adobe_analytics": [
  "reportSuites": [
        "MyFirstOverrideReportSuite",
          "MySecondOverrideReportSuite",
          "MyThirdOverrideReportSuite"
      ]
  ],  
  "com_adobe_identity": [
    "idSyncContainerId": "1234567"
  ],
  "com_adobe_target": [
    "propertyToken": "63a46bbc-26cb-7cc3-def0-9ae1b51b6c62"
 ],
]

let experienceEvent = ExperienceEvent(xdm: xdmData, datastreamConfigOverride: configOverrides)

Edge.sendEvent(experienceEvent: experienceEvent) { (handles: [EdgeEventHandle]) in
  // Handle the Edge Network response
}
```

>[!TAB Android (Kotlin)]

Este ejemplo muestra el aspecto de la anulación de la configuración de una secuencia de datos en un SDK móvil [!DNL Android] integración.

```kotlin
// Create experience event from Map
val xdmData = mutableMapOf < String, Any > ()
xdmData["eventType"] = "SampleXDMEvent"
xdmData["sample"] = "data"

val configOverrides = mapOf(
    "com_adobe_experience_platform"
    to mapOf(
        "datasets"
        to mapOf(
            "event"
            to mapOf("datasetId"
                to "SampleEventDatasetIdOverride"),
            "profile"
            to mapOf("datasetId"
                to "SampleProfileDatasetIdOverride")
        )
    ),
    "com_adobe_analytics"
    to mapOf(
        "reportSuites"
        to listOf(
            "MyFirstOverrideReportSuite",
            "MySecondOverrideReportSuite",
            "MyThirdOverrideReportSuite"
        )
    ),
    "com_adobe_identity"
    to mapOf(
        "idSyncContainerId"
        to "1234567"
    ),
    "com_adobe_target"
    to mapOf(
        "propertyToken"
        to "63a46bbc-26cb-7cc3-def0-9ae1b51b6c62"
    )
)

val experienceEvent = ExperienceEvent.Builder()
    .setXdmSchema(xdmData)
    .setDatastreamConfigOverride(configOverrides)
    .build()

Edge.sendEvent(experienceEvent) {
    // Handle the Edge Network response
}
```

>[!ENDTABS]

## Ejemplo de carga útil {#payload-example}

Los ejemplos anteriores generan un [!DNL Edge Network] carga útil similar a la de abajo.

```json
{
  "meta": {
    "configOverrides": {
      "com_adobe_experience_platform": {
        "datasets": {
          "event": {
            "datasetId": "SampleProfileDatasetIdOverride"
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
  "events": [  ]
}
```
