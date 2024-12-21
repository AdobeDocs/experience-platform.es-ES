---
solution: Experience Platform
title: Guía de IU de segmentación de Edge
description: Aprenda a utilizar la segmentación de Edge para evaluar definiciones de segmentos en Platform de forma instantánea en Edge de, lo que permite casos de uso de personalización de la misma página y de la siguiente.
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
source-git-commit: 828a586f0264147676da5c43c73d3b3b9d50b9c2
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 1%

---

# Guía de la interfaz de usuario de segmentación de Edge

>[!NOTE]
>
>La segmentación de Edge ahora está disponible de forma general para todos los usuarios de Platform. Si ha creado definiciones de segmentos perimetrales durante la versión beta, estas definiciones de segmentos seguirán funcionando.

La segmentación de Edge es la capacidad para evaluar segmentos en Adobe Experience Platform de forma instantánea [en el perímetro](../../web-sdk/home.md), lo que permite casos de uso de personalización de la misma página y de la siguiente.

>[!IMPORTANT]
>
> Los datos perimetrales se almacenarán en una ubicación de servidor perimetral más cercana a la ubicación donde se recopilaron y pueden almacenarse en una ubicación distinta a la designada como centro (o principal) del centro de datos de Adobe Experience Platform.
>
> Además, el motor de segmentación de Edge solo aceptará solicitudes en Edge donde haya **una** identidad principal marcada, lo cual es coherente con las identidades principales no basadas en Edge.

## Tipos de consultas de segmentación de Edge {#query-types}

Actualmente, solo los tipos de consulta seleccionados se pueden evaluar con la segmentación de Edge. Las secciones siguientes proporcionan una lista de tipos de consulta que se pueden evaluar con la segmentación de Edge y los que no son compatibles actualmente.

Una consulta se puede evaluar con la segmentación de extremos si cumple cualquiera de los criterios descritos en la siguiente tabla.

>[!NOTE]
>
>Si la consulta coincide con cualquiera de los tipos de consulta de la tabla siguiente, se evaluará automáticamente mediante la segmentación de extremos. El sistema determina esta capacidad automáticamente en función de la expresión de consulta.

| Tipo de consulta | Detalles |
| ---------- | ------- |
| Evento único | Cualquier definición de segmento que haga referencia a un único evento entrante sin restricción horaria. |
| Evento único dentro de un intervalo de tiempo relativo | Cualquier definición de segmento que haga referencia a un único evento entrante. |
| Evento único con una ventana de tiempo | Cualquier definición de segmento que haga referencia a un único evento entrante con un intervalo de tiempo. |
| Solo perfil | Cualquier definición de segmento que haga referencia únicamente a un atributo de perfil. |
| Evento único con un atributo de perfil en un intervalo de tiempo relativo inferior a 24 horas | Cualquier definición de segmento que haga referencia a un único evento entrante, con uno o más atributos de perfil, y que se produzca en un intervalo de tiempo relativo inferior a 24 horas. |
| Segmento de segmentos | Cualquier definición de segmento que contenga una o más definiciones de segmento por lotes o de flujo continuo. **Nota:** Si se usa el segmento de segmentos con definiciones de segmento de **lote**, la descalificación del perfil puede tardar **hasta 24 horas** en producirse. Si el segmento de segmentos se usa con las definiciones de segmento **streaming**, la descalificación del perfil se producirá de manera continua. |
| Varios eventos con un atributo de perfil | Cualquier definición de segmento que haga referencia a varios eventos no secuenciales **en las últimas 24 horas** y (opcionalmente) tenga uno o más atributos de perfil. |

Una definición de segmento **no** se habilitará para la segmentación de perímetros en el siguiente escenario:

- La definición del segmento incluye una combinación de un solo evento y un evento `inSegment`.
   - Sin embargo, si la definición del segmento contenida en el evento `inSegment` es solo de perfil, la definición del segmento **se** habilitará para la segmentación de Edge.
- La definición del segmento utiliza &quot;Ignorar año&quot; como parte de sus restricciones de tiempo.

## Pasos siguientes

En esta guía se explica cómo evaluar las definiciones de segmentos con la segmentación de Edge en Adobe Experience Platform. Para obtener más información acerca del uso de la interfaz de usuario del Experience Platform, lea la [Guía del usuario de segmentación](./overview.md). Para aprender a realizar acciones similares y trabajar con definiciones de segmentos mediante las API de Experience Platform, visite la [guía de API de segmentación de Edge](../api/edge-segmentation.md).

## Apéndice

En la siguiente sección se enumeran las preguntas más frecuentes sobre la segmentación de Edge:

### ¿Cuánto tiempo tarda una definición de segmento en estar disponible en el Edge Network?

Una definición de segmento tarda hasta una hora en estar disponible en el Edge Network.
