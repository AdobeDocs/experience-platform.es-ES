---
title: Tipos de acción en la extensión del SDK web de Adobe Experience Platform
description: Obtenga información sobre los distintos tipos de acciones proporcionados por la extensión de etiqueta del SDK web de Adobe Experience Platform.
solution: Experience Platform
exl-id: a4bf0bb9-59b4-4c43-97e6-387768176517
source-git-commit: db7700d5c504e484f9571bbb82ff096497d0c96e
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 2%

---


# Tipos de acción

Después de configurar la variable [Extensión de la etiqueta del SDK web de Adobe Experience Platform](web-sdk-extension-configuration.md), debe configurar los tipos de acción.

Esta página describe los tipos de acción admitidos por el [Extensión de la etiqueta del SDK web de Adobe Experience Platform](web-sdk-extension-configuration.md).

## Enviar evento {#send-event}

Envía un evento a Adobe [!DNL Experience Platform] para que Adobe Experience Platform pueda recopilar los datos que envía y actuar en consecuencia. Seleccione una instancia (si tiene más de una). Los datos que desee enviar se pueden enviar en la variable **[!UICONTROL Datos XDM]** campo . Utilice un objeto JSON que se ajuste a la estructura del esquema XDM. Este objeto se puede crear en la página o a través de un **[!UICONTROL Código personalizado]** **[!UICONTROL Elemento de datos]**.

Existen otros campos en el tipo de acción Enviar evento que también pueden resultar útiles en función de la implementación. Tenga en cuenta que todos estos campos son opcionales.

- **Tipo:** Este campo permite especificar un tipo de evento que se registrará en el esquema XDM. Consulte la [documentación](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#using-the-sendbeacon-api) para obtener más información sobre los tipos de eventos predeterminados.
- **Datos:** Los datos que no coinciden con un esquema XDM se pueden enviar mediante este campo. Este campo es útil si está intentando actualizar un perfil de Adobe Target o enviar atributos de Recommendations de Target. Para ver ejemplos, consulte [documentación](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=es).<!--- **Merge ID:** If you would like to specify a merge ID for your event, you can do so in this field. Please note that the solutions downstream are not able to merge your event data at this time. -->
- **ID del conjunto de datos:** Si necesita enviar datos a un conjunto de datos que no sea el especificado en su conjunto de datos, puede especificar ese ID de conjunto de datos aquí.
- **El documento se descargará:** Si desea asegurarse de que los eventos llegan al servidor incluso si el usuario sale de la página, consulte la **[!UICONTROL El documento se descargará]** casilla de verificación. Esto permite que los eventos lleguen al servidor, pero las respuestas se ignoran.
- **Procesar decisiones de personalización visual:** Si desea procesar contenido personalizado en la página, marque la casilla **[!UICONTROL Procesar decisiones de personalización visual]** casilla de verificación. También puede especificar ámbitos de decisión o superficies si es necesario. Consulte la [documentación de personalización](../personalization/rendering-personalization-content.md#automatically-rendering-content) para obtener más información sobre la renderización de contenido personalizado.

## Establecer consentimiento {#set-consent}

Una vez que el usuario haya dado su consentimiento, este consentimiento debe comunicarse al SDK web de Adobe Experience Platform mediante el tipo de acción &quot;Definir consentimiento&quot;. Actualmente se admiten dos tipos de estándares: Adobe y IAB TCF. Consulte [Compatibilidad con las preferencias de consentimiento del cliente](../consent/supporting-consent.md). Al utilizar Adobe versión 2.0, solo se admite un valor de elemento de datos. Deberá crear un elemento de datos que se resuelva en el objeto de consentimiento.

En esta acción, también se le proporcionará un campo opcional para incluir un mapa de identidad de modo que las identidades se puedan sincronizar una vez recibido el consentimiento. La sincronización es útil cuando el consentimiento está configurado como &quot;Pendiente&quot; o &quot;Fuera&quot; porque es probable que la llamada de consentimiento sea la primera llamada a activarse.

## Restablecer ID de combinación de eventos {#reset-event-merge-id}

Si desea restablecer el ID de combinación de eventos en la página, puede hacerlo con esta acción. Para restablecer su ID, seleccione el ID de combinación que desee restablecer y active la acción según sea necesario.

## Variable de actualización (Beta) {#update-variable}

>[!IMPORTANT]
>
>Actualmente se trata de una funcionalidad beta y está sujeta a cambios. Las versiones futuras pueden contener cambios de ruptura.

Utilice esta acción para modificar un objeto XDM como resultado de un evento. El objetivo de esta acción es crear un objeto al que posteriormente se pueda hacer referencia desde un **[!UICONTROL Enviar evento]** para registrar el objeto XDM de evento.

Para utilizar este tipo de acción debe haber definido una [variable](data-element-types.md#variable) elemento de datos. Una vez que elija un elemento de datos variable para modificarlo, aparecerá un editor, similar al del [Objeto XDM](data-element-types.md#xdm-object) elemento de datos.

![](./assets/update-variable.png)

El esquema XDM que se utiliza para el editor es el esquema seleccionado en el [!UICONTROL variable] elemento de datos. Puede establecer una o varias propiedades del objeto haciendo clic en una de las propiedades del árbol de la izquierda y, a continuación, modificando el valor de la derecha. Por ejemplo, en la captura de pantalla siguiente, la propiedad productionBy se establece en el elemento de datos &quot;Produced by data element&quot;.

![](./assets/update-variable-set-property.png)

Existen algunas diferencias entre el editor en la acción de la variable de actualización y el editor en el elemento de datos del objeto XDM. En primer lugar, la acción de la variable de actualización tiene un elemento de nivel raíz denominado &quot;xdm&quot;. Si hace clic en este elemento, puede especificar un elemento de datos para utilizarlo para configurar el objeto completo. En segundo lugar, la acción actualizar variable tiene casillas de verificación para borrar los datos del objeto xdm. Haga clic en una de las propiedades de la izquierda y, a continuación, marque la casilla de verificación de la derecha para borrar el valor. Esto borrará el valor actual antes de establecer cualquier valor en la variable .

## Pasos siguientes {#next-steps}

Después de leer este artículo, debe comprender mejor cómo configurar las acciones. A continuación, lea sobre cómo [configurar los tipos de elementos de datos](data-element-types.md).
