---
title: Envío de datos a Adobe Analytics mediante el SDK web
description: Obtenga información sobre cómo enviar datos a Adobe Analytics con el SDK web de Adobe Experience Platform.
exl-id: b18d1163-9edf-4a9c-b247-cd1aa7dfca50
source-git-commit: 8c652e96fa79b587c7387a4053719605df012908
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---


# Envío de datos a Adobe Analytics mediante el SDK web

El SDK web de Experience Platform puede enviar datos a Adobe Analytics a través del Edge Network de Experience Platform. El Adobe de proporciona varias opciones para enviar datos a Adobe Analytics mediante el SDK web:

* Añada el [**[!UICONTROL grupo de campos de Adobe Analytics ExperienceEvent]**](../../xdm/field-groups/event/analytics-full-extension.md) a su esquema y, a continuación, utilice el [`XDM` objeto](../commands/sendevent/xdm.md).
* Utilice el [`data` objeto](../commands/sendevent/data.md) para enviar datos a Adobe Analytics sin un esquema XDM.
* Usar generado automáticamente [variables de datos de contexto](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/page-vars/contextdata) y [reglas de procesamiento](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/c-processing-rules-configuration/processing-rules-about).

## Utilice el `XDM` objeto {#use-xdm-object}

Si desea utilizar un esquema predefinido específico de Adobe Analytics, puede añadir la variable [grupo de campos de esquema de Adobe Analytics ExperienceEvent](../../xdm/field-groups/event/analytics-full-extension.md) a su esquema. Una vez agregado, puede rellenar este esquema con la variable `xdm` en el SDK web para enviar datos a un grupo de informes. Cuando los datos llegan al Edge Network, traducen el objeto XDM a un formato que Adobe Analytics comprende.

Existen dos maneras de enviar datos a Adobe Analytics a través del SDK web:

* [Envío de datos a Adobe Analytics mediante la extensión de etiqueta del SDK web](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/web-sdk/web-sdk-tag-extension)
* [Enviar datos a Adobe Analytics mediante la biblioteca JavaScript del SDK web](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/web-sdk/web-sdk-javascript-library)

Consulte [Asignación de variables de objeto XDM a Adobe Analytics](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/xdm-var-mapping) en la Guía de implementación de Adobe Analytics para obtener una referencia completa de los campos XDM y cómo se asignan a las variables de Analytics.

## Utilice el `data` objeto {#use-data-object}

Como alternativa al uso del objeto XDM, puede utilizar el objeto de datos en su lugar. El objeto de datos está dirigido a implementaciones que actualmente utilizan el AppMeasurement, lo que facilita la actualización al SDK web.

En función de si utiliza AppMeasurement o la extensión de etiquetas de Analytics, consulte las siguientes guías para obtener más información sobre cómo migrar al SDK web:

* [Migración de la extensión de etiqueta de Adobe Analytics a la extensión de etiqueta del SDK web](https://experienceleague.adobe.com/es/docs/analytics/implementation/aep-edge/web-sdk/analytics-extension-to-web-sdk)
* [Migración del AppMeasurement al SDK web](https://experienceleague.adobe.com/es/docs/analytics/implementation/aep-edge/web-sdk/appmeasurement-to-web-sdk)

Consulte la documentación sobre [asignación de variables de objeto de datos a Adobe Analytics](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/data-var-mapping) en la guía de implementación de Adobe Analytics para obtener una referencia completa de los campos de objetos de datos y cómo se asignan a las variables de Analytics.

## Usar variables de datos de contexto {#use-context-data-variables}

Todas las variables que no se asignan automáticamente están disponibles como [variables de datos de contexto](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/page-vars/contextdata). A continuación, puede utilizar [reglas de procesamiento](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/c-processing-rules-configuration/processing-rules-about) para asignar variables de datos de contexto a variables de Analytics. Por ejemplo, si tuviera un esquema XDM personalizado con el siguiente aspecto:

```json
{
  "xdm": {
    "key":"value",
    "animal": {
      "species": "Raven",
      "size": "13 inches"
    },
    "array": [
      "v0",
      "v1",
      "v2"
    ],
    "objectArray":[{
      "ad1": "300x200",
      "ad2": "60x240",
      "ad3": "600x50"
    }]
  }
}
```

A continuación, estos campos son las claves de datos de contexto disponibles en la interfaz de reglas de procesamiento:

```javascript
a.x.key //value
a.x.animal.species //Raven
a.x.animal.size //13 inches
a.x.array.0 //v0
a.x.array.1 //v1
a.x.array.2 //v2
a.x.objectarray.0.ad1 //300x200
a.x.objectarray.1.ad2 //60x240
a.x.objectarray.2.ad3 //600x50
```

## Preguntas frecuentes

+++¿Cómo diferencio las llamadas de vista de página de las llamadas de seguimiento de vínculos en el SDK web?

El AppMeasurement de Adobe Analytics utiliza llamadas de método independientes para las vistas de página ([`t()` método](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/functions/t-method)) y llamadas de seguimiento de vínculos ([`tl()` método](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/functions/tl-method)). En su lugar, el SDK web solo proporciona el [`sendEvent`](../commands/sendevent/overview.md) para enviar vistas de página y seguimiento de vínculos. Los datos que se incluyen en un evento determinan si es un [vista de página](https://experienceleague.adobe.com/en/docs/analytics/components/metrics/page-views) o una [evento de página](https://experienceleague.adobe.com/en/docs/analytics/components/metrics/page-events) en Adobe Analytics.

De forma predeterminada, todos los eventos se consideran vistas de página en Adobe Analytics. Si desea establecer un evento del SDK web en una llamada de seguimiento de vínculos de Adobe Analytics, establezca los campos siguientes:

* **Objeto XDM**: `xdm.web.webInteraction.name`, `web.webInteraction.type`, y `web.webInteraction.URL`
* **Objeto de datos**: `data.__adobe.analytics.linkName`, `data.__adobe.analytics.linkType`, y `data.__adobe.analytics.linkURL`
* **Datos de contexto**: no compatible

Consulte la [`tl()` método](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/functions/tl-method) en la guía de implementación de Adobe Analytics para obtener más información.

Si activa [`clickCollectionEnabled`](../commands/configure/clickcollectionenabled.md) en el `configure` , estos campos se rellenan automáticamente.

+++

+++¿Cómo diferencia un conjunto de datos los datos de otros servicios con los datos destinados a Adobe Analytics?

Todos los eventos enviados a una secuencia de datos se pasan a todos los servicios configurados. Por ejemplo, si realiza llamadas independientes para personalización y Analytics, ambos eventos se envían a Analytics y a Target. Estos eventos se registran en los informes de Analytics y pueden afectar a métricas como la tasa de salida hacia otro sitio.

Si utiliza el SDK web, estas llamadas se suelen combinar en la variable [`sendEvent`](../commands/sendevent/overview.md) comando.

+++
