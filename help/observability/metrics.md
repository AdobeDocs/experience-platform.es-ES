---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Métricas disponibles
topic: developer guide
translation-type: tm+mt
source-git-commit: 947955403a270914437d9172bca458f9c49ccd8f

---


# Lista de las métricas disponibles

A continuación se muestra una lista de métricas que están expuestas por Observability Insights, cada una con su servicio de plataforma, descripción y parámetro de consulta de ID aceptado.

| Métrica de perspectivas | Servicio de plataforma | Descripción | Parámetro de consulta de ID |
| ---- | ---- | ---- | ---- |
| timeseries.ingestion.dataset.new.count | Ingesta de datos | Número total de conjuntos de datos creados. | N/D |
| timeseries.ingestion.dataset.size | Ingesta de datos | Tamaño acumulado de todos los datos ingeridos para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos (opcional) |
| timeseries.ingestion.dataset.dailysize | Ingesta de datos | Tamaño de los datos ingestados en base al uso diario para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos (opcional) |
| timeseries.ingestion.dataset.batchfailed.count | Ingesta de datos | Número de lotes en los que se ha producido un error en un conjunto de datos o en todos los conjuntos de datos. | Id. de conjunto de datos (opcional) |
| timeseries.ingestion.dataset.batchsuccess.count | Ingesta de datos | Número de lotes ingeridos para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos (opcional) |
| timeseries.ingestion.dataset.recordsuccess.count | Ingesta de datos | Número de registros ingeridos para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos (opcional) |
| timeseries.data.collection.validation.total.messages.rate | Ingesta de datos (flujo continuo) | Número total de mensajes para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos (opcional) |
| timeseries.data.collection.validation.valid.messages.rate | Ingesta de datos (flujo continuo) | Número total de mensajes válidos para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos (opcional) |
| timeseries.data.collection.validation.Invalid.messages.rate | Ingesta de datos (flujo continuo) | Número total de mensajes no válidos para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos (opcional) |
| timeseries.data.collection.validation.categoría.type.count | Ingesta de datos (flujo continuo) | Número total de mensajes de &quot;tipo&quot; no válidos para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos (opcional) |
| timeseries.data.collection.validation.categoría.range.count | Ingesta de datos (flujo continuo) | Número total de mensajes de &quot;intervalo&quot; no válidos para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos (opcional) |
| timeseries.data.collection.validation.categoría.format.count | Ingesta de datos (flujo continuo) | Número total de mensajes de &quot;formato&quot; no válidos para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos (opcional) |
| timeseries.data.collection.validation.categoría.pattern.count | Ingesta de datos (flujo continuo) | Número total de mensajes de &quot;patrón&quot; no válidos para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos (opcional) |
| timeseries.data.collection.validation.categoría.presence.count | Ingesta de datos (flujo continuo) | Número total de mensajes de &quot;presencia&quot; no válidos para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos (opcional) |
| timeseries.data.collection.validation.categoría.enum.count | Ingesta de datos (flujo continuo) | Número total de mensajes &quot;enum&quot; no válidos para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos (opcional) |
| timeseries.data.collection.validation.categoría.unclassi.count | Ingesta de datos (flujo continuo) | Número total de mensajes &quot;no clasificados&quot; no válidos para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos (opcional) |
| timeseries.data.collection.validation.categoría.unknown.count | Ingesta de datos (flujo continuo) | Número total de mensajes &quot;desconocidos&quot; no válidos para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos (opcional) |
| timeseries.data.collection.inlet.total.messages.received | Ingesta de datos (flujo continuo) | Número total de mensajes recibidos para una entrada de datos o para todas las entradas de datos. | ID de entrada (opcional) |
| timeseries.data.collection.inlet.total.messages.size.received | Ingesta de datos (flujo continuo) | Tamaño total de los datos recibidos para una entrada de datos o para todas las entradas de datos. | ID de entrada (opcional) |
| timeseries.data.collection.inlet.success | Ingesta de datos (flujo continuo) | Número total de llamadas HTTP correctas a una entrada de datos o a todas las entradas de datos. | ID de entrada (opcional) |
| timeseries.data.collection.inlet.fail | Ingesta de datos (flujo continuo) | Número total de llamadas HTTP fallidas a una entrada de datos o a todas las entradas de datos. | ID de entrada (opcional) |
| timeseries.perfiles.dataset.recordread.count | Perfil del cliente en tiempo real | Número de registros leídos del lago de datos por Perfil, para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos (opcional) |
| timeseries.perfiles.dataset.recordsuccess.count | Perfil del cliente en tiempo real | Número de registros escritos en su fuente de datos por Perfil, para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos (opcional) |
| timeseries.perfiles.dataset.recordfailed.count | Perfil del cliente en tiempo real | Número de registros con errores por Perfil, para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos (opcional) |
| timeseries.perfiles.dataset.batchsuccess.count | Perfil del cliente en tiempo real | Número de lotes de Perfil ingeridos para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos (opcional) |
| timeseries.perfiles.dataset.batchfailed.count | Perfil del cliente en tiempo real | Número de lotes de Perfil con error para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos (opcional) |
| timeseries.identity.dataset.recordsuccess.count | Servicio de identidad | Número de registros escritos en la fuente de datos por Identity Service, para un conjunto de datos o todos los conjuntos de datos. | Id. de conjunto de datos (opcional) |
| timeseries.identity.dataset.recordfailed.count | Servicio de identidad | Número de registros en los que el servicio de identidad ha fallado, para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos (opcional) |
| timeseries.identity.dataset.namespacecode.recordsuccess.count | Servicio de identidad | Número de registros de identidad que se han ingerido correctamente para una Área de nombres. | ID de Área de nombres (**requerido**) |
| timeseries.identity.dataset.namespacecode.recordfailed.count | Servicio de identidad | Número de registros de identidad con error de una Área de nombres. | ID de Área de nombres (**requerido**) |
| timeseries.identity.dataset.namespacecode.recordskipped.count | Servicio de identidad | Número de registros de identidad omitidos por una Área de nombres. | ID de Área de nombres (**requerido**) |
| timeseries.identity.graph.imsorg.uniqueidentities.count | Servicio de identidad | Número de identidades únicas almacenadas en el gráfico de identidad de la organización de IMS. | N/D |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | Servicio de identidad | Número de identidades únicas almacenadas en el gráfico de identidad de una Área de nombres. | ID de Área de nombres (**requerido**) |
| timeseries.identity.graph.imsorg.numidgraphics.count | Servicio de identidad | Número de identidades gráficas únicas almacenadas en el gráfico de identidad de su organización de IMS. | N/D |
| timeseries.identity.graph.imsorg.graphforce.uniqueidentities.count | Servicio de identidad | Número de identidades únicas almacenadas en el gráfico de identidad de la organización de IMS para una intensidad de gráfico determinada (&quot;desconocida&quot;, &quot;débil&quot; o &quot;fuerte&quot;). | Intensidad del gráfico (**obligatoria**) |
| timeseries.gdpr.job.totaljob.count | RGPD | Número total de trabajos creados a partir del RGPD. | ENV (**requerido**) |
| timeseries.gdpr.Jobs.completeJobs.count | RGPD | Número total de trabajos completados del RGPD. | ENV (**requerido**) |
| timeseries.gdpr.job.errorjob.count | RGPD | Número total de trabajos de error del RGPD. | ENV (**requerido**) |
| timeseries.queryservice.consulta.schedule.once.count | Servicio de Consulta | Número total de consultas programadas no recurrentes. | N/D |
| timeseries.queryservice.consulta.schedule recurrente.count | Servicio de Consulta | Número total de consultas programadas recurrentes. | N/D |
| timeseries.queryservice.consulta.batchquery.count | Servicio de Consulta | Número total de consultas por lotes ejecutadas. | N/D |
| timeseries.queryservice.consulta.schedulequery.count | Servicio de Consulta | Número total de consultas programadas ejecutadas. | N/D |
| timeseries.queryservice.consulta.interactivequery.count | Servicio de Consulta | Número total de consultas interactivas ejecutadas. | N/D |
| timeseries.queryservice.consulta.batchfrompsqlquery.count | Servicio de Consulta | Número total de consultas por lotes ejecutadas desde PSQL. | N/D |