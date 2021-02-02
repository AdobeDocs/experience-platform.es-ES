---
keywords: Experience Platform;inicio;temas populares;servicio de Consulta;servicio de consulta;RStudio;rstudio;conectar al servicio de consulta;
solution: Experience Platform
title: Conectar con RStudio
topic: connect
description: Este documento recorre los pasos para conectar R Studio con el servicio de Consulta de Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: eac93f3465fa6ce4af7a6aa783cf5f8fb4ac9b9b
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 2%

---


# [!DNL RStudio]

Este documento recorre los pasos para conectar [!DNL RStudio] con Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Esta guía asume que ya tiene acceso a [!DNL RStudio] y está familiarizado con cómo utilizarlo. Puede encontrar más información sobre [!DNL RStudio] en la [documentación oficial [!DNL RStudio] ](https://rstudio.com/products/rstudio/).

## Conectando [!DNL RStudio] con [!DNL Query Service]

Después de instalar [!DNL RStudio], en la pantalla **[!DNL Console]** que aparece, primero deberá preparar la secuencia de comandos de R para utilizar [!DNL PostgreSQL].

```r
install.packages("RPostgreSQL")
install.packages("rstudioapi")
require("RPostgreSQL")
require("rstudioapi")
```

Una vez que haya preparado la secuencia de comandos R para utilizar [!DNL PostgreSQL], ahora puede conectar [!DNL RStudio] a [!DNL Query Service] cargando el controlador [!DNL PostgreSQL].

```r
drv <- dbDriver("PostgreSQL")
con <- dbConnect(drv, 
 dbname = "{DATABASE_NAME}",
 host="{HOST_NUMBER}",
 port={PORT_NUMBER},
 user="{USERNAME}",
 password="{PASSWORD}")
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{DATABASE_NAME}` | Nombre de la base de datos que se va a utilizar. |
| `{HOST_NUMBER` y `{PORT_NUMBER}` | El extremo del host y su puerto para el servicio de Consulta. |
| `{USERNAME}` y `{PASSWORD}` | Las credenciales de inicio de sesión que se utilizarán. El nombre de usuario toma la forma `ORG_ID@AdobeOrg`. |

>[!NOTE]
>
>Para obtener más información sobre cómo encontrar el nombre de la base de datos, el host, el puerto y las credenciales de inicio de sesión, visite la [página de credenciales en la plataforma](https://platform.adobe.com/query/configuration). Para encontrar sus credenciales, inicie sesión en [!DNL Platform] y luego seleccione **[!UICONTROL Consultas]**, seguido de **[!UICONTROL Credenciales]**.

## Escritura de consultas

Ahora que se ha conectado a [!DNL Query Service], puede escribir consultas para ejecutar y editar sentencias SQL. Por ejemplo, puede utilizar `dbGetQuery(con, sql)` para ejecutar consultas, donde `sql` es la consulta SQL que desea ejecutar.

La siguiente consulta utiliza un conjunto de datos que contiene [Eventos de experiencias](../best-practices/experience-event-queries.md) y crea un histograma de vistas de página de un sitio web, dada la altura de pantalla del dispositivo.

```sql
df_pageviews <- dbGetQuery(con,
"SELECT t.range AS buckets, 
 Count(*) AS pageviews 
FROM (SELECT CASE 
 WHEN device.screenheight BETWEEN 0 AND 99 THEN '0 - 99' 
 WHEN device.screenheight BETWEEN 100 AND 199 THEN '100-199' 
 WHEN device.screenheight BETWEEN 200 AND 299 THEN '200-299' 
 WHEN device.screenheight BETWEEN 300 AND 399 THEN '300-399' 
 WHEN device.screenheight BETWEEN 400 AND 499 THEN '400-499' 
 WHEN device.screenheight BETWEEN 500 AND 599 THEN '500-599' 
 ELSE '600-699' 
 end AS range 
 FROM aa_post_vals_3) t 
GROUP BY t.range 
ORDER BY buckets 
LIMIT 1000000")
```

Una respuesta correcta devuelve los resultados de la consulta:

```r
df_pageviews
 buckets pageviews
1 0 - 99 198985
2 500-599 67138
3 300-399 2147
4 200-299 354
5 400-499 6947
6 100-199 4415
7 600-699 3097040
```

## Pasos siguientes

Para obtener más información sobre cómo escribir y ejecutar consultas, lea la guía sobre [consultas en ejecución](../best-practices/writing-queries.md).