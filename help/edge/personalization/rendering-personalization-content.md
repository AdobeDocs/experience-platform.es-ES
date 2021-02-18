---
title: Representar contenido personalizado con el SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo procesar contenido personalizado con el SDK web de Adobe Experience Platform.
keywords: personalización;decisionesDeProcesamiento;enviarEvento;ámbitosDeDecisión;resultados.decisiones;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---


# Representar contenido personalizado

Adobe Experience Platform [!DNL Web SDK] permite consultar las soluciones de personalización en Adobe, incluido Adobe Target. Existen dos modos de personalización: recuperar contenido que se puede procesar automáticamente y contenido que el desarrollador debe procesar. El SDK también proporciona funciones para [administrar el parpadeo](../personalization/manage-flicker.md).

## Representación automática del contenido

El SDK procesa automáticamente el contenido personalizado cuando envía un evento al servidor y establece `renderDecisions` en `true` como una opción en el evento.

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

Puede solicitar la lista de decisiones que se devolverán como una promesa en el comando `sendEvent` especificando la opción `decisionScopes`. Un ámbito es una cadena que permite a la solución de personalización saber qué decisión desea.

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
> Si utiliza [!DNL Target], los ámbitos se convierten en mBoxes en el servidor, solo se solicitan a la vez en lugar de individualmente. El mbox global siempre se envía.

### Recuperar contenido automático

Si desea que `result.decisions` incluya las decisiones que se pueden procesar automáticamente y NO que Alloy las procese automáticamente, puede establecer `renderDecisions` en `false` e incluir el ámbito especial `__view__`.
