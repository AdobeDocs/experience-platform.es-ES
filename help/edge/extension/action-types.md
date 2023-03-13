---
title: Tipos de acción en la extensión SDK para web de Adobe Experience Platform
description: Obtenga información acerca de los diferentes tipos de acción que proporciona la extensión de etiqueta SDK web de Adobe Experience Platform.
solution: Experience Platform
exl-id: a4bf0bb9-59b4-4c43-97e6-387768176517
source-git-commit: 1b0f1e2e1625f6994a6e09bd086e4b63a3e8d4ab
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 5%

---

# Tipos de acción

Después de configurar el [Extensión de etiqueta de SDK web de Adobe Experience Platform](web-sdk-extension-configuration.md), configure los tipos de acción.

Esta página describe los tipos de acción disponibles.


## Enviar evento

Envía un evento al Adobe [!DNL Experience Platform] para que Adobe Experience Platform pueda recopilar los datos que envía y actuar con esa información. Seleccione una instancia (si tiene más de una). Los datos que desee enviar se pueden enviar en la variable **[!UICONTROL Datos XDM]** field. Utilice un objeto JSON que se ajuste a la estructura del esquema XDM. Este objeto se puede crear en la página o a través de un **[!UICONTROL Código personalizado]** **[!UICONTROL Elemento de datos]**.

Hay otros campos en el tipo de acción Enviar evento que también pueden ser útiles según la implementación. Tenga en cuenta que estos campos son todos opcionales.

- **Tipo:** Este campo permite especificar un tipo de evento que se registrará en el esquema XDM. Consulte la [documentación](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#using-the-sendbeacon-api) para obtener más información sobre los tipos de eventos predeterminados.
- **Datos:** Los datos que no coinciden con un esquema XDM se pueden enviar mediante este campo. Este campo es útil si intenta actualizar un perfil de Adobe Target o enviar atributos de Recommendations de Target. Para ver ejemplos, consulte nuestra [documentación](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=es).<!--- **Merge ID:** If you would like to specify a merge ID for your event, you can do so in this field. Please note that the solutions downstream are not able to merge your event data at this time. -->
- **ID de conjunto de datos:** Si necesita enviar datos a un conjunto de datos que no sea el especificado en su conjunto de datos, puede especificar ese ID del conjunto de datos aquí.
- **Se descargará el documento:** Si desea asegurarse de que los eventos llegan al servidor incluso si el usuario sale de la página, consulte la **[!UICONTROL Se descargará el documento]** casilla de verificación Esto permite que los eventos lleguen al servidor, pero las respuestas se omiten.
- **Procesar decisiones de personalización visuales:** Si desea procesar contenido personalizado en la página, consulte la **[!UICONTROL Procesar decisiones de personalización visuales]** casilla de verificación También puede especificar ámbitos de decisión o superficies si es necesario. Consulte la [documentación de personalización](../personalization/rendering-personalization-content.md#automatically-rendering-content) para obtener más información sobre la renderización de contenido personalizado.

## Definir consentimiento

Una vez que haya recibido el consentimiento de su usuario, este se debe comunicar al SDK para web de Adobe Experience Platform mediante el tipo de acción Definir consentimiento. Actualmente se admiten dos tipos de estándares: Adobe y IAB TCF. Consulte [Preferencias de consentimiento del cliente de soporte](../consent/supporting-consent.md). Al utilizar la versión 2.0 del Adobe, solo se admite un valor de elemento de datos. Deberá crear un elemento de datos que se resuelva en el objeto de consentimiento.

En esta acción, también se le proporciona un campo opcional para incluir un mapa de identidad, de modo que las identidades se puedan sincronizar una vez recibido el consentimiento. La sincronización es útil cuando el consentimiento está configurado como Pendiente o Fuera porque la llamada de consentimiento es probablemente la primera llamada a activación.

## Restablecer ID de combinación de eventos

Si desea restablecer el ID de combinación de eventos en la página, puede hacerlo con esta acción. Para restablecer su ID, seleccione el ID de combinación que desee restablecer y active la acción según sea necesario.

## ¿Qué sigue?

Después de establecer las acciones, [configuración de los tipos de elementos de datos](data-element-types.md).
