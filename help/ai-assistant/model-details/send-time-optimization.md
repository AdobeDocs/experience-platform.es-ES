---
title: Detalles del modelo de optimización del tiempo de envío
description: Obtenga información acerca del modelo de IA utilizado para la optimización del tiempo de envío en Adobe Journey Optimizer.
hide: true
hidefromtoc: true
exl-id: 95e1fc8f-1817-40d7-aa55-93daa50f43c0
source-git-commit: d1c7d1038b45bae4c014e3488f55a427c9cb02ed
workflow-type: tm+mt
source-wordcount: '1220'
ht-degree: 0%

---

# Detalles del modelo de optimización del tiempo de envío

## Información general del modelo {#model-overview}

* **Nombre y versión del modelo**: optimización del tiempo de envío
* **Fecha de la versión del modelo**: septiembre de 2024
* **Objetivo del modelo**: el modelo de optimización del tiempo de envío de Adobe Journey Optimizer elige el tiempo de envío óptimo de los mensajes push y de correo electrónico para maximizar la participación del consumidor, en función del comportamiento histórico de apertura y clic de los consumidores.
* **Usuarios previstos**: Los usuarios principales de este modelo son los profesionales de marketing, los jefes de producto y los equipos de participación de los clientes que aprovechan Adobe Journey Optimizer para impulsar estrategias de marketing basadas en datos.
* **Casos de uso**: la optimización del tiempo de envío se utiliza mejor en comunicaciones de marketing menos urgentes; por ejemplo, un anuncio semanal, información promocional sobre un nuevo producto o información sobre una venta de un mes de duración. La optimización del tiempo de envío solo está disponible para los tipos de acción push y de correo electrónico integrados de Journey Optimizer, y no está disponible actualmente para los mensajes enviados mediante acciones personalizadas o para otros tipos de acción.
* **Posible uso incorrecto**: la optimización del tiempo de envío no debe utilizarse para mensajes operativos urgentes y urgentes, por ejemplo, una confirmación de pedido, una notificación de restablecimiento de contraseña o una notificación de cambio de puerta de vuelo.

## Detalles del modelo {#model-details}

* **Tipo de modelo**: el modelo de optimización del tiempo de envío ingiere los datos de comportamiento del consumidor de Adobe Journey Optimizer de su organización y observa los eventos abiertos y de clic de nivel de usuario para predecir cuándo es más probable que los consumidores interactúen con la mensajería. El comportamiento de apertura y clics a nivel de consumidor para cada hora de la semana se pondera y combina con la similitud y el comportamiento general del consumidor con un estimador [!DNL Bayesian]. A continuación, se clasifican las predicciones de [!DNL Bayesian] para cada hora de la semana, lo que da como resultado un &quot;mapa de calor&quot; para cada métrica (aperturas de correo electrónico, clics en correos electrónicos y aperturas push), para cada cliente, a fin de predecir las horas de la semana en las que es más probable que el contacto con cada consumidor resulte en el resultado de participación deseado.
* **Entrada**: la optimización del tiempo de envío utiliza datos de la zona horaria del consumidor en el campo `timeZone` dentro del grupo de campos [!UICONTROL Detalles de preferencia], si se proporciona, para determinar la zona horaria de un consumidor. Si la zona horaria de un consumidor no está disponible en el campo `timeZone`, la optimización del tiempo de envío intenta deducir la zona horaria del consumidor, según la coincidencia de zona horaria más común con la primera dirección postal encontrada almacenada en el perfil del consumidor mediante el [tipo de datos de dirección postal](../../xdm/data-types/postal-address.md). La optimización del tiempo de envío hace predicciones para cada consumidor en función de tres tipos de datos de comportamiento:
   * El comportamiento abierto y de clic de los consumidores en general.
   * Comportamiento de apertura y clic de consumidores similares en la misma zona horaria.
   * Comportamiento de apertura y clic de ese consumidor individual.
* **Salida**: estas predicciones se ponderan y combinan usando un enfoque de [!DNL Bayesian], lo que da como resultado un &quot;mapa de calor&quot; para cada métrica (aperturas de correo electrónico, clics de correo electrónico y aperturas push), para cada cliente, que indica las horas de la semana en que es más probable que ponerse en contacto con ese consumidor genere el resultado de participación deseado (apertura/clic), como se muestra en el siguiente ejemplo de mapa de calor:

![Mapa de calor de optimización del tiempo de envío.](../images/models/send-time-optimization.png)

* **Entrada y salida de ejemplo**: Para minimizar el impacto del modelo en la riqueza de perfiles, las puntuaciones del modelo se almacenan y se comprimen en tres atributos de perfil almacenados en `_experience.intelligentServices.journeyAI.sendTimeOptimization`, y no están diseñados para ser legibles en lenguaje natural.

## Formación de modelo {#model-training}

* **Datos de formación y preprocesamiento**: el conjunto de datos de formación de cada organización se obtiene únicamente de sus propios datos en Adobe Experience Platform.
   * Una vez habilitada la función Optimización del tiempo de envío para su organización, el modelo recibe formación sobre correo electrónico y eventos push, de envío, de apertura y de clic en todos los recorridos y acciones de la organización durante las últimas 16 semanas, independientemente de si esas acciones utilizan Optimización del tiempo de envío. Esto permite que la optimización del tiempo de envío se beneficie de todos los datos generados por los consumidores.
   * Los modelos se entrenan inicialmente y se puntúan semanalmente. Después de 16 semanas, los modelos se vuelven a entrenar y a anotar mensualmente. La puntuación de modelo incluye todos los perfiles de cliente, tanto los existentes como los nuevos, desde la última ejecución de la puntuación.
   * Los mensajes enviados por Optimización del tiempo de envío reciben cualquiera de las siguientes opciones:
      * Un tiempo de envío de mensaje de &quot;exploración&quot;, seleccionado para probar diferentes tiempos de envío y observar cómo responden los consumidores.
      * Un tiempo de envío de mensaje &quot;optimizado&quot;, seleccionado para maximizar las tasas de clics/aperturas. El 5 % de los eventos de envío recibe un tiempo de envío de &quot;exploración&quot; y el 95 % de los eventos de envío están &quot;optimizados&quot;.
   * Los tiempos de envío de exploración se seleccionan al azar entre los tiempos de envío disponibles según el tiempo de espera máximo configurado. Por ejemplo, en el caso de que se seleccione un mensaje a las 9 a. m. del miércoles con la optimización del tiempo de envío activada y un tiempo de espera máximo de 3 horas, los tiempos de envío de la exploración para el mensaje se dividirán equitativamente entre las 9 a. m., las 10 a. m., las 11 a. m. y las 12 p. m.

## Evaluación de modelo {#model-evaluation}

* **Evaluación del modelo**: la optimización del tiempo de envío puede aumentar la tasa de clics en correos electrónicos y la tasa de apertura push en el intervalo de aproximadamente el 2 % al 10 % en todos los mensajes optimizados por una organización.
   * Por ejemplo, si una organización que envía correos electrónicos sin optimización del tiempo de envío tiene una tasa de clics del 5,0 % como promedio, el mismo conjunto de correos electrónicos con optimización del tiempo de envío podría generar una tasa de clics promedio de hasta el 5,5 % (5,0 % * (1+10 %) = 5,5 %).
   * Debido a la variabilidad dentro de los tamaños de muestra pequeños, es posible que no se pueda observar un beneficio de la optimización del tiempo de envío en los envíos de mensajes únicos.
   * Es más probable que las organizaciones obtengan mayores beneficios al utilizar la optimización del tiempo de envío cuando:
      * Los recorridos existentes utilizan tiempos de envío fijos y no bien optimizados;
      * La variabilidad en el comportamiento del consumidor (clics y aperturas) corresponde a la ubicación del consumidor y a las preferencias del consumidor;
      * Las organizaciones utilizan la optimización del tiempo de envío en una fracción mayor de mensajes push y de correo electrónico;
      * Las organizaciones eligen tiempos de espera máximos dentro del intervalo recomendado de 6 a 12 horas.

## Implementación de modelo {#model-deployment}

* **Actualización del modelo**: los modelos se entrenan y se clasifican semanalmente. Después de 16 semanas, los modelos se vuelven a entrenar y a anotar mensualmente. La puntuación de modelo incluye todos los perfiles de consumidor, tanto los existentes como los nuevos desde la última ejecución de puntuación.

## Equidad y parcialidad {#fairness-and-bias}

* **Precisión del modelo**: La inferencia incorrecta de la zona horaria de un consumidor puede hacer que un mensaje se envíe antes de lo óptimo para un consumidor determinado o más tarde de lo óptimo para un consumidor determinado. Sin embargo, todos los consumidores de una comunicación que utiliza la optimización del tiempo de envío recibirán un mensaje y tendrán la oportunidad de interactuar con él. Además, este modelo no utiliza datos demográficos del consumidor ni proxies para datos demográficos: solo se utilizan datos de comportamiento del consumidor y de zona horaria del consumidor. Por lo tanto, las preocupaciones por la equidad son limitadas y mitigadas.
* **Sesgos de datos**: La inferencia incorrecta de la zona horaria de un consumidor puede hacer que un mensaje se envíe antes de lo óptimo para un consumidor determinado o más tarde de lo óptimo para un consumidor determinado. Sin embargo, todos los consumidores de una comunicación que utiliza la optimización del tiempo de envío recibirán un mensaje y tendrán la oportunidad de interactuar con él. Además, este modelo no utiliza datos demográficos del consumidor ni proxies para datos demográficos: solo se utilizan datos de comportamiento del consumidor y de zona horaria del consumidor. Por lo tanto, las preocupaciones por sesgo son limitadas y mitigadas.

## Solidez {#robustness}

* **Solidez del modelo**: Los perfiles sin datos de evento de interacción suficientes (a menudo el caso de los nuevos perfiles) recibirán un tiempo de envío inmediato, un tiempo de envío de exploración dentro de la ventana seleccionada o un tiempo de envío basado en el tiempo de envío de mayor rendimiento entre todos los clientes.

## Consideraciones éticas {#ethical-considerations}

* **Consideraciones éticas asociadas con el modelo**: La inferencia incorrecta de la zona horaria de un consumidor puede hacer que un mensaje se envíe antes de lo óptimo para un consumidor determinado o más tarde de lo óptimo para un consumidor determinado. Sin embargo, todos los consumidores de una comunicación que utiliza la optimización del tiempo de envío recibirán un mensaje y tendrán la oportunidad de interactuar con él. Además, este modelo no utiliza datos demográficos del consumidor ni proxies para datos demográficos: solo se utilizan datos de comportamiento del consumidor y de zona horaria del consumidor. Por lo tanto, las preocupaciones éticas son limitadas y mitigadas.