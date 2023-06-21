---
audience: user
user-guide-title: Ayuda del servicio de Consulta de Adobe Experience Platform
breadcrumb-title: Guía del servicio de consultas
user-guide-description: Utilice SQL estándar para consultar los datos dentro del lago de datos en Experience Platform.
feature: Queries
source-git-commit: a0f826a2e5fcdfc2f9e08221f30ba01470c9b3be
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 18%

---


# Adobe Experience Platform Query Service {#query}

- [Introducción al servicio de consultas](home.md)
- [Empaquetado del servicio de consultas](packages.md)
- [Protecciones del servicio de consultas](guardrails.md)
- Introducción {#get-started}
   - [Requisitos previos](get-started/prerequisites.md)
- Data Distiller {#data-distiller}
   - [Información general](data-distiller/overview.md)
   - [Uso de licencias](data-distiller/license-usage.md)
   - Almacén acelerado de consultas {#query-accelerated-store}
      - [Envío de consultas aceleradas](data-distiller/query-accelerated-store/send-accelerated-queries.md)
      - [Guía del modelo de datos de Reporting Insights](data-distiller/query-accelerated-store/reporting-insights-data-model.md)
   - Atributos derivados {#derived-attributes}
      - [Información general](data-distiller/derived-attributes/overview.md)
      - [Flujo SQL fluido](data-distiller/derived-attributes/seamless-sql-flow.md)
      - [Crear atributos derivados basados en deciles](data-distiller/derived-attributes/decile-based-derived-attributes.md)
- Casos de uso {#use-cases}
   - [Exploración abandonada](use-cases/abandoned-browse.md)
   - [Análisis de atribución](use-cases/attribution-analysis.md)
   - [Filtrado de bots](use-cases/bot-filtering.md)
   - [Creación de un informe de tendencias de eventos](use-cases/trended-report-of-events.md)
   - [Valor de duración del cliente](use-cases/customer-lifetime-value.md)
   - [Atributos derivados basados en deciles](use-cases/deciles-use-case.md)
   - [Coincidencia aproximada](use-cases/fuzzy-match.md)
   - [Enumeración de las vistas de página de un usuario](use-cases/list-visitor-sessions.md)
   - [Enumerar visitantes por sus vistas de página](use-cases/visitors-by-number-of-page-views.md)
   - [Puntuación de tendencia](use-cases/propensity-score.md)
   - [SQLAlchemy](use-cases/sqlalchemy.md)
   - [Devolver y usar variables de comercialización de datos de Analytics](use-cases/merchandising-variables.md)
   - [Ver el informe de resumen de un visitante](use-cases/roll-up-report-of-a-visitor.md)
   - [Perspectivas de análisis web y móvil](use-cases/analytics-insights.md)
- Conectar clientes al servicio de consultas {#clients}
   - [Información general sobre conexiones de cliente](clients/overview.md)
   - [Modos SSL](./clients/ssl-modes.md)
   - [Aqua Data Studio](clients/aqua-data-studio.md)
   - [DbVisualizer](./clients/dbvisulaizer.md)
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
   - [Consultas parametrizadas (limitadas)](ui/parameterized-queries.md)
   - [Programaciones de consultas](ui/query-schedules.md)
   - [Registros de consultas](ui/query-logs.md)
   - [Monitorización de consultas programadas](ui/monitor-queries.md)
   - [Guía de credenciales](ui/credentials.md)
   - [Generar conjuntos de datos de salida a partir de resultados de consulta](ui/create-datasets.md)
- Extremos de API del servicio de consultas {#api}
   - [Primeros pasos](api/getting-started.md)
   - [Consultas](api/queries.md)
   - [Parámetros de conexión](api/connection-parameters.md)
   - [Horarios](api/scheduled-queries.md)
   - [Ejecuta para consultas programadas](api/runs-scheduled-queries.md)
   - [Plantillas de consulta](api/query-templates.md)
   - [Consultas aceleradas](api/accelerated-queries.md)
   - [Suscripciones de alerta](api/alert-subscriptions.md)
- Control de datos {#data-governance}
   - [Información general](data-governance/overview.md)
   - [Guía de registro de auditoría](data-governance/audit-log-guide.md)
   - [Identidades en conjuntos de datos de esquema ad hoc](data-governance/ad-hoc-schema-identities.md)
   - [Compatibilidad de control de acceso basado en atributos para esquemas ad hoc](./data-governance/ad-hoc-schema-labels.md)
- Prácticas recomendadas {#best-practices}
   - [Ejecución de consulta](best-practices/writing-queries.md)
   - [Organización de recursos de datos](./best-practices/organize-data-assets.md)
- Conceptos esenciales {#essential-concepts}
   - [Uso de estructuras de datos anidadas](essential-concepts/nested-data-structures.md)
   - [Acoplar estructuras de datos anidadas](essential-concepts/flatten-nested-data.md)
   - [Bloque anónimo](essential-concepts/anonymous-block.md)
   - [Carga incremental](essential-concepts/incremental-load.md)
   - [Deduplicación de datos](essential-concepts/deduplication.md)
   - [Ejemplos de conjuntos de datos](essential-concepts/dataset-samples.md)
   - [Cálculo de estadísticas de conjuntos de datos](essential-concepts/dataset-statistics.md)
- Referencia SQL {#sql}
   - [Resumen de SQL](sql/overview.md)
   - [Sintaxis SQL](sql/syntax.md)
   - [Funciones definidas por el Adobe](sql/adobe-defined-functions.md)
   - [Funciones SQL de Spark](sql/spark-sql-functions.md)
   - [Comandos de metadatos](sql/metadata.md)
   - [Instrucciones preparadas](sql/prepared-statements.md)
- [Preguntas frecuentes](troubleshooting-guide.md)
- [Referencia de API](https://www.adobe.io/experience-platform-apis/references/query-service/)
- [Notas de la versión de Platform](https://experienceleague.adobe.com/docs/experience-platform/release-notes/latest.html?lang=es)
