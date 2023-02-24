---
title: Flujo SQL sin problemas para atributos derivados
description: SQL del servicio de consulta se ha ampliado para proporcionar compatibilidad perfecta con atributos derivados. Obtenga información sobre cómo utilizar esta extensión SQL para crear un atributo derivado habilitado para perfil y cómo utilizar el atributo para Perfil del cliente en tiempo real y Servicio de segmentación.
source-git-commit: 1ff66d0ac8e0491a6db518545d122555d9d54c75
workflow-type: tm+mt
source-wordcount: '1192'
ht-degree: 1%

---

# Flujo SQL perfecto para atributos derivados

SQL del servicio de consulta se ha ampliado para proporcionar compatibilidad perfecta con atributos derivados. Esto proporciona un método alternativo eficiente para crear atributos derivados para los casos de uso comercial del Perfil del cliente en tiempo real.

Este documento describe varias extensiones SQL prácticas que generan un atributo derivado para su uso con el Perfil del cliente en tiempo real. El flujo de trabajo simplifica el proceso que, de lo contrario, tendría que completar mediante varias llamadas de API o interacciones de la interfaz de usuario de Platform.

Normalmente, la generación y publicación de un atributo para el perfil del cliente en tiempo real implicaría los siguientes pasos:

* Cree un área de nombres de identidad, si todavía no existe.
* Cree el tipo de datos para almacenar el atributo derivado, si es necesario.
* Cree un grupo de campos con ese tipo de datos para almacenar la información de atributo derivada.
* Cree o asigne una columna de identidad principal con el espacio de nombres creado anteriormente.
* Cree un esquema utilizando el grupo de campos y el tipo de datos creados anteriormente.
* Cree un nuevo conjunto de datos con su esquema y actívelo para el perfil, si es necesario.
* De forma opcional, marque un conjunto de datos como habilitado para perfiles.

Después de completar los pasos mencionados anteriormente, está listo para rellenar el conjunto de datos. Si habilitó el conjunto de datos para el perfil, también puede crear segmentos que hagan referencia al nuevo atributo y comenzar a producir perspectivas.

El servicio de consulta le permite realizar todas las acciones enumeradas anteriormente mediante consultas SQL. Esto incluye realizar cambios en los conjuntos de datos y grupos de campos si es necesario.

## Crear una tabla con una opción para habilitarla para el perfil {#enable-dataset-for-profile}

>[!NOTE]
>
>La consulta SQL que se proporciona a continuación supone el uso de un área de nombres preexistente.

Utilice una consulta Crear tabla como Seleccionar (CTAS) para crear un conjunto de datos, asignar tipos de datos, establecer una identidad principal, crear un esquema y marcarlo como perfil habilitado. La instrucción SQL de ejemplo siguiente crea atributos y los hace disponibles para el perfil de datos del cliente en tiempo real (Real-Time CDP). La consulta SQL seguirá el formato que se muestra en el ejemplo siguiente:

```sql
CREATE TABLE <your_table_name> [IF NOT EXISTS] (fieldname <your_data_type> primary identity namespace <your_namespace>, [field_name2 <your_data_type>]) [WITH(LABEL='PROFILE')];
```

Alternativamente, los conjuntos de datos también se pueden habilitar para el perfil a través de la interfaz de usuario de Platform. Para obtener más información sobre cómo marcar un conjunto de datos como habilitado para el perfil, consulte la [habilitar un conjunto de datos para la documentación del perfil del cliente en tiempo real](../../../catalog/datasets/user-guide.md#enable-profile).

En la siguiente consulta de ejemplo, la variable `decile_table` el conjunto de datos se crea con `id` como columna de identidad principal y tiene el área de nombres `IDFA`. También tiene un campo denominado `decile1Month` del tipo de datos de asignación. La tabla creada (`decile_table`) está habilitado para el perfil.

```sql
CREATE TABLE decile_table (id text PRIMARY KEY NAMESPACE 'IDFA', 
            decile1Month map<text, integer>) WITH (label='PROFILE');
```

<!--        decile3Month map<text, integer>,
            decile6Month map<text, integer>,
            decile9month map<text, integer>,
            decile12month map<text, integer>,
            decilelifetime map<text, integer> -->

Al ejecutar correctamente la consulta, se devuelve el ID del conjunto de datos a la consola, como se ve en el ejemplo siguiente.

```console
Created Table DataSet Id
>
637fd84969ba291e62dba79f
(1 row)
```

Uso `label='PROFILE'` en un `CREATE TABLE` para crear un conjunto de datos habilitado para perfiles. La variable `upsert` está activada de forma predeterminada. La variable `upsert` se puede sobrescribir usando la función `ALTER` como se muestra en el ejemplo siguiente.

```sql
ALTER TABLE <your_table_name> DROP label upsert;
```

Consulte la documentación de sintaxis SQl para obtener más información sobre el uso de la variable [MODIFICAR TABLA](../../sql/syntax.md#alter-table) y [etiqueta como parte de una consulta CTAS](../../sql/syntax.md#create-table-as-select).

## Construcciones para ayudar a administrar atributos derivados a través de SQL

Las funciones que se describen a continuación son de bueno beneficio al administrar atributos derivados a través de SQL.

### Cambiar conjuntos de datos existentes para habilitarlos para el perfil {#enable-existing-dataset-for-profile}

La construcción SQL ALTER TABLE se puede usar para hacer que los conjuntos de datos existentes estén habilitados para el perfil. Esto requiere que se añada una etiqueta habilitada para perfil al esquema y al conjunto de datos correspondiente.

```sql
ALTER TABLE your_decile_table ADD label 'PROFILE';
```

>[!NOTE]
>
>Si la ejecución de la variable `ALTER TABLE` devuelve el comando `ALTER SUCCESS`.

### Añadir una identidad principal a un conjunto de datos existente {#add-primary-identity}

Marque una columna existente en un conjunto de datos como conjunto de identidad principal; de lo contrario, se producirá un error. Para establecer una identidad principal mediante SQL, utilice el formato de consulta que se muestra a continuación.

```sql
ALTER TABLE <your_table_name> ADD CONSTRAINT primary identity NAMESPACE
```

Por ejemplo:

```sql
ALTER TABLE test1_dataset ADD CONSTRAINT PRIMARY KEY(id2) NAMESPACE 'IDFA';
```

En el ejemplo proporcionado, `id2` es una columna existente en `test1_dataset`.

### Desactivación de un conjunto de datos para el perfil {#disable-dataset-for-profile}

Si desea deshabilitar la tabla para usos de perfil, debe utilizar el comando DROP. Ejemplo de instrucción SQL que UTILIZA `DROP` a continuación.

```sql
ALTER TABLE table_name DROP LABEL 'PROFILE';
```

Por ejemplo:

```sql
ALTER TABLE decile_table DROP label 'PROFILE';
```

Esta instrucción SQL proporciona un método alternativo eficaz a la utilización de una llamada API. Para obtener más información, consulte la documentación sobre cómo [deshabilitar un conjunto de datos para usar con Real-Time CDP mediante la API de conjuntos de datos](../../../catalog/datasets/enable-upsert.md#disable-the-dataset-for-profile).

### Permitir la actualización e inserción de funcionalidad para su conjunto de datos {#enable-upsert-functionality-for-dataset}

El comando UPSERT permite insertar un nuevo registro o actualizar los datos existentes en una tabla. Específicamente, le permite actualizar una fila existente si ya existe un valor especificado en una tabla o insertar una fila nueva si el valor especificado no existe.

A continuación se muestra un ejemplo que utiliza el formato correcto.

```sql
ALTER TABLE table_name ADD LABEL 'UPSERT';
```

Por ejemplo:

```sql
ALTER TABLE table_with_a_decile ADD label 'UPSERT';
```

Esta instrucción SQL proporciona un método alternativo eficaz a la utilización de una llamada API. Para obtener más información, consulte la documentación sobre cómo [habilitar un conjunto de datos para usar con Real-Time CDP y UPSERT mediante la API de conjuntos de datos](../../../catalog/datasets/enable-upsert.md#enable-the-dataset).

### Deshabilitar la actualización e inserción de funcionalidad para su conjunto de datos {#disable-upsert-functionality-for-dataset}

Este comando deshabilita la capacidad de actualizar e insertar filas en el conjunto de datos.

A continuación se muestra un ejemplo que utiliza el formato correcto.

```sql
ALTER TABLE table_name DROP LABEL 'UPSERT';
```

Por ejemplo:

```sql
ALTER TABLE table_with_a_decile DROP label 'UPSERT';
```

### Mostrar información de tabla adicional asociada a cada tabla {#show-labels-for-tables}

Se conservan metadatos adicionales para conjuntos de datos habilitados para perfiles. Utilice la variable `SHOW TABLES` para mostrar un `labels` que proporciona información sobre cualquier etiqueta asociada a tablas.

A continuación se puede ver un ejemplo de la salida de este comando:

```sql
       name          |        dataSetId         |     dataSet    | description | labels 
---------------------+--------------------------+----------------+-------------+----------
 luma_midvalues      | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues     | 5c86b896b3c162151785b43c | Luma midValues |             | false
 table_with_a_decile | 5c86b896b3c162151785b43c | Luma midValues |             | 'UPSERT', 'PROFILE'
(3 rows)
```

Se puede ver en el ejemplo que `table_with_a_decile` se ha habilitado para el perfil y se ha aplicado con etiquetas como [&#39;UPSERT&#39;](#enable-upsert-functionality-for-dataset), [&#39;PERFIL&#39;](#enable-existing-dataset-for-profile) como se describió anteriormente.

### Creación de un grupo de campos con SQL

Los grupos de campos ahora se pueden crear mediante el uso de SQL. Esto proporciona una alternativa al uso del Editor de esquemas en la interfaz de usuario de Platform o a la realización de una llamada de API al registro de esquemas.

A continuación se puede ver una instrucción de ejemplo para crear un grupo de campos.

```sql
CREATE FIELDGROUP <field_group_name> [IF NOT EXISTS]  (field_name <data_type> primary identity namespace <namespace>, [field_name_2 >data_type>]) [ WITH(LABEL='PROFILE') ];
```

>[!IMPORTANT]
>
>La creación de grupos de campos mediante SQL fallará si se usa la variable `label` no se proporciona el indicador en la instrucción o si el grupo de campos ya existe.
>Asegúrese de que la consulta incluya un `IF NOT EXISTS` para evitar que la consulta falle porque el grupo de campos ya existe.

Un ejemplo real puede aparecer similar al que se ve a continuación.

```sql
CREATE FIELDGROUP field_group_for_test123 (decile1Month map<text, integer>, decile3Month map<text, integer>, decile6Month map<text, integer>, decile9Month map<text, integer>, decile12Month map<text, integer>, decilelietime map<text, integer>) WITH (LABEL-'PROFILE');
```

La ejecución correcta de esta instrucción devuelve el ID del grupo de campos creado. Por ejemplo `c731a1eafdfdecae1683c6dca197c66ed2c2b49ecd3a9525`.

Consulte la documentación sobre cómo [crear un nuevo grupo de campos en el Editor de esquemas](../../../xdm/ui/resources/field-groups.md#create) o utilizando [API de registro de esquema](../../../xdm/api/field-groups.md#create) para obtener más información sobre métodos alternativos.

### Colocación de un grupo de campos

Ocasionalmente puede ser necesario quitar un grupo de campos del Registro de esquemas. Para ello, ejecute el `DROP FIELDGROUP` con la ID del grupo de campos.

```sql
DROP FIELDGROUP [IF EXISTS] <your_field_group_id>;
```

Por ejemplo:

```sql
DROP FIELDGROUP field_group_for_test123;
```

>[!IMPORTANT]
>
>La eliminación de un grupo de campos mediante SQL fallará si el grupo de campos no existe. Asegúrese de que la instrucción incluya un `IF EXISTS` para evitar que la consulta falle.

### Mostrar todos los nombres de los grupos de campos y las ID de las tablas

La variable `SHOW FIELDGROUPS` devuelve una tabla que contiene el nombre, fieldgroupId y el propietario de las tablas.

A continuación se puede ver un ejemplo de la salida de este comando:

```sql
       name                      |        fieldgroupId                             |     owner      |
---------------------------------+-------------------------------------------------+-----------------
 AEP Mobile Lifecycle Details    | _experience.aep-mobile-lifecycle-details        | Luma midValues |
 AEP Web SDK ExperienceEvent     | _experience.aep-web-sdk-experienceevent         | Luma midValues |
 AJO Classification Fields       | _experience.journeyOrchestration.classification | Luma midValues |
 AJO Entity Fields               | _experience.customerJourneyManagement.entities  | Luma midValues |
(4 rows)
```

## Pasos siguientes

Después de leer este documento, tiene una mejor comprensión de cómo usar SQL para crear un perfil y un conjunto de datos habilitado para la actualización basado en atributos derivados. Ya está listo para usar este conjunto de datos con flujos de trabajo de ingesta por lotes para realizar actualizaciones en los datos de perfil. Para obtener más información sobre la ingesta de datos en Adobe Experience Platform, comience por leer la [información general sobre la ingesta de datos](../../../ingestion/home.md).
