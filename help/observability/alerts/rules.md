---
keywords: Experience Platform;inicio;temas populares;intervalo de fechas
title: Reglas de alerta estándar
description: 'Este documento cubre las reglas de alerta predefinidas proporcionadas por el Experience Platform. '
source-git-commit: de8d8d92622abc75f2d09f4bb771dbe4268d0b38
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 12%

---


# Reglas de alerta estándar

Adobe Experience Platform proporciona varias reglas de alerta predefinidas que puede habilitar para su organización. La siguiente tabla cubre los detalles de estas reglas de alerta proporcionadas por el Adobe. Para obtener información más general sobre las alertas en el Experience Platform, consulte la [descripción general de las alertas](./overview.md).

| Regla | Descripción | Frecuencia de evaluación | Ventana de repetición |
| --- | --- | --- | --- |
| Éxito en la ejecución del flujo de fuentes | Esta alerta déclencheur cuando los datos se introducen correctamente desde una conexión de origen. | N/D | N/D |
| Error en la ejecución del flujo de fuentes | Esta alerta déclencheur cuando se produce un error al introducir datos desde una conexión de origen. | N/D | N/D |
| Retraso de trabajo del segmento | Este déclencheur se produce cuando los trabajos de un segmento tardan más de 150 minutos en completarse. | 30 segundos | 3 horas |
| Definición de segmento deshabilitada | Esta alerta déclencheur cuando se deshabilita una definición de segmento. | N/D | N/D |

{style=&quot;table-layout:auto&quot;}

<!-- (Definitions to be added once available)
| Entitlement Threshold Exceeded | This alert triggers when the number of created profiles exceeds 80% of your organization's entitlement. | 30 seconds | N/A |
| No ingestion activity in past 24 hours | This alert triggers when no new data has been ingested in the last 24-hour period. | 1 day | 1 day |
| SFTP source has not ingested data | This alert triggers when an [SFTP source](../../sources/connectors/cloud-storage/sftp.md) has not ingested any data within a certain time period. | 1 day | 1 day |
| Ingestion error rate exceeded | This alert triggers when the error rate for data ingestion exceeds 20%. | 30 seconds | 30 seconds |
| Feed Message | This alert when an identity sharing feed message has been sent to a user using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Access Revoked | This alert triggers when another Platform user revokes access to an identity sharing feed using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Modified | This alert triggers when an identity sharing feed is modified by a user using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Shared | This alert triggers when a user shares a new feed in [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Link Request | This alert triggers when a user requests to connect for partner sharing. | N/A | N/A |
| Link Action | This alert triggers when a user accepts a request to connect for partner sharing. | N/A | N/A |
-->
