---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Comandos de metadatos
topic: metadata
translation-type: tm+mt
source-git-commit: 45da024d45b5eebdfc393ee14890e24aed6021ce

---


# Comandos de metadatos

En el caso de los metadatos del conjunto de datos, los siguientes comandos PSQL se admiten actualmente para la consulta:

>[!NOTE] Los comandos que se enumeran a continuación distinguen entre mayúsculas y minúsculas.

| Comando | Descripción |
|------- | ------------|
| `\conninfo` | Extrae información sobre la conexión de base de datos actual. |
| `\d` | Muestra una lista de todas las tablas, vistas, vistas materializadas, secuencias y tablas externas visibles. |
| `\dE` | Muestra una lista de tablas externas. |
| `\df or \df+` | Muestra una lista de funciones. |
| `\di` | Muestra una lista de índices. |
| `\dm` | Muestra una lista de vistas materializadas. |
| `\dn` | Muestra una lista de esquemas (Áreas de nombres). |
| `\ds` | Muestra una lista de secuencias. |
| `\dS` | Muestra una lista de tablas definidas por PostgreSQL. |
| `\dt` | Muestra una lista de tablas. |
| `\dT` | Muestra una lista de tipos de datos. |
| `\dv` | Muestra una lista de vistas. |
| `\encoding` | Lista la codificación actual del conjunto de caracteres del cliente. |
| `\errverbose` | Repite el mensaje de error más reciente del servidor con la máxima amplitud. |
| `\l or \list` | Muestra una lista de bases de datos en el servidor. |
| `\set` | Muestra los nombres y valores de todas las variables psql actuales. |
| `\showtables` | Muestra la siguiente información: <br>name: Nombre por el cual se hará referencia a la tabla.<br>datasetId: ID del conjunto de datos que se almacena.<br>conjunto de datos: Nombre del conjunto de datos que se almacena.<br>description: Descripción del conjunto de datos.<br>resuelto: Un valor booleano que indica si el conjunto de datos se resuelve o no en la sesión actual. |
| `\timing` | Activa o desactiva la visualización. La pantalla se muestra en milisegundos. Los intervalos superiores a un segundo se muestran en formato de minutos:segundos, con campos de horas y días agregados cuando es necesario. |

Se pueden combinar todos los comandos con los que `\d` se inicio. Por ejemplo, puede publicar `\dtsn` para mostrar una lista de todas las tablas, secuencias y esquemas. `\d` por sí mismo muestra todas las tablas, vistas, vistas materializadas y secuencias visibles.

Para obtener más información sobre los comandos mencionados anteriormente, consulte la documentación de [postgresql.org](https://www.postgresql.org/docs/10/app-psql.html). Sin embargo, tenga en cuenta que la plataforma de experiencia no admite todas las opciones que se muestran en la documentación de PostgreSQL.

