---
keywords: Experience Platform;inicio;temas populares;segmentación perimetral;Segmentación;Servicio de segmentación;servicio de segmentación;guía de interfaz de usuario;Edge de flujo continuo;
solution: Experience Platform
title: Guía de la interfaz de usuario de segmentación de Edge
topic-legacy: ui guide
description: La segmentación de Edge es la capacidad de evaluar segmentos en Platform instantáneamente en el perímetro, habilitando los casos de uso de personalización de la misma página y de la siguiente página.
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
source-git-commit: 75583d9688f0c5ee0fe4627ce64b5436ca621aa1
workflow-type: tm+mt
source-wordcount: '853'
ht-degree: 0%

---

# Guía de la interfaz de usuario de segmentación de Edge

>[!NOTE]
>
>La segmentación perimetral ahora está disponible para todos los usuarios de Platform. Si ha creado segmentos Edge durante la versión beta, estos segmentos seguirán funcionando.

La segmentación de Edge es la capacidad de evaluar segmentos en Adobe Experience Platform de forma instantánea [en el borde](../../edge/home.md), habilitando los casos de uso de personalización de la misma página y de la página siguiente.

>[!IMPORTANT]
>
> Los datos perimetrales se almacenarán en una ubicación de servidor perimetral más cercana a donde se recopilaron y pueden almacenarse en una ubicación distinta a la designada como centro de datos de Adobe Experience Platform hub (o principal).
>
> Además, el motor de segmentación de aristas solo aceptará solicitudes en el perímetro donde haya **one** identidad marcada principal, que es coherente con las identidades principales no basadas en periferia.

## Tipos de consultas de segmentación de Edge

Actualmente solo se pueden evaluar los tipos de consulta seleccionados con segmentación de Edge. Las siguientes secciones proporcionan una lista de tipos de consulta que pueden evaluarse con segmentación de Edge y los que no son compatibles actualmente.

### Tipos de consulta admitidos {#query-types}

Una consulta se puede evaluar con segmentación de Edge si cumple cualquiera de los criterios descritos en la siguiente tabla.

>[!NOTE]
>
>Si la consulta coincide con cualquiera de los tipos de consulta de la tabla siguiente, se evaluará automáticamente mediante la segmentación de Edge. El sistema determina esta capacidad automáticamente en función de la expresión de consulta.

| Tipo de consulta | Detalles | Ejemplo | Ejemplo de PQL |
| ---------- | ------- | ------- | ----------- |
| Un solo evento | Cualquier definición de segmento que haga referencia a un solo evento entrante sin restricciones de tiempo. | Personas que han agregado un elemento al carro de compras. | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart")])` |
| Perfil único | Cualquier definición de segmento que haga referencia a un único atributo de perfil | Personas que viven en Estados Unidos. | `homeAddress.countryCode = "US"` |
| Un solo evento que hace referencia a un perfil | Cualquier definición de segmento que haga referencia a uno o más atributos de perfil y a un solo evento entrante sin restricciones de tiempo. | Personas que viven en Estados Unidos que visitaron la página principal. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart")])` |
| Se ha anulado un evento único con un atributo de perfil | Cualquier definición de segmento que haga referencia a un solo evento entrante denegado y a uno o más atributos de perfil | Personas que viven en Estados Unidos y que tienen **not** visité la página principal. | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView")]))` |
| Un solo evento dentro de un intervalo de tiempo | Cualquier definición de segmento que haga referencia a un solo evento entrante dentro de un período de tiempo determinado. | Personas que visitaron la página principal en las últimas 24 horas. | `chain(xEvent, timestamp, [X: WHAT(eventType = "addToCart") WHEN(< 8 days before now)])` |
| Un solo evento con un atributo de perfil dentro de un periodo | Cualquier definición de segmento que haga referencia a uno o más atributos de perfil y a un solo evento entrante en un período de tiempo determinado. | Personas que viven en Estados Unidos que visitaron la página principal en las últimas 24 horas. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "addToCart") WHEN(< 8 days before now)])` |
| Se ha anulado un evento único con un atributo de perfil dentro de un periodo de tiempo | Cualquier definición de segmento que haga referencia a uno o más atributos de perfil y a un solo evento entrante denegado en un periodo de tiempo. | Personas que viven en Estados Unidos y que tienen **not** visité la página principal en las últimas 24 horas. | `homeAddress.countryCode = "US" and not(chain(xEvent, timestamp, [X: WHAT(eventType = "addToCart") WHEN(< 8 days before now)]))` |
| Evento de frecuencia dentro de un intervalo de tiempo de 24 horas | Cualquier definición de segmento que haga referencia a un evento que se produce un determinado número de veces dentro de un intervalo de tiempo de 24 horas. | Personas que visitaron la página principal **al menos** cinco veces en las últimas 24 horas. | `chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| Evento de frecuencia con un atributo de perfil dentro de un intervalo de tiempo de 24 horas | Cualquier definición de segmento que haga referencia a uno o más atributos de perfil y a un evento que se produce un determinado número de veces dentro de un intervalo de tiempo de 24 horas. | Personas de los Estados Unidos que visitaron la página principal **al menos** cinco veces en las últimas 24 horas. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| Evento de frecuencia anulado con un perfil dentro de un intervalo de tiempo de 24 horas | Cualquier definición de segmento que haga referencia a uno o más atributos de perfil y a un evento rechazado que tenga lugar un determinado número de veces dentro de un intervalo de tiempo de 24 horas. | Personas que no han visitado la página principal **more** más de cinco veces en las últimas 24 horas. | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] ))` |
| Varias visitas entrantes dentro de un perfil de tiempo de 24 horas | Cualquier definición de segmento que haga referencia a varios eventos que se producen dentro de un intervalo de tiempo de 24 horas. | Personas que visitaron la página principal **o** visité la página de cierre de compra en las últimas 24 horas. | `chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| Varios eventos con un perfil dentro de un intervalo de tiempo de 24 horas | Cualquier definición de segmento que haga referencia a uno o más atributos de perfil y a varios eventos que se producen en un periodo de tiempo de 24 horas. | Personas de los Estados Unidos que visitaron la página principal **y** visité la página de cierre de compra en las últimas 24 horas. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| Segmento de segmentos | Cualquier definición de segmento que contenga uno o más segmentos de flujo continuo o por lotes. | Personas que viven en Estados Unidos y que están en el segmento &quot;segmento existente&quot;. | `homeAddress.countryCode = "US" and inSegment("existing segment")` |
| Consulta que hace referencia a un mapa | Cualquier definición de segmento que haga referencia a un mapa de propiedades. | Personas que han agregado al carro de compras en función de datos de segmentos externos. | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart") WHERE(externalSegmentMapProperty.values().exists(stringProperty="active"))])` |

## Pasos siguientes

Esta guía explica cómo evaluar segmentos con segmentación de Edge en Adobe Experience Platform. Para obtener más información sobre el uso de la interfaz de usuario del Experience Platform, lea la [Guía del usuario de segmentación](./overview.md). Para aprender a realizar acciones similares y trabajar con segmentos mediante API de Experience Platform, visite [guía de API de segmentación de Edge](../api/edge-segmentation.md).
