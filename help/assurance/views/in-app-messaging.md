---
title: Vista de mensajería en la aplicación
description: Esta guía detalla información sobre la vista Mensajería en la aplicación de Adobe Experience Platform Assurance.
exl-id: 6131289a-aebb-4b3a-9045-4b2cf23415f8
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 1%

---

# Vista Mensajería en la aplicación en Assurance

La vista Mensajería en la aplicación dentro de Adobe Experience Platform Assurance permite validar la aplicación, monitorizar los mensajes en la aplicación que se envían al dispositivo y simular mensajes en el dispositivo.

## Mensajes en el dispositivo

En la parte superior del **[!UICONTROL Mensajes en el dispositivo]** La pestaña es una **[!UICONTROL Mensaje]** desplegable. Esto incluirá todos los mensajes que se hayan recibido en la sesión de Assurance. Si un mensaje no está en la lista, significa que la aplicación nunca lo recibió.

![Mensaje](./images/in-app-messaging/message.png)

Si se selecciona un mensaje, se mostrará mucha información sobre dicho mensaje, tal como se describe en las secciones siguientes.

### Previsualización de mensaje

En el panel derecho hay un **[!UICONTROL Previsualización de mensaje]** , que muestra una vista previa del mensaje. Seleccionar **[!UICONTROL Simular en dispositivo]** enviará ese mensaje a cualquier dispositivo que esté conectado actualmente a la sesión.

![Vista previa](./images/in-app-messaging/preview.png)

### Comportamiento del mensaje

Debajo de **[!UICONTROL Previsualización de mensaje]** El panel es el **[!UICONTROL Comportamiento del mensaje]** pestaña. Tiene todos los detalles sobre cómo se muestra el mensaje. Esta información incluye información de posición, animaciones, gestos de barrido y ajustes de apariencia.

![Comportamiento](./images/in-app-messaging/gestures.png)

### Pestaña Información

En la sección izquierda, hay cuatro pestañas que muestran detalles sobre el mensaje. El **[!UICONTROL Información]** La pestaña muestra información cargada desde Adobe Journey Optimizer (AJO) acerca de la campaña de mensajes.

También puede seleccionar **[!UICONTROL Ver campaña]** para abrir el mensaje en AJO para su inspección o edición.

![Información](./images/in-app-messaging/info.png)

### Pestaña Reglas

El **[!UICONTROL Reglas]** La pestaña muestra lo que debe suceder para que se muestre este mensaje. Esto proporciona una perspectiva de qué déclencheur exactamente se mostrará un mensaje. Veamos este ejemplo:

![Reglas](./images/in-app-messaging/rules.png)

El ejemplo muestra tres condiciones diferentes para la regla. Si selecciona un evento (de una lista de eventos, la pestaña Analizar o en la cronología), ese evento se evaluará según estas reglas. Si el evento coincide con una condición, mostrará una marca de verificación verde:

![Coincidencia de regla](./images/in-app-messaging/rule-match.png)

Si el evento no coincide, mostrará un icono rojo:

![Regla no coincidente](./images/in-app-messaging/rule-mismatch.png)

Si las tres condiciones coinciden con el evento actual, se muestra el mensaje.

### Pestaña Analizar

El **[!UICONTROL Analizar]** proporciona información adicional sobre las reglas. Aquí filtramos todos los eventos de la sesión según la proximidad de la regla de mensaje al evento.

![Analizar](./images/in-app-messaging/analyze.png)

En el ejemplo de la variable **[!UICONTROL Pestaña Reglas]** , existen tres condiciones en la regla. Esta pestaña muestra qué porcentaje de la regla coincide con cada evento. La mayoría de los eventos coinciden con el 33% (una de las tres condiciones) y el resto con el 100%.

Como resultado, puede encontrar eventos que están cerca de coincidir pero que no coinciden completamente con la regla.

![Umbral](./images/in-app-messaging/threshold.png)

El **[!UICONTROL Coincidir con umbral]** slider permite filtrar qué eventos se deben mostrar. Por ejemplo, se puede establecer en 50 % - 90 % para obtener una lista de eventos que coincidan con dos de las tres condiciones exactas.

### Pestaña Interacciones

El **[!UICONTROL Interacciones]** Esta pestaña muestra una lista de los eventos de interacción que se enviaron a Edge con fines de seguimiento.

![Interacciones](./images/in-app-messaging/interactions.png)

Normalmente, cada vez que se muestra un mensaje, hay cuatro eventos de interacción:

```
trigger > display > interact > dismiss
```

La interacción &quot;interactuar&quot; tiene asociado un valor de &quot;acción&quot; adicional. Los valores posibles incluyen &quot;clicked&quot; o &quot;cancel&quot;.

La columna de validación muestra si Edge recibió y procesó correctamente el evento de interacción.

## Validación

El **[!UICONTROL Validación]** ejecuta validaciones con su sesión actual y comprueba si la aplicación se ha configurado correctamente para la mensajería en la aplicación:

![Validación](./images/in-app-messaging/validation.png)

Si se encuentran errores, se proporcionarán detalles sobre cómo corregirlos.

## Lista de eventos

![Validación](./images/in-app-messaging/event-list.png)

El **[!UICONTROL Lista de eventos]** proporciona una visión rápida de todos los eventos de la sesión de Assurance relacionados con la mensajería en la aplicación. Algunos de los eventos que pueden ver aquí son:

* Solicitudes y respuestas para recuperar mensajes
* Mostrar eventos de mensaje
* Eventos de seguimiento de interacción

En esta vista, puede utilizar muchas de las funciones de la lista de eventos estándar, como la aplicación de búsquedas, la aplicación de filtros, la adición o eliminación de columnas y la exportación de datos.

Seleccione un evento para ver los detalles sin procesar del evento en el panel derecho.

Desde el panel de detalles derecho, se puede marcar el evento seleccionado, lo que resulta útil para marcar algo que otra persona debe revisar.
