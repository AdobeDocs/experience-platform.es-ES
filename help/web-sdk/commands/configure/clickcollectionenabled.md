---
title: clickCollectionEnabled
description: Obtenga información sobre cómo configurar Web SDK para determinar si los datos de clics en vínculos se recopilan automáticamente.
exl-id: e91b5bc6-8880-4884-87f9-60ec8787027e
source-git-commit: fdb809ea86e91a98b45877c99c3e64d7c49d1cd5
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 0%

---

# `clickCollectionEnabled`

La propiedad `clickCollectionEnabled` es un booleano que determina si Web SDK recopila automáticamente los datos del vínculo. Si no establece esta variable, su valor predeterminado es `true`, lo que significa que los datos de seguimiento de vínculos se recopilan automáticamente de manera predeterminada. Es útil establecer esta propiedad en `false` en los casos en que prefiera rastrear los datos de vínculos manualmente.

Cuando `clickCollectionEnabled` está habilitado, los siguientes elementos XDM se rellenan automáticamente con datos:

* `xdm.web.webInteraction.name`
* `xdm.web.webInteraction.type`
* `xdm.web.webInteraction.URL`

Los vínculos internos, de descarga y de salida se rastrean automáticamente de forma predeterminada cuando este booleano está habilitado. Si desea tener más control sobre el seguimiento automático de vínculos, Adobe recomienda usar el objeto [`clickCollection`](clickcollection.md).

## Compatibilidad con elementos [!DNL Shadow DOM] abiertos

Web SDK admite el rastreo automático de clics para los vínculos dentro de **elementos DOM en la sombra abiertos**.

Muchos sitios web modernos utilizan [componentes web](https://developer.mozilla.org/en-US/docs/Web/Web_Components) para generar elementos de interfaz de usuario encapsulados y reutilizables. Estos componentes suelen utilizar una tecnología denominada [**Shadow DOM**](https://developer.mozilla.org/en-US/docs/Web/API/Web_components/Using_shadow_DOM) para mantener su estructura y estilos internos separados del resto de la página.

Existen dos tipos de DOM en la sombra:

* **Abrir DOM en la sombra:** JavaScript que se ejecuta en la página tiene acceso a la estructura interna. Esto significa que otros scripts pueden interactuar con el contenido del componente o inspeccionarlo.
* **DOM de sombra cerrada:** La estructura interna está oculta a JavaScript fuera del componente, por lo que no es accesible para su seguimiento o manipulación.

Web SDK realiza automáticamente un seguimiento de los clics en `<a>` y `<area>` elementos dentro de **DOM sombreados abiertos**, tal como lo hace para los vínculos del documento principal. Esto garantiza que los clics en vínculos dentro de los componentes web que usan open [!DNL Shadow DOM] se incluyan en los datos de análisis. No se rastrearán los clics dentro de **DOM en la sombra cerrados**, ya que su estructura interna está oculta del código de JavaScript que funciona fuera del componente.

## Lógica de seguimiento de vínculos automática

Web SDK realiza un seguimiento de todos los clics en `<a>` y `<area>` elementos de HTML si no tiene un atributo `onClick`. Los clics se capturan con un detector de eventos de clic [capture](https://www.w3.org/TR/uievents/#capture-phase) que está adjunto al documento. Cuando se hace clic en un vínculo válido, se ejecuta la siguiente lógica en orden:

1. Si el vínculo coincide con criterios basados en valores de [`downloadLinkQualifier`](downloadlinkqualifier.md), o si el vínculo contiene un atributo HTML `download`, `xdm.web.webInteraction.type` se establece en `"download"` (si `clickCollection.downloadLinkEnabled` está habilitado).
1. Si el dominio de destino del vínculo difiere del actual `window.location.hostname`, `xdm.web.webInteraction.type` se establece en `"exit"` (si `clickCollection.exitLinkEnabled` está habilitado).
1. Si el vínculo no cumple los requisitos para `"download"` o `"exit"`, `xdm.web.webInteraction.type` se establece en `"other"`.

En todos los casos, `xdm.web.webInteraction.name` se establece en la etiqueta de texto del vínculo y `xdm.web.webInteraction.URL` se establece en la dirección URL de destino del vínculo. Si también desea establecer el nombre del vínculo en la dirección URL, puede anular este campo XDM con la llamada de retorno `filterClickDetails` en el objeto `clickCollection`.

## Habilitar el seguimiento automático de vínculos mediante la extensión de etiquetas Web SDK {#tag-extension}

La extensión de etiqueta administra automáticamente esta variable; no es necesario configurarla explícitamente. Si se selecciona alguna de las siguientes opciones al [configurar la extensión de etiqueta](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md), se recopilarán los datos de seguimiento de vínculos aplicables:

* [!UICONTROL Recopilar clics en vínculos internos]
* [!UICONTROL Recopilar clics en vínculos externos]
* [!UICONTROL Recopilar clics en vínculos de descarga]

Consulte [`clickCollection`](clickcollection.md) para obtener más información.

## Habilitar el seguimiento automático de vínculos mediante la biblioteca JavaScript de Web SDK {#library}

Establezca el booleano `clickCollectionEnabled` al ejecutar el comando `configure`. Si omite esta propiedad al configurar Web SDK, el valor predeterminado es `true`. Establezca este valor en `false` si prefiere establecer `xdm.web.webInteraction.type` y `xdm.web.webInteraction.value` manualmente.

```js
alloy(configure, {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: false
});
```
