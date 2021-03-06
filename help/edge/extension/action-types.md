---
title: Tipos de acción en la extensión del SDK web de Adobe Experience Platform
description: Obtenga información sobre los distintos tipos de acciones proporcionados por la extensión de etiqueta del SDK web de Adobe Experience Platform.
solution: Experience Platform
exl-id: a4bf0bb9-59b4-4c43-97e6-387768176517
source-git-commit: 5218e6cf82b74efbbbcf30495395a4fe2ad9fe14
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 3%

---

# Tipos de acción

Después de configurar la [extensión de etiqueta del SDK web de Adobe Experience Platform](web-sdk-extension-configuration.md), configure los tipos de acción.

Esta página describe los tipos de acción disponibles.


## Enviar evento

Envía un evento al Adobe [!DNL Experience Platform] para que Adobe Experience Platform pueda recopilar los datos que envía y actuar en consecuencia. Seleccione una instancia (si tiene más de una). Los datos que desee enviar se pueden enviar en el campo **[!UICONTROL XDM Data]**. Utilice un objeto JSON que se ajuste a la estructura del esquema XDM. Este objeto se puede crear en la página o a través de un **[!UICONTROL Custom Code]** **[!UICONTROL Data Element]**.

Existen otros campos en el tipo de acción Enviar evento que también pueden resultar útiles en función de la implementación. Tenga en cuenta que todos estos campos son opcionales.

- **Tipo:** este campo permite especificar un tipo de evento que se registrará en el esquema XDM. Consulte la [documentación](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#using-the-sendbeacon-api) para obtener más información sobre los tipos de evento predeterminados.
- **Datos:** Los datos que no coinciden con un esquema XDM se pueden enviar utilizando este campo. Este campo es útil si está intentando actualizar un perfil de Adobe Target o enviar atributos de Recommendations de Target. Para ver ejemplos, consulte nuestra [documentación](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en).
<!--- **Merge ID:** If you would like to specify a merge ID for your event, you can do so in this field. Please note that the solutions downstream are not able to merge your event data at this time. -->
- **ID de conjunto de datos:** si necesita enviar datos a un conjunto de datos que no sea el especificado en su conjunto de datos, puede especificar ese ID de conjunto de datos aquí.
- **El documento se descargará:** si desea asegurarse de que los eventos llegan al servidor aunque el usuario salga de la página, marque la casilla de verificación  **[!UICONTROL Document will]** unloadbox. Esto permite que los eventos lleguen al servidor, pero las respuestas se ignoran.
- **Renderizar decisiones de personalización visual:** si desea procesar contenido personalizado en la página, marque la casilla  **[!UICONTROL Render visual personalization]** decisionss. También puede especificar ámbitos de decisión si es necesario. Consulte la [documentación de personalización](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html?lang=en#automatically-rendering-content) para obtener más información sobre el procesamiento de contenido personalizado.

## Definir consentimiento

Una vez que el usuario haya dado su consentimiento, este consentimiento debe comunicarse al SDK web de Adobe Experience Platform mediante el tipo de acción &quot;Definir consentimiento&quot;. Actualmente se admiten dos tipos de estándares: Adobe y IAB TCF. Consulte [Compatibilidad con las preferencias de consentimiento del cliente](../consent/supporting-consent.md). Al utilizar Adobe versión 2.0, solo se admite un valor de elemento de datos. Deberá crear un elemento de datos que se resuelva en el objeto de consentimiento.

En esta acción, también se le proporcionará un campo opcional para incluir un mapa de identidad de modo que las identidades se puedan sincronizar una vez recibido el consentimiento. La sincronización es útil cuando el consentimiento está configurado como &quot;Pendiente&quot; o &quot;Fuera&quot; porque es probable que la llamada de consentimiento sea la primera llamada a activarse.

## Restablecer ID de combinación de eventos

Si desea restablecer el ID de combinación de eventos en la página, puede hacerlo con esta acción. Para restablecer su ID, seleccione el ID de combinación que desee restablecer y active la acción según sea necesario.

## Siguientes pasos

Después de configurar las acciones, [configure los tipos de elementos de datos](data-element-types.md).
