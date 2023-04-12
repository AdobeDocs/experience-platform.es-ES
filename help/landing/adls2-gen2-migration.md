---
title: Migración del lago de datos a Gen2
description: Obtenga información sobre las nuevas funciones que proporciona la migración de Data Lake a Gen2 en Adobe Experience Platform.
exl-id: 56d9c77a-d7eb-498d-994f-b15d150dedb7
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---

# Migración de Data Lake de Adobe Experience Platform a Gen2

Adobe Experience Platform está migrando al lago de datos Gen2. Se trata de una nueva generación de lago de datos que proporciona a los usuarios de Platform beneficios como replicación geográfica, controles de acceso basados en roles (RBAC) más precisos y una mejor escala.

## Impacto del usuario

Mientras el Adobe esté migrando el lago de datos de Gen1 a Gen 2, los usuarios podrán **read** del lago de datos, pero todas las capacidades que **write** en el lago de datos se verá afectado. A continuación se muestra una lista de las capacidades afectadas:

- **Fuentes**: Se retrasarán los datos procedentes de los orígenes y de varios flujos de trabajo de consumo de datos. Los usuarios verán sus datos una vez completada la migración.
- **Servicio de consultas**: Los usuarios pueden realizar consultas, pero no podrán escribir el resultado de la consulta en un conjunto de datos.
- **Perfil del cliente en tiempo real**: Datos introducidos en el almacén de perfiles mediante **batch** La ingesta no estará disponible durante la migración. Sin embargo, los datos introducidos mediante **streaming** La ingesta estará disponible durante la migración. Además, las exportaciones de perfil no estarán disponibles durante la migración.
- **Data Science Workspace**: Las escrituras de Data Science Workspace fallarán.
- **Servicio de segmentación**: Audiencias derivadas de **batch** no se puede activar la segmentación durante la migración. Audiencias derivadas de **streaming** la segmentación no se verá afectada.
- **Customer Journey Analytics**: Los datos de los informes de Customer Journey Analytics pueden estar desactualizados y no se actualizarán durante la migración, ya que los lotes no se incorporan en Data Lake.

## Comunicación con los usuarios de la plataforma

El Adobe se pondrá en contacto con los administradores del sistema para analizar en detalle el impacto de la migración y confirmar las fechas y horas de migración de organizaciones específicas.
