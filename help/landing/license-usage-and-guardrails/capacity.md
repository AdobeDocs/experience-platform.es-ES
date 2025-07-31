---
title: Uso de licencias y capacidad
description: Obtenga información sobre el uso de licencias y los límites de capacidad en Adobe Experience Platform.
exl-id: 38dad2f1-bd0f-4cc3-a3a6-5105ea866ea4
source-git-commit: 326710e48ea9d6eb16f62b9f288311a1d255b287
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 6%

---

# Uso de licencias y capacidades

En Adobe Experience Platform, las capacidades le permiten saber si su organización ha superado alguna de sus protecciones y le proporcionan información sobre cómo solucionar estos problemas.

Para obtener más información sobre las protecciones en Experience Platform, lea [Información general sobre las protecciones de Real-Time CDP](../../rtcdp/guardrails/overview.md).

## Comportamiento de capacidad {#behavior}

>[!CONTEXTUALHELP]
>id="platform_capacity_streamingthroughput"
>title="Rendimiento de streaming"
>abstract="El valor de rendimiento de flujo mide los eventos de entrada máximos combinados por segundo para la transmisión de la ingesta al servicio Perfil, en sus zonas protegidas de producción y desarrollo."

>[!CONTEXTUALHELP]
>id="platform_capacity_streamingaudiences"
>title="Recuento de audiencia de streaming"
>abstract="Número máximo de audiencias de streaming por zona protegida. Este número incluye el número de audiencias de Edge que tiene en la zona protegida."

>[!CONTEXTUALHELP]
>id="platform_capacity_edgeaudiences"
>title="Audiencias de Edge"
>abstract="Número máximo de audiencias de Edge por zona protegida."

Actualmente, Capacity admite los siguientes servicios:

- Segmentación de streaming
- Ingesta por streaming

Dentro de estos servicios, se rastrean las siguientes barreras:

- El número máximo de audiencias de streaming es de 500
   - De estas 500 audiencias de streaming, el número máximo de audiencias de Edge es de 150
- El rendimiento máximo combinado de la segmentación por streaming es de 1500 registros por segundo (rps)

La capacidad de audiencia está en el nivel de **espacio aislado**. Esto significa que, para cada zona protegida que tenga en su organización, puede tener 500 audiencias de streaming, de las cuales 150 pueden ser audiencias de Edge.

La capacidad de rendimiento está en el nivel de **organización** y se puede distribuir a cada zona protegida. Por ejemplo, con las 1500 rps para el rendimiento de segmentación de streaming, puede establecer su zona protegida de producción en 1500 rps y su zona protegida de desarrollo en 150 rps.

Experience Platform calcula el rendimiento de la zona protegida en intervalos móviles de 15 minutos. Este rendimiento se mide en tiempo real y los datos se actualizan cada 60 segundos.

Si el uso alcanza el 80 % y el 90 % de la capacidad con licencia, Experience Platform emitirá una alerta en la que notificará que está alcanzando el máximo de la capacidad especificada. Puede modificar la configuración para personalizar el porcentaje de capacidad para recibir la alerta o eliminarla por completo.

Si su uso supera el 100% de su capacidad con licencia, se considerará que ha incumplido su capacidad. En este punto, experimentará latencia de rendimiento y se garantizarán los objetivos de nivel de servicio (SLT, por sus siglas en inglés) **no**.

## Preguntas frecuentes

En la siguiente sección se describen las preguntas más frecuentes sobre las capacidades de Capacity.

### ¿Puedo tener un límite máximo de rendimiento combinado que suma menos de mi objetivo máximo?

+++ Respuesta

No. El límite máximo de rendimiento combinado **debe** sumarse a la protección de su organización.

+++

### ¿Qué sucede si excedo mis capacidades máximas?

+++ Respuesta

Esto depende de la capacidad que se exceda.

Actualmente, si supera la cantidad máxima de audiencias permitidas, las audiencias excesivas no se verán afectadas. Sin embargo, la capacidad de crear nuevas audiencias puede estar restringida en el futuro.

Si supera el rendimiento de flujo continuo, experimentará latencia de rendimiento en la ingesta y segmentación.

+++

### ¿Por qué debo adherir a mis capacidades máximas?

+++ Respuesta

Trabajar dentro de sus capacidades máximas garantiza que sus datos permanezcan consistentes y que su integridad de datos se mantenga intacta.

Garantiza un rendimiento coherente durante los eventos de mayor actividad, evitando problemas técnicos que podrían afectar negativamente al rendimiento del sistema y afectar a las experiencias de los clientes que siguen el flujo de trabajo, lo que a la larga mejora la higiene de los datos y el rendimiento general del sistema.

+++

### ¿Cuáles son las prácticas recomendadas para administrar el rendimiento de la segmentación de flujo continuo?

+++ Respuesta

Para administrar mejor el rendimiento de la segmentación de flujo, debe evaluar los conjuntos de datos para asegurarse de que priorizan los datos necesarios para la personalización.


Si no se requiere procesamiento en tiempo real, debe utilizar la ingesta por lotes en lugar de la ingesta por flujo continuo.

+++
