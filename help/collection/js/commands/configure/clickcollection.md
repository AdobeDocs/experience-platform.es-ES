---
title: clickCollection
description: Ajuste la configuración de la colección de clics.
exl-id: 5a128b4a-4727-4415-87b4-4ae87a7e1750
source-git-commit: 46c8748e9ab972705b8283c174c285e571acb2ed
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%

---

# `clickCollection`

El objeto `clickCollection` contiene varias variables que le ayudan a controlar los datos de vínculos recopilados automáticamente. Utilice estas variables cuando desee incluir o excluir tipos de vínculos de la recopilación de datos. Es compatible con Web SDK versiones 2.25.0 o posteriores.

Esta variable requiere lo siguiente:

* [`clickCollectionEnabled`](clickcollectionenabled.md) debe estar habilitado.
* Si usa `clickCollection.filterClickDetails`, el método obsoleto [`onBeforeLinkClickSend`](onbeforelinkclicksend.md) debe estar vacío.
* La carga del evento debe contener un valor en `xdm.web.webPageDetails.name` en algún momento de la visita del visitante.

Si la implementación no cumple todos los requisitos anteriores, este objeto no hace nada.

Las siguientes propiedades están disponibles en el objeto `clickCollection`:

| Propiedad | Tipo | Descripción |
| --- | --- | --- |
| **`internalLinkEnabled`** | `boolean` | Determina si se realiza un seguimiento automático de los vínculos del dominio actual. Por ejemplo, `https://example.com/index.html` a `https://example.com/product.html` se consideraría un vínculo interno. |
| **`downloadLinkEnabled`** | `boolean` | Determina si la biblioteca realiza un seguimiento de los vínculos que se pueden considerar descargas en función de la propiedad [`downloadLinkQualifier`](downloadlinkqualifier.md). |
| **`externalLinkEnabled`** | `boolean` | Determina si los vínculos a dominios externos se rastrean automáticamente. Por ejemplo, `https://example.com` a `https://example.net` se consideraría un vínculo externo. |
| **`eventGroupingEnabled`** | `boolean` | Determina si la biblioteca de espera hasta el siguiente evento de &quot;vista de página&quot; para enviar datos de seguimiento de vínculos. La biblioteca considera un evento como una &quot;vista de página&quot; cuando los siguientes elementos están incluidos en la carga útil:<ul><li>`xdm.web.webPageDetails.name` contiene un valor de cadena</li><li>`xdm.web.webPageDetails.pageViews.value` es mayor que `0`</li></ul>Cuando se carga el evento &quot;vista de página&quot;, la biblioteca combina los datos de seguimiento de vínculos almacenados con el resto de los datos de ese evento. Al habilitar esta opción, se reduce el número total de eventos que se envían a Adobe. Si `internalLinkEnabled` está deshabilitado, esta variable no hace nada. |
| **`sessionStorageEnabled`** | `boolean` | Determina si los datos de seguimiento de vínculos se almacenan en el almacenamiento de la sesión en lugar de en las variables locales. Si `internalLinkEnabled` o `eventGroupingEnabled` están deshabilitados, esta variable no hace nada.<br>Adobe recomienda habilitar esta variable al usar `eventGroupingEnabled` fuera de aplicaciones de una sola página. Si `eventGroupingEnabled` está habilitado mientras que `sessionStorageEnabled` está deshabilitado, hacer clic en una nueva página resulta en la pérdida de datos de seguimiento de vínculos, ya que no se conservan en el almacenamiento de sesión. Dado que las aplicaciones de una sola página no suelen desplazarse a una página nueva, no se requiere almacenamiento de sesión para las páginas de SPA. |
| **`filterClickDetails`** | `function` | Una función de llamada de retorno que proporciona controles completos sobre los datos de seguimiento de vínculos que recopila. Puede utilizar esta función de llamada de retorno para alterar, ofuscar o cancelar el envío de datos de seguimiento de vínculos. Esta llamada de retorno es útil cuando desea omitir información específica, como información de identificación personal dentro de los vínculos. |

Si no establece este objeto en el comando [`configure`](overview.md), la configuración predeterminada de este objeto depende del valor de [`clickCollectionEnabled`](clickcollectionenabled.md):

* `internalLinkEnabled`: coincide con `clickCollectionEnabled`
* `downloadLinkEnabled`: coincide con `clickCollectionEnabled`
* `externalLinkEnabled`: coincide con `clickCollectionEnabled`
* `eventGroupingEnabled`: el valor predeterminado es `false`; debe habilitarse explícitamente
* `sessionStorageEnabled`: el valor predeterminado es `false`; debe habilitarse explícitamente
* `filterClickDetails`: no contiene una función; debe estar registrado explícitamente

>[!TIP]
>
>Adobe recomienda habilitar `eventGroupingEnabled` cuando `internalLinkEnabled` esté habilitado, ya que reduce el número de eventos que se contabilizan para el uso contractual.

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

## Configuración de la colección de clics para la extensión de etiquetas Web SDK

Estas opciones se pueden configurar en la extensión de etiquetas Web SDK con [Opciones de configuración de recopilación de datos](/help/tags/extensions/client/web-sdk/configure/data-collection.md).
