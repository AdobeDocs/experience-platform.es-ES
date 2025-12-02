---
title: datos
description: Aprenda a enviar datos que no sean XDM a Adobe a través del objeto de datos.
exl-id: 537fc34e-3cda-4aa7-ae0d-0d3ef4b89848
source-git-commit: f4a2778c71ad6a48621212f3ece1776d1b3ac643
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---

# `data`

El objeto `data` le permite enviar una carga útil a Adobe que no coincide con un esquema XDM. Resulta útil en situaciones que no son de XDM, como enviar datos directamente a Adobe Analytics, Adobe Target o Adobe Audience Manager. Cuando los datos llegan al conjunto de datos, puede usar la asignación [Data Prep](/help/data-prep/ui/mapping.md) para asignar campos XDM a cada campo en el objeto `data`. Si Adobe ya ha configurado un producto para detectar campos en el objeto `data`, puede enviar esos datos tal cual a una secuencia de datos.

>[!IMPORTANT]
>
>Los datos de este objeto deben tener al menos una de las acciones siguientes:
>
>* Se debe configurar un servicio del conjunto de datos para recuperar datos de una propiedad determinada en el objeto `data`.
>* La propiedad dada debe asignarse a un campo XDM mediante la preparación de datos.
>
>Si una propiedad determinada no está asignada a un campo XDM o la utiliza un servicio configurado, esos datos se pierden de forma permanente.

Establezca el objeto `data` como parte del objeto JSON dentro del parámetro del comando `sendEvent`. Para los datos que planea asignar en el conjunto de datos, puede estructurar este objeto como desee. Para los datos utilizados por ciertos servicios, asegúrese de que la jerarquía de objetos coincide con lo que espera el servicio. Puede incluir el objeto `data` y el objeto [`xdm`](xdm.md) en el mismo comando `sendEvent`.

```javascript
alloy("sendEvent", {
  "data": dataObject
});
```

## Usar el objeto `data` con Adobe Analytics {#analytics}

Puede utilizar el objeto `data` con Adobe Analytics para enviar datos a un grupo de informes sin un esquema XDM. Las variables se configuran para utilizar la misma sintaxis que las variables de AppMeasurement, lo que simplifica el proceso de actualización a Web SDK. Consulte [Asignación de variables de objetos de datos a Adobe Analytics](https://experienceleague.adobe.com/es/docs/analytics/implementation/aep-edge/data-var-mapping) en la guía de implementación de Adobe Analytics para obtener más información.

## Usar el objeto `data` mediante la extensión de etiqueta Web SDK

El objeto `data` está disponible como [elemento de datos variable](/help/tags/extensions/client/web-sdk/data-element-types.md#variable) al usar la extensión de etiquetas Web SDK.
