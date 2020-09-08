---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Suscripción a Eventos de Privacy Service
topic: privacy events
translation-type: tm+mt
source-git-commit: c5455dc0812b251483170ac19506d7c60ad4ecaa
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 1%

---


# Suscribirse a [!DNL Privacy Service Events]

[!DNL Privacy Service Events] son mensajes proporcionados por Adobe Experience Platform [!DNL Privacy Service], que aprovechan los Eventos de E/S de Adobe enviados a un webgancho configurado para facilitar la automatización eficaz de las solicitudes de trabajos. Reducen o eliminan la necesidad de sondear la [!DNL Privacy Service] API para comprobar si se ha completado un trabajo o si se ha alcanzado un determinado hito en un flujo de trabajo.

Actualmente existen cuatro tipos de notificaciones relacionadas con el ciclo vital de la solicitud de trabajo de privacidad:

| Tipo | Descripción |
| --- | --- |
| Trabajo completado | Todas [!DNL Experience Cloud] las solicitudes se han devuelto y el estado general o global del trabajo se ha marcado como completado. |
| Error de trabajo | Una o más aplicaciones han informado de un error al procesar la solicitud. |
| Producto completado | Una de las aplicaciones asociadas con este trabajo ha completado su trabajo. |
| Error del producto | Una de las aplicaciones informó de un error al procesar la solicitud. |

Este documento proporciona los pasos para configurar un registro de eventos para [!DNL Privacy Service] las notificaciones y cómo interpretar las cargas de notificaciones.

## Primeros pasos

Consulte la siguiente documentación del Privacy Service antes de iniciar este tutorial:

* [Información general del Privacy Service](./home.md)
* [Guía para desarrolladores de API de Privacy Service](./api/getting-started.md)

## Registro de un enlace web en [!DNL Privacy Service Events]

Para recibir [!DNL Privacy Service Events], debe utilizar la consola de desarrollador de Adobe para registrar un enlace web en la [!DNL Privacy Service] integración.

Siga el tutorial sobre la [suscripción de [!DNL I/O Event] notificaciones](../observability/notifications/subscribe.md) para ver los pasos detallados sobre cómo hacerlo. Asegúrese de elegir Eventos **[!UICONTROL de]** Privacy Service como proveedor de evento para acceder a los eventos enumerados anteriormente.

## Recibir [!DNL Privacy Service Event] notificaciones

Una vez que haya registrado correctamente los trabajos de web y privacidad, puede recibir inicios de recibir notificaciones de evento. Estos eventos se pueden ver mediante el propio webgancho o seleccionando la ficha **[!UICONTROL Seguimiento]** de depuración en la descripción general del registro de evento del proyecto en la consola de desarrollador de Adobe.

![](images/privacy-events/debug-tracing.png)

El siguiente JSON es un ejemplo de una carga útil de [!DNL Privacy Service Event] notificación que se enviaría a su enlace web cuando una de las aplicaciones asociadas con un trabajo de privacidad haya completado su trabajo:

```json
{
  "id":"b472e249-368b-4706-90f3-1d774713f827",
  "event_id":"b116f797-e50b-432e-9c65-189106a34820",
  "specversion":"0.2",
  "type":"com.adobe.platform.gdpr.productcomplete",
  "source":"https://ns.adobe.com/platform/gdpr",
  "time":"Wed Oct 23 18:52:32 GMT 2019",
  "data":{
    "imsOrg":"{IMS_ORG}",
    "value":{
      "jobId":"6f0f2b62-88a7-4515-ba05-432d9a7021c5",
      "message":"analytics.access.complete"
    }
  }
}
```

| Propiedad | Descripción |
| --- | --- |
| `id` | ID única generada por el sistema para la notificación. |
| `type` | Tipo de notificación que se envía, dando contexto a la información proporcionada en `data`. Los valores posibles incluyen: <ul><li>`com.adobe.platform.gdpr.jobcomplete`</li><li>`com.adobe.platform.gdpr.joberror`</li><li>`com.adobe.platform.gdpr.productcomplete`</li><li>`com.adobe.platform.gdpr.producterror`</li></ul> |
| `time` | Marca de hora del momento en que se produjo el evento. |
| `data.value` | Contiene información adicional sobre qué desencadenó la notificación: <ul><li>`jobId`:: ID del trabajo de privacidad que activó la notificación.</li><li>`message`:: Mensaje relativo al estado específico del trabajo. Para `productcomplete` o `producterror` notificaciones, este campo indica la aplicación Experience Cloud en cuestión.</li></ul> |

## Pasos siguientes

Este documento cubría cómo registrar los Eventos de Privacy Service en un enlace web configurado y cómo interpretar las cargas de notificación. Para obtener información sobre cómo realizar el seguimiento de los trabajos de privacidad mediante la interfaz de usuario, consulte la guía [de usuario del](./ui/user-guide.md)Privacy Service.