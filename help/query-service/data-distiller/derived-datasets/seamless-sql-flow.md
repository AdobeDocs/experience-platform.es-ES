---
title: Flujo SQL fluido para conjuntos de datos derivados
description: Query Service SQL se ha ampliado para proporcionar compatibilidad perfecta con conjuntos de datos derivados. Obtenga información sobre cómo utilizar esta extensión SQL para crear un conjunto de datos derivado que esté habilitado para el perfil y cómo utilizar el conjunto de datos para el perfil del cliente en tiempo real y el servicio de segmentación.
exl-id: bb1a1d8d-4662-40b0-857a-36efb8e78746
source-git-commit: 7364da23c261d83681af605047a7cd7539f4a83f
workflow-type: tm+mt
source-wordcount: '1240'
ht-degree: 1%

---

# Flujo SQL fluido para conjuntos de datos derivados

Query Service SQL se ha ampliado para proporcionar compatibilidad perfecta con conjuntos de datos derivados. Esto proporciona un método alternativo eficaz para crear conjuntos de datos derivados para los casos de uso empresariales del Perfil del cliente en tiempo real.

Este documento describe varias extensiones SQL cómodas que generan un conjunto de datos derivado para utilizarlo con el perfil del cliente en tiempo real. El flujo de trabajo simplifica el proceso que, de lo contrario, tendría que completar a través de varias llamadas de API o interacciones de IU de Platform.

Normalmente, la generación y publicación de un conjunto de datos derivado para el perfil del cliente en tiempo real implicaría los siguientes pasos:

* Cree un área de nombres de identidad, si todavía no existe.
* Cree el tipo de datos para almacenar el conjunto de datos derivado, si es necesario.
* Cree un grupo de campos con ese tipo de datos para almacenar la información del conjunto de datos derivada.
* Cree o asigne una columna de identidad principal con el área de nombres creada anteriormente.
* Cree un esquema con el grupo de campos y el tipo de datos creados anteriormente.
* Cree un nuevo conjunto de datos con el esquema y actívelo para el perfil, si es necesario.
* Opcionalmente, marcar un conjunto de datos como habilitado para el perfil.

Después de completar los pasos mencionados anteriormente, está listo para rellenar el conjunto de datos. Si ha habilitado el conjunto de datos para el perfil, también puede crear segmentos que hagan referencia al nuevo conjunto de datos y comiencen a producir perspectivas.

El servicio de consultas le permite realizar todas las acciones enumeradas anteriormente mediante consultas SQL. Esto incluye realizar cambios en los conjuntos de datos y grupos de campos si es necesario.

## Cree una tabla con una opción para habilitarla para el perfil {#enable-dataset-for-profile}

>[!NOTE]
>
>La consulta SQL proporcionada a continuación supone el uso de un área de nombres preexistente.

Utilice una consulta Crear tabla como selección (CTAS) para crear un conjunto de datos, asignar tipos de datos, establecer una identidad principal, crear un esquema y marcarlo como habilitado para perfiles. La instrucción SQL de ejemplo siguiente crea un conjunto de datos y lo pone a disposición de Real-time Customer Data Platform (Real-Time CDP). La consulta SQL seguirá el formato mostrado en el ejemplo siguiente:

```sql
CREATE TABLE <your_table_name> [IF NOT EXISTS] (fieldname <your_data_type> primary identity namespace <your_namespace>, [field_name2 <your_data_type>]) [WITH(LABEL='PROFILE')];
```

Los tipos de datos admitidos son: booleano, fecha, fecha y hora, texto, flotante, bigint, entero, mapa, matriz y estructura/fila.

El siguiente bloque de código SQL proporciona ejemplos para definir tipos de datos de estructura/fila, asignación y matriz. La línea uno muestra la sintaxis de fila. La línea dos muestra la sintaxis del mapa, y la línea tres, la sintaxis de la matriz.

```sql {line-numbers="true"}
ROW (Column_name <data_type> [, column name <data_type> ]*)
MAP <data_type, data_type>
ARRAY <data_type>
```

Como alternativa, los conjuntos de datos también se pueden habilitar para perfiles mediante la IU de Platform. Para obtener más información sobre cómo marcar un conjunto de datos como habilitado para el perfil, consulte la [habilitar un conjunto de datos para la documentación del perfil del cliente en tiempo real](../../../catalog/datasets/user-guide.md#enable-profile).

En la consulta de ejemplo siguiente, la variable `decile_table` el conjunto de datos se crea con `id` como columna de identidad principal y tiene el área de nombres `IDFA`. También tiene un campo llamado `decile1Month` del tipo de datos de asignación. La tabla creada (`decile_table`) está habilitado para el perfil.

```sql
CREATE TABLE decile_table (id text PRIMARY KEY NAMESPACE 'IDFA', 
            decile1Month map<text, integer>) WITH (label='PROFILE');
```

Cuando la consulta se ejecuta correctamente, el ID del conjunto de datos se devuelve a la consola, como se ve en el ejemplo siguiente.

```console
Created Table DataSet Id
>
637fd84969ba291e62dba79f
(1 row)
```

Uso `label='PROFILE'` en un `CREATE TABLE` para crear un conjunto de datos habilitado para perfiles. El `upsert` La capacidad está activada de forma predeterminada. El `upsert` La capacidad se puede sobrescribir utilizando el `ALTER` , como se muestra en el ejemplo siguiente.

```sql
ALTER TABLE <your_table_name> DROP label upsert;
```

Consulte la documentación sobre la sintaxis SQL para obtener más información sobre el uso de [MODIFICAR TABLA](../../sql/syntax.md#alter-table) comando y [etiqueta como parte de una consulta CTAS](../../sql/syntax.md#create-table-as-select).

## Construcciones para ayudar a administrar conjuntos de datos derivados a través de SQL

Las funciones que se describen a continuación son muy útiles para administrar conjuntos de datos derivados mediante SQL.

### Cambie los conjuntos de datos existentes para que estén habilitados para el perfil {#enable-existing-dataset-for-profile}

La construcción ALTER TABLE SQL se puede utilizar para habilitar los conjuntos de datos existentes para el perfil. Esto requiere que se añada una etiqueta habilitada para perfil al esquema y al conjunto de datos correspondiente.

```sql
ALTER TABLE your_decile_table ADD label 'PROFILE';
```

>[!NOTE]
>
>Al ejecutar correctamente la variable `ALTER TABLE` comando, la consola devuelve `ALTER SUCCESS`.

### Añadir una identidad principal a un conjunto de datos existente {#add-primary-identity}

Marcar una columna existente en un conjunto de datos como un conjunto de identidad principal; de lo contrario, se producirá un error. Para establecer una identidad principal mediante SQL, utilice el formato de consulta que se muestra a continuación.

```sql
ALTER TABLE <your_table_name> ADD CONSTRAINT primary identity NAMESPACE
```

Por ejemplo:

```sql
ALTER TABLE test1_dataset ADD CONSTRAINT PRIMARY KEY(id2) NAMESPACE 'IDFA';
```

En el ejemplo proporcionado, `id2` es una columna existente en `test1_dataset`.

### Deshabilitar un conjunto de datos para el perfil {#disable-dataset-for-profile}

Si desea deshabilitar la tabla para usos de perfil, debe utilizar el comando DROP. Instrucción SQL de ejemplo que utiliza `DROP` se ve a continuación.

```sql
ALTER TABLE table_name DROP LABEL 'PROFILE';
```

Por ejemplo:

```sql
ALTER TABLE decile_table DROP label 'PROFILE';
```

Esta instrucción SQL proporciona un método alternativo eficaz para utilizar una llamada de API. Para obtener más información, consulte la documentación sobre cómo [deshabilitar un conjunto de datos para utilizarlo con Real-Time CDP mediante la API de conjuntos de datos](../../../catalog/datasets/enable-upsert.md#disable-the-dataset-for-profile).

### Permitir la actualización e inserción de la funcionalidad para el conjunto de datos {#enable-upsert-functionality-for-dataset}

El comando UPSERT permite insertar un nuevo registro o actualizar los datos existentes en una tabla. Específicamente, le permite actualizar una fila existente si un valor especificado ya existe en una tabla, o insertar una nueva fila si el valor especificado no existe ya.

A continuación se muestra una instrucción de ejemplo que utiliza el formato correcto.

```sql
ALTER TABLE table_name ADD LABEL 'UPSERT';
```

Por ejemplo:

```sql
ALTER TABLE table_with_a_decile ADD label 'UPSERT';
```

Esta instrucción SQL proporciona un método alternativo eficaz para utilizar una llamada de API. Para obtener más información, consulte la documentación sobre cómo [habilitar un conjunto de datos para utilizarlo con Real-Time CDP y UPSERT mediante la API de conjuntos de datos](../../../catalog/datasets/enable-upsert.md#enable-the-dataset).

### Deshabilitar la actualización e inserción de la funcionalidad para el conjunto de datos {#disable-upsert-functionality-for-dataset}

Este comando deshabilita la capacidad de actualizar e insertar filas en el conjunto de datos.

A continuación se muestra una instrucción de ejemplo que utiliza el formato correcto.

```sql
ALTER TABLE table_name DROP LABEL 'UPSERT';
```

Por ejemplo:

```sql
ALTER TABLE table_with_a_decile DROP label 'UPSERT';
```

### Mostrar información de tabla adicional asociada a cada tabla {#show-labels-for-tables}

Los metadatos adicionales se conservan para conjuntos de datos habilitados para perfiles. Utilice el `SHOW TABLES` para mostrar un extra `labels` que proporciona información sobre cualquier etiqueta asociada con tablas.

A continuación se muestra un ejemplo de la salida de este comando:

```sql
       name          |        dataSetId         |     dataSet    | description | labels 
---------------------+--------------------------+----------------+-------------+----------
 luma_midvalues      | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues     | 5c86b896b3c162151785b43c | Luma midValues |             | false
 table_with_a_decile | 5c86b896b3c162151785b43c | Luma midValues |             | 'UPSERT', 'PROFILE'
(3 rows)
```

Se puede ver en el ejemplo que `table_with_a_decile` se ha habilitado para el perfil y se ha aplicado con etiquetas como [&#39;ACTUALIZAR&#39;](#enable-upsert-functionality-for-dataset), [&#39;PERFIL&#39;](#enable-existing-dataset-for-profile) como se describió anteriormente.

### Creación de un grupo de campos con SQL

Los grupos de campos ahora se pueden crear mediante el uso de SQL. Esto proporciona una alternativa a utilizar el Editor de esquemas en la interfaz de usuario de Platform o realizar una llamada de API al Registro de esquemas.

A continuación, se muestra una instrucción de ejemplo para crear un grupo de campos.

```sql
CREATE FIELDGROUP <field_group_name> [IF NOT EXISTS]  (field_name <data_type> primary identity namespace <namespace>, [field_name_2 >data_type>]) [ WITH(LABEL='PROFILE') ];
```

>[!IMPORTANT]
>
>La creación de grupos de campos mediante SQL fallará si `label` El indicador no se proporciona en la instrucción o si el grupo de campos ya existe.
>Asegúrese de que la consulta incluye un `IF NOT EXISTS` para evitar que la consulta falle porque el grupo de campos ya existe.

Un ejemplo del mundo real podría parecer similar al que se ve a continuación.

```sql
CREATE FIELDGROUP field_group_for_test123 (decile1Month map<text, integer>, decile3Month map<text, integer>, decile6Month map<text, integer>, decile9Month map<text, integer>, decile12Month map<text, integer>, decilelietime map<text, integer>) WITH (LABEL-'PROFILE');
```

La ejecución correcta de esta instrucción devuelve el ID de grupo de campos creado. Por ejemplo `c731a1eafdfdecae1683c6dca197c66ed2c2b49ecd3a9525`.

Consulte la documentación sobre cómo [crear un nuevo grupo de campos en el Editor de esquemas](../../../xdm/ui/resources/field-groups.md#create) o utilizando el [API de registro de esquema](../../../xdm/api/field-groups.md#create) para obtener más información sobre métodos alternativos.

### Soltar un grupo de campos

En ocasiones puede ser necesario quitar un grupo de campos del Registro de esquemas. Esto se hace ejecutando la variable `DROP FIELDGROUP` con el ID de grupo de campos.

```sql
DROP FIELDGROUP [IF EXISTS] <your_field_group_id>;
```

Por ejemplo:

```sql
DROP FIELDGROUP field_group_for_test123;
```

>[!IMPORTANT]
>
>La eliminación de un grupo de campos mediante SQL fallará si el grupo de campos no existe. Asegúrese de que la instrucción incluye un `IF EXISTS` para evitar que la consulta falle.

### Mostrar todos los nombres e ID de grupos de campos de las tablas

El `SHOW FIELDGROUPS` El comando devuelve una tabla que contiene el nombre, fieldgroupId y el propietario de las tablas.

A continuación se muestra un ejemplo de la salida de este comando:

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

Después de leer este documento, tiene una mejor comprensión de cómo utilizar SQL para crear un perfil y un conjunto de datos habilitado para la actualización basado en conjuntos de datos derivados. Ya está listo para usar este conjunto de datos con flujos de trabajo de ingesta por lotes para realizar actualizaciones en los datos de perfil. Para obtener más información sobre la ingesta de datos en Adobe Experience Platform, comience por leer el [información general sobre ingesta de datos](../../../ingestion/home.md).
