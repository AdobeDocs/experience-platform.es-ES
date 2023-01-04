---
title: Compatibilidad con las preferencias de consentimiento del cliente mediante el SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo admitir las preferencias de consentimiento con el SDK web de Adobe Experience Platform.
keywords: consentimiento;defaultConsent;consentimiento predeterminado;setConsent;grupo de campos Privacidad del perfil;grupo de campos Privacidad del evento de experiencia;grupo de campos Privacidad;
exl-id: 647e4a84-4a66-45d6-8b05-d78786bca63a
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 0%

---

# Compatibilidad con las preferencias de consentimiento del cliente

Para respetar la privacidad del usuario, es posible que desee solicitar el consentimiento del usuario antes de permitir que el SDK utilice datos específicos del usuario para determinados fines. Actualmente, el SDK solo permite a los usuarios activar o desactivar todas las opciones, pero en el Adobe futuro espera proporcionar un control más granular sobre determinadas finalidades.

Si el usuario opta por cualquier opción, el SDK puede realizar las siguientes tareas:

* Envíe datos a y desde los servidores de Adobe.
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

Cuando el consentimiento predeterminado para el propósito general está establecido en pendiente, se intenta ejecutar cualquier comando que dependa de las preferencias de inclusión del usuario (por ejemplo, la variable `sendEvent` ) da como resultado que el comando se ponga en cola dentro del SDK. Estos comandos no se procesan hasta que no haya comunicado las preferencias de inclusión del usuario al SDK.

>[!NOTE]
>
>Los comandos solo se ponen en cola en la memoria. No se guardan entre cargas de página.

Si no desea recopilar eventos que se produjeron antes de que se establecieran las preferencias de inclusión del usuario, puede pasar `"defaultConsent": "out"` durante la configuración del SDK. El intento de ejecutar cualquier comando que dependa de las preferencias de inclusión del usuario no tendrá ningún efecto hasta que haya comunicado las preferencias de inclusión del usuario al SDK.

>[!NOTE]
>
>Actualmente, el SDK solo admite un único propósito, o ninguno. Aunque planificamos crear un conjunto más sólido de propósitos o categorías que se correspondan con las diferentes capacidades de Adobe y ofertas de productos, la implementación actual es un enfoque de inclusión de todo o nada.  Esto solo se aplica a Adobe Experience Platform [!DNL Web SDK] y NO otras bibliotecas JavaScript de Adobe.

En este punto, es posible que prefiera pedir al usuario que se una en alguna parte de la interfaz de usuario. Una vez recopiladas las preferencias del usuario, comunique estas preferencias al SDK.

## Comunicación de las preferencias de consentimiento a través del estándar Adobe Experience Platform

El SDK admite las versiones 1.0 y 2.0 del estándar de consentimiento de Adobe Experience Platform. Actualmente, las normas 1.0 y 2.0 solo admiten la aplicación automática de una preferencia de consentimiento total o nulo. El estándar 1.0 se está eliminando progresivamente en favor del estándar 2.0. El estándar 2.0 le permite agregar preferencias de consentimiento adicionales que se pueden utilizar para aplicar manualmente las preferencias de consentimiento.

### Uso de la versión 2.0 estándar de Adobe

Si utiliza Adobe Experience Platform, debe incluir un grupo de campos de esquema de privacidad en el esquema de perfil. Consulte [Gobernanza, privacidad y seguridad en Adobe Experience Platform](../../landing/governance-privacy-security/overview.md) para obtener más información sobre la versión 2.0 del estándar de Adobe. Puede agregar datos dentro del objeto value debajo correspondiente al esquema del `consents` del campo [!UICONTROL Consentimientos y preferencias] grupo de campos de perfil.

Si el usuario decide participar, ejecute el `setConsent` con la preferencia de recopilación establecida en `y` de la siguiente manera:

```javascript
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
    }]
});
```

El campo de hora debe especificar cuándo el usuario actualizó por última vez sus preferencias de consentimiento. Si el usuario decide excluirse, ejecute el `setConsent` con la preferencia de recopilación establecida en `n` de la siguiente manera:

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "2.0",
      value: {
        collect: {
          val: "n"
        },
        metadata: {
          time: "2021-03-17T15:51:30-07:00"
        }
      }
    }]
});
```

### Uso de la versión 1.0 estándar de Adobe

Si el usuario decide participar, ejecute el `setConsent` con la variable `general` opción definida en `in` de la siguiente manera:

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

Si el usuario decide excluirse, ejecute el `setConsent` con la variable `general` opción definida en `out` de la siguiente manera:

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

## Comunicación de las preferencias de consentimiento a través del estándar IAB TCF

El SDK admite la grabación de las preferencias de consentimiento de un usuario proporcionadas mediante el marco de transparencia y consentimiento (TCF) de Interactive Advertising Bureau Europe (IAB). La cadena de consentimiento se puede establecer mediante el mismo `setConsent` como se muestra arriba:

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

Cuando el consentimiento se establece de esta manera, el perfil del cliente en tiempo real se actualiza con la información de consentimiento. Para que esto funcione, el esquema XDM de perfil debe contener la variable [Grupo de campos del esquema de privacidad de perfil](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-privacy.schema.md). Al enviar eventos, la información de consentimiento IAB debe agregarse manualmente al objeto XDM de evento. El SDK no incluye automáticamente la información de consentimiento en los eventos. Para enviar la información de consentimiento en eventos, la variable [Grupo de campos de privacidad de eventos de experiencia](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/experience-event/experienceevent-privacy.schema.md) debe agregarse al esquema de Experience Event .

## Envío de varios estándares en una solicitud

El SDK también admite el envío de más de un objeto de consentimiento en una solicitud.

```javascript
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
    },{
      standard: "IAB TCF",
      version: "2.0",
      value: "CO1Z4yuO1Z4yuAcABBENArCsAP_AAH_AACiQGCNX_T5eb2vj-3Zdt_tkaYwf55y3o-wzhhaIse8NwIeH7BoGP2MwvBX4JiQCGBAkkiKBAQdtHGhcCQABgIhRiTKMYk2MjzNKJLJAilsbe0NYCD9mnsHT3ZCY70--u__7P3fAwQgkwVLwCRIWwgJJs0ohTABCOICpBwCUEIQEClhoACAnYFAR6gAAAIDAACAAAAEEEBAIABAAAkIgAAAEBAKACIBAACAEaAhAARIEAsAJEgCAAVA0JACKIIQBCDgwCjlACAoAAAAA.YAAAAAAAAAAA",
      gdprApplies: true
    }]
});
```

## Persistencia de las preferencias de consentimiento

Una vez que haya comunicado las preferencias de usuario al SDK mediante la función `setConsent` , el SDK mantiene las preferencias del usuario en una cookie. La próxima vez que el usuario cargue el sitio web en el explorador, el SDK recuperará y utilizará estas preferencias persistentes para determinar si los eventos se pueden enviar o no a Adobe.

Deberá almacenar las preferencias de usuario de forma independiente para poder mostrar el cuadro de diálogo de consentimiento con las preferencias actuales. No hay forma de recuperar las preferencias de usuario del SDK. Para asegurarse de que las preferencias de usuario permanecen sincronizadas con el SDK, puede llamar a la función `setConsent` en cada carga de página. El SDK solo realizará una llamada al servidor si las preferencias han cambiado.

## Sincronización de identidades al configurar el consentimiento

Cuando el consentimiento predeterminado está pendiente o agotado, la variable `setConsent` puede ser la primera solicitud que sale y establece identidad. Debido a esto, puede ser importante sincronizar identidades en la primera solicitud. El mapa de identidad se puede agregar a `setConsent` igual que en el `sendEvent` comando. Consulte [Recuperación del ID de Experience Cloud](../identity/overview.md)
