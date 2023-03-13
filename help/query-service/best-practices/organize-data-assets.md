---
title: Prácticas recomendadas para la organización de recursos de datos en el servicio de consultas
description: Este documento describe un medio lógico de organizar los datos para facilitar su uso con el servicio de consultas.
exl-id: 12d6af99-035a-4f80-b7c0-c6413aa50697
source-git-commit: d3ea7ee751962bb507c91e1afea0da35da60a66d
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 0%

---

# Organización de recursos de datos en el servicio de consultas

Este documento proporciona instrucciones sobre las prácticas recomendadas para organizar recursos de datos, incluidos conjuntos de datos, vistas y tablas temporales, para utilizarlos con el servicio de consultas de Adobe Experience Platform. Explica cómo estructurar los datos, así como la información sobre cómo acceder, actualizar y eliminar esta información.

Es importante organizar lógicamente los recursos de datos dentro de la plataforma [!DNL Data Lake] a medida que crecen. El servicio de consultas amplía las construcciones SQL que permiten agrupar lógicamente los recursos de datos en una zona protegida. Este método de organización permite compartir recursos de datos entre esquemas sin necesidad de moverlos físicamente.

## Primeros pasos

Antes de continuar con este documento, debe comprender bien [Servicio de consultas](../home.md) y han leído el [guía de interfaz de usuario](../ui/user-guide.md).

## Organización de datos en el servicio de consultas

Los siguientes ejemplos muestran las construcciones disponibles a través de Adobe Experience Platform Query Service para organizar lógicamente los datos mediante sintaxis SQL estándar. Comience creando una base de datos que actúe como contenedor de los puntos de datos. Una base de datos puede contener uno o más esquemas y, a continuación, cada esquema puede tener una o más referencias a un recurso de datos (conjuntos de datos, vistas, tablas temporales, etc.). Estas referencias incluyen cualquier relación o asociación entre los conjuntos de datos.

Consulte la [Guía del usuario del Editor de consultas](../ui/user-guide.md) para obtener instrucciones detalladas sobre cómo utilizar la interfaz de usuario del servicio de consultas para crear consultas SQL.

Se admiten las siguientes construcciones SQL para organizar lógicamente conjuntos de datos en una zona protegida.

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

Una vez creado un esquema para actuar como contenedor para los recursos de datos, cada conjunto de datos se puede asociar con uno o más esquemas de la base de datos mediante la sintaxis estándar de SQL ALTER TABLE.

El siguiente ejemplo agrega `dataset1`, `dataset2`, `dataset3` y `v1` a la `databaseA.schema1` contenedor creado en el ejemplo anterior.

```SQL
ALTER TABLE dataset1 SET SCHEMA databaseA.schema1;
 
ALTER TABLE dataset2 SET SCHEMA databaseA.schema1;
 
ALTER TABLE dataset3 SET SCHEMA databaseA.schema1;
 
ALTER VIEW v1  SET SCHEMA databaseA.schema1;
```

## Acceso a los recursos de datos desde el contenedor de datos

Al calificar correctamente el nombre de la base de datos, cualquier [!DNL PostgreSQL] El cliente puede conectarse a cualquiera de las estructuras de datos creadas con la palabra clave SHOW. Para obtener más información sobre la palabra clave SHOW, consulte la [Sección SHOW dentro de la documentación de sintaxis SQL](../sql/syntax.md#show).

&quot;all&quot; es el nombre de base de datos predeterminado que contiene cada base de datos y contenedor de esquema en una zona protegida. Cuando realice una [!DNL PostgreSQL] conexión mediante `dbname="all"`, puede acceder a **cualquiera** base de datos y esquema creados para organizar lógicamente los datos.

Lista de todas las bases de datos en `dbname="all"` muestra tres bases de datos disponibles.

```sql
SHOW DATABASES;
  
name     
---------
databaseA
databaseB
databaseC
```

Enumerando todos los esquemas en `dbname="all"` muestra los tres esquemas relacionados con cada base de datos de la zona protegida.

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

La notación de puntos permite acceder a todas las tablas asociadas con un esquema específico conectado a la base de datos elegida. Al conectar con `DBNAME = databaseA.schema1;`, todas las tablas asociadas con ese esquema específico (`schema1`) se muestran. Proporciona información sobre qué conjunto de datos contiene qué tabla.

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

## Actualización o eliminación de recursos de datos de un contenedor de datos

A medida que aumenta la cantidad de recursos de datos en su organización de IMS (o zona protegida), es necesario actualizar o eliminar los recursos de datos de un contenedor de datos. Los recursos individuales se pueden eliminar del contenedor de organización haciendo referencia a la base de datos y al nombre de esquema adecuados mediante la notación de puntos. La tabla y la vista (`t1` y `v1` respectivamente) añadidas a `databaseA.schema1` en el primer ejemplo, se eliminan utilizando la sintaxis del siguiente ejemplo.

```sql
ALTER TABLE databaseA.schema2.t1 REMOVE SCHEMA databaseA.schema2;
ALTER VIEW databaseA.schema2.v1 REMOVE SCHEMA databaseA.schema2;
```

### Eliminación de recursos de datos

El [SOLTAR TABLA](../sql/syntax.md#drop-table) La función solo elimina físicamente un recurso de datos de [!DNL Data Lake] cuando exista una única referencia a la tabla en todas las bases de datos de su organización IMS.

```sql
DROP TABLE databaseA.schema2.t1;
```

### Eliminación de un contenedor de recursos de datos

Tanto la base de datos como el esquema también se pueden eliminar mediante funciones SQL estándar.

#### Eliminación de una base de datos

Si hay otras referencias a recursos de datos asociados con la base de datos, la función generará un error al intentar quitar la base de datos.

```sql
DROP DATABASE databaseA;
```

#### Eliminación de un esquema

Hay tres consideraciones importantes que se deben tener en cuenta al eliminar un esquema:

- Al eliminar un esquema, no se elimina físicamente ningún recurso de datos, como tablas, vistas o tablas temporales.
- Si se hace referencia a algún recurso de datos en el esquema de destinatario y el modo es RESTRICT, se generará una excepción.
- Si hay recursos de datos a los que se hace referencia en el esquema de destino y el modo es CASCADE, el sistema elimina todos los recursos de datos a los que hace referencia el contenedor de esquema y, a continuación, elimina el contenedor de esquema.

```sql
DROP SCHEMA databaseA.schema2;
```

## Pasos siguientes

Al leer este documento, ahora comprende mejor las prácticas recomendadas con respecto a la organización y estructura de los recursos de datos para su uso con el servicio de consultas de Adobe Experience Platform. Se recomienda continuar aprendiendo las prácticas recomendadas del servicio de consultas leyendo sobre [documentación de deduplicación de datos](../essential-concepts/deduplication.md).
