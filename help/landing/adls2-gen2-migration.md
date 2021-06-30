---
title: Migración del lago de datos a Gen2
description: Obtenga información sobre las nuevas funciones que proporciona la migración de Data Lake a Gen2 en Adobe Experience Platform.
exl-id: 56d9c77a-d7eb-498d-994f-b15d150dedb7
source-git-commit: 97f803f649b2c42b0449a2f8f0cff370ed1aba93
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# Migración de Data Lake de Adobe Experience Platform a Gen2

Adobe Experience Platform está migrando al lago de datos Gen2. Se trata de una nueva generación de lago de datos que proporciona a los usuarios de Platform beneficios como replicación geográfica, controles de acceso basados en roles (RBAC) más precisos y una mejor escala.

## Impacto del usuario

Mientras que el Adobe está migrando el lago de datos de Gen1 a Gen 2, los usuarios podrán **leer** desde el lago de datos, pero todas las funcionalidades que **escribir** en el lago de datos se verán afectadas. A continuación se muestra una lista de las capacidades afectadas:

- **Fuentes**: Se retrasarán los datos procedentes de los orígenes y de varios flujos de trabajo de consumo de datos. Los usuarios verán sus datos una vez completada la migración.
- **Servicio** de consultas: Los usuarios pueden realizar consultas, pero no podrán escribir el resultado de la consulta en un conjunto de datos.
- **Perfil** del cliente en tiempo real: Los datos introducidos en el Almacenamiento de perfiles mediante  **** lotes no estarán disponibles durante la migración. Sin embargo, los datos introducidos mediante la ingesta de **streaming** estarán disponibles durante la migración. Además, las exportaciones de perfil no estarán disponibles durante la migración.
- **Data Science Workspace**: Las escrituras de Data Science Workspace fallarán.
- **Servicio** de segmentación: Las audiencias derivadas de la segmentación por  **** lotes no se pueden activar durante la migración. Las audiencias derivadas de la segmentación **streaming** no se verán afectadas.
- **Customer Journey Analytics**: Los datos de los informes de Customer Journey Analytics pueden estar desactualizados y no se actualizarán durante la migración, ya que los lotes no se incorporan en Data Lake.

## Comunicación con los usuarios de la plataforma

El Adobe se pondrá en contacto con los administradores del sistema para analizar en detalle el impacto de la migración y confirmar las fechas y horas de migración para organizaciones específicas de IMS.
