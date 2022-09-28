---
keywords: Experience Platform;inicio;temas populares;intervalo de fechas
title: Reglas de alerta estándar
description: Este documento cubre las reglas de alerta predefinidas proporcionadas por el Experience Platform.
feature: Alerts
exl-id: b4af1c15-b1bc-4e4b-a447-09cc17a63988
source-git-commit: f707a6338ad72578328b363792010fa50ea9ce88
workflow-type: tm+mt
source-wordcount: '966'
ht-degree: 3%

---

# Reglas de alerta estándar

Adobe Experience Platform proporciona varias reglas de alerta predefinidas que puede habilitar para su organización. Este documento cubre los detalles de estas reglas de alerta proporcionadas por el Adobe. Para obtener información más general sobre las alertas en el Experience Platform, consulte la [información general sobre alertas](./overview.md).

When [visualización de reglas de alerta en la interfaz de usuario de Platform](./ui.md), puede suscribirse a cada regla individualmente. Al suscribirse a alertas mediante [Notificaciones de eventos de E/S](./subscribe.md)sin embargo, las reglas de alerta están organizadas en diferentes paquetes de suscripción. En las tablas siguientes, cada regla se muestra con su nombre de suscripción correspondiente al Evento de E/S.

## Ingesta de datos

Las siguientes reglas de alerta son específicas de [Ingesta de datos](../../ingestion/home.md) y  [sources](../../sources/home.md):

| Suscripción a un evento de E/S | Regla de alerta | Descripción |
| --- | --- | --- |
| Información de ejecución del flujo de origen | Inicio de ejecución del flujo de fuentes | Esta alerta déclencheur cuando una conexión de origen comienza a procesar datos. |
| Información de ejecución del flujo de origen | Éxito en la ejecución del flujo de fuentes | Esta alerta déclencheur cuando los datos se introducen correctamente desde una conexión de origen. |
| Retrasos, errores y errores de ejecución del flujo de origen | Error en la ejecución del flujo de fuentes | Esta alerta déclencheur cuando se produce un error al introducir datos desde una conexión de origen. |
| Retrasos, errores y errores de ejecución del flujo de origen | Retraso de ingesta | Esta alerta déclencheur cuando la ejecución de un flujo de ingesta por lotes tarda más de 150 minutos en procesarse. |
| Retrasos, errores y errores de ejecución del flujo de origen | Fallo de ingesta | Esta alerta déclencheur cuando la proporción de registros con errores en todos los registros supera un umbral del 0,5 %. |

{style=&quot;table-layout:auto&quot;}

Si se ha suscrito previamente al siguiente tipo de alerta, ya no recibirá alertas, ya que esta alerta ha quedado obsoleta:

| Suscripción a un evento de E/S | Regla de alerta | Descripción |
| --- | --- | --- |
| Retrasos, errores y errores de ejecución del flujo de origen | Falta de ingesta | Esta alerta le envía un mensaje si la ingesta se retrasa más de siete horas y no se introducen datos en Platform. |

{style=&quot;table-layout:auto&quot;}

## Servicio de identidad

Las siguientes reglas de alerta son específicas de [Servicio de identidad](../../identity-service/home.md):

| Suscripción a un evento de E/S | Regla de alerta | Descripción |
| --- | --- | --- |
| Información de ingesta de identidad | Inicio de la ejecución del flujo del servicio de identidad | Esta alerta déclencheur cuando se inicia la ejecución de un flujo del servicio de identidad, al procesar los datos. En otras palabras, los datos ingestados se están cargando desde el lago de datos en el servicio de identidad. |
| Información de ingesta de identidad | Correcto de ejecución del flujo del servicio de identidad | Esta alerta déclencheur cuando los datos se cargan correctamente desde el lago de datos en el servicio de identidad. |
| Retrasos, errores y errores de ingesta de identidad | Retraso de ejecución del flujo del servicio de identidad | Este déclencheur se produce cuando la ejecución de un flujo del servicio de identidad tarda más de 150 minutos en procesarse. |
| Retrasos, errores y errores de ingesta de identidad | Error de ejecución del flujo del servicio de identidad | Esta alerta déclencheur cuando se produce un error al ingerir datos en el servicio de identidad. |

{style=&quot;table-layout:auto&quot;}

## Perfil del cliente en tiempo real

Las siguientes reglas de alerta son específicas de [Perfil del cliente en tiempo real](../../profile/home.md):

| Suscripción a un evento de E/S | Regla de alerta | Descripción |
| --- | --- | --- |
| Información de ingesta de perfiles | Inicio de la ejecución del flujo de perfiles | Esta alerta déclencheur cuando se inicia la ejecución de un flujo de perfiles para procesar datos. |
| Información de ingesta de perfiles | Éxito en la ejecución del flujo de perfiles | Esta alerta déclencheur cuando los datos se cargan correctamente en Perfil desde el lago de datos. |
| Retrasos, errores y errores de ingesta de perfiles | Retraso de ejecución del flujo de perfil | Esta alerta se déclencheur cuando se cargan datos del lago de datos en el perfil durante más de 150 minutos. |
| Retrasos, errores y errores de ingesta de perfiles | Error de ejecución del flujo de perfil | Esta alerta déclencheur cuando se produce un error al ingerir datos en el perfil. |

{style=&quot;table-layout:auto&quot;}

## Segmentación

Las siguientes reglas de alerta son específicas de [Servicio de segmentación](../../segmentation/home.md):

| Suscripción a un evento de E/S | Regla de alerta | Descripción |
| --- | --- | --- |
| Información del trabajo de evaluación de segmentos | Inicio del trabajo del segmento | Esta alerta déclencheur cuando un trabajo de evaluación de segmentos comienza a procesar datos. |
| Información del trabajo de evaluación de segmentos | Éxito en el trabajo de segmentos | Esta alerta déclencheur cuando un trabajo de evaluación de segmentos se completa correctamente. |
| Retrasos, errores y errores del trabajo de evaluación de segmentos | Retraso de trabajo del segmento | Esta alerta déclencheur cuando los trabajos de evaluación de segmentos tardan más de 150 minutos en completarse. |
| Retrasos, errores y errores del trabajo de evaluación de segmentos | Error en el trabajo del segmento | Esta alerta déclencheur cuando un trabajo de evaluación de segmentos resulta en un error. |
| Retrasos, errores y errores del trabajo de evaluación de segmentos | Definición de segmento deshabilitada | Esta alerta déclencheur cuando una definición de segmento está deshabilitada debido a un error interno. Esto automáticamente déclencheur una sala de guerra para que un equipo de ingeniería de Adobe investigue el problema. Esta alerta solo pretende ser informativa y no requiere ninguna acción por su parte. |

{style=&quot;table-layout:auto&quot;}

## Destinos

Las siguientes reglas de alerta son específicas de [destinos](../../destinations/home.md):

| Suscripción a un evento de E/S | Regla de alerta | Descripción |
| --- | --- | --- |
| Información de ejecución del flujo de destino | Inicio de la ejecución del flujo de destino | Esta alerta déclencheur cuando una ejecución de flujo de destino comienza a activar un segmento. |
| Información de ejecución del flujo de destino | Éxito de ejecución del flujo de destino | Esta alerta déclencheur cuando un segmento se activa correctamente en un destino. |
| Retrasos, errores y errores de ejecución del flujo de destino | Retraso de ejecución del flujo de destino | Este déclencheur se produce cuando la ejecución de un flujo de destino tarda más de 150 minutos en activarse un segmento. |
| Retrasos, errores y errores de ejecución del flujo de destino | Error de ejecución del flujo de destino | Este déclencheur se produce cuando se produce un error al activar un segmento en un destino. |
| Retrasos, errores y errores de ejecución del flujo de destino | La tasa de omisión de página supera el umbral | Este déclencheur se genera cuando la proporción de ID omitidos con respecto a los ID totales supera un umbral. |

{style=&quot;table-layout:auto&quot;}

## Servicio de consultas

Las siguientes reglas de alerta son específicas de [Servicio de consultas](../../query-service/home.md):

| Suscripción a un evento de E/S | Regla de alerta | Descripción |
| --- | --- | --- |
| Información ad hoc del servicio de consultas | Éxito ad hoc del servicio de consultas | Esta alerta déclencheur cuando un trabajo de esquema ad hoc se completa correctamente. |
| Retrasos, errores y errores específicos del servicio de consultas | Fallo ad hoc del servicio de consulta | Esta alerta déclencheur cuando falla un trabajo de esquema ad hoc. |
| Información de consulta programada del servicio de consulta | Inicio de consulta programada del servicio de consulta | Esta alerta déclencheur cuando se empieza a ejecutar una consulta programada. |
| Información de consulta programada del servicio de consulta | Éxito de consulta programada del servicio de consulta | Esta alerta déclencheur cuando un trabajo de consulta programado se completa correctamente. |
| Retrasos, errores y errores de consultas programadas del servicio de consultas | error de consulta programada del servicio de consulta | Esta alerta déclencheur cuando falla un trabajo de consulta programado. |

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
