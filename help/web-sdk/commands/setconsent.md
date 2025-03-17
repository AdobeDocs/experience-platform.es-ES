---
title: setConsent
description: Se utiliza en cada página para rastrear las preferencias de consentimiento de los usuarios.
exl-id: d01a6ef1-4fa7-4a60-a3a1-19568b4e0d23
source-git-commit: 83b4745693749c5f50791d6efeb3a7ba02a4cce5
workflow-type: tm+mt
source-wordcount: '1330'
ht-degree: 3%

---


# `setConsent`

El comando `setConsent` indica a Web SDK si debe enviar datos (adhesión), descartar datos (exclusión) o utilizar [`defaultConsent`](configure/defaultconsent.md) (consentimiento desconocido).

Web SDK admite los siguientes estándares:

* **[estándar Adobe](/help/landing/governance-privacy-security/consent/adobe/overview.md)**: Se admiten los estándares 1.0 y 2.0.
* **[Marco de transparencia y consentimiento IAB](/help/landing/governance-privacy-security/consent/iab/overview.md)**: Si usa este estándar, el Perfil del cliente en tiempo real del visitante se actualiza con la información de consentimiento si la implementación está configurada correctamente:
   1. El esquema de perfil individual de XDM contiene el [grupo de campos de consentimiento TCF de IAB 2.0](/help/xdm/field-groups/profile/iab.md).
   1. El esquema Experience Event contiene el [grupo de campos de consentimiento TCF 2.0 de IAB](/help/xdm/field-groups/event/iab.md).
   1. Incluya la información de consentimiento de IAB en el evento [objeto XDM](sendevent/xdm.md). Web SDK no incluye automáticamente la información de consentimiento al enviar datos de evento.

Después de utilizar este comando, Web SDK escribe las preferencias del usuario en una cookie. La próxima vez que el usuario cargue el sitio web en el explorador, SDK recuperará estas preferencias persistentes para determinar si los eventos se pueden enviar a Adobe.

Adobe recomienda almacenar todas las preferencias del cuadro de diálogo de consentimiento por separado del consentimiento de Web SDK. Web SDK no ofrece una forma de obtener el consentimiento. Para asegurarse de que las preferencias del usuario permanecen sincronizadas con SDK, puede llamar al comando `setConsent` en cada carga de página. Web SDK solo realiza una llamada al servidor cuando cambia el consentimiento.

## Consideraciones de sincronización de identidad {#identity-considerations}

El comando `setConsent` solo usa `ECID` del mapa de identidad, ya que el comando funciona en el nivel de dispositivo. El comando `setConsent` no tiene en cuenta otras identidades del mapa de identidad.

## Usando `defaultConsent` junto con `setConsent` {#using-consent}

Web SDK ofrece dos comandos de configuración de consentimiento complementarios:

* [`defaultConsent`](configure/defaultconsent.md): este comando está diseñado para capturar las preferencias de consentimiento de los clientes de Adobe que utilizan Web SDK.
* [`setConsent`](setconsent.md): este comando está diseñado para capturar las preferencias de consentimiento de los visitantes del sitio.

Cuando se utilizan juntos, esta configuración puede llevar a diferentes resultados de recopilación de datos y configuración de cookies, según sus valores configurados.

Consulte la tabla siguiente para comprender cuándo se produce la recopilación de datos y cuándo se configuran las cookies, según la configuración de consentimiento.

| defaultConsent | setConsent | Se produce la recopilación de datos | Web SDK establece cookies de explorador |
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
| **AMCV_###@AdobeOrg** | 34128000 (395 días) | Presente cuando [`idMigrationEnabled`](configure/idmigrationenabled.md) está habilitado. Ayuda al realizar la transición a Web SDK mientras algunas partes del sitio siguen utilizando `visitor.js`. |
| **Cookie Demdex** | 15552000 (180 días) | Presente si la sincronización de ID está habilitada. Audience Manager establece esta cookie para asignar un ID único a un visitante del sitio. La cookie demdex ayuda a Audience Manager a realizar diversas funciones básicas, como la identificación del visitante, la sincronización de ID, la segmentación, el modelado, la creación de informes, etc. |
| **kndctr_orgid_cluster** | 1800 (30 minutos) | Almacena la región de Edge Network que sirve las solicitudes del usuario actual. La región se utiliza en la ruta URL para que Edge Network pueda enrutar la solicitud a la región correcta. Si un usuario se conecta con una dirección IP diferente o en una sesión diferente, la solicitud se vuelve a dirigir a la región más cercana. |
| **kndct_orgid_identity** | 34128000 (395 días) | Almacena el ECID, así como otra información relacionada con el ECID. |
| **kndctr_orgid_permission** | 15552000 (180 días) | Almacena la preferencia de consentimiento de los usuarios para el sitio web. |
| **s_ecid** | 63115200 (2 años) | Contiene una copia del Experience Cloud ID ([!DNL ECID]) o MID. El MID se almacena en un par de clave-valor que sigue esta sintaxis, `s_ecid=MCMID\|<ECID>`. |

## Definición del consentimiento mediante la extensión de etiqueta Web SDK

La configuración del consentimiento se realiza como una acción dentro de una regla de la interfaz de etiquetas de recopilación de datos de Adobe Experience Platform.

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Reglas]** y luego seleccione la regla que desee.
1. En [!UICONTROL Acciones], seleccione una acción existente o cree una acción.
1. Establezca el campo desplegable [!UICONTROL Extension] en **[!UICONTROL Adobe Experience Platform Web SDK]** y establezca [!UICONTROL Action Type] en **[!UICONTROL Set permission]**.
1. Establece los campos deseados a la derecha, incluidos **[!UICONTROL Estándar]** y **[!UICONTROL Consentimiento general]**.
1. Haga clic en **[!UICONTROL Conservar cambios]** y, a continuación, ejecute el flujo de trabajo de publicación.

Puede incluir varios objetos de consentimiento dentro de esta acción.

## Definir el consentimiento mediante la biblioteca JavaScript de Web SDK

Ejecute el comando `setConsent` al llamar a la instancia configurada de Web SDK. Puede incluir los siguientes objetos en este comando:

* **`consent[]`**: una matriz de `consent` objetos. El objeto de consentimiento tiene un formato diferente en función del estándar y la versión que elija. Consulte las pestañas siguientes para ver ejemplos de cada objeto de consentimiento, según el estándar de consentimiento.
* **`identityMap`**: un objeto que controla cómo se genera un ECID y a qué ID está asociada la información de consentimiento. Adobe recomienda incluir este objeto cuando `setConsent` se ejecute antes que otros comandos, como [`sendEvent`](sendevent/overview.md).
* **`edgeConfigOverrides`**: un objeto que contiene [anulaciones de configuración de secuencia de datos](datastream-overrides.md).

>[!BEGINTABS]

>[!TAB Adobe 2.0]

### Objeto `consent` estándar de Adobe 2.0

Si utiliza Adobe Experience Platform, deberá incluir un grupo de campos de esquema de privacidad en el esquema de perfil. Consulte [Gobernanza, privacidad y seguridad en Adobe Experience Platform](../../landing/governance-privacy-security/overview.md) para obtener más información sobre el estándar Adobe 2.0. Puede agregar datos dentro del objeto de valor siguiente correspondiente al esquema del campo `consents` del grupo de campos de perfil [!UICONTROL Consentimientos y preferencias].

* **`standard`**: el estándar de consentimiento que elija. Establezca esta propiedad en `"Adobe"` para el estándar Adobe 2.0.
* **`version`**: cadena que representa la versión del estándar de consentimiento. Establezca esta propiedad en `"2.0"` para el estándar Adobe 2.0.
* **`value`**: un objeto que contiene valores de consentimiento.
   * **`value.collect.val`**: el valor de consentimiento. Establezca esto en `"y"` cuando los usuarios acepten la inclusión y en `"n"` cuando los usuarios acepten la exclusión.
   * **`value.metadata.time`**: marca de tiempo de la última vez que los usuarios actualizaron su configuración de consentimiento.

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

### Objeto `consent` estándar de IAB TCF 2.0

Para registrar las preferencias de consentimiento del usuario proporcionadas mediante el estándar del marco de transparencia y consentimiento (TCF) de Advertising Bureau Europe (IAB) interactivo, establezca la cadena de consentimiento como se muestra a continuación.

Cuando el consentimiento se establece de esta manera, el Perfil del cliente en tiempo real se actualiza con la información de consentimiento. Para que esto funcione, el esquema XDM de perfil debe contener el [grupo de campos del esquema de privacidad del perfil](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-privacy.schema.md). Al enviar eventos, la información de consentimiento de IAB debe añadirse manualmente al objeto XDM de evento. Web SDK no incluye automáticamente la información de consentimiento en los eventos.

Para enviar la información de consentimiento en eventos, debe agregar el grupo de campos Privacidad de Experience Event al esquema [!DNL XDM ExperienceEvent] habilitado para [!DNL Profile]. Consulte la sección sobre [actualización del esquema de ExperienceEvent](../../landing/governance-privacy-security/consent/iab/dataset.md#event-schema) en la guía de preparación de conjuntos de datos para ver los pasos sobre cómo configurarlo.

* **`standard`**: el estándar de consentimiento que elija. Establezca esta propiedad en `"IAB TCF"` para el estándar IAB TCF 2.0.
* **`version`**: cadena que representa la versión del estándar de consentimiento. Establezca esta propiedad en `"2.0"` para el estándar IAB TCF 2.0.
* **`value`**: cadena que contiene el valor de consentimiento.
* **`gdprApplies`**: Un booleano que determina si el RGPD se aplica a este valor de consentimiento. Su valor predeterminado es `true`.
* **`gdprContainsPersonalData`**: un booleano que determina si los datos de evento asociados con este usuario contienen datos personales. Su valor predeterminado es `false`.

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

### Objeto `consent` estándar de Adobe 1.0

* **`standard`**: el estándar de consentimiento que elija. Establezca esta propiedad en `"Adobe"` para el estándar Adobe 1.0.
* **`version`**: cadena que representa la versión del estándar de consentimiento. Establezca esta propiedad en `"1.0"` para el estándar Adobe 1.0.
* **`value.general`**: el valor de consentimiento. Establezca esto en `"in"` cuando los usuarios acepten la inclusión y en `"out"` cuando los usuarios acepten la exclusión.

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

Web SDK también admite el envío de más de un objeto de consentimiento en una solicitud, como se muestra en el ejemplo siguiente.

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

Una vez que haya comunicado las preferencias de usuario a Web SDK mediante el comando `setConsent`, SDK conserva las preferencias de usuario respecto a una cookie. La próxima vez que el usuario cargue el sitio web en el explorador, Web SDK recuperará y utilizará estas preferencias persistentes para determinar si se pueden enviar o no eventos a Adobe.

Deberá almacenar las preferencias de usuario de forma independiente para poder mostrar el cuadro de diálogo de consentimiento con las preferencias actuales. No hay forma de recuperar las preferencias de usuario de Web SDK. Para asegurarse de que las preferencias del usuario permanecen sincronizadas con SDK, puede llamar al comando `setConsent` en cada carga de página. Web SDK solo realizará una llamada al servidor si las preferencias han cambiado.
