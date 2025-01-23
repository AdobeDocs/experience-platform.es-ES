---
title: Predecir la pérdida de clientes con una regresión logística basada en SQL
description: Aprenda a predecir la pérdida de clientes mediante la regresión logística basada en SQL. Esta guía cubre todo el proceso, desde la creación del modelo hasta la evaluación y la predicción. Obtenga información procesable del comportamiento de compra de los clientes para implementar estrategias de retención proactivas y optimizar las decisiones comerciales.
source-git-commit: 95c7ad3f8eb86cacd42077008824eea9e25b4db0
workflow-type: tm+mt
source-wordcount: '1126'
ht-degree: 1%

---

# Predecir la pérdida de clientes con una regresión logística basada en SQL

Predecir la pérdida de clientes ayuda a las empresas a retener clientes, optimizar recursos y aumentar la rentabilidad al mejorar la satisfacción y la lealtad a través de perspectivas procesables.

Descubra cómo utilizar la regresión logística basada en SQL para predecir la pérdida de clientes. Utilice esta completa guía SQL para transformar los datos de comercio electrónico sin procesar en perspectivas de clientes significativas basadas en métricas de comportamiento clave (como la frecuencia de compra, el valor de pedido promedio y la actualización de la última compra). El documento abarca todo el proceso, desde la preparación de datos y la ingeniería de funciones hasta la creación, evaluación y predicción de modelos.

Utilice esta guía para crear un potente modelo de predicción de pérdida que identifique a los clientes en riesgo, perfeccione las estrategias de retención e impulse mejores decisiones comerciales. Incluye instrucciones paso a paso, consultas SQL y explicaciones detalladas para ayudarle a aplicar con confianza las técnicas de aprendizaje automático dentro de su entorno de datos.

## Introducción

Antes de crear el modelo de pérdida, es importante explorar las funciones clave del cliente y los requisitos de datos. Las siguientes secciones describen los atributos esenciales del cliente y los campos de datos requeridos para una formación precisa sobre el modelo.

### Definir las funciones del cliente {#define-customer-features}

Para clasificar con precisión la pérdida, el modelo analiza los hábitos y tendencias de compra. La siguiente tabla describe las funciones clave de comportamiento del cliente utilizadas en el modelo:

| Función | Descripción |
|---------------------------|-------------------------------------------------------|
| `total_purchases` | Número total de compras realizadas por el cliente. |
| `total_revenue` | Ingresos totales generados por compras de clientes. |
| `avg_order_value` | El valor promedio de las compras de un cliente. |
| `customer_lifetime` | Número de días entre la primera y la última compra del cliente. |
| `days_since_last_purchase` | Número de días desde la última compra del cliente. |
| `purchase_frequency` | El número de meses distintos en los que el cliente realizó compras. |

### Suposiciones y campos obligatorios {#assumptions-required-fields}

Para generar predicciones de cancelación por parte del cliente, el modelo depende de los campos clave de la tabla `webevents` que capturan los detalles de transacción del cliente. El conjunto de datos debe incluir los campos siguientes:

| Campo | Descripción |
|--------------------------------|----------------------------------------------------|
| `identityMap['ECID'][0].id` | Identificador único que se utiliza para rastrear clientes entre sesiones. |
| `productListItems.priceTotal[0]` | El coste total de los artículos comprados por transacción. |
| `productListItems.quantity[0]` | Número total de artículos de una compra. |
| `timestamp` | La fecha y hora exactas de cada evento de compra. |
| `commerce.order.purchaseID` | Un valor obligatorio que confirma una compra completada. |

El conjunto de datos debe contener registros históricos estructurados de transacciones de clientes, y cada fila representa un evento de compra. Cada evento debe incluir marcas de hora en un formato de fecha y hora adecuado compatible con la función SQL `DATEDIFF` (por ejemplo, AAAA-MM-DD HH:MI:SS). Además, cada registro debe contener un identificador de Experience Cloud válido (`ECID`) en el campo `identityMap` para identificar a los clientes de forma única.

>[!TIP]
>
>El procesamiento de grandes conjuntos de datos con millones de registros puede afectar significativamente al rendimiento. Para optimizar la ejecución de la consulta, particione el conjunto de datos de experiencia por marca de tiempo, realice un procesamiento incremental mediante instantáneas y aplique funciones de agregación eficientes según sea necesario. Además, filtre los datos antes de la agregación para reducir la sobrecarga de procesamiento.

## Creación de un modelo {#create-a-model}

Para predecir la pérdida de clientes, debe crear un modelo de regresión logística basado en SQL que analice el historial de compras de clientes y las métricas de comportamiento. El modelo clasifica a los clientes como `churned` o `not churned` determinando si han realizado una compra en los últimos 90 días.

### Utilice SQL para crear el modelo de predicción de pérdida {#sql-create-model}

El modelo basado en SQL procesa los datos de `webevents` agregando métricas clave y asignando etiquetas de pérdida en función de una regla de inactividad de 90 días. Este enfoque distingue a los clientes activos de los clientes en riesgo. La consulta SQL también realiza ingeniería de funciones para mejorar la precisión del modelo y la clasificación de pérdida. Estas perspectivas permiten a su empresa implementar estrategias de retención dirigidas, reducir la pérdida y maximizar el valor de duración del cliente.

>[!NOTE]
>
>El modelo de predicción de pérdida utiliza un umbral predeterminado de 90 días para clasificar los clientes como cancelados. Para ajustar este umbral y alinearlo con los objetivos empresariales y las estrategias de retención, modifique la condición `DATEDIFF(CURRENT_DATE, MAX(timestamp)) > 90` en las consultas SQL.

Utilice la siguiente instrucción SQL para crear el modelo `retention_model_logistic_reg` con las características y etiquetas especificadas:

```sql
CREATE MODEL retention_model_logistic_reg
TRANSFORM (
  vector_assembler(array(total_purchases, total_revenue, avg_order_value, customer_lifetime, days_since_last_purchase, purchase_frequency)) features
  -- Combines selected customer metrics into a feature vector for model training
)
OPTIONS (
  MODEL_TYPE = 'logistic_reg',  -- Specifies logistic regression as the model type
  LABEL = 'churned'             -- Defines the target label for churn classification
)
AS
WITH customer_features AS (
    SELECT
       identityMap['ECID'][0].id AS customer_id,  -- Extract the unique customer ID from identityMap
       AVG(COALESCE(productListItems.priceTotal[0], 0)) AS avg_order_value,  -- Calculates the average order value, and handles null values with COALESCE
       SUM(COALESCE(productListItems.priceTotal[0], 0)) AS total_revenue, -- The sum of all purchase values per customer
       COUNT(COALESCE(productListItems.quantity[0], 0)) AS total_purchases,  -- The total number of items purchased by the customer
       DATEDIFF(MAX(timestamp), MIN(timestamp)) AS customer_lifetime,  -- The days between first and last recorded purchase
       DATEDIFF(CURRENT_DATE, MAX(timestamp)) AS days_since_last_purchase,  -- The days since the last purchase event
       COUNT(DISTINCT CONCAT(YEAR(timestamp), MONTH(timestamp))) AS purchase_frequency  -- The count of unique months with purchases
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0)  -- Filters transactions with valid total price
      AND commerce.`order`.purchaseID <> ''  -- Ensures the order has a valid purchase ID
    GROUP BY customer_id 
),
customer_labels AS (
    SELECT
      identityMap['ECID'][0].id AS customer_id,  -- Extract the unique customer ID for labeling
      CASE
          WHEN DATEDIFF(CURRENT_DATE, MAX(timestamp)) > 90 THEN 1  -- Marks the customer as churned if no purchase occurred in the last 90 days
          ELSE 0
      END AS churned
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0) 
      AND commerce.`order`.purchaseID <> ''  
    GROUP BY customer_id  
)
SELECT
    f.customer_id,
    f.total_purchases,
    f.total_revenue,
    f.avg_order_value,
    f.customer_lifetime,
    f.days_since_last_purchase,
    f.purchase_frequency,
    l.churned
FROM
    customer_features f
JOIN
    customer_labels l
ON f.customer_id = l.customer_id  -- Join features with churn labels
ORDER BY RANDOM()  -- Shuffles rows randomly for training
LIMIT 500000;  -- Limit the dataset to 500,000 rows for model training
```

### Salida de modelo {#model-output}

El conjunto de datos de salida contiene métricas relacionadas con el cliente y su estado de cancelación. Cada fila representa un cliente, sus valores de funciones y su estado de pérdida. Puede utilizar este resultado para analizar el comportamiento de los clientes, entrenar modelos predictivos y desarrollar estrategias de retención dirigidas para retener a los clientes en riesgo. A continuación se muestra un ejemplo de tabla de salida:

```console
 customer_id  | total_purchases | total_revenue | avg_order_value  | customer_lifetime | days_since_last_purchase | purchase_frequency | churned |
--------------+-----------------+---------------+------------------+-------------------+--------------------------+--------------------+----------
  100001      | 25              | 1250.00       | 50.00            | 540               | 20                       | 10                 | 0       
  100002      | 3               | 90.00         | 30.00            | 120               | 95                       | 1                  | 1       
  100003      | 60              | 7200.00       | 120.00           | 800               | 5                        | 24                 | 0       
  100004      | 15              | 750.00        | 50.00            | 365               | 60                       | 8                  | 0       
  100005      | 1               | 25.00         | 25.00            | 60                | 180                      | 1                  | 1       
```

| Columna | Descripción |
|-----------|------------------------------------------------------------------------------------|
| `churned` | El valor indica si el cliente realizó una compra en los últimos 90 días (0 = no cancelada, 1 = cancelada). |

## Usar SQL para evaluar el modelo {#model-evaluation}

A continuación, evalúe el modelo de predicción de pérdida para determinar su eficacia en la identificación de clientes en riesgo. Evalúe el rendimiento del modelo con métricas clave que midan la precisión y la fiabilidad.

Para medir la precisión del modelo `retention_model_logistic_reg` en la predicción de la pérdida de clientes, use la función `model_evaluate`. El siguiente ejemplo SQL evalúa el modelo mediante un conjunto de datos estructurado como los datos de aprendizaje:

```sql
SELECT * 
FROM model_evaluate(retention_model_logistic_reg, 1,
WITH customer_features AS (
    SELECT
       identityMap['ECID'][0].id AS customer_id,
       AVG(COALESCE(productListItems.priceTotal[0], 0)) AS avg_order_value,
       SUM(COALESCE(productListItems.priceTotal[0], 0)) AS total_revenue,
       COUNT(COALESCE(productListItems.quantity[0], 0)) AS total_purchases, 
       DATEDIFF(MAX(timestamp), MIN(timestamp)) AS customer_lifetime,
       DATEDIFF(CURRENT_DATE, MAX(timestamp)) AS days_since_last_purchase,
       COUNT(DISTINCT CONCAT(YEAR(timestamp), MONTH(timestamp))) AS purchase_frequency 
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0)
      AND commerce.`order`.purchaseID <> ''
    GROUP BY customer_id
),
customer_labels AS (
    SELECT
      identityMap['ECID'][0].id AS customer_id,
      CASE
          WHEN DATEDIFF(CURRENT_DATE, MAX(timestamp)) > 90 THEN 1 
          ELSE 0
      END AS churned
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0) 
      AND commerce.`order`.purchaseID <> '' 
    GROUP BY customer_id
)
SELECT
    f.customer_id,
    f.total_purchases,
    f.total_revenue,
    f.avg_order_value,
    f.customer_lifetime,
    f.days_since_last_purchase,
    f.purchase_frequency,
    l.churned
FROM
    customer_features f
JOIN
    customer_labels l
ON f.customer_id = l.customer_id); -- Joins customer features with churn labels
```

### Resultado de evaluación del modelo

El resultado de la evaluación incluye métricas de rendimiento clave, como AUC-ROC, precisión, precisión y recuperación. Estas métricas proporcionan perspectivas sobre la eficacia del modelo que puede utilizar para refinar las estrategias de retención y tomar decisiones basadas en datos.

>[!NOTE]
>
>Los valores de rendimiento varían de 0 a 1, donde 1,0 representa un rendimiento perfecto.

```console
 auc_roc | accuracy | precision | recall 
---------+----------+-----------+--------
1        | 0.99998  |  1        |  1      
```

| Métrica | Descripción |
|------------|-------------------------------------------------------------------------|
| `auc_roc` | Esta métrica indica la capacidad del modelo para distinguir entre clientes cancelados y no cancelados. Un valor más cercano a 1 indica un mejor rendimiento. |
| `accuracy` | La métrica de precisión representa la proporción de predicciones correctas, lo que proporciona una medida general del rendimiento del modelo. |
| `precision` | La precisión muestra la proporción de clientes cancelados correctamente identificados e indica fiabilidad en la predicción de pérdida. Un valor alto significa menos falsos positivos. |
| `recall` | Recall mide la capacidad del modelo para identificar todos los clientes reales que se pierden. Un valor de recuperación alto indica menos clientes de pérdida perdidos. |

>[!NOTE]
>
>Las puntuaciones casi perfectas en este ejemplo son para fines de demostración. En la práctica, los datos del mundo real pueden arrojar valores más bajos debido al ruido y la variabilidad.

## Predicción de modelo {#model-prediction}

Una vez evaluado el modelo, utilice `model_predict` para aplicarlo a un nuevo conjunto de datos y predecir la pérdida del cliente. Puede utilizar estas predicciones para identificar a los clientes en riesgo e implementar estrategias de retención dirigidas.

### Usar SQL para generar predicciones de pérdida {#sql-model-predict}

La consulta SQL siguiente utiliza el modelo `retention_model_logistic_reg` para predecir la pérdida de clientes con un conjunto de datos estructurado como los datos de formación:

```sql
SELECT * 
FROM model_predict(retention_model_logistic_reg, 1,  -- Applies the trained model for churn prediction
WITH customer_features AS (
    SELECT
       identityMap['ECID'][0].id AS customer_id,
       AVG(COALESCE(productListItems.priceTotal[0], 0)) AS avg_order_value,  
       SUM(COALESCE(productListItems.priceTotal[0], 0)) AS total_revenue, 
       COUNT(COALESCE(productListItems.quantity[0], 0)) AS total_purchases,  
       DATEDIFF(MAX(timestamp), MIN(timestamp)) AS customer_lifetime,  
       DATEDIFF(CURRENT_DATE, MAX(timestamp)) AS days_since_last_purchase,  
       COUNT(DISTINCT CONCAT(YEAR(timestamp), MONTH(timestamp))) AS purchase_frequency  
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0)  -- Ensures only valid purchase data is considered
      AND commerce.`order`.purchaseID <> ''  
    GROUP BY customer_id
),
customer_labels AS (
    SELECT
      identityMap['ECID'][0].id AS customer_id,  
      CASE
          WHEN DATEDIFF(CURRENT_DATE, MAX(timestamp)) > 90 THEN 1  -- Identify customers who have not purchased in the last 90 days
          ELSE 0
      END AS churned
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0)  
      AND commerce.`order`.purchaseID <> ''  
    GROUP BY customer_id
)
SELECT
    f.customer_id,  
    f.total_purchases,  
    f.total_revenue,  
    f.avg_order_value,  
    f.customer_lifetime,  
    f.days_since_last_purchase,  
    f.purchase_frequency,  
    l.churned  
FROM
    customer_features f
JOIN
    customer_labels l
ON f.customer_id = l.customer_id);  -- Matches features with their churn labels for prediction
```

### Salida de predicción de modelo {#prediction-output}

El conjunto de datos de salida incluye funciones clave del cliente y su estado de cancelación previsto, lo que indica si es probable que un cliente se produzca. Utilice estas perspectivas para implementar estrategias de retención proactivas y reducir la pérdida de clientes.

```console
 total_purchases | total_revenue | avg_order_value | customer_lifetime | days_since_last_purchase | purchase_frequency | churned | prediction
-----------------+---------------+-----------------+-------------------+--------------------------+--------------------+---------+------------
 2               | 299           | 149.5           | 0                 | 13                        | 1                  | 0       | 0
 1               | 710           | 710.00          | 0                 | 149                       | 1                  | 1       | 1
 1               | 19.99         | 19.99           | 0                 | 30                        | 1                  | 0       | 0
 1               | 4528          | 4528.00         | 0                 | 26                        | 1                  | 0       | 0
 1               | 21.84         | 21.84           | 0                 | 90                        | 1                  | 0       | 0
 1               | 16.64         | 16.64           | 0                 | 268                       | 1                  | 1       | 1
```

| Columna | Descripción |
|---------------|-------------------------------------------------------------------------------|
| `prediction` | El estado de cancelación previsto por el cliente en función del modelo (0 = no cancelado, 1 = cancelado). |

## Pasos siguientes

Ahora ha aprendido a crear, evaluar y utilizar un modelo basado en SQL para predecir la pérdida de clientes. Con esta base, puede analizar el comportamiento de los clientes, identificar a los clientes en riesgo e implementar estrategias de retención proactivas para mejorar la retención de clientes. Para mejorar y aplicar aún más el modelo de predicción de pérdida, tenga en cuenta los siguientes pasos:

- Automatice el proceso: Integre el modelo en una canalización de datos para una monitorización continua y perspectivas en tiempo real. [Explore cómo comprobar y procesar conjuntos de datos con SQL](../../../dashboards/query.md).
- Monitorizar el rendimiento del modelo: evalúe continuamente el modelo con nuevos datos para mantener la precisión y la relevancia.  Use el [Asistente de IA](../../../ai-assistant/landing.md) en la interfaz de usuario de Adobe Experience Platform para monitorizar los cambios clave de rendimiento y [pronosticar las tendencias de audiencia](../../../ai-assistant/new-features/audience-forecasting.md).
