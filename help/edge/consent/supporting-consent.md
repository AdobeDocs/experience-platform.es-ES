---
title: Compatibilidad con las preferencias de consentimiento del cliente mediante el SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo admitir las preferencias de consentimiento con el SDK web de Adobe Experience Platform.
keywords: consentimiento;defaultConsent;consentimiento predeterminado;setConsent;combinación de privacidad de perfil;combinación de privacidad de eventos de experiencia;combinación de privacidad de privacidad de privacidad
translation-type: tm+mt
source-git-commit: 308c10eb0d1f78dad2b8b6158f28d0384a65c78c
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 0%

---


# Compatibilidad con las preferencias de consentimiento del cliente

Para respetar la privacidad del usuario, es posible que desee solicitar el consentimiento del usuario antes de permitir que el SDK utilice datos específicos del usuario para determinados fines. Actualmente, el SDK solo permite a los usuarios activar o desactivar todas las opciones, pero en el futuro Adobe espera proporcionar un control más granular de determinadas finalidades.

Si el usuario opta por cualquier opción, el SDK puede realizar las siguientes tareas:

* Envíe datos desde y hacia los servidores de Adobe.
* Leer y escribir cookies o elementos de almacenamiento web.

Si el usuario decide excluirse de todos los aspectos, el SDK no realiza ninguna de estas tareas.

## Configuración del consentimiento

De forma predeterminada, el usuario se incluye en todas las opciones. Para evitar que el SDK realice las tareas anteriores hasta que el usuario decida entrar, pase `"defaultConsent": "pending"` durante la configuración del SDK de la siguiente manera:

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "imsOrgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": "pending"
});
```

Cuando el consentimiento predeterminado para el propósito general se establece en pendiente, al intentar ejecutar cualquier comando que dependa de las preferencias de inclusión del usuario (por ejemplo, el comando `event`), se pone en cola el comando dentro del SDK. Estos comandos no se procesan hasta que no haya comunicado las preferencias de inclusión del usuario al SDK.

En este punto, es posible que prefiera pedir al usuario que se una en alguna parte de la interfaz de usuario. Una vez recopiladas las preferencias del usuario, comunique estas preferencias al SDK.

## Comunicación de las preferencias de consentimiento a través de Adobe Standard

Si el usuario decide participar, ejecute el comando `setConsent` con la opción `general` establecida en `in` de la siguiente manera:

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

Dado que el usuario ha elegido, el SDK ejecuta todos los comandos en cola anteriores. Los comandos futuros que dependan de que el usuario haya elegido no se pondrán en cola y, en su lugar, se ejecutarán rápidamente.

Si el usuario decide excluirse, ejecute el comando `setConsent` con la opción `general` establecida en `out` de la siguiente manera:

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
>Una vez que un usuario ha optado por no participar, el SDK no le permitirá establecer el consentimiento del usuario en `in`.

Dado que el usuario optó por la exclusión, se rechazan las promesas que se devolvieron de comandos en cola anteriores. Los comandos futuros que dependan de que el usuario opte por la opción devolverán promesas que se rechazan de manera similar. Para obtener más información sobre la gestión o supresión de errores, consulte [Ejecución de comandos](../fundamentals/executing-commands.md).

>[!NOTE]
>
>Actualmente, el SDK solo admite el propósito `general` . Aunque planificamos crear un conjunto más sólido de propósitos o categorías que se correspondan con las diferentes capacidades y ofertas de productos de Adobe, la implementación actual es un enfoque de inclusión de todo o nada.  Esto solo se aplica a Adobe Experience Platform [!DNL Web SDK] y NO a otras bibliotecas JavaScript de Adobe.

## Comunicación de las preferencias de consentimiento a través del estándar IAB TCF

El SDK admite la grabación de las preferencias de consentimiento de un usuario proporcionadas mediante el marco de transparencia y consentimiento (TCF) de Interactive Advertising Bureau Europe (IAB). La cadena de consentimiento se puede configurar mediante el mismo comando `setConsent` que se muestra arriba de esta manera:

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

Cuando el consentimiento se establece de esta manera, el perfil del cliente en tiempo real se actualiza con la información de consentimiento. Para que esto funcione, el esquema XDM de perfil debe contener la [Mixin de privacidad de perfil](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-privacy.schema.md). Al enviar eventos, la información de consentimiento IAB debe agregarse manualmente al objeto XDM de evento. El SDK no incluye automáticamente la información de consentimiento en los eventos. Para enviar la información de consentimiento en eventos, la [Mezcla de privacidad de eventos de experiencia](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/experience-event/experienceevent-privacy.schema.md) debe agregarse al esquema de eventos de experiencia.

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

Después de haber comunicado las preferencias de usuario al SDK mediante el comando `setConsent`, el SDK mantiene las preferencias del usuario en una cookie. La próxima vez que el usuario cargue el sitio web en el explorador, el SDK recuperará y utilizará estas preferencias persistentes para determinar si se pueden enviar eventos a Adobe o no. No es necesario ejecutar el comando `setConsent` de nuevo, excepto para comunicar un cambio en las preferencias del usuario, que puede hacer en cualquier momento.

## Sincronización de identidades al configurar el consentimiento

Cuando el consentimiento predeterminado está pendiente, `setConsent` puede ser la primera solicitud que se emite y establece la identidad. Debido a esto, puede ser importante sincronizar identidades en la primera solicitud. El mapa de identidad se puede agregar al comando `setConsent` como en el comando `sendEvent`. Consulte [Recuperación del Experience Cloud ID](../identity/overview.md)

