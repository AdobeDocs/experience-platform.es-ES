---
title: Definir identidades principales en un conjunto de datos ad hoc
description: El servicio de consulta de Adobe Experience Platform le permite establecer una identidad o una identidad principal para los campos de conjuntos de datos de esquema específicos directamente a través del comando SQL ALTER TABLE. En el documento se explica cómo utilizar el comando ALTER TABLE para establecer una identidad primaria o una identidad secundaria.
source-git-commit: bf51fc3e0c9635c0555f87f3389fb4a9542c092d
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 1%

---

# Establecer identidades principales en un conjunto de datos ad hoc

El servicio de consulta de Adobe Experience Platform le permite marcar columnas de conjuntos de datos como identidades principales o secundarias mediante restricciones para el SQL `ALTER TABLE` comando. Puede utilizar esta función para asegurarse de que los campos marcados son coherentes con los requisitos de privacidad de datos. Este comando permite agregar o eliminar restricciones para columnas de tabla de identidad primarias y secundarias directamente a través de SQL.

## Primeros pasos

El etiquetado de las columnas de conjuntos de datos como identidad primaria o secundaria requiere una comprensión de la variable `ALTER TABLE` El comando SQL y una buena comprensión de los requisitos de privacidad de datos. Antes de continuar con este documento, revise la siguiente documentación:

* [La guía de sintaxis SQL para la variable `ALTER TABLE` command](../sql/syntax.md).
* [Información general sobre la administración de datos](../../data-governance/home.md) para obtener más información.

## Añadir restricciones {#add-constraints}

La variable `ALTER TABLE` permite etiquetar una columna de conjunto de datos como la identidad de una persona y, a continuación, utilizar esa etiqueta como identidad principal actualizando los metadatos asociados mediante SQL. Esto resulta especialmente útil cuando los conjuntos de datos se crean mediante SQL en lugar de hacerlo directamente desde un esquema a través de la interfaz de usuario de Platform. El comando se puede utilizar para garantizar que las operaciones de datos dentro de Platform sean compatibles con las políticas de uso de datos.

**Ejemplos**

En el siguiente ejemplo se agrega una restricción al `t1` tabla. Los valores de la variable `id` ahora se marcan como identidades principales en la sección `IDFA` espacio de nombres. Un área de nombres de identidad es una palabra clave que declara el tipo de datos de identidad que representa el campo.

```sql
ALTER TABLE t1 ADD CONSTRAINT PRIMARY IDENTITY (id) NAMESPACE 'IDFA';
```

El segundo ejemplo garantiza que la variable `id` se marca como identidad secundaria.

```sql
ALTER TABLE t1 ADD CONSTRAINT IDENTITY(id) NAMESPACE 'IDFA';
```

## Eliminar restricciones {#drop-constraints}

Las restricciones también se pueden eliminar de las columnas de la tabla utilizando la variable `ALTER TABLE` comando.

**Ejemplos**

El ejemplo siguiente elimina el requisito de que la variable `c1` se etiquetará como identidad principal en la `t1` tabla.

```sql
ALTER TABLE t1 DROP CONSTRAINT PRIMARY IDENTITY (c1) ;
```

Como se ve a continuación, se utiliza la misma sintaxis para cuando se elimina una restricción de identidad.

```sql
ALTER TABLE t1 DROP CONSTRAINT IDENTITY (c1) ;
```

## Mostrar identidades

Usar el comando de metadatos `show identities` desde la interfaz de la línea de comandos para mostrar una tabla con todos los atributos asignados como identidad.

```shell
> show identities;
```

A continuación se muestra un ejemplo de tabla devuelta.

```console
 tableName | columnName | datatype | namespace | ifPrimary
-----------+------------+----------+-----------+----------
(0 rows)
```

## Limitaciones XDM {#limitations}

La siguiente lista explica consideraciones importantes para actualizar identidades en conjuntos de datos existentes al utilizar XDM.

* Para especificar una columna como identidad, debe **must** defina también el espacio de nombres que se va a conservar como metadatos para la columna.
* XDM no admite la especificación de un nombre de columna en el atributo namespace.
* Si el esquema utiliza la variable `identityMap` Campo XDM, raíz o nivel superior `identityMap` object **must** se etiquetarán como identidad o identidad principal.
