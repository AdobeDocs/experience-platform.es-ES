---
title: Representación de contenido personalizado
seo-title: Adobe Experience Platform Web SDK Representación de contenido personalizado
description: Obtenga información sobre cómo procesar contenido personalizado con el SDK web de la plataforma de experiencia
seo-description: Obtenga información sobre cómo procesar contenido personalizado con el SDK web de la plataforma de experiencia
translation-type: tm+mt
source-git-commit: 4bff4b20ccc1913151aa1783d5123ffbb141a7d0
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---


# Información general sobre las opciones de personalización

El SDK web de Adobe Experience Platform admite consultas de las soluciones de personalización de Adobe, incluido Adobe Destinatario. Existen dos modos de personalización: recuperar contenido que se puede procesar automáticamente y contenido que el desarrollador debe procesar. El SDK también ofrece funciones para [administrar el parpadeo](../../edge/solution-specific/target/flicker-management.md).

## Representación automática de contenido

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

El procesamiento del contenido personalizado es asincrónico, por lo que no debe haber ninguna suposición cuando una parte concreta del contenido forma parte de la página.

## Representación manual de contenido

Puede solicitar la lista de decisiones para que se devuelvan como una promesa en el `event` comando utilizando `scopes`. Un ámbito es una cadena que permite a la solución de personalización saber qué decisión desea.

```javascript
alloy("sendEvent",{
    xdm:{...},
    scopes:['demo-1', 'demo-2']
  }).then(function(result){
    if (result.decisions){
      //do something with the decisions
    }
  })
```

Esto devolverá una lista de decisiones como un objeto JSON para cada decisión.

```javascript
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

{info}Si utiliza ámbitos de Destinatario para convertirse en mBoxes en el servidor, solo serán solicitudes a la vez en lugar de individualmente. El mbox global siempre se envía.
{info}

### Recuperar contenido automático

Si desea que el `result.decisions` informe incluya las decisiones de procesamiento automático, puede establecer `renderDecisions` en false e incluir el ámbito especial `__view__`
