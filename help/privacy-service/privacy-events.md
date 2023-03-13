---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Suscribirse a eventos de Privacy Service
description: Obtenga información sobre cómo suscribirse a eventos de Privacy Service mediante un webhook preconfigurado.
exl-id: 9bd34313-3042-46e7-b670-7a330654b178
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 2%

---

# Suscribirse a [!DNL Privacy Service Events]

[!DNL Privacy Service Events] son mensajes proporcionados por Adobe Experience Platform [!DNL Privacy Service], que aprovechan los eventos de Adobe I/O enviados a un webhook configurado para facilitar una automatización eficaz de las solicitudes de trabajo. Reducen o eliminan la necesidad de sondear el [!DNL Privacy Service] API para comprobar si un trabajo se ha completado o si se ha alcanzado un determinado hito dentro de un flujo de trabajo.

Actualmente hay cuatro tipos de notificaciones relacionadas con el ciclo de vida de la solicitud de trabajo de privacidad:

| Tipo | Descripción |
| --- | --- |
| Trabajo completado | Todo [!DNL Experience Cloud] Las aplicaciones de han informado y el estado general o global del trabajo se ha marcado como completado. |
| Error de trabajo | Una o más aplicaciones han informado de un error al procesar la solicitud. |
| Producto completado | Una de las aplicaciones asociadas a este trabajo ha finalizado su trabajo. |
| Error de producto | Una de las aplicaciones informó de un error al procesar la solicitud. |

Este documento proporciona información sobre los pasos necesarios para configurar un registro de evento para [!DNL Privacy Service] notificaciones y cómo interpretar las cargas útiles de notificaciones.

## Primeros pasos

Consulte la siguiente documentación del Privacy Service antes de iniciar este tutorial:

* [Información general de Privacy Service](./home.md)
* [Guía de API de Privacy Service](./api/overview.md)

## Registre un webhook para [!DNL Privacy Service Events]

Para poder recibir [!DNL Privacy Service Events], debe utilizar la consola de Adobe Developer para registrar un webhook en su [!DNL Privacy Service] integración.

Siga el tutorial de [suscribirse a notificaciones de [!DNL I/O Event]](../observability/alerts/subscribe.md) para ver los pasos detallados sobre cómo hacerlo. Asegúrese de elegir **[!UICONTROL Eventos de Privacy Service]** como proveedor de eventos para acceder a los eventos enumerados anteriormente.

## Recibir [!DNL Privacy Service Event] notificaciones

Una vez que haya registrado correctamente su webhook y se hayan ejecutado los trabajos de privacidad, puede empezar a recibir notificaciones de eventos. Estos eventos se pueden ver mediante el propio webhook o seleccionando el **[!UICONTROL Seguimiento de depuración]** en la información general del registro de eventos del proyecto en la consola de Adobe Developer.

![](images/privacy-events/debug-tracing.png)

El siguiente JSON es un ejemplo de [!DNL Privacy Service Event] carga útil de notificación que se enviaría a su webhook cuando una de las aplicaciones asociadas con un trabajo de privacidad haya completado su trabajo:

```json
{
  "id":"b472e249-368b-4706-90f3-1d774713f827",
  "event_id":"b116f797-e50b-432e-9c65-189106a34820",
  "specversion":"0.2",
  "type":"com.adobe.platform.gdpr.productcomplete",
  "source":"https://ns.adobe.com/platform/gdpr",
  "time":"Wed Oct 23 18:52:32 GMT 2019",
  "data":{
    "imsOrg":"{ORG_ID}",
    "value":{
      "jobId":"6f0f2b62-88a7-4515-ba05-432d9a7021c5",
      "message":"analytics.access.complete"
    }
  }
}
```

| Propiedad | Descripción |
| --- | --- |
| `id` | ID único y generado por el sistema para la notificación. |
| `type` | El tipo de notificación que se envía, dando contexto a la información proporcionada en `data`. Los valores potenciales incluyen: <ul><li>`com.adobe.platform.gdpr.jobcomplete`</li><li>`com.adobe.platform.gdpr.joberror`</li><li>`com.adobe.platform.gdpr.productcomplete`</li><li>`com.adobe.platform.gdpr.producterror`</li></ul> |
| `time` | Una marca de tiempo del momento en el que ocurrió el evento. |
| `data.value` | Contiene información adicional sobre el activador de la notificación: <ul><li>`jobId`: ID del trabajo de privacidad que activó la notificación.</li><li>`message`: Un mensaje con respecto al estado específico del trabajo. Para `productcomplete` o `producterror` notificaciones, este campo indica la aplicación del Experience Cloud en cuestión.</li></ul> |

## Pasos siguientes

En este documento se explica cómo registrar eventos de Privacy Service en un webhook configurado y cómo interpretar las cargas de notificación. Para obtener información sobre cómo rastrear trabajos de privacidad mediante la interfaz de usuario, consulte la [Guía del usuario del Privacy Service](./ui/user-guide.md).
