---
title: xdm
description: Aprenda a enviar datos al Adobe a través del objeto alineado con el esquema XDM.
exl-id: 1d8ef191-aed6-4c8b-a1fd-614bd8ed73da
source-git-commit: 8c652e96fa79b587c7387a4053719605df012908
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---

# `xdm`

El objeto `xdm` contiene la carga de datos enviada al Adobe. Los campos establecidos dentro de este objeto se asignan directamente a los elementos definidos en el esquema del conjunto de datos.

Adobe Experience Platform utiliza esquemas para describir la estructura de los datos de una manera uniforme y reutilizable. Al definir los datos de forma coherente en todos los sistemas, resulta más fácil conservar el significado y, por lo tanto, obtener valor de los datos.

Este objeto tiene un límite máximo de 32 KB.

## Configuración del objeto XDM mediante la extensión del SDK web

Establezca el objeto **[!UICONTROL XDM]** dentro de las acciones de una regla de etiqueta. El [objeto XDM](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object) proporciona una interfaz intuitiva para asignar otros elementos de datos a sus respectivos campos XDM.

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Reglas]** y luego seleccione la regla que desee.
1. En [!UICONTROL Acciones], seleccione una acción existente o cree una acción.
1. Establezca el campo desplegable [!UICONTROL Extension] en **[!UICONTROL SDK web de Adobe Experience Platform]** y establezca [!UICONTROL Action Type] en **[!UICONTROL Send event]**.
1. Proporcione el elemento de datos que contiene el objeto deseado en el campo **[!UICONTROL XDM]**.
1. Haga clic en **[!UICONTROL Conservar cambios]** y, a continuación, ejecute el flujo de trabajo de publicación.

## Configuración del objeto XDM mediante la biblioteca JavaScript del SDK web

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
