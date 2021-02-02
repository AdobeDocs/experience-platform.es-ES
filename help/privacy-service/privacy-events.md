---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Suscripción a Eventos de Privacy Service
topic: privacy events
description: Obtenga información sobre cómo suscribirse a eventos Privacy Service mediante un enlace web preconfigurado.
translation-type: tm+mt
source-git-commit: 2b919a3b6cbbd59521874cfd2d11e20de3077740
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 1%

---


# Suscribirse a [!DNL Privacy Service Events]

[!DNL Privacy Service Events] son mensajes proporcionados por Adobe Experience Platform  [!DNL Privacy Service], que aprovechan los Eventos de Adobe I/O enviados a un enlace web configurado para facilitar la automatización eficaz de las solicitudes de trabajo. Reducen o eliminan la necesidad de sondear la API [!DNL Privacy Service] para comprobar si se ha completado un trabajo o si se ha alcanzado un determinado hito en un flujo de trabajo.

Actualmente existen cuatro tipos de notificaciones relacionadas con el ciclo vital de la solicitud de trabajo de privacidad:

| Tipo | Descripción |
| --- | --- |
| Trabajo completado | Todas las aplicaciones [!DNL Experience Cloud] han informado y el estado global o general del trabajo se ha marcado como completado. |
| Error de trabajo | Una o más aplicaciones han informado de un error al procesar la solicitud. |
| Producto completado | Una de las aplicaciones asociadas con este trabajo ha completado su trabajo. |
| Error del producto | Una de las aplicaciones informó de un error al procesar la solicitud. |

Este documento proporciona los pasos para configurar un registro de evento para las notificaciones [!DNL Privacy Service] y cómo interpretar las cargas de notificación.

## Primeros pasos

Consulte la siguiente documentación del Privacy Service antes de iniciar este tutorial:

* [Información general del Privacy Service](./home.md)
* [Guía para desarrolladores de API de Privacy Service](./api/getting-started.md)

## Registrar un enlace web en [!DNL Privacy Service Events]

Para recibir [!DNL Privacy Service Events], debe utilizar Adobe Developer Console para registrar un enlace web en la integración [!DNL Privacy Service].

Siga el tutorial sobre [suscripción a [!DNL I/O Event] notificaciones](../observability/notifications/subscribe.md) para ver los pasos detallados sobre cómo realizar esto. Asegúrese de elegir **[!UICONTROL Eventos de Privacy Service]** como proveedor de evento para acceder a los eventos enumerados anteriormente.

## Recibir [!DNL Privacy Service Event] notificaciones

Una vez que haya registrado correctamente los trabajos de web y privacidad, puede recibir inicios de recibir notificaciones de evento. Estos eventos se pueden ver mediante el propio webgancho o seleccionando la ficha **[!UICONTROL Seguimiento de depuración]** en la descripción general del registro de evento del proyecto en Adobe Developer Console.

![](images/privacy-events/debug-tracing.png)

El siguiente JSON es un ejemplo de una carga útil de notificación [!DNL Privacy Service Event] que se enviaría a su enlace web cuando una de las aplicaciones asociadas con un trabajo de privacidad haya completado su trabajo:

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
| `type` | El tipo de notificación que se envía, dando contexto a la información proporcionada en `data`. Los valores posibles incluyen: <ul><li>`com.adobe.platform.gdpr.jobcomplete`</li><li>`com.adobe.platform.gdpr.joberror`</li><li>`com.adobe.platform.gdpr.productcomplete`</li><li>`com.adobe.platform.gdpr.producterror`</li></ul> |
| `time` | Marca de hora del momento en que se produjo el evento. |
| `data.value` | Contiene información adicional sobre qué desencadenó la notificación: <ul><li>`jobId`:: ID del trabajo de privacidad que activó la notificación.</li><li>`message`:: Mensaje relativo al estado específico del trabajo. Para las notificaciones `productcomplete` o `producterror`, este campo indica la aplicación Experience Cloud en cuestión.</li></ul> |

## Pasos siguientes

Este documento cubría cómo registrar los Eventos de Privacy Service en un enlace web configurado y cómo interpretar las cargas de notificación. Para obtener información sobre cómo rastrear los trabajos de privacidad mediante la interfaz de usuario, consulte la [guía del usuario del Privacy Service](./ui/user-guide.md).