---
title: Tipos de acción en la extensión SDK para web de Adobe Experience Platform
description: Obtenga información acerca de los diferentes tipos de acción que proporciona la extensión de etiqueta SDK web de Adobe Experience Platform.
solution: Experience Platform
exl-id: a4bf0bb9-59b4-4c43-97e6-387768176517
source-git-commit: fb9f7757d77b221c733bbed5124fa576a6b02ed2
workflow-type: tm+mt
source-wordcount: '1264'
ht-degree: 1%

---


# Tipos de acción

Después de configurar el [Extensión de etiqueta de SDK web de Adobe Experience Platform](web-sdk-extension-configuration.md), debe configurar los tipos de acción.

Esta página describe los tipos de acción admitidos por [Extensión de etiqueta de SDK web de Adobe Experience Platform](web-sdk-extension-configuration.md).


## Aplicar respuesta {#apply-response}

Utilice el **[!UICONTROL Aplicar respuesta]** Tipo de acción cuando desea realizar varias acciones basadas en una respuesta del Edge Network. Este tipo de acción se utiliza generalmente en implementaciones híbridas en las que el servidor realiza una llamada inicial al Edge Network y, a continuación, toma la respuesta de esa llamada e inicializa el SDK web en el explorador.

El uso de este tipo de acción puede reducir los tiempos de carga del cliente para casos de uso de personalización híbrida.

![Imagen de la interfaz de usuario del Experience Platform que muestra el tipo de acción Aplicar respuesta.](assets/apply-response.png)

Este tipo de acción admite las siguientes opciones de configuración:

* **[!UICONTROL Instancia]**: seleccione la instancia del SDK web que está utilizando.
* **[!UICONTROL Encabezados de respuesta]**: seleccione el elemento de datos que devuelve un objeto que contiene las claves de encabezado y los valores devueltos por la llamada al servidor de Edge Network.
* **[!UICONTROL Cuerpo de respuesta]**: seleccione el elemento de datos que devuelve el objeto que contiene la carga útil JSON proporcionada por la respuesta del Edge Network.
* **[!UICONTROL Procesar decisiones de personalización visuales]**: Active esta opción para procesar automáticamente el contenido de personalización proporcionado por el Edge Network y ocultarlo previamente para evitar parpadeos.

## Enviar evento {#send-event}

Envía un evento al Adobe [!DNL Experience Platform] para que Adobe Experience Platform pueda recopilar los datos que envía y actuar con esa información. Seleccione una instancia (si tiene más de una). Los datos que desee enviar se pueden enviar en la variable **[!UICONTROL Datos XDM]** field. Utilice un objeto JSON que se ajuste a la estructura del esquema XDM. Este objeto se puede crear en la página o a través de un **[!UICONTROL Código personalizado]** **[!UICONTROL Elemento de datos]**.

Hay otros campos en el tipo de acción Enviar evento que también pueden ser útiles según la implementación. Tenga en cuenta que estos campos son todos opcionales.

* **Tipo:** Este campo le permite especificar un tipo de evento que se registrará en el esquema XDM. Consulte [`type`](/help/web-sdk/commands/sendevent/type.md) en el `sendEvent` para obtener más información.
* **Datos:** Los datos que no coinciden con un esquema XDM se pueden enviar mediante este campo. Este campo es útil si intenta actualizar un perfil de Adobe Target o enviar atributos de Recommendations de Target. Consulte [`data`](/help/web-sdk/commands/sendevent/data.md) en el `sendEvent` para obtener más información.<!--- **Merge ID:** If you would like to specify a merge ID for your event, you can do so in this field. Please note that the solutions downstream are not able to merge your event data at this time. -->
* **ID de conjunto de datos:** Si necesita enviar datos a un conjunto de datos que no sea el especificado en su conjunto de datos, puede especificar ese ID del conjunto de datos aquí.
* **Se descargará el documento:** Si desea asegurarse de que los eventos llegan al servidor incluso si el usuario sale de la página, consulte la **[!UICONTROL Se descargará el documento]** casilla de verificación Esto permite que los eventos lleguen al servidor, pero las respuestas se omiten.
* **Procesar decisiones de personalización visuales:** Si desea procesar contenido personalizado en la página, consulte la **[!UICONTROL Procesar decisiones de personalización visuales]** casilla de verificación También puede especificar ámbitos de decisión o superficies si es necesario. Consulte la [documentación de personalización](/help/web-sdk/personalization/rendering-personalization-content.md#automatically-rendering-content) para obtener más información sobre la renderización de contenido personalizado.

## Definir consentimiento {#set-consent}

Una vez que haya recibido el consentimiento de su usuario, este se debe comunicar al SDK para web de Adobe Experience Platform mediante el tipo de acción Definir consentimiento. Actualmente se admiten dos tipos de estándares: Adobe y IAB TCF. Consulte [Preferencias de consentimiento del cliente de soporte](../../../../web-sdk/commands/setconsent.md). Al utilizar la versión 2.0 del Adobe, solo se admite un valor de elemento de datos. Deberá crear un elemento de datos que se resuelva en el objeto de consentimiento.

En esta acción, también se le proporciona un campo opcional para incluir un mapa de identidad, de modo que las identidades se puedan sincronizar una vez recibido el consentimiento. La sincronización es útil cuando el consentimiento está configurado como Pendiente o Fuera porque la llamada de consentimiento es probablemente la primera llamada a activación.

## Actualizar variable {#update-variable}

Utilice esta acción para modificar un objeto XDM como resultado de un evento. Esta acción está diseñada para crear un objeto al que posteriormente se pueda hacer referencia desde una **[!UICONTROL Enviar evento]** acción, para registrar el objeto XDM de evento.

Para utilizar este tipo de acción, debe haber definido una [variable](data-element-types.md#variable) elemento de datos. Una vez que elija un elemento de datos variable para modificarlo, aparecerá un editor, similar al editor de la variable [Objeto XDM](data-element-types.md#xdm-object) elemento de datos.

![](assets/update-variable.png)

El esquema XDM utilizado para el editor es el esquema seleccionado en la [!UICONTROL variable] elemento de datos. Puede establecer una o más propiedades del objeto haciendo clic en una de las propiedades del árbol de la izquierda y, a continuación, modificando el valor de la derecha. Por ejemplo, en la captura de pantalla siguiente, la propiedad productionBy se establece en el elemento de datos &quot;Producido por el elemento de datos&quot;.

![](assets/update-variable-set-property.png)

Existen algunas diferencias entre el editor de la acción de la variable de actualización y el editor del elemento de datos del objeto XDM. En primer lugar, la acción de actualización de la variable tiene un elemento de nivel raíz denominado &quot;xdm&quot;. Si hace clic en este elemento, puede especificar un elemento de datos para utilizar y establecer el objeto completo. En segundo lugar, la acción actualizar variable tiene casillas de verificación para borrar los datos del objeto xdm. Haga clic en una de las propiedades de la izquierda y, a continuación, marque la casilla de verificación de la derecha para borrar el valor. Esto borrará el valor actual antes de establecer cualquier valor en la variable.

## Enviar evento multimedia {#send-media-event}

Envía un evento multimedia a Adobe Experience Platform o Adobe Analytics. Esta acción es útil cuando realiza un seguimiento de eventos de medios en el sitio web. Seleccione una instancia (si tiene más de una). La acción requiere un `playerId` que representa un identificador único para una sesión de medios rastreada. También requiere un **[!UICONTROL Calidad de la experiencia]** y una `playhead` elemento de datos al iniciar una sesión de contenido.

![Imagen de la IU de Platform que muestra la pantalla de envío de eventos multimedia.](assets/send-media-event.png)

El **[!UICONTROL Enviar evento multimedia]** el tipo de acción admite las siguientes propiedades:

* **[!UICONTROL Instancia]**: la instancia del SDK web que se está utilizando.
* **[!UICONTROL Tipo de evento de medios]**: tipo de evento multimedia que se rastrea.
* **[!UICONTROL ID del reproductor]**: el identificador único de la sesión de contenidos.
* **[!UICONTROL Cabezal De Reproducción]**: Posición actual de la reproducción del contenido, en segundos.
* **[!UICONTROL Detalles de sesión de medios]**: al enviar un evento de inicio de contenido, se deben especificar los detalles de sesión de contenido necesarios.
* **[!UICONTROL Detalles del capítulo]**: en esta sección puede especificar los detalles del capítulo al enviar un evento de medios de inicio de capítulos.
* **[!UICONTROL Detalles de publicidad]**: Al enviar un `AdBreakStart` evento, debe especificar los detalles publicitarios necesarios.
* **[!UICONTROL Detalles de Advertising pod]**: Detalles sobre el pod de publicidad al enviar un `AdStart` evento.
* **[!UICONTROL Detalles del error]**: Detalles sobre el error de reproducción que se está rastreando.
* **[!UICONTROL Detalles de actualización de estado]**: El estado del reproductor que se está actualizando.
* **[!UICONTROL Metadatos personalizados]**: los metadatos personalizados sobre el evento multimedia del que se está realizando un seguimiento.
* **[!UICONTROL Calidad de la experiencia]**: la calidad de los medios de los datos de experiencia que se están rastreando.

## Obtener rastreador de Media Analytics {#get-media-analytics-tracker}

Esta acción se utiliza para obtener la API heredada de Media Analytics. Al configurar la acción y proporcionar un nombre de objeto, la API heredada de Media Analytics se exportará a ese objeto de ventana. Si no se proporciona ninguno, se exporta a `window.Media` como la biblioteca Media JS actual.

![Imagen de la IU de Platform que muestra el tipo de acción Obtener rastreador de Media Analytics.](assets/get-media-analytics-tracker.png)

## Redirigir con identidad {#redirect-with-identity}

Utilice este tipo de acción para compartir identidades de la página actual con otros dominios. Esta acción está diseñada para utilizarse con un **[!UICONTROL click]** tipo de evento y una condición de comparación de valores. Consulte [Añadir identidad a una URL mediante la extensión del SDK web](../../../../web-sdk/commands/appendidentitytourl.md#extension) para obtener más información sobre cómo utilizar este tipo de acción.

## Pasos siguientes {#next-steps}

Después de leer este artículo, debería comprender mejor cómo configurar sus acciones. A continuación, obtenga información sobre cómo [configuración de los tipos de elementos de datos](data-element-types.md).
