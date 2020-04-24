---
keywords: Experience Platform;getting started;customer ai;popular topics
solution: Experience Platform
title: Introducción a la API del cliente
topic: Getting started
translation-type: tm+mt
source-git-commit: 3146442ed0638559ddd68452fd42cc5731b4dc8a

---


# Entrada y salida de AI del cliente

El siguiente documento describe las diferentes entradas y salidas utilizadas en la API del cliente.

## Datos de entrada de AI del cliente

La API del cliente utiliza datos del Evento de experiencias de consumo para calcular las puntuaciones de tendencia. Para obtener más información sobre el Evento de la experiencia del consumidor, consulte la documentación de [Preparar datos para su uso en Servicios inteligentes](../data-preparation.md).

## Datos de salida de AI del cliente

La IA del cliente genera varios atributos para perfiles individuales que se consideran elegibles. Existen dos maneras de consumir la puntuación en función de lo que haya aprovisionado. Si tiene habilitado el Perfil de cliente en tiempo real para su conjunto de datos, puede consumirlo mediante el Perfil de cliente en tiempo real. Si no tiene Perfil de cliente en tiempo real, puede descargar el conjunto de datos de salida de AI del cliente disponible en el lago de datos.

>[!NOTE]
>Los valores de salida son consumidos por el Perfil del cliente en tiempo real, que puede utilizarse para crear y definir segmentos.

En la tabla siguiente se describen los distintos atributos encontrados en la salida de la API del cliente:

| Atributo | Descripción |
| ----- | ----------- |
| Puntuación | La probabilidad relativa de que un cliente alcance el objetivo previsto dentro del intervalo de tiempo definido. Este valor no debe tratarse como un porcentaje de probabilidad, sino como la probabilidad de un individuo en comparación con la población total. Esta puntuación va de 0 a 100. |
| Probabilidad | Este atributo es la verdadera probabilidad de un perfil para alcanzar el objetivo previsto dentro del intervalo de tiempo definido. Al comparar resultados entre objetivos diferentes, se recomienda considerar la probabilidad por encima del percentil o la puntuación. La probabilidad siempre debe utilizarse para determinar la probabilidad media entre la población elegible, ya que la probabilidad tiende a estar en el lado inferior en el caso de eventos que no ocurren con frecuencia. Los valores para el intervalo de probabilidad entre 0 y 1. |
| Percentil | Este valor proporciona información sobre el rendimiento de un perfil en relación con otros perfiles con una puntuación similar. Por ejemplo, un perfil con una clasificación de percentil de 99 para la reproducción indica que tiene un mayor riesgo de producir, en comparación con el 99% de todos los demás perfiles que fueron puntuados. Los percentiles oscilan entre 1 y 100. |
| Tipo de tendencia | El tipo de tendencia seleccionado. |
| Fecha de puntuación | Fecha en la que se produjo la puntuación. |
| Factores influyentes | Razones predichas por las que es probable que un perfil se convierta o se produzca. Los factores están compuestos por los atributos siguientes:<ul><li>Código: El perfil o atributo del comportamiento que influye positivamente en la puntuación predicha de un perfil. </li><li>Valor: Valor del perfil o atributo de comportamiento.</li><li>Importancia: Indica el peso del perfil o el atributo de comportamiento que tiene en la puntuación prevista (bajo, medio, alto)</li></ul> |

## Pasos siguientes {#next-steps}

Una vez que haya preparado los datos y haya colocado todas las credenciales y esquemas, siga las instrucciones de inicio de la guía [Configurar una instancia](./user-guide/configure.md) de AI de cliente. Esta guía lo acompaña durante la creación de una instancia para la API del cliente.