---
keywords: Experience Platform;inicio;temas populares;notificaciones de ingesta de datos;notificaciones;eventos de suscripción;eventos de estado de ingesta de datos;eventos de estado;suscripción;notificaciones de estado;
solution: Experience Platform
title: Notificaciones de ingesta de datos
topic-legacy: overview
description: Para ayudar a monitorizar el proceso de ingesta, Adobe Experience Platform permite suscribirse a un conjunto de eventos que se publican en cada paso del proceso y le notifican el estado de los datos introducidos y los posibles errores.
exl-id: fd34e1ab-f6f6-44f0-88ee-7020e9322c39
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 2%

---

# Notificaciones de ingesta de datos

El proceso de ingesta de datos en Adobe Experience Platform consta de varios pasos. Una vez que identifique los archivos de datos que deben ingerirse en [!DNL Platform], el proceso de ingesta comienza y cada paso se produce de forma consecutiva hasta que los datos se introducen correctamente o no. El proceso de ingesta se puede iniciar utilizando la variable [API de ingesta de datos de Adobe Experience Platform](https://www.adobe.io/experience-platform-apis/references/data-ingestion/) o utilizando [!DNL Experience Platform] interfaz de usuario.

Datos cargados en [!DNL Platform] debe seguir varios pasos para llegar a su destino, [!DNL Data Lake] o [!DNL Real-Time Customer Profile] almacén de datos. Cada paso implica procesar los datos, validarlos y, después, almacenarlos antes de pasarlos al siguiente paso. En función de la cantidad de datos introducidos, este proceso puede llevar mucho tiempo y siempre existe la posibilidad de que el proceso falle debido a errores de validación, semántica o procesamiento. En caso de error, es necesario corregir los problemas de datos y, a continuación, se debe reiniciar todo el proceso de ingesta utilizando los archivos de datos corregidos.

Para ayudar a controlar el proceso de ingesta, [!DNL Experience Platform] permite suscribirse a un conjunto de eventos que se publican en cada paso del proceso y notificarle el estado de los datos introducidos y los posibles errores.

## Registro de un enlace web para notificaciones de ingesta de datos

Para recibir notificaciones de ingesta de datos, debe utilizar [Consola de Adobe Developer](https://www.adobe.com/go/devs_console_ui) para registrar un enlace web en la integración con su Experience Platform.

Siga el tutorial en [suscribirse a [!DNL Adobe I/O Event] notificaciones](../../observability/alerts/subscribe.md) para ver los pasos detallados sobre cómo hacerlo.

>[!IMPORTANT]
>
>Durante el proceso de suscripción, asegúrese de seleccionar **[!UICONTROL Notificaciones de la plataforma]** como proveedor de eventos y seleccione la variable **[!UICONTROL Notificación de ingesta de datos]** suscripción de evento cuando se le pida.

## Recibir notificaciones de ingesta de datos

Una vez que haya registrado correctamente su vínculo web y haya introducido nuevos datos, puede empezar a recibir notificaciones de eventos. Estos eventos se pueden ver mediante el propio vínculo web o seleccionando la variable **[!UICONTROL Seguimiento de depuración]** en la descripción general del registro de eventos de su proyecto en la consola de Adobe Developer.

El siguiente JSON es un ejemplo de una carga útil de notificación que se enviaría a su enlace web en caso de un evento de ingesta por lotes fallido:

```json
{
  "event_id": "93a5b11a-b0e6-4b29-ad82-81b1499cb4f2",
  "event": {
    "xdm:ingestionId": "01EGK8H8HF9JGFKNDCABHGA24G",
    "xdm:customerIngestionId": "01EGK8H8HF9JGFKNDCABHGA24G",
    "xdm:imsOrg": "{ORG_ID}",
    "xdm:completed": 1598374341560,
    "xdm:datasetId": "5e55b556c2ae4418a8446037",
    "xdm:eventCode": "ing_load_failure",
    "xdm:sandboxName": "prod",
    "sentTime": "1598374341595",
    "processStartTime": 1598374342614,
    "transformedTime": 1598374342621,
    "header": {
      "_adobeio": {
        "imsOrgId": "{ORG_ID}",
        "providerMetadata": "aep_observability_catalog_events",
        "eventCode": "platform_event"
      }
    }
  }
}
```

| Propiedad | Descripción |
| --- | --- |
| `event_id` | Un ID único generado por el sistema para la notificación. |
| `event` | Un objeto que contiene los detalles del evento que activó la notificación. |
| `event.xdm:datasetId` | ID del conjunto de datos al que se aplica el evento de ingesta. |
| `event.xdm:eventCode` | Código de estado que indica el tipo de evento que se activó para el conjunto de datos. Consulte la [apéndice](#event-codes) para valores específicos y sus definiciones. |

Para ver el esquema completo de las notificaciones de eventos, consulte la sección [repositorio público de GitHub](https://github.com/adobe/xdm/blob/master/schemas/notifications/ingestion.schema.json).

## Pasos siguientes

Una vez que se haya registrado [!DNL Platform] notificaciones al proyecto, puede ver los eventos recibidos del [!UICONTROL Información general del proyecto]. Consulte la guía de [seguimiento de eventos de Adobe I/O](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/support/tracing.md) para obtener instrucciones detalladas sobre cómo rastrear los eventos.

## Apéndice

La siguiente sección contiene información adicional sobre la interpretación de las cargas útiles de notificación de ingesta de datos.

### Eventos de notificación de estado disponibles {#event-codes}

En la tabla siguiente se enumeran las notificaciones de estado de ingesta de datos disponibles a las que puede suscribirse.

| Código de evento | Servicio de plataforma | Estado | Descripción del evento |
| --- | ---------------- | ------ | ----------------- |
| `ing_load_success` | [!DNL Data Ingestion] | success | Se ha introducido correctamente un lote en un conjunto de datos dentro de la variable [!DNL Data Lake]. |
| `ing_load_failure` | [!DNL Data Ingestion] | error | No se pudo ingerir un lote en un conjunto de datos dentro del [!DNL Data Lake]. |
| `ps_load_success` | [!DNL Real-Time Customer Profile] | success | Se ha introducido correctamente un lote en la variable [!DNL Profile] almacén de datos. |
| `ps_load_failure` | [!DNL Real-Time Customer Profile] | error | No se pudo ingerir un lote en la variable [!DNL Profile] almacén de datos. |
| `ig_load_success` | [!DNL Identity Service] | success | Los datos se cargaron correctamente en el gráfico de identidad. |
| `ig_load_failure` | [!DNL Identity Service] | error | No se pudieron cargar los datos en el gráfico de identidad. |

>[!NOTE]
>
>Solo se proporciona un tema de evento para todas las notificaciones de ingesta de datos. Para distinguir entre diferentes estados, se puede utilizar el código de evento.
