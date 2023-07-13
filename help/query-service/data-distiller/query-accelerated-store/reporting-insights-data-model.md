---
title: Guía de información de Query Accelerated Store Reporting
description: Obtenga información sobre cómo crear un modelo de datos de perspectivas de creación de informes a través del servicio de consultas para utilizarlo con datos de almacenamiento acelerados y paneles definidos por el usuario.
exl-id: 216d76a3-9ea3-43d3-ab6f-23d561831048
source-git-commit: e59def7a05862ad880d0b6ada13b1c69c655ff90
workflow-type: tm+mt
source-wordcount: '1033'
ht-degree: 0%

---

# Consultar guía de perspectivas de informes de tienda acelerados

El almacén acelerado de consultas le permite reducir el tiempo y la potencia de procesamiento necesarios para obtener perspectivas críticas de sus datos. Normalmente, los datos se procesan a intervalos regulares (por ejemplo, por hora o por día), donde se crean vistas agregadas y se crean informes sobre ellas. El análisis de estos informes generados a partir de los datos agregados deriva perspectivas destinadas a mejorar el rendimiento empresarial. El almacén acelerado de consultas proporciona un servicio de caché, concurrencia, una experiencia interactiva y una API sin estado. Sin embargo, supone que los datos están preprocesados y optimizados para consultas agregadas y no para consultas de datos sin procesar.

El almacén acelerado de consultas le permite crear un modelo de datos personalizado o ampliar un modelo de datos de Adobe Real-time Customer Data Platform existente. A continuación, puede interactuar con sus perspectivas de creación de informes o incrustarlas en un marco de creación de informes o visualización de su elección. Consulte la documentación del modelo de datos de Real-time Customer Data Platform Insights para obtener información sobre cómo [personalice las plantillas de consulta SQL para crear informes de Real-Time CDP para los casos de uso de los indicadores clave de rendimiento (KPI) y marketing](../../../dashboards/cdp-insights-data-model.md).

El modelo de datos de Real-Time CDP de Adobe Experience Platform proporciona perspectivas sobre perfiles, audiencias y destinos y habilita los paneles de perspectivas de Real-Time CDP. Este documento le guía a través del proceso de creación del modelo de datos de perspectivas de creación de informes y también cómo ampliar los modelos de datos de Real-Time CDP según sea necesario.

## Requisitos previos

Este tutorial utiliza paneles definidos por el usuario para visualizar datos del modelo de datos personalizado en la interfaz de usuario de Platform. Consulte la [documentación de paneles definidos por el usuario](../../../dashboards/user-defined-dashboards.md) para obtener más información sobre esta función.

## Primeros pasos

El SKU de Data Distiller es necesario para crear un modelo de datos personalizado para las perspectivas de creación de informes y ampliar los modelos de datos de Real-Time CDP que contienen datos de Platform enriquecidos. Consulte la [empaquetado](../../packages.md) y [barandas](../../guardrails.md#query-accelerated-store) la documentación relacionada con el SKU de Data Distiller. Si no tiene el SKU de Distiller de datos, póngase en contacto con el representante del servicio de atención al cliente de Adobe para obtener más información.

<!-- Document is hidden temporarily
Please see the [packaging](../../packages.md), [guardrails](../../guardrails.md#query-accelerated-store), and [licensing](../../data-distiller/license-usage.md) documentation that relates to the Data Distiller SKU. 
-->

## Creación de un modelo de datos de perspectivas de informes

Este tutorial utiliza un ejemplo de creación de un modelo de datos de perspectiva de audiencia. Si utiliza una o más plataformas de anunciante para llegar a su audiencia, puede utilizar la API del anunciante para obtener un recuento aproximado de coincidencias de su audiencia.

Al principio, tiene un modelo de datos inicial de sus fuentes (potencialmente de su API de plataforma de anunciante). Para crear una vista agregada de los datos sin procesar, cree un modelo de perspectivas de creación de informes como se describe en la siguiente imagen. Esto permite que un conjunto de datos obtenga los límites superior e inferior de la coincidencia de audiencia.

![Un diagrama relacional de entidades (ERD) del modelo de usuario de Audience Insight.](../../images/query-accelerated-store/audience-insight-user-model.png)

En este ejemplo, la variable `externalaudiencereach` La tabla o el conjunto de datos se basa en un ID y rastrea los límites inferior y superior para el recuento de coincidencias. El `externalaudiencemapping` La tabla/conjunto de datos de dimensión asigna el ID externo a un destino y a una audiencia en Platform.

## Creación de un modelo para informar sobre perspectivas con Data Distiller

A continuación, cree un modelo de perspectiva de informes (`audienceinsight` en este ejemplo) y utilice el comando SQL `ACCOUNT=acp_query_batch and TYPE=QSACCEL` para asegurarse de que se crea en el almacén acelerado. A continuación, utilice el servicio de consultas para crear una `audienceinsight.audiencemodel` esquema para `audienceinsight` base de datos.

>[!NOTE]
>
>Se requiere el SKU de Distiller de datos para la `ACCOUNT=acp_query_batch` comando. Sin él, se crea un modelo de datos normal en el lago de datos.

```sql
CREATE database audienceinsight WITH (TYPE=QSACCEL, ACCOUNT=acp_query_batch);
 
CREATE schema audienceinsight.audiencemodel;
```

## Crear tablas, relaciones y rellenar datos

Ahora que ha creado su `audienceinsight` modelo de perspectiva de informes, cree el `externalaudiencereach` y `externalaudiencemapping` y establecer relaciones entre ellas. A continuación, utilice el `ALTER TABLE` para agregar una restricción FOREIGN KEY entre las tablas y definir una relación. El siguiente ejemplo de SQL muestra cómo hacerlo.

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
SELECT cast(null as int) audience_id,
       cast(null as int) destination_id,
       cast(null as int) ext_custom_audience_id
 WHERE false;
 
ALTER TABLE externalaudiencereach ADD  CONSTRAINT FOREIGN KEY (ext_custom_audience_id) REFERENCES externalaudiencemapping (ext_custom_audience_id) NOT enforced;
```

Después de la ejecución correcta de ambos `ALTER TABLE` comandos, se forma la relación entre las tablas hecho y dimensión.

Una vez ejecutadas las instrucciones, utilice el `SHOW datagroups;` para devolver una lista de los conjuntos de datos disponibles en el almacén acelerado desde el `audienceinsight.audiencemodel`. Los resultados tabulados deben ser similares al ejemplo que se proporciona a continuación.

>[!IMPORTANT]
>
>Solo se puede acceder a los datos del almacén acelerado desde el extremo de API sin estado del servicio de consultas `POST /data/foundation/query/accelerated-queries`.

```console
    Database     |    Schema     | GroupType |      ChildType       |        ChildName        | PhysicalParent |               ChildId               
-----------------+---------------+-----------+----------------------+-------------------------+----------------+--------------------------------------
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | externalaudiencemapping | true           | 9155d3b4-889d-41da-9014-5b174f6fa572
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | externalaudiencereach   | true           | 1b941a6d-6214-4810-815c-81c497a0b636
```

## Consultar el modelo de datos de perspectiva de informes

Utilice el servicio de consultas para consultar `audiencemodel.externalaudiencereach` tabla de dimensiones. A continuación se muestra un ejemplo de consulta.

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

Puede ampliar el modelo de audiencia con detalles adicionales para crear una tabla de dimensiones más completa. Por ejemplo, puede asignar el nombre de audiencia y el nombre de destino al identificador de audiencia externo. Para ello, utilice el servicio de consulta para crear o actualizar un nuevo conjunto de datos y añadirlo al modelo de audiencia que combina audiencias y destinos con una identidad externa. El diagrama siguiente ilustra el concepto de esta extensión del modelo de datos.

![Diagrama de ERD que vincula el modelo de datos de Real-Time CDP insight y el modelo de almacén acelerado de consultas.](../../images/query-accelerated-store/updatingAudienceInsightUserModel.png)

## Creación de tablas de dimensiones para ampliar el modelo de perspectivas de informes

Utilice el servicio de consultas para agregar atributos descriptivos clave de los conjuntos de datos de dimensión de Real-Time CDP enriquecidos a `audienceinsight` Modelo de datos de y establezca una relación entre la tabla de hechos y la nueva tabla de dimensiones. El SQL siguiente muestra cómo integrar tablas de dimensiones existentes en el modelo de datos de perspectivas de creación de informes.

```sql
CREATE TABLE audienceinsight.audiencemodel.external_seg_dest_map AS
  SELECT ext_custom_audience_id,
         destination_name,
         audience_name,
         destination_status,
         a.destination_id,
         a.audience_id
  FROM   externalaudiencemapping AS a
         LEFT OUTER JOIN adwh_dim_audiences AS b
                      ON ( ( a.audience_id ) = ( b.audience_id ) )
         LEFT OUTER JOIN adwh_dim_destination AS c
                      ON ( ( a.destination_id ) = ( c.destination_id ) );
 
ALTER TABLE externalaudiencereach  ADD  CONSTRAINT FOREIGN KEY (ext_custom_audience_id) REFERENCES external_seg_dest_map (ext_custom_audience_id) NOT enforced;
```

Utilice el `SHOW datagroups;` para confirmar la creación del comando adicional `external_seg_dest_map` tabla de dimensiones.

```console
    Database     |     Schema     | GroupType |      ChildType       |                ChildName  | PhysicalParent |               ChildId               
-----------------+----------------+-----------+----------------------+----------------------------------------------------+----------------+--------------------------------------
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | external_seg_dest_map      | true           | 4b4b86b7-2db7-48ee-a67e-4b28cb900810
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | externalaudiencemapping    | true           | b0302c05-28c3-488b-a048-1c635d88dca9
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | externalaudiencereach      | true           | 4485c610-7424-4ed6-8317-eed0991b9727
```

## Consulte el modelo de datos de perspectivas de informes de tienda acelerados extendidos

Ahora que la variable `audienceinsight` El modelo de datos de se ha aumentado, está listo para consultarse. El siguiente SQL muestra la lista de destinos y audiencias asignados.

```sql
SELECT a.ext_custom_audience_id,
       b.destination_name,
       b.audience_name,
       b.destination_status,
       b.destination_id,
       b.audience_id
FROM   audiencemodel.externalaudiencereach1 AS a
       LEFT OUTER JOIN audiencemodel.external_seg_dest_map AS b
                    ON ( ( a.ext_custom_audience_id ) = (
                         b.ext_custom_audience_id ) )
LIMIT  25; 
```

La consulta devuelve todos los conjuntos de datos del almacén acelerado de consultas:

```console
ext_custom_audience_id | destination_name |       audience_name        | destination_status | destination_id | audience_id 
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

## Visualice los datos con paneles definidos por el usuario

Ahora que ha creado su modelo de datos personalizado, está listo para visualizar los datos con consultas personalizadas y paneles definidos por el usuario.

El siguiente SQL proporciona un desglose del recuento de coincidencias por audiencias en un destino y un desglose de cada destino de audiencias por audiencia.

```sql
SELECT b.destination_name,
       a.approximate_count_upper_bound,
       b.audience_name
FROM   audiencemodel.externalaudiencereach AS a
       LEFT OUTER JOIN audiencemodel.external_seg_dest_map AS b
                    ON ( ( a.ext_custom_audience_id ) = (
                         b.ext_custom_audience_id ) )
GROUP  BY b.destination_name,
          a.approximate_count_upper_bound,
          b.audience_name
ORDER BY b.destination_name
LIMIT  5000
```

La siguiente imagen proporciona un ejemplo de las posibles visualizaciones personalizadas que se pueden usar con el modelo de datos de perspectivas de creación de informes.

![Un recuento de coincidencias por destino y widget de audiencia creado a partir del nuevo modelo de datos de perspectivas de informes.](../../images/query-accelerated-store/user-defined-dashboard-widget.png)

El modelo de datos personalizado se encuentra en la lista de modelos de datos disponibles en el espacio de trabajo del panel definido por el usuario. Consulte la [guía de panel definida por el usuario](../../../dashboards/user-defined-dashboards.md) para obtener instrucciones sobre cómo utilizar el modelo de datos personalizado.
