---
keywords: Experience Platform;inicio;temas populares;PSQL;psql;servicio de Consulta;servicio de consulta;metadatos;comandos;comandos de metadatos;
solution: Experience Platform
title: Comandos PostgreSQL de metadatos en el servicio de Consulta
topic: metadata
description: Lista de comandos PostgreSQL que actualmente se admiten para consultar metadatos en el servicio de Consulta de Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 97dc0b5fb44f5345fd89f3f56bd7861668da9a6e
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---


# Comandos PostgreSQL de metadatos en el servicio de Consulta

En el caso de los metadatos del conjunto de datos, los siguientes comandos PostgreSQL se admiten actualmente para la consulta:

>[!NOTE]
>
>Los comandos que se enumeran a continuación distinguen entre mayúsculas y minúsculas.

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
| `\showtables` | Muestra la siguiente información: <br>nombre: Nombre por el cual se hará referencia a la tabla.<br>datasetId: ID del conjunto de datos que se almacena.<br>conjunto de datos: Nombre del conjunto de datos que se almacena.<br>description: Descripción del conjunto de datos.<br>resuelto: Un valor booleano que indica si el conjunto de datos se resuelve o no en la sesión actual. |
| `\timing` | Activa o desactiva la visualización. La pantalla se muestra en milisegundos. Los intervalos superiores a un segundo se muestran en formato de minutos:segundos, con campos de horas y días agregados cuando es necesario. |

Se pueden combinar todos los comandos que inicio con `\d`. Por ejemplo, puede emitir `\dtsn` para mostrar una lista de todas las tablas, secuencias y esquemas. `\d` por sí mismo muestra todas las tablas, vistas, vistas materializadas y secuencias visibles.

Para obtener información adicional sobre los comandos enumerados anteriormente, consulte la documentación en [postgresql.org](https://www.postgresql.org/docs/10/app-psql.html). Sin embargo, tenga en cuenta que [!DNL Experience Platform] no todas las opciones que se muestran en la documentación de PostgreSQL son compatibles.

