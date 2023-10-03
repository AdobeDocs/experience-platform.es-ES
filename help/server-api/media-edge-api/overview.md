---
solution: Experience Platform
title: API de Media Edge
description: Información general sobre las API de Media Edge
exl-id: 55c952de-caab-4301-acf2-f7b64cebbb1c
source-git-commit: ba5a539603da656117c95d19c9e989ef0e252f82
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 5%

---

# Información general de API de Media Edge

Las API de Media Edge se basan en Adobe Experience Platform para proporcionar datos de seguimiento de eventos de medios en el marco de [Esquemas XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=en#:~:text=Experience%20Data%20Model%20(XDM)%2C,the%20power%20of%20digital%20experiences). Para los clientes de Media Analytics, esta opción ofrece las siguientes funciones:

* Con [Adobe Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=es)Por lo tanto, los clientes pueden obtener detalles granulares y casi en tiempo real de la duración, los inicios y las paradas para evaluarlos y combinarlos para métricas de contenidos. Los clientes que migran de Adobe Analytics tienen todas las métricas de creación de informes disponibles en Adobe Customer Journey Analytics.

* Con [Adobe Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html?lang=es)Además, los clientes pueden enriquecer sus perfiles en tiempo real con datos de consumo de medios.

* Con [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=en)Además, los clientes pueden optimizar las campañas omnicanal y automatizar los recorridos con señales de consumo de medios.


## Optimización de flujos de datos de seguimiento de medios

Ambos [API de Media Collection](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-overview.html?lang=en&amp;media-tracking-data-flows) y las API de Media Edge proporcionan datos de seguimiento de medios como servicios RESTful. Sin embargo, el uso del servicio Media Edge tiene las siguientes ventajas:

* Es la forma más sencilla de incorporar esquemas XDM al flujo de datos.

* Las llamadas de se dirigen desde un reproductor multimedia directamente a [Red perimetral de Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=en).

* Rastrea eventos de medios de forma eficaz con un mínimo de llamadas entre servidores.

La siguiente tabla muestra un posible servicio de API de Adobe para varios casos de análisis de medios:

| Caso de uso | servicio API |
| -------- | ----------- |
| solución de Adobe Experience Platform | Media Edge |
| REAL-TIME CDP + CUSTOMER JOURNEY ANALYTICS | Media Edge |
| Solución Adobe Analytics + Adobe Experience Platform | Media Edge |
| Solo Adobe Analytics (ya está realizando el seguimiento) | Colección de medios |

>[!NOTE]
>
> El servicio de API de recopilación de medios para Analytics sigue recibiendo datos XDM, pero no está optimizado para ellos en la medida en que lo esté el servicio de Media Edge. Según los datos enviados desde el Reproductor de medios, algunos datos solo de Analytics también se pueden enrutar a través del servicio de API de Media Edge.

El siguiente gráfico muestra los flujos de datos de los dos servicios API:

![Flujos de datos de Media Analytics](../assets/edge-api-dataflow.png)

## Pasos siguientes

* Para obtener más información sobre el uso de las API de Media Edge, consulte la [Documentación de introducción](getting-started.md).

* Para obtener más información sobre cómo trabajar con Platform Edge, consulte [Instalación de Media Analytics con Experience Platform Edge](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/implementation-edge.html?lang=en).
