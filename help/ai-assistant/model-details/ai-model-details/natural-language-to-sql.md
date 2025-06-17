---
title: Detalles del modelo de lenguaje natural a SQL del Asistente de IA
description: Obtenga información sobre el modelo de IA Assistant Natural Language to SQL AI.
exl-id: ca157945-5f74-45d0-9d40-c65d09a8e80d
source-git-commit: 3d870c367317d73bba8b75b38f7b2a93ab6b5bbd
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 0%

---

# Detalles del modelo de lenguaje natural a SQL de AI Assistant Operational Insights

>[!IMPORTANT]
>
>Adobe está publicando activamente más detalles del modelo; se agregará documentación adicional a Experience League a medida que esté disponible.

## Información general del modelo {#model-overview}

* **Nombre y versión del modelo**: Adobe Experience Platform AI Assistant Operational Insights Natural Language to SQL Model ([!DNL NL2SQL]).
* **Fecha de la versión del modelo**: febrero de 2025
* **Propósito del modelo**: El modelo está diseñado para traducir las consultas de lenguaje natural de los clientes acerca de perspectivas operativas en consultas SQL. Estas consultas SQL se ejecutan a través del gráfico de conocimientos de Adobe Experience Platform, que contiene metadatos sobre las entidades Experience Platform de los clientes, como esquemas, conjuntos de datos, audiencias, destinos y recorridos. A continuación, los resultados de las consultas SQL se utilizan para generar respuestas a las preguntas originales del lenguaje natural de los clientes.
* **Usuarios previstos**: Los usuarios principales de este modelo son profesionales de marketing, analistas de datos o administradores de recorrido de clientes, quienes buscan comprender y actuar en base a perspectivas operacionales dentro de Experience Platform usando lenguaje natural. Es posible que no sean expertos en SQL o ingeniería de datos, pero necesitan respuestas rápidas y precisas sobre sus entidades de Experience Platform para tomar decisiones informadas y optimizar las experiencias de los clientes.
* **Casos de uso**: este modelo ayuda a los usuarios a acceder a los metadatos de sus entidades de Experience Platform, como audiencias, recorridos, esquemas, atributos, conjuntos de datos y destinos. Los usuarios pueden hacer preguntas en lenguaje natural (como qué audiencias se activan o qué audiencias utilizan un esquema específico) y el modelo las traduce en consultas SQL a través del gráfico de conocimiento de Experience Platform. Esto permite a los usuarios obtener rápidamente visibilidad operativa y tomar decisiones informadas sin necesidad de explorar o consultar manualmente el sistema.
* **Puntos problemáticos**: Este modelo aborda los principales problemas a los que se enfrentan los usuarios y analistas empresariales que trabajan con Experience Platform, como la complejidad de navegar por grandes volúmenes de metadatos interconectados, la necesidad de escribir manualmente consultas SQL para recuperar perspectivas operacionales y la falta de visibilidad sobre la forma en que las entidades de Experience Platform, como audiencias, conjuntos de datos y recorridos, están conectadas o funcionan. Al permitir el acceso a los metadatos mediante lenguaje natural y automatizar la generación de SQL, el modelo reduce la dependencia en los recursos técnicos, acorta el tiempo de detección de insight y permite a los usuarios tomar decisiones más rápidas basadas en datos.

## Detalles del modelo {#model-details}

* **Tipo de modelo**: LLM Prompt con aprendizaje dinámico en contexto
* **Entrada**: consultas de lenguaje natural del usuario.
* **Salida**: el modelo genera consultas SQL en sintaxis [!DNL Snowflake], que se ejecutarán sobre el gráfico de conocimientos de Experience Platform.

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

## Evaluación de modelo {#model-evaluation}

* **Métricas y procedimientos de evaluación**: El modelo se evalúa mirando las [!DNL NL2SQL] solicitudes y evaluando cuántas de ellas arrojan los resultados SQL correctos. El proceso de evaluación es una combinación de coincidencia basada en reglas (estandarización SQL y luego coincidencia directa de cadenas SQL), solucionador SQL basado en LLM y evaluación humana.
* **Datos de evaluación y preprocesamiento**: Utilizamos conjuntos abiertos para pruebas de regresión y también tenemos proyectos de anotación semanales para monitorizar el rendimiento del modelo a través del tráfico de clientes reales muestreado.

## Implementación de modelo {#model-deployment}

* **Supervisión del modelo**: El modelo base está hospedado por [!DNL Azure].
* **Actualización del modelo**: Adobe Experience Platform AI Assistant Operational Insights Natural Language to SQL Model se actualiza regularmente (semanalmente) mediante la expansión del banco de preguntas. El modelo también se actualiza mediante nuevas estrategias de solicitud e instrucciones cuando es necesario.

## Equidad y parcialidad {#fairness-and-bias}

* **Justicia del modelo**: Para garantizar que el modelo interprete y genere consultas de manera consistente en diferentes intenciones del usuario y variaciones lingüísticas sin introducir sesgos ni reforzar estereotipos, Adobe utiliza una auditoría rápida, explicabilidad y salvaguardas contra la generación de resultados sesgados o poco éticos.
* **Sesgos de datos**: la salida del modelo se ve afectada por los ejemplos de aprendizaje en contexto y por lo que el recuperador selecciona en el mensaje. Los ejemplos del banco de preguntas contienen ejemplos considerados representativos desde la perspectiva de la gestión de productos. Según el caso de uso, los clientes deben considerar cómo los potenciales sesgos en los resultados del modelo pueden alinearse con o afectar a su aplicación prevista.

## Consideraciones éticas {#ethical-considerations}

**Consideraciones éticas asociadas con el modelo**: Para evitar exponer PII o atributos confidenciales, el modelo se ha diseñado para evitar reforzar los sesgos de datos existentes y respetar los límites de control de acceso. Esto incluye filtrar, etiquetar y auditar campos de esquema para el uso responsable.
