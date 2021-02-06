---
keywords: Experience Platform;inicio;temas populares;notificaciones de ingestión de datos;notificaciones;eventos de suscripción;eventos de estado de ingestión de datos;eventos de estado;suscripción;notificaciones de estado;
solution: Experience Platform
title: Notificaciones de inserción de datos
topic: overview
description: Para ayudar a supervisar el proceso de ingestión, Adobe Experience Platform permite suscribirse a un conjunto de eventos que se publican en cada paso del proceso, notificándole el estado de los datos ingestados y los posibles fallos.
translation-type: tm+mt
source-git-commit: 089a4d517476b614521d1db4718966e3ebb13064
workflow-type: tm+mt
source-wordcount: '681'
ht-degree: 1%

---


# Notificaciones de ingestión de datos

El proceso de ingesta de datos en Adobe Experience Platform consta de varios pasos. Una vez que identifique los archivos de datos que deben ingerirse en [!DNL Platform], se iniciará el proceso de ingestión y cada paso se producirá de forma consecutiva hasta que los datos se ingieran correctamente o se produzcan errores. El proceso de ingestión se puede iniciar mediante la [API de inserción de datos de Adobe Experience Platform](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) o mediante la interfaz de usuario [!DNL Experience Platform].

Los datos cargados en [!DNL Platform] deben pasar por varios pasos para alcanzar su destino, el [!DNL Data Lake] o el [!DNL Real-time Customer Profile] almacén de datos. Cada paso implica el procesamiento de los datos, la validación de los datos y, a continuación, el almacenamiento de los datos antes de pasarlos al siguiente paso. Dependiendo de la cantidad de datos que se ingesten, este proceso puede llevar mucho tiempo y siempre hay una posibilidad de que el proceso falle debido a errores de validación, semántica o procesamiento. En el evento de un error, los problemas de datos deben corregirse y, a continuación, se debe reiniciar todo el proceso de ingestión utilizando los archivos de datos corregidos.

Para ayudar a monitorear el proceso de ingestión, [!DNL Experience Platform] permite suscribirse a un conjunto de eventos que se publican en cada paso del proceso, notificándole el estado de los datos ingestados y posibles fallos.

## Registro de un enlace web para notificaciones de ingesta de datos

Para recibir las notificaciones de ingestión de datos, debe utilizar [Consola de desarrollador de Adobe](https://www.adobe.com/go/devs_console_ui) para registrar un enlace web en la integración de Experience Platform.

Siga el tutorial sobre [suscripción a [!DNL Adobe I/O Event] notificaciones](../../observability/notifications/subscribe.md) para ver los pasos detallados sobre cómo realizar esto.

>[!IMPORTANT]
>
>Durante el proceso de suscripción, asegúrese de seleccionar **[!UICONTROL Notificaciones de plataforma]** como proveedor de evento y, cuando se le solicite, seleccione la suscripción de evento **[!UICONTROL Notificación de ingestión de datos]**.

## Recibir notificaciones de inserción de datos

Una vez que haya registrado correctamente su enlace web y que se hayan ingerido nuevos datos, puede recibir inicios para recibir notificaciones de evento. Estos eventos se pueden ver mediante el propio webgancho o seleccionando la ficha **[!UICONTROL Seguimiento de depuración]** en la descripción general del registro de evento del proyecto en Adobe Developer Console.

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

Para vista del esquema completo de las notificaciones de evento, consulte el [repositorio público de GitHub](https://github.com/adobe/xdm/blob/master/schemas/notifications/ingestion.schema.json).

## Pasos siguientes

Una vez que haya registrado [!DNL Platform] las notificaciones al proyecto, puede realizar la vista de eventos recibidos desde la [!UICONTROL información general del proyecto]. Consulte la guía sobre [rastreo de Eventos de Adobe I/O](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/support/tracing.md) para obtener instrucciones detalladas sobre cómo rastrear sus eventos.

## Apéndice

La siguiente sección contiene información adicional sobre la interpretación de las cargas de notificación de ingesta de datos.

### Eventos de notificación de estado disponibles {#event-codes}

La siguiente tabla lista las notificaciones de estado de ingesta de datos disponibles a las que puede suscribirse.

| Código de evento | Servicio de plataforma | Estado | Descripción del evento |
| --- | ---------------- | ------ | ----------------- |
| `ing_load_success` | [!DNL Data Ingestion] | success | Un lote se ingerió correctamente en un conjunto de datos dentro de [!DNL Data Lake]. |
| `ing_load_failure` | [!DNL Data Ingestion] | error | No se pudo ingerir un lote en un conjunto de datos dentro de [!DNL Data Lake]. |
| `ps_load_success` | [!DNL Real-time Customer Profile] | success | Un lote se ingerió correctamente en el almacén de datos [!DNL Profile]. |
| `ps_load_failure` | [!DNL Real-time Customer Profile] | error | No se pudo ingerir un lote en el almacén de datos [!DNL Profile]. |
| `ig_load_success` | [!DNL Identity Service] | success | Los datos se cargaron correctamente en el gráfico de identidad. |
| `ig_load_failure` | [!DNL Identity Service] | error | No se pudieron cargar los datos en el gráfico de identidad. |

>[!NOTE]
>
>Solo se proporciona un tema de evento para todas las notificaciones de ingesta de datos. Para distinguir entre distintos estados, se puede utilizar el código de evento.