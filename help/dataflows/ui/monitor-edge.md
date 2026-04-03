---
title: Monitorización de segmentación de Edge
description: Aprenda a utilizar el panel de monitorización para observar el rendimiento de la segmentación de Edge.
exl-id: 7abba7e8-1f2d-4a21-a93f-8bda7aa4d849
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 3%

---

# Monitorización de segmentación de Edge

Puede utilizar el panel de monitorización de la IU de Adobe Experience Platform para llevar a cabo una monitorización en tiempo real de la segmentación de Edge dentro de su organización. Utilice esta función para acceder a una mayor transparencia en el rendimiento de los datos perimetrales.

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [Datastreams](../../datastreams/overview.md): Datastreams le permite conectar Experience Platform Edge Network a su conjunto de datos.
* [Capacidades](../../landing/license-usage-and-guardrails/capacity.md): en Experience Platform, las capacidades le permiten saber si su organización ha superado alguna de sus protecciones y le proporcionan información sobre cómo solucionar estos problemas.
* [Segmentación de Edge](../../segmentation/methods/edge-segmentation.md): la segmentación de Edge es la capacidad de evaluar definiciones de segmentos en Adobe Experience Platform de forma instantánea [en el perímetro](../../landing/edge-and-hub-comparison.md), lo que permite casos de uso de personalización de la misma página y de la siguiente.

## Acceso {#access}

Para acceder al panel de monitorización del rendimiento de la segmentación de Edge, seleccione **[!UICONTROL Monitoring]** en la sección **[!UICONTROL Data management]**, seguido de **[!UICONTROL Edge]**.

![El método para acceder al panel de segmentación de perímetros del monitor está resaltado.](/help/dataflows/assets/ui/monitor-edge/access.png)

Aparecerá el tablero de monitorización. Esto muestra las métricas de monitorización para el rendimiento de flujo de Edge, un gráfico que muestra la velocidad del rendimiento de flujo de Edge y una vista de flujo de datos. Estas métricas se pueden filtrar por servicio, por perímetro y por fecha.

![Las opciones de filtrado del panel de supervisión están resaltadas.](/help/dataflows/assets/ui/monitor-edge/filtering.png)

>[!NOTE]
>
>Puede ver la vista de secuencia de datos **solamente** si selecciona [!UICONTROL Edge segmentation throughput].

Si filtra por servicio, puede elegir sobre qué servicio desea ver la información de rendimiento. Esto incluye servicios como la segmentación de Edge, la recopilación de datos, Target, Adobe Journey Optimizer, Offer Decisioning, destinos personalizados personalizados, reenvío de eventos, Adobe Analytics y Adobe Audience Manager.

Si filtra por borde, puede elegir sobre qué borde desea ver información. Los perímetros admitidos son la costa este de EE. UU., la costa oeste de EE. UU., Europa, India, Singapur, Australia, Japón y Suiza. Es posible seleccionar varias aristas para verlas a la vez.

Si filtra por fecha, puede elegir la escala temporal para filtrar los eventos. Este periodo puede establecerse en 30 días. También puede usar una de las siguientes escalas de tiempo preconfiguradas: [!UICONTROL Last 6 hours], [!UICONTROL Last 12 hours], [!UICONTROL Last 24 hours], [!UICONTROL Last 7 days] y [!UICONTROL Last 30 days].

## Monitorización de métricas de rendimiento de Edge

La tabla de métricas proporciona información específica sobre el rendimiento de Edge del servicio seleccionado. Puede consultar la siguiente tabla para obtener más detalles sobre cada columna.

| Métrica | Descripción |
| ------ | ----------- |
| Solicitudes recibidas | El número de solicitudes recibidas por las aristas seleccionadas dentro del periodo de tiempo. |
| Rendimiento máximo | La tasa más alta de solicitudes recibidas por los perímetros seleccionados dentro del periodo de tiempo. |

{style="table-layout:auto"}

## Gráfico de monitorización del rendimiento de la segmentación de Edge

El gráfico de monitorización muestra los registros por segundo recibidos por los perímetros seleccionados dentro del periodo de tiempo asignado, en comparación con la capacidad máxima permitida.

![Se muestra el gráfico de rendimiento de la segmentación de borde.](/help/dataflows/assets/ui/monitor-edge/edge-segmentation-throughput.png)

## Vista de secuencia de datos

>[!NOTE]
>
>La vista de secuencia de datos está **solamente** disponible si está filtrando el rendimiento de segmentación de Edge.

La sección de vista de secuencia de datos muestra una lista de las secuencias de datos más recientes que han pasado a través de los bordes de la zona protegida.

![Se muestra la vista de secuencia de datos, que muestra información sobre las secuencias de datos enumeradas.](/help/dataflows/assets/ui/monitor-edge/datastream-view.png)

| Campo | Descripción |
| ----- | ----------- |
| Nombre de secuencia de datos | Nombre de la secuencia de datos. |
| Conjuntos de datos | Nombre de los conjuntos de datos a los que pertenece el conjunto de datos. |
| Servicio habilitado | Nombres de los servicios para los que está habilitado el conjunto de datos. |
| Solicitudes | Número de solicitudes que han pasado a través del conjunto de datos. |
| Rendimiento máximo | La tasa más alta de solicitudes que pasaron por el conjunto de datos. |
