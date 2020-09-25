---
source-git-commit: b9816767556b9d50cf2ff5268816d1de6b85fc63
workflow-type: tm+mt
translation-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---
# Migración de Data Lake de Adobe Experience Platform a Gen2

Adobe Experience Platform está migrando a Gen2 Data Lake. Esta es una nueva generación de laca de datos que proporciona a los usuarios de la Plataforma beneficios como replicación geográfica, controles de acceso basados en roles (RBAC) más precisos y una mejor escala.

## Impacto del usuario

Mientras que Adobe está migrando el Data Lake de Gen1 a Gen 2, los usuarios podrán **leer** desde Data Lake, pero todas las capacidades que **escriben** en Data Lake se verán afectadas. A continuación se muestra una lista de las capacidades afectadas:

- **Fuentes**: Los datos provenientes de las fuentes y de diversos flujos de trabajo de ingestión de datos se retrasarán. Los usuarios verán sus datos una vez que se complete la migración.
- **Servicio** de consulta: Los usuarios pueden realizar consultas pero no podrán escribir el resultado de la consulta en un conjunto de datos.
- **Perfil** del cliente en tiempo real: Durante la migración no estarán disponibles los datos ingeridos en el almacén de Perfiles mediante **ingestión por lotes** . Sin embargo, durante la migración estarán disponibles los datos ingestados mediante **transmisión** por secuencias. Además, las exportaciones de Perfiles no estarán disponibles durante la migración.
- **Área de trabajo** de ciencias de datos: Las escrituras de Data Science Workspace fallarán.
- **Servicio** de segmentación: Las audiencias derivadas de la segmentación por **lotes** no se pueden activar durante la migración. No se verán afectadas las audiencias derivadas de la segmentación de **flujo continuo** .
- **Customer Journey Analytics**: Es posible que los datos de los informes de Customer Journey Analytics estén desactualizados y no se actualicen durante la migración, ya que los lotes no se están ingeriendo en Data Lake.

## Comunicación a los usuarios de la plataforma

El Adobe se pondrá en contacto con los administradores del sistema para analizar en detalle el impacto de la migración y confirmar las fechas y horas de migración para las organizaciones de IMS específicas.