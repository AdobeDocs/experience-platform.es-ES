---
keywords: Experience Platform;inicio;temas populares;servicio de consultas;servicio de consultas;consultas de experienceevent;consulta de experienceevent;consulta de Experience Event;
title: Enumeración de las vistas de página de un usuario
description: Obtenga información sobre cómo escribir consultas que utilizan eventos de experiencia para crear una lista de las últimas 100 páginas que ha utilizado un usuario especificado.
exl-id: d831910d-d3a4-4a5a-b897-b09f0546dab0
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 1%

---

# Enumeración de las vistas de página de un usuario

Este documento proporciona un ejemplo del SQL necesario para enumerar las vistas de página de un usuario especificado. Con Adobe Experience Platform Query Service, puede escribir consultas que utilicen [!DNL Experience Events] para capturar una variedad de casos de uso. Los eventos de experiencia se representan mediante la clase ExperienceEvent del Modelo de datos de experiencia (XDM), que captura una instantánea del sistema inmutable y no agregada cuando un usuario interactúa con un sitio web o servicio. Los Eventos de experiencia incluso se pueden utilizar para el análisis de dominio de tiempo. Consulte la sección [pasos siguientes](#next-steps) para ver más casos de uso que implican que [!DNL Experience Events] genere informes de visitantes.

Encontrará más información sobre XDM y [!DNL Experience Events] en la [[!DNL XDM System] descripción general](../../xdm/home.md). Al combinar el servicio de consultas con [!DNL Experience Events], puede realizar un seguimiento efectivo de las tendencias de comportamiento entre los usuarios. El siguiente documento proporciona ejemplos de consultas que involucran a [!DNL Experience Events].

## Objetivo

En el ejemplo siguiente se enumeran las últimas 100 páginas que ha visto un usuario especificado.

```sql
SELECT 
timestamp, 
web.webReferrer.type as referrerType, 
web.webReferrer.URL as referrer, 
web.webPageDetails.name as pageName, 
_experience.analytics.event1to100.event1.value as A, 
_experience.analytics.event1to100.event2.value as B, 
_experience.analytics.event1to100.event3.value as C, 
web.webPageDetails.pageviews.value as pageViews
FROM your_analytics_table 
WHERE endUserIds._experience.aaid.id = '457C3510571E5930-69AA721C4CBF9339' 
ORDER BY timestamp 
LIMIT 100;
```

Los resultados de esta consulta se pueden ver a continuación.

```console
      timestamp       |  referrerType  |                            referrer                                |                 pageName            |  A  |  B  |  C  | pageViews
----------------------+----------------+--------------------------------------------------------------------+-------------------------------------+-----+-----+-----+--------------
2019-11-08 17:15:28.0 | typed_bookmark |                                                                    |                                     |     |     |     |
2019-11-08 17:53:05.0 | social         | http://www.reddit.com                                              | Home                                |     |     |     |          1.0
2019-11-08 17:53:45.0 | typed_bookmark |                                                                    | Kids                                |     |     |     |          1.0
2019-11-08 19:22:34.0 | typed_bookmark |                                                                    |                                     |     |     |     |          
2019-11-08 20:01:12.0 | search_engine  | http://www.google.com/search?ie=UTF-8&q=laundry parkas&cid=sem:115 | Home                                |     |     |     |          1.0 
2019-11-08 20:01:57.0 | typed_bookmark |                                                                    | Kids                                |     |     |     |          1.0
2019-11-08 20:03:36.0 | typed_bookmark |                                                                    | Search Results                      | 1.0 |     |     |          1.0
2019-11-08 20:04:30.0 | typed_bookmark |                                                                    | Product Details: Pemmican Power Bar |     |     |     |          1.0
2019-11-08 20:05:27.0 | typed_bookmark |                                                                    | Shopping Cart: Cart Details         |     |     |     |          1.0
2019-11-08 20:06:07.0 | typed_bookmark |                                                                    | Shopping Cart: Shipping Information |     |     |     |          1.0
2019-11-08 20:07:02.0 | typed_bookmark |                                                                    | Shopping Cart: Billing Information  |     |     | 1.0 |          1.0
2019-11-08 20:07:52.0 | typed_bookmark |                                                                    | Shopping Cart: Order Review         |     |     |     |          1.0
2019-11-08 20:08:45.0 | typed_bookmark |                                                                    | Order Confirmation                  |     |     |     |          1.0
2019-11-08 20:09:24.0 | typed_bookmark |                                                                    | Home                                |     |     |     |          1.0
2019-11-08 20:10:03.0 | typed_bookmark |                                                                    | Editorial Page: Camping Essentials  |     |     |     |          1.0
2019-11-08 20:11:01.0 | typed_bookmark |                                                                    | Account Registration|Form           |     |     |     |          1.0
2019-11-08 20:11:38.0 | typed_bookmark |                                                                    | Seasonal Sale                       |     |     |     |          1.0
2019-11-08 20:12:10.0 | typed_bookmark |                                                                    | Blog: Iris Sagan                    |     |     |     |          1.0
2019-11-08 20:13:09.0 | typed_bookmark |                                                                    | Product Details: UltraTech Socks    |     |     |     |          1.0
2019-11-08 20:14:05.0 | typed_bookmark |                                                                    | Seasonal Sale                       |     |     |     |          1.0
```

## Pasos siguientes {#next-steps}

Al leer este documento, entiende mejor cómo usar el servicio de consultas con [!DNL Experience Events] para enumerar las vistas de página como un usuario especificado.

Consulte los siguientes casos de uso para obtener más información sobre otros casos de uso basados en visitantes:

- [Recupere una lista de visitantes organizados por número de vistas de página.](./visitors-by-number-of-page-views.md)
- [Ver un informe de resumen de un visitante.](./roll-up-report-of-a-visitor.md)
- [Crea un informe de tendencias de los eventos por día.](./trended-report-of-events.md)
