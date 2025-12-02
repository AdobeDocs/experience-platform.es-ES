---
title: Redirigir con identidad
description: Permite compartir un identificador de visitante entre los dominios de la organización.
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 1%

---

# Redirigir con identidad

El tipo de acción **[!UICONTROL Redirect with identity]** le permite compartir un identificador de visitante de la página actual con otro dominio de su organización. Está diseñado para utilizarse con un evento de clic y una condición de comparación de valores. Desde el punto de vista funcional, es similar al comando [`appendIdentityToUrl`](/help/collection/js/commands/appendidentitytourl.md) de la biblioteca JavaScript.

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Rules]** y, a continuación, seleccione la regla que desee.
1. En [!UICONTROL Actions], seleccione una acción existente o cree una acción.
1. Establezca el campo desplegable [!UICONTROL Extension] en **[!UICONTROL Adobe Experience Platform Web SDK]**, luego establezca [!UICONTROL Action type] en **[!UICONTROL Redirect with identity]**.

## Casos de uso

* **Identificar a un individuo en todos los dominios**: Si un visitante hace clic de un dominio a otro propiedad de su organización, puede usar esta acción para que se los siga considerando el mismo individuo. Este método de identificación es especialmente útil si tiene informes que combinan datos de varios dominios, lo que evita la inflación de visitantes.
* **Identifique a un individuo desde una aplicación móvil a una aplicación web**: Si un visitante está dentro de su aplicación móvil y hace clic en un vínculo a la aplicación web, puede utilizar esta acción para que Web SDK reconozca que es el mismo individuo. Este flujo de trabajo ofrece una experiencia coherente para la creación de informes y la personalización.

## Campos disponibles

* **[!UICONTROL Instance]**: la instancia de SDK a la que se aplica la acción. Este menú desplegable está desactivado si su implementación utiliza una sola instancia de SDK.
* **[!UICONTROL Datastream configuration overrides]**: este comando admite las invalidaciones de configuración de la secuencia de datos, lo que le permite controlar qué aplicaciones y servicios reciben estos datos. Cuando se establece una anulación de la configuración de la secuencia de datos tanto en un comando individual como en los ajustes de configuración de la extensión de la etiqueta, el comando individual tiene prioridad. Consulte [Anulaciones de configuración de secuencia de datos](../configure/configuration-overrides.md) para obtener más información.

## Regla de ejemplo

Este comando suele utilizarse con una regla específica que escucha clics y comprueba los dominios deseados.

+++Criterios de evento de regla

Déclencheur cuando se hace clic en una etiqueta delimitadora con una propiedad `href`.

* **[!UICONTROL Extension]**: principal
* **[!UICONTROL Event type]**: clic
* **[!UICONTROL When the user clicks on]**: elementos específicos
* **[!UICONTROL Elements matching the CSS selector]**: `a[href]`

![Evento de regla](../assets/id-sharing-event-configuration.png)

+++

+++Condición de regla

Déclencheur solo en los dominios deseados.

* **[!UICONTROL Logic type]**: Normal
* **[!UICONTROL Extension]**: principal
* **[!UICONTROL Condition Type]**: comparación de valores
* **[!UICONTROL Left Operand]**: `%this.hostname%`
* **[!UICONTROL Operator]**: coincide con el regex
* **[!UICONTROL Right Operand]**: una expresión regular que coincide con los dominios deseados. Por ejemplo, `adobe.com$|behance.com$`

![Condición de regla](../assets/id-sharing-condition-configuration.png)

+++

+++Acción de regla

Anexe la identidad a la dirección URL.

* **[!UICONTROL Extension]**: Adobe Experience Platform Web SDK
* **[!UICONTROL Action Type]**: redireccionar con identidad

![Acción de regla](../assets/id-sharing-action-configuration.png)

+++
