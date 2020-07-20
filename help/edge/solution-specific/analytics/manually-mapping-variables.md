---
title: Asignación manual de variables en Analytics
seo-title: Asignación manual de variables en Analytics con SDK web
description: Asignación manual de variables a Analytics mediante reglas de procesamiento
seo-description: asignar manualmente variables a Analytics mediante reglas de procesamiento con SDK web
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 11%

---


# Asignación manual de variables en Analytics

El Adobe Experience Platform (AEP) [!DNL Web SDK] puede asignar ciertas variables automáticamente, pero las variables personalizadas deben asignarse manualmente.

Para datos XDM a los que no se asigna automáticamente [!DNL Analytics], puede utilizar datos [de](https://docs.adobe.com/content/help/es-ES/analytics/implementation/vars/page-vars/contextdata.html) contexto para coincidir con el [esquema](https://docs.adobe.com/content/help/es-ES/experience-platform/xdm/schema/composition.html). A continuación, se puede asignar a [!DNL Analytics] mediante reglas [de procesamiento](https://docs.adobe.com/content/help/es-ES/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html) para rellenar [!DNL Analytics] variables.

Además, puede utilizar un conjunto predeterminado de acciones y listas de productos para enviar o recuperar datos con el AEP [!DNL Web SDK]. Para ello, consulte [Productos](https://docs.adobe.com/content/help/en/experience-platform/edge/implement/commerce.html).

## Datos de contexto

Para su uso por [!DNL Analytics], los datos XDM se acoplan con notación de puntos y se ponen a disposición como `contextData`. La siguiente lista de pares de valores muestra un ejemplo de `context data`:

```javascript
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

Se puede acceder a todos los datos recopilados por la red Edge mediante reglas [de procesamiento](https://docs.adobe.com/content/help/es-ES/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html). En [!DNL Analytics], puede utilizar reglas de procesamiento para incorporar datos de contexto en [!DNL Analytics] variables.

Por ejemplo, en la regla siguiente, Analytics está configurado para rellenar los términos de búsqueda **interna (eVar2)** con los datos asociados con **a.x_atag.search.term(Context Data)**.

![](assets/examplerule.png)


## Esquema XDM

[!DNL Experience Platform] utiliza esquemas para describir la estructura de los datos de una manera consistente y reutilizable. Al definir los datos de manera consistente en todos los sistemas, resulta más fácil conservar el significado y, por lo tanto, obtener valor de los datos. [!DNL Analytics] los datos de contexto funcionan con la estructura definida por el esquema.

El siguiente ejemplo muestra cómo se puede utilizar el [`event` comando](https://docs.adobe.com/content/help/en/experience-platform/edge/fundamentals/tracking-events.html) con la `xdm` opción para enviar y recuperar datos con AEP [!DNL Web SDK]. En este ejemplo, el `event` comando coincide con el Esquema [Detalles del comercio de](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md) ExperienceEvent para que se realice un seguimiento de productListItems `name` y `SKU` valores:


```
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

Para obtener más información sobre el seguimiento de eventos con AEP [!DNL Web SDK], consulte eventos [](https://docs.adobe.com/content/help/en/experience-platform/edge/fundamentals/tracking-events.html)de seguimiento.
