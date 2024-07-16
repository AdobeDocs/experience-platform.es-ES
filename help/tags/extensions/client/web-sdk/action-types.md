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

Después de configurar la [extensión de etiquetas del SDK web de Adobe Experience Platform](web-sdk-extension-configuration.md), debe configurar los tipos de acción.

En esta página se describen los tipos de acción admitidos por la [extensión de etiqueta de SDK web de Adobe Experience Platform](web-sdk-extension-configuration.md).


## Aplicar respuesta {#apply-response}

Utilice el tipo de acción **[!UICONTROL Aplicar respuesta]** cuando desee realizar diversas acciones basadas en una respuesta del Edge Network. Este tipo de acción se utiliza generalmente en implementaciones híbridas en las que el servidor realiza una llamada inicial al Edge Network y, a continuación, toma la respuesta de esa llamada e inicializa el SDK web en el explorador.

El uso de este tipo de acción puede reducir los tiempos de carga del cliente para casos de uso de personalización híbrida.

![Imagen de la interfaz de usuario del Experience Platform que muestra el tipo de acción Aplicar respuesta.](assets/apply-response.png)

Este tipo de acción admite las siguientes opciones de configuración:

* **[!UICONTROL Instancia]**: seleccione la instancia del SDK web que está utilizando.
* **[!UICONTROL Encabezados de respuesta]**: seleccione el elemento de datos que devuelve un objeto que contiene las claves de encabezado y los valores devueltos por la llamada al servidor del Edge Network.
* **[!UICONTROL Cuerpo de respuesta]**: seleccione el elemento de datos que devuelve el objeto que contiene la carga útil JSON proporcionada por la respuesta del Edge Network.
* **[!UICONTROL Procesar decisiones de personalización visuales]**: habilite esta opción para procesar automáticamente el contenido de personalización proporcionado por el Edge Network y ocultarlo previamente para evitar parpadeos.

## Enviar evento {#send-event}

Envía un evento al Adobe [!DNL Experience Platform] para que Adobe Experience Platform pueda recopilar los datos enviados y actuar con esa información. Seleccione una instancia (si tiene más de una). Los datos que desee enviar se pueden enviar en el campo **[!UICONTROL Datos XDM]**. Utilice un objeto JSON que se ajuste a la estructura del esquema XDM. Este objeto se puede crear en la página o mediante un **[!UICONTROL código personalizado]** **[!UICONTROL elemento de datos]**.

Hay otros campos en el tipo de acción Enviar evento que también pueden ser útiles según la implementación. Tenga en cuenta que estos campos son todos opcionales.

* **Tipo:** Este campo le permite especificar un tipo de evento que se registrará en el esquema XDM. Consulte [`type`](/help/web-sdk/commands/sendevent/type.md) en el comando `sendEvent` para obtener más información.
* **Datos:** Los datos que no coinciden con un esquema XDM se pueden enviar mediante este campo. Este campo es útil si intenta actualizar un perfil de Adobe Target o enviar atributos de Recommendations de Target. Vea [`data`](/help/web-sdk/commands/sendevent/data.md) en el comando `sendEvent` para obtener más información.<!--- **Merge ID:** If you would like to specify a merge ID for your event, you can do so in this field. Please note that the solutions downstream are not able to merge your event data at this time. -->
* **ID del conjunto de datos:** Si necesita enviar datos a un conjunto de datos distinto del que especificó en su secuencia de datos, puede especificar ese ID del conjunto de datos aquí.
* Se descargará **documento:** Si desea asegurarse de que los eventos lleguen al servidor incluso si el usuario sale de la página, marque la casilla de verificación **[!UICONTROL Documento se descargará]**. Esto permite que los eventos lleguen al servidor, pero las respuestas se omiten.
* **Procesar decisiones de personalización visuales:** Si desea procesar contenido personalizado en su página, marque la casilla de verificación **[!UICONTROL Procesar decisiones de personalización visual]**. También puede especificar ámbitos de decisión o superficies si es necesario. Consulte la [documentación de personalización](/help/web-sdk/personalization/rendering-personalization-content.md#automatically-rendering-content) para obtener más información sobre cómo procesar contenido personalizado.

## Definir consentimiento {#set-consent}

Una vez que haya recibido el consentimiento de su usuario, este se debe comunicar al SDK para web de Adobe Experience Platform mediante el tipo de acción Definir consentimiento. Actualmente se admiten dos tipos de estándares: Adobe y IAB TCF. Ver [Preferencias de consentimiento del cliente de soporte](../../../../web-sdk/commands/setconsent.md). Al utilizar la versión 2.0 del Adobe, solo se admite un valor de elemento de datos. Deberá crear un elemento de datos que se resuelva en el objeto de consentimiento.

En esta acción, también se le proporciona un campo opcional para incluir un mapa de identidad, de modo que las identidades se puedan sincronizar una vez recibido el consentimiento. La sincronización es útil cuando el consentimiento está configurado como Pendiente o Fuera porque la llamada de consentimiento es probablemente la primera llamada a activación.

## Actualizar variable {#update-variable}

Utilice esta acción para modificar un objeto XDM como resultado de un evento. Esta acción está diseñada para crear un objeto al que posteriormente se pueda hacer referencia desde una acción **[!UICONTROL Enviar evento]** para registrar el objeto XDM de evento.

Para usar este tipo de acción, debe haber definido un elemento de datos [variable](data-element-types.md#variable). Una vez que elija un elemento de datos de variable para modificar, aparecerá un editor, similar al editor del elemento de datos [XDM object](data-element-types.md#xdm-object).

![](assets/update-variable.png)

El esquema XDM utilizado para el editor es el esquema seleccionado en el elemento de datos [!UICONTROL variable]. Puede establecer una o más propiedades del objeto haciendo clic en una de las propiedades del árbol de la izquierda y, a continuación, modificando el valor de la derecha. Por ejemplo, en la captura de pantalla siguiente, la propiedad productionBy se establece en el elemento de datos &quot;Producido por el elemento de datos&quot;.

![](assets/update-variable-set-property.png)

Existen algunas diferencias entre el editor de la acción de la variable de actualización y el editor del elemento de datos del objeto XDM. En primer lugar, la acción de actualización de la variable tiene un elemento de nivel raíz denominado &quot;xdm&quot;. Si hace clic en este elemento, puede especificar un elemento de datos para utilizar y establecer el objeto completo. En segundo lugar, la acción actualizar variable tiene casillas de verificación para borrar los datos del objeto xdm. Haga clic en una de las propiedades de la izquierda y, a continuación, marque la casilla de verificación de la derecha para borrar el valor. Esto borrará el valor actual antes de establecer cualquier valor en la variable.

## Enviar evento multimedia {#send-media-event}

Envía un evento multimedia a Adobe Experience Platform o Adobe Analytics. Esta acción es útil cuando realiza un seguimiento de eventos de medios en el sitio web. Seleccione una instancia (si tiene más de una). La acción requiere un `playerId` que represente un identificador único para una sesión multimedia rastreada. También requiere **[!UICONTROL Calidad de la experiencia]** y un elemento de datos `playhead` al iniciar una sesión multimedia.

![Imagen de la interfaz de usuario de la plataforma que muestra la pantalla de eventos de medios de envío.](assets/send-media-event.png)

El tipo de acción **[!UICONTROL Enviar evento multimedia]** admite las siguientes propiedades:

* **[!UICONTROL Instancia]**: La instancia del SDK web que se está usando.
* **[!UICONTROL Tipo de evento de medios]**: El tipo de evento de medios que se está rastreando.
* **[!UICONTROL ID del reproductor]**: El identificador único de la sesión multimedia.
* **[!UICONTROL Cabezal de reproducción]**: Posición actual de la reproducción de contenido, en segundos.
* **[!UICONTROL Detalles de la sesión de contenido]**: al enviar un evento de inicio de contenido, se deben especificar los detalles necesarios de la sesión de contenido.
* **[!UICONTROL Detalles del capítulo]**: En esta sección puede especificar los detalles del capítulo al enviar un evento multimedia de inicio de capítulo.
* **[!UICONTROL Detalles de Advertising]**: al enviar un evento `AdBreakStart`, debe especificar los detalles de publicidad requeridos.
* **[!UICONTROL Detalles del pod de Advertising]**: detalles sobre el pod de publicidad al enviar un evento `AdStart`.
* **[!UICONTROL Detalles del error]**: Detalles sobre el error de reproducción que se está rastreando.
* **[!UICONTROL Detalles de actualización de estado]**: El estado del reproductor que se está actualizando.
* **[!UICONTROL Metadatos personalizados]**: Los metadatos personalizados sobre el evento multimedia que se está rastreando.
* **[!UICONTROL Calidad de la experiencia]**: La calidad multimedia de los datos de experiencia de los que se está realizando un seguimiento.

## Obtener rastreador de Media Analytics {#get-media-analytics-tracker}

Esta acción se utiliza para obtener la API heredada de Media Analytics. Al configurar la acción y proporcionar un nombre de objeto, la API heredada de Media Analytics se exportará a ese objeto de ventana. Si no se proporciona ninguno, se exportará a `window.Media` como lo hace la biblioteca Media JS actual.

![Imagen de la interfaz de usuario de la plataforma que muestra el tipo de acción Obtener rastreador de Media Analytics.](assets/get-media-analytics-tracker.png)

## Redirigir con identidad {#redirect-with-identity}

Utilice este tipo de acción para compartir identidades de la página actual con otros dominios. Esta acción está diseñada para utilizarse con un tipo de evento **[!UICONTROL click]** y una condición de comparación de valores. Consulte [Anexar identidad a una URL mediante la extensión del SDK web](../../../../web-sdk/commands/appendidentitytourl.md#extension) para obtener más información sobre cómo usar este tipo de acción.

## Pasos siguientes {#next-steps}

Después de leer este artículo, debería comprender mejor cómo configurar sus acciones. A continuación, obtenga información sobre cómo [configurar los tipos de elementos de datos](data-element-types.md).
