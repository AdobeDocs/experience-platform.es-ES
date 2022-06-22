---
title: Atributos derivados
description: Los atributos derivados le permiten calcular atributos en una cadencia normal y, opcionalmente, publicar estos atributos derivados en Perfil del cliente en tiempo real como atributos de perfil. Este documento proporciona información general sobre cómo utilizar el servicio de consulta para crear atributos derivados para usarlos con los datos de perfil.
source-git-commit: 72e157e0a6310ebf2f55205b03b60600a56e3cf6
workflow-type: tm+mt
source-wordcount: '1650'
ht-degree: 1%

---

# Atributos derivados

Los atributos derivados le permiten calcular atributos en una cadencia normal y, opcionalmente, publicar estos atributos derivados en Perfil del cliente en tiempo real como atributos de perfil.

Los atributos derivados, como los creados con datos decimales, son necesarios para una variedad de casos de uso que analizan datos de perfil. Con los datos decimales puede crear audiencias a partir de segmentos en función de su percentil o clasificación de un atributo determinado. Por ejemplo, los casos de uso potenciales podrían incluir:

* Identificación del 10 % más bajo de suscriptores en función de la audiencia por canal. Esto permitiría a los especialistas en marketing dirigirse a una audiencia concreta y vender un nuevo paquete de suscriptores.
* Identificar una audiencia que se encuentra en el 10% superior de los folletos en función de sus millas totales recorridas y que tiene el estado &quot;Volante&quot;. Esta audiencia podría utilizarse para dirigirse selectivamente a la venta de una nueva oferta de tarjeta de crédito.

## Primeros pasos

Esta descripción general requiere una comprensión práctica de [Llamadas de API de plataforma](../landing/api-guide.md) y los siguientes componentes de Adobe Experience Platform:

* [Resumen del perfil del cliente en tiempo real](../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.
* [Aspectos básicos de la composición del esquema](../xdm/schema/composition.md): Introducción a los esquemas del Modelo de datos de experiencia (XDM) y a los componentes, principios y prácticas recomendadas para la composición de esquemas.
* [Habilitación de un esquema para el perfil del cliente en tiempo real](../profile/tutorials/add-profile-data.md): Este tutorial describe los pasos necesarios para agregar datos al perfil del cliente en tiempo real.

## Compatibilidad con SQL para atributos derivados

Para definir la clasificación de los decimales en función de una dimensión (categoría) en particular y una métrica correspondiente (ingresos, puntos, duración de la audiencia, etc.), se debe diseñar un esquema para permitir la creación de bloques de decimales. Este esquema se puede utilizar como parte del esquema de perfil más grande.

### Creación de un área de nombres de identidad para el esquema de perfil {#identity-namespace}

Las áreas de nombres de identidad son un componente de [Identity Service de ](../identity-service/home.md) que sirve de indicadores del contexto al que se relaciona una identidad. Una identidad completa incluye un valor de ID y un área de nombres. Al hacer coincidir y combinar datos de registro entre fragmentos de perfil, tanto el valor de identidad como el espacio de nombres deben coincidir.

Los conjuntos de datos creados relacionados con la identidad se pueden agrupar como grupos de datos y ayudar a mantener el ciclo de vida de los datos. Las áreas de nombres personalizadas se pueden crear utilizando la variable [API del servicio de identidad](../identity-service/api/create-custom-namespace.md) o a través de la interfaz de usuario. Consulte la [administración de la documentación de las áreas de nombres personalizadas](../identity-service/namespaces.md#manage-namespaces) para obtener instrucciones sobre cómo hacerlo mediante la interfaz de usuario de .

El descriptor de identidad principal se puede asignar a un campo de la interfaz de usuario de Esquemas o se puede crear mediante la API de registro de esquemas. Consulte la documentación para obtener instrucciones sobre cómo [definición de un campo de identidad en la interfaz de usuario de Adobe Experience Platform](../xdm/ui/fields/identity.md#define-an-identity-field)o a través de la variable [API del Registro de esquemas](../xdm/api/descriptors.md#create).

El servicio de consulta también le permite establecer una identidad o una identidad principal para los campos de conjuntos de datos de esquema específicos directamente a través de SQL. Consulte la documentación sobre [definición de identidad secundaria e identidad principal en identidades de esquema ad hoc](./data-governance/ad-hoc-schema-identities.md) para obtener más información.

## Crear atributos derivados

La consulta de ejemplo proporcionada en este documento se centra en los deciles para categorizar grandes conjuntos de datos y clasificar los datos de los valores más altos a los más bajos (o viceversa), y filtrar según el periodo de tiempo.

### Deciles {#deciles}

Un decil es un método para dividir un conjunto de datos clasificados en 10 partes iguales. Cuando los datos se dividen en decimales, se asigna una clasificación de decimales a cada fila del conjunto de datos. Esto permite ordenar los datos en orden descendente o ascendente.

Una clasificación de decimales organiza los datos en orden de menor a mayor y se realiza en una escala del 1 al 10, donde cada número sucesivo corresponde a un aumento de 10 puntos porcentuales.

Los bloques de decimales representan el número de grupos clasificados y se utilizan para asignar una clasificación a una dimensión (categoría) del conjunto de datos. El bloque puede ser un número o una expresión que se evalúa como un valor entero positivo para cada partición. Los bloques no deben tener un valor nulo.

Los cuartiles se utilizan para dividir la distribución por cuatro y los percentiles por 100.

### Creación del esquema para bloques de decimales {#create-schema}

El esquema creado para los bloques de decimales tiene tres partes integrales: un tipo de datos, un grupo de campos para el tipo de datos (por conjunto de datos de origen) y un campo de identidad principal.

>[!NOTE]
>
>Debe crearse un área de nombres de identidad para poder crear el esquema. Consulte la [área de nombres de identidad](#identity-namespace) para obtener más información.

Adobe proporciona varias clases XDM estándar (&quot;core&quot;), incluidos XDM Individual Profile y XDM ExperienceEvent. Además de estas clases principales, también puede crear sus propias clases personalizadas para describir casos de uso más específicos para su organización. Consulte las guías sobre cómo [crear y editar esquemas en la interfaz de usuario](../xdm/ui/resources/schemas.md#create) o utilizando [extremo schemas en la API del Registro de esquemas](../xdm/api/schemas.md#create) para obtener más información.

Los datos que se están incorporando en el Experience Platform para su uso en el Perfil del cliente en tiempo real deben cumplir un esquema del Modelo de datos de experiencia (XDM) habilitado para Perfil. Para que un esquema esté habilitado para Profile, debe implementar la clase XDM Individual Profile o XDM ExperienceEvent .

Puede [activar un esquema para utilizarlo en el perfil del cliente en tiempo real mediante la API del Registro de esquemas](../xdm/tutorials/create-schema-api.md) o [Interfaz de usuario del Editor de esquemas](../xdm/tutorials/create-schema-ui.md).  Encontrará instrucciones detalladas sobre cómo habilitar un esquema para Perfil en su documentación respectiva.

### Crear un tipo de datos {#create-data-type}

Los tipos de datos se utilizan como campos de referencia en clases o grupos de campos de esquema y permiten el uso coherente de una estructura de varios campos que se puede incluir en cualquier parte del esquema. La creación del tipo de datos es un paso único por simulador de pruebas, ya que se puede reutilizar para todos los grupos de campos relacionados con decimales.

Consulte la documentación para obtener instrucciones sobre cómo [definir un tipo de datos personalizado](../xdm/api/data-types.md) usando la variable [API del Registro de esquemas](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

### Creación del grupo de campos de deciles {#create-field-group}

La creación del grupo de campos es un paso único por simulador de pruebas. También se puede reutilizar para todos los esquemas relacionados con decimales.

Consulte la documentación para obtener instrucciones sobre cómo [crear grupos de campos a través de la interfaz de usuario](../xdm/ui/resources/field-groups.md#create)

## Utilizar el servicio de consulta para crear deciles

El servicio de consulta proporciona una manera ideal de crear un conjunto de datos que contenga deciles categóricos. Esto se puede utilizar junto con el servicio de segmentación para crear audiencias basadas en la clasificación de atributos.

Los conceptos mostrados en los ejemplos siguientes se pueden aplicar para crear otros conjuntos de datos de bloque de deciles, siempre y cuando se defina una categoría (dimensión) y haya una métrica disponible. Los ejemplos se basan en datos de un esquema de lealtad de aerolíneas. Los datos de lealtad de la aerolínea utilizan la clase de eventos de experiencia, en la que cada evento es un registro de una transacción comercial para **kilometraje**, ya sea acreditado o adeudado, y **estado de lealtad** &quot;Volante&quot;, &quot;Frecuente&quot;, &quot;Plata&quot; o &quot;Oro&quot;. El campo de identidad principal es `membershipNumber`.

### Creación de una plantilla de consulta {#create-a-query-template}

La plantilla se puede crear mediante el Editor de consultas de la interfaz de usuario o a través del [API del servicio de consulta](./api/query-templates.md#create-a-query-template).

Las secciones de la plantilla de consulta que se muestran a continuación se examinarán en bueno detalle.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/query/query-templates \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
         "name": "Airline Loyalty Deciles Insert into profile",
         "sql":
            "WITH summed_miles_1 AS (
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
                LEFT JOIN map_6 ON  (all_memberships.membershipNumber = map_6.membershipNumber)"
        }'
```

#### Períodos retroactivos

El tipo de datos de decimales contiene un bloque para retrospectivas de 1, 3, 6, 9, 12 y duración. La consulta utiliza los períodos retrospectivos de 1, 3 y 6 meses, por lo que cada sección contendrá algunas consultas &quot;repetidas&quot; para crear tablas temporales para cada período retrospectivo.

>[!NOTE]
>
>Si los datos de origen no tienen una columna que pueda utilizarse para determinar un período retroactivo, todas las clasificaciones de clases decimales se realizarán en `decileMonthAll`.

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

Tenga en cuenta las columnas de identidad, dimensión y métrica para la consulta (`membershipNumber`, `loyaltyStatus` y `totalMiles` respectivamente).

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

Con varios períodos retrospectivos, debe crear los mapas de cubos de deciles de antemano utilizando la variable `MAP_FROM_ARRAYS` y `COLLECT_LIST` funciones. En el fragmento de ejemplo, `MAP_FROM_ARRAYS` crea un mapa con un par de claves (`loyaltyStatus`) y valores (`decileBucket`). `COLLECT_LIST` devuelve una matriz con todos los valores de la columna especificada.

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

### Ejecutar la plantilla de consulta

Las consultas pueden [se ejecuta a través de la interfaz de usuario de](./ui/user-guide.md#executing-queries) o [API del servicio de consulta](./api/queries.md#create-a-query).

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/query/queries \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "dbName": "prod:all",
    "templateId": "{{airline_decile_query_template_id}}",
    "insertIntoParameters": {
        "datasetName": "airline_loyalty_decile"
    }
}'
```

En los resultados de la consulta se garantiza una correlación entre el número de clasificación y el percentil debido al uso de decimales. Cada clasificación equivale al 10 %, por lo que la identificación de una audiencia basada en el 30 % superior solo necesita dirigirse a las clasificaciones 1, 2 y 3.

## Pasos siguientes

El servicio de segmentación proporciona una interfaz de usuario y una API de RESTful que le permiten generar audiencias basadas en estos bloques de decimales. Consulte la [Información general del servicio de segmentación](../segmentation/home.md) para obtener información sobre cómo crear, evaluar y acceder a segmentos.

Para obtener información detallada sobre cómo crear y utilizar segmentos en el Generador de segmentos (la implementación de la interfaz de usuario del servicio de segmentación), consulte la [Guía del Generador de segmentos](../segmentation/ui/overview.md).

Para obtener información sobre la creación de definiciones de segmentos mediante la API, consulte el tutorial sobre [creación de segmentos de audiencia mediante la API](../segmentation/tutorials/create-a-segment.md).
