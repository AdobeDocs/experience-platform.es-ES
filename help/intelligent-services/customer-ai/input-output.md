---
keywords: Experience Platform;getting started;customer ai;popular topics;customer ai input;customer ai output
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: Entrada y salida de AI del cliente
topic: Getting started
description: El siguiente documento describe las diferentes entradas y salidas utilizadas en la API del cliente.
translation-type: tm+mt
source-git-commit: de16ebddd8734f082f908f5b6016a1d3eadff04c
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 1%

---


# Entrada y salida de AI del cliente

El siguiente documento describe las diferentes entradas y salidas utilizadas en la API del cliente.

## Datos de entrada de AI del cliente

La API del cliente utiliza datos del Evento de experiencias de consumo para calcular las puntuaciones de tendencia. Para obtener más información sobre el Evento de la experiencia del consumidor, consulte la documentación de [Preparar datos para su uso en Servicios inteligentes](../data-preparation.md).

### Datos históricos

La API del cliente requiere datos históricos para la formación de modelos, pero la cantidad de datos requeridos se basa en dos elementos clave: ventana de resultados y población elegible.

De forma predeterminada, la API del cliente busca que un usuario haya tenido actividades en los últimos 120 días si no se proporciona ninguna definición de población elegible durante la configuración de la aplicación. Además, la API del cliente requiere un mínimo de 500 eventos cualificados y 500 no aptos (1000 en total) de datos históricos basados en una definición de objetivo predicha.

Los siguientes ejemplos proporcionados utilizan una fórmula sencilla para ayudarle a determinar la cantidad mínima de datos necesaria. Si tiene más de lo mínimo, es probable que el modelo proporcione resultados más precisos. Si tiene menos de la cantidad mínima necesaria, el modelo fallará, ya que no hay una cantidad suficiente de datos para la formación de modelos.

**Fórmula**:

Longitud mínima de los datos requerida = población elegible + ventana de resultados

>[!NOTE]
>
> 30 es el número mínimo de días requeridos para la población elegible. Si no se proporciona, el valor predeterminado es 120 días.

Ejemplos :

- Desea predecir si es probable que un cliente compre un reloj en los próximos 30 días. También desea puntuar a los usuarios que tienen alguna actividad web en los últimos 60 días. En este caso, la longitud mínima de los datos requerida = 60 días + 30 días. La población elegible es de 60 días y la duración del resultado es de 30 días, con un total de 90 días.

- Desea predecir si es probable que el usuario compre un reloj en los próximos 7 días. En este caso, la longitud mínima de los datos requerida = 120 días + 7 días. La población elegible tiene un valor predeterminado de 120 días y la ventana de resultados es de 7 días con un total de 127 días.

- Desea predecir si es probable que el cliente compre un reloj en los próximos 7 días. También desea puntuar a los usuarios que tengan alguna actividad web en los últimos 7 días. En este caso, la longitud mínima de los datos requerida = 30 días + 7 días. La población elegible requiere un mínimo de 30 días y la duración del resultado es de 7 días, con un total de 37 días.

Además de los datos mínimos requeridos, la API del cliente también funciona mejor con los datos recientes. En este caso de uso, la AI del cliente realiza una predicción para el futuro en función de los datos de comportamiento recientes de un usuario. En otras palabras, es probable que los datos más recientes den una predicción más precisa.

## Datos de salida de AI del cliente

La IA del cliente genera varios atributos para perfiles individuales que se consideran elegibles. Existen dos maneras de consumir la puntuación en función de lo que haya aprovisionado. Si tiene habilitado el Perfil de cliente en tiempo real para su conjunto de datos, puede consumirlo mediante el Perfil de cliente en tiempo real. Si no tiene Perfil de cliente en tiempo real, puede descargar el conjunto de datos de salida de AI del cliente disponible en el lago de datos.

>[!NOTE]
>
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