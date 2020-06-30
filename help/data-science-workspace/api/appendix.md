---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Apéndice
topic: Developer guide
translation-type: tm+mt
source-git-commit: c48079ba997a7b4c082253a0b2867df76927aa6d
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 4%

---


# Apéndice

Las siguientes secciones proporcionan información de referencia para varias funciones de la [!DNL Sensei Machine Learning] API.

## Parámetros de Consulta para la recuperación de recursos {#query}

La [!DNL Sensei Machine Learning] API admite parámetros de consulta al recuperar recursos. Los parámetros de consulta disponibles y sus usos se describen en la tabla siguiente:

| Parámetro de consulta | Descripción | Valor predeterminado |
| --------------- | ----------- | ------- |
| `start` | Indica el índice de inicio de la paginación. | `start=0` |
| `limit` | Indica el número máximo de resultados que se van a devolver. | `limit=25` |
| `orderby` | Indica las propiedades que se van a utilizar para ordenar en orden de prioridad. Incluya un guión (**-**) antes de un nombre de propiedad para ordenarlo en orden descendente; de lo contrario, los resultados se ordenarán en orden ascendente. | `orderby=created` |
| `property` | Indica la expresión de comparación que un objeto debe satisfacer para poder ser devuelto. | `property=deleted==false` |

>[!NOTE] Cuando se combinan varios parámetros de consulta, deben separarse con ampersands (**&amp;**).

## Configuraciones de CPU y GPU Python {#cpu-gpu-config}

Los motores Python tienen la capacidad de elegir entre una CPU o una GPU para fines de entrenamiento o puntuación, y se define en una instancia [MLI](./mlinstances.md) como una especificación de tarea (`tasks.specification`).

A continuación se muestra un ejemplo de configuración que especifica el uso de una CPU para la formación y una GPU para la puntuación:

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

>[!NOTE] Los valores de `cpus` y `gpus` no significan el número de CPU o GPU, sino el número de máquinas físicas. Estos valores son permisibles `"1"` y, de lo contrario, generarán una excepción.

## Configuraciones de recursos PySpark y Spark {#resource-config}

Los motores de chispa tienen la capacidad de modificar los recursos computacionales con fines de capacitación y puntuación. Estos recursos se describen en la siguiente tabla:

| Recurso | Descripción | Tipo |
| -------- | ----------- | ---- |
| driverMemory | Memoria para controlador en megabytes | int |
| driverCores | Número de núcleos utilizados por el conductor | int |
| ejecutorMemory | Memoria para ejecutor en megabytes | int |
| ejecutorCores | Número de núcleos utilizados por el ejecutor | int |
| numEjecutors | Número de ejecutores | int |

Los recursos pueden especificarse en una instancia [MLInance](./mlinstances.md) como (A) parámetros individuales de entrenamiento o puntuación, o (B) dentro de un objeto de especificaciones adicionales (`specification`). Por ejemplo, las siguientes configuraciones de recursos son las mismas para la formación y la puntuación:

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
