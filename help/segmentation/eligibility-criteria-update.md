---
title: Actualización de criterios de idoneidad de segmentación
description: Obtenga información acerca de las actualizaciones de los criterios de idoneidad para la segmentación que afectan a los tipos de audiencias que se pueden evaluar mediante streaming y segmentación de Edge.
hide: true
hidefromtoc: true
exl-id: c91c0f75-9bc8-4fa7-9d27-9b07d0ea560c
source-git-commit: eafb7337edacc5d2b2aa9c38540aff946c8d39c0
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 3%

---

# Actualización de criterios de idoneidad de segmentación

>[!IMPORTANT]
>
>Todas las definiciones de segmentos existentes que se evalúan actualmente mediante streaming o segmentación de Edge seguirán funcionando tal cual, a menos que se editen o actualicen.

A partir del 20 de mayo de 2025, se realizarán tres actualizaciones que afectarán a la elegibilidad de la segmentación.

1. Conjunto de reglas apto
2. Idoneidad de la ventana horaria
3. Inclusión de datos por lotes en audiencias de streaming
4. Políticas de combinación activas

## Conjunto de reglas {#ruleset}

Cualquier definición de segmento **nueva o editada** que coincida con los siguientes conjuntos de reglas **ya no se evaluará** mediante la transmisión por secuencias o la segmentación de perímetros. En su lugar, se evaluarán mediante la segmentación por lotes.

- Un solo evento con un intervalo de tiempo superior a 24 horas
   - Active una audiencia con todos los perfiles que hayan visto una página web en los últimos tres días.
- Un solo evento sin ventana de tiempo
   - Active una audiencia con todos los perfiles que hayan visto una página web.

## Periodo de tiempo {#time-window}

Para evaluar una audiencia con segmentación por streaming, **debe** estar restringida en un período de tiempo de 24 horas.

## Inclusión de datos por lotes en audiencias de streaming {#include-batch-data}

Antes de esta actualización, podía crear una definición de audiencia de flujo continuo que combinara fuentes de datos de flujo y por lotes. Sin embargo, con la última actualización, la creación de una audiencia con fuentes de datos por lotes y de flujo continuo se evaluará mediante la segmentación por lotes.

Si necesita evaluar una definición de segmento mediante streaming o segmentación de Edge que coincida con el conjunto de reglas actualizado, debe crear explícitamente un lote y un conjunto de reglas de streaming y combinarlos con un segmento de segmentos. Este conjunto de reglas por lotes **debe** basarse en un esquema de perfil.

Por ejemplo, supongamos que tiene dos audiencias, con un perfil de alojamiento de audiencia que contiene datos de esquema y el otro esquema de evento de experiencia de alojamiento:

| Público | Esquema | Tipo de Source | Definición de consulta | ID de público |
| -------- | ------ | ----------- | ---------------- | ----------- |
| Residentes de California | Perfil | Lote | La dirección postal está en el estado de California | `e3be6d7f-1727-401f-a41e-c296b45f607a` |
| Cierres de compra recientes | Evento de experiencia | Streaming | Tiene al menos un cierre de compra en las últimas 24 horas | `9e1646bb-57ff-4309-ba59-17d6c5bab6a1` |

Si desea utilizar el componente por lotes en la audiencia de flujo continuo, deberá hacer referencia a la audiencia por lotes mediante un segmento de segmentos.

Por lo tanto, un conjunto de reglas de ejemplo que combinara las dos audiencias tendría el siguiente aspecto:

```
inSegment("e3be6d7f-1727-401f-a41e-c296b45f607a") and 
CHAIN(xEvent, timestamp, [C0: WHAT(eventType.equals("commerce.checkouts", false)) 
WHEN(<= 24 hours before now)])
```

La audiencia resultante *se* evaluará usando la segmentación de flujo continuo, ya que aprovecha la pertenencia de la audiencia por lotes haciendo referencia al componente de audiencia por lotes.

Sin embargo, si desea combinar dos audiencias con datos de evento, **no puede** combinar los dos eventos. Deberá crear ambas audiencias y luego crear otra audiencia que use `inSegment` para hacer referencia a ambas audiencias.

Por ejemplo, supongamos que tiene dos audiencias, con ambas audiencias albergando datos de esquema de evento de experiencia:

| Público | Esquema | Tipo de Source | Definición de consulta | ID de público |
| -------- | ------ | ----------- | ---------------- | ----------- |
| Abandonos recientes | Evento de experiencia | Lote | Tiene al menos un evento de abandono en las últimas 24 horas | `e3be6d7f-1727-401f-a41e-c296b45f607a` |
| Cierres de compra recientes | Evento de experiencia | Streaming | Tiene al menos un cierre de compra en las últimas 24 horas | `9e1646bb-57ff-4309-ba59-17d6c5bab6a1` |

En este caso, debe crear una tercera audiencia de la siguiente manera:

```
inSegment("e3be6d7f-1727-401f-a41e-c296b45f607a") and inSegment("9e1646bb-57ff-4309-ba59-17d6c5bab6a1")
```

>[!IMPORTANT]
>
>Todas las definiciones de segmentos existentes que coincidan con los conjuntos de reglas permanecerán evaluadas mediante streaming o segmentación de Edge hasta que se editen.
>
>Además, todas las definiciones de segmentos existentes que actualmente cumplen los demás criterios de evaluación de segmentación de Edge o streaming se seguirán evaluando con la segmentación de Edge o streaming.

## Política de combinación {#merge-policy}

Cualquier definición de segmento **nueva o editada** que califique para la segmentación de Edge o streaming **debe** estar en la política de combinación &quot;Activa en Edge&quot;.

Si no hay ninguna política de combinación activa establecida, tendrás que [configurar tu política de combinación](../profile/merge-policies/ui-guide.md#configure) y establecerla para que esté activa en Edge.
