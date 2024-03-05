---
title: edgeConfigId
description: Determine el ID de la secuencia de datos a la que desea enviar los datos.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# `edgeConfigId`

El `edgeConfigId` propiedad es una cadena que determina qué [secuencia de datos](../../../datastreams/overview.md) en Adobe Experience Platform a la que desea enviar datos. Esta propiedad es necesaria al enviar datos al Adobe.

Para localizar un ID de secuencia de datos:

1. Iniciar sesión en [experience.adobe.com](https://experience.adobe.com) usando sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Datastreams]**.
1. Utilice el campo de búsqueda para localizar el conjunto de datos deseado y luego seleccione **[!UICONTROL Copiar]** ![Copiar](../../assets/copy.png) junto al ID de la secuencia de datos.

También puede seleccionar el nombre de la secuencia de datos deseado y el ID de la secuencia de datos aparece en la columna derecha para que lo copie.

## Seleccione el ID de la secuencia de datos mediante la extensión de etiqueta del SDK web

Elija de una lista de flujos de datos disponibles o introduzca un ID de flujo de datos directamente cuando [configuración de la extensión de etiqueta](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Iniciar sesión en [experience.adobe.com](https://experience.adobe.com) usando sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensiones]**, luego haga clic en **[!UICONTROL Configurar]** en el [!UICONTROL SDK web de Adobe Experience Platform] Tarjeta de.
1. Busque el [!UICONTROL Datastreams] , luego seleccione el método deseado para determinar la secuencia de datos.
   * Si elige una de las listas, seleccione la zona protegida y la secuencia de datos de cada lista desplegable correspondiente.
   * Si introduce valores, introduzca el ID de flujo de datos deseado.
1. Clic **[!UICONTROL Guardar]** y, a continuación, publique los cambios.

Puede enviar datos a diferentes flujos de datos para los entornos de etiquetas de producción, ensayo y desarrollo.

## Seleccione el ID de la secuencia de datos mediante la biblioteca JavaScript del SDK web

Configure las variables `edgeConfigId` propiedad de cadena al ejecutar el `configure` comando. Esta propiedad es necesaria para todas las implementaciones de SDK web. Si omite esta propiedad, el SDK web no sabe a qué secuencia de datos enviar datos, lo que provoca que esos datos se pierdan de forma permanente.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```

Si configura varias instancias del SDK web en una sola página, debe configurar una diferente `edgeConfigId` para cada instancia.
