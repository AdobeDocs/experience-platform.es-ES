---
title: Tipos de acción en la extensión SDK para web de Adobe Experience Platform
description: Obtenga información acerca de los diferentes tipos de acción que proporciona la extensión de etiqueta SDK web de Adobe Experience Platform.
solution: Experience Platform
exl-id: a4bf0bb9-59b4-4c43-97e6-387768176517
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 2%

---


# Tipos de acción

Después de configurar el [Extensión de etiqueta de SDK web de Adobe Experience Platform](web-sdk-extension-configuration.md), debe configurar los tipos de acción.

Esta página describe los tipos de acción admitidos por [Extensión de etiqueta de SDK web de Adobe Experience Platform](web-sdk-extension-configuration.md).

## Enviar evento {#send-event}

Envía un evento al Adobe [!DNL Experience Platform] para que Adobe Experience Platform pueda recopilar los datos que envía y actuar con esa información. Seleccione una instancia (si tiene más de una). Los datos que desee enviar se pueden enviar en la variable **[!UICONTROL Datos XDM]** field. Utilice un objeto JSON que se ajuste a la estructura del esquema XDM. Este objeto se puede crear en la página o a través de un **[!UICONTROL Código personalizado]** **[!UICONTROL Elemento de datos]**.

Hay otros campos en el tipo de acción Enviar evento que también pueden ser útiles según la implementación. Tenga en cuenta que estos campos son todos opcionales.

- **Tipo:** Este campo le permite especificar un tipo de evento que se registrará en el esquema XDM. Consulte [`type`](/help/web-sdk/commands/sendevent/type.md) en el `sendEvent` para obtener más información.
- **Datos:** Los datos que no coinciden con un esquema XDM se pueden enviar mediante este campo. Este campo es útil si intenta actualizar un perfil de Adobe Target o enviar atributos de Recommendations de Target. Consulte [`data`](/help/web-sdk/commands/sendevent/data.md) en el `sendEvent` para obtener más información.<!--- **Merge ID:** If you would like to specify a merge ID for your event, you can do so in this field. Please note that the solutions downstream are not able to merge your event data at this time. -->
- **ID de conjunto de datos:** Si necesita enviar datos a un conjunto de datos que no sea el especificado en su conjunto de datos, puede especificar ese ID del conjunto de datos aquí.
- **Se descargará el documento:** Si desea asegurarse de que los eventos llegan al servidor incluso si el usuario sale de la página, consulte la **[!UICONTROL Se descargará el documento]** casilla de verificación Esto permite que los eventos lleguen al servidor, pero las respuestas se omiten.
- **Procesar decisiones de personalización visuales:** Si desea procesar contenido personalizado en la página, consulte la **[!UICONTROL Procesar decisiones de personalización visuales]** casilla de verificación También puede especificar ámbitos de decisión o superficies si es necesario. Consulte la [documentación de personalización](/help/web-sdk/personalization/rendering-personalization-content.md#automatically-rendering-content) para obtener más información sobre la renderización de contenido personalizado.

## Definir consentimiento {#set-consent}

Una vez que haya recibido el consentimiento de su usuario, este se debe comunicar al SDK para web de Adobe Experience Platform mediante el tipo de acción Definir consentimiento. Actualmente se admiten dos tipos de estándares: Adobe y IAB TCF. Consulte [Preferencias de consentimiento del cliente de soporte](/help/web-sdk/consent/supporting-consent.md). Al utilizar la versión 2.0 del Adobe, solo se admite un valor de elemento de datos. Deberá crear un elemento de datos que se resuelva en el objeto de consentimiento.

En esta acción, también se le proporciona un campo opcional para incluir un mapa de identidad, de modo que las identidades se puedan sincronizar una vez recibido el consentimiento. La sincronización es útil cuando el consentimiento está configurado como Pendiente o Fuera porque la llamada de consentimiento es probablemente la primera llamada a activación.

## Actualizar variable {#update-variable}

Utilice esta acción para modificar un objeto XDM como resultado de un evento. Esta acción está diseñada para crear un objeto al que posteriormente se pueda hacer referencia desde una **[!UICONTROL Enviar evento]** acción, para registrar el objeto XDM de evento.

Para utilizar este tipo de acción, debe haber definido una [variable](data-element-types.md#variable) elemento de datos. Una vez que elija un elemento de datos variable para modificarlo, aparecerá un editor, similar al editor de la variable [Objeto XDM](data-element-types.md#xdm-object) elemento de datos.

![](assets/update-variable.png)

El esquema XDM utilizado para el editor es el esquema seleccionado en la [!UICONTROL variable] elemento de datos. Puede establecer una o más propiedades del objeto haciendo clic en una de las propiedades del árbol de la izquierda y, a continuación, modificando el valor de la derecha. Por ejemplo, en la captura de pantalla siguiente, la propiedad productionBy se establece en el elemento de datos &quot;Producido por el elemento de datos&quot;.

![](assets/update-variable-set-property.png)

Existen algunas diferencias entre el editor de la acción de la variable de actualización y el editor del elemento de datos del objeto XDM. En primer lugar, la acción de actualización de la variable tiene un elemento de nivel raíz denominado &quot;xdm&quot;. Si hace clic en este elemento, puede especificar un elemento de datos para utilizar y establecer el objeto completo. En segundo lugar, la acción actualizar variable tiene casillas de verificación para borrar los datos del objeto xdm. Haga clic en una de las propiedades de la izquierda y, a continuación, marque la casilla de verificación de la derecha para borrar el valor. Esto borrará el valor actual antes de establecer cualquier valor en la variable.

## Pasos siguientes {#next-steps}

Después de leer este artículo, debería comprender mejor cómo configurar sus acciones. A continuación, obtenga información sobre cómo [configuración de los tipos de elementos de datos](data-element-types.md).
