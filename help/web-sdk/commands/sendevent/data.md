---
title: data
description: Aprenda a enviar datos que no sean XDM al Adobe.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 1%

---

# data

El `data` La propiedad permite enviar datos a un Adobe que no coincide con un esquema XDM. Resulta útil en situaciones que no son de XDM, como actualizar un [Perfil de Adobe Target](/help/web-sdk/personalization/adobe-target/target-overview.md). Cuando los datos llegan al Adobe, puede utilizar la herramienta de asignación de flujos de datos para asignar campos XDM a cada campo en la `data` propiedad.

>[!IMPORTANT]
>
>Los datos de esta propiedad deben tener al menos una de las siguientes acciones:
>
>* Se debe configurar un servicio del conjunto de datos para recuperar datos de una propiedad específica en el `data` objeto
>* Cada propiedad debe asignarse a un campo XDM
>
>Si un campo determinado no está asignado a un campo XDM o lo utiliza un servicio configurado, esos datos se pierden de forma permanente.

## Uso de la propiedad data mediante la extensión de etiqueta del SDK web

Proporcione un elemento de datos en la **[!UICONTROL Datos]** dentro de las acciones de una regla de etiqueta.

1. Iniciar sesión en [experience.adobe.com](https://experience.adobe.com) usando sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Reglas]**, luego seleccione la regla que desee.
1. En [!UICONTROL Acciones], seleccione una acción existente o cree una acción.
1. Configure las variables [!UICONTROL Extensión] campo desplegable a **[!UICONTROL SDK web de Adobe Experience Platform]** y configure el [!UICONTROL Tipo de acción] hasta **[!UICONTROL Enviar evento]**.
1. Proporcione el elemento de datos que contiene el objeto deseado en la **[!UICONTROL Datos]** field.
1. Clic **[!UICONTROL Conservar cambios]**, luego ejecute el flujo de trabajo de publicación.

## Utilice la propiedad data mediante la biblioteca JavaScript del SDK web

Configure las variables `data` como parte del objeto JSON dentro del parámetro de la propiedad `sendEvent` comando. Para los datos que planea asignar en el conjunto de datos, puede estructurar esta propiedad como desee. Para los datos utilizados por ciertos servicios, asegúrese de que la jerarquía de objetos coincide con lo que espera el servicio. Puede incluir ambos `data` y el objeto [`xdm`](xdm.md) objeto en el mismo `sendEvent` comando.

```javascript
alloy("sendEvent", {
  "data": dataObject
});
```
