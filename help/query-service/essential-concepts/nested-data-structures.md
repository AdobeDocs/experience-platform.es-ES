---
keywords: Experience Platform;servicio de consultas;servicio de consultas;estructuras de datos anidadas;datos anidados;
title: Uso de estructuras de datos anidadas en el servicio de consultas
description: Este documento proporciona un ejemplo práctico para procesar y transformar campos de datos anidados mediante instrucciones CTAS e INSERT INTO.
exl-id: 593379fb-88ad-4b14-8d2e-aa6d18129974
source-git-commit: d3ea7ee751962bb507c91e1afea0da35da60a66d
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 1%

---

# Uso de estructuras de datos anidadas en el servicio de consultas

El servicio de consulta de Adobe Experience Platform admite el uso de campos de datos anidados. La complejidad de las estructuras de datos empresariales puede complicar la transformación o el procesamiento de estos datos. Este documento proporciona ejemplos de cómo crear, procesar o transformar conjuntos de datos con tipos de datos complejos, incluidas estructuras de datos anidadas.

El servicio de consultas proporciona un [!DNL PostgreSQL] para ejecutar consultas SQL en todos los conjuntos de datos administrados por el Experience Platform. Platform admite el uso de tipos de datos primitivos o complejos en columnas de tabla como struct, matrices, mapas y struct, matrices y mapas profundamente anidados. Los conjuntos de datos también pueden contener estructuras anidadas en las que el tipo de datos de columna puede ser tan complejo como una matriz de estructuras anidadas o un mapa de mapas en el que el valor de un par clave-valor puede ser una estructura con varios niveles de anidamiento.

## Primeros pasos

Este tutorial requiere el uso de un cliente PSQL de terceros o de la herramienta Editor de consultas para escribir, validar y ejecutar consultas en la interfaz de usuario (IU) de Experience Platform. Encontrará todos los detalles sobre cómo ejecutar consultas a través de la interfaz de usuario en la [Guía de IU del Editor de consultas](../ui/user-guide.md). Para obtener una lista detallada sobre los clientes de escritorio de terceros que pueden conectarse al servicio de consultas, consulte la [información general sobre conexiones de cliente](../clients/overview.md).

También debería tener una buena comprensión de la `INSERT INTO` y `CTAS` sintaxis. Puede encontrar información específica sobre su uso en el [`INSERT INTO`](../sql/syntax.md#insert-into) y [`CTAS`](../sql/syntax.md#create-table-as-select) secciones de la [Documentación de referencia de sintaxis SQL](../sql/syntax.md).

## Crear un conjunto de datos

El servicio de consultas proporciona la opción Crear tabla como seleccionar (`CTAS`) para crear una tabla basada en el resultado de una `SELECT` o, como en este caso, utilizando una referencia a un esquema XDM existente en Adobe Experience Platform. A continuación se muestra el esquema XDM para `Final_subscription` creado para este ejemplo.

![Diagrama del esquema final_subscription.](../images/best-practices/final-subscription-schema.png)

En el ejemplo siguiente se muestra el SQL utilizado para crear el objeto `final_subscription_test2` conjunto de datos. `final_subscription_test2` se crea con la variable `Final_subscription` esquema. Los datos se extraen del origen mediante una `SELECT` para rellenar algunas filas.

```sql
CREATE TABLE final_subscription_test2 with(schema='Final_subscription') AS (
        SELECT struct(userid, collect_set(subscription) AS subscription) AS _lumaservices3 FROM(
            SELECT user AS userid,
                   struct( last(eventtime) AS last_eventtime,
                           last(status) AS last_status,
                           offer_id, 
                           subsid AS subscription_id)
                   AS subscription
             FROM (
                   SELECT _lumaservices3.msftidentities.userid user
                        , _lumaservices3.subscription.subscription_id subsid
                        , _lumaservices3.subscription.subscription_status status
                        , _lumaservices3.subscription.offer_id offer_id
                        , TIMESTAMP eventtime
 
                   FROM
                        xbox_subscription_event
                   UNION   
                   SELECT _lumaservices3.msftidentities.userid user
                        , _lumaservices3.subscription.subscription_id subsid
                        , _lumaservices3.subscription.subscription_status status
                        , _lumaservices3.subscription.offer_id offer_id
                        , TIMESTAMP eventtime
                   FROM
                        office365_subscription_event
             ) 
             GROUP BY user,subsid,offer_id
             ORDER BY user ASC
       ) GROUP BY userid)
```

En el conjunto de datos inicial `final_subscription_test2`, el tipo de datos struct se utiliza para contener tanto el `subscription` y el `userid` que es exclusivo de cada usuario. El `subscription` Este campo describe las suscripciones de producto de un usuario. Puede haber varias suscripciones, pero una tabla solo puede contener la información de una suscripción por fila.

## Utilice INSERT INTO para actualizar los campos de datos anidados

Después del `final_subscription_test2` se ha creado el conjunto de datos, `INSERT INTO` se utiliza para anexar datos adicionales a la tabla. Al copiar datos, los tipos de datos de origen y destino deben coincidir. Alternativamente, el tipo de datos de origen debe ser `CAST` al tipo de datos de destinatario. A continuación, los datos incrementales se añaden al conjunto de datos de destino mediante el siguiente SQL.

```sql
INSERT INTO final_subscription_test
      SELECT struct(userid, collect_set(subscription) AS subscription) AS _lumaservices3 FROM(
            SELECT user AS userid,
                   struct( last(eventtime) AS last_eventtime,
                           last(status) AS last_status,
                           offer_id, 
                           subsid AS subscription_id)
                   AS subscription
             FROM  SELECT _lumaservices3.msftidentities.userid user
                        , _lumaservices3.subscription.subscription_id subsid
                        , _lumaservices3.subscription.subscription_status status
                        , _lumaservices3.subscription.offer_id offer_id
                        , TIMESTAMP eventtime
 
                   FROM
                        xbox_subscription_event
                   UNION   
                   SELECT _lumaservices3.msftidentities.userid user
                        , _lumaservices3.subscription.subscription_id subsid
                        , _lumaservices3.subscription.subscription_status status
                        , _lumaservices3.subscription.offer_id offer_id
                        , timestamp eventtime
                   FROM
                        office365_subscription_event
             ) 
             GROUP BY user,subsid,offer_id
             ORDER BY user ASC
       ) GROUP BY userid)
```

## Procesamiento de datos de un conjunto de datos anidado

Para saber la lista de las suscripciones activas de un usuario de un conjunto de datos, debe escribir una consulta que separe los elementos de una matriz en varias filas y columnas. Para ello, primero debe comprender la forma del modelo de datos, ya que la información de suscripción se mantiene dentro de una matriz anidada dentro del conjunto de datos.

El PSQL `\d` El comando se utiliza para desplazarse nivel a nivel hasta los datos de suscripción necesarios. Las tablas ilustran la estructura del `final_subscription_test2` conjunto de datos. Los tipos de datos complejos se pueden reconocer de un vistazo porque no son valores de tipo típicos, como texto, booleano, marca de tiempo, etc.

| Columna | Tipo |
|--------|-------|
| `_lumaservices3` | final_subscription_test2__lumaservices3 |

Los campos de la columna siguiente se muestran mediante la variable `\d final_subscription_test2__lumaservices3` comando.

| Columna | Tipo |
|---------|-------|
| `userid` | texto |
| `subscription` | _lumaservices3_subscription_e[] |

`subscription` es una matriz de elementos struct. Sus campos se muestran mediante la variable `\d _lumaservices3_subscription_e[]` comando.

| Columna | Tipo |
|---------|-------|
| `last_eventtime` | timestamp |
| `last_status` | texto |
| `offer_id` | texto |
| `subscription_id` | texto |

Para consultar los campos anidados de la suscripción, primero debe separar los elementos del `subscription` en varias filas y devuelva los resultados utilizando la función explode. El siguiente ejemplo de SQL devuelve la suscripción activa de un usuario basándose en `userid`.

```sql
SELECT userid, subs AS active_subscription FROM (
    SELECT _lumaservices3.userid AS userid, explode(_lumaservices3.subscription) AS subs 
    FROM final_subscription_test2
)
WHERE subs.last_status='Active';
```

Esta solución de ejemplo simplificada solo permite una suscripción de usuario activa. Siendo realistas, puede haber muchas suscripciones activas para un solo usuario. El siguiente ejemplo modifica la consulta anterior para permitir varias suscripciones activas simultáneas.

```sql
SELECT userid, collect_list(subs) AS active_subscriptions FROM (
     SELECT
          _lumaservices3.userid AS userid,
          explode(_lumaservices3.subscription) AS subs
     FROM final_subscription_test2
     )
WHERE subs.last_status='Active' 
GROUP BY userid ;
```

A pesar de la creciente complejidad de este ejemplo SQL, la variable `collect_list` para suscripciones activas no garantiza que la salida esté en el mismo orden que el origen. Para crear una lista de suscripciones activas para un usuario, debe utilizar GROUP BY o el barajado para acumular los resultados de la lista.

## Pasos siguientes

Al leer este documento, ahora comprende cómo procesar o transformar conjuntos de datos que utilizan tipos de datos complejos en Adobe Experience Platform Query Service. Consulte la [guía de ejecución de consultas](../best-practices/writing-queries.md) para obtener más información sobre la ejecución de consultas SQL en conjuntos de datos dentro del lago de datos.
