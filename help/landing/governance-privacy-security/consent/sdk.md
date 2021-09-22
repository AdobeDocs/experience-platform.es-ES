---
title: Procesamiento de datos de consentimiento del cliente mediante el SDK web de Adobe Experience Platform
topic-legacy: getting started
description: Obtenga información sobre cómo integrar el SDK web de Adobe Experience Platform para procesar datos de consentimiento del cliente en Adobe Experience Platform.
exl-id: 3a53d908-fc61-452b-bec3-af519dfefa41
source-git-commit: 69e510c9a0f477ad7cab530128c6728f68dfdab1
workflow-type: tm+mt
source-wordcount: '1330'
ht-degree: 1%

---

# Integración del SDK web de Platform para el procesamiento de los datos de consentimiento del cliente

El SDK web de Adobe Experience Platform le permite recuperar las señales de consentimiento del cliente generadas por las plataformas de administración de consentimiento (CMP) y enviarlas a Adobe Experience Platform siempre que se produzca un evento de cambio de consentimiento.

**El SDK no interactúa con ninguna CMP lista para usar**. Depende de usted determinar cómo integrar el SDK en su sitio web, detectar cambios de consentimiento en el CMP y llamar al comando correspondiente. Este documento proporciona instrucciones generales sobre cómo integrar su CMP con el SDK web de Platform.

## Requisitos previos {#prerequisites}

Este tutorial supone que ya ha determinado cómo generar datos de consentimiento dentro de su CMP y ha creado un conjunto de datos que contiene campos de consentimiento que se ajustan al estándar de Adobe o al marco de transparencia y consentimiento IAB (TCF) 2.0 . Si aún no ha creado este conjunto de datos, consulte los siguientes tutoriales antes de volver a esta guía:

* [Creación de un conjunto de datos mediante el estándar de Adobe](./adobe/dataset.md)
* [Crear un conjunto de datos con el estándar TCF 2.0](./iab/dataset.md)

Esta guía sigue el flujo de trabajo para configurar el SDK mediante la extensión de etiqueta en la interfaz de usuario de la recopilación de datos. Si no desea utilizar la extensión y prefiere incrustar directamente la versión independiente del SDK en su sitio, consulte los siguientes documentos en lugar de esta guía:

* [Configurar un conjunto de datos](../../../edge/fundamentals/datastreams.md)
* [Instalación del SDK](../../../edge/fundamentals/installing-the-sdk.md)
* [Configuración del SDK para los comandos de consentimiento](../../../edge/consent/supporting-consent.md)

Los pasos de instalación de esta guía requieren comprender bien las extensiones de etiquetas y cómo se instalan en las aplicaciones web. Consulte la siguiente documentación para obtener más información:

* [Información general sobre etiquetas](../../../tags/home.md)
* [Guía de inicio rápido](../../../tags/quick-start/quick-start.md)
* [Información general sobre la publicación](../../../tags/ui/publishing/overview.md)

## Configurar un conjunto de datos

Para que el SDK envíe datos al Experience Platform, primero debe configurar un conjunto de datos. En la interfaz de usuario de la recopilación de datos, seleccione **[!UICONTROL Datastreams]** en el panel de navegación izquierdo.

Después de crear un nuevo conjunto de datos o de seleccionar uno existente para editarlo, seleccione el botón de alternancia situado junto a **[!UICONTROL Adobe Experience Platform]**. A continuación, utilice los valores que se indican a continuación para completar el formulario.

![](../../images/governance-privacy-security/consent/adobe/sdk/edge-config.png)

| Campo Datastream | Valor |
| --- | --- |
| [!UICONTROL Entorno de pruebas] | Nombre de la plataforma [sandbox](../../../sandboxes/home.md) que contiene la conexión de flujo continuo necesaria y los conjuntos de datos para configurar el conjunto de datos. |
| [!UICONTROL Entrada de flujo continuo] | Conexión de flujo continuo válida para el Experience Platform. Consulte el tutorial sobre la [creación de una conexión de flujo continuo](../../../ingestion/tutorials/create-streaming-connection-ui.md) si no tiene una entrada de flujo continuo existente. |
| [!UICONTROL Conjunto de datos del evento] | Conjunto de datos [!DNL XDM ExperienceEvent] que planea usar para enviar datos de evento a mediante el SDK. Aunque es necesario que proporcione un conjunto de datos de evento para crear un conjunto de datos de Platform, tenga en cuenta que los datos de consentimiento enviados mediante eventos no se respetan en los flujos de trabajo de aplicación descendentes. |
| [!UICONTROL Conjunto de datos de perfil] | El conjunto de datos [!DNL Profile] habilitado con campos de consentimiento del cliente que ha creado [anteriormente](#prerequisites). |

Cuando termine, seleccione **[!UICONTROL Save]** en la parte inferior de la pantalla y continúe siguiendo las indicaciones adicionales para completar la configuración.

## Instalación y configuración del SDK web de Platform

Una vez creado un conjunto de datos como se describe en la sección anterior, debe configurar la extensión del SDK web de plataforma que implementará en su sitio. Si no tiene la extensión SDK instalada en la propiedad tag, seleccione **[!UICONTROL Extensions]** en el panel de navegación izquierdo, seguido de la pestaña **[!UICONTROL Catalog]**. A continuación, seleccione **[!UICONTROL Install]** en la extensión del SDK de plataforma dentro de la lista de extensiones disponibles.

![](../../images/governance-privacy-security/consent/adobe/sdk/install.png)

Al configurar el SDK, en **[!UICONTROL Edge Configurations]**, seleccione el conjunto de datos que creó en el paso anterior.

![](../../images/governance-privacy-security/consent/adobe/sdk/config-sdk.png)

Seleccione **[!UICONTROL Save]** para instalar la extensión.

### Crear un elemento de datos para establecer el consentimiento predeterminado

Con la extensión de SDK instalada, tiene la opción de crear un elemento de datos para representar el valor de consentimiento de recopilación de datos predeterminado (`collect.val`) para sus usuarios. Esto puede resultar útil si desea tener diferentes valores predeterminados en función del usuario, como `pending` para usuarios de la Unión Europea y `in` para usuarios de América del Norte.

En este caso de uso, puede implementar lo siguiente para establecer el consentimiento predeterminado en función de la región del usuario:

1. Determine la región del usuario en el servidor web.
1. Antes de la etiqueta `script` (código incrustado) en la página web, renderice una etiqueta `script` independiente que establezca una variable `adobeDefaultConsent` basada en la región del usuario.
1. Configure un elemento de datos que utilice la variable JavaScript `adobeDefaultConsent` y utilice este elemento de datos como valor de consentimiento predeterminado para el usuario.

Si la región del usuario está determinada por una CMP, puede realizar los siguientes pasos:

1. Gestione el evento &quot;CMP loaded&quot; en la página.
1. En el controlador de eventos, establezca una variable `adobeDefaultConsent` basada en la región del usuario y, a continuación, cargue el script de la biblioteca de etiquetas mediante JavaScript.
1. Configure un elemento de datos que utilice la variable JavaScript `adobeDefaultConsent` y utilice este elemento de datos como valor de consentimiento predeterminado para el usuario.

Para crear un elemento de datos en la interfaz de usuario de la recopilación de datos, seleccione **[!UICONTROL Elementos de datos]** en el panel de navegación izquierdo y, a continuación, seleccione **[!UICONTROL Agregar elemento de datos]** para navegar hasta el cuadro de diálogo de creación de elementos de datos.

A partir de aquí, debe crear un elemento de datos [!UICONTROL Variable JavaScript] basado en `adobeDefaultConsent`. Seleccione **[!UICONTROL Guardar]** cuando haya terminado.

![](../../images/governance-privacy-security/consent/adobe/sdk/data-element.png)

Una vez creado el elemento de datos, vuelva a la página de configuración de la extensión del SDK web. En la sección [!UICONTROL Privacy], seleccione **[!UICONTROL Proporcionado por el elemento de datos]** y utilice el cuadro de diálogo proporcionado para seleccionar el elemento de datos de consentimiento predeterminado que creó anteriormente.

![](../../images/governance-privacy-security/consent/adobe/sdk/default-consent.png)

### Implementar la extensión en el sitio web

Una vez que haya terminado de configurar la extensión, esta se puede integrar en el sitio web. Consulte la [guía de publicación](../../../tags/ui/publishing/overview.md) en la documentación de etiquetas para obtener información detallada sobre cómo implementar la compilación de biblioteca actualizada.

## Creación de comandos de cambio de consentimiento {#commands}

Una vez que haya integrado la extensión de SDK en su sitio web, puede empezar a utilizar el comando Platform Web SDK `setConsent` para enviar datos de consentimiento a Platform.

>[!IMPORTANT]
>
>El comando `setConsent` solo actualiza los datos directamente en el almacén de perfiles y no envía ningún dato al lago de datos.

Hay dos escenarios en los que se debe llamar a `setConsent` en el sitio:

1. Cuando se carga el consentimiento en la página (es decir, en cada carga de página)
1. Como parte de un enlace CMP o un detector de eventos que detecta cambios en la configuración del consentimiento

>[!NOTE]
>
>Para obtener una introducción a la sintaxis común de los comandos del SDK de Platform, consulte el documento sobre [ejecución de comandos](../../../edge/fundamentals/executing-commands.md).

El comando `setConsent` espera dos argumentos:

1. Una cadena que indica el tipo de comando (en este caso, `"setConsent"`)
1. Objeto de carga útil que contiene una única propiedad de tipo matriz: `consent`. La matriz `consent` debe contener al menos un objeto que proporcione los campos de consentimiento necesarios para el estándar de Adobe.

Los campos de consentimiento requeridos para el estándar de Adobe se muestran en el siguiente ejemplo de llamada `setConsent`:

```js
alloy("setConsent", {
  consent: [{
    standard: "Adobe",
    version: "2.0",
    value: {
      collect: {
        val: "y"
      },
      share: {
        val: "y"
      },
      personalize: {
        content: {
          val: "y"
        }
      },
      metadata: {
        time: "2020-10-12T15:52:25+00:00"
      }
    }
  }]
});
```

| Propiedad Payload | Descripción |
| --- | --- |
| `standard` | El estándar de consentimiento que se está utilizando. Para el estándar de Adobe, este valor debe establecerse en `Adobe`. |
| `version` | Número de versión del estándar de consentimiento indicado en `standard`. Este valor debe establecerse en `2.0` para el procesamiento de consentimiento estándar de Adobe. |
| `value` | La información de consentimiento actualizada del cliente, proporcionada como un objeto XDM que se ajusta a la estructura de los campos de consentimiento del conjunto de datos con perfil habilitado. |

>[!NOTE]
>
>Si está utilizando otros estándares de consentimiento junto con `Adobe` (como `IAB TCF`), puede agregar objetos adicionales a la matriz `consent` para cada estándar. Cada objeto debe contener valores adecuados para `standard`, `version` y `value` para el estándar de consentimiento que representan.

El siguiente JavaScript proporciona un ejemplo de una función que gestiona los cambios de preferencias de consentimiento en un sitio web, que puede utilizarse como una rellamada en un detector de eventos o un vínculo CMP:

```js
var setConsent = function () {

  // Retrieve the current consent data.
  var categories = getConsentData();

  // If the script is running on a consent change, generate a new timestamp.
  // If the script is running on page load, set the timestamp to when the consent values last changed.
  var now = new Date();
  var collectedAt = consentChanged ? now.toISOString() : categories.collectedAt;

  //  Map the consent values and timestamp to XDM
  var consentXDM = {
    collect: {
      val: categories.collect !== -1 ? "y" : "n"
    },
    personalize: {
      content: {
        val: categories.personalizeContent !== -1 ? "y" : "n"
      }
    },
    share: {
      val: categories.share !== -1 ? "y" : "n"
    },
    metadata: {
      time: collectedAt
    }
  };

  // Pass the XDM object to the Platform Web SDK
  alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "2.0",
      value: consentXDM
    }]
  });
});
```

## Gestión de respuestas del SDK

Todos los comandos [!DNL Platform SDK] devuelven promesas que indican si la llamada se ha realizado correctamente o no. A continuación, puede utilizar estas respuestas para lógica adicional, como mostrar mensajes de confirmación al cliente. Consulte la sección sobre [gestión correcta o falla](../../../edge/fundamentals/executing-commands.md#handling-success-or-failure) en la guía sobre la ejecución de comandos del SDK para ver ejemplos específicos.

Una vez que haya realizado correctamente `setConsent` llamadas con el SDK, puede utilizar el visor de perfiles en la interfaz de usuario de Platform para verificar si los datos están aterrizando en el almacén de perfiles. Consulte la sección sobre [navegación por perfiles por identidad](../../../profile/ui/user-guide.md#browse-identity) para obtener más información.

## Pasos siguientes

Al seguir esta guía, ha configurado la extensión del SDK web de Platform para enviar datos de consentimiento al Experience Platform. Para obtener instrucciones sobre cómo probar la implementación, consulte la documentación del estándar de consentimiento que está implementando:

* [Adobe estándar](./adobe/overview.md#test)
* [Estándar TCF 2.0](./iab/overview.md#test)
