---
keywords: Experience Platform;inicio;temas populares;segmentación perimetral;Segmentación;Servicio de segmentación;servicio de segmentación;guía de interfaz de usuario;Edge de flujo continuo;
solution: Experience Platform
title: Guía de la interfaz de usuario de segmentación de Edge
topic-legacy: ui guide
description: La segmentación de Edge es la capacidad de evaluar segmentos en Platform instantáneamente en el perímetro, habilitando los casos de uso de personalización de la misma página y de la siguiente página.
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
source-git-commit: 8f2540902cdcff99627393429424dbfe1de2d3da
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 3%

---

# Guía de la interfaz de usuario de segmentación de Edge (beta)

>[!NOTE]
>
>La segmentación de Edge está actualmente en fase beta. La documentación y las funciones están sujetas a cambios.

La segmentación de Edge es la capacidad de evaluar segmentos en Adobe Experience Platform instantáneamente en el perímetro, habilitando los casos de uso de personalización de la misma página y de la siguiente página.

## Tipos de consultas de segmentación de Edge

Una consulta se puede evaluar con segmentación de Edge si cumple cualquiera de los siguientes criterios:

| Tipo de consulta | Detalles | Ejemplo |
| ---------- | ------- | ------- |
| Visita entrante | Cualquier definición de segmento que haga referencia a un solo evento entrante sin restricciones de tiempo. | ![](../images/ui/edge-segmentation/incoming-hit.png) |
| Visita entrante que hace referencia a un perfil | Cualquier definición de segmento que haga referencia a un solo evento entrante, sin restricción de tiempo, y uno o más atributos de perfil. | ![](../images/ui/edge-segmentation/profile-hit.png) |
| Visita entrante con un periodo de tiempo de 24 horas | Cualquier definición de segmento que haga referencia a un solo evento entrante en un plazo de 24 horas. |  |
| Visita entrante que hace referencia a un perfil con un periodo de tiempo de 24 horas | Cualquier definición de segmento que haga referencia a un solo evento entrante en un plazo de 24 horas y uno o más atributos de perfil |  |

Si la consulta coincide con cualquiera de los tipos de consulta anteriores, se evaluará automáticamente mediante la segmentación perimetral.

Los siguientes tipos de consulta son **no** compatibles actualmente con la segmentación de Edge:

| Tipo de consulta | Detalles |
| ---------- | ------- |
| Varios eventos | Si una consulta contiene más de un evento, no se puede evaluar mediante la segmentación perimetral. |
| Consulta de frecuencia | Cualquier definición de segmento que haga referencia a un evento que se produzca al menos un determinado número de veces. |  |
| Consulta de frecuencia que hace referencia a un perfil | Cualquier definición de segmento que haga referencia a un evento que se produzca al menos un determinado número de veces y que tenga uno o más atributos de perfil. |  |

## Pasos siguientes

Esta guía del usuario explica cómo evaluar segmentos con segmentación de Edge en Adobe Experience Platform.

Para obtener más información sobre el uso de la interfaz de usuario de Adobe Experience Platform, lea la [Guía del usuario de segmentación](./overview.md). Para aprender a realizar acciones similares y trabajar con segmentos mediante la interfaz de usuario de Adobe Experience Platform, visite la [guía de la API de segmentación de Edge](../api/edge-segmentation.md).
