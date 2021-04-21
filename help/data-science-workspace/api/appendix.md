---
keywords: Experience Platform;guía para desarrolladores;punto final;Data Science Workspace;temas populares;
solution: Experience Platform
title: Guía de API de aprendizaje automático de Sensei Apéndice
topic-legacy: Developer guide
description: Las siguientes secciones proporcionan información de referencia sobre varias funciones de la API de aprendizaje automático Sensei.
exl-id: 2c8d3ae8-7ad7-4ff6-8d6b-3a42d3eccdff
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 3%

---

# [!DNL Sensei Machine Learning] apéndice de la guía de API

Las secciones siguientes proporcionan información de referencia sobre varias funciones de la API [!DNL Sensei Machine Learning].

## Parámetros de consulta para la recuperación de recursos {#query}

La API [!DNL Sensei Machine Learning] es compatible con los parámetros de consulta al recuperar recursos. En la tabla siguiente se describen los parámetros de consulta disponibles y sus usos:

| Parámetro de consulta | Descripción | Valor predeterminado |
| --------------- | ----------- | ------- |
| `start` | Indica el índice de inicio de la paginación. | `start=0` |
| `limit` | Indica el número máximo de resultados que se van a devolver. | `limit=25` |
| `orderby` | Indica las propiedades que se utilizarán para la ordenación en orden de prioridad. Incluya un guión (**-**) antes de un nombre de propiedad para ordenarlo en orden descendente; de lo contrario, los resultados se ordenarán en orden ascendente. | `orderby=created` |
| `property` | Indica la expresión de comparación que un objeto debe satisfacer para ser devuelto. | `property=deleted==false` |

>[!NOTE]
>
>Cuando se combinan varios parámetros de consulta, deben separarse con ampersands (**&amp;**).

## Configuraciones de CPU y GPU de Python {#cpu-gpu-config}

Los motores Python tienen la capacidad de elegir entre una CPU o una GPU para sus fines de entrenamiento o puntuación, y se define en una [instancia MLI](./mlinstances.md) como una especificación de tarea (`tasks.specification`).

A continuación se muestra un ejemplo de configuración que especifica el uso de una CPU para formación y una GPU para puntuación:

```json
[
    {
        "name": "train",
        "parameters": [
            {
                "key": "training parameter",
                "value": "parameter value"
            }    
        ],
        "specification": {
            "type": "ContainerTaskSpec",
            "cpus": "1"
        }
    },
    {
        "name": "score",
        "parameters": [
            {
                "key": "scoring parameter",
                "value": "parameter value" 
            }
        ],
        "specification": {
            "type": "ContainerTaskSpec",
            "gpus": "1"
        }
    }
]
```

>[!NOTE]
>
>Los valores de `cpus` y `gpus` no significan el número de CPU o GPU, sino el número de máquinas físicas. Estos valores son permisibles `"1"` y arrojarán una excepción en caso contrario.

## Configuraciones de recursos PySpark y Spark {#resource-config}

Los motores de encendido (Spark Engines) tienen la capacidad de modificar los recursos computacionales con fines de entrenamiento y puntuación. Estos recursos se describen en la siguiente tabla:

| Recurso | Descripción | Tipo |
| -------- | ----------- | ---- |
| driverMemory | Memoria para el controlador en megabytes | int |
| driverCores | Número de núcleos utilizados por el controlador | int |
| ejecutorMemory | Memoria para el ejecutor en megabytes | int |
| ejecutorCores | Número de núcleos utilizados por el ejecutor | int |
| numEjecutors | Número de ejecutores | int |

Los recursos se pueden especificar en una [instancia MLI](./mlinstances.md) como (A) parámetros individuales de capacitación o puntuación, o (B) dentro de un objeto de especificaciones adicionales (`specification`). Por ejemplo, las siguientes configuraciones de recursos son las mismas para la formación y la puntuación:

```json
[
    {
        "name": "train",
        "parameters": [
            {
                "key": "driverMemory",
                "value": "2048"
            },
            {
                "key": "driverCores",
                "value": "1"
            },
            {
                "key": "executorMemory",
                "value": "2048"
            },
            {
                "key": "executorCores",
                "value": "2"
            },
            {
                "key": "numExecutors",
                "value": "3"
            }
        ]
    },
    {
        "name": "score",
        "parameters": [
            {
                "key": "scoring parameter",
                "value": "parameter value"
            }
        ],
        "specification": {
            "type": "SparkTaskSpec",
            "name": "Spark Task name",
            "className": "Class name",
            "driverMemoryInMB": 2048,
            "driverCores": 1,
            "executorMemoryInMB": 2048,
            "executorCores": 2,
            "numExecutors": 3
        }
    }
]
```
