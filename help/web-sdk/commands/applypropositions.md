---
title: applyPropositions
description: Volver a procesar propuestas que ya se hayan procesado con sendEvent.
exl-id: 6b79f334-4ea6-4ba4-8640-d35b7f90df98
source-git-commit: 9aab41b338907f3c9fb15d08bfa877eb218f5627
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# `applyPropositions`

El comando `applyPropositions` le permite volver a procesar propuestas que ya se representaron con el comando [`sendEvent`](sendevent/overview.md). Este comando resulta útil cuando se trabaja con aplicaciones de una sola página en las que se vuelven a procesar partes de la página, sobrescribiendo potencialmente las personalizaciones ya aplicadas a la página.

Este comando admite los campos siguientes:

* **Propositions**: matriz de objetos de propuesta que desea volver a procesar.
* **Nombre de vista**: Nombre de la vista que se va a procesar. Las notificaciones de visualización para estas decisiones se almacenan en caché y se pueden incluir en un comando `sendEvent` posterior usando la opción `personalization.includePendingDisplayNotifications`.
* **Metadatos**: Un objeto que determina cómo se pueden aplicar las ofertas de HTML. Contiene las siguientes propiedades:
   * Ámbito
   * Selector
   * Tipo de acción

## Aplicación de propuestas mediante la extensión de etiqueta del SDK web

La aplicación de propuestas se realiza como una acción dentro de una regla en la interfaz de etiquetas de recopilación de datos de Adobe Experience Platform.

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Reglas]** y luego seleccione la regla que desee.
1. En [!UICONTROL Acciones], seleccione una acción existente o cree una acción.
1. Establezca el campo desplegable [!UICONTROL Extension] en **[!UICONTROL SDK web de Adobe Experience Platform]** y establezca el [!UICONTROL Tipo de acción] en **[!UICONTROL Aplicar propuestas]**.
1. Defina los campos deseados a la derecha.
1. Haga clic en **[!UICONTROL Conservar cambios]** y, a continuación, ejecute el flujo de trabajo de publicación.

## Aplicar propuestas mediante la biblioteca JavaScript del SDK web

Ejecute el comando `applyPropositions` al llamar a la instancia configurada del SDK web. El objeto que contiene las opciones de configuración admite los siguientes campos:

* **`propositions`**: matriz de objetos de propuesta que desea volver a procesar. Este objeto no suele utilizarse, ya que el campo `propositionScopes` suele determinar qué ámbitos o superficies desea volver a procesar.
* **`metadata`**: determina cómo se aplican las ofertas de HTML. Es un mapa donde la clave es un ámbito o una superficie y el valor es un objeto que contiene las claves `selector` y `actionType`.
   * `selector`: cadena que contiene un selector CSS de dónde aplicar el HTML.
   * `actionType`: acción que se va a realizar con el HTML. Los valores válidos incluyen `setHtml`, `replaceHtml` y `appendHtml`.
* **`viewName`**: nombre de la vista que se va a procesar en una aplicación de una sola página. Las notificaciones de visualización para estas decisiones se almacenan en caché y se pueden incluir en un comando `sendEvent` posterior con `personalization.includePendingDisplayNotifications`.

```js
alloy("applyPropositions",{
  "propositions": [],
  "metadata": {},
  "viewName": ""
});
```
