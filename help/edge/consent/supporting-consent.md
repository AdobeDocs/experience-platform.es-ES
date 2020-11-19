---
title: Apoyo al consentimiento
seo-title: Compatibilidad con la preferencia de consentimiento del SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo admitir las preferencias de consentimiento con el SDK web de Experience Platform
seo-description: Obtenga información sobre cómo admitir las preferencias de consentimiento con el SDK web de Experience Platform
keywords: consent;defaultConsent;default consent;setConsent;Profile Privacy Mixin;Experience Event Privacy Mixin;Privacy Mixin;
translation-type: tm+mt
source-git-commit: 0928dd3eb2c034fac14d14d6e53ba07cdc49a6ea
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 0%

---


# Apoyo al consentimiento

Para respetar la privacidad del usuario, es posible que desee solicitar el consentimiento del usuario antes de permitir que el SDK utilice datos específicos del usuario para determinados fines. Actualmente, el SDK solo permite a los usuarios adhesión o excluir todos los fines, pero en el futuro Adobe espera proporcionar un control más granular sobre determinados fines.

Si el usuario adhesión a todos los fines, el SDK puede realizar las siguientes tareas:

* Enviar datos desde y hacia los servidores de Adobe.
* Leer y escribir cookies o elementos de almacenamiento web (excepto para mantener las preferencias de inclusión del usuario).

Si el usuario exclusión todos los fines, el SDK no realiza ninguna de estas tareas.

## Configuración del consentimiento

De forma predeterminada, el usuario está adhesión para todos los fines. Para evitar que el SDK realice las tareas anteriores hasta que el usuario adhesión, pase `"defaultConsent": "pending"` durante la configuración del SDK lo siguiente:

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "imsOrgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": "pending"
});
```

Cuando el consentimiento predeterminado para el propósito general se establece en pendiente, al intentar ejecutar cualquier comando que dependa de las preferencias de inclusión del usuario (por ejemplo, el comando `event` ), el comando se pone en cola dentro del SDK. Estos comandos no se procesan hasta que no haya comunicado las preferencias de selección del usuario al SDK.

En este punto, puede que prefiera pedir al usuario que adhesión en alguna parte de la interfaz de usuario. Una vez recopiladas las preferencias del usuario, comunique estas preferencias al SDK.

## Comunicación de preferencias de consentimiento a través de Adobe Standard

Si el usuario adhesión, ejecute el `setConsent` comando con la `general` opción establecida en `in` :

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "1.0",
      value: {
        general: "in"
      }
    }]
});
```

Dado que el usuario ya ha adhesión, el SDK ejecuta todos los comandos en cola anteriores. Los comandos futuros que dependan del usuario que adhesión no se pondrán en cola y se ejecutarán sin demora.

Si el usuario decide exclusión, ejecute el `setConsent` comando con la `general` opción establecida en `out` :

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "1.0",
      value: {
        general: "out"
      }
    }]
});
```

>[!NOTE]
>
>Una vez que un usuario ha exclusión, el SDK no le permitirá establecer el consentimiento de los usuarios en `in`.

Dado que el usuario eligió exclusión, se rechazan las promesas que se devolvieron de comandos en cola anteriores. Los futuros comandos que dependan de que el usuario adhesión devolverán promesas rechazadas de manera similar. Para obtener más información sobre la gestión o supresión de errores, consulte [Ejecución de comandos](../fundamentals/executing-commands.md).

>[!NOTE]
>
>Actualmente, el SDK solo admite el `general` propósito. Aunque planeamos crear un conjunto más sólido de propósitos o categorías que se correspondan con las diferentes capacidades de Adobe y ofertas de productos, la implementación actual es un enfoque de inclusión total o nulo.  Esto solo se aplica a Adobe Experience Platform [!DNL Web SDK] y NO a otras bibliotecas JavaScript de Adobe.

## Comunicar las preferencias de consentimiento a través del estándar TCF de IAB

El SDK admite la grabación de las preferencias de consentimiento de un usuario a través del estándar Interactive Advertising Bureau Europe (IAB) Transparency and Consent Framework (TCF). La cadena de consentimiento se puede configurar mediante el mismo `setConsent` comando que se muestra arriba:

```javascript
alloy("setConsent", {
    consent: [{
      standard: "IAB TCF",
      version: "2.0",
      value: "CO1Z4yuO1Z4yuAcABBENArCsAP_AAH_AACiQGCNX_T5eb2vj-3Zdt_tkaYwf55y3o-wzhhaIse8NwIeH7BoGP2MwvBX4JiQCGBAkkiKBAQdtHGhcCQABgIhRiTKMYk2MjzNKJLJAilsbe0NYCD9mnsHT3ZCY70--u__7P3fAwQgkwVLwCRIWwgJJs0ohTABCOICpBwCUEIQEClhoACAnYFAR6gAAAIDAACAAAAEEEBAIABAAAkIgAAAEBAKACIBAACAEaAhAARIEAsAJEgCAAVA0JACKIIQBCDgwCjlACAoAAAAA.YAAAAAAAAAAA",
      gdprApplies: true
    }]
});
```

Cuando el consentimiento se establece de esta manera, el Perfil del cliente en tiempo real se actualiza con la información de consentimiento. Para que esto funcione, el esquema perfil XDM debe contener la mezcla de privacidad de [Perfil](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-privacy.schema.md). Al enviar eventos, la información de consentimiento de IAB debe agregarse manualmente al objeto XDM de evento. El SDK no incluye automáticamente la información de consentimiento en los eventos. Para enviar la información de consentimiento en eventos, debe agregarse la mezcla [de privacidad de](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/experience-event/experienceevent-privacy.schema.md) Experience Evento al esquema de Experience Evento.

## Envío de ambos estándares en una solicitud

El SDK también admite el envío de más de un objeto de consentimiento en una solicitud.

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "1.0",
      value: {
        general: "in"
      }
    },{
      standard: "IAB TCF",
      version: "2.0",
      value: "CO1Z4yuO1Z4yuAcABBENArCsAP_AAH_AACiQGCNX_T5eb2vj-3Zdt_tkaYwf55y3o-wzhhaIse8NwIeH7BoGP2MwvBX4JiQCGBAkkiKBAQdtHGhcCQABgIhRiTKMYk2MjzNKJLJAilsbe0NYCD9mnsHT3ZCY70--u__7P3fAwQgkwVLwCRIWwgJJs0ohTABCOICpBwCUEIQEClhoACAnYFAR6gAAAIDAACAAAAEEEBAIABAAAkIgAAAEBAKACIBAACAEaAhAARIEAsAJEgCAAVA0JACKIIQBCDgwCjlACAoAAAAA.YAAAAAAAAAAA",
      gdprApplies: true
    }]
});
```

## Persistencia de las preferencias de consentimiento

Después de comunicar las preferencias de usuario al SDK mediante el `setConsent` comando, el SDK mantiene las preferencias del usuario en una cookie. La próxima vez que el usuario cargue el sitio web en el navegador, el SDK recuperará y utilizará estas preferencias persistentes para determinar si se pueden enviar o no eventos a Adobe. No es necesario volver a ejecutar el `setConsent` comando, excepto para comunicar un cambio en las preferencias del usuario, que puede realizar en cualquier momento.

## Sincronización de identidades al configurar el consentimiento

Cuando el consentimiento por defecto está pendiente, la `setConsent` solicitud puede ser la primera que sale y establece la identidad. Debido a esto, puede ser importante sincronizar identidades en la primera solicitud. El mapa de identidad se puede agregar al `setConsent` comando como en el `sendEvent` comando. Consulte [Recuperación de ID de Experience Cloud](../identity/overview.md)

