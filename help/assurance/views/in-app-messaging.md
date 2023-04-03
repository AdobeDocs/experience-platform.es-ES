---
title: Vista de mensajería en la aplicación
description: Esta guía detalla información sobre la vista Mensajería en la aplicación en Adobe Experience Platform Assurance.
source-git-commit: 5778d4db27d0f57281821dc8e042a31b69745514
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 1%

---


# Vista Mensajería en la aplicación en Assurance

La vista Mensajería en la aplicación dentro de Adobe Experience Platform Assurance permite validar la aplicación, supervisar los mensajes en la aplicación que se envían al dispositivo y simular mensajes en el dispositivo.

## Mensajes en el dispositivo

En la parte superior del **[!UICONTROL Mensajes en el dispositivo]** es una **[!UICONTROL Mensaje]** lista desplegable. Esto incluirá todos los mensajes recibidos en la sesión de Assurance. Si un mensaje no está en esta lista, significa que la aplicación nunca lo recibió.

![Mensaje](./images/in-app-messaging/message.png)

Al seleccionar un mensaje, se mostrará mucha información sobre ese mensaje, tal como se describe en las secciones siguientes.

### Vista previa del mensaje

En el panel derecho hay una **[!UICONTROL Vista previa del mensaje]** , que muestra una vista previa del mensaje. Selección **[!UICONTROL Simular en el dispositivo]** enviará ese mensaje a cualquier dispositivo que esté conectado a la sesión.

![Vista previa](./images/in-app-messaging/preview.png)

### Comportamiento del mensaje

Debajo de **[!UICONTROL Vista previa del mensaje]** es el **[!UICONTROL Comportamiento del mensaje]** pestaña . Esto tiene todos los detalles sobre cómo se muestra el mensaje. Esta información incluye información de posición, animaciones, gestos de barrido y ajustes de apariencia.

![Comportamiento](./images/in-app-messaging/gestures.png)

### Ficha Información

En la sección izquierda, hay cuatro pestañas que muestran detalles sobre el mensaje. La variable **[!UICONTROL Información]** muestra información cargada desde Adobe Journey Optimizer (AJO) sobre la campaña de mensajes.

También puede seleccionar **[!UICONTROL Ver campaña]** para abrir el mensaje en AJO para su inspección o edición.

![Información](./images/in-app-messaging/info.png)

### Ficha Reglas

La variable **[!UICONTROL Reglas]** muestra lo que debe suceder para que se muestre este mensaje. Esto proporciona una perspectiva exacta de qué déclencheur un mensaje para mostrarse. Mirando este ejemplo:

![Reglas](./images/in-app-messaging/rules.png)

El ejemplo muestra tres condiciones diferentes para la regla. Si selecciona un evento (de una lista de eventos, la ficha Analizar o la cronología), ese evento se evaluará en relación con estas reglas. Si el evento coincide con una condición, mostrará una marca de verificación verde:

![Coincidencia de regla](./images/in-app-messaging/rule-match.png)

Si el evento no coincide, se mostrará un icono rojo:

![Discordancia de reglas](./images/in-app-messaging/rule-mismatch.png)

Si las tres condiciones coinciden con el evento actual, se mostrará el mensaje.

### Pestaña Analizar

La variable **[!UICONTROL Analizar]** proporciona perspectivas adicionales sobre las reglas. Aquí, filtramos todos los eventos de la sesión en función de la proximidad de la regla del mensaje al evento.

![Analizar](./images/in-app-messaging/analyze.png)

En el ejemplo de la sección **[!UICONTROL Ficha Reglas]** , hay tres condiciones en la regla. Esta pestaña muestra el porcentaje de la regla con el que coincide cada evento. La mayoría de los eventos coinciden en un 33% (una de las tres condiciones) y el resto en un 100%.

Como resultado, puede encontrar eventos que estén cerca de coincidir pero que no coincidan completamente con la regla.

![Umbral](./images/in-app-messaging/threshold.png)

La variable **[!UICONTROL Umbral de coincidencia]** El control deslizante le permite filtrar qué eventos se deben mostrar. Por ejemplo, esto podría establecerse en 50 % - 90 % para obtener una lista de eventos que coincidan exactamente con dos de las tres condiciones.

### Ficha Interacciones

La variable **[!UICONTROL Interacciones]** La pestaña muestra una lista de eventos de interacción que se enviaron a Edge para realizar un seguimiento.

![Interacciones](./images/in-app-messaging/interactions.png)

Normalmente hay cuatro eventos de interacción cada vez que se muestra un mensaje:

```
trigger > display > interact > dismiss
```

La interacción &quot;interactuar&quot; tiene un valor &quot;acción&quot; adicional asociado a ella. Los valores posibles incluyen &quot;clic&quot; o &quot;cancelar&quot;.

La columna de validación muestra si Edge recibió y procesó correctamente el evento de interacción.

## Validación

La variable **[!UICONTROL Validación]** ejecuta validaciones en la sesión actual, comprobando si la aplicación se ha configurado correctamente para la mensajería en la aplicación:

![Validación](./images/in-app-messaging/validation.png)

Si se han encontrado errores, se proporcionarán detalles sobre cómo corregirlos.

## Lista de eventos

![Validación](./images/in-app-messaging/event-list.png)

La variable **[!UICONTROL Lista de eventos]** proporciona una vista rápida de todos los eventos de la sesión de Assurance relacionados con la mensajería en la aplicación. Algunos de los eventos que puede ver aquí son:

* Solicitudes y respuestas para recuperar mensajes
* Mostrar eventos de mensaje
* Eventos de seguimiento de interacción

En esta vista, puede utilizar muchas de las funciones de la lista de eventos estándar, incluidas la aplicación de búsquedas, la aplicación de filtros, la adición o eliminación de columnas y la exportación de datos.

Seleccione un evento para ver los detalles sin procesar del evento en el panel derecho.

Desde el panel de detalles derecho, el evento seleccionado se puede marcar, lo que resulta útil para marcar algo que otra persona debe revisar.
