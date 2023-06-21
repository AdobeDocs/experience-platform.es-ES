---
title: Preguntas más frecuentes sobre los atributos calculados
description: Encuentre respuestas a las preguntas más frecuentes acerca del uso de atributos calculados.
badge: "Beta"
source-git-commit: 3b4e1e793a610c9391b3718584a19bd11959e3be
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---


# Preguntas frecuentes

>[!IMPORTANT]
>
>Atributos calculados actualmente en **beta** y es **no** disponible para todos los usuarios.

En Adobe Experience Platform, los atributos calculados son funciones que se utilizan para agregar datos de nivel de evento en atributos de nivel de perfil. Estas funciones se calculan automáticamente para que se puedan utilizar en la segmentación, activación y personalización. A continuación se muestra una lista de las preguntas más frecuentes sobre los atributos calculados.

## ¿Qué conjuntos de datos contribuyen a los cálculos de atributos calculados?

Los atributos calculados tienen en cuenta los conjuntos de datos de evento de experiencia habilitados para Perfil del cliente en tiempo real para calcular los atributos calculados.

## ¿Qué campos del modelo de datos de experiencia (XDM) se pueden utilizar para crear atributos calculados?

Todos los campos XDM del esquema de unión de Experience Event se pueden utilizar para crear atributos calculados.

## ¿Qué representa la &quot;última hora de evaluación&quot;?

La última hora de evaluación significa que los eventos **previo** a esa marca de tiempo se tuvieron en cuenta en la última actualización correcta del atributo calculado.

## ¿Puedo elegir la frecuencia de actualización? ¿Cómo se decide esto?

La frecuencia de actualización se determina automáticamente en función del período retroactivo del atributo calculado. Para obtener más información al respecto, lea la [sección de período retrospectivo](./overview.md#lookback-periods) de la descripción general de los atributos calculados.

## ¿En qué afecta a los cálculos la caducidad de los datos de Experience Event?

Los cálculos de atributos calculados se basan en el periodo retrospectivo definido y en los eventos de experiencia comprendidos dentro de ese periodo de tiempo. Como resultado, estos cálculos son **no** se ve afectado por la caducidad de los datos de Experience Event. Sin embargo, para garantizar la precisión de los atributos calculados, el período retroactivo debe permanecer **dentro** los límites de las caducidades de los datos.

## ¿Puedo crear un atributo calculado basado en otro atributo calculado?

Dado que los atributos calculados se crean mediante campos de Evento de experiencia y residen en un campo de Perfil, no hay forma de utilizar directamente un atributo calculado para crear otro atributo calculado.

## ¿Hay algún límite en el número de atributos calculados que puedo crear?

El número máximo actual de **publicado** atributos calculados es 25.

## ¿Hay alguna consecuencia en sentido descendente de la desactivación de un atributo calculado?

Antes de deshabilitar el atributo calculado, debe hacer lo siguiente **debería** elimínelos de sus sistemas descendentes (como la segmentación, los recorridos o los destinos), ya que puede haber complicaciones que surjan si no se eliminan.

## ¿Qué sucede cuando se deshabilita un atributo calculado? {#inactive-status}

Cuando un atributo calculado está deshabilitado o inactivo, ya no se actualiza. Como resultado, este atributo calculado **no puede** se utilizará en la búsqueda de perfiles u otros usos posteriores.

## ¿Cómo ayudan los atributos calculados a impulsar la participación?

Los atributos calculados impulsan el enriquecimiento de perfiles al añadir los atributos de evento a un nivel de perfil combinado. Por ejemplo, puede personalizar los correos electrónicos de marketing con el último producto visualizado.
