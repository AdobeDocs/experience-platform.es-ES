---
title: Representación de contenido personalizado
seo-title: Adobe Experience Platform Web SDK Representación de contenido personalizado
description: Obtenga información sobre cómo procesar contenido personalizado con el SDK web Experience Platform
seo-description: Obtenga información sobre cómo procesar contenido personalizado con el SDK web Experience Platform
keywords: personalization;renderDecisions;sendEvent;decisionScopes;result.decisions;
translation-type: tm+mt
source-git-commit: 0928dd3eb2c034fac14d14d6e53ba07cdc49a6ea
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---


# Descripción general de las opciones de personalización

Adobe Experience Platform [!DNL Web SDK] permite consultar las soluciones de personalización en Adobe, incluido Adobe Target. Existen dos modos de personalización: recuperar contenido que se puede procesar automáticamente y contenido que el desarrollador debe procesar. El SDK también ofrece funciones para [administrar el parpadeo](../personalization/manage-flicker.md).

## Representación automática del contenido

El SDK procesa automáticamente el contenido personalizado cuando envía un evento al servidor y lo establece `renderDecisions` como `true` opción en el evento.

```javascript
alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
});
```

El procesamiento de contenido personalizado es asíncrono, por lo que no debe darse por sentado cuándo una parte concreta del contenido forma parte de la página.

## Representación manual del contenido

Puede solicitar la lista de las decisiones que se devolverán como una promesa en el `sendEvent` comando especificando la `decisionScopes` opción. Un ámbito es una cadena que permite a la solución de personalización saber qué decisión desea.

```javascript
alloy("sendEvent",{
    xdm:{...},
    decisionScopes:['demo-1', 'demo-2']
  }).then(function(result){
    if (result.decisions){
      // Do something with the decisions.
    }
  });
```

Esto devolverá una lista de decisiones como un objeto JSON para cada decisión.

```json
{
  "decisions": [
    {
      "id": "TNT:123456:0",
      "scope": "demo-1",
      "items": [
        {
          "schema": "https://ns.adobe.com/personalization/html-content-item",
          "data": {
            "id": "11223344",
            "content": "<h2 style=\"color: yellow\">Scoped Decision for location \"alloy-location-1\"</h2>"
          }
        }
      ]
    },
    {
      "id": "TNT:654321:1",
      "scope": "demo-2",
      "items": [
        {
          "schema": "https://ns.adobe.com/personalization/json-content-item",
          "data": {
            "id": "4433221",
            "content": {
              "name":"Scoped decision in JSON"
            }
          }
        }
      ]
    }
  ]
}
```

>[!TIP]
>
> Si utiliza [!DNL Target], los ámbitos se convierten en mBoxes en el servidor, solo se solicitan de forma simultánea en lugar de individualmente. El mbox global siempre se envía.

### Recuperar contenido automático

Si desea `result.decisions` incluir las decisiones de procesamiento automático y NO tener a Alloy procesarlas automáticamente, puede establecer `renderDecisions` en `false`e incluir el ámbito especial `__view__`.
