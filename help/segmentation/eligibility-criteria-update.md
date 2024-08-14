---
title: Actualización de criterios de idoneidad de segmentación
description: Obtenga información acerca de las actualizaciones de los criterios de idoneidad para la segmentación que afectan a los tipos de audiencias que se pueden evaluar mediante streaming y segmentación de Edge.
hide: true
hidefromtoc: true
source-git-commit: 0bbee2100ed6fdc0f40457965e195d07de6eb2a1
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---


# Actualización de criterios de idoneidad de segmentación

A partir del 24 de septiembre de 2024, se realizarán dos actualizaciones que afectarán a la elegibilidad de la segmentación.

1. Tipos de consulta de segmentación de Edge y streaming
2. Políticas de combinación de streaming y segmentación de Edge

## Tipos de consulta

Cualquier **definición de segmento nueva o editada** que coincida con los siguientes tipos de consulta **ya no se evaluará** mediante la transmisión o la segmentación de perímetros. En su lugar, se evaluarán mediante la segmentación por lotes.

- Un solo evento con un intervalo de tiempo superior a 24 horas
   - Active una audiencia con todos los perfiles que hayan visto una página web en los últimos tres días.
- Un solo evento sin ventana de tiempo
   - Active una audiencia con todos los perfiles que hayan visto una página web.

Si necesita evaluar una definición de segmento mediante streaming o segmentación de Edge que coincida con el tipo de consulta actualizado, puede crear explícitamente una consulta por lotes y una consulta de flujo continuo y combinarlas con un segmento de segmentos.

Por ejemplo, si necesita activar una audiencia con todos los perfiles que vieron una página web en los últimos 3 días mediante la segmentación por flujo continuo, puede crear las siguientes consultas:

- T1 (flujo): Todos los perfiles que vieron una página web en las últimas 24 horas
- T2 (lote): todos los perfiles que vieron una página web en los últimos 3 días

A continuación, puede combinarlas consultando Q1 o Q2.

Del mismo modo, si necesita activar una audiencia con todos los perfiles que vieron una página web, puede crear las siguientes consultas:

- T3 (flujo): Todos los perfiles que vieron una página web en las últimas 24 horas
- T4 (lote): todos los perfiles que vieron una página web.

A continuación, puede combinarlas consultando Q3 o Q4.

>[!IMPORTANT]
>
>Todas las definiciones de segmentos existentes que coincidan con los tipos de consulta permanecerán evaluadas mediante streaming o segmentación de Edge hasta que se editen.
>
>Además, todas las definiciones de segmentos existentes que actualmente cumplen los demás criterios de evaluación de segmentación de Edge o streaming se seguirán evaluando con la segmentación de Edge o streaming.

## Política de combinación

Cualquier definición de segmento **nueva o editada** que califique para la segmentación de Edge o streaming **debe** estar en la política de combinación &quot;Activa en Edge&quot;.

Todas las definiciones de segmentos existentes que se evalúen mediante streaming o segmentación de Edge seguirán funcionando tal cual.
