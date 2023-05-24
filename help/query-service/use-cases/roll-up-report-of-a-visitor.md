---
keywords: Experience Platform;inicio;temas populares;servicio de consultas;servicio de consultas;consultas de experienceevent;consulta de experienceevent;consulta de Experience Event;
title: Ver un informe de resumen de un visitante específico
description: El siguiente documento proporciona ejemplos de consultas que implican eventos de experiencia en el servicio de consultas de Adobe Experience Platform.
exl-id: 1348503f-65c1-41f9-b111-1284a49449a1
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 1%

---

# Ver un informe de resumen de un visitante específico

Este documento proporciona un ejemplo de SQL para agregar datos de varias propiedades de análisis para un usuario específico y ver esos datos juntos en un informe. Con Adobe Experience Platform Query Service, puede escribir consultas que utilicen [!DNL Experience Events] para recopilar una variedad de casos de uso. Los eventos de experiencia se representan mediante la clase ExperienceEvent del Modelo de datos de experiencia (XDM), que captura una instantánea del sistema inmutable y no agregada cuando un usuario interactúa con un sitio web o servicio. Los Eventos de experiencia incluso se pueden utilizar para el análisis de dominio de tiempo. Consulte la [sección de pasos siguientes](#next-steps) para ver más casos de uso que impliquen [!DNL Experience Events] para generar informes de visitantes.

Más información sobre XDM y [!DNL Experience Events] se puede encontrar en la [[!DNL XDM System] descripción general](../../xdm/home.md). Combinando el servicio de consultas con [!DNL Experience Events], puede rastrear de manera eficaz las tendencias de comportamiento entre sus usuarios. El siguiente documento proporciona ejemplos de consultas que implican [!DNL Experience Events].

## Objetivo

El siguiente ejemplo de SQL muestra cómo ver un informe agregado de varios valores de análisis para un usuario especificado.

```sql
SELECT 
endUserIds._experience.aaid.id, 
SUM(web.webPageDetails.pageviews.value) as pageViews, 
SUM(_experience.analytics.event1to100.event1.value) as A, 
SUM(_experience.analytics.event1to100.event2.value) as B, 
SUM(_experience.analytics.event1to100.event3.value) as C,
SUM(
    CASE 
    WHEN _experience.analytics.customDimensions.evars.evar1 = 'parkas' 
    THEN 1 
    ELSE 0 
    END) as viewedParkas
FROM your_analytics_table 
WHERE endUserIds._experience.aaid.id = '457C3510571E5930-69AA721C4CBF9339' 
GROUP BY endUserIds._experience.aaid.id
ORDER BY pageViews DESC;
```

Los resultados de la consulta se muestran en la siguiente tabla.

```console
               id                 | pageViews |   A   |   B   |   C   | viewedParkas
----------------------------------+-----------+-------+-------+-------+--------------
457C3510571E5930-69AA721C4CBF9339 |     706.0 | 83.0  |  7.0  | 38.0  |          22
```

## Pasos siguientes {#next-steps}

Al leer este documento, tiene una mejor comprensión de cómo utilizar el servicio de consulta con [!DNL Experience Events] para ver un informe agregado de los valores de analytics de un usuario especificado.

Consulte los siguientes casos de uso para obtener más información sobre otros casos de uso basados en visitantes:

- [Recupere una lista de visitantes organizados por número de vistas de página.](./visitors-by-number-of-page-views.md)
- [Enumerar las sesiones anteriores de un visitante.](./list-visitor-sessions.md)
- [Crea un informe de tendencias de los eventos por día.](./trended-report-of-events.md)
