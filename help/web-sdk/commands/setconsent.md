---
title: setConsent
description: Se utiliza en cada página para rastrear el consentimiento del usuario.
source-git-commit: 90493d179e620604337bda96cb3b7f5401ca4a81
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 1%

---

# setConsent

El `setConsent` indica al SDK web si debe enviar datos (inclusión), descartar datos (exclusión) o utilizar [`defaultConsent`](configure/defaultconsent.md) (consentimiento desconocido).

El SDK web admite los siguientes estándares:

* **[Adobe estándar](/help/landing/governance-privacy-security/consent/adobe/overview.md)**: Se admiten los estándares 1.0 y 2.0.
* **[Marco de transparencia y consentimiento IAB](/help/landing/governance-privacy-security/consent/iab/overview.md)**: Si utiliza este estándar, el Perfil del cliente en tiempo real del visitante se actualiza con la información de consentimiento si la implementación está configurada correctamente:
   1. El esquema de perfil individual XDM contiene el [Grupo de campos de consentimiento de IAB TCF 2.0](/help/xdm/field-groups/profile/iab.md).
   1. El esquema Experience Event contiene la variable [Grupo de campos de consentimiento de IAB TCF 2.0](/help/xdm/field-groups/event/iab.md).
   1. Incluya la información de consentimiento de la IAB en el evento [Objeto XDM](sendevent/xdm.md). El SDK web no incluye automáticamente la información de consentimiento al enviar datos de evento.

Después de utilizar este comando, el SDK web escribe las preferencias del usuario en una cookie. La próxima vez que el usuario cargue el sitio web en el explorador, el SDK recuperará estas preferencias persistentes para determinar si los eventos se pueden enviar al Adobe.

El Adobe recomienda almacenar todas las preferencias del cuadro de diálogo de consentimiento por separado del consentimiento del SDK web. El SDK web no ofrece una forma de recuperar el consentimiento. Para asegurarse de que las preferencias de usuario permanecen sincronizadas con el SDK, puede llamar a la función `setConsent` en cada carga de página. El SDK web solo realiza una llamada al servidor cuando cambia el consentimiento.

## Definición del consentimiento mediante la extensión de etiqueta del SDK web

La configuración del consentimiento se realiza como una acción dentro de una regla de la interfaz de etiquetas de recopilación de datos de Adobe Experience Platform.

1. Iniciar sesión en [experience.adobe.com](https://experience.adobe.com) usando sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Reglas]**, luego seleccione la regla que desee.
1. En [!UICONTROL Acciones], seleccione una acción existente o cree una acción.
1. Configure las variables [!UICONTROL Extensión] campo desplegable a **[!UICONTROL SDK web de Adobe Experience Platform]** y configure el [!UICONTROL Tipo de acción] hasta **[!UICONTROL Definir consentimiento]**.
1. Configure los campos deseados a la derecha, incluidos los siguientes **[!UICONTROL Standard]** y **[!UICONTROL Consentimiento general]**.
1. Clic **[!UICONTROL Conservar cambios]**, luego ejecute el flujo de trabajo de publicación.

Puede incluir varios objetos de consentimiento dentro de esta acción.

## Definir consentimiento mediante la biblioteca JavaScript del SDK web

Ejecute el `setConsent` al llamar a la instancia configurada del SDK web. Puede incluir los siguientes objetos en este comando:

* **`consent[]`**: una matriz de `consent` objetos. El objeto de consentimiento tiene un formato diferente en función del estándar y la versión que elija.
* **`identityMap`**: Objeto que controla cómo se genera un ECID y a qué ID está asociada la información de consentimiento. El Adobe recomienda incluir este objeto cuando `setConsent` se ejecuta antes que otros comandos, como [`sendEvent`](sendevent/overview.md).
* **`edgeConfigOverrides`**: Un objeto que contiene [anulaciones de configuración de secuencia de datos](datastream-overrides.md).

>[!BEGINTABS]

>[!TAB Adobe 2.0]

### Adobe 2.0 estándar `consent` objeto

* **`standard`**: el estándar de consentimiento que elija. Establezca esta propiedad como `"Adobe"` para el estándar Adobe 2.0.
* **`version`**: una cadena que representa la versión del estándar de consentimiento. Establezca esta propiedad como `"2.0"` para el estándar Adobe 2.0.
* **`value`**: Un objeto que contiene valores de consentimiento.
   * **`value.collect.val`**: el valor de consentimiento. Los valores válidos son `"y"` (adhesión) y `"n"` (exclusión).
   * **`value.metadata.time`**: Marca de tiempo en la que el usuario establece el valor de consentimiento.

```js
alloy("setConsent", {
  "consent": [{
    "standard": "Adobe",
    "version": "2.0",
    "value": {
      "collect": {
        "val": "y"
      },
      "metadata": {
        "time": "YYYY-03-17T15:48:42-07:00"
      }
    }
  }]
});
```

>[!TAB IAB TCF 2.0]

### Estándar IAB TCF 2.0 `consent` objeto

* **`standard`**: el estándar de consentimiento que elija. Establezca esta propiedad como `"IAB TCF"` para el estándar IAB TCF 2.0.
* **`version`**: una cadena que representa la versión del estándar de consentimiento. Establezca esta propiedad como `"2.0"` para el estándar IAB TCF 2.0.
* **`value`**: una cadena que contiene el valor de consentimiento.
* **`gdprApplies`**: Un booleano que determina si el RGPD se aplica a este valor de consentimiento. Su valor predeterminado es `true`.
* **`gdprContainsPersonalData`**: Un booleano que determina si los datos de evento asociados con este usuario contienen datos personales. Su valor predeterminado es `false`.

```js
alloy("setConsent", {
  consent: [{
    "standard": "IAB TCF",
    "version": "2.0",
    "value": "CO052l-O052l-DGAMBFRACBgAIBAAAAABIYgEawAQEagAAAA",
    "gdprApplies": true,
    "gdprContainsPersonalData": true
  }]
});
```

>[!TAB Adobe 1.0]

### Adobe 1.0 estándar `consent` objeto

* **`standard`**: el estándar de consentimiento que elija. Establezca esta propiedad como `"Adobe"` para la norma Adobe 1.0.
* **`version`**: una cadena que representa la versión del estándar de consentimiento. Establezca esta propiedad como `"1.0"` para la norma Adobe 1.0.
* **`value.general`**: el valor de consentimiento. Los valores válidos son `"in"` (adhesión) y `"out"` (exclusión).

```js
// Set consent using the Adobe 1.0 standard
alloy("setConsent", {
  "consent": [{
    "standard": "Adobe",
    "version": "1.0",
    "value": {
      "general": "in"
    }
  }]
});
```

>[!ENDTABS]
