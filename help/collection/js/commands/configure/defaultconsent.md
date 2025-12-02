---
title: defaultConsent
description: Establezca el método de recopilación de consentimiento predeterminado para su propiedad web.
exl-id: 2a22fa8b-a234-4d3e-9b55-c7482a928fe6
source-git-commit: 1e272eb18fac2f59f9737756d48947a25573d772
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 5%

---


# `defaultConsent`

La propiedad `defaultConsent` determina cómo se administra el consentimiento de recopilación de datos antes de llamar al comando [`setConsent`](../setconsent.md). Esta propiedad es valiosa cuando no desea recopilar accidentalmente datos de personas que residen en áreas en las que se requiere consentimiento antes de recopilar datos.

Si tiene un visitante que no se encuentra dentro de la jurisdicción del Reglamento General de Protección de Datos (RGPD), el consentimiento predeterminado podría establecerse en `in`. Los visitantes dentro de la jurisdicción del RGPD pueden tener el consentimiento predeterminado establecido en `pending`. Su plataforma de administración de consentimiento (CMP) puede detectar la región del cliente y proporcionar el indicador `gdprApplies` a IAB TCF 2.0. Este indicador se puede utilizar para establecer el consentimiento predeterminado.

Establezca la propiedad de cadena `defaultConsent` en el nivel de consentimiento deseado al ejecutar el comando `configure`. Esta propiedad distingue entre mayúsculas y minúsculas y sólo admite los tres valores siguientes: `"in"`, `"out"` y `"pending"`. Si intenta utilizar cualquier otro valor, la biblioteca genera un error. Si no se establece en el comando `configure`, el valor predeterminado es **`in`**.

>[!IMPORTANT]
>
>El valor `defaultConsent` no persiste entre cargas de página. Asegúrese de establecer el consentimiento predeterminado deseado cada vez que llame al comando `configure`.

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

Web SDK ofrece dos opciones de consentimiento complementarias:

* `defaultConsent` (esta página): determina las preferencias de consentimiento predeterminadas.
* [`setConsent`](../setconsent.md): capture las preferencias de consentimiento de los visitantes.

Cuando se utilizan juntos, esta configuración puede llevar a diferentes resultados de recopilación de datos y configuración de cookies, según sus valores configurados.

Consulte la tabla siguiente para comprender cuándo se produce la recopilación de datos y cuándo se configuran las cookies, según la configuración de consentimiento.

| `defaultConsent` | `setConsent` | Se produce la recopilación de datos | Web SDK establece cookies de explorador |
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

Consulte [Cookies de Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/en/docs/core-services/interface/data-collection/cookies/web-sdk) para obtener una lista de las cookies que establece la biblioteca.

>[!NOTE]
>
>Las cookies de identidad y consentimiento se establecen incluso si un visitante decide excluirse del seguimiento. Estas cookies son necesarias para cumplir con sus preferencias de recopilación de datos.

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
