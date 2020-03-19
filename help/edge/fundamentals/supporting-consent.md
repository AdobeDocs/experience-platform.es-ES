---
title: Apoyo al consentimiento
seo-title: Compatibilidad con la preferencia de consentimiento del SDK web de Adobe Experience Platform
description: Descubra cómo se admiten las preferencias de consentimiento con el SDK web de la plataforma de experiencia
seo-description: Descubra cómo se admiten las preferencias de consentimiento con el SDK web de la plataforma de experiencia
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (Beta) Consentimiento de apoyo

>[!IMPORTANT]
>
>El SDK web de la plataforma de experiencia de Adobe se encuentra en fase beta y no está disponible para todos los usuarios. La documentación y la funcionalidad están sujetas a cambios.

Para respetar la privacidad del usuario, es posible que desee solicitar el consentimiento del usuario antes de permitir que el SDK utilice datos específicos del usuario para determinados fines. Actualmente, el SDK solo permite a los usuarios incluir o excluir todos los fines, pero en el futuro Adobe espera proporcionar un control más granular sobre determinados fines.

Si el usuario opta por todos los aspectos, el SDK puede realizar las siguientes tareas:

* Enviar datos desde y hacia los servidores de Adobe.
* Leer y escribir cookies o elementos de almacenamiento web (excepto para mantener las preferencias de inclusión del usuario).

Si el usuario no tiene ninguna finalidad, el SDK no realiza ninguna de estas tareas.

## Configuración del consentimiento

De forma predeterminada, el usuario ha optado por todos los propósitos. Para evitar que el SDK lleve a cabo las tareas anteriores hasta que el usuario decida participar, pase `"defaultConsent": { "general": "pending" }` durante la configuración del SDK de la siguiente manera:

```javascript
alloy("configure", {
  "configId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "imsOrgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": { "general": "pending" }
});
```

Cuando el consentimiento predeterminado para el propósito general se establece en pendiente, al intentar ejecutar cualquier comando que dependa de las preferencias de inclusión del usuario (por ejemplo, el comando `event` ), el comando se pone en cola dentro del SDK. Estos comandos no se procesan hasta que no haya comunicado las preferencias de selección del usuario al SDK.

En este punto, puede que prefiera pedir al usuario que opte por entrar en algún lugar de la interfaz de usuario. Una vez recopiladas las preferencias del usuario, comunique estas preferencias al SDK.

## Comunicación de preferencias de consentimiento

Si el usuario decide participar, ejecute el `setConsent` comando con la `general` opción establecida en `in` :

```javascript
alloy("setConsent", {
  "general": "in"
});
```

Dado que el usuario ya ha elegido, el SDK ejecuta todos los comandos en cola anteriores. Los comandos futuros que dependan de que el usuario opte por la aplicación _no se pondrán_ en cola y se ejecutarán sin demora.

Si el usuario decide desactivar la opción, ejecute el `setConsent` comando con la `general` opción establecida en `out` :

```javascript
alloy("setConsent", {
  "general": "out"
});
```

>[!NOTE]
>
>Una vez que un usuario ha optado por la exclusión, el SDK no le permitirá establecer el consentimiento de los usuarios en `in`.

Dado que el usuario ha elegido la opción de desactivación, se rechazan las promesas que se devolvieron de comandos en cola anteriores. Los comandos futuros que dependan de que el usuario opte por el servicio devolverán promesas que se rechazan de manera similar. Para obtener más información sobre la gestión o supresión de errores, consulte [Ejecución de comandos](executing-commands.md).

>[!NOTE]
>
>Actualmente, el SDK solo admite el `general` propósito. Aunque planeamos crear un conjunto más sólido de propósitos o categorías que se correspondan con las diferentes capacidades y ofertas de productos de Adobe, la implementación actual es un enfoque de inclusión total o nulo.  Esto solo se aplica al SDK web de Adobe Experience Platform y NO a otras bibliotecas JavaScript de Adobe.

## Persistencia de las preferencias de consentimiento

Después de comunicar las preferencias de usuario al SDK mediante el `setConsent` comando, el SDK mantiene las preferencias del usuario en una cookie. La próxima vez que el usuario cargue el sitio web en el navegador, el SDK recuperará y usará estas preferencias persistentes. No es necesario volver a ejecutar el `setConsent` comando, excepto para comunicar un cambio en las preferencias del usuario, que puede realizar en cualquier momento.