---
title: defaultConsent
description: Establezca el método de recopilación de consentimiento predeterminado.
source-git-commit: b9db136a9077e3420bfeb44ae45e7d72c322acbb
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# `defaultConsent`

El `defaultConsent` determina cómo administra el consentimiento de recopilación de datos antes de llamar al método [`setConsent`](../setconsent.md) comando. Esta propiedad es valiosa cuando no desea recopilar accidentalmente datos de personas que residen en áreas en las que se requiere consentimiento antes de recopilar datos.

Esta propiedad permite tres valores:

* **Entrada**: la recopilación de datos se realiza de la forma habitual hasta que el usuario se excluye.
* **Fuera**: los datos se descartan permanentemente hasta que el usuario se incluye.
* **Pendiente**: los datos se almacenan localmente hasta que el usuario opta por utilizar el [`setConsent`](../setconsent.md) comando. Los datos no persisten entre cargas de página.

Si tiene un visitante que no está dentro de la jurisdicción del Reglamento General de Protección de Datos (RGPD), el consentimiento predeterminado podría establecerse en `in`. Los visitantes dentro de la jurisdicción del RGPD pueden tener el consentimiento predeterminado establecido en `pending`. Su plataforma de administración de consentimiento (CMP) puede detectar la región del cliente y proporcionar el indicador `gdprApplies` a IAB TCF 2.0. Este indicador se puede utilizar para establecer el consentimiento predeterminado.

## Definir consentimiento predeterminado con la extensión de etiqueta del SDK web

Seleccione el botón de opción que desee en **[!UICONTROL Consentimiento predeterminado]** cuando [configuración de la extensión de etiqueta](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Iniciar sesión en [experience.adobe.com](https://experience.adobe.com) usando sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensiones]**, luego haga clic en **[!UICONTROL Configurar]** en el [!UICONTROL SDK web de Adobe Experience Platform] Tarjeta de.
1. Desplácese hacia abajo hasta el [!UICONTROL Privacidad] y, a continuación, seleccione la **[!UICONTROL Consentimiento predeterminado]**.
1. Clic **[!UICONTROL Guardar]** y, a continuación, publique los cambios.

## Establecer el consentimiento predeterminado mediante la biblioteca JavaScript del SDK web

Configure las variables `defaultConsent` al nivel de consentimiento deseado al ejecutar el `configure` comando. Esta propiedad distingue entre mayúsculas y minúsculas y solo admite los tres valores siguientes: `"in"`, `"out"`, y `"pending"`. Si intenta utilizar cualquier otro valor, la biblioteca genera un error.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": "pending"
});
```
