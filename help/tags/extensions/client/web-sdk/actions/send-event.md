---
title: Enviar evento
description: Envíe datos a Adobe Experience Platform Edge Network.
exl-id: 4ac7750e-48ab-4eb6-873d-bb2556dbf788
source-git-commit: caaf5cad7276d6429fbbf35585fd4845de6ff60c
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 0%

---

# Enviar evento

La acción **[!UICONTROL Send event]** envía una carga útil a un conjunto de datos en Adobe Experience Platform Edge Network. Es una función central de la recopilación y personalización de datos. Casi todas las organizaciones utilizan esta acción como parte de su implementación de Web SDK.

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Vaya a **[!UICONTROL Rules]** y, a continuación, seleccione la regla que desee.
1. En [!UICONTROL Actions], seleccione una acción existente o cree una acción.
1. Establezca el campo desplegable [!UICONTROL Extension] en **[!UICONTROL Adobe Experience Platform Web SDK]**, luego establezca [!UICONTROL Action type] en **[!UICONTROL Send event]**.

## Campos generales

![Imagen de la interfaz de usuario de Experience Platform Tags que muestra la configuración de instancia para el tipo de acción Enviar evento.](../assets/instance-settings.png)

* **[!UICONTROL Instance]**: la instancia de SDK a la que se aplica la acción. Este menú desplegable está desactivado si su implementación utiliza una sola instancia de SDK.
* **[!UICONTROL Use guided events]**: active esta opción para rellenar u ocultar automáticamente ciertos campos a fin de habilitar un caso de uso determinado. Esta configuración puede ayudar a reducir el ruido de las opciones disponibles al configurar la acción para cada propósito respectivo y sigue las prácticas recomendadas de Adobe en [eventos de página superior/inferior](/help/collection/use-cases/personalization/top-bottom-page-events.md). Al activar esta casilla de verificación, se déclencheur la visualización de los siguientes botones de opción:
   * **[!UICONTROL Request personalization]**: obtenga las decisiones de personalización más recientes sin registrar un evento de Adobe Analytics. Normalmente se denomina en la parte superior de la página. Al seleccionarlo, este botón de opción establece los siguientes campos:
      * [!UICONTROL Type] está bloqueado a [!UICONTROL Decisioning Proposition Fetch]
      * [!UICONTROL Render visual personalization decisions] está bloqueado para habilitarse
      * [!UICONTROL Automatically send a display event] está bloqueado y deshabilitado
   * **[!UICONTROL Collect analytics]**: registre un evento sin obtener decisiones de personalización. Normalmente se llama en la parte inferior de la página. Al seleccionarlo, este botón de opción establece los siguientes campos:
      * [!UICONTROL Include rendered propositions] está bloqueado para habilitarse

## Campos de datos

![Imagen de la interfaz de usuario de etiquetas de Experience Platform que muestra la configuración del elemento de datos para el tipo de acción Enviar evento.](../assets/data.png)

* **[!UICONTROL Type]**: el tipo de evento. Puede seleccionar entre un conjunto de valores predefinidos o definir su propio valor. Vea [Valores aceptados para `eventType`](/help/xdm/classes/experienceevent.md#accepted-values-for-eventtype) para obtener más información. El equivalente de la biblioteca JavaScript para este campo es [`eventType`](/help/collection/js/commands/sendevent/eventtype.md).
* **[!UICONTROL XDM]**: la carga útil XDM que desea enviar a Adobe. Puede usar un [objeto XDM](../data-element-types.md#xdm-object) o [variable](../data-element-types.md#variable) en este campo. Si tiene reglas que rellenan varios objetos XDM, puede usar [Objetos combinados](../../core/overview.md#merged-objects) para combinarlos.
* **[!UICONTROL Data]**: la carga de datos que desea enviar a Adobe. Algunas aplicaciones y servicios no requieren la adherencia a un esquema XDM, como Adobe Analytics o Adobe Target. Usar un tipo de elemento de datos [Variable](../data-element-types.md#variable) para este campo.
* **[!UICONTROL Include rendered propositions]**: active esta casilla de verificación para utilizar este evento como evento de visualización, incluidas las propuestas que se procesaron cuando se desactivó la opción &quot;enviar automáticamente un evento de visualización&quot;. El campo XDM `_experience.decisioning` se rellena con información sobre la personalización procesada.
* **[!UICONTROL Document will unload]**: active esta casilla de verificación para asegurarse de que el evento llega al servidor incluso si el usuario sale de la página. Esta configuración permite que los eventos lleguen al servidor, pero se omiten las respuestas de Edge Network.
* **[!UICONTROL Merge ID]** _(obsoleto)_: Rellena el campo XDM `eventMergeId`.

## Campos de personalización

![Imagen de la interfaz de usuario de Experience Platform Tags que muestra la configuración de Personalization para el tipo de acción Enviar evento.](../assets/personalization-settings.png)

* **[!UICONTROL Scopes]**: matriz de ámbitos que desea solicitar explícitamente desde la personalización. Puede introducir los ámbitos manualmente o proporcionar un elemento de datos. Al escribir ámbitos manualmente, cada campo representa un ámbito. Seleccione **[!UICONTROL Add scope]** para agregar más ámbitos a la acción.
* **[!UICONTROL Surfaces]**: una matriz de superficies para consultar con el evento. Consulte [Crear experiencias web](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html) en la documentación de Adobe Journey Optimizer para obtener más información. Al introducir superficies manualmente, cada campo representa una superficie. Seleccione **[!UICONTROL Add surface]** para agregar más superficies a la acción.
* **Procesar decisiones de personalización visuales:** Casilla de verificación que, cuando está habilitada, permite procesar contenido personalizado en la página. Consulte [Procesar acciones DOM automáticamente](/help/collection/use-cases/personalization/render-auto-pers-content.md) para obtener más información.
* **[!UICONTROL Request default personalization]**: controla si se solicita el ámbito de toda la página y la superficie predeterminada. De manera predeterminada, se solicita automáticamente durante la primera llamada de `sendEvent` de la carga de la página. El equivalente de la biblioteca JavaScript de estos botones de opción es [`requestDefaultPersonalization`](/help/collection/js/commands/sendevent/personalization.md). Puede elegir entre las siguientes opciones:
   * **[!UICONTROL Automatic]**: comportamiento predeterminado. Solicitar solo la personalización predeterminada cuando aún no se ha solicitado.
   * **[!UICONTROL Enabled]**: solicite explícitamente el ámbito de página y la superficie predeterminada. Esto actualiza la caché de la vista SPA.
   * **[!UICONTROL Disabled]**: suprime explícitamente la solicitud para el ámbito de página y la superficie predeterminada.
* **[!UICONTROL Decision context]**: asignación de clave-valor que se usa al evaluar conjuntos de reglas de Adobe Journey Optimizer para la toma de decisiones en el dispositivo. Puede proporcionar el contexto de decisión manualmente o mediante un elemento de datos.

## Campos de Advertising

![IU de etiquetas de Experience Platform que muestra la configuración de publicidad para la acción Enviar evento](../assets/send-event-advertising.png)

* **[!UICONTROL Request default advertising data]**: Determina cuándo (o si) la biblioteca agrega información publicitaria a la carga útil XDM. Puede elegir entre las siguientes opciones:
   * **[!UICONTROL Automatic]**: todos los datos de publicidad disponibles en el momento del evento se agregan a la carga útil del evento.
   * **[!UICONTROL Wait]**: Retrasar el envío del evento hasta que se reciban los datos de publicidad.
   * **[!UICONTROL Disabled]**: no agregue datos publicitarios a la carga útil de evento. Seleccione esta opción si su implementación no utiliza Adobe Analytics ni Customer Journey Analytics.

## Anulaciones de configuración de secuencia de datos

Este comando admite las anulaciones de configuración de la secuencia de datos, lo que le permite controlar qué aplicaciones y servicios reciben estos datos. Cuando se establece una anulación de la configuración de la secuencia de datos tanto en un comando individual como en los ajustes de configuración de la extensión de la etiqueta, el comando individual tiene prioridad. Consulte [Anulaciones de configuración de secuencia de datos](../configure/configuration-overrides.md) para obtener más información.
