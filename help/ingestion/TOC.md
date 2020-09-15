---
product: experience-platform
audience: user
user-guide-title: Ayuda de Adobe Experience Platform Data Ingestion
breadcrumb-title: Data Ingestion Guide
user-guide-description: Adobe Experience Platform brings data from multiple sources together in order to help marketers better understand the behavior of their customers. Adobe Experience Platform Data Ingestion represents the multiple methods by which Platform ingests data from these sources, as well as how that data is persisted within the Data Lake for use by downstream Platform services.
translation-type: tm+mt
source-git-commit: 2a5d6a9462950007d00f321ca9f3a3c457a3243e
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 7%

---


# Adobe Experience Platform Data Ingestion {#ingestion}

- [Información general sobre la inserción de datos](home.md)
- Transmisión por flujo continuo {#streaming}
   - [Información general](streaming-ingestion/overview.md)
   - [Conector Kafka](streaming-ingestion/kafka.md)
   - [Resolución de problemas](streaming-ingestion/troubleshooting.md)
- Ingesta por lotes{#batch}
   - [Información general](batch-ingestion/overview.md)
   - [API de ingestión por lotes](batch-ingestion/api-overview.md)
   - [Ingestión parcial por lotes](batch-ingestion/partial.md)
   - [Resolución de problemas](batch-ingestion/troubleshooting.md)
- Tutoriales {#tutorials}
   - [Asignación de un archivo CSV a XDM](tutorials/map-a-csv-file.md)
   - [Ingesta de datos de lote mediante la interfaz de usuario](tutorials/ingest-batch-data.md)
   - [Creación de una conexión de flujo autenticada](tutorials/create-authenticated-streaming-connection.md)
   - [Creación de una conexión de flujo continuo (API)](tutorials/create-streaming-connection.md)
   - [Creación de una conexión de flujo continuo (IU)](tutorials/create-streaming-connection-ui.md)
   - [Transmisión de datos de registros](tutorials/streaming-record-data.md)
   - [Transmisión de datos de series temporales](tutorials/streaming-time-series-data.md)
   - [Transmisión de varios mensajes](tutorials/streaming-multiple-messages.md)
- Calidad y control de la ingestión de datos{#quality}
   - [Información general](quality/overview.md)
   - [Monitorear flujos de datos](quality/monitor-data-flows.md)
   - [Recuperar diagnósticos de error](quality/error-diagnostics.md)
   - [Recuperar lotes con errores](quality/retrieve-failed-batches.md)
   - [Validación de la ingesta de flujo continuo](quality/streaming-validation.md)
   - [Suscripción a eventos de ingesta de datos](quality/subscribe-events.md)
- [Conectores de origen](source-connectors.md)
- [Referencia de API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)
- [Notas de la versión de la plataforma](https://www.adobe.com/go/platform-release-notes-en)