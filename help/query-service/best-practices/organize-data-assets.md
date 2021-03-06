---
title: Prácticas recomendadas para la organización de recursos de datos en el servicio de consulta
description: Este documento describe un medio lógico de organizar los datos para facilitar su uso con el servicio de consulta.
source-git-commit: ed9fa7b83f9e1c974bc74e9dde018a87823954ee
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 0%

---

# Organización de recursos de datos en el servicio de consulta

Este documento proporciona instrucciones sobre prácticas recomendadas para organizar recursos de datos, incluidos conjuntos de datos, vistas y tablas temporales para su uso con el servicio de consulta de Adobe Experience Platform. Abarca cómo estructurar los datos, así como información sobre cómo acceder, actualizar y eliminar esta información.

Es importante organizar lógicamente los recursos de datos dentro de la plataforma [!DNL Data Lake] a medida que crecen. El servicio de consulta amplía las construcciones SQL que permiten agrupar lógicamente recursos de datos dentro de un simulador para pruebas. Este método de organización permite compartir recursos de datos entre esquemas sin necesidad de moverlos físicamente.

## Primeros pasos

Antes de continuar con este documento, debe tener una buena comprensión de [Servicio de consultas](../home.md) y haber leído las [guía de interfaz de usuario](../ui/user-guide.md).

## Organización de datos en el servicio de consulta

Los siguientes ejemplos muestran las construcciones disponibles a través del servicio de consulta de Adobe Experience Platform para organizar lógicamente los datos utilizando la sintaxis SQL estándar. Debe empezar creando una base de datos para que actúe como contenedor de sus puntos de datos. Una base de datos puede contener uno o más esquemas y cada esquema puede tener una o más referencias a un recurso de datos (conjuntos de datos, vistas, tablas temporales, etc.). Estas referencias incluyen cualquier relación o asociación entre los conjuntos de datos.

Consulte la [Guía del usuario del Editor de consultas](../ui/user-guide.md) para obtener instrucciones detalladas sobre cómo utilizar la interfaz de usuario del servicio de consulta para crear consultas SQL.

Se admiten las siguientes construcciones SQL para organizar lógicamente conjuntos de datos en un entorno limitado.

```SQL
CREATE DATABASE databaseA;
CREATE SCHEMA databaseA.schema1;
CREATE table t1 ...;
CREATE view v1 ...;
ALTER TABLE t1 ADD PRIMARY KEY (c1) NOT ENFORCED;
ALTER TABLE t2 ADD FOREIGN KEY (c1) REFERENCES t1(c1) NOT ENFORCED;
```

El ejemplo (ligeramente truncado para la brevedad) muestra esta metodología donde `databaseA` contiene esquema `schema1`.

## Asociación de recursos de datos a un esquema

Una vez que se ha creado un esquema para que actúe como contenedor de los recursos de datos, cada conjunto de datos puede asociarse con uno o más esquemas de la base de datos mediante la sintaxis estándar SQL ALTER TABLE.

El siguiente ejemplo agrega `dataset1`, `dataset2`, `dataset3` y `v1` a `databaseA.schema1` contenedor creado en el ejemplo anterior.

```SQL
ALTER TABLE dataset1 SET SCHEMA databaseA.schema1;
 
ALTER TABLE dataset2 SET SCHEMA databaseA.schema1;
 
ALTER TABLE dataset3 SET SCHEMA databaseA.schema1;
 
ALTER VIEW v1  SET SCHEMA databaseA.schema1;
```

## Acceso a los recursos de datos desde el contenedor de datos

Al calificar adecuadamente el nombre de la base de datos, cualquier [!DNL PostgreSQL] El cliente puede conectarse a cualquiera de las estructuras de datos que ha creado con la palabra clave SHOW. Para obtener más información sobre la palabra clave SHOW, consulte la [SHOW dentro de la documentación de sintaxis SQL](../sql/syntax.md#show).

&quot;all&quot; es el nombre predeterminado de la base de datos que contiene cada base de datos y contenedor de esquema en un simulador para pruebas. Cuando realice una [!DNL PostgreSQL] conexión mediante `dbname="all"`, puede acceder a **any** base de datos y esquema que ha creado para organizar lógicamente los datos.

Enumerar todas las bases de datos en `dbname="all"` muestra tres bases de datos disponibles.

```sql
SHOW DATABASES;
  
name     
---------
databaseA
databaseB
databaseC
```

Enumerar todo el esquema en `dbname="all"` muestra los tres esquemas relacionados con cada base de datos en el simulador de pruebas.

```SQL
SHOW SCHEMAS;
  
database       | schema
----------------------
databaseA      | schema1
databaseA      | schema2
databaseB      | schema3
```

Cuando realice una [!DNL PostgreSQL] conexión mediante `dbname="databaseA"`, puede acceder a cualquier esquema asociado con esa base de datos específica, como se muestra en el ejemplo siguiente.

```sql
SHOW DATABASES;
  
name     
---------
databaseA
 

SHOW SCHEMAS;
  
database       | schema
----------------------
databaseA      | schema1
databaseA      | schema2
```

La notación de puntos permite acceder a todas las tablas asociadas a un esquema específico conectado a la base de datos seleccionada. Conectándose a `DBNAME = databaseA.schema1;`, todas las tablas asociadas a ese esquema específico (`schema1`). Esto proporciona información sobre qué conjunto de datos contiene qué tabla.

```sql
SHOW DATABASES;
  
name     
---------
databaseA


SHOW SCHEMAS;
  
database       | schema
----------------------
databaseA      | schema1


SHOW tables;
name       | type
----------------------
dataset1| table
dataset2| table
dataset3| table
```

## Actualizar o quitar recursos de datos de un contenedor de datos

A medida que crece la cantidad de recursos de datos en su organización (o simulador de pruebas) de IMS, se hace necesario actualizar o eliminar los recursos de datos de un contenedor de datos. Los recursos individuales se pueden eliminar del contenedor de organización haciendo referencia a la base de datos y el nombre de esquema adecuados con notación de puntos. La tabla y la vista (`t1` y `v1` respectivamente) se ha añadido a `databaseA.schema1` en el primer ejemplo, se eliminan utilizando la sintaxis del ejemplo siguiente.

```sql
ALTER TABLE databaseA.schema2.t1 REMOVE SCHEMA databaseA.schema2;
ALTER VIEW databaseA.schema2.v1 REMOVE SCHEMA databaseA.schema2;
```

### Eliminación de recursos de datos

La variable [TABLA DE COLOCACIÓN](../sql/syntax.md#drop-table) solo elimina físicamente un recurso de datos de la función [!DNL Data Lake] cuando exista una única referencia a la tabla en todas las bases de datos de su organización de IMS.

```sql
DROP TABLE databaseA.schema2.t1;
```

### Eliminación de un contenedor de recursos de datos

Tanto la base de datos como el esquema también se pueden eliminar mediante funciones SQL estándar.

#### Eliminación de una base de datos

Si hay otras referencias a recursos de datos asociados con la base de datos, la función generará un error al intentar eliminar la base de datos.

```sql
DROP DATABASE databaseA;
```

#### Eliminación de un esquema

Hay tres consideraciones importantes que se deben tener en cuenta al quitar un esquema:

- Al eliminar un esquema, no se elimina físicamente ningún recurso de datos, como tablas, vistas o tablas temporales.
- Si hay algún recurso de datos al que se haga referencia en el esquema de destino y el modo es RESTRICT, se generará una excepción.
- Si hay algún recurso de datos al que se haga referencia en el esquema de destino y el modo es CASCADE, el sistema elimina todos los recursos de datos a los que hace referencia el contenedor de esquema y, a continuación, elimina el contenedor de esquema.

```sql
DROP SCHEMA databaseA.schema2;
```

## Pasos siguientes

Al leer este documento, ahora puede comprender mejor las prácticas recomendadas relacionadas con la organización y estructura de los recursos de datos para su uso con el servicio de consulta de Adobe Experience Platform. Se recomienda seguir aprendiendo sobre las prácticas recomendadas del servicio de consulta leyendo sobre [documentación de deduplicación de datos](./deduplication.md).
