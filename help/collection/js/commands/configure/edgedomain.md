---
title: edgeDomain
description: Determine el dominio al que desea enviar los datos.
exl-id: 6beb5116-cd23-42fd-934c-5cf84d1d7153
source-git-commit: 2d3c31e399989652a0472bbe2174ca8d8554ba30
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 3%

---

# `edgeDomain`

La propiedad `edgeDomain` le permite cambiar el dominio al que Web SDK envía los datos. El uso de un dominio personalizado puede ayudar a reducir el impacto de los bloqueadores de anuncios.

>[!NOTE]
>
>Esta propiedad no cambia dónde se configuran las cookies. Web SDK siempre establece [cookies de origen](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=es), independientemente de dónde envíe los datos.

El valor que use para `edgeDomain` depende de su participación en el [programa de certificados administrado por Adobe](https://experienceleague.adobe.com/en/docs/core-services/interface/data-collection/adobe-managed-cert):

**Si su organización participa en el programa de certificados administrado por Adobe**, establezca el valor en el dominio de origen seleccionado al configurar el certificado. Normalmente, este valor es un subdominio propiedad de su organización. Por ejemplo, `data.example.com`. Los registros CNAME de su organización reenvían esos datos a Adobe.

**Si su organización no participa en el programa de certificación**, establezca el valor en un subdominio de `data.adobedc.net`. Adobe recomienda utilizar el ID de empresa de IMS asignado por Adobe de su organización para mantener la coherencia. Por ejemplo, `example.data.adobedc.net`. Siga estos pasos para determinar su ID de compañía de IMS:

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. En cualquier lugar de la interfaz de Experience Cloud, presione `[Cmd]` + `[I]` (macOS) o `[Ctrl]` + `[I]` (Windows).
1. Aparece **[!UICONTROL User data debugger]**. Seleccione la pestaña **[!UICONTROL Assigned orgs]** .
1. Expanda la organización IMS deseada.
1. Busque el campo **[!UICONTROL Tenant]**. Este valor es el subdominio recomendado de `data.adobedc.net` para usar.

Establezca la cadena `edgeDomain` al ejecutar el comando `configure`. Si omite esta propiedad al configurar SDK, el valor predeterminado es `edge.adobedc.net`. Aunque el valor predeterminado es aceptable, Adobe considera una práctica recomendada establecer un valor específico de la organización.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  edgeDomain: "data.example.com"
});
```

## Dominio de Edge que utiliza la extensión de etiquetas de Web SDK

La extensión de etiqueta equivalente a esta propiedad es el campo **[!UICONTROL Edge domain]** en [Configuración de la instancia de SDK](/help/tags/extensions/client/web-sdk/configure/general.md) al configurar la extensión.
