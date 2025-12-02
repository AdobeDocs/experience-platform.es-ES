---
title: Aplicar propuestas
description: Procesar propuestas en aplicaciones de una sola página sin incrementar las métricas.
source-git-commit: 217282135bcd750740f4d3f8c6e17a0b8f9578bd
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# Aplicar propuestas

El tipo de acción **[!UICONTROL Apply propositions]** le permite procesar propuestas en aplicaciones de una sola página sin incrementar las métricas. Este tipo de acción es útil cuando se trabaja con aplicaciones de una sola página en las que se vuelven a procesar partes de la página, sobrescribiendo potencialmente las personalizaciones ya aplicadas a la página.

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Rules]** y, a continuación, seleccione la regla que desee.
1. En [!UICONTROL Actions], seleccione una acción existente o cree una acción.
1. Establezca el campo desplegable [!UICONTROL Extension] en **[!UICONTROL Adobe Experience Platform Web SDK]**, luego establezca [!UICONTROL Action type] en **[!UICONTROL Apply propositions]**.

![Interfaz de usuario de etiquetas de Experience Platform que muestra el tipo de acción Aplicar propuestas.](../assets/apply-propositions.png)

## Casos de uso

Puede utilizar este tipo de acción para varios casos de uso, como:

1. **Procesar ofertas de mbox HTML**. Las propuestas solicitadas explícitamente a través de un ámbito o superficie desde una acción **[!UICONTROL Send event]** no se representan automáticamente. Puede utilizar el tipo de acción **[!UICONTROL Apply propositions]** para indicar a Web SDK dónde procesarlos especificando los metadatos de la propuesta.
2. **Procesar las ofertas para una vista en una aplicación de una sola página**. Al procesar un evento de cambio de vista, si los datos de Analytics aún no están listos, puede utilizar la acción **[!UICONTROL Apply propositions]** para procesar las propuestas de vista en la parte superior de la página. Consulte [eventos de parte superior e inferior de la página (segunda vista de página: opción 2)](/help/collection/use-cases/personalization/top-bottom-page-events.md) para obtener más información. Para usar esto, ingrese un **[!UICONTROL View name]** en el formulario.
3. **Volver a procesar propuestas**. Cuando el sitio utiliza un marco de trabajo como React para volver a procesar contenido, es posible que tenga que volver a aplicar la personalización. En estos casos, puede usar el tipo de acción **[!UICONTROL Apply propositions]** para hacerlo.

Este tipo de acción no envía un evento de visualización para propuestas procesadas. Realiza un seguimiento de las propuestas procesadas para que se puedan incluir en las llamadas a **[!UICONTROL Send event]** subsiguientes.

## Campos disponibles

Este tipo de acción admite los siguientes campos:

* **[!UICONTROL Instance]**: la instancia de SDK a la que se aplica la acción. Este menú desplegable está desactivado si su implementación utiliza una sola instancia de SDK.
* **[!UICONTROL Propositions]**: matriz de objetos de propuesta que desea volver a procesar.
* **[!UICONTROL View name]**: nombre de la vista que se va a procesar.
* **[!UICONTROL Proposition metadata]**: un objeto que determina cómo se pueden aplicar las ofertas de HTML. Puede proporcionar esta información a través del formulario o de un elemento de datos. Contiene las siguientes propiedades:
   * **[!UICONTROL Scope]**
   * **[!UICONTROL Selector]**
   * **[!UICONTROL Action type]**
