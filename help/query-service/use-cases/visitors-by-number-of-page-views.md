---
keywords: Experience Platform;inicio;temas populares;servicio de consultas;servicio de consultas;consultas de eventos de experiencias;consulta de eventos de experiencias;consulta de eventos de experiencias;consulta de eventos de experiencias;
title: Enumerar visitantes por su número de vistas de página
description: Aprenda a escribir consultas que utilicen eventos de experiencias para recuperar una lista de visitantes organizada por el número de vistas de página.
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 1%

---

# Enumerar visitantes según el número de vistas de página

Este documento proporciona un ejemplo del SQL requerido para recuperar una lista de visitantes organizada por el número de vistas de página. Con el servicio de consulta de Adobe Experience Platform, puede escribir consultas que utilicen [!DNL Experience Events] para capturar una variedad de casos de uso. Los eventos de experiencia están representados por la clase ExperienceEvent del Modelo de datos de experiencia (XDM), que captura una instantánea inmutable y no agregada del sistema cuando un usuario interactúa con un sitio web o servicio. Los eventos de experiencia pueden incluso utilizarse para el análisis del dominio de tiempo. Consulte la [sección pasos siguientes](#next-steps) para más casos de uso que impliquen [!DNL Experience Events] para generar informes de visitantes.

Más información sobre XDM y [!DNL Experience Events] se encuentra en la variable [[!DNL XDM System] información general](../../xdm/home.md). Combinando el servicio de consulta con [!DNL Experience Events], puede realizar un seguimiento eficaz de las tendencias de comportamiento entre los usuarios. El siguiente documento proporciona ejemplos de consultas que involucran [!DNL Experience Events].

## Objetivo

En el siguiente ejemplo se crea un informe que enumera los 10 ID de los usuarios que vieron la mayoría de las páginas.

```sql
SELECT 
endUserIds._experience.aaid.id, 
SUM(web.webPageDetails.pageviews.value) as pageViews 
FROM your_analytics_table
GROUP BY endUserIds._experience.aaid.id 
ORDER BY pageViews DESC
LIMIT 10;
```

Los resultados de la consulta se muestran en la siguiente tabla.

```console
               id                  | pageViews
-----------------------------------+-----------
 457C3510571E5930-69AA721C4CBF9339 |     706.0
 776F85658792C017-6491FE6570382A01 |     700.0
 6BEC9C6AB52E779F-28F5B023113F2C85 |     654.0
 1C0CCFB2DC63611E-6E4A4D4142AEB613 |     642.0
 112EE9A6F3BE29D1-514A6C355A2C9EF6 |     629.0
 CCC75A0E6AC7F2FA-11D58515D370F626 |     624.0
 749F850A44153120-3710C53FA2162349 |     614.0
 2B668C6DDDAF0C505-92EDCC072F7CDDA |     587.0
 7EB7257335935320-101921AF45111FE6 |     586.0
 5F4759CA80DCA9C9-2C0DA93D80D9DBFA |     586.0
(10 rows)
```

## Pasos siguientes {#next-steps}

Al leer este documento, tiene una mejor comprensión de cómo utilizar el servicio de consulta con [!DNL Experience Events] para enumerar los usuarios que vieron la mayoría de las páginas.

Consulte los siguientes casos de uso para conocer otros casos utilizados basados en visitantes:

- [Enumerar las sesiones anteriores de un visitante.](./list-visitor-sessions.md)
- [Ver un informe de resumen de un visitante.](./roll-up-report-of-a-visitor.md)
- [Cree un informe de tendencias de eventos por día.](./trended-report-of-events.md)
