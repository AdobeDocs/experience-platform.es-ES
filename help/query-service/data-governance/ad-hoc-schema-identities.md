---
title: Definir identidades principales en un conjunto de datos ad hoc
description: Adobe Experience Platform Query Service permite establecer una identidad o una identidad principal para los campos de conjuntos de datos de esquemas ad hoc directamente mediante el comando SQL ALTER TABLE. El documento explica cómo utilizar el comando ALTER TABLE para establecer una identidad principal o secundaria.
exl-id: b8e6b87e-c6e5-4688-a936-a3a1510a3c5b
source-git-commit: d9c3ccdf0c0e191af1ab18e894688f301378156d
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 1%

---

# Establecimiento de identidades principales en un conjunto de datos ad hoc

El servicio de consultas de Adobe Experience Platform permite marcar columnas de conjuntos de datos como identidades principales o secundarias mediante restricciones para el comando SQL `ALTER TABLE`. Puede utilizar esta función para asegurarse de que los campos marcados son coherentes con los requisitos de privacidad de datos. Este comando permite agregar o eliminar restricciones para las columnas de la tabla de identidad principal y secundaria directamente a través de SQL.

## Introducción

Para etiquetar columnas de conjuntos de datos como identidad principal o secundaria se requiere comprender el comando SQL `ALTER TABLE` y comprender bien los requisitos de privacidad de datos. Antes de continuar con este documento, revise la siguiente documentación:

* [Guía de sintaxis SQL para el comando `ALTER TABLE`](../sql/syntax.md).
* [Información general sobre la administración de datos](../../data-governance/home.md) para obtener más información.

## Añadir restricciones {#add-constraints}

El comando `ALTER TABLE` le permite etiquetar una columna de conjunto de datos como identidad de una persona y luego utilizar esa etiqueta como identidad principal al actualizar los metadatos asociados mediante SQL. Esto resulta especialmente útil cuando los conjuntos de datos se crean mediante SQL en lugar de hacerlo directamente desde un esquema a través de la IU de Platform. El comando se puede utilizar para garantizar que las operaciones de datos en Platform sean compatibles con las políticas de uso de datos.

**Ejemplos**

En el siguiente ejemplo se agrega una restricción a la tabla `t1` existente. Los valores de la columna `id` ahora están marcados como identidades principales en el área de nombres `IDFA`. Un área de nombres de identidad es una palabra clave que declara el tipo de datos de identidad que representa el campo.

```sql
ALTER TABLE t1 ADD CONSTRAINT PRIMARY IDENTITY (id) NAMESPACE 'IDFA';
```

El segundo ejemplo garantiza que la columna `id` se marque como identidad secundaria.

```sql
ALTER TABLE t1 ADD CONSTRAINT IDENTITY(id) NAMESPACE 'IDFA';
```

## Eliminar restricciones {#drop-constraints}

Las restricciones también se pueden eliminar de las columnas de la tabla mediante el comando `ALTER TABLE`.

**Ejemplos**

El ejemplo siguiente elimina el requisito de que la columna `c1` esté etiquetada como identidad principal en la tabla `t1` existente.

```sql
ALTER TABLE t1 DROP CONSTRAINT PRIMARY IDENTITY (c1) ;
```

Como se ve a continuación, se utiliza la misma sintaxis para eliminar una restricción de identidad.

```sql
ALTER TABLE t1 DROP CONSTRAINT IDENTITY (c1) ;
```

## Mostrar identidades

Utilice el comando de metadatos `show identities` de la interfaz de la línea de comandos para mostrar una tabla con todos los atributos asignados como identidad.

```shell
> show identities;
```

A continuación se muestra un ejemplo de una tabla devuelta.

```console
 tableName | columnName | datatype | namespace | ifPrimary
-----------+------------+----------+-----------+----------
(0 rows)
```

## Limitaciones de XDM {#limitations}

En la siguiente lista se explican consideraciones importantes para actualizar identidades en conjuntos de datos existentes al utilizar XDM.

* Para especificar una columna como identidad, **debe** definir también el área de nombres que se conservará como metadatos para la columna.
* XDM no admite la especificación de un nombre de columna en el atributo namespace.
* Si el esquema utiliza el campo XDM `identityMap`, el objeto `identityMap` raíz o de nivel superior **debe** etiquetarse como identidad o identidad principal.
