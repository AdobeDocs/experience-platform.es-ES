---
keywords: Experience Platform;inicio;temas populares;ingesta de datos;notificaciones;eventos de suscripción;eventos de estado de ingesta de datos;eventos de estado;suscribirse;notificaciones de estado;
solution: Experience Platform
title: Notificaciones de ingesta de datos
description: Para ayudar a monitorizar el proceso de ingesta, Adobe Experience Platform permite suscribirse a un conjunto de eventos que se publican en cada paso del proceso, notificándole el estado de los datos introducidos y cualquier posible error.
exl-id: fd34e1ab-f6f6-44f0-88ee-7020e9322c39
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 1%

---

# Notificaciones de ingesta de datos

El proceso de ingesta de datos en Adobe Experience Platform consta de varios pasos. Una vez que identifique los archivos de datos que deben ingerirse en [!DNL Experience Platform], el proceso de ingesta comienza y cada paso ocurre consecutivamente hasta que los datos se incorporan correctamente o fallan. El proceso de ingesta se puede iniciar mediante la [API de ingesta por lotes de Adobe Experience Platform](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/) o mediante la interfaz de usuario [!DNL Experience Platform].

Los datos cargados en [!DNL Experience Platform] deben pasar por varios pasos para llegar a su destino, el almacén de datos [!DNL Data Lake] o [!DNL Real-Time Customer Profile]. Cada paso implica procesar los datos, validarlos y, a continuación, almacenarlos antes de pasarlos al siguiente paso. Según la cantidad de datos que se esté introduciendo, este puede convertirse en un proceso laborioso y siempre existe la posibilidad de que el proceso falle debido a errores de validación, semántica o procesamiento. En caso de error, es necesario corregir los problemas de datos y, a continuación, reiniciar todo el proceso de ingesta con los archivos de datos corregidos.

Para ayudar a supervisar el proceso de ingesta, [!DNL Experience Platform] permite suscribirse a un conjunto de eventos que se publican en cada paso del proceso, notificándole el estado de los datos ingeridos y los posibles errores.

## Registrar un webhook para notificaciones de ingesta de datos

Para recibir notificaciones de ingesta de datos, debes usar [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) para registrar un webhook en tu integración con Experience Platform.

Siga el tutorial de [suscripción a [!DNL Adobe I/O Event] notificaciones](../../observability/alerts/subscribe.md) para ver los pasos detallados sobre cómo hacerlo.

>[!IMPORTANT]
>
>Durante el proceso de suscripción, asegúrese de seleccionar **[!UICONTROL Notificaciones de plataforma]** como proveedor de eventos y, cuando se le solicite, seleccione la suscripción al evento **[!UICONTROL Notificación de ingesta de datos]**.

## Recibir notificaciones de ingesta de datos

Una vez que haya registrado correctamente su webhook y se hayan introducido nuevos datos, puede empezar a recibir notificaciones de eventos. Estos eventos se pueden ver usando el propio webhook o seleccionando la pestaña **[!UICONTROL Debug Tracing]** en la descripción general del registro de eventos de su proyecto en Adobe Developer Console.

El siguiente JSON es un ejemplo de una carga útil de notificación que se enviaría a su webhook en caso de que se produzca un evento de ingesta por lotes fallido:

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
| `event_id` | ID único y generado por el sistema para la notificación. |
| `event` | Un objeto que contiene los detalles del evento que activó la notificación. |
| `event.xdm:datasetId` | El ID del conjunto de datos al que se aplica el evento de ingesta. |
| `event.xdm:eventCode` | Un código de estado que indica el tipo de evento activado para el conjunto de datos. Consulte el [apéndice](#event-codes) para ver valores específicos y sus definiciones. |

Para ver el esquema completo de las notificaciones de eventos, consulte el [repositorio público de GitHub](https://github.com/adobe/xdm/blob/master/schemas/notifications/ingestion.schema.json).

## Pasos siguientes

Una vez que haya registrado [!DNL Experience Platform] notificaciones en su proyecto, podrá ver los eventos recibidos desde la [!UICONTROL Descripción general del proyecto]. Consulte la guía de [seguimiento de Adobe I/O Events](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/support/tracing.md) para obtener instrucciones detalladas sobre cómo rastrear los eventos.

## Apéndice

La siguiente sección contiene información adicional sobre la interpretación de las cargas útiles de notificación de ingesta de datos.

### Eventos de notificación de estado disponibles {#event-codes}

En la tabla siguiente se enumeran las notificaciones de estado de ingesta de datos disponibles a las que puede suscribirse.

| Código de evento | Servicio de Experience Platform | Estado | Descripción del evento |
| --- | ---------------- | ------ | ----------------- |
| `ing_load_success` | [!DNL Data Ingestion] | success | Se ha ingerido correctamente un lote en un conjunto de datos dentro de [!DNL Data Lake]. |
| `ing_load_failure` | [!DNL Data Ingestion] | fracaso | No se pudo ingerir un lote en un conjunto de datos dentro de [!DNL Data Lake]. |
| `ps_load_success` | [!DNL Real-Time Customer Profile] | success | Se ha ingerido correctamente un lote en el almacén de datos [!DNL Profile]. |
| `ps_load_failure` | [!DNL Real-Time Customer Profile] | fracaso | No se pudo ingerir un lote en el almacén de datos [!DNL Profile]. |
| `ig_load_success` | [!DNL Identity Service] | success | Los datos se cargaron correctamente en el gráfico de identidad. |
| `ig_load_failure` | [!DNL Identity Service] | fracaso | No se han podido cargar los datos en el gráfico de identidad. |

>[!NOTE]
>
>Solo se proporciona un tema de evento para todas las notificaciones de ingesta de datos. Para distinguir entre diferentes estados, se puede utilizar el código de evento.
