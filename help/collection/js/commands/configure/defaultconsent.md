---
title: defaultConsent
description: Establezca el método de recopilación de consentimiento predeterminado para su propiedad web.
exl-id: 2a22fa8b-a234-4d3e-9b55-c7482a928fe6
source-git-commit: bf0bb72777cacd822fd6e887ac3ef71764784214
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---


# `defaultConsent`

La propiedad `defaultConsent` determina cómo se administra el consentimiento de recopilación de datos antes de llamar al comando [`setConsent`](../setconsent.md). Esta propiedad es valiosa cuando no desea recopilar accidentalmente datos de personas que residen en áreas en las que se requiere consentimiento antes de recopilar datos.

Si tiene un visitante que no se encuentra dentro de la jurisdicción del Reglamento General de Protección de Datos (RGPD), el consentimiento predeterminado podría establecerse en `in`. Los visitantes dentro de la jurisdicción del RGPD pueden tener el consentimiento predeterminado establecido en `pending`. Su plataforma de administración de consentimiento (CMP) puede detectar la región del cliente y proporcionar el indicador `gdprApplies` a IAB TCF 2.0. Este indicador se puede utilizar para establecer el consentimiento predeterminado.

Establezca la propiedad de cadena `defaultConsent` en el nivel de consentimiento deseado al ejecutar el comando `configure`. Esta propiedad distingue entre mayúsculas y minúsculas y sólo admite los tres valores siguientes: `"in"`, `"out"` y `"pending"`. Si intenta utilizar cualquier otro valor, la biblioteca genera un error. Si no se establece en el comando `configure`, el valor predeterminado es **`in`**.

>[!IMPORTANT]
>
>El valor `defaultConsent` no persiste entre cargas de página. Asegúrese de establecer el consentimiento predeterminado deseado cada vez que llame al comando `configure`. Por el contrario, el consentimiento resuelto de un visitante (establecido mediante [`setConsent`](../setconsent.md)) persiste en una cookie y se aplica automáticamente en las cargas de página posteriores.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  defaultConsent: "pending"
});
```

* **`in`**: la recopilación de datos funciona normalmente hasta que el usuario se excluye.
* **`out`**: los datos se descartan permanentemente hasta que el usuario se incluye.
* **`pending`**: los datos se almacenan localmente hasta que el usuario decida participar usando el comando [`setConsent`](../setconsent.md).

>[!NOTE]
>
>Aunque Adobe planea crear un conjunto más sólido de propósitos o categorías que se correspondan con las capacidades y ofertas de productos de Adobe, la implementación actual es un enfoque de inclusión de todo o nada. Esta limitación solo se aplica a Web SDK y no a otras bibliotecas de Adobe JavaScript.

## Usando `defaultConsent` junto con `setConsent` {#using-consent}

Cuando se usan juntos, `defaultConsent` y `setConsent` producen resultados diferentes de recopilación de datos, configuración de cookies e identidad según sus valores configurados. Consulte [Consentimiento e identidad en la recopilación de datos](/help/collection/identity/consent.md#how-consent-affects-identity) para obtener una tabla de interacción completa.

## Estableciendo consentimiento predeterminado basado en `gdprApplies`

Algunas CMP permiten determinar si el Reglamento general de protección de datos (RGPD) se aplica al cliente. Si desea dar su consentimiento a clientes en los que no se aplique el RGPD, puede utilizar el indicador `gdprApplies` en una llamada de API TCF. Por ejemplo:

```js
var alloyConfiguration = { ... };
window.__tcfapi('getTCData', 2, function (tcData, success) {
  if (success) {
    alloyConfiguration.defaultConsent = tcData.gdprApplies ? "pending" : "in";
    window.alloy("configure", alloyConfiguration);
  }
});
```

En el bloque de código anterior, se llama al comando `configure` después de obtener `tcData` de la API de TCF. Si `gdprApplies` es verdadero, el consentimiento predeterminado es `pending`. Si `gdprApplies` es falso, el consentimiento predeterminado se establece en `in`. Asegúrese de completar la variable `alloyConfiguration` con la configuración.

## Consentimiento predeterminado con la extensión de etiqueta Web SDK

Consulte [Configuración de consentimiento](/help/tags/extensions/client/web-sdk/configure/consent.md) en la documentación de la extensión de etiquetas de Web SDK para obtener información sobre cómo realizar estas acciones mediante etiquetas.
