---
title: Asignación manual de variables en Adobe Analytics
seo-title: Asignación manual de variables en Adobe Analytics con SDK web
description: Cómo asignar variables manualmente a Adobe Analytics mediante reglas de procesamiento
seo-description: Asignación manual de variables a Adobe Analytics mediante reglas de procesamiento con el SDK web
keywords: adobe analytics;analytics;variables;mapping variables;map variables;contextData;context Data;Processing rules;rules;xdm;schema;
translation-type: tm+mt
source-git-commit: 206b5addd6baf5a120b469b21313ee86ac1fe53b
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 35%

---


# Asignación manual de variables en Adobe Analytics

Adobe Experience Platform [!DNL Web SDK] puede asignar ciertas variables automáticamente, pero las variables personalizadas deben asignarse manualmente.

For XDM data that is not automatically mapped to [!DNL Analytics], you can use [context data](https://docs.adobe.com/content/help/es-ES/analytics/implementation/vars/page-vars/contextdata.html) to match your [schema](https://docs.adobe.com/content/help/es-ES/experience-platform/xdm/schema/composition.html). A continuación, se puede asignar a [!DNL Analytics] mediante reglas [de procesamiento](https://docs.adobe.com/content/help/es-ES/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html) para rellenar [!DNL Analytics] variables.

Además, puede utilizar un conjunto predeterminado de acciones y listas de productos para enviar o recuperar datos con el SDK web de Adobe Experience Platform. Para ello, consulte [Productos](https://docs.adobe.com/content/help/es-ES/experience-platform/edge/implement/commerce.html).

## Datos de contexto

To be used by [!DNL Analytics], XDM data is flattened using dot notation and made available as `contextData`. La siguiente lista de pares de valores muestra un ejemplo de `context data`:

```json
{
  "bh": "900",
  "bw": "1680",
  "c": "24",
  "c.a.d.key.[0]": "value1",
  "c.a.d.key.[1]": "value2",
  "c.a.d.object.key1": "value1",
  "c.a.d.object.key2.[0]": "value2",
  "c.a.x.environment.browserdetails.javascriptenabled": "true",
  "c.a.x.environment.type": "browser",
  "cust_hit_time_gmt": "1579781427",
  "g": "http://example.com/home",
  "gn": "home",
  "j": "1.8.5",
  "k": "Y",
  "s": "1680x1050",
  "tnta": "218287:1:0|0,218287:1:0|2,218287:1:0|1,218287:1:0|32767,218287:1:0|1,218287:1:0|0,218287:1:0|1,218287:1:0|0,218287:1:0|1",
  "user_agent": "Mozilla/5.0 AppleWebKit/537.36 Safari/537.36",
  "v": "Y"
}
```

## Reglas de procesamiento

Se puede acceder a todos los datos recopilados por la red perimetral mediante [reglas de procesamiento](https://docs.adobe.com/content/help/es-ES/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html). In [!DNL Analytics], you can use processing rules to incorporate context data into [!DNL Analytics] variables.

For example, in the following rule, Adobe Analytics is set to populate **Internal Search terms (eVar2)** with the data associated with **a.x._atag.search.term(Context Data)**.

![](assets/examplerule.png)


## Esquema XDM

Adobe Experience Platform utiliza esquemas para describir la estructura de los datos de una manera consistente y reutilizable. Al definir los datos de manera consistente en todos los sistemas, resulta más fácil conservar el significado y, por lo tanto, obtener valor de los datos. [!DNL Analytics] los datos de contexto funcionan con la estructura definida por el esquema.

The following example shows how the [`event` command](https://docs.adobe.com/content/help/es-ES/experience-platform/edge/fundamentals/tracking-events.html) can be used with the `xdm` option to send and retrieve data with Adobe Experience Platform Web SDK. En este ejemplo, el comando `event` coincide con el [Esquema de detalles comerciales de ExperienceEvent](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md) para que se realice un seguimiento de productListItems `name` y de los valores de `SKU`:


```javascript
alloy("event",{
  "xdm":{
    "commerce":{
      "productViews":{
        "value":1
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"Large Field Hat",
      },
      {
        "SKU":"HT104",
        "name":"Small Field Hat",
      }
    ]
  }
});
```

Para obtener más información sobre el seguimiento de eventos con Adobe Experience Platform [!DNL Web SDK], consulte [Seguimiento de eventos](https://docs.adobe.com/content/help/es-ES/experience-platform/edge/fundamentals/tracking-events.html).
