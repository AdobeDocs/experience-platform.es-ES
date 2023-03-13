---
title: Migración de Data Lake a Gen2
description: Obtenga información sobre las nuevas funciones que proporciona la migración del lago de datos a Gen2 en Adobe Experience Platform.
exl-id: 56d9c77a-d7eb-498d-994f-b15d150dedb7
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# Migración de Adobe Experience Platform Data Lake a Gen2

Adobe Experience Platform está migrando al lago de datos Gen2. Se trata de una nueva generación de lago de datos que proporciona a los usuarios de Platform ventajas como replicación de regiones geográficas, controles de acceso basados en funciones más precisos (RBAC) y una mejor escala.

## Impacto del usuario

Mientras el Adobe migra el lago de datos de Gen1 a Gen 2, los usuarios podrán **leer** del lago de datos, pero todas las funcionalidades que **escribir** en el lago de datos se verá afectado. A continuación se muestra una lista de las capacidades afectadas:

- **Fuentes**: Se retrasarán los datos que llegan desde las fuentes y varios flujos de trabajo de ingesta de datos. Los usuarios verán sus datos una vez que se haya completado la migración.
- **Servicio de consultas**: los usuarios pueden realizar consultas, pero no podrán escribir el resultado de la consulta en un conjunto de datos.
- **Perfil del cliente en tiempo real**: datos introducidos en el almacén de perfiles mediante **lote** la ingesta no estará disponible durante la migración. Sin embargo, los datos introducidos mediante **transmisión** la ingesta estará disponible durante la migración. Además, las exportaciones de perfiles no estarán disponibles durante la migración.
- **Data Science Workspace**: las escrituras desde Data Science Workspace fallarán.
- **Servicio de segmentación**: audiencias derivadas de **lote** la segmentación no se puede activar durante la migración. Audiencias derivadas de **transmisión** la segmentación no se verá afectada.
- **Customer Journey Analytics**: los datos de los informes del Customer Journey Analytics pueden estar desactualizados y no se actualizarán durante la migración, ya que los lotes no se están ingiriendo en el lago de datos.

## Comunicación a los usuarios de Platform

El Adobe se pondrá en contacto con los administradores del sistema para analizar en detalle el impacto de la migración y para confirmar las fechas y horas de migración de organizaciones de IMS específicas.
