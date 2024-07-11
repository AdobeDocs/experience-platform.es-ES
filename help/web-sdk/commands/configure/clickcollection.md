---
title: clickCollection
description: Ajuste la configuración de la colección de clics.
source-git-commit: 660d4e72bd93ca65001092520539a249eae23bfc
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 0%

---


# `clickCollection`

El `clickCollection` contiene varias variables que ayudan a controlar los datos de vínculos recopilados automáticamente. Utilice estas variables cuando desee incluir o excluir tipos de vínculos de la recopilación de datos.

Requiere [`clickCollectionEnabled`](clickcollectionenabled.md) para que esté habilitado.

Es compatible con el SDK web 2.25.0 o posterior.

Las siguientes variables están disponibles en el `clickCollection` objeto:

* **`clickCollection.internalLinkEnabled`**: Un booleano que determina si se realiza un seguimiento automático de los vínculos del dominio actual. Por ejemplo, `https://example.com/index.html` hasta `https://example.com/product.html`.
* **`clickCollection.downloadLinkEnabled`**: Un booleano que determina si la biblioteca realiza un seguimiento de los vínculos que se clasifican como descargas en función del [`downloadLinkQualifier`](downloadlinkqualifier.md) propiedad.
* **`clickCollection.externalLinkEnabled`**: Un booleano que determina si se realiza un seguimiento automático de los vínculos a dominios externos. Por ejemplo, `https://example.com` hasta `https://example.net`.
* **`clickCollection.eventGroupingEnabled`**: Un booleano que determina si la biblioteca de espera hasta la siguiente página para enviar datos de seguimiento de vínculos. Cuando se cargue la página siguiente, combine los datos de seguimiento de vínculos con el evento de carga de página. Al habilitar esta opción, se reduce el número de eventos que se envían al Adobe. If `internalLinkEnabled` está deshabilitada, esta variable no hace nada.
* **`clickCollection.sessionStorageEnabled`**: Un booleano que determina si los datos de seguimiento de vínculos se almacenan en el almacenamiento de sesión en lugar de en las variables locales. If `internalLinkEnabled` o `eventGroupingEnabled` están desactivadas, esta variable no hace nada.

  El Adobe recomienda habilitar esta variable al utilizar `eventGroupingEnabled`. If `eventGroupingEnabled` está habilitado mientras `sessionStorageEnabled` está deshabilitada, al hacer clic en una nueva página se pierden datos de seguimiento de vínculos, ya que no se conserva en el almacenamiento de sesión. Aunque es aceptable deshabilitar `sessionStorageEnabled` SPA en aplicaciones de una sola página, no es ideal para páginas que no sean de una sola página (no de una sola página).
* **`filterClickDetails`**: función de llamada de retorno que proporciona controles completos sobre los datos de seguimiento de vínculos que recopila. Puede utilizar esta función de llamada de retorno para alterar, ofuscar o cancelar el envío de datos de seguimiento de vínculos. Esta llamada de retorno es útil cuando desea omitir información específica, como información de identificación personal dentro de los vínculos.

## Haga clic en Configuración de colección mediante la extensión de etiqueta del SDK web

Seleccione el **[!UICONTROL Habilitar la recopilación de datos de clics]** casilla de verificación cuando [configuración de la extensión de etiqueta](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Al activar esta casilla de verificación, se muestran las siguientes opciones relacionadas con la recopilación de clics:

* [!UICONTROL Vínculos internos]
   * [!UICONTROL Habilitar agrupación de eventos]
   * [!UICONTROL Habilitar almacenamiento de sesión]
* [!UICONTROL Vínculos externos]
* [!UICONTROL Vínculos de descarga]
* [!UICONTROL Filtrar propiedades de clic]

1. Iniciar sesión en [experience.adobe.com](https://experience.adobe.com) usando sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensiones]**, luego haga clic en **[!UICONTROL Configurar]** en el [!UICONTROL SDK web de Adobe Experience Platform] Tarjeta de.
1. Desplácese hacia abajo hasta el [!UICONTROL Recopilación de datos] y, a continuación, seleccione la casilla de verificación **[!UICONTROL Habilitar la recopilación de datos de clics]**.
1. Seleccione la configuración de recopilación de clics que desee.
1. Clic **[!UICONTROL Guardar]** y, a continuación, publique los cambios.

El [!UICONTROL Filtrar propiedades de clic] callback abre un editor de código personalizado que le permite insertar el código deseado. En el editor de código, tiene acceso a las siguientes variables:

* **`content.clickedElement`**: el elemento DOM en el que se hizo clic.
* **`content.pageName`**: Nombre de la página cuando se produjo el clic.
* **`content.linkName`**: nombre del vínculo en el que se hizo clic.
* **`content.linkRegion`**: La región del vínculo en el que se hizo clic.
* **`content.linkType`**: el tipo de vínculo (de salida, de descarga, etc.).
* **`content.linkURL`**: URL de destino del vínculo en el que se hizo clic.
* **`return true`**: Salga inmediatamente de la llamada de retorno con los valores de variable actuales.
* **`return false`**: Salga inmediatamente de la llamada de retorno y interrumpa la recopilación de datos.

Cualquier variable definida fuera de `content` se pueden usar, pero no se incluyen en la carga útil enviada al Adobe.

## Haga clic en Configuración de la colección mediante la biblioteca JavaScript del SDK web

Configure las variables deseadas dentro de la variable `clickCollection` al ejecutar el [`configure`](overview.md) comando. Si no se establece, la configuración predeterminada de este objeto depende del valor de [`clickCollectionEnabled`](clickcollectionenabled.md).

* `internalLinkEnabled`: coincide `clickCollectionEnabled`
* `downloadLinkEnabled`: coincide `clickCollectionEnabled`
* `externalLinkEnabled`: coincide `clickCollectionEnabled`
* `eventGroupingEnabled`: el valor predeterminado es `false`; debe estar habilitado explícitamente
* `sessionStorageEnabled`: el valor predeterminado es `false`; debe estar habilitado explícitamente
* `filterClickDetails`: no contiene una función; debe registrarse explícitamente

>[!TIP]
>El Adobe recomienda activar `eventGroupingEnabled`, ya que ayuda a reducir el número de eventos que se contabilizan en el uso contractual.

```js
alloy("configure", {
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: true,
  clickCollection: {
    internalLinkEnabled: true,
    downloadLinkEnabled: true,
    externalLinkEnabled: true,
    eventGroupingEnabled: true,
    sessionStorageEnabled: true,
    filterClickDetails: function(content) {
      // If the link is a clickable telephone number, anonymize it
      if(content.linkUrl?.includes("tel:")) {
        content.linkName = content.linkUrl = "Phone number";
      }
      // If the link is an email address, anonymize it
      if(content.linkUrl?.includes("mailto:")) {
        content.linkName = content.linkUrl = "Email address";
      }
    }
  }
});
```
