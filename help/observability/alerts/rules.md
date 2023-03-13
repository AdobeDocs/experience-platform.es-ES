---
keywords: Experience Platform;inicio;temas populares;intervalo de fechas
title: Reglas de alerta estándar
description: Este documento describe las reglas de alerta predefinidas proporcionadas por Experience Platform.
feature: Alerts
exl-id: b4af1c15-b1bc-4e4b-a447-09cc17a63988
source-git-commit: 6650894c145fd1f42731fd5ed8aeb6e38062aa61
workflow-type: tm+mt
source-wordcount: '943'
ht-degree: 1%

---

# Reglas de alerta estándar

Adobe Experience Platform proporciona varias reglas de alerta predefinidas que puede habilitar para su organización. Este documento cubre los detalles de estas reglas de alerta proporcionadas por el Adobe. Para obtener información más general sobre las alertas de Experience Platform, consulte la [información general sobre alertas](./overview.md).

Cuándo [visualización de reglas de alerta en la IU de Platform](./ui.md), puede suscribirse a cada regla individualmente. Al suscribirse a alertas mediante [Notificaciones de eventos de E/S](./subscribe.md)Sin embargo, las reglas de alerta están organizadas en diferentes paquetes de suscripción. En las tablas siguientes, cada regla se muestra con su nombre de suscripción de evento de E/S correspondiente.

## Ingesta de datos

Las siguientes reglas de alerta son específicas de [Ingesta de datos](../../ingestion/home.md) y  [orígenes](../../sources/home.md):

| Suscripción a evento de E/S | Regla de alerta | Descripción |
| --- | --- | --- |
| Información de ejecución de flujo de origen | Inicio de ejecución de flujo de fuentes | Esta alerta entra en déclencheur cuando una conexión de origen comienza a procesar datos. |
| Información de ejecución de flujo de origen | Ejecución correcta de flujo de orígenes | Esta alerta detecta un déclencheur cuando los datos se incorporan correctamente desde una conexión de origen. |
| Retrasos, errores y errores de ejecución del flujo de origen | Error de ejecución de flujo de orígenes | Esta alerta déclencheur cuando se produce un error durante la ingesta de datos desde una conexión de origen. |
| Retrasos, errores y errores de ejecución del flujo de origen | Retraso de ingesta | Esta alerta se déclencheur cuando una ejecución de flujo de ingesta por lotes tarda más de 150 minutos en procesarse. |
| Retrasos, errores y errores de ejecución del flujo de origen | Error de ingesta | Esta alerta se déclencheur cuando la proporción de registros con errores respecto a todos los registros supera un umbral del 0,5 %. |

{style="table-layout:auto"}

Si se ha suscrito anteriormente al siguiente tipo de alerta, ya no recibirá alertas porque esta alerta ha quedado obsoleta:

| Suscripción a evento de E/S | Regla de alerta | Descripción |
| --- | --- | --- |
| Retrasos, errores y errores de ejecución del flujo de origen | Falta de ingesta | Esta alerta le envía un mensaje si la ingesta se retrasa más de siete horas y no se incorporan datos en Platform. |

{style="table-layout:auto"}

## Servicio de identidad

Las siguientes reglas de alerta son específicas de [Servicio de identidad](../../identity-service/home.md):

| Suscripción a evento de E/S | Regla de alerta | Descripción |
| --- | --- | --- |
| Información de ingesta de identidad | Inicio de ejecución de flujo de servicio de identidad | Esta alerta se déclencheur cuando una ejecución del flujo del servicio de ID comienza a procesar datos. En otras palabras, los datos ingeridos se están cargando desde el lago de datos al servicio de identidad. |
| Información de ingesta de identidad | Ejecución correcta del flujo del servicio de identidad | Esta alerta déclencheur cuándo se cargan correctamente los datos del lago de datos en el servicio de identidad. |
| Retrasos, errores y errores de ingesta de identidad | Retraso de ejecución de flujo de servicio de identidad | Esta alerta se déclencheur cuando la ejecución de un flujo del servicio de ID tarda más de 150 minutos en procesarse. |
| Retrasos, errores y errores de ingesta de identidad | Error de ejecución de flujo del servicio de identidad | Esta alerta déclencheur cuando se produce un error al ingerir datos en el servicio de identidad. |

{style="table-layout:auto"}

## Perfil del cliente en tiempo real

Las siguientes reglas de alerta son específicas de [Perfil del cliente en tiempo real](../../profile/home.md):

| Suscripción a evento de E/S | Regla de alerta | Descripción |
| --- | --- | --- |
| Información de ingesta de perfil | Inicio de ejecución de flujo de perfil | Esta alerta se déclencheur cuando una ejecución de flujo de perfil comienza a procesar datos. |
| Información de ingesta de perfil | Ejecución correcta de flujo de perfil | Esta alerta déclencheur cuándo los datos se cargan correctamente en el perfil desde el lago de datos. |
| Retrasos, errores y errores de ingesta de perfiles | Retraso de ejecución de flujo de perfil | Esta alerta entra en déclencheur cuando se cargan datos del lago de datos en el perfil y tardan más de 150 minutos en procesarse. |
| Retrasos, errores y errores de ingesta de perfiles | Error de ejecución de flujo de perfil | Esta alerta déclencheur cuando se produce un error al ingerir datos en el perfil. |

{style="table-layout:auto"}

## Segmentación

Las siguientes reglas de alerta son específicas de [Servicio de segmentación](../../segmentation/home.md):

| Suscripción a evento de E/S | Regla de alerta | Descripción |
| --- | --- | --- |
| Información de trabajo de evaluación de segmentos | Inicio del trabajo de segmento | Esta alerta entra en déclencheur cuando un trabajo de evaluación de segmentos comienza a procesar datos. |
| Información de trabajo de evaluación de segmentos | Trabajo de segmento correcto | Esta alerta entra en déclencheur cuando un trabajo de evaluación de segmentos se completa correctamente. |
| Retrasos, errores y errores del trabajo de evaluación de segmentos | Retraso del trabajo del segmento | Esta alerta se déclencheur cuando los trabajos de evaluación de un segmento tardan más de 150 minutos en completarse. <br> Aparecerá uno de los siguientes estados: <br>- ACTIVACIÓN: se ha cumplido la condición para el error o el retraso (considérela en un estado ACTIVO). <br>- INACTIVO: la condición no se ha cumplido o no se ha resuelto (Considérela en un estado RESUELTO). |
| Retrasos, errores y errores del trabajo de evaluación de segmentos | Error del trabajo de segmento | Esta alerta déclencheur cuando un trabajo de evaluación de segmentos genera un error. |
| Retrasos, errores y errores del trabajo de evaluación de segmentos | Definición de segmento deshabilitada | Esta alerta se déclencheur cuando una definición de segmento está deshabilitada debido a un error interno. Esto automáticamente déclencheur una sala de guerra para un equipo de ingeniería de Adobe para investigar el problema. Esta alerta solo pretende ser informativa y no requiere ninguna acción por su parte. |

{style="table-layout:auto"}

## Destinos

Las siguientes reglas de alerta son específicas de [destinos](../../destinations/home.md):

| Suscripción a evento de E/S | Regla de alerta | Descripción |
| --- | --- | --- |
| Información de ejecución de flujo de destino | Inicio de ejecución de flujo de destino | Esta alerta entra en déclencheur cuando una ejecución de flujo de destino comienza a activar un segmento. |
| Información de ejecución de flujo de destino | Ejecución correcta de flujo de destino | Esta alerta déclencheur cuando un segmento se activa correctamente en un destino. |
| Retrasos, errores y errores de ejecución del flujo de destino | Retraso de ejecución de flujo de destino | Esta alerta se déclencheur cuando una ejecución de flujo de destino tarda más de 150 minutos en activar un segmento. |
| Retrasos, errores y errores de ejecución del flujo de destino | Error de ejecución de flujo de destino | Esta alerta déclencheur cuando se produce un error al activar un segmento en un destino. |
| Retrasos, errores y errores de ejecución del flujo de destino | La tasa de omisión supera el umbral | Esta alerta entra en déclencheur cuando la proporción de ID omitidos respecto al total de ID supera un umbral. |

{style="table-layout:auto"}

## Servicio de consultas

Las siguientes reglas de alerta son específicas de [Servicio de consultas](../../query-service/home.md):

| Suscripción a evento de E/S | Regla de alerta | Descripción |
| --- | --- | --- |
| Información de consulta programada del servicio de consultas | Inicio de consulta programado del servicio de consultas | Esta alerta entra en déclencheur cuando una consulta programada empieza a ejecutarse. |
| Información de consulta programada del servicio de consultas | Consulta programada del servicio de consulta correcta | Esta alerta se déclencheur cuando un trabajo de consulta programado se completa correctamente. |
| Retrasos, errores y errores de consulta programados del servicio de consulta | error de consulta programada del servicio de consulta | Esta alerta entra en déclencheur cuando falla un trabajo de consulta programado. |

<!-- (Definitions to be added once available)
| Segment Job Delay | This alert triggers when a segment job takes longer than 150 minutes to complete. | N/A | 30 seconds | 3 hours |
| No Ingestion Activity in Past 24 Hours | This alert triggers when no new data has been ingested in the last 24-hour period. | N/A | 1 day | 1 day |
| Ingestion Error Rate Exceeded | This alert triggers when the error rate for data ingestion exceeds the allotted threshold. | 20% | 30 seconds | 30 seconds |
| Entitlement Threshold Exceeded | This alert triggers when the number of created profiles exceeds 80% of your organization's entitlement. | 30 seconds | N/A |
| SFTP source has not ingested data | This alert triggers when an [SFTP source](../../sources/connectors/cloud-storage/sftp.md) has not ingested any data within a certain time period. | 1 day | 1 day |
| Feed Message | This alert when an identity sharing feed message has been sent to a user using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Access Revoked | This alert triggers when another Platform user revokes access to an identity sharing feed using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Modified | This alert triggers when an identity sharing feed is modified by a user using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Shared | This alert triggers when a user shares a new feed in [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Link Request | This alert triggers when a user requests to connect for partner sharing. | N/A | N/A |
| Link Action | This alert triggers when a user accepts a request to connect for partner sharing. | N/A | N/A |
-->
