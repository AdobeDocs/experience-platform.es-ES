---
title: data
description: Aprenda a enviar datos que no sean XDM al Adobe a través del objeto de datos.
exl-id: 537fc34e-3cda-4aa7-ae0d-0d3ef4b89848
source-git-commit: 8c652e96fa79b587c7387a4053719605df012908
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 0%

---


# `data`

El `data` permite enviar una carga útil a un Adobe que no coincide con un esquema XDM. Resulta útil en situaciones que no son de XDM, como enviar datos directamente a Adobe Analytics, Adobe Target o Adobe Audience Manager. Cuando los datos llegan al conjunto de datos, puede utilizar [Asignación de preparación de datos](/help/data-prep/ui/mapping.md) para asignar campos XDM a cada campo de la variable `data` objeto.

>[!IMPORTANT]
>
>Los datos de este objeto deben tener al menos una de las acciones siguientes:
>
>* Se debe configurar un servicio del conjunto de datos para recuperar datos de una propiedad determinada en el `data` objeto.
>* La propiedad dada debe asignarse a un campo XDM mediante la preparación de datos.
>
>Si una propiedad determinada no está asignada a un campo XDM o la utiliza un servicio configurado, esos datos se pierden de forma permanente.

## Utilice el `data` mediante la extensión de etiqueta del SDK web {#tag-extension}

Proporcione un elemento de datos en la **[!UICONTROL Datos]** dentro de las acciones de una regla de etiqueta.

1. Iniciar sesión en [experience.adobe.com](https://experience.adobe.com) usando sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Reglas]**, luego seleccione la regla que desee.
1. En [!UICONTROL Acciones], seleccione una acción existente o cree una acción.
1. Configure las variables [!UICONTROL Extensión] campo desplegable a **[!UICONTROL SDK web de Adobe Experience Platform]** y configure el [!UICONTROL Tipo de acción] hasta **[!UICONTROL Enviar evento]**.
1. Proporcione el elemento de datos que contiene el objeto deseado en la **[!UICONTROL Datos]** field.
1. Clic **[!UICONTROL Conservar cambios]**, luego ejecute el flujo de trabajo de publicación.

## Utilice el `data` mediante la biblioteca JavaScript del SDK web {#library}

Configure las variables `data` como parte del objeto JSON dentro del parámetro del objeto `sendEvent` comando. Para los datos que planea asignar en el conjunto de datos, puede estructurar este objeto como desee. Para los datos utilizados por ciertos servicios, asegúrese de que la jerarquía de objetos coincide con lo que espera el servicio. Puede incluir ambos `data` y el objeto [`xdm`](xdm.md) objeto en el mismo `sendEvent` comando.

```javascript
alloy("sendEvent", {
  "data": dataObject
});
```

## Utilice el `data` objeto con Adobe Analytics {#analytics}

Puede usar el complemento `data` con Adobe Analytics para enviar datos a un grupo de informes sin un esquema XDM. Las variables están configuradas para utilizar la misma sintaxis que [!DNL AppMeasurement] , simplificando el proceso de actualización al SDK web. Consulte [Asignación de variables de objetos de datos a Adobe Analytics](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/data-var-mapping) en la guía de implementación de Adobe Analytics para obtener más información.
