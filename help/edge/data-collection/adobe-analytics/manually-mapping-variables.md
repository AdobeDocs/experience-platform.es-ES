---
title: Asignación manual de variables de Adobe Analytics en el SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo asignar manualmente variables a Adobe Analytics mediante reglas de procesamiento en el SDK web de Experience Platform.
seo-description: Manually map variables into Adobe Analytics using processing rules with Web SDK
keywords: adobe analytics;analytics;variables;variables de asignación;variables de asignación;contextData;datos de contexto;reglas de procesamiento;reglas;xdm;schema;
exl-id: 395050c1-8d39-4da8-acea-6e618ed662dd
source-git-commit: 3bf13c3f5ac0506ac88effc56ff68758deb5f566
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 12%

---

# Asignación manual de variables en Adobe Analytics

Adobe Experience Platform [!DNL Web SDK] puede asignar determinadas variables automáticamente, pero las variables personalizadas deben asignarse manualmente.

Para datos XDM que no se asignan automáticamente a [!DNL Analytics], puede utilizar [datos de contexto](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/contextdata.html?lang=es) para que coincida con su [esquema](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=es). A continuación, se puede asignar a [!DNL Analytics] usando [reglas de procesamiento](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html?lang=es) para rellenar [!DNL Analytics] variables.

Además, puede utilizar un conjunto predeterminado de acciones y listas de productos para enviar o recuperar datos con el SDK web de Adobe Experience Platform. Para ello, consulte [Recopilar información comercial y de productos](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/collect-commerce-data.html).

## Datos de contexto

Para que lo utilice [!DNL Analytics], los datos XDM se acoplan con notación de puntos y se ponen a disposición como `contextData`. La siguiente lista de pares de valores muestra un ejemplo de lo que `context data` tiene el siguiente aspecto cuando se aplana:

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

Se puede acceder a todos los datos recopilados por la red perimetral mediante [reglas de procesamiento](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html?lang=es). Entrada [!DNL Analytics], puede utilizar reglas de procesamiento para incorporar datos de contexto en [!DNL Analytics] variables.

Por ejemplo, en la regla siguiente, Adobe Analytics está configurado para rellenar **Términos de búsqueda interna (eVar 2)** con los datos asociados con **a.x._atag.search.term(Context Data)**.

![Imagen de la interfaz de usuario de Analytics que muestra un ejemplo de regla.](assets/examplerule.png)

## Esquema XDM

Adobe Experience Platform utiliza esquemas para describir la estructura de los datos de una manera uniforme y reutilizable. Al definir los datos de forma coherente en todos los sistemas, resulta más fácil conservar el significado y, por lo tanto, obtener valor de los datos. [!DNL Analytics] los datos de contexto funcionan con la estructura definida por el esquema.

El siguiente ejemplo muestra cómo se puede usar la función [`event` mando](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=es) se puede utilizar con el `xdm` para enviar y recuperar datos con el SDK web de Adobe Experience Platform. En este ejemplo, el comando `event` coincide con el [Esquema de detalles comerciales de ExperienceEvent](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md) para que se realice un seguimiento de productListItems `name` y de los valores de `SKU`:


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

Para obtener más información sobre el seguimiento de eventos con Adobe Experience Platform [!DNL Web SDK], consulte [Seguimiento de eventos](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=es).
