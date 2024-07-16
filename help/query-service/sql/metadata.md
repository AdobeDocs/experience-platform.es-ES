---
keywords: Experience Platform;inicio;temas populares;PSQL;psql;servicio de consultas;servicio de consultas;metadatos;comandos;comandos de metadatos;
solution: Experience Platform
title: Comandos PostgreSQL de metadatos en el servicio de consultas
description: Una lista de comandos PostgreSQL que actualmente se admiten para consultar metadatos en el servicio de consultas de Adobe Experience Platform.
exl-id: bfcbad55-3086-44c9-9938-6ba0504e747b
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 0%

---

# Comandos de metadatos [!DNL PostgreSQL] en el servicio de consultas

Para los metadatos del conjunto de datos, actualmente se admiten los siguientes [!DNL PostgreSQL] comandos para la consulta:

>[!NOTE]
>
>Los comandos que se enumeran a continuación distinguen entre mayúsculas y minúsculas.

| Comando | Descripción |
|------- | ------------|
| `\conninfo` | Genera información sobre la conexión de base de datos actual. |
| `\d` | Muestra una lista de todas las tablas, vistas, vistas materializadas, secuencias y tablas externas visibles. |
| `\dE` | Muestra una lista de tablas externas. |
| `\df or \df+` | Muestra una lista de funciones. |
| `\di` | Muestra una lista de índices. |
| `\dm` | Muestra una lista de vistas materializadas. |
| `\dn` | Muestra una lista de esquemas (áreas de nombres). |
| `\ds` | Muestra una lista de secuencias. |
| `\dS` | Muestra una lista de tablas definidas por PostgreSQL. |
| `\dt` | Muestra una lista de tablas. |
| `\dT` | Muestra una lista de tipos de datos. |
| `\dv` | Muestra una lista de vistas. |
| `\encoding` | Muestra la codificación actual del conjunto de caracteres del cliente. |
| `\errverbose` | Repite el mensaje de error del servidor más reciente con el máximo nivel de detalle. |
| `\l or \list` | Muestra una lista de las bases de datos del servidor. |
| `\set` | Muestra los nombres y valores de todas las variables psql actuales. |
| `\showtables` | Muestra la siguiente información: <br>nombre: nombre con el que se hará referencia a la tabla.<br>datasetId: ID del conjunto de datos que está almacenado.<br>conjunto de datos: nombre del conjunto de datos que está almacenado.<br>description: Una descripción del conjunto de datos.<br>resuelto: un valor booleano que indica si el conjunto de datos se resuelve o no en la sesión actual. |
| `\timing` | Alterna la visualización entre encendido y apagado. La pantalla se muestra en milisegundos. Los intervalos superiores a un segundo se muestran en formato minutos: segundos, con campos de horas y días añadidos cuando es necesario. |

Se pueden combinar todos los comandos que comienzan con `\d`. Por ejemplo, puede emitir `\dtsn` para mostrar una lista de todas las tablas, secuencias y esquemas. `\d` por sí solo muestra todas las tablas, vistas, vistas materializadas y secuencias visibles.

Para obtener información adicional sobre los comandos enumerados arriba, consulte la documentación en [postgresql.org](https://www.postgresql.org/docs/10/app-psql.html). Sin embargo, tenga en cuenta que [!DNL Experience Platform] no admite todas las opciones que se muestran en la documentación de [!DNL PostgreSQL].
