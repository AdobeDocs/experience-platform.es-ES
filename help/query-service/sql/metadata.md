---
keywords: Experience Platform;inicio;temas populares;PSQL;psql;servicio de consulta;servicio de consulta;metadatos;comandos;comandos de metadatos;
solution: Experience Platform
title: Comandos PostgreSQL de metadatos en el servicio de consulta
topic-legacy: metadata
description: Lista de comandos PostgreSQL que actualmente se admiten para consultar metadatos en el servicio de consulta de Adobe Experience Platform.
exl-id: bfcbad55-3086-44c9-9938-6ba0504e747b
source-git-commit: 9c450f340706040593dfea5292702c4b00dd9852
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 0%

---

# Metadatos [!DNL PostgreSQL] comandos en Query Service

Para los metadatos de su conjunto de datos, haga lo siguiente: [!DNL PostgreSQL] actualmente se admiten comandos para consulta:

>[!NOTE]
>
>Los comandos que se indican a continuación distinguen entre mayúsculas y minúsculas.

| Comando | Descripción |
|------- | ------------|
| `\conninfo` | Genera información sobre la conexión de base de datos actual. |
| `\d` | Muestra una lista de todas las tablas visibles, vistas, vistas materializadas, secuencias y tablas externas. |
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
| `\encoding` | Muestra la codificación del conjunto de caracteres cliente actual. |
| `\errverbose` | Repite el mensaje de error del servidor más reciente con la máxima amplitud. |
| `\l or \list` | Muestra una lista de bases de datos en el servidor. |
| `\set` | Muestra los nombres y valores de todas las variables psql actuales. |
| `\showtables` | Muestra la siguiente información: <br>nombre: Nombre al que se hace referencia a la tabla.<br>datasetId: ID del conjunto de datos que se almacena.<br>conjunto de datos: El nombre del conjunto de datos que se almacena.<br>descripción: Descripción del conjunto de datos.<br>resuelto: Un valor booleano que indica si el conjunto de datos se resuelve o no en la sesión actual. |
| `\timing` | Activa o desactiva la visualización. La pantalla se muestra en milisegundos. Los intervalos superiores a un segundo se muestran en formato de minutos:segundos, con los campos horas y días agregados cuando es necesario. |

Todos los comandos que comienzan con `\d` se puede combinar. Por ejemplo, puede causar problemas `\dtsn` para mostrar una lista de todas las tablas, secuencias y esquemas. `\d` por sí solo muestra todas las tablas, vistas, vistas materializadas y secuencias visibles.

Para obtener información adicional sobre los comandos enumerados anteriormente, consulte la documentación en [postgresql.org](https://www.postgresql.org/docs/10/app-psql.html). Sin embargo, tenga en cuenta que no todas las opciones que se muestran en la [!DNL PostgreSQL] la documentación es compatible con [!DNL Experience Platform].
