---
title: datos
description: Aprenda a enviar datos que no sean XDM al Adobe a través del objeto de datos.
exl-id: 537fc34e-3cda-4aa7-ae0d-0d3ef4b89848
source-git-commit: 8c652e96fa79b587c7387a4053719605df012908
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 0%

---


# `data`

El objeto `data` le permite enviar una carga útil a un Adobe que no coincide con un esquema XDM. Resulta útil en situaciones que no son de XDM, como enviar datos directamente a Adobe Analytics, Adobe Target o Adobe Audience Manager. Cuando los datos llegan al conjunto de datos, puede usar la asignación [Data Prep](/help/data-prep/ui/mapping.md) para asignar campos XDM a cada campo en el objeto `data`.

>[!IMPORTANT]
>
>Los datos de este objeto deben tener al menos una de las acciones siguientes:
>
>* Se debe configurar un servicio del conjunto de datos para recuperar datos de una propiedad determinada en el objeto `data`.
>* La propiedad dada debe asignarse a un campo XDM mediante la preparación de datos.
>
>Si una propiedad determinada no está asignada a un campo XDM o la utiliza un servicio configurado, esos datos se pierden de forma permanente.

## Usar el objeto `data` mediante la extensión de etiqueta del SDK web {#tag-extension}

Proporcione un elemento de datos en el campo **[!UICONTROL Data]** dentro de las acciones de una regla de etiqueta.

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Reglas]** y luego seleccione la regla que desee.
1. En [!UICONTROL Acciones], seleccione una acción existente o cree una acción.
1. Establezca el campo desplegable [!UICONTROL Extension] en **[!UICONTROL SDK web de Adobe Experience Platform]** y establezca [!UICONTROL Action Type] en **[!UICONTROL Send event]**.
1. Proporcione el elemento de datos que contiene el objeto deseado en el campo **[!UICONTROL Datos]**.
1. Haga clic en **[!UICONTROL Conservar cambios]** y, a continuación, ejecute el flujo de trabajo de publicación.

## Usar el objeto `data` a través de la biblioteca JavaScript del SDK web {#library}

Establezca el objeto `data` como parte del objeto JSON dentro del parámetro del comando `sendEvent`. Para los datos que planea asignar en el conjunto de datos, puede estructurar este objeto como desee. Para los datos utilizados por ciertos servicios, asegúrese de que la jerarquía de objetos coincide con lo que espera el servicio. Puede incluir el objeto `data` y el objeto [`xdm`](xdm.md) en el mismo comando `sendEvent`.

```javascript
alloy("sendEvent", {
  "data": dataObject
});
```

## Usar el objeto `data` con Adobe Analytics {#analytics}

Puede utilizar el objeto `data` con Adobe Analytics para enviar datos a un grupo de informes sin un esquema XDM. Las variables están configuradas para utilizar la misma sintaxis que las variables [!DNL AppMeasurement], lo que simplifica el proceso de actualización al SDK web. Consulte [Asignación de variables de objetos de datos a Adobe Analytics](https://experienceleague.adobe.com/es/docs/analytics/implementation/aep-edge/data-var-mapping) en la guía de implementación de Adobe Analytics para obtener más información.
