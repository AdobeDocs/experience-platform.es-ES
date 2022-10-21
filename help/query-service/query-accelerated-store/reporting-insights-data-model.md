---
title: Consulta de Perspectivas de Informes de Almacenamiento Acelerado
description: Obtenga información sobre cómo crear un modelo de datos de perspectivas de informes mediante el servicio de consulta para utilizarlo con datos de almacenamiento acelerados y paneles definidos por el usuario.
source-git-commit: 16ae8a16d8c4f7ec68a054e8d15a518f453a05c7
workflow-type: tm+mt
source-wordcount: '1031'
ht-degree: 0%

---

# Consulta de perspectivas de informes de almacén acelerado

El almacén acelerado de consultas le permite reducir el tiempo y la potencia de procesamiento necesarios para obtener perspectivas críticas de sus datos. Normalmente, los datos se procesan a intervalos regulares (por ejemplo, cada hora o cada día) en los que se crean y generan informes sobre vistas agregadas. El análisis de estos informes generado a partir de los datos agregados deriva perspectivas que pretenden mejorar el rendimiento del negocio. El almacén acelerado de consultas proporciona un servicio de caché, concurrencia, una experiencia interactiva y una API sin estado. Sin embargo, supone que los datos se preprocesan y optimizan para consultas agregadas y no para consultas de datos sin procesar.

El almacén acelerado de consultas le permite crear un modelo de datos personalizado o ampliar modelos de datos de Real-time Customer Data Platform existentes. A continuación, puede interactuar con o incrustar sus perspectivas de informes en un marco de informes/visualización de su elección. Consulte la documentación del modelo de datos de Real-time Customer Data Platform Insights para obtener información sobre cómo [personalice las plantillas de consulta SQL para crear informes de Real-Time CDP para los casos de uso de los indicadores clave de rendimiento (KPI) y marketing](../../dashboards/cdp-insights-data-model.md).

El modelo de datos de Real-Time CDP de Adobe Experience Platform proporciona perspectivas sobre perfiles, segmentos y destinos, y permite los paneles de perspectiva de Real-Time CDP. Este documento le guía a través del proceso de creación del modelo de datos de perspectivas de informes y también sobre cómo ampliar los modelos de datos de Real-Time CDP según sea necesario.

## Requisitos previos

Este tutorial utiliza tableros definidos por el usuario para visualizar datos de su modelo de datos personalizado dentro de la interfaz de usuario de Platform. Consulte la [documentación de paneles definidos por el usuario](../../dashboards/user-defined-dashboards.md) para obtener más información sobre esta función.

## Primeros pasos

El SKU de Distiller de datos es necesario para crear un modelo de datos personalizado para la información de informes y para ampliar los modelos de datos de Real-Time CDP que contienen datos de Platform enriquecidos. Consulte la [embalaje](../packages.md), [guardrails](../guardrails.md#query-accelerated-store)y [licencias](../data-distiller/licence-usage.md) documentación relacionada con el SKU de Distiller de datos. Si no tiene el SKU de Distiller de datos, póngase en contacto con su representante del servicio al cliente de Adobe para obtener más información.

## Creación de un modelo de datos de perspectivas de informes

Este tutorial utiliza un ejemplo de creación de un modelo de datos de perspectiva de audiencia. Si utiliza una o varias plataformas de anunciantes para llegar a la audiencia, puede utilizar la API del anunciante para obtener un recuento aproximado de coincidencias de la audiencia.

Al principio, tiene un modelo de datos inicial de sus fuentes (potencialmente de su API de plataforma de anunciante). Para obtener una vista agregada de los datos sin procesar, cree un modelo de perspectivas de informes como se describe en la imagen siguiente. Esto permite que un conjunto de datos obtenga los límites superior e inferior de la coincidencia de audiencia.

![Diagrama relacional de entidad (ERD) del modelo de usuario de perspectiva de audiencia.](../images/query-accelerated-store/audience-insight-user-model.png)

En este ejemplo, la variable `externalaudiencereach` la tabla/conjunto de datos se basa en un ID y rastrea los límites inferior y superior del recuento de coincidencias. La variable `externalaudiencemapping` tabla de dimensiones/conjunto de datos asigna el ID externo a un destino y un segmento en Platform.

## Creación de un modelo para generar informes de perspectivas con Data Distiller

A continuación, cree un modelo de perspectiva de informes (`audienceinsight` en este ejemplo) y utilice el comando SQL `ACCOUNT=acp_query_batch and TYPE=QSACCEL` para asegurarse de que se crea en el almacén acelerado. A continuación, utilice el servicio de consulta para crear un `audienceinsight.audiencemodel` esquema para la variable `audienceinsight` base de datos.

>[!NOTE]
>
>El SKU de Distiller de datos es necesario para la variable `ACCOUNT=acp_query_batch` comando. Sin él, se crea un modelo de datos normal en el lago de datos.

```sql
CREATE database audienceinsight WITH (TYPE=QSACCEL, ACCOUNT=acp_query_batch);
 
CREATE schema audienceinsight.audiencemodel;
```

## Crear tablas, relaciones y rellenar datos

Ahora que ha creado su `audienceinsight` modelo de perspectiva de informes, cree la variable `externalaudiencereach` y `externalaudiencemapping` y establecer relaciones entre ellas. A continuación, utilice el `ALTER TABLE` para añadir una restricción de clave externa entre las tablas y definir una relación. El siguiente ejemplo SQL muestra cómo hacerlo.

```sql
CREATE TABLE IF NOT exists audienceinsight.audiencemodel.externalaudiencereach
WITH ( DISTRIBUTION = REPLICATE ) AS
  SELECT cast(null as int) approximate_count_upper_bound,
         cast(null as string) deliverystatusdescription,
         cast(null as timestamp)  timeupdated ,
         cast(null as int) operationstatuscode ,
         cast(null as string) operationstatusdescription,
         cast(null as int) approximate_count_lower_bound,
         cast(null as timestamp)timecreated ,
         cast(null as timestamp)timecontentupdated ,
         cast(null as int) deliverystatuscode ,
         cast(null as int)  ext_custom_audience_id
   WHERE false;
 
CREATE TABLE IF NOT exists audienceinsight.audiencemodel.externalaudiencemapping
WITH ( DISTRIBUTION = REPLICATE ) AS
SELECT cast(null as int) segment_id,
       cast(null as int) destination_id,
       cast(null as int) ext_custom_audience_id
 WHERE false;
 
ALTER TABLE externalaudiencereach ADD  CONSTRAINT FOREIGN KEY (ext_custom_audience_id) REFERENCES externalaudiencemapping (ext_custom_audience_id) NOT enforced;
```

Después de la ejecución correcta de ambos `ALTER TABLE` , se forma la relación entre las tablas de hechos y dimensiones.

Una vez ejecutadas las instrucciones, utilice la variable `SHOW datagroups;` para devolver una lista de los conjuntos de datos disponibles en el almacén acelerado desde el `audienceinsight.audiencemodel`. Los resultados tabulados deben ser similares al ejemplo que se proporciona a continuación.

>[!IMPORTANT]
>
>Solo se puede acceder a los datos del almacén acelerado desde el extremo de API sin estado del servicio de consulta `POST /data/foundation/query/accelerated-queries`.

```console
    Database     |    Schema     | GroupType |      ChildType       |        ChildName        | PhysicalParent |               ChildId               
-----------------+---------------+-----------+----------------------+-------------------------+----------------+--------------------------------------
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | externalaudiencemapping | true           | 9155d3b4-889d-41da-9014-5b174f6fa572
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | externalaudiencereach   | true           | 1b941a6d-6214-4810-815c-81c497a0b636
```

## Consultar el modelo de datos de perspectivas de informes

Utilice el servicio de consulta para consultar la `audiencemodel.externalaudiencereach` tabla de dimensiones. A continuación se puede ver un ejemplo de consulta.

```sql
SELECT a.ext_custom_audience_id,
       a.approximate_count_upper_bound
FROM   audiencemodel.externalaudiencereach AS a
       LEFT OUTER JOIN audiencemodel.externalaudiencemapping AS b
                    ON ( ( a.ext_custom_audience_id ) =
                         ( b.ext_custom_audience_id ) )
GROUP  BY a.ext_custom_audience_id,
          a.approximate_count_upper_bound
LIMIT  5000 ;
```

Los resultados tabulados incluyen un recuento y un ID.

```console
ext_custom_audience_id | approximate_count_upper_bound
------------------------+-------------------------------
 23850912218170554      |                          1000
 23850808585120554      |                       1012000
 23850808585220554      |                        100000
 23850814978560554      |                          1000
 23850808585180554      |                        421000
 23850814978510554      |                       3001000
 23850814978530554      |                        300000
 23850912218160554      |                        105000
 23850808584990554      |                          1000
 23850809520110554      |                          1000
(10 rows)
```

## Ampliación del modelo de datos con el modelo de datos de perspectivas de Real-Time CDP

Puede ampliar el modelo de audiencia con detalles adicionales para crear una tabla de dimensiones más rica. Por ejemplo, puede asignar el nombre del segmento y el nombre de destino al identificador de audiencia externo. Para ello, utilice el servicio de consulta para crear o actualizar un nuevo conjunto de datos y añadirlo al modelo de audiencia que combina segmentos y destinos con una identidad externa. El diagrama siguiente ilustra el concepto de esta extensión del modelo de datos.

![Diagrama ERD que vincula el modelo de datos de Real-Time CDP Insight y el modelo de almacén acelerado Query.](../images/query-accelerated-store/updatingAudienceInsightUserModel.png)

## Crear tablas de dimensión para ampliar el modelo de perspectivas de informes

Utilice el servicio de consulta para agregar atributos descriptivos clave de los conjuntos de datos de dimensiones enriquecidos de Real-Time CDP al `audienceinsight` modelo de datos y establezca una relación entre la tabla de hechos y la nueva tabla de dimensiones. El SQL siguiente muestra cómo integrar las tablas de dimensión existentes en el modelo de datos de perspectivas de informes.

```sql
CREATE TABLE audienceinsight.audiencemodel.external_seg_dest_map AS
  SELECT ext_custom_audience_id,
         destination_name,
         segment_name,
         destination_status,
         a.destination_id,
         a.segment_id
  FROM   externalaudiencemapping AS a
         LEFT OUTER JOIN adwh_dim_segments AS b
                      ON ( ( a.segment_id ) = ( b.segment_id ) )
         LEFT OUTER JOIN adwh_dim_destination AS c
                      ON ( ( a.destination_id ) = ( c.destination_id ) );
 
ALTER TABLE externalaudiencereach  ADD  CONSTRAINT FOREIGN KEY (ext_custom_audience_id) REFERENCES external_seg_dest_map (ext_custom_audience_id) NOT enforced;
```

Utilice la variable `SHOW datagroups;` para confirmar la creación del `external_seg_dest_map` tabla de dimensiones.

```console
    Database     |     Schema     | GroupType |      ChildType       |                ChildName  | PhysicalParent |               ChildId               
-----------------+----------------+-----------+----------------------+----------------------------------------------------+----------------+--------------------------------------
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | external_seg_dest_map      | true           | 4b4b86b7-2db7-48ee-a67e-4b28cb900810
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | externalaudiencemapping    | true           | b0302c05-28c3-488b-a048-1c635d88dca9
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | externalaudiencereach      | true           | 4485c610-7424-4ed6-8317-eed0991b9727
```

## Consulte el modelo de datos de perspectivas del almacén acelerado ampliado

Ahora que la variable `audienceinsight` el modelo de datos se ha ampliado, está listo para ser consultado. El siguiente SQL muestra la lista de destinos y segmentos asignados.

```sql
SELECT a.ext_custom_audience_id,
       b.destination_name,
       b.segment_name,
       b.destination_status,
       b.destination_id,
       b.segment_id
FROM   audiencemodel.externalaudiencereach1 AS a
       LEFT OUTER JOIN audiencemodel.external_seg_dest_map AS b
                    ON ( ( a.ext_custom_audience_id ) = (
                         b.ext_custom_audience_id ) )
LIMIT  25; 
```

La consulta devuelve todos los conjuntos de datos del almacén acelerado de consultas:

```console
ext_custom_audience_id | destination_name |       segment_name        | destination_status | destination_id | segment_id 
------------------------+------------------+---------------------------+--------------------+----------------+-------------
 23850808595110554      | FCA_Test2        | United States             | enabled            |     -605911558 | -1357046572
 23850799115800554      | FCA_Test2        | Born in 1980s             | enabled            |     -605911558 | -1224554872
 23850799115790554      | FCA_Test2        | Born in 1970s             | enabled            |     -605911558 |  1899603869
 23850798177620554      | FCA_Test1        | Billionaires              | enabled            |      321720439 |  1401872665
 23850814978560554      | FCA_Test3        | Canada - Saskatchewan     | enabled            |     1182494936 | -1917996562
 23850808585180554      | FCA_Test3        | United States             | enabled            |     1182494936 | -1357046572
 23850814978530554      | FCA_Test3        | Canada - British Columbia | enabled            |     1182494936 |  -652840507
 23850808585120554      | FCA_Test3        | Canada - Quebec           | enabled            |     1182494936 |  -519557860
 23850809520110554      | FCA_Test3        | Born in 1960s             | enabled            |     1182494936 |   237824266
 23850808585220554      | FCA_Test3        | Western Canada            | enabled            |     1182494936 |  1075937528
 23850808584990554      | FCA_Test3        | Canada - Ontario          | enabled            |     1182494936 |  1593438041
 23850814978510554      | FCA_Test3        | Canada - Alberta          | enabled            |     1182494936 |  1862946783
 23850912218170554      | FCA_Test4        | Canada - Alberta          | enabled            |     1549248886 |  1862946783
 23850912218160554      | FCA_Test4        | Born in 1970s             | enabled            |     1549248886 |  1899603869
```

## Visualizar los datos con tableros definidos por el usuario

Ahora que ha creado su modelo de datos personalizado, ya puede visualizar los datos con consultas personalizadas y tableros definidos por el usuario.

El siguiente SQL proporciona un desglose del recuento de coincidencias por audiencias en un destino y un desglose de cada destino de audiencias por segmento.

```sql
SELECT b.destination_name,
       a.approximate_count_upper_bound,
       b.segment_name
FROM   audiencemodel.externalaudiencereach AS a
       LEFT OUTER JOIN audiencemodel.external_seg_dest_map AS b
                    ON ( ( a.ext_custom_audience_id ) = (
                         b.ext_custom_audience_id ) )
GROUP  BY b.destination_name,
          a.approximate_count_upper_bound,
          b.segment_name
ORDER BY b.destination_name
LIMIT  5000
```

La siguiente imagen proporciona un ejemplo de las posibles visualizaciones personalizadas que utilizan su modelo de datos de perspectivas de informes.

![Recuento de coincidencias por destino y widget de segmento creado a partir del nuevo modelo de datos de perspectivas de informes.](../images/query-accelerated-store/user-defined-dashboard-widget.png)

El modelo de datos personalizado se encuentra en la lista de modelos de datos disponibles en el espacio de trabajo del tablero definido por el usuario. Consulte la [guía de tablero definida por el usuario](../../dashboards/user-defined-dashboards.md) para obtener instrucciones sobre cómo utilizar el modelo de datos personalizado.
