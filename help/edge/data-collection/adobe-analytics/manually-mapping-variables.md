---
title: Asignación manual de variables de Adobe Analytics en el SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo asignar variables manualmente a Adobe Analytics mediante reglas de procesamiento en el SDK web de Experience Platform.
seo-description: Asignación manual de variables a Adobe Analytics mediante reglas de procesamiento con el SDK web
keywords: adobe analytics;analytics;variables;asignación de variables;asignación de variables;contextData;datos de contexto;reglas de procesamiento;reglas;xdm;esquema;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 33%

---


# Asignación manual de variables en Adobe Analytics

Adobe Experience Platform [!DNL Web SDK] puede asignar ciertas variables automáticamente, pero las variables personalizadas deben asignarse manualmente.

Para datos XDM que no se asignan automáticamente a [!DNL Analytics], puede utilizar [datos de contexto](https://docs.adobe.com/content/help/es-ES/analytics/implementation/vars/page-vars/contextdata.html) para coincidir con su [esquema](https://docs.adobe.com/content/help/es-ES/experience-platform/xdm/schema/composition.html). A continuación, se puede asignar a [!DNL Analytics] mediante [reglas de procesamiento](https://docs.adobe.com/content/help/es-ES/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html) para rellenar variables [!DNL Analytics].

Además, puede utilizar un conjunto predeterminado de acciones y listas de productos para enviar o recuperar datos con el SDK web de Adobe Experience Platform. Para ello, consulte [Productos](https://docs.adobe.com/content/help/es-ES/experience-platform/edge/implement/commerce.html).

## Datos de contexto

Para ser utilizados por [!DNL Analytics], los datos XDM se acoplan con notación de puntos y se ponen a disposición como `contextData`. La siguiente lista de pares de valores muestra un ejemplo de `context data`:

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

Se puede acceder a todos los datos recopilados por la red perimetral mediante [reglas de procesamiento](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html). En [!DNL Analytics], puede utilizar reglas de procesamiento para incorporar datos de contexto en variables [!DNL Analytics].

Por ejemplo, en la regla siguiente, Adobe Analytics está configurado para rellenar **términos de búsqueda interna (eVar2)** con los datos asociados con **a.x._atag.search.term(Context Data)**.

![](assets/examplerule.png)


## Esquema XDM

Adobe Experience Platform utiliza esquemas para describir la estructura de los datos de una manera consistente y reutilizable. Al definir los datos de manera consistente en todos los sistemas, resulta más fácil conservar el significado y, por lo tanto, obtener valor de los datos. [!DNL Analytics] los datos de contexto funcionan con la estructura definida por el esquema.

El siguiente ejemplo muestra cómo se puede utilizar el comando [`event`](https://docs.adobe.com/content/help/es-ES/experience-platform/edge/fundamentals/tracking-events.html) con la opción `xdm` para enviar y recuperar datos con el SDK web de Adobe Experience Platform. En este ejemplo, el comando `event` coincide con el [Esquema de detalles comerciales de ExperienceEvent](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md) para que se realice un seguimiento de productListItems `name` y de los valores de `SKU`:


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

Para obtener más información sobre el seguimiento de eventos con Adobe Experience Platform [!DNL Web SDK], consulte [eventos de seguimiento](https://docs.adobe.com/content/help/en/experience-platform/edge/fundamentals/tracking-events.html).
