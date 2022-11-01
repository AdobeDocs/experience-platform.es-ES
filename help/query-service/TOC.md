---
audience: user
user-guide-title: Ayuda del servicio de Consulta de Adobe Experience Platform
breadcrumb-title: Guía del servicio de consultas
user-guide-description: Utilice SQL estándar para consultar los datos dentro del lago de datos en Experience Platform.
feature: Queries
source-git-commit: 745cf377cebb6f612820d963d9207bfec3c12338
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 18%

---


# Servicio de consultas de Adobe Experience Platform {#query}

- [Información general del servicio de consultas](home.md)
- [Paquete de servicio de consulta](packages.md)
- [Protecciones del servicio de consultas](guardrails.md)
- Distiller de datos {#data-distiller}
   - [Uso de licencias](data-distiller/licence-usage.md)
- Introducción {#get-started}
   - [Requisitos previos](get-started/prerequisites.md)
- Casos de uso {#use-cases}
   - [Exploración abandonada](use-cases/abandoned-browse.md)
   - [Análisis De Actividad Con Adobe Target](use-cases/activity-analysis-with-adobe-target.md)
   - [Análisis de atribución](use-cases/attribution-analysis.md)
   - [Filtrado de bots](use-cases/bot-filtering.md)
   - [Perspectivas de análisis web y móvil](use-cases/analytics-insights.md)
- API del servicio de consulta {#api}
   - [Primeros pasos](api/getting-started.md)
   - [Consultas](api/queries.md)
   - [Parámetros de conexión](api/connection-parameters.md)
   - [Consultas programadas](api/scheduled-queries.md)
   - [Ejecuta para consultas programadas](api/runs-scheduled-queries.md)
   - [Plantillas de consulta](api/query-templates.md)
   - [Suscripciones de alertas](api/alert-subscriptions.md)
- Interfaz de usuario del servicio de consulta {#ui}
   - [Información general sobre la IU](ui/overview.md)
   - [Guía del usuario del Editor de consultas](ui/user-guide.md)
   - [Plantillas de consulta](ui/query-templates.md)
   - [Uso de credenciales del servicio de consulta](ui/credentials.md)
   - [Generación de conjuntos de datos a partir de resultados de consultas](ui/create-datasets.md)
- [Supervisar consultas](monitor-queries.md)
- Almacén acelerado de consultas{#query-accelerated-store}
   - [Modelo de datos de perspectivas de informes](query-accelerated-store/reporting-insights-data-model.md)
- Prácticas recomendadas {#best-practices}
   - [Directrices generales para la ejecución de consultas](best-practices/writing-queries.md)
   - [Directrices para la organización de recursos de datos](./best-practices/organize-data-assets.md)
   - [Trabajo con estructuras de datos anidadas](best-practices/nested-data-structures.md)
   - [Acoplar estructuras de datos anidadas](best-practices/flatten-nested-data.md)
   - [Bloque anónimo](best-practices/anonymous-block.md)
   - [Carga incremental](best-practices/incremental-load.md)
   - [Deduplicación de datos](best-practices/deduplication.md)
- Atributos derivados {#derived-attributes}
   - [Información general](derived-attributes/overview.md)
   - [Caso de uso de decimales](derived-attributes/deciles-use-case.md)
- Consultas de ejemplo {#sample-queries}
   - [Ejemplos de consultas de eventos de experiencia](sample-queries/experience-event.md)
   - [Ejemplos de consultas de Adobe Analytics](sample-queries/adobe-analytics.md)
- Referencia SQL {#sql}
   - [Información general de SQL](sql/overview.md)
   - [Sintaxis SQL](sql/syntax.md)
   - [Funciones definidas por Adobe](sql/adobe-defined-functions.md)
   - [Spark SQL functions](sql/spark-sql-functions.md)
   - [Comandos de metadatos](sql/metadata.md)
   - [Declaraciones preparadas](sql/prepared-statements.md)
   - [Ejemplos de conjuntos de datos](sql/dataset-samples.md)
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
- Control de datos {#data-governance}
   - [Información general](data-governance/overview.md)
   - [Guía de registro de auditoría](data-governance/audit-log-guide.md)
   - [Identidades en conjuntos de datos de esquema específicos](data-governance/ad-hoc-schema-identities.md)
   - [Compatibilidad con el control de acceso basado en atributos para esquemas ad hoc](./data-governance/ad-hoc-schema-labels.md)
- [Guía de resolución de problemas](troubleshooting-guide.md)
- [Referencia de API](https://www.adobe.io/experience-platform-apis/references/query-service/)
- [Notas de la versión de Platform](https://www.adobe.com/go/platform-release-notes-en)