---
title: Procesamiento de datos de consentimiento del cliente mediante Adobe Experience Platform Web SDK
description: Obtenga información sobre cómo integrar Adobe Experience Platform Web SDK para procesar datos de consentimiento de clientes en Adobe Experience Platform.
role: Developer
feature: Consent, Web SDK
exl-id: 3a53d908-fc61-452b-bec3-af519dfefa41
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1322'
ht-degree: 1%

---

# Integración de Experience Platform Web SDK para procesar los datos de consentimiento del cliente

Adobe Experience Platform Web SDK permite recuperar las señales de consentimiento del cliente generadas por las plataformas de administración de consentimiento (CMP) y enviarlas a Adobe Experience Platform siempre que se produzca un evento de cambio de consentimiento.

**SDK no interactúa con ninguna CMP predeterminada**. Depende de usted determinar cómo integrar SDK en su sitio web, detectar cambios de consentimiento en la CMP y llamar al comando correspondiente. En este documento se proporciona una guía general sobre cómo integrar CMP con Experience Platform Web SDK.

## Requisitos previos {#prerequisites}

Este tutorial supone que ya ha determinado cómo generar datos de consentimiento dentro de su CMP y que ha creado un conjunto de datos que contiene campos de consentimiento que se ajustan al estándar de Adobe o al estándar de transparencia y consentimiento (TCF) 2.0 de IAB. Si aún no ha creado este conjunto de datos, consulte los siguientes tutoriales antes de volver a esta guía:

* [Creación de un conjunto de datos con el estándar de Adobe](./adobe/dataset.md)
* [Creación de un conjunto de datos con el estándar TCF 2.0](./iab/dataset.md)

Esta guía sigue el flujo de trabajo para configurar SDK con la extensión de etiqueta en la interfaz de usuario de. Si no desea utilizar la extensión de y prefiere incrustar directamente la versión independiente de SDK en el sitio, consulte los siguientes documentos en lugar de esta guía:

* [Configuración de una secuencia de datos](/help/datastreams/overview.md)
* [Instalación de SDK](/help/web-sdk/install/overview.md)
* [Configuración de SDK para comandos de consentimiento](/help/web-sdk/commands/configure/defaultconsent.md)

Los pasos de instalación de esta guía requieren una comprensión práctica de las extensiones de etiquetas y de cómo se instalan en las aplicaciones web. Consulte la siguiente documentación para obtener más información:

* [Información general sobre etiquetas](/help/tags/home.md)
* [Guía de inicio rápido](/help/tags/quick-start/quick-start.md)
* [Información general sobre la publicación](/help/tags/ui/publishing/overview.md)

## Configuración de una secuencia de datos

Para que SDK envíe datos a Experience Platform, primero debe configurar una secuencia de datos. En la IU de recopilación de datos o en la IU de Experience Platform, seleccione **[!UICONTROL Flujos de datos]** en el panel de navegación izquierdo.

Después de crear una nueva secuencia de datos o seleccionar una existente para editarla, selecciona el botón de alternancia situado junto a **[!UICONTROL Adobe Experience Platform]**. A continuación, utilice los valores enumerados a continuación para completar el formulario.

![](../../images/governance-privacy-security/consent/adobe/sdk/edge-config.png)

| Campo de secuencia de datos | Valor |
| --- | --- |
| [!UICONTROL espacio aislado] | Nombre de la zona protegida [sandbox](../../../sandboxes/home.md) de Experience Platform que contiene la conexión de flujo continuo y los conjuntos de datos necesarios para configurar la secuencia de datos. |
| [!UICONTROL Conjunto de datos del evento] | Un conjunto de datos [!DNL XDM ExperienceEvent] que planea enviar datos de evento a mediante SDK. Aunque debe proporcionar un conjunto de datos de evento para crear un flujo de datos de Experience Platform, tenga en cuenta que los datos de consentimiento enviados mediante eventos no se respetan en los flujos de trabajo de aplicación descendentes. |
| [!UICONTROL Conjunto de datos del perfil] | El conjunto de datos habilitado para [!DNL Profile] con campos de consentimiento de cliente que creó [anteriormente](#prerequisites). |

Cuando termine, seleccione **[!UICONTROL Guardar]** en la parte inferior de la pantalla y siga las indicaciones adicionales para completar la configuración.

## Instalación y configuración de Experience Platform Web SDK

Una vez creada una secuencia de datos como se describe en la sección anterior, debe configurar la extensión de Experience Platform Web SDK que implementará finalmente en el sitio. Si no tiene la extensión de SDK instalada en la propiedad de etiquetas, seleccione **[!UICONTROL Extensiones]** en el panel de navegación izquierdo, seguido de la pestaña **[!UICONTROL Catálogo]**. A continuación, seleccione **[!UICONTROL Instalar]** en la extensión de Experience Platform SDK dentro de la lista de extensiones disponibles.

![](../../images/governance-privacy-security/consent/adobe/sdk/install.png)

Al configurar SDK, en **[!UICONTROL Configuraciones de Edge]**, seleccione la secuencia de datos que creó en el paso anterior.

![](../../images/governance-privacy-security/consent/adobe/sdk/config-sdk.png)

Seleccione **[!UICONTROL Guardar]** para instalar la extensión.

### Creación de un elemento de datos para establecer el consentimiento predeterminado

Con la extensión de SDK instalada, tiene la opción de crear un elemento de datos para representar el valor predeterminado del consentimiento de recopilación de datos (`collect.val`) para los usuarios. Esto puede resultar útil si desea tener diferentes valores predeterminados según el usuario, como `pending` para usuarios de la Unión Europea y `in` para usuarios de América del Norte.

En este caso de uso, puede implementar lo siguiente para establecer el consentimiento predeterminado en función de la región del usuario:

1. Determine la región del usuario en el servidor web.
1. Antes de la etiqueta `script` (código incrustado) en la página web, procese una etiqueta `script` independiente que establezca una variable `adobeDefaultConsent` basada en la región del usuario.
1. Configure un elemento de datos que utilice la variable de JavaScript `adobeDefaultConsent` y use este elemento de datos como el valor de consentimiento predeterminado para el usuario.

Si la región del usuario está determinada por una CMP, puede seguir estos pasos:

1. Controle el evento &quot;CMP loaded&quot; en la página.
1. En el controlador de eventos, establezca una variable `adobeDefaultConsent` basada en la región del usuario y, a continuación, cargue el script de la biblioteca de etiquetas mediante JavaScript.
1. Configure un elemento de datos que utilice la variable de JavaScript `adobeDefaultConsent` y use este elemento de datos como el valor de consentimiento predeterminado para el usuario.

Para crear un elemento de datos en la interfaz de usuario, seleccione **[!UICONTROL Elementos de datos]** en el panel de navegación izquierdo y, a continuación, seleccione **[!UICONTROL Agregar elemento de datos]** para ir al cuadro de diálogo de creación de elementos de datos.

Desde aquí, debe crear un elemento de datos de [!UICONTROL JavaScript Variable] basado en `adobeDefaultConsent`. Seleccione **[!UICONTROL Guardar]** cuando haya terminado.

![](../../images/governance-privacy-security/consent/adobe/sdk/data-element.png)

Una vez creado el elemento de datos, vuelva a la página de configuración de la extensión de Web SDK. En la sección [!UICONTROL Privacidad], seleccione **[!UICONTROL Proporcionado por el elemento de datos]** y utilice el cuadro de diálogo proporcionado para seleccionar el elemento de datos de consentimiento predeterminado que creó anteriormente.

![](../../images/governance-privacy-security/consent/adobe/sdk/default-consent.png)

### Implemente la extensión en el sitio web

Una vez que haya terminado de configurar la extensión, puede integrarla en su sitio web. Consulte la [guía de publicación](../../../tags/ui/publishing/overview.md) en la documentación de etiquetas para obtener información detallada sobre cómo implementar la compilación de biblioteca actualizada.

## Realizar comandos de cambio de consentimiento {#commands}

Una vez que haya integrado la extensión de SDK en su sitio web, puede empezar a utilizar el comando Experience Platform Web SDK `setConsent` para enviar datos de consentimiento a Experience Platform.

El comando `setConsent` realiza dos acciones:

1. Actualiza los atributos de perfil del usuario directamente en el almacén de perfiles. Esto no envía ningún dato al lago de datos.
1. Crea un [Evento de experiencia](../../../xdm/classes/experienceevent.md) que registra una cuenta con marca de tiempo del evento de cambio de consentimiento. Estos datos se envían directamente al lago de datos y se pueden utilizar para realizar un seguimiento de los cambios de preferencia de consentimiento a lo largo del tiempo.

### Cuándo llamar a `setConsent`

Hay dos escenarios en los que se debe llamar a `setConsent` en el sitio:

1. Cuando se carga el consentimiento en la página (es decir, en cada carga de página)
1. Como parte de un vínculo o detector de eventos CMP que detecta los cambios en la configuración de consentimiento

### `setConsent` sintaxis

El comando [`setConsent`](/help/web-sdk/commands/setconsent.md) espera un objeto de carga útil que contenga una sola propiedad de tipo matriz: `consent`. La matriz `consent` debe contener al menos un objeto que proporcione los campos de consentimiento requeridos para el estándar de Adobe.

Los campos de consentimiento requeridos para el estándar de Adobe se muestran en el siguiente ejemplo de llamada a `setConsent`:

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
        time: "YYYY-10-12T15:52:25+00:00"
      }
    }
  }]
});
```

| Propiedad de carga útil | Descripción |
| --- | --- |
| `standard` | El estándar de consentimiento que se está utilizando. Para el estándar de Adobe, este valor debe establecerse en `Adobe`. |
| `version` | Número de versión del estándar de consentimiento indicado en `standard`. Este valor debe establecerse en `2.0` para el procesamiento de consentimiento estándar de Adobe. |
| `value` | La información de consentimiento actualizada del cliente, proporcionada como un objeto XDM que se ajusta a la estructura de los campos de consentimiento del conjunto de datos habilitado para el perfil. |

>[!NOTE]
>
>Si está utilizando otros estándares de consentimiento junto con `Adobe` (como `IAB TCF`), puede agregar objetos adicionales a la matriz `consent` para cada estándar. Cada objeto debe contener los valores apropiados para `standard`, `version` y `value` para el estándar de consentimiento que representan.

El siguiente JavaScript proporciona un ejemplo de una función que administra los cambios de preferencias de consentimiento en un sitio web, que se puede utilizar como llamada de retorno en un detector de eventos o un vínculo CMP:

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

  // Pass the XDM object to the Experience Platform Web SDK
  alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "2.0",
      value: consentXDM
    }]
  });
});
```

## Gestión de respuestas de SDK

Todos los comandos [!DNL Experience Platform SDK] devuelven promesas que indican si la llamada se realizó correctamente o no. A continuación, puede utilizar estas respuestas para lógicas adicionales, como mostrar mensajes de confirmación al cliente. Consulte [Respuestas de comandos](/help/web-sdk/commands/command-responses.md) para obtener más información.

Una vez que haya realizado correctamente `setConsent` llamadas con SDK, puede usar el visor de perfiles en la interfaz de usuario de Experience Platform para comprobar si los datos están llegando al almacén de perfiles. Consulte la sección sobre [perfiles de exploración por identidad](../../../profile/ui/user-guide.md#browse-identity) para obtener más información.

## Pasos siguientes

Al seguir esta guía, ha configurado la extensión Experience Platform Web SDK para enviar datos de consentimiento a Experience Platform. Para obtener instrucciones sobre cómo probar la implementación, consulte la documentación del estándar de consentimiento que está implementando:

* [Adobe standard](./adobe/overview.md#test)
* [Estándar TCF 2.0](./iab/overview.md#test)
