---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Incorporación de conjuntos de datos
topic: queries
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507

---


# Incorporación de conjuntos de datos

La unión de conjuntos de datos permite incluir datos de otros conjuntos de datos en la consulta. En este ejemplo se utiliza un conjunto de datos del sistema operativo personalizado para asignar el `operatingsystemID` valor al `operatingsystem` .

Conjuntos de datos:
- your_analytics_table
- custom_operator_system_lookup

Cree una `SELECT` sentencia para los 50 sistemas operativos principales por número de vistas de página.

```sql
SELECT 
  b.operatingsystem AS OperatingSystem,
  SUM(a.web.webPageDetails.pageviews.value) AS PageViews
FROM your_analytics_table a 
     JOIN custom_operating_system_lookup b 
      ON a._experience.analytics.environment.operatingsystemID = b.operatingsystemid 
WHERE _ACP_YEAR=2018 
GROUP BY OperatingSystem 
ORDER BY PageViews DESC
LIMIT 50;
```

![Imagen](../images/queries/joining-datasets/select-operating-systems.png)