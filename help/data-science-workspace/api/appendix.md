---
keywords: Experience Platform;guía para desarrolladores;extremo;Workspace de ciencia de datos;temas populares;
solution: Experience Platform
title: Apéndice de la guía de API de aprendizaje automático de Sensei
description: Las secciones siguientes proporcionan información de referencia sobre diversas funciones de la API de aprendizaje automático de Sensei.
role: Developer
exl-id: 2c8d3ae8-7ad7-4ff6-8d6b-3a42d3eccdff
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 1%

---

# Apéndice de guía de API [!DNL Sensei Machine Learning]

>[!NOTE]
>
>Data Science Workspace ya no se puede adquirir.
>
>Esta documentación está destinada a clientes existentes con derechos anteriores a Data Science Workspace.

Las secciones siguientes proporcionan información de referencia sobre diversas características de la API [!DNL Sensei Machine Learning].

## Parámetros de consulta para recuperación de recursos {#query}

La API [!DNL Sensei Machine Learning] proporciona compatibilidad con parámetros de consulta para recuperar recursos. En la tabla siguiente se describen los parámetros de consulta disponibles y sus usos:

| Parámetro de consulta | Descripción | Valor predeterminado |
| --------------- | ----------- | ------- |
| `start` | Indica el índice de inicio de la paginación. | `start=0` |
| `limit` | Indica el número máximo de resultados que se van a devolver. | `limit=25` |
| `orderby` | Indica las propiedades que se van a utilizar para ordenar en orden de prioridad. Incluya un guión (**-**) antes del nombre de una propiedad para ordenar en orden descendente; de lo contrario, los resultados se ordenarán en orden ascendente. | `orderby=created` |
| `property` | Indica la expresión de comparación que un objeto debe satisfacer para ser devuelto. | `property=deleted==false` |

>[!NOTE]
>
>Al combinar varios parámetros de consulta, deben separarse con el símbolo et (**&amp;**).

## Configuraciones de CPU y GPU en Python {#cpu-gpu-config}

Los motores Python tienen la capacidad de elegir entre una CPU o una GPU para su entrenamiento o puntuación, y se define en una [MLInstance](./mlinstances.md) como una especificación de tarea (`tasks.specification`).

A continuación se muestra un ejemplo de configuración que especifica el uso de una CPU para el aprendizaje y una GPU para la puntuación:

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
>Los valores de `cpus` y `gpus` no indican el número de CPU o GPU, sino el número de máquinas físicas. Estos valores tienen el permiso `"1"` y, en caso contrario, producirán una excepción.

## Configuraciones de recursos de PySpark y Spark {#resource-config}

Los motores Spark tienen la capacidad de modificar los recursos computacionales con fines de entrenamiento y puntuación. Estos recursos se describen en la siguiente tabla:

| Recurso | Descripción | Tipo |
| -------- | ----------- | ---- |
| driverMemory | Memoria para controlador en megabytes | int |
| driverCores | Número de núcleos utilizados por el controlador | int |
| executeMemory | Memoria para ejecutor en megabytes | int |
| executeCores | Número de núcleos utilizados por el ejecutor | int |
| numExecutors | Número de ejecutores | int |

Los recursos se pueden especificar en una [MLInstance](./mlinstances.md) como (A) parámetros de entrenamiento o puntuación individuales, o (B) dentro de un objeto de especificaciones adicional (`specification`). Por ejemplo, las siguientes configuraciones de recursos son las mismas para la formación y la puntuación:

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
