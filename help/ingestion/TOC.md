---
audience: user
user-guide-title: Ayuda de ingesta de datos de Adobe Experience Platform
breadcrumb-title: Guía de ingesta de datos
user-guide-description: Incluya sus datos en Experience Platform mediante la ingesta por lotes o de streaming.
feature: Data Ingestion
role: Developer
source-git-commit: f1d851afae5ad271e3c7d9d887f614058a262874
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 21%

---


# Ingesta de datos de Adobe Experience Platform {#ingestion}

- [Resumen de ingesta de datos](home.md)
- Ingesta por streaming {#streaming}
   - [Información general](streaming-ingestion/overview.md)
   - [Conector Kafka](streaming-ingestion/kafka.md)
   - [Resolución de problemas](streaming-ingestion/troubleshooting.md)
   - [INCLUSIÓN EN LA LISTA DE PERMITIDOS de direcciones IP](streaming-ingestion/allowlisting.md)
- Ingesta por lotes{#batch}
   - [Introducción a las API de ingesta por lotes](batch-ingestion/getting-started.md)
   - [Resumen de API](batch-ingestion/overview.md)
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
- [Protecciones para la ingesta de datos](guardrails.md)
- [Conectores de Source](source-connectors.md)
- [Referencia de API de ingesta por lotes](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/)
- [Referencia de API de ingesta de transmisión](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/)
- [Notas de la versión de Experience Platform](https://experienceleague.adobe.com/es/docs/experience-platform/release-notes/latest)
