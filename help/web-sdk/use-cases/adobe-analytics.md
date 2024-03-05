---
title: Envío de datos a Adobe Analytics mediante el SDK web
description: Obtenga información sobre cómo enviar datos a Adobe Analytics con el SDK web de Adobe Experience Platform.
keywords: adobe analytics;analytics;datos asignados;variables asignadas;
exl-id: b18d1163-9edf-4a9c-b247-cd1aa7dfca50
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 3%

---

# Envío de datos a Adobe Analytics mediante el SDK web

El SDK web de Adobe Experience Platform puede enviar datos a Adobe Analytics a través de Adobe Experience Platform Edge Network. Cuando los datos llegan a Edge Network, traducen el objeto XDM a un formato que Adobe Analytics comprende.

## Grupo de campos XDM

Con el fin de facilitar la captura de las métricas de Adobe Analytics más comunes, Adobe proporciona un grupo de campos orientado a Adobe Analytics que puede utilizar. Para obtener más información sobre este esquema, consulte [Grupo de campos de esquema de extensión completa de Adobe Analytics ExperienceEvent](/help/xdm/field-groups/event/analytics-full-extension.md).

## Asignación de variables

La red perimetral asigna automáticamente muchas variables XDM. Consulte [Asignación de variables de Analytics en la red perimetral](https://experienceleague.adobe.com/docs/analytics/implementation/aep-edge/variable-mapping.html?lang=es) en la guía de implementación de Adobe Analytics para obtener una lista completa de variables asignadas automáticamente.

Todas las variables que no se asignan automáticamente están disponibles como [Variables de datos de contexto](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/contextdata.html?lang=es). A continuación, puede utilizar [Reglas de procesamiento](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/c-processing-rules-configuration/processing-rules-about.html) para asignar variables de datos de contexto a variables de Analytics. Por ejemplo, si tuviera un esquema XDM personalizado con el siguiente aspecto:

```js
{
  key:value,
  object:{
    key1:value1,
    key2:value2
  },
  array:[
    "v0",
    "v1",
    "v2"
  ],
  arrayofobjects:[
    {
      obj1key:objval0
    },
    {
      obj2key:objval1
    }
  ]
}
```

A continuación, estas serían las claves de datos de contexto disponibles en la interfaz de reglas de procesamiento:

```javascript
a.x.key //value
a.x.object.key1 //value1
a.x.object.key2 //value2
a.x.array.0 //v0
a.x.array.1 //v1
a.x.array.2 //v2
a.x.arrayofobjects.0.obj1key //objval0
a.x.arrayofobjects.1.obj2key //objval1
```

>[!NOTE]
>
>Con la colección Edge Network, todos los eventos se envían a Analytics y a cualquier otro servicio que haya configurado para su flujo de datos. Por ejemplo, si tiene Analytics y Target configurados como servicios y realiza llamadas independientes para la personalización y para Analytics, ambos eventos se envían a Analytics y a Target. Estos eventos se registran en los informes de Analytics y pueden afectar a métricas como la tasa de salida hacia otro sitio.

## Vistas de página y llamadas de seguimiento de vínculos

El AppMeasurement de Adobe Analytics utiliza llamadas de método independientes para las vistas de página ([`t()` método](https://experienceleague.adobe.com/docs/analytics/implementation/vars/functions/t-method.html)) y llamadas de seguimiento de vínculos ([`tl()` método](https://experienceleague.adobe.com/docs/analytics/implementation/vars/functions/tl-method.html)). En su lugar, el SDK web solo proporciona el [`sendEvent`](../commands/sendevent/overview.md) para enviar vistas de página y seguimiento de vínculos. Los datos que se incluyen en un evento determinan si es un [vista de página](https://experienceleague.adobe.com/docs/analytics/components/metrics/page-views.html?lang=es) o una [evento de página](https://experienceleague.adobe.com/docs/analytics/components/metrics/page-events.html) en Adobe Analytics.

De forma predeterminada, todos los eventos se consideran vistas de página en Adobe Analytics. Si desea establecer un evento del SDK web en una llamada de seguimiento de vínculos de Adobe Analytics, establezca los siguientes campos XDM:

* **`web.webInteraction.URL`**: la dirección URL del vínculo.
* **`web.webInteraction.name`**: el nombre de la dimensión Vínculo personalizado, Vínculo de descarga o Vínculo de salida, según el valor de `web.webInteraction.type`
* **`web.webInteraction.type`**: Determina el tipo de vínculo donde se hizo clic. Los valores válidos incluyen `other` (vínculos personalizados), `download` (vínculos de descarga) y `exit` (vínculos de salida).

Si activa [`clickCollectionEnabled`](../commands/configure/clickcollectionenabled.md) en el `configure` , estos campos XDM se rellenan automáticamente.
