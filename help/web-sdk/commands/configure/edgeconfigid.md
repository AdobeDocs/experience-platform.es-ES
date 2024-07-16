---
title: edgeConfigId
description: Determine el ID de la secuencia de datos a la que desea enviar los datos.
exl-id: 2d709f70-c014-4868-b2f5-17e8b88343d1
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# `edgeConfigId`

La propiedad `edgeConfigId` es una cadena que determina a qué [secuencia de datos](../../../datastreams/overview.md) de Adobe Experience Platform desea enviar datos. Esta propiedad es necesaria al enviar datos al Adobe.

Para localizar un ID de secuencia de datos:

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Flujos de datos]**.
1. Utilice el campo de búsqueda para localizar el conjunto de datos deseado y, a continuación, seleccione **[!UICONTROL Copiar]** ![Copiar](../../assets/copy.png) junto al identificador del conjunto de datos.

También puede seleccionar el nombre de la secuencia de datos deseado y el ID de la secuencia de datos aparece en la columna derecha para que lo copie.

## Seleccione el ID de la secuencia de datos mediante la extensión de etiqueta del SDK web

Elija de una lista de flujos de datos disponibles o ingrese un ID de flujo de datos directamente al [configurar la extensión de etiqueta](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensions]** y, a continuación, haga clic en **[!UICONTROL Configure]** en la tarjeta de [!UICONTROL Adobe Experience Platform Web SDK].
1. Busque la sección [!UICONTROL Datastreams] y, a continuación, seleccione el método que desee para determinar la secuencia de datos.
   * Si elige una de las listas, seleccione la zona protegida y la secuencia de datos de cada lista desplegable correspondiente.
   * Si introduce valores, introduzca el ID de flujo de datos deseado.
1. Haz clic en **[!UICONTROL Guardar]** y después publica los cambios.

Puede enviar datos a diferentes flujos de datos para los entornos de etiquetas de producción, ensayo y desarrollo.

## Seleccione el ID de la secuencia de datos mediante la biblioteca JavaScript del SDK web

Establezca la propiedad de cadena `edgeConfigId` al ejecutar el comando `configure`. Esta propiedad es necesaria para todas las implementaciones de SDK web. Si omite esta propiedad, el SDK web no sabe a qué secuencia de datos enviar datos, lo que provoca que esos datos se pierdan de forma permanente.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```

Si configura varias instancias del SDK web en una sola página, debe configurar un(a) `edgeConfigId` diferente para cada instancia.
