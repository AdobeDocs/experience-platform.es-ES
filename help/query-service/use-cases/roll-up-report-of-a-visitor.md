---
keywords: Experience Platform;inicio;temas populares;servicio de consultas;servicio de consultas;consultas de eventos de experiencias;consulta de eventos de experiencias;consulta de eventos de experiencias;consulta de eventos de experiencias;
title: Ver un informe de resumen de un visitante específico
description: El siguiente documento proporciona ejemplos de consultas que involucran eventos de experiencia en el servicio de consulta de Adobe Experience Platform.
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 1%

---

# Ver un informe de resumen de un visitante específico

Este documento proporciona un ejemplo SQL para agregar datos de varias propiedades de análisis para un usuario específico y verlos juntos en un informe. Con el servicio de consulta de Adobe Experience Platform, puede escribir consultas que utilicen [!DNL Experience Events] para capturar una variedad de casos de uso. Los eventos de experiencia están representados por la clase ExperienceEvent del Modelo de datos de experiencia (XDM), que captura una instantánea inmutable y no agregada del sistema cuando un usuario interactúa con un sitio web o servicio. Los eventos de experiencia pueden incluso utilizarse para el análisis del dominio de tiempo. Consulte la [sección pasos siguientes](#next-steps) para más casos de uso que impliquen [!DNL Experience Events] para generar informes de visitantes.

Más información sobre XDM y [!DNL Experience Events] se encuentra en la variable [[!DNL XDM System] información general](../../xdm/home.md). Combinando el servicio de consulta con [!DNL Experience Events], puede realizar un seguimiento eficaz de las tendencias de comportamiento entre los usuarios. El siguiente documento proporciona ejemplos de consultas que involucran [!DNL Experience Events].

## Objetivo

El siguiente ejemplo SQL muestra cómo ver un informe agregado de varios valores de análisis para un usuario especificado.

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

Al leer este documento, tiene una mejor comprensión de cómo utilizar el servicio de consulta con [!DNL Experience Events] para ver un informe agregado de los valores de análisis de un usuario especificado.

Consulte los siguientes casos de uso para conocer otros casos utilizados basados en visitantes:

- [Recupere una lista de visitantes organizada por número de vistas de página.](./visitors-by-number-of-page-views.md)
- [Enumerar las sesiones anteriores de un visitante.](./list-visitor-sessions.md)
- [Cree un informe de tendencias de eventos por día.](./trended-report-of-events.md)
