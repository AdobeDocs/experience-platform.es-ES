---
audience: user
user-guide-title: Ayuda del servicio de Consulta de Adobe Experience Platform
breadcrumb-title: Guía del servicio de consultas
user-guide-description: Utilice SQL estándar para consultar los datos dentro del lago de datos en Experience Platform.
feature: Queries
role: User,Developer
source-git-commit: 20869e76976ff3868f1d4dbc7c6d97b58682e5c3
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 21%

---


# Adobe Experience Platform Query Service {#query}

- [Introducción al servicio de consultas](home.md)
- [Empaquetado del servicio de consultas](packaging.md)
- [Protecciones del servicio de consultas](guardrails.md)
- Introducción {#get-started}
   - [Requisitos previos](get-started/prerequisites.md)
- Data Distiller {#data-distiller}
   - [Información general](data-distiller/overview.md)
   - [Uso de licencias](data-distiller/license-usage.md)
   - Conjuntos de datos derivados {#derived-datasets}
      - [Información general](data-distiller/derived-datasets/overview.md)
      - [Crear conjuntos de datos derivados con SQL](data-distiller/derived-datasets/create-derived-datasets-with-sql.md)
      - [Crear conjuntos de datos derivados basados en deciles](data-distiller/derived-datasets/decile-based-derived-attributes.md)
   - SQL Insights para el sistema de informes ampliado de la aplicación {#sql-insights}
      - [Información general](data-distiller/sql-insights/overview.md)
      - [Modo de consulta profesional](data-distiller/sql-insights/query-pro-mode.md)
      - [Envío de consultas aceleradas](data-distiller/sql-insights/send-accelerated-queries.md)
      - [Guía del modelo de datos de Reporting Insights](data-distiller/sql-insights/reporting-insights-data-model.md)
   - Canalizaciones de características de AI/ML {#ml-feature-pipelines}
      - [Información general](data-distiller/ml-feature-pipelines/overview.md)
      - [Conectar con Jupyter Notebooks](data-distiller/ml-feature-pipelines/establish-connection.md)
      - [Análisis exploratorio de datos](data-distiller/ml-feature-pipelines/exploratory-analysis.md)
      - [Funciones de ingeniero para ML](data-distiller/ml-feature-pipelines/feature-engineering.md)
      - [Exportación de datos a entornos XML](data-distiller/ml-feature-pipelines/export-data.md)
      - [Flujo de trabajo completo de enriquecimiento de la canalización de datos AI/ML](data-distiller/ml-feature-pipelines/end-to-end-notebook-workflow.md)
- Estadísticas de Data Distiller y aprendizaje automático {#advanced-statistics}
   - [Información general](advanced-statistics/overview.md)
   - [Ingeniería de funciones](advanced-statistics/feature-engineering.md)
   - [Modelos](advanced-statistics/models.md)
   - [Transformación de características](advanced-statistics/feature-transformation.md)
Implementar modelos {#implement-models}
      - [Implementación de modelos](advanced-statistics/implement-models/implement-models.md)
      - [Regresión](advanced-statistics/implement-models/regression.md)
      - [Clasificación](advanced-statistics/implement-models/classification.md)
      - [Clúster](advanced-statistics/implement-models/clustering.md)
Ejemplos {#examples}
      - [Filtrado de bots mediante estadísticas y aprendizaje automático](advanced-statistics/examples/statistics-and-ml-bot-filtering.md)
      - [Predecir la pérdida de clientes mediante una regresión logística basada en SQL](advanced-statistics/examples/predict-customer-churn.md)
- Audiencias de Data Distiller {#data-distiller-audiences}
   - [Creación de audiencias externas con SQL](data-distiller-audiences/overview.md)
- Ejemplos {#use-cases}
   - [Información general](use-cases/overview.md)
   - [Exploración abandonada](use-cases/abandoned-browse.md)
   - [Análisis de atribución](use-cases/attribution-analysis.md)
   - [Filtrado de bots](use-cases/bot-filtering.md)
   - [Filtrado de bots mediante estadísticas e introducción al aprendizaje automático](use-cases/statistics-and-ml-bot-filtering-stub.md)
   - [Creación de un informe de tendencias de eventos](use-cases/trended-report-of-events.md)
   - [Análisis de consentimiento](use-cases/consent-analysis.md)
   - [Valor de tiempo de vida del cliente](use-cases/customer-lifetime-value.md)
   - [Exploración de datos](./use-cases/data-exploration.md)
   - [Conjuntos de datos derivados basados en deciles](use-cases/deciles-use-case.md)
   - [Coincidencia aproximada](use-cases/fuzzy-match.md)
   - [Enumeración de las vistas de página de un usuario](use-cases/list-visitor-sessions.md)
   - [Enumerar visitantes por sus vistas de página](use-cases/visitors-by-number-of-page-views.md)
   - [Predecir la pérdida de clientes mediante SQL](use-cases/predict-customer-churn-stub.md)
   - [Puntuación de tendencia](use-cases/propensity-score.md)
   - [Recuperar registros similares con funciones de orden superior](use-cases/retrieve-similar-records.md)
   - [Devolver y usar variables de comercialización de datos de Analytics](use-cases/merchandising-variables.md)
   - [SQLAlchemy](use-cases/sqlalchemy.md)
   - [Ver el informe de resumen de un visitante](use-cases/roll-up-report-of-a-visitor.md)
   - [Perspectivas de análisis web y móvil](use-cases/analytics-insights.md)
- Conceptos clave {#key-concepts}
   - [Uso de estructuras de datos anidadas](key-concepts/nested-data-structures.md)
   - [Acoplar estructuras de datos anidadas](key-concepts/flatten-nested-data.md)
   - [Bloque anónimo](key-concepts/anonymous-block.md)
   - [Plantilla en línea](key-concepts/inline-templates.md)
   - [Carga incremental](key-concepts/incremental-load.md)
   - [Deduplicación de datos](key-concepts/deduplication.md)
   - [Ejemplos de conjuntos de datos](key-concepts/dataset-samples.md)
   - [Cálculo de estadísticas de conjuntos de datos](key-concepts/dataset-statistics.md)
- Hipercubos de Data Distiller {#hypercubes}
   - [Análisis eficiente de big data con hipercubos](hypercubes/overview.md)
- Conectar clientes al servicio de consultas {#clients}
   - [Información general sobre conexiones de cliente](clients/overview.md)
   - [Modos SSL](./clients/ssl-modes.md)
   - [Aqua Data Studio](clients/aqua-data-studio.md)
   - [DbVisualizer](./clients/dbvisulaizer.md)
   - [Copiloto de GitHub](./clients/github-copilot.md)
   - [Jupyter Notebook](clients//jupyter-notebook.md)
   - [Buscador](clients/looker.md)
   - [Póstico](clients/postico.md)
   - [Power BI](clients/power-bi.md)
   - [PSQL](clients/psql.md)
   - [RStudio](clients/rstudio.md)
   - [Tableau](clients/tableau.md)
- IU del servicio de consultas {#ui}
   - [Información general de IU](ui/overview.md)
   - [Guía del usuario del Editor de consultas](ui/user-guide.md)
   - [Plantillas de consulta](ui/query-templates.md)
   - [Consultas parametrizadas](ui/parameterized-queries.md)
   - [Programaciones de consultas](ui/query-schedules.md)
   - [Registros de consultas](ui/query-logs.md)
   - [Monitorización de consultas programadas](ui/monitor-queries.md)
   - [Guía de credenciales](ui/credentials.md)
   - [Generar conjuntos de datos de salida a partir de resultados de consulta](ui/create-datasets.md)
- API de servicio de consultas {#api}
   - [Introducción](api/getting-started.md)
   - [Consultas](api/queries.md)
   - [Parámetros de conexión](api/connection-parameters.md)
   - [Programaciones](api/scheduled-queries.md)
   - [Ejecuta para consultas programadas](api/runs-scheduled-queries.md)
   - [Plantillas de consulta](api/query-templates.md)
   - [Consultas aceleradas](api/accelerated-queries.md)
   - [Suscripciones de alerta](api/alert-subscriptions.md)
- API de autorización de Data Distiller {#auth-api}
   - [Información general](auth-api/overview.md)
   - [Primeros pasos](auth-api/getting-started.md)
   - [Acceso IP](auth-api/ip-access.md)
   - [Validación](auth-api/validate.md)
- Gobernanza de datos {#data-governance}
   - [Información general](data-governance/overview.md)
   - [Guía de registro de auditoría](data-governance/audit-log-guide.md)
   - [Identidades en conjuntos de datos de esquema ad hoc](data-governance/ad-hoc-schema-identities.md)
   - [Compatibilidad de control de acceso basado en atributos para esquemas ad hoc](./data-governance/ad-hoc-schema-labels.md)
- Prácticas recomendadas {#best-practices}
   - [Ejecución de consulta](best-practices/writing-queries.md)
   - [Organización de recursos de datos](./best-practices/organize-data-assets.md)
- Referencia SQL {#sql}
   - [Resumen de SQL](sql/overview.md)
   - [Sintaxis SQL](sql/syntax.md)
   - [Funciones definidas por el Adobe](sql/adobe-defined-functions.md)
   - [Funciones de orden superior](sql/higher-order-functions.md)
   - [Funciones SQL de Spark](sql/spark-sql-functions.md)
   - [Comandos de metadatos](sql/metadata.md)
   - [Instrucciones preparadas](sql/prepared-statements.md)
- [Preguntas frecuentes](troubleshooting-guide.md)
- [LISTA DE PERMITIDOS de direcciones IP](ip-address-allowlist.md)
- [Referencia de API](https://www.adobe.io/experience-platform-apis/references/query-service/)
- [Notas de la versión de Platform](https://experienceleague.adobe.com/es/docs/experience-platform/release-notes/latest)
