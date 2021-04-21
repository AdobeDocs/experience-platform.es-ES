---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;servicio de consulta;RStudio;estudio;conexión al servicio de consulta;
solution: Experience Platform
title: Conexión de RStudio al servicio de consulta
topic-legacy: connect
description: Este documento recorre los pasos para conectar R Studio con Adobe Experience Platform Query Service.
exl-id: 8dd82bad-6ffb-4536-9c27-223f471a49c6
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---

# Conectar [!DNL RStudio] al servicio de consulta

Este documento recorre los pasos para conectar [!DNL RStudio] con Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> En esta guía se da por hecho que ya tiene acceso a [!DNL RStudio] y está familiarizado con su uso. Puede encontrar más información sobre [!DNL RStudio] en la [oficial [!DNL RStudio] documentación](https://rstudio.com/products/rstudio/).
> 
> Además, para utilizar RStudio con Query Service, debe instalar el controlador PostgreSQL JDBC 4.2. Puede descargar el controlador JDBC desde el [sitio oficial PostgreSQL](https://jdbc.postgresql.org/download.html).

## Crear una conexión [!DNL Query Service] en la interfaz [!DNL RStudio]

Después de instalar [!DNL RStudio], debe instalar el paquete RJDBC. Vaya al panel **[!DNL Packages]** y seleccione **[!DNL Install]**.

![](../images/clients/rstudio/install-package.png)

Aparece una ventana emergente que muestra la pantalla **[!DNL Install Packages]**. Asegúrese de que **[!DNL Repository (CRAN)]** está seleccionado para la sección **[!DNL Install from]**. El valor de **[!DNL Packages]** debe ser `RJDBC`. Asegúrese de que **[!DNL Install dependencies]** está seleccionado. Después de confirmar que todos los valores son correctos, seleccione **[!DNL Install]** para instalar los paquetes.

![](../images/clients/rstudio/install-jrdbc.png)

Ahora que el paquete RJDBC ha sido instalado, reinicie RStudio para completar el proceso de instalación.

Después de reiniciar RStudio, ahora puede conectarse al servicio de consulta. Seleccione el paquete **[!DNL RJDBC]** en el panel **[!DNL Packages]** e introduzca el siguiente comando en la consola:

```console
pgsql <- JDBC("org.postgresql.Driver", "{PATH TO THE POSTGRESQL JDBC JAR}", "`")
```

Donde {PATH TO THE POSTGRESQL JDBC JAR} representa la ruta al JAR JDBC PostgreSQL que se instaló en el equipo.

Ahora, puede crear la conexión con el servicio de consulta introduciendo el siguiente comando en la consola:

```console
qsconnection <- dbConnect(pgsql, "jdbc:postgresql://{HOSTNAME}:{PORT}/{DATABASE_NAME}?user={USERNAME}&password={PASSWORD}&sslmode=require")
```

>[!NOTE]
>
>Para obtener más información sobre cómo encontrar el nombre de la base de datos, el host, el puerto y las credenciales de inicio de sesión, visite la página [credenciales de Platform](https://platform.adobe.com/query/configuration). Para encontrar sus credenciales, inicie sesión en [!DNL Platform] y luego seleccione **[!UICONTROL Queries]**, seguido de **[!UICONTROL Credentials]**.

![](../images/clients/rstudio/connection-rjdbc.png)

## Escritura de consultas

Ahora que se ha conectado a [!DNL Query Service], puede escribir consultas para ejecutar y editar instrucciones SQL. Por ejemplo, puede utilizar `dbGetQuery(con, sql)` para ejecutar consultas, donde `sql` es la consulta SQL que desea ejecutar.

La siguiente consulta utiliza un conjunto de datos que contiene [Eventos de experiencia](../best-practices/experience-event-queries.md) y crea un histograma de vistas de página de un sitio web, dada la altura de pantalla del dispositivo.

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
