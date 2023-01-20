---
title: Caso de uso de atributos derivados basados en decimales
description: En esta guía se muestran los pasos necesarios para utilizar el servicio de consulta para crear atributos derivados basados en decimales y utilizarlos con los datos de perfil.
exl-id: 0ec6b511-b9fd-4447-b63d-85aa1f235436
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '1508'
ht-degree: 2%

---

# Caso de uso de atributos derivados basados en decimales

Los atributos derivados facilitan casos de uso complicados para analizar datos del lago de datos que se pueden utilizar con otros servicios de Platform descendentes o publicar en sus datos del Perfil del cliente en tiempo real.

Este ejemplo de uso muestra cómo crear atributos derivados basados en decimales para usarlos con los datos del perfil del cliente en tiempo real. Como ejemplo, en esta guía se explica cómo crear un conjunto de datos que utilice deciles categóricos para segmentar y crear audiencias basadas en atributos de clasificación.

Se ilustran los siguientes conceptos clave:

* Creación de esquemas para el agrupamiento de decimales.
* Creación de deciles categóricos.
* Creación de atributos derivados complejos.
* Cálculo de decimales durante un periodo retroactivo.
* Una consulta de ejemplo para mostrar la agregación, clasificación y adición de identidades únicas para permitir que las audiencias se generen en función de estos bloques decimales.

## Primeros pasos

Esta guía requiere una comprensión práctica de [ejecución de consultas en el servicio de consultas](../best-practices/writing-queries.md) y los siguientes componentes de Adobe Experience Platform:

* [Resumen del perfil del cliente en tiempo real](../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.
* [Aspectos básicos de la composición del esquema](../../xdm/schema/composition.md): Introducción a los esquemas del Modelo de datos de experiencia (XDM) y a los componentes, principios y prácticas recomendadas para la composición de esquemas.
* [Habilitación de un esquema para el perfil del cliente en tiempo real](../../profile/tutorials/add-profile-data.md): Este tutorial describe los pasos necesarios para agregar datos al perfil del cliente en tiempo real.
* [Definición de un tipo de datos personalizado](../../xdm/api/data-types.md): Los tipos de datos se utilizan como campos de referencia en clases o grupos de campos de esquema y permiten el uso coherente de una estructura de varios campos que se puede incluir en cualquier parte del esquema.

## Objetivos

El ejemplo dado en este documento utiliza deciles para crear atributos derivados para clasificar datos de un esquema de lealtad de aerolíneas. Los atributos derivados le permiten maximizar la utilidad de sus datos identificando una audiencia en función del &quot;n&quot; % superior para una categoría elegida.

## Generar atributos derivados basados en decimales

Para definir la clasificación de los deciles en función de una dimensión en particular y una métrica correspondiente, se debe diseñar un esquema para permitir la creación de bloques de decimales.

Esta guía utiliza un conjunto de datos de lealtad de aerolíneas para demostrar cómo utilizar el servicio de consulta para generar deciles en función de las millas voladas en varios períodos retrospectivos.

## Utilizar el servicio de consulta para crear deciles

Con el servicio de consulta, puede crear un conjunto de datos que contenga decimales categóricos, que luego se pueden segmentar para crear audiencias basadas en la clasificación de atributos. Los conceptos mostrados en los ejemplos siguientes se pueden aplicar para crear otros conjuntos de datos de bloque de deciles, siempre y cuando se defina una categoría y haya una métrica disponible.

Los datos de lealtad de aerolíneas de ejemplo utilizan un [Clase XDM ExperienceEvents](../../xdm/classes/experienceevent.md). Cada evento es un registro de una transacción comercial por kilometraje, ya sea abonado o adeudado, y el estado de fidelidad de membresía de &quot;Volante&quot;, &quot;Frecuente&quot;, &quot;Plata&quot; o &quot;Oro&quot;. El campo de identidad principal es `membershipNumber`.

### Conjunto de datos de muestra

El conjunto de datos de fidelidad de aerolíneas inicial para este ejemplo es &quot;Datos de fidelidad de aerolíneas&quot; y tiene el esquema siguiente. Tenga en cuenta que la identidad principal del esquema es `_profilefoundationreportingstg.membershipNumber`.

![Diagrama del esquema de datos de lealtad de la aerolínea.](../images/use-cases/airline-loyalty-data.png)

**Datos de muestra**

La tabla siguiente muestra los datos de ejemplo contenidos en la variable `_profilefoundationreportingstg` objeto utilizado para este ejemplo. Proporciona contexto para el uso de bloques de decimales para crear atributos derivados complejos.

>[!NOTE]
>
>Para la brevedad, el ID de inquilino `_profilefoundationreportingstg` se ha omitido al principio del espacio de nombres en los títulos de columna y menciones posteriores en todo el documento.

| `.membershipNumber` | `.emailAddress.address` | `.transactionDate` | `.transactionType` | `.transactionDetails` | `.mileage` | `.loyaltyStatus` |
|---|---|---|---|---|---|---|
| C435678623 | sfeldmark1vr@studiopress.com | 2022-01-01 | STATUS_MILES | Nuevo miembro | 5000 | FLYER |
| B789279247 | pgalton32n@barnesandnoble.com | 2022-02-01 | AWARD_MILES | JFK-FRA | 7500 | PLATA |
| B789279247 | pgalton32n@barnesandnoble.com | 2022-02-01 | STATUS_MILES | JFK-FRA | 7500 | PLATA |
| B789279247 | pgalton32n@barnesandnoble.com | 2022-02-10 | AWARD_MILES | FRA-JFK | 5000 | PLATA |
| A123487284 | rritson1zn@sciencedaily.com | 2022-01-07 | STATUS_MILES | Nueva tarjeta de crédito | 10 000 | FLYER |

{style=&quot;table-layout:auto&quot;}

## Generar conjuntos de datos decimales

En los datos de lealtad de las compañías aéreas que se han visto anteriormente, la variable `.mileage` contiene el número de millas voladas por un miembro para cada vuelo individual realizado. Estos datos se utilizan para crear decimales para el número de millas recorridas durante retrospectivas de por vida y una variedad de periodos retrospectivos. Para este fin, se crea un conjunto de datos que contiene decimales en un tipo de datos de mapa para cada periodo retroactivo y un decil apropiado para cada periodo retroactivo asignado en `membershipNumber`.

Cree un &quot;Esquema de Decile de Lealtad de Aerolíneas&quot; para crear un conjunto de datos decimal mediante el servicio de Consulta.

![Diagrama del esquema de Decile de Lealtad de la Aerolínea.](../images/use-cases/airline-loyalty-decile-schema.png)

### Habilitar el esquema para el perfil de cliente en tiempo real

Los datos introducidos en el Experience Platform para su uso por el perfil del cliente en tiempo real deben cumplir los requisitos de [un esquema del Modelo de datos de experiencia (XDM) habilitado para Perfil](../../xdm/ui/resources/schemas.md). Para que un esquema esté habilitado para Profile, debe implementar la clase XDM Individual Profile o XDM ExperienceEvent .

[Habilite el esquema para utilizarlo en el perfil de cliente en tiempo real mediante la API del Registro de esquemas](../../xdm/tutorials/create-schema-api.md) o [Interfaz de usuario del Editor de esquemas](../../xdm/tutorials/create-schema-ui.md).  Encontrará instrucciones detalladas sobre cómo habilitar un esquema para Perfil en su documentación respectiva.

A continuación, cree un tipo de datos para reutilizarlo en todos los grupos de campos relacionados con decimales. La creación del grupo de campos decimales es un paso único por simulador de pruebas. También se puede reutilizar para todos los esquemas relacionados con decimales.

### Crear un área de nombres de identidad y marcarla como identificador principal {#identity-namespace}

Cualquier esquema creado para utilizarse con decimales debe tener una identidad principal asignada. Puede [definición de un campo de identidad en la interfaz de usuario de Adobe Experience Platform schemas](../../xdm/ui/fields/identity.md#define-an-identity-field)o a través de la variable [API del Registro de esquemas](../../xdm/api/descriptors.md#create).

El servicio de consulta también le permite establecer una identidad o una identidad principal para los campos de conjuntos de datos de esquema específicos directamente a través de SQL. Consulte la documentación sobre [definición de identidad secundaria e identidad principal en identidades de esquema ad hoc](../data-governance/ad-hoc-schema-identities.md) para obtener más información.

### Crear una consulta para calcular decimales durante un periodo retroactivo {#create-a-query}

En el siguiente ejemplo se muestra la consulta SQL para calcular un decil durante un periodo retroactivo.

Se puede crear una plantilla mediante el Editor de consultas de la interfaz de usuario o a través del [API del servicio de consulta](../api/query-templates.md#create-a-query-template).

```sql
CREATE TABLE AS airline_loyality_decile 
{  WITH summed_miles_1 AS (
        SELECT _profilefoundationreportingstg.membershipNumber AS membershipNumber,
            _profilefoundationreportingstg.loyaltyStatus AS loyaltyStatus,
            SUM(_profilefoundationreportingstg.mileage) AS totalMiles
        FROM airline_loyalty_data
        WHERE _profilefoundationreportingstg.transactionDate < (MAKE_DATE(YEAR(CURRENT_DATE), MONTH(CURRENT_DATE), 1) - MAKE_YM_INTERVAL(0, 0))
    GROUP BY 1,2
    ),
    summed_miles_3 AS (
        SELECT _profilefoundationreportingstg.membershipNumber AS membershipNumber,
            _profilefoundationreportingstg.loyaltyStatus AS loyaltyStatus,
            SUM(_profilefoundationreportingstg.mileage) AS totalMiles
        FROM airline_loyalty_data
        WHERE _profilefoundationreportingstg.transactionDate < (MAKE_DATE(YEAR(CURRENT_DATE), MONTH(CURRENT_DATE), 1) - MAKE_YM_INTERVAL(0, 1))
    GROUP BY 1,2
    ),
    summed_miles_6 AS (
        SELECT _profilefoundationreportingstg.membershipNumber AS membershipNumber,
            _profilefoundationreportingstg.loyaltyStatus AS loyaltyStatus,
            SUM(_profilefoundationreportingstg.mileage) AS totalMiles
        FROM airline_loyalty_data
        WHERE _profilefoundationreportingstg.transactionDate < (MAKE_DATE(YEAR(CURRENT_DATE), MONTH(CURRENT_DATE), 1) - MAKE_YM_INTERVAL(0, 4))
    GROUP BY 1,2
    ),
    rankings_1 AS (
        SELECT membershipNumber,
            loyaltyStatus,
            totalMiles,
            NTILE(10) OVER (PARTITION BY loyaltyStatus ORDER BY totalMiles DESC) AS decileBucket
        FROM summed_miles_1
    ),
    rankings_3 AS (
        SELECT membershipNumber,
            loyaltyStatus,
            totalMiles,
            NTILE(10) OVER (PARTITION BY loyaltyStatus ORDER BY totalMiles DESC) AS decileBucket
        FROM summed_miles_3
    ),
    rankings_6 AS (
        SELECT membershipNumber,
            loyaltyStatus,
            totalMiles,
            NTILE(10) OVER (PARTITION BY loyaltyStatus ORDER BY totalMiles DESC) AS decileBucket
        FROM summed_miles_6
    ),
    map_1 AS (
        SELECT membershipNumber,
            MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonth1
        FROM rankings_1
        GROUP BY membershipNumber
    ),
    map_3 AS (
        SELECT membershipNumber,
            MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonth3
        FROM rankings_3
        GROUP BY membershipNumber
    ),
    map_6 AS (
        SELECT membershipNumber,
            MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonth6
        FROM rankings_6
        GROUP BY membershipNumber
    ),
    all_memberships AS (
        SELECT DISTINCT _profilefoundationreportingstg.membershipNumber AS membershipNumber FROM airline_loyalty_data
    )
    SELECT STRUCT(
            all_memberships.membershipNumber AS membershipNumber,
            STRUCT(
                    map_1.decileMonth1 AS decileMonth1,
                    map_3.decileMonth3 AS decileMonth3,
                    map_6.decileMonth6 AS decileMonth6
            ) AS decilesMileage
        ) AS _profilefoundationreportingstg
    FROM all_memberships
        LEFT JOIN map_1 ON  (all_memberships.membershipNumber = map_1.membershipNumber)
        LEFT JOIN map_3 ON  (all_memberships.membershipNumber = map_3.membershipNumber)
        LEFT JOIN map_6 ON  (all_memberships.membershipNumber = map_6.membershipNumber)
    }
```

### Revisión de consulta

Las secciones de la consulta de ejemplo se examinan en bueno detalle a continuación.

#### Periodos retroactivos

El tipo de datos de decimales contiene un bloque para retrospectivas de 1, 3, 6, 9, 12 y duración. La consulta utiliza los periodos retroactivos de 1, 3 y 6 meses, por lo que cada sección contendrá algunas consultas &quot;repetidas&quot; para crear tablas temporales para cada periodo retroactivo.

>[!NOTE]
>
>Si los datos de origen no tienen una columna que se pueda usar para determinar un período retroactivo, todas las clasificaciones de clases decimales se realizarán en `decileMonthAll`.

#### Agregación

Utilice expresiones de tabla comunes (CTE) para sumar el kilometraje antes de crear bloques de decimales. Esto proporciona el total de millas para un período retroactivo específico. Los CTE existen temporalmente y solo se pueden utilizar dentro del ámbito de la consulta más grande.

```sql
summed_miles_1 AS (
    SELECT _profilefoundationreportingstg.membershipNumber AS membershipNumber,
           _profilefoundationreportingstg.loyaltyStatus AS loyaltyStatus,
           SUM(_profilefoundationreportingstg.mileage) AS totalMiles
    FROM airline_loyalty_data
    WHERE _profilefoundationreportingstg.transactionDate < (MAKE_DATE(YEAR(CURRENT_DATE), MONTH(CURRENT_DATE), 1) - MAKE_YM_INTERVAL(0, 0))
    GROUP BY 1,2
)
```

El bloque se repite dos veces en la plantilla (`summed_miles_3` y `summed_miles_6`) con un cambio en el cálculo de fechas para generar los datos de los demás periodos retroactivos.

Es importante tener en cuenta las columnas de identidad, dimensión y métrica de la consulta (`membershipNumber`, `loyaltyStatus` y `totalMiles` respectivamente).

#### Clasificación

Los deciles permiten realizar bloques categóricos. Para crear el número de clasificación, la variable `NTILE` se utiliza con un parámetro de `10` dentro de una VENTANA agrupada por la variable `loyaltyStatus` campo . Esto resulta en una clasificación del 1 al 10. Configure las variables `ORDER BY` de `WINDOW` a `DESC` para garantizar un valor de clasificación de `1` se da a la variable **bueno** dentro de la dimensión.

```sql
rankings_1 AS (
    SELECT membershipNumber,
           loyaltyStatus,
           totalMiles,
           NTILE(10) OVER (PARTITION BY loyaltyStatus ORDER BY totalMiles DESC) AS decileBucket
    FROM summed_miles_1
)
```

#### Agregación de mapas

Con varios períodos retrospectivos, debe crear los mapas de bloques decimales de antemano utilizando la variable `MAP_FROM_ARRAYS` y `COLLECT_LIST` funciones. En el fragmento de ejemplo, `MAP_FROM_ARRAYS` crea un mapa con un par de claves (`loyaltyStatus`) y valores (`decileBucket`). `COLLECT_LIST` devuelve una matriz con todos los valores de la columna especificada.

```sql
map_1 AS (
    SELECT membershipNumber,
           MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonth1
    FROM rankings_1
    GROUP BY membershipNumber
)
```

>[!NOTE]
>
>La agregación de mapas no es necesaria si la clasificación de decimales solo es necesaria durante un periodo de duración.

#### Identidades únicas

La lista de identidades únicas (`membershipNumber`) es necesario para crear una lista única de todas las suscripciones.

```sql
all_memberships AS (
    SELECT DISTINCT _profilefoundationreportingstg.membershipNumber AS membershipNumber FROM airline_loyalty_data
)
```

>[!NOTE]
>
>Si la clasificación de decimales solo es necesaria para un periodo de duración, este paso se puede omitir y la agregación por `membershipNumber` se puede hacer en el último paso.

#### Unir todos los datos temporales

El paso final es unir todos los datos temporales en un formulario idéntico a la estructura de los deciles del grupo de campos.

```sql
SELECT STRUCT(
           all_memberships.membershipNumber AS membershipNumber,
           STRUCT(
                map_1.decileMonth1 AS decileMonth1,
                map_3.decileMonth3 AS decileMonth3,
                map_6.decileMonth6 AS decileMonth6
           ) AS decilesMileage
       ) AS _profilefoundationreportingstg
FROM all_memberships
    LEFT JOIN map_1 ON  (all_memberships.membershipNumber = map_1.membershipNumber)
    LEFT JOIN map_3 ON  (all_memberships.membershipNumber = map_3.membershipNumber)
    LEFT JOIN map_6 ON  (all_memberships.membershipNumber = map_6.membershipNumber)
```

Si solo están disponibles los datos de duración, la consulta aparecerá de la siguiente manera:

```sql
SELECT STRUCT(
           rankings.membershipNumber AS membershipNumber,
           STRUCT(
                MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonthAll
           ) AS decilesMileage
       ) AS _profilefoundationreportingstg
FROM rankings
GROUP BY rankings.membershipNumber
```

En los resultados de la consulta se garantiza una correlación entre el número de clasificación y el percentil debido al uso de decimales. Cada clasificación equivale al 10 %, por lo que la identificación de una audiencia basada en el 30 % superior solo necesita dirigirse a las clasificaciones 1, 2 y 3.

### Ejecutar la plantilla de consulta

Ejecute la consulta para rellenar el conjunto de datos decimal. También puede guardar la consulta como una plantilla y programarla para que se ejecute en una cadencia. Cuando se guarda como plantilla, la consulta también se puede actualizar para utilizar el patrón de creación e inserción que hace referencia a la variable `table_exists` comando. Más información sobre cómo usar la variable `table_exists`se puede encontrar en el [Guía de sintaxis SQL](../sql/syntax.md#table-exists).

## Pasos siguientes

El caso de uso de ejemplo que se proporciona más arriba resalta los pasos para que los atributos decimales estén disponibles en el Perfil del cliente en tiempo real. Esto permite que el servicio de segmentación, ya sea a través de una interfaz de usuario o de la API RESTful, pueda generar audiencias basadas en estos bloques decimales. Consulte la [Información general del servicio de segmentación](../../segmentation/home.md) para obtener información sobre cómo crear, evaluar y acceder a segmentos.
