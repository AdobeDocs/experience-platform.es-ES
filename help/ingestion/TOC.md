---
audience: user
user-guide-title: Ayuda de ingesta de datos de Adobe Experience Platform
breadcrumb-title: Guía de ingesta de datos
user-guide-description: Incluya sus datos en Experience Platform mediante la ingestión por lotes o streaming.
feature: Data Ingestion
source-git-commit: f77bbc60f2bc1f12970e8050ec6a924b9713f303
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 29%

---


# Ingesta de datos de Adobe Experience Platform {#ingestion}

- [Resumen de ingesta de datos](home.md)
- Ingesta de streaming {#streaming}
   - [Información general](streaming-ingestion/overview.md)
   - [Conector Kafka](streaming-ingestion/kafka.md)
   - [Resolución de problemas](streaming-ingestion/troubleshooting.md)
- Ingesta por lotes{#batch}
   - [Introducción a las API de ingesta por lotes](batch-ingestion/getting-started.md)
   - [Información general de API](batch-ingestion/overview.md)
   - [Guía para desarrolladores de API](batch-ingestion/api-overview.md)
   - [Ingesta parcial por lotes](batch-ingestion/partial.md)
   - [Resolución de problemas](batch-ingestion/troubleshooting.md)
- Tutoriales {#tutorials}
   - Asignación de un archivo CSV a XDM {#map-csv}
      - [Información general](./tutorials/map-csv/overview.md)
      - [Asignación de un archivo CSV a un esquema existente](./tutorials/map-csv/existing-schema.md)
      - [Asignación de un archivo CSV mediante recomendaciones generadas por IA](./tutorials/map-csv/recommendations.md)
   - [Ingesta de datos por lotes mediante la IU](tutorials/ingest-batch-data.md)
   - [Creación de una conexión de flujo continuo autenticada](tutorials/create-authenticated-streaming-connection.md)
   - [Creación de una conexión de flujo continuo (API)](tutorials/create-streaming-connection.md)
   - [Creación de una conexión de flujo continuo (IU)](tutorials/create-streaming-connection-ui.md)
   - [Transmisión de datos de registro](tutorials/streaming-record-data.md)
   - [Datos de series temporales de streaming](tutorials/streaming-time-series-data.md)
   - [Transmisión de varios mensajes](tutorials/streaming-multiple-messages.md)
- Calidad de los datos y monitorización{#quality}
   - [Información general](quality/overview.md)
   - [Monitorización de la ingesta de datos](quality/monitor-data-ingestion.md)
   - [Recuperar diagnósticos de error](quality/error-diagnostics.md)
   - [Recuperar lotes fallidos](quality/retrieve-failed-batches.md)
   - [Validación de ingesta de streaming](quality/streaming-validation.md)
   - [Notificaciones de ingesta de datos](quality/subscribe-events.md)
- [Protecciones para la ingesta de datos](guardrails.md)
- [Conectores de origen](source-connectors.md)
- [Referencia de API](https://www.adobe.io/experience-platform-apis/references/data-ingestion/)
- [Notas de la versión de Platform](https://experienceleague.adobe.com/docs/experience-platform/release-notes/latest.html?lang=es)
