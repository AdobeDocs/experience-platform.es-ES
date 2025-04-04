---
title: Migración de Data Lake a Gen2
description: Obtenga información sobre las nuevas funciones que proporciona la migración del lago de datos a Gen2 en Adobe Experience Platform.
exl-id: 56d9c77a-d7eb-498d-994f-b15d150dedb7
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# Migración de Adobe Experience Platform Data Lake a Gen2

Adobe Experience Platform está migrando al lago de datos Gen2. Se trata de una nueva generación de lago de datos que proporciona a los usuarios de Experience Platform ventajas como replicación de regiones geográficas, controles de acceso basados en funciones más precisos (RBAC) y una mejor escala.

## Impacto del usuario

Mientras Adobe migra el lago de datos de Gen1 a Gen 2, los usuarios podrán **leer** del lago de datos, pero todas las capacidades que **escriba** en el lago de datos se verán afectadas. A continuación se muestra una lista de las capacidades afectadas:

- **Fuentes**: Los datos que llegan desde las fuentes y varios flujos de trabajo de ingesta de datos se retrasarán. Los usuarios verán sus datos una vez que se haya completado la migración.
- **Servicio de consultas**: los usuarios pueden realizar consultas, pero no podrán escribir el resultado de la consulta en un conjunto de datos.
- **Perfil del cliente en tiempo real**: Los datos ingeridos en el almacén de perfiles mediante la ingesta de **lotes** no estarán disponibles durante la migración. Sin embargo, los datos ingeridos mediante la ingesta de **streaming** estarán disponibles durante la migración. Además, las exportaciones de perfiles no estarán disponibles durante la migración.
- **Data Science Workspace**: Las escrituras de Data Science Workspace fallarán.
- **Servicio de segmentación**: Las audiencias derivadas de la segmentación **por lotes** no se pueden activar durante la migración. Las audiencias derivadas de la segmentación **streaming** no se verán afectadas.
- **Customer Journey Analytics**: los datos de los informes de Customer Journey Analytics pueden no estar actualizados y no se actualizarán durante la migración, ya que los lotes no se están ingiriendo en el lago de datos.

## Comunicación a los usuarios de Experience Platform

Adobe se pondrá en contacto con los administradores del sistema para analizar en detalle el impacto de la migración y confirmar las fechas y horas de migración de organizaciones específicas.
