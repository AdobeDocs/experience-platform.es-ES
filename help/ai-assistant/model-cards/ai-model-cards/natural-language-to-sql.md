---
title: Tarjeta de modelo de lenguaje natural a SQL del Asistente de IA
description: Obtenga información sobre el modelo de IA Assistant Natural Language to SQL AI.
hide: true
hidefromtoc: true
source-git-commit: 70b705a7c6df24ad9549c46832ff4898253670ac
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Tarjeta modelo de lenguaje natural a SQL de AI Assistant Operational Insights

## Información general del modelo {#model-overview}

* El nombre oficial del modelo es AI Assistant Operational Insights Natural Language to SQL Model ([!DNL NL2SQL]) y se publicó en su última versión de GA en febrero de 2025.
* El modelo está diseñado para traducir consultas en lenguaje natural de los clientes sobre perspectivas operativas en consultas SQL. Estas consultas SQL se ejecutan a través del gráfico de conocimientos de Adobe Experience Platform, que contiene metadatos sobre las entidades Experience Platform de los clientes, como esquemas, conjuntos de datos, audiencias, destinos y recorridos. A continuación, los resultados de las consultas SQL se utilizan para generar respuestas a las preguntas originales del lenguaje natural de los clientes.
* Los usuarios principales de este modelo son los profesionales de marketing, los analistas de datos o los administradores de recorrido de clientes, que buscan comprender las perspectivas operativas dentro de Experience Platform y actuar en consecuencia utilizando un lenguaje natural. Es posible que no sean expertos en SQL o ingeniería de datos, pero necesitan respuestas rápidas y precisas sobre sus entidades de Experience Platform para tomar decisiones informadas y optimizar las experiencias de los clientes.
* Este modelo forma parte del Asistente de IA para perspectivas operativas, donde ayuda a los usuarios a acceder a los metadatos sobre sus entidades de Experience Platform, como audiencias, recorridos, esquemas, atributos, conjuntos de datos y destinos. Los usuarios pueden hacer preguntas en lenguaje natural (como qué audiencias se activan o qué audiencias utilizan un esquema específico) y el modelo las traduce en consultas SQL a través del gráfico de conocimiento de Experience Platform. Esto permite a los usuarios obtener rápidamente visibilidad operativa y tomar decisiones informadas sin necesidad de explorar o consultar manualmente el sistema.
* Este modelo aborda los principales problemas a los que se enfrentan los usuarios y analistas empresariales que trabajan con Experience Platform, como la complejidad de navegar por grandes volúmenes de metadatos interconectados, la necesidad de escribir manualmente consultas SQL para recuperar perspectivas operativas y la falta de visibilidad sobre cómo se conectan o funcionan entidades de Experience Platform como audiencias, conjuntos de datos y recorridos. Al permitir el acceso a los metadatos mediante lenguaje natural y automatizar la generación de SQL, el modelo reduce la dependencia en los recursos técnicos, acorta el tiempo de detección de insight y permite a los usuarios tomar decisiones más rápidas basadas en datos.
* El modelo no debe utilizarse para acceder a Información de identificación personal (PII) o deducirla, como nombres de clientes, direcciones de correo electrónico o números de teléfono, aunque dichos datos existan en la plataforma.
* Además, no se debe confiar en él para las comprobaciones de cumplimiento o de gobernanza, como la validación de políticas de retención de datos, reglas de control de acceso o el estado de consentimiento. Estas tareas requieren sistemas y estrategias especializados.

## Detalles del modelo {#model-details}

* El tipo de modelo es LLM Prompt con Aprendizaje dinámico en contexto.
* La entrada del modelo son consultas de lenguaje natural del usuario.
* El modelo genera consultas SQL en sintaxis [!DNL Snowflake], que se ejecutan a través de Experience Platform Knowledge Graph.

**Entrada de ejemplo**

```console
How many datasets were created within the last 10 days?
```

**Ejemplo de salida**

```SQL
SELECT
    COUNT(*) AS datasetCount 
FROM hkg_dim_dataset 
WHERE
    createdTime >= DATEADD(day, -10, CURRENT_DATE);
```

## Formación de modelo {#model-training}

* [!DNL NL2SQL] utilizó [!DNL OpenAI] modelos basados en GPT para el aprendizaje en contexto.
* El banco de preguntas [!DNL NL2SQL] contiene 428 consultas del equipo [!DNL Operational Insights] y 524 de equipos externos para casos de uso alfa.

## Evaluación de modelo {#model-evaluation}

* El modelo se evalúa con precisión. Por ejemplo, de todas las [!DNL NL2SQL] solicitudes, ¿cuántas de ellas arrojan los resultados SQL correctos?
* El proceso de evaluación es una combinación de coincidencia basada en reglas (estandarización SQL y luego coincidencia directa de cadenas SQL), solucionador SQL basado en LLM y evaluación humana
* Los conjuntos abiertos se utilizan para pruebas de regresión y los proyectos de anotación semanales supervisan el rendimiento del modelo a través del tráfico de clientes reales muestreado.
* En cuanto a la evaluación contradictoria, existe un modelo independiente dentro y fuera de ámbito que funciona como protección para [!DNL NL2SQL].

## Implementación de modelo {#model-deployment}

* El modelo LLM es un modelo basado en GPT alojado por [!DNL Azure OpenAI] API.
* El modelo base está hospedado por [!DNL Azure].
* El modelo se actualiza periódicamente, con periodicidad semanal, mediante la ampliación del banco de preguntas. El modo también se actualiza mediante nuevas estrategias de solicitud e instrucciones cuando es necesario.

## Explicabilidad {#explainability}

El modelo utiliza un modelo de explicación independiente para SQL.

## Equidad y parcialidad {#fairness-and-bias}

* Para garantizar que el modelo interprete y genere consultas de forma coherente en las distintas intenciones del usuario y variaciones lingüísticas sin introducir sesgos ni reforzar estereotipos, Adobe utiliza una auditoría rápida, explicabilidad y garantías contra la generación de resultados sesgados o poco éticos.
* La salida del modelo se ve afectada por los ejemplos de aprendizaje en contexto y por lo que el recuperador selecciona en el mensaje. Los ejemplos del banco de preguntas contienen ejemplos considerados representativos desde la perspectiva del módulo de pagos, y también estamos ampliando los bancos de preguntas en función del tráfico real de clientes.

## Solidez {#robustness}

Dado que la mayoría de las consultas que recibe no están cubiertas por el banco de preguntas, la precisión del tráfico de producción refleja la solidez del modelo.

## Consideraciones de privacidad y seguridad {#privacy-and-security-considerations}

El modelo no procesa ni conserva información de identificación personal (PII), y esa información está enmascarada para la generación de SQL. Para la comprobación de permisos de control de acceso basado en atributos, el equipo de Experience Platform Knowledge Graph procesará más el SQL generado para garantizar la calidad del control.

## Consideraciones éticas {#ethical-considerations}

Para evitar exponer PII o atributos confidenciales, el modelo se ha diseñado para admitir la privacidad, evitar reforzar los sesgos de datos existentes y respetar los límites de control de acceso. Esto incluye filtrar, etiquetar y auditar campos de esquema para el uso responsable.

