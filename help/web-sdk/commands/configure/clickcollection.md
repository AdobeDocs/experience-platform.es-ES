---
title: clickCollection
description: Ajuste la configuración de la colección de clics.
exl-id: 5a128b4a-4727-4415-87b4-4ae87a7e1750
source-git-commit: d3be2a9e75514023a7732a1c3460f8695ef02e68
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# `clickCollection`

El objeto `clickCollection` contiene varias variables que le ayudan a controlar los datos de vínculos recopilados automáticamente. Utilice estas variables cuando desee incluir o excluir tipos de vínculos de la recopilación de datos.

Requiere que [`clickCollectionEnabled`](clickcollectionenabled.md) esté habilitado.

Es compatible con el SDK web 2.25.0 o posterior.

Las siguientes variables están disponibles en el objeto `clickCollection`:

* **`clickCollection.internalLinkEnabled`**: un booleano que determina si los vínculos del dominio actual se rastrean automáticamente. Por ejemplo, `https://example.com/index.html` a `https://example.com/product.html`.
* **`clickCollection.downloadLinkEnabled`**: un booleano que determina si la biblioteca realiza un seguimiento de los vínculos que se califican como descargas en función de la propiedad [`downloadLinkQualifier`](downloadlinkqualifier.md).
* **`clickCollection.externalLinkEnabled`**: un booleano que determina si se realiza un seguimiento automático de los vínculos a dominios externos. Por ejemplo, `https://example.com` a `https://example.net`.
* **`clickCollection.eventGroupingEnabled`**: un booleano que determina si la biblioteca espera hasta la siguiente página para enviar los datos de seguimiento de vínculos. Cuando se cargue la página siguiente, combine los datos de seguimiento de vínculos con el evento de carga de página. Al habilitar esta opción, se reduce el número de eventos que se envían al Adobe. Si `internalLinkEnabled` está deshabilitado, esta variable no hace nada.
* **`clickCollection.sessionStorageEnabled`**: un booleano que determina si los datos de seguimiento de vínculos se almacenan en el almacenamiento de sesión en lugar de en las variables locales. Si `internalLinkEnabled` o `eventGroupingEnabled` están deshabilitados, esta variable no hace nada.

  El Adobe recomienda habilitar esta variable cuando se use `eventGroupingEnabled` fuera de aplicaciones de una sola página. Si `eventGroupingEnabled` está habilitado mientras que `sessionStorageEnabled` está deshabilitado, hacer clic en una nueva página resulta en la pérdida de datos de seguimiento de vínculos, ya que no se conservan en el almacenamiento de sesión. SPA Dado que las aplicaciones de una sola página no suelen navegar a una nueva página, no se requiere almacenamiento de sesión para las páginas de la página de la página de la página de la página de la página de la página de la página de la página de la página de la página de la página de la página de la página de inicio
* **`filterClickDetails`**: función de devolución de llamada que proporciona controles completos sobre los datos de seguimiento de vínculos que recopila. Puede utilizar esta función de llamada de retorno para alterar, ofuscar o cancelar el envío de datos de seguimiento de vínculos. Esta llamada de retorno es útil cuando desea omitir información específica, como información de identificación personal dentro de los vínculos.

## Haga clic en Configuración de colección mediante la extensión de etiqueta del SDK web

Seleccione cualquiera de las siguientes opciones al [configurar la extensión de etiqueta](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md):

* [!UICONTROL Recopilar vínculos internos]
   * [!UICONTROL Opciones de agrupación de eventos]:
      * [!UICONTROL Sin agrupación de eventos]
      * [!UICONTROL Agrupación de eventos mediante el almacenamiento de sesión]
      * [!UICONTROL Agrupación de eventos con objeto local]
* [!UICONTROL Recopilar vínculos externos]
* [!UICONTROL Recopilar vínculos de descarga]
* [!UICONTROL Propiedades de clic en filtro]

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Extensions]** y, a continuación, haga clic en **[!UICONTROL Configure]** en la tarjeta de [!UICONTROL Adobe Experience Platform Web SDK].
1. Desplácese hacia abajo hasta la sección [!UICONTROL Recopilación de datos] y, a continuación, seleccione la configuración de recopilación de clics que desee.
1. Haz clic en **[!UICONTROL Guardar]** y después publica los cambios.

La llamada de retorno [!UICONTROL Filter click properties] abre un editor de código personalizado que le permite insertar el código deseado. En el editor de código, tiene acceso a las siguientes variables:

* **`content.clickedElement`**: el elemento DOM donde se hizo clic.
* **`content.pageName`**: nombre de página cuando se produjo el clic.
* **`content.linkName`**: nombre del vínculo donde se hizo clic.
* **`content.linkRegion`**: región del vínculo donde se hizo clic.
* **`content.linkType`**: tipo de vínculo (de salida, de descarga, etc.).
* **`content.linkURL`**: dirección URL de destino del vínculo donde se hizo clic.
* **`return true`**: salga inmediatamente de la llamada de retorno con los valores de las variables actuales.
* **`return false`**: salga inmediatamente de la llamada de retorno y anule la recopilación de datos.

Se puede usar cualquier variable definida fuera de `content`, pero no se incluye en la carga útil enviada al Adobe.

## Haga clic en Configuración de la colección mediante la biblioteca JavaScript del SDK web

Establezca las variables deseadas dentro del objeto `clickCollection` al ejecutar el comando [`configure`](overview.md). Si no se establece, la configuración predeterminada de este objeto depende del valor de [`clickCollectionEnabled`](clickcollectionenabled.md).

* `internalLinkEnabled`: coincide con `clickCollectionEnabled`
* `downloadLinkEnabled`: coincide con `clickCollectionEnabled`
* `externalLinkEnabled`: coincide con `clickCollectionEnabled`
* `eventGroupingEnabled`: el valor predeterminado es `false`; debe habilitarse explícitamente
* `sessionStorageEnabled`: el valor predeterminado es `false`; debe habilitarse explícitamente
* `filterClickDetails`: no contiene una función; debe estar registrado explícitamente

>[!TIP]
>Adobe recomienda habilitar `eventGroupingEnabled` cuando `internalLinkEnabled` está habilitado, ya que reduce el número de eventos que se contabilizan para el uso contractual.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
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
