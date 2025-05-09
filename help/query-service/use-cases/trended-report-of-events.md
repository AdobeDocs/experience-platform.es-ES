---
keywords: Experience Platform;inicio;temas populares;servicio de consultas;servicio de consultas;consultas de experienceevent;consulta de experienceevent;consulta de Experience Event;
title: Creación de un informe de tendencias de eventos
description: Obtenga información sobre cómo escribir consultas que utilizan eventos de experiencia para crear un informe de tendencias de eventos en un intervalo de fechas especificado, agrupados por fecha.
exl-id: 8f7ed5b5-c265-4a1e-a360-4293d1e86e97
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---

# Creación de un informe de tendencias de eventos

Este documento proporciona un ejemplo del SQL necesario para crear un informe de tendencias de eventos por día en un intervalo de fechas específico. Con Adobe Experience Platform Query Service, puede escribir consultas que utilicen [!DNL Experience Events] para capturar una variedad de casos de uso. Los eventos de experiencia se representan mediante la clase ExperienceEvent del Modelo de datos de experiencia (XDM), que captura una instantánea del sistema inmutable y no agregada cuando un usuario interactúa con un sitio web o servicio. Los Eventos de experiencia incluso se pueden utilizar para el análisis de dominio de tiempo. Consulte la sección [pasos siguientes](#next-steps) para ver más casos de uso que implican que [!DNL Experience Events] genere informes de visitantes.

Los informes le permiten acceder a los datos de Experience Platform para sacar el máximo partido a las perspectivas comerciales estratégicas de su organización. Con estos informes, puede examinar los datos de Experience Platform de varias formas, mostrar métricas clave en formatos fáciles de entender y compartir las perspectivas resultantes.

Encontrará más información sobre XDM y [!DNL Experience Events] en la [[!DNL XDM System] descripción general](../../xdm/home.md). Al combinar el servicio de consultas con [!DNL Experience Events], puede realizar un seguimiento efectivo de las tendencias de comportamiento entre los usuarios. El siguiente documento proporciona ejemplos de consultas que involucran a [!DNL Experience Events].

## Objetivos

En el ejemplo siguiente se crea un informe de tendencias de los eventos de un intervalo de fechas especificado, agrupados por fecha. Específicamente, este ejemplo de SQL resume varios valores de análisis como `A`, `B` y `C`, y luego resume el número de veces que se han visto parkas durante el período de un mes.

La columna de marca de tiempo encontrada en [!DNL Experience Event] conjuntos de datos está en formato UTC. El ejemplo utiliza la función `from_utc_timestamp()` para transformar la marca de tiempo de UTC a EDT y, a continuación, utiliza la función `date_format()` para aislar la fecha del resto de la marca de tiempo.

```sql
SELECT 
date_format( from_utc_timestamp(timestamp, 'EDT') , 'yyyy-MM-dd') as Day,
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
WHERE TIMESTAMP >= to_timestamp('2019-03-01') AND TIMESTAMP <= to_timestamp('2019-03-31')
GROUP BY Day 
ORDER BY Day ASC, pageViews DESC;
```

Los resultados de esta consulta se pueden ver a continuación.

```console
     Day     | pageViews |   A    |   B   |    C    | viewedParkas
-------------+-----------+--------+-------+---------+--------------
 2019-03-01  |   55317.0 | 8503.0 | 804.0 | 1578.0  |           73
 2019-03-02  |   55302.0 | 8600.0 | 854.0 | 1528.0  |           86
 2019-03-03  |   54613.0 | 8162.0 | 795.0 | 1568.0  |          100
 2019-03-04  |   54501.0 | 8479.0 | 832.0 | 1509.0  |          100
 2019-03-05  |   54941.0 | 8603.0 | 816.0 | 1514.0  |           73
 2019-03-06  |   54817.0 | 8434.0 | 855.0 | 1538.0  |           76
 2019-03-07  |   55201.0 | 8604.0 | 843.0 | 1517.0  |           64
 2019-03-08  |   55020.0 | 8490.0 | 849.0 | 1536.0  |           99
 2019-03-09  |   43186.0 | 6736.0 | 643.0 | 1150.0  |           52
 2019-03-10  |   48471.0 | 7542.0 | 772.0 | 1272.0  |           70
 2019-03-11  |   56307.0 | 8721.0 | 818.0 | 1571.0  |           81
 2019-03-12  |   55374.0 | 8653.0 | 843.0 | 1501.0  |           59
 2019-03-13  |   55046.0 | 8509.0 | 887.0 | 1556.0  |           65
 2019-03-14  |   55518.0 | 8551.0 | 848.0 | 1516.0  |           77
 2019-03-15  |   55329.0 | 8575.0 | 818.0 | 1607.0  |           96
 2019-03-16  |   55030.0 | 8651.0 | 815.0 | 1542.0  |           66
 2019-03-17  |   55143.0 | 8435.0 | 774.0 | 1572.0  |           65
 2019-03-18  |   54065.0 | 8211.0 | 816.0 | 1574.0  |          111
 2019-03-19  |   55097.0 | 8395.0 | 771.0 | 1498.0  |           86
 2019-03-20  |   55198.0 | 8472.0 | 863.0 | 1583.0  |           82
 2019-03-21  |   54978.0 | 8490.0 | 820.0 | 1580.0  |           83
 2019-03-22  |   55464.0 | 8561.0 | 820.0 | 1559.0  |           83
 2019-03-23  |   55384.0 | 8482.0 | 800.0 | 1139.0  |           82
 2019-03-24  |   55295.0 | 8594.0 | 841.0 | 1382.0  |           78
 2019-03-25  |   42069.0 | 6365.0 | 606.0 | 1509.0  |           62
 2019-03-26  |   49724.0 | 7629.0 | 724.0 | 1553.0  |           44
 2019-03-27  |   55111.0 | 8524.0 | 804.0 | 1524.0  |           94
 2019-03-28  |   55030.0 | 8439.0 | 822.0 | 1554.0  |           73
 2019-03-29  |   55281.0 | 8601.0 | 854.0 | 1580.0  |           73
 2019-03-30  |   55162.0 | 8538.0 | 846.0 | 1534.0  |           79
 2019-03-31  |   55437.0 | 8486.0 | 807.0 | 1649.0  |           68
 (31 rows)
```

## Pasos siguientes {#next-steps}

Al leer este documento, entiende mejor cómo usar el servicio de consultas con [!DNL Experience Events] para rastrear de manera eficaz las tendencias de comportamiento entre sus usuarios.

Para obtener más información acerca de otros casos de uso basados en visitantes que usan [!DNL Experience Events], lea los siguientes documentos:

- [Recupere una lista de visitantes organizados por número de vistas de página.](./visitors-by-number-of-page-views.md)
- [Enumerar las sesiones anteriores de un visitante.](./list-visitor-sessions.md)
- [Ver un informe de resumen de un visitante.](./roll-up-report-of-a-visitor.md)
