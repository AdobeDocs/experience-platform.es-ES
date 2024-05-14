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

El `xdm` contiene la carga útil de datos enviada al Adobe. Los campos establecidos dentro de este objeto se asignan directamente a los elementos definidos en el esquema del conjunto de datos.

Adobe Experience Platform utiliza esquemas para describir la estructura de los datos de una manera uniforme y reutilizable. Al definir los datos de forma coherente en todos los sistemas, resulta más fácil conservar el significado y, por lo tanto, obtener valor de los datos.

Este objeto tiene un límite máximo de 32 KB.

## Configuración del objeto XDM mediante la extensión del SDK web

Configure las variables **[!UICONTROL XDM]** dentro de las acciones de una regla de etiqueta. El [Objeto XDM](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object) proporciona una interfaz intuitiva para asignar otros elementos de datos a sus respectivos campos XDM.

1. Iniciar sesión en [experience.adobe.com](https://experience.adobe.com) usando sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Reglas]**, luego seleccione la regla que desee.
1. En [!UICONTROL Acciones], seleccione una acción existente o cree una acción.
1. Configure las variables [!UICONTROL Extensión] campo desplegable a **[!UICONTROL SDK web de Adobe Experience Platform]** y configure el [!UICONTROL Tipo de acción] hasta **[!UICONTROL Enviar evento]**.
1. Proporcione el elemento de datos que contiene el objeto deseado en la **[!UICONTROL XDM]** field.
1. Clic **[!UICONTROL Conservar cambios]**, luego ejecute el flujo de trabajo de publicación.

## Configure el objeto XDM mediante la biblioteca JavaScript del SDK web

Configure las variables `xdm` al ejecutar el `sendEvent` comando. Asegúrese de que la jerarquía de este objeto coincida con el esquema del conjunto de datos configurado. Puede incluir ambos `xdm` y el objeto [`data`](data.md) objeto en el mismo `sendEvent` comando.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference)
});
```

El ejemplo siguiente utiliza el [Grupo de campos del esquema Detalles de Commerce](/help/xdm/field-groups/event/commerce-details.md):

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
