---
audience: user
user-guide-title: Ayuda del servicio de Consulta de Adobe Experience Platform
breadcrumb-title: Guía del servicio de consultas
user-guide-description: Utilice SQL estándar para consultar los datos dentro del lago de datos en Experience Platform.
feature: Queries
source-git-commit: 3d549b14571be7ec3455da0e23181951cb991a9d
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 16%

---


# Servicio de consultas de Adobe Experience Platform {#query}

- [Información general del servicio de consultas](home.md)
- [Paquete de servicio de consulta](packages.md)
- [Protecciones del servicio de consultas](guardrails.md)
- Introducción {#get-started}
   - [Requisitos previos](get-started/prerequisites.md)
- Distiller de datos {#data-distiller}
   - [Uso de licencias](data-distiller/licence-usage.md)
   - Almacén acelerado de consultas {#query-accelerated-store}
      - [Envío de consultas aceleradas](data-distiller/query-accelerated-store/send-accelerated-queries.md)
      - [Guía del modelo de datos de perspectivas de informes](data-distiller/query-accelerated-store/reporting-insights-data-model.md)
   - Atributos derivados {#derived-attributes}
      - [Información general](data-distiller/derived-attributes/overview.md)
      - [Crear atributos derivados basados en decimales](data-distiller/derived-attributes/decile-based-derived-attributes.md)
- Casos de uso {#use-cases}
   - [Exploración abandonada](use-cases/abandoned-browse.md)
   - [Análisis de actividades con Adobe Target](use-cases/activity-analysis-with-adobe-target.md)
   - [Análisis de atribución](use-cases/attribution-analysis.md)
   - [Filtrado de bots](use-cases/bot-filtering.md)
   - [Crear un informe de tendencias de eventos](use-cases/trended-report-of-events.md)
   - [Atributos derivados basados en decimales](use-cases/deciles-use-case.md)
   - [Enumerar las vistas de página de un usuario](use-cases/list-visitor-sessions.md)
   - [Enumerar visitantes según sus vistas de página](use-cases/visitors-by-number-of-page-views.md)
   - [Puntuación de tendencia](use-cases/propensity-score.md)
   - [SQLAlchemy](use-cases/sqlalchemy.md)
   - [Devolución y uso de variables de comercialización a partir de datos de Analytics](use-cases/merchandising-variables.md)
   - [Ver el informe de resumen de un visitante](use-cases/roll-up-report-of-a-visitor.md)
   - [Perspectivas de análisis web y móvil](use-cases/analytics-insights.md)
- Conectar clientes con el servicio de consulta {#clients}
   - [Información general sobre conexiones de cliente](clients/overview.md)
   - [Modos SSL](./clients/ssl-modes.md)
   - [Estudio de datos de Aqua](clients/aqua-data-studio.md)
   - [DbVisualizer](./clients/dbvisulaizer.md)
   - [Portátil Jupyter](clients//jupyter-notebook.md)
   - [Buscador](clients/looker.md)
   - [Postico](clients/postico.md)
   - [Power BI](clients/power-bi.md)
   - [PSQL](clients/psql.md)
   - [RStudio](clients/rstudio.md)
   - [Tableau](clients/tableau.md)
- Interfaz de usuario del servicio de consulta {#ui}
   - [Información general sobre la IU](ui/overview.md)
   - [Guía del usuario del Editor de consultas](ui/user-guide.md)
   - [Plantillas de consulta](ui/query-templates.md)
   - [Programaciones de consultas](ui/query-schedules.md)
   - [Monitorización de consultas programadas](ui/monitor-queries.md)
   - [Guía de credenciales](ui/credentials.md)
   - [Generar conjuntos de datos de salida a partir de resultados de consulta](ui/create-datasets.md)
- Puntos finales de API del servicio de consulta {#api}
   - [Primeros pasos](api/getting-started.md)
   - [Consultas](api/queries.md)
   - [Parámetros de conexión](api/connection-parameters.md)
   - [Programaciones](api/scheduled-queries.md)
   - [Ejecuta para consultas programadas](api/runs-scheduled-queries.md)
   - [Plantillas de consulta](api/query-templates.md)
   - [Consultas aceleradas](api/accelerated-queries.md)
   - [Suscripciones de alertas](api/alert-subscriptions.md)
- Control de datos {#data-governance}
   - [Información general](data-governance/overview.md)
   - [Guía de registro de auditoría](data-governance/audit-log-guide.md)
   - [Identidades en conjuntos de datos de esquema específicos](data-governance/ad-hoc-schema-identities.md)
   - [Compatibilidad con el control de acceso basado en atributos para esquemas ad hoc](./data-governance/ad-hoc-schema-labels.md)
- Prácticas recomendadas {#best-practices}
   - [Ejecución de la consulta](best-practices/writing-queries.md)
   - [Organización de recursos de datos](./best-practices/organize-data-assets.md)
- Conceptos esenciales {#essential-concepts}
   - [Trabajo con estructuras de datos anidadas](essential-concepts/nested-data-structures.md)
   - [Acoplar estructuras de datos anidadas](essential-concepts/flatten-nested-data.md)
   - [Bloque anónimo](essential-concepts/anonymous-block.md)
   - [Carga incremental](essential-concepts/incremental-load.md)
   - [Deduplicación de datos](essential-concepts/deduplication.md)
   - [Ejemplos de conjuntos de datos](essential-concepts/dataset-samples.md)
- Referencia SQL {#sql}
   - [Información general de SQL](sql/overview.md)
   - [Sintaxis SQL](sql/syntax.md)
   - [Funciones definidas por Adobe](sql/adobe-defined-functions.md)
   - [Spark SQL functions](sql/spark-sql-functions.md)
   - [Comandos de metadatos](sql/metadata.md)
   - [Declaraciones preparadas](sql/prepared-statements.md)
- [Preguntas frecuentes](troubleshooting-guide.md)
- [Referencia de API](https://www.adobe.io/experience-platform-apis/references/query-service/)
- [Notas de la versión de Platform](https://www.adobe.com/go/platform-release-notes-en)
