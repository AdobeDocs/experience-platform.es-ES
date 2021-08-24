---
keywords: Experience Platform;inicio;temas populares;intervalo de fechas
title: Reglas de alerta estándar
description: 'Este documento cubre las reglas de alerta predefinidas proporcionadas por el Experience Platform. '
source-git-commit: 8c00fb98a213b578f6970c1e1978f0159f8f38df
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 13%

---


# Reglas de alerta estándar

Adobe Experience Platform proporciona varias reglas de alerta predefinidas que puede habilitar para su organización. La siguiente tabla cubre los detalles de estas reglas de alerta proporcionadas por el Adobe. Para obtener información más general sobre las alertas en el Experience Platform, consulte la [descripción general de las alertas](./overview.md).

| Regla | Descripción | Frecuencia de evaluación | Ventana de repetición |
| --- | --- | --- | --- |
| Umbral de derecho excedido | Esta alerta se déclencheur cuando el número de perfiles creados supera el 80 % de los derechos de su organización. | 30 segundos | N/D |
| No hay actividad de ingesta en las últimas 24 horas | Esta alerta se déclencheur cuando no se han introducido nuevos datos en el último periodo de 24 horas. | 1 día | 1 día |
| La fuente SFTP no ha introducido datos | Esta alerta déclencheur cuando una [fuente SFTP](../../sources/connectors/cloud-storage/sftp.md) no ha ingerido ningún dato en un período de tiempo determinado. | 1 día | 1 día |
| Se ha superado la tasa de error de ingesta | Este déclencheur se produce cuando la tasa de error de consumo de datos supera el 20 %. | 30 segundos | 30 segundos |
| Mensaje de fuente | Esta alerta cuando se ha enviado un mensaje de fuente de uso compartido de identidad a un usuario mediante [Segment Match](../../segmentation/ui/segment-match.md). | N/D | N/D |
| Acceso a fuente revocado | Esta alerta déclencheur cuando otro usuario de Platform revoca el acceso a una fuente de uso compartido de identidad mediante [Coincidencia de segmento](../../segmentation/ui/segment-match.md). | N/D | N/D |
| Fuente modificada | Esta alerta se déclencheur cuando un usuario modifica una fuente de uso compartido de identidad utilizando [Segment Match](../../segmentation/ui/segment-match.md). | N/D | N/D |
| Fuente compartida | Esta alerta déclencheur cuando un usuario comparte una fuente nueva en [Segment Match](../../segmentation/ui/segment-match.md). | N/D | N/D |
| Solicitud de vínculo | Esta alerta déclencheur cuando un usuario solicita conectarse para compartir socios. | N/D | N/D |
| Acción de vínculo | Esta alerta se déclencheur cuando un usuario acepta una solicitud de conexión para el uso compartido de socios. | N/D | N/D |
| Definición de segmento deshabilitada | Esta alerta déclencheur cuando se deshabilita una definición de segmento. | N/D | N/D |
| Retraso de trabajo del segmento | Este déclencheur se produce cuando los trabajos de un segmento tardan más de 150 minutos en completarse. | 30 segundos | 3 horas |
| Error en la ejecución del flujo de fuentes | Esta alerta déclencheur cuando se produce un error al introducir datos desde una conexión de origen. | N/D | N/D |
| Éxito en la ejecución del flujo de fuentes | Esta alerta déclencheur cuando los datos se introducen correctamente desde una conexión de origen. | N/D | N/D |

{style=&quot;table-layout:auto&quot;}