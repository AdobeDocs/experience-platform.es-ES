---
keywords: Experience Platform;inicio;temas populares;segmentación de Edge;Segmentación;Servicio de segmentación;servicio de segmentación;guía de iu;streaming edge;
solution: Experience Platform
title: Guía de IU de segmentación de Edge
description: La segmentación de Edge es la capacidad de evaluar segmentos en Platform de forma instantánea en Edge, lo que permite casos de uso de personalización de la misma página y de la siguiente.
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 0%

---

# Guía de la interfaz de usuario de segmentación de Edge

>[!NOTE]
>
>La segmentación de Edge ahora está disponible de forma general para todos los usuarios de Platform. Si ha creado segmentos perimetrales durante la versión beta, estos seguirán funcionando.

La segmentación de Edge es la capacidad de evaluar segmentos en Adobe Experience Platform de forma instantánea [en el borde](../../edge/home.md), habilitando casos de uso de personalización de la misma página y de la siguiente.

>[!IMPORTANT]
>
> Los datos perimetrales se almacenarán en una ubicación de servidor perimetral más cercana a la ubicación donde se recopilaron y pueden almacenarse en una ubicación distinta a la designada como centro (o principal) del centro de datos de Adobe Experience Platform.
>
> Además, el motor de segmentación de Edge solo aceptará solicitudes en el Edge donde haya **uno** identidad marcada principal, que es coherente con las identidades principales no basadas en edge.

## Tipos de consulta de segmentación de Edge {#query-types}

Actualmente, solo los tipos de consulta seleccionados se pueden evaluar con la segmentación de Edge. Las secciones siguientes proporcionan una lista de tipos de consulta que se pueden evaluar con la segmentación de Edge y los que no son compatibles actualmente.

Una consulta se puede evaluar con la segmentación de extremos si cumple cualquiera de los criterios descritos en la siguiente tabla.

>[!NOTE]
>
>Si la consulta coincide con cualquiera de los tipos de consulta de la tabla siguiente, se evaluará automáticamente mediante la segmentación de extremos. El sistema determina esta capacidad automáticamente en función de la expresión de consulta.

| Tipo de consulta | Detalles | Ejemplo | Ejemplo de PQL |
| ---------- | ------- | ------- | ----------- |
| Evento único | Cualquier definición de segmento que haga referencia a un único evento entrante sin restricción horaria. | Personas que han agregado un elemento al carro de compras. | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart")])` |
| Perfil único | Cualquier definición de segmento que haga referencia a un único atributo de solo perfil | Personas que viven en los Estados Unidos. | `homeAddress.countryCode = "US"` |
| Evento único que hace referencia a un perfil | Cualquier definición de segmento que haga referencia a uno o varios atributos de perfil y a un único evento entrante sin restricción horaria. | Personas que viven en los EE.UU. que visitaron la página principal. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView")])` |
| Evento único anulado con un atributo de perfil | Cualquier definición de segmento que haga referencia a un evento entrante único negado y a uno o más atributos de perfil | Personas que viven en los Estados Unidos y tienen **no** ha visitado la página principal. | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView")]))` |
| Evento único dentro de una ventana de tiempo | Cualquier definición de segmento que haga referencia a un único evento entrante en un período de tiempo establecido. | Personas que visitaron la página principal en las últimas 24 horas. | `chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 8 days before now)])` |
| Evento único con un atributo de perfil dentro de una ventana de tiempo | Cualquier definición de segmento que haga referencia a uno o varios atributos de perfil y a un único evento entrante en un período de tiempo establecido. | Personas que viven en Estados Unidos y que visitaron la página principal en las últimas 24 horas. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 8 days before now)])` |
| Evento único anulado con un atributo de perfil en un período de tiempo | Cualquier definición de segmento que haga referencia a uno o varios atributos de perfil y a un evento entrante único y negado en un período de tiempo. | Personas que viven en los Estados Unidos y tienen **no** visitó la página principal en las últimas 24 horas. | `homeAddress.countryCode = "US" and not(chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 8 days before now)]))` |
| Evento de frecuencia en un intervalo de tiempo de 24 horas | Cualquier definición de segmento que haga referencia a un evento que se produce un determinado número de veces en un intervalo de tiempo de 24 horas. | Personas que visitaron la página principal **al menos** cinco veces en las últimas 24 horas. | `chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| Evento de frecuencia con un atributo de perfil en un intervalo de tiempo de 24 horas | Cualquier definición de segmento que haga referencia a uno o varios atributos de perfil y a un evento que se produce un determinado número de veces en un intervalo de tiempo de 24 horas. | Personas de EE. UU. que visitaron la página principal **al menos** cinco veces en las últimas 24 horas. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| Evento de frecuencia anulado con un perfil dentro de un intervalo de tiempo de 24 horas | Cualquier definición de segmento que haga referencia a uno o varios atributos de perfil y a un evento denegado que se produce un determinado número de veces en un intervalo de tiempo de 24 horas. | Personas que no han visitado la página principal **más** cinco veces en las últimas 24 horas. | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] ))` |
| Varias visitas entrantes en un perfil de tiempo de 24 horas | Cualquier definición de segmento que haga referencia a varios eventos que se producen en un intervalo de tiempo de 24 horas. | Personas que visitaron la página principal **o** visitó la página de cierre de compra en las últimas 24 horas. | `chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| Varios eventos con un perfil en un intervalo de tiempo de 24 horas | Cualquier definición de segmento que haga referencia a uno o varios atributos de perfil y a varios eventos que se producen en un período de tiempo de 24 horas. | Personas de los EE.UU. que visitaron la página principal **y** visitó la página de cierre de compra en las últimas 24 horas. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| Segmento de segmentos | Cualquier definición de segmento que contenga uno o más segmentos de flujo continuo o por lotes. | Personas que viven en Estados Unidos y están en el segmento &quot;segmento existente&quot;. | `homeAddress.countryCode = "US" and inSegment("existing segment")` |
| Consulta que hace referencia a un mapa | Cualquier definición de segmento que haga referencia a un mapa de propiedades. | Personas que han agregado a su carro de compras en función de datos de segmentos externos. | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart") WHERE(externalSegmentMapProperty.values().exists(stringProperty="active"))])` |

Una definición de segmento **no** Debe habilitarse la segmentación de Edge en los siguientes casos:

- La definición del segmento incluye una combinación de un solo evento y una `inSegment` evento.
   - Sin embargo, si el segmento contenido en la variable `inSegment` El evento es solo de perfil, la definición del segmento **testamento** habilitarse para la segmentación de Edge.

## Pasos siguientes

En esta guía se explica cómo evaluar segmentos con segmentación de Edge en Adobe Experience Platform. Para obtener más información sobre el uso de la interfaz de usuario de Experience Platform, lea la [Guía del usuario de segmentación](./overview.md). Para aprender a realizar acciones similares y trabajar con segmentos mediante las API de Experience Platform, visite [guía de API de segmentación de Edge](../api/edge-segmentation.md).

## Apéndice

En la siguiente sección se enumeran las preguntas más frecuentes sobre la segmentación de Edge:

### ¿Cuánto tiempo tarda un segmento en estar disponible en la red perimetral?

Un segmento puede tardar hasta una hora en estar disponible en la red perimetral.