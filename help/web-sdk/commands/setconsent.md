---
title: setConsent
description: Se utiliza en cada página para rastrear las preferencias de consentimiento de los usuarios.
exl-id: d01a6ef1-4fa7-4a60-a3a1-19568b4e0d23
source-git-commit: d3591053939147589dae24e1e4c20d53b1f87dd3
workflow-type: tm+mt
source-wordcount: '1372'
ht-degree: 2%

---


# `setConsent`

El `setConsent` indica al SDK web si debe enviar datos (inclusión), descartar datos (exclusión) o utilizar [`defaultConsent`](configure/defaultconsent.md) (consentimiento desconocido).

El SDK web admite los siguientes estándares:

* **[Adobe estándar](/help/landing/governance-privacy-security/consent/adobe/overview.md)**: Se admiten los estándares 1.0 y 2.0.
* **[Marco de transparencia y consentimiento IAB](/help/landing/governance-privacy-security/consent/iab/overview.md)**: Si utiliza este estándar, el Perfil del cliente en tiempo real del visitante se actualiza con la información de consentimiento si la implementación está configurada correctamente:
   1. El esquema de perfil individual XDM contiene el [Grupo de campos de consentimiento de IAB TCF 2.0](/help/xdm/field-groups/profile/iab.md).
   1. El esquema Experience Event contiene la variable [Grupo de campos de consentimiento de IAB TCF 2.0](/help/xdm/field-groups/event/iab.md).
   1. Incluya la información de consentimiento de la IAB en el evento [Objeto XDM](sendevent/xdm.md). El SDK web no incluye automáticamente la información de consentimiento al enviar datos de evento.

Después de utilizar este comando, el SDK web escribe las preferencias del usuario en una cookie. La próxima vez que el usuario cargue el sitio web en el explorador, el SDK recuperará estas preferencias persistentes para determinar si los eventos se pueden enviar al Adobe.

El Adobe recomienda almacenar todas las preferencias del cuadro de diálogo de consentimiento por separado del consentimiento del SDK web. El SDK web no ofrece una forma de recuperar el consentimiento. Para asegurarse de que las preferencias de usuario permanecen sincronizadas con el SDK, puede llamar a la función `setConsent` en cada carga de página. El SDK web solo realiza una llamada al servidor cuando cambia el consentimiento.

## Uso de `defaultConsent` junto con `setConsent` {#using-consent}

El SDK web ofrece dos comandos de configuración de consentimiento complementarios:

* [`defaultConsent`](configure/defaultconsent.md): este comando está diseñado para capturar las preferencias de consentimiento de los clientes de Adobe que utilizan el SDK web.
* [`setConsent`](setconsent.md): este comando está diseñado para capturar las preferencias de consentimiento de los visitantes del sitio.

Cuando se utilizan juntos, esta configuración puede llevar a diferentes resultados de recopilación de datos y configuración de cookies, según sus valores configurados.

Consulte la tabla siguiente para comprender cuándo se produce la recopilación de datos y cuándo se configuran las cookies, según la configuración de consentimiento.

| defaultConsent | setConsent | Se produce la recopilación de datos | El SDK web establece cookies de explorador |
|---------|----------|---------|---------|
| `in` | `in` | Sí | Sí |
| `in` | `out` | No | Sí |
| `in` | Sin configurar | Sí | Sí |
| `pending` | `in` | Sí | Sí |
| `pending` | `out` | No | Sí |
| `pending` | Sin configurar | No | No |
| `out` | `in` | Sí | Sí |
| `out` | `out` | No | Sí |
| `out` | Sin configurar | No | No |

Las siguientes cookies se establecen cuando la configuración de consentimiento lo permite:

| Nombre | Edad máxima | Descripción |
|---|---|---|
| **AMCV_###@AdobeOrg** | 34128000 (395 días) | Presente cuando [`idMigrationEnabled`](configure/idmigrationenabled.md) está activada. Ayuda al realizar la transición al SDK web mientras algunas partes del sitio aún utilizan `visitor.js`. |
| **Cookie Demdex** | 15552000 (180 días) | Presente si la sincronización de ID está habilitada. El Audience Manager establece esta cookie para asignar un ID único a un visitante del sitio. La cookie demdex ayuda a Audience Manager a realizar diversas funciones básicas, como la identificación del visitante, la sincronización de ID, la segmentación, el modelado, la creación de informes, etc. |
| **kndctr_orgid_cluster** | 1800 (30 minutos) | Almacena la región del Edge Network que sirve las solicitudes del usuario actual. La región se utiliza en la ruta URL para que el Edge Network pueda enrutar la solicitud a la región correcta. Si un usuario se conecta con una dirección IP diferente o en una sesión diferente, la solicitud se vuelve a dirigir a la región más cercana. |
| **kndct_orgid_identity** | 34128000 (395 días) | Almacena el ECID, así como otra información relacionada con el ECID. |
| **kndctr_orgid_permission** | 15552000 (180 días) | Almacena la preferencia de consentimiento de los usuarios para el sitio web. |
| **s_ecid** | 63115200 (2 años) | Contiene una copia del ID de Experience Cloud ([!DNL ECID]) o MID. El MID se almacena en un par de clave-valor que sigue esta sintaxis, `s_ecid=MCMID\|<ECID>`. |

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

* **`consent[]`**: una matriz de `consent` objetos. El objeto de consentimiento tiene un formato diferente en función del estándar y la versión que elija. Consulte las pestañas siguientes para ver ejemplos de cada objeto de consentimiento, según el estándar de consentimiento.
* **`identityMap`**: Objeto que controla cómo se genera un ECID y a qué ID está asociada la información de consentimiento. El Adobe recomienda incluir este objeto cuando `setConsent` se ejecuta antes que otros comandos, como [`sendEvent`](sendevent/overview.md).
* **`edgeConfigOverrides`**: Un objeto que contiene [anulaciones de configuración de secuencia de datos](datastream-overrides.md).

>[!BEGINTABS]

>[!TAB Adobe 2.0]

### Adobe 2.0 estándar `consent` objeto

Si utiliza Adobe Experience Platform, deberá incluir un grupo de campos de esquema de privacidad en el esquema de perfil. Consulte [Gobernanza, privacidad y seguridad en Adobe Experience Platform](../../landing/governance-privacy-security/overview.md) para obtener más información sobre el estándar Adobe 2.0. Puede agregar datos dentro del objeto de valor siguiente correspondiente al esquema del `consents` del campo [!UICONTROL Consentimientos y preferencias] grupo de campos de perfil.

* **`standard`**: el estándar de consentimiento que elija. Establezca esta propiedad como `"Adobe"` para el estándar Adobe 2.0.
* **`version`**: una cadena que representa la versión del estándar de consentimiento. Establezca esta propiedad como `"2.0"` para el estándar Adobe 2.0.
* **`value`**: Un objeto que contiene valores de consentimiento.
   * **`value.collect.val`**: el valor de consentimiento. Configure esto como `"y"` cuando los usuarios se incluyan y a `"n"` cuando los usuarios se excluyen.
   * **`value.metadata.time`**: Marca de tiempo en la que los usuarios actualizaron su configuración de consentimiento por última vez.

```js
// Set consent using the Adobe 2.0 standard
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

Para registrar las preferencias de consentimiento del usuario proporcionadas a través del estándar del marco de transparencia y consentimiento (TCF) de Interactive Advertising Bureau Europe (IAB), establezca la cadena de consentimiento como se muestra a continuación.

Cuando el consentimiento se establece de esta manera, el Perfil del cliente en tiempo real se actualiza con la información de consentimiento. Para que esto funcione, el esquema XDM de perfil debe contener la variable [Grupo de campos del esquema de privacidad de perfil](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-privacy.schema.md). Al enviar eventos, la información de consentimiento de IAB debe añadirse manualmente al objeto XDM de evento. El SDK web no incluye automáticamente la información de consentimiento en los eventos.

Para enviar la información de consentimiento en eventos, debe agregar el grupo de campos Privacidad de Experience Event a su [!DNL Profile]-enabled [!DNL XDM ExperienceEvent] esquema. Consulte la sección sobre [actualización del esquema de ExperienceEvent](../../landing/governance-privacy-security/consent/iab/dataset.md#event-schema) en la guía de preparación del conjunto de datos para ver los pasos sobre cómo configurarlo.

* **`standard`**: el estándar de consentimiento que elija. Establezca esta propiedad como `"IAB TCF"` para el estándar IAB TCF 2.0.
* **`version`**: una cadena que representa la versión del estándar de consentimiento. Establezca esta propiedad como `"2.0"` para el estándar IAB TCF 2.0.
* **`value`**: una cadena que contiene el valor de consentimiento.
* **`gdprApplies`**: Un booleano que determina si el RGPD se aplica a este valor de consentimiento. Su valor predeterminado es `true`.
* **`gdprContainsPersonalData`**: Un booleano que determina si los datos de evento asociados con este usuario contienen datos personales. Su valor predeterminado es `false`.

```js
// Set consent using the IAB TCF 2.0 standard
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
* **`value.general`**: el valor de consentimiento. Configure esto como `"in"` cuando los usuarios se incluyan y a `"out"` cuando los usuarios se excluyen.

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

### Envío de varios estándares en una solicitud {#multiple-standards}

El SDK web también admite el envío de más de un objeto de consentimiento en una solicitud, como se muestra en el ejemplo siguiente.

```js
alloy("setConsent", {
    consent: [{
        standard: "Adobe",
        version: "2.0",
        value: {
            collect: {
                val: "y"
            },
            metadata: {
                time: "2021-03-17T15:48:42-07:00"
            }
        }
    }, {
        standard: "IAB TCF",
        version: "2.0",
        value: "CO1Z4yuO1Z4yuAcABBENArCsAP_AAH_AACiQGCNX_T5eb2vj-3Zdt_tkaYwf55y3o-wzhhaIse8NwIeH7BoGP2MwvBX4JiQCGBAkkiKBAQdtHGhcCQABgIhRiTKMYk2MjzNKJLJAilsbe0NYCD9mnsHT3ZCY70--u__7P3fAwQgkwVLwCRIWwgJJs0ohTABCOICpBwCUEIQEClhoACAnYFAR6gAAAIDAACAAAAEEEBAIABAAAkIgAAAEBAKACIBAACAEaAhAARIEAsAJEgCAAVA0JACKIIQBCDgwCjlACAoAAAAA.YAAAAAAAAAAA",
        gdprApplies: true
    }]
});
```


## Persistencia de las preferencias de consentimiento {#persistence}

Después de haber comunicado las preferencias de usuario al SDK web mediante la variable `setConsent` , el SDK mantiene las preferencias de usuario en una cookie. La próxima vez que el usuario cargue el sitio web en el explorador, el SDK web recuperará y utilizará estas preferencias persistentes para determinar si se pueden enviar o no eventos al Adobe.

Deberá almacenar las preferencias de usuario de forma independiente para poder mostrar el cuadro de diálogo de consentimiento con las preferencias actuales. No hay forma de recuperar las preferencias de usuario del SDK web. Para asegurarse de que las preferencias de usuario permanecen sincronizadas con el SDK, puede llamar a la función `setConsent` en cada carga de página. El SDK web solo realiza una llamada al servidor si las preferencias han cambiado.

## Sincronización de identidades al establecer el consentimiento {#sync-identities}

Cuando el consentimiento predeterminado (configurado a través de la variable [defaultConsent](configure/defaultconsent.md) parameter) se establece en `pending` o `out`, el `setConsent` la configuración puede ser la primera solicitud que se emite y establece la identidad. Debido a esto, puede ser importante sincronizar identidades en la primera solicitud. Puede añadir el mapa de identidad a `setConsent` comando igual que en el `sendEvent` comando. Consulte [uso de identityMap](../identity/overview.md#using-identitymap) para ver un ejemplo de cómo incluir el mapa de identidad en el comando.
