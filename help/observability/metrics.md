---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Métricas disponibles
topic: developer guide
translation-type: tm+mt
source-git-commit: 6a988c990d3d4df706a44cdbc82f77bef20c2ea1

---


# Lista de las métricas disponibles

Las siguientes tablas lista todas las métricas expuestas por Perspectivas de la Observabilidad, desglosadas por servicio de plataforma. Cada métrica incluye una descripción y un parámetro de consulta de ID aceptado.

## Ingesta de datos

La siguiente tabla describe las métricas de la inserción de datos de la plataforma Adobe Experience Platform. Las métricas en **negrita** son métricas de ingesta de flujo continuo.

| Métrica de perspectivas | Descripción | Parámetro de consulta de ID |
| ---- | ---- | ---- | ---- |
| timeseries.ingestion.dataset.new.count | Número total de conjuntos de datos creados. | N/D |
| timeseries.ingestion.dataset.size | Tamaño acumulado de todos los datos ingeridos para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos (opcional) |
| timeseries.ingestion.dataset.dailysize | Tamaño de los datos ingestados en base al uso diario para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos (opcional) |
| timeseries.ingestion.dataset.batchfailed.count | Número de lotes en los que se ha producido un error en un conjunto de datos o en todos los conjuntos de datos. | Id. de conjunto de datos (opcional) |
| timeseries.ingestion.dataset.batchsuccess.count | Número de lotes ingeridos para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos (opcional) |
| timeseries.ingestion.dataset.recordsuccess.count | Número de registros ingeridos para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos (opcional) |
| **timeseries.data.collection.validation.total.messages.rate** | Número total de mensajes para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos (opcional) |
| **timeseries.data.collection.validation.valid.messages.rate** | Número total de mensajes válidos para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos (opcional) |
| **timeseries.data.collection.validation.Invalid.messages.rate** | Número total de mensajes no válidos para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos (opcional) |
| **timeseries.data.collection.validation.categoría.type.count** | Número total de mensajes de &quot;tipo&quot; no válidos para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos (opcional) |
| **timeseries.data.collection.validation.categoría.range.count** | Número total de mensajes de &quot;intervalo&quot; no válidos para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos (opcional) |
| **timeseries.data.collection.validation.categoría.format.count** | Número total de mensajes de &quot;formato&quot; no válidos para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos (opcional) |
| **timeseries.data.collection.validation.categoría.pattern.count** | Número total de mensajes de &quot;patrón&quot; no válidos para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos (opcional) |
| **timeseries.data.collection.validation.categoría.presence.count** | Número total de mensajes de &quot;presencia&quot; no válidos para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos (opcional) |
| **timeseries.data.collection.validation.categoría.enum.count** | Número total de mensajes &quot;enum&quot; no válidos para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos (opcional) |
| **timeseries.data.collection.validation.categoría.unclassi.count** | Número total de mensajes &quot;no clasificados&quot; no válidos para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos (opcional) |
| **timeseries.data.collection.validation.categoría.unknown.count** | Número total de mensajes &quot;desconocidos&quot; no válidos para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos (opcional) |
| **timeseries.data.collection.inlet.total.messages.received** | Número total de mensajes recibidos para una entrada de datos o para todas las entradas de datos. | ID de entrada (opcional) |
| **timeseries.data.collection.inlet.total.messages.size.received** | Tamaño total de los datos recibidos para una entrada de datos o para todas las entradas de datos. | ID de entrada (opcional) |
| **timeseries.data.collection.inlet.success** | Número total de llamadas HTTP correctas a una entrada de datos o a todas las entradas de datos. | ID de entrada (opcional) |
| **timeseries.data.collection.inlet.fail** | Número total de llamadas HTTP fallidas a una entrada de datos o a todas las entradas de datos. | ID de entrada (opcional) |

## Servicio de identidad

La tabla siguiente describe las métricas del servicio de identidad de Adobe Experience Platform.

| Métrica de perspectivas | Descripción | Parámetro de consulta de ID |
| ---- | ---- | ---- | ---- |
| timeseries.identity.dataset.recordsuccess.count | Número de registros escritos en la fuente de datos por Identity Service, para un conjunto de datos o todos los conjuntos de datos. | Id. de conjunto de datos (opcional) |
| timeseries.identity.dataset.recordfailed.count | Número de registros en los que el servicio de identidad ha fallado, para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos (opcional) |
| timeseries.identity.dataset.namespacecode.recordsuccess.count | Número de registros de identidad que se han ingerido correctamente para una Área de nombres. | ID de Área de nombres (**requerido**) |
| timeseries.identity.dataset.namespacecode.recordfailed.count | Número de registros de identidad con error de una Área de nombres. | ID de Área de nombres (**requerido**) |
| timeseries.identity.dataset.namespacecode.recordskipped.count | Número de registros de identidad omitidos por una Área de nombres. | ID de Área de nombres (**requerido**) |
| timeseries.identity.graph.imsorg.uniqueidentities.count | Número de identidades únicas almacenadas en el gráfico de identidad de la organización de IMS. | N/D |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | Número de identidades únicas almacenadas en el gráfico de identidad de una Área de nombres. | ID de Área de nombres (**requerido**) |
| timeseries.identity.graph.imsorg.numidgraphs.count | Número de identidades gráficas únicas almacenadas en el gráfico de identidad de su organización de IMS. | N/D |
| timeseries.identity.graph.imsorg.graphstrength.uniqueidentities.count | Número de identidades únicas almacenadas en el gráfico de identidad de la organización de IMS para una intensidad de gráfico determinada (&quot;desconocida&quot;, &quot;débil&quot; o &quot;fuerte&quot;). | Intensidad del gráfico (**obligatoria**) |

## Privacy Service

La tabla siguiente describe las métricas de Adobe Experience Platform Privacy Service.

| Métrica de perspectivas | Descripción | Parámetro de consulta de ID |
| ---- | ---- | ---- | ---- |
| timeseries.gdpr.jobs.totaljobs.count | Número total de trabajos creados a partir del RGPD. | ENV (**requerido**) |
| timeseries.gdpr.jobs.completedjobs.count | Número total de trabajos completados del RGPD. | ENV (**requerido**) |
| timeseries.gdpr.jobs.errorjobs.count | Número total de trabajos de error del RGPD. | ENV (**requerido**) |

## Servicio de Consulta

La siguiente tabla describe las métricas del servicio de Consulta de la plataforma Adobe Experience Platform.

| Métrica de perspectivas | Descripción | Parámetro de consulta de ID |
| ---- | ---- | ---- | ---- |
| timeseries.queryservice.query.scheduleonce.count | Número total de consultas programadas no recurrentes. | N/D |
| timeseries.queryservice.query.scheduledrecurring.count | Número total de consultas programadas recurrentes. | N/D |
| timeseries.queryservice.query.batchquery.count | Número total de consultas por lotes ejecutadas. | N/D |
| timeseries.queryservice.query.scheduledquery.count | Número total de consultas programadas ejecutadas. | N/D |
| timeseries.queryservice.query.interactivequery.count | Número total de consultas interactivas ejecutadas. | N/D |
| timeseries.queryservice.query.batchfrompsqlquery.count | Número total de consultas por lotes ejecutadas desde PSQL. | N/D |

## Perfil del cliente en tiempo real

La siguiente tabla describe las métricas de Perfil del cliente en tiempo real.

| Métrica de perspectivas | Descripción | Parámetro de consulta de ID |
| ---- | ---- | ---- | ---- |
| timeseries.profiles.dataset.recordread.count | Número de registros leídos del lago de datos por Perfil, para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos (opcional) |
| timeseries.profiles.dataset.recordsuccess.count | Número de registros escritos en su fuente de datos por Perfil, para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos (opcional) |
| timeseries.profiles.dataset.recordfailed.count | Número de registros con errores por Perfil, para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos (opcional) |
| timeseries.profiles.dataset.batchsuccess.count | Número de lotes de Perfil ingeridos para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos (opcional) |
| timeseries.profiles.dataset.batchfailed.count | Número de lotes de Perfil con error para un conjunto de datos o para todos los conjuntos de datos. | Id. de conjunto de datos (opcional) |
| platform.ups.ingest.streaming.request.m1_rate | Tasa de solicitud entrante. | Organización IMS |
| platform.ups.ingest.streaming.access.put.success.m1_rate | Tasa de éxito de inserción. | Organización IMS |
| platform.ups.ingest.streaming.records.created.m15_rate | Tasa de nuevos registros ingeridos para un conjunto de datos. | Id. de conjunto de datos |
| platform.ups.ingest.streaming.request.error.created.outOfOrder.m1_rate | Tasa de registros con marca de hora desordenada para crear solicitudes para un conjunto de datos. | Id. de conjunto de datos |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.created.timestamp | Marca de hora para la última solicitud de registro de creación de un conjunto de datos. | Id. de conjunto de datos |
| platform.ups.ingest.streaming.request.error.updated.outOfOrder.m1_rate | Tasa de registros con marca de hora desordenada para la solicitud de actualización de un conjunto de datos. | Id. de conjunto de datos |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.updated.timestamp | Marca de hora para la última solicitud de registro de actualización de un conjunto de datos. | Id. de conjunto de datos |
| platform.ups.ingest.streaming.record.size.m1_rate | Tamaño promedio del registro. | Organización IMS |
| platform.ups.ingest.streaming.records.updated.m15_rate | Tasa de solicitudes de actualización para registros ingestados para un conjunto de datos. | Id. de conjunto de datos |
