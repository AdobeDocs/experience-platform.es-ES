---
title: datastreamId
description: Determine el ID de la secuencia de datos a la que desea enviar los datos.
exl-id: 2d709f70-c014-4868-b2f5-17e8b88343d1
source-git-commit: b9fea4833c4fe869b27c1270aafd3f7ed62d59db
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# `datastreamId`

La propiedad `datastreamId` es una cadena que determina a qué [secuencia de datos](/help/datastreams/overview.md) de Adobe Experience Platform desea enviar datos. Esta propiedad es necesaria al enviar datos a Adobe. Las versiones 2.20.0 o anteriores de Web SDK usan `edgeConfigId` en su lugar.

Para localizar un ID de secuencia de datos:

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Data Collection]** > **[!UICONTROL Datastreams]**.
1. Utilice el campo de búsqueda para localizar el conjunto de datos deseado y, a continuación, seleccione **[!UICONTROL Copy]** ![Copiar](../../assets/copy.png) junto al identificador del conjunto de datos.

También puede seleccionar el nombre del flujo de datos deseado y el ID del flujo de datos aparece en la columna derecha para que lo copie.

## Ejemplo de código

Establezca la propiedad de cadena `datastreamID` al ejecutar el comando `configure`. Esta propiedad es necesaria para todas las implementaciones de Web SDK. Si omite esta propiedad, Web SDK no sabe a qué secuencia de datos enviar datos, lo que provoca que esos datos se pierdan de forma permanente.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```

>[!NOTE]
>
>Si configura varias instancias de Web SDK en una sola página, debe configurar un(a) `datastreamId` diferente para cada instancia.

## Seleccione el ID de la secuencia de datos con la extensión de etiquetas Web SDK

Consulte [Configuración de secuencia de datos](/help/tags/extensions/client/web-sdk/configure/datastreams.md) en la documentación de la extensión de etiquetas de Web SDK para obtener información sobre cómo establecer la secuencia de datos deseada para cada entorno mediante etiquetas. Puede enviar datos a diferentes flujos de datos para los entornos de etiquetas de producción, ensayo y desarrollo.
