---
title: applyPropositions
description: Volver a procesar propuestas que ya se hayan procesado con sendEvent.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 1%

---


# `applyPropositions`

El `applyPropositions` permite volver a procesar las propuestas que ya se han procesado con el comando [`sendEvent`](sendevent/overview.md) comando. Este comando resulta útil cuando se trabaja con aplicaciones de una sola página en las que se vuelven a procesar partes de la página, sobrescribiendo potencialmente las personalizaciones ya aplicadas a la página.

Este comando admite los campos siguientes:

* **Propuestas**: matriz de objetos de propuesta que desea volver a procesar.
* **Ver nombre**: Nombre de la vista que se va a procesar. Las notificaciones de visualización para estas decisiones se almacenan en caché y se pueden incluir en una `sendEvent` mediante el comando `personalization.includePendingDisplayNotifications` opción.
* **Metadatos**: Un objeto que determina cómo se pueden aplicar las ofertas de HTML. Contiene las siguientes propiedades:
   * Ámbito
   * Selector
   * Tipo de acción

## Aplicación de propuestas mediante la extensión de etiqueta del SDK web

La aplicación de propuestas se realiza como una acción dentro de una regla en la interfaz de etiquetas de recopilación de datos de Adobe Experience Platform.

1. Iniciar sesión en [experience.adobe.com](https://experience.adobe.com) usando sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Reglas]**, luego seleccione la regla que desee.
1. En [!UICONTROL Acciones], seleccione una acción existente o cree una acción.
1. Configure las variables [!UICONTROL Extensión] campo desplegable a **[!UICONTROL SDK web de Adobe Experience Platform]** y configure el [!UICONTROL Tipo de acción] hasta **[!UICONTROL Aplicar propuestas]**.
1. Defina los campos deseados a la derecha.
1. Clic **[!UICONTROL Conservar cambios]**, luego ejecute el flujo de trabajo de publicación.

## Aplicar propuestas mediante la biblioteca JavaScript del SDK web

Ejecute el `applyPropositions` al llamar a la instancia configurada del SDK web. El objeto que contiene las opciones de configuración admite los siguientes campos:

* **`propositions`**: matriz de objetos de propuesta que desea volver a procesar. Este objeto no se utiliza normalmente, ya que `propositionScopes` normalmente determina qué ámbitos o superficies desea volver a procesar.
* **`metadata`**: Determina cómo se aplican las ofertas del HTML. Es un mapa donde la clave es un ámbito o una superficie, y el valor es un objeto que contiene las claves `selector` y `actionType`.
   * `selector`: Una cadena que contiene un selector CSS de dónde aplicar el HTML.
   * `actionType`: Acción que se va a realizar con el HTML. Los valores válidos incluyen `setHtml`, `replaceHtml` y `appendHtml`.
* **`viewName`**: Nombre de la vista que se va a procesar en una aplicación de una sola página. Las notificaciones de visualización para estas decisiones se almacenan en caché y se pueden incluir en una `sendEvent` comando con `personalization.includePendingDisplayNotifications`.

```js
alloy("applyPropositiions",{
  "propositions": [],
  "metadata": {},
  "viewName": ""
});
```
