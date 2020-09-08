---
keywords: Experience Platform;home;popular topics;data ingestion notifications;notifications;subscribe events;data ingestion status events;status events;subscribe;status notifications;
solution: Experience Platform
title: Suscripción a eventos de ingesta de datos
topic: overview
translation-type: tm+mt
source-git-commit: 80a1694f11cd2f38347989731ab7c56c2c198090
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 1%

---


# Notificaciones de ingestión de datos

El proceso de ingesta de datos en Adobe Experience Platform consta de varios pasos. Una vez que se identifican los archivos de datos que se deben ingerir en [!DNL Platform], se inicia el proceso de ingestión y cada paso se produce de forma consecutiva hasta que los datos se ingieren correctamente o se producen errores. El proceso de ingestión se puede iniciar mediante la API [de ingestión de datos de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) Adobe Experience Platform o mediante la interfaz de [!DNL Experience Platform] usuario.

Los datos cargados en [!DNL Platform] deben seguir varios pasos para llegar a su destino, al [!DNL Data Lake] o al almacén de datos [!DNL Real-time Customer Profile] . Cada paso implica el procesamiento de los datos, la validación de los datos y, a continuación, el almacenamiento de los datos antes de pasarlos al siguiente paso. Dependiendo de la cantidad de datos que se ingesten, este proceso puede llevar mucho tiempo y siempre hay una posibilidad de que el proceso falle debido a errores de validación, semántica o procesamiento. En el evento de un error, los problemas de datos deben corregirse y, a continuación, se debe reiniciar todo el proceso de ingestión utilizando los archivos de datos corregidos.

Para ayudar a supervisar el proceso de ingestión, [!DNL Experience Platform] permite suscribirse a un conjunto de eventos que se publican en cada paso del proceso, notificándole el estado de los datos ingestados y los posibles fallos.

## Registro de un enlace web para notificaciones de ingesta de datos

Para recibir las notificaciones de ingestión de datos, debe utilizar [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) para registrar un enlace web en la integración de Experience Platform.

Siga el tutorial sobre la [suscripción de [!DNL Adobe I/O Event] notificaciones](../../observability/notifications/subscribe.md) para ver los pasos detallados sobre cómo hacerlo.

>[!IMPORTANT]
>
>Durante el proceso de suscripción, asegúrese de seleccionar las notificaciones **[!UICONTROL de]** plataforma como proveedor de evento y, cuando se le solicite, seleccione la suscripción de evento de notificaciones **[!UICONTROL de ingesta de]** datos.

## Recibir notificaciones de inserción de datos

Una vez que haya registrado correctamente su enlace web y que se hayan ingerido nuevos datos, puede recibir inicios para recibir notificaciones de evento. Estos eventos se pueden ver mediante el propio webgancho o seleccionando la ficha **[!UICONTROL Seguimiento]** de depuración en la descripción general del registro de evento del proyecto en la consola de desarrollador de Adobe.

El siguiente JSON es un ejemplo de una carga útil de notificación que se enviaría a su enlace web en caso de un evento de ingestión por lotes fallido:

```json
{
  "event_id": "93a5b11a-b0e6-4b29-ad82-81b1499cb4f2",
  "event": {
    "xdm:ingestionId": "01EGK8H8HF9JGFKNDCABHGA24G",
    "xdm:customerIngestionId": "01EGK8H8HF9JGFKNDCABHGA24G",
    "xdm:imsOrg": "{IMS_ORG}",
    "xdm:completed": 1598374341560,
    "xdm:datasetId": "5e55b556c2ae4418a8446037",
    "xdm:eventCode": "ing_load_failure",
    "xdm:sandboxName": "prod",
    "sentTime": "1598374341595",
    "processStartTime": 1598374342614,
    "transformedTime": 1598374342621,
    "header": {
      "_adobeio": {
        "imsOrgId": "{IMS_ORG}",
        "providerMetadata": "aep_observability_catalog_events",
        "eventCode": "platform_event"
      }
    }
  }
}
```

| Propiedad | Descripción |
| --- | --- |
| `event_id` | ID única generada por el sistema para la notificación. |
| `event` | Objeto que contiene los detalles del evento que activó la notificación. |
| `event.xdm:datasetId` | ID del conjunto de datos al que se aplica el evento de ingestión. |
| `event.xdm:eventCode` | Código de estado que indica el tipo de evento que se activó para el conjunto de datos. Consulte el [apéndice](#event-codes) para conocer los valores específicos y sus definiciones. |

Para vista del esquema completo de las notificaciones de evento, consulte el repositorio [](https://github.com/adobe/xdm/blob/master/schemas/notifications/ingestion.schema.json)público de GitHub.

## Pasos siguientes

Una vez que haya registrado [!DNL Platform] las notificaciones al proyecto, puede realizar la vista de eventos recibidos desde la información general [!UICONTROL del]proyecto. Consulte la guía sobre [rastreo de Eventos](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/support/tracing.md) de E/S de Adobe para obtener instrucciones detalladas sobre cómo rastrear sus eventos.

## Apéndice

La siguiente sección contiene información adicional sobre la interpretación de las cargas de notificación de ingesta de datos.

### Eventos de notificación de estado disponibles {#event-codes}

La siguiente tabla lista las notificaciones de estado de ingesta de datos disponibles a las que puede suscribirse.

| Código de evento | Servicio de plataforma | Estado | Descripción del evento |
| --- | ---------------- | ------ | ----------------- |
| `ing_load_success` | [!DNL Data Ingestion] | success | Un lote se ingerió correctamente en un conjunto de datos dentro del [!DNL Data Lake]. |
| `ing_load_failure` | [!DNL Data Ingestion] | error | No se pudo ingerir un lote en un conjunto de datos dentro del [!DNL Data Lake]. |
| `ps_load_success` | [!DNL Real-time Customer Profile] | success | Un lote se ha ingerido correctamente en el almacén [!DNL Profile] de datos. |
| `ps_load_failure` | [!DNL Real-time Customer Profile] | error | No se pudo ingerir un lote en el almacén [!DNL Profile] de datos. |
| `ig_load_success` | [!DNL Identity Service] | success | Los datos se cargaron correctamente en el gráfico de identidad. |
| `ig_load_failure` | [!DNL Identity Service] | error | No se pudieron cargar los datos en el gráfico de identidad. |

>[!NOTE]
>
>Solo se proporciona un tema de evento para todas las notificaciones de ingesta de datos. Para distinguir entre distintos estados, se puede utilizar el código de evento.