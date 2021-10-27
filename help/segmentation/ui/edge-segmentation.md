---
keywords: Experience Platform;inicio;temas populares;segmentación perimetral;Segmentación;Servicio de segmentación;servicio de segmentación;guía de interfaz de usuario;Edge de flujo continuo;
solution: Experience Platform
title: Guía de la interfaz de usuario de segmentación de Edge
topic-legacy: ui guide
description: La segmentación de Edge es la capacidad de evaluar segmentos en Platform instantáneamente en el perímetro, habilitando los casos de uso de personalización de la misma página y de la siguiente página.
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
source-git-commit: bb5a56557ce162395511ca9a3a2b98726ce6c190
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 1%

---

# Guía de la interfaz de usuario de segmentación de Edge (beta)

>[!IMPORTANT]
>
>La segmentación de Edge está actualmente en fase beta. La documentación y las funciones están sujetas a cambios.

La segmentación de Edge es la capacidad de evaluar segmentos en Adobe Experience Platform de forma instantánea [en el borde](../../edge/home.md), habilitando los casos de uso de personalización de la misma página y de la página siguiente.

## Tipos de consultas de segmentación de Edge

Actualmente solo se pueden evaluar los tipos de consulta seleccionados con segmentación de Edge. Las siguientes secciones proporcionan una lista de tipos de consulta que pueden evaluarse con segmentación de Edge y los que no son compatibles actualmente.

### Tipos de consulta admitidos

Una consulta se puede evaluar con segmentación de Edge si cumple cualquiera de los criterios descritos en la siguiente tabla.

>[!NOTE]
>
>Si la consulta coincide con cualquiera de los tipos de consulta de la tabla siguiente, se evaluará automáticamente mediante la segmentación de Edge. El sistema determina esta capacidad automáticamente en función de la expresión de consulta.

| Tipo de consulta | Detalles | Ejemplo |
| ---------- | ------- | ------- |
| Un solo evento | Cualquier definición de segmento que haga referencia a un solo evento entrante sin restricciones de tiempo. | Personas que han agregado un elemento al carro de compras. |
| Un solo evento que hace referencia a un perfil | Cualquier definición de segmento que haga referencia a uno o más atributos de perfil y a un solo evento entrante sin restricciones de tiempo. | Personas que viven en Estados Unidos que visitaron la página principal. |
| Se ha anulado un evento único con un atributo de perfil | Cualquier definición de segmento que haga referencia a un solo evento entrante denegado y a uno o más atributos de perfil | Personas que viven en Estados Unidos y que tienen **not** visité la página principal. |
| Un solo evento dentro de un intervalo de tiempo de 24 horas | Cualquier definición de segmento que haga referencia a un solo evento entrante en un plazo de 24 horas. | Personas que visitaron la página principal en las últimas 24 horas. |
| Evento único con un atributo de perfil dentro de un intervalo de tiempo de 24 horas | Cualquier definición de segmento que haga referencia a uno o más atributos de perfil y a un evento entrante único denegado en un plazo de 24 horas. | Personas que viven en Estados Unidos que visitaron la página principal en las últimas 24 horas. |
| Se ha anulado un evento único con un atributo de perfil en un periodo de tiempo de 24 horas | Cualquier definición de segmento que haga referencia a uno o más atributos de perfil y a un evento entrante único denegado en un plazo de 24 horas. | Personas que viven en Estados Unidos y que tienen **not** visité la página principal en las últimas 24 horas. |
| Evento de frecuencia dentro de un intervalo de tiempo de 24 horas | Cualquier definición de segmento que haga referencia a un evento que se produce un determinado número de veces dentro de un intervalo de tiempo de 24 horas. | Personas que visitaron la página principal **al menos** cinco veces en las últimas 24 horas. |
| Evento de frecuencia con un atributo de perfil dentro de un intervalo de tiempo de 24 horas | Cualquier definición de segmento que haga referencia a uno o más atributos de perfil y a un evento que se produce un determinado número de veces dentro de un intervalo de tiempo de 24 horas. | Personas de los Estados Unidos que visitaron la página principal **al menos** cinco veces en las últimas 24 horas. |
| Evento de frecuencia anulado con un perfil dentro de un intervalo de tiempo de 24 horas | Cualquier definición de segmento que haga referencia a uno o más atributos de perfil y a un evento rechazado que tenga lugar un determinado número de veces dentro de un intervalo de tiempo de 24 horas. | Personas que no han visitado la página principal **more** más de cinco veces en las últimas 24 horas. |
| Varias visitas entrantes dentro de un perfil de tiempo de 24 horas | Cualquier definición de segmento que haga referencia a varios eventos que se producen dentro de un intervalo de tiempo de 24 horas. | Personas que visitaron la página principal **o** visité la página de cierre de compra en las últimas 24 horas. |
| Varios eventos con un perfil dentro de un intervalo de tiempo de 24 horas | Cualquier definición de segmento que haga referencia a uno o más atributos de perfil y a varios eventos que se producen en un periodo de tiempo de 24 horas. | Personas de los Estados Unidos que visitaron la página principal **y** visité la página de cierre de compra en las últimas 24 horas. |

## Pasos siguientes

Esta guía explica cómo evaluar segmentos con segmentación de Edge en Adobe Experience Platform. Para obtener más información sobre el uso de la interfaz de usuario del Experience Platform, lea la [Guía del usuario de segmentación](./overview.md). Para aprender a realizar acciones similares y trabajar con segmentos mediante API de Experience Platform, visite [guía de API de segmentación de Edge](../api/edge-segmentation.md).
