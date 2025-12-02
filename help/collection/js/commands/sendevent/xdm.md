---
title: xdm
description: Aprenda a enviar datos a Adobe a través del objeto alineado con el esquema XDM.
exl-id: 1d8ef191-aed6-4c8b-a1fd-614bd8ed73da
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 0%

---

# `xdm`

El objeto `xdm` contiene la carga de datos enviada a Adobe. Los campos establecidos dentro de este objeto se asignan directamente a los elementos definidos en el esquema del conjunto de datos.

Adobe Experience Platform utiliza esquemas para describir la estructura de los datos de una manera uniforme y reutilizable. Al definir los datos de forma coherente en todos los sistemas, resulta más fácil conservar el significado y, por lo tanto, obtener valor de los datos.

Establezca el objeto `xdm` al ejecutar el comando `sendEvent`. Asegúrese de que la jerarquía de este objeto coincida con el esquema del conjunto de datos configurado. Puede incluir el objeto `xdm` y el objeto [`data`](data.md) en el mismo comando `sendEvent`.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference)
});
```

El ejemplo siguiente utiliza el [grupo de campos de esquema Detalles de Commerce](/help/xdm/field-groups/event/commerce-details.md):

```javascript
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "productViews":{
        "value":1
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"Large field hat",
      },
      {
        "SKU":"HT104",
        "name":"Small field hat",
      }
    ]
  }
});
```

## Usar el objeto `xdm` mediante la extensión de etiqueta Web SDK

El objeto `xdm` está disponible como [elemento de datos de variable](/help/tags/extensions/client/web-sdk/data-element-types.md#variable) o [elemento de datos de objeto XDM](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object) al usar la extensión de etiqueta de Web SDK. Adobe recomienda utilizar un elemento de datos variable en la mayoría de los casos.
