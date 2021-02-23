---
keywords: Experience Platform;inicio;temas populares;servicio de Consulta;servicio de consulta;RStudio;rstudio;conectar al servicio de consulta;
solution: Experience Platform
title: Connect RStudio al servicio de Consulta
topic: connect
description: Este documento recorre los pasos para conectar R Studio con el servicio de Consulta de Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: f1b2fd7efd43f317a85c831cd64c09be29688f7a
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---


# Conectar [!DNL RStudio] al servicio de Consulta

Este documento recorre los pasos para conectar [!DNL RStudio] con Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Esta guía asume que ya tiene acceso a [!DNL RStudio] y está familiarizado con cómo utilizarlo. Puede encontrar más información sobre [!DNL RStudio] en la [documentación oficial [!DNL RStudio] ](https://rstudio.com/products/rstudio/).
> 
> Además, para utilizar RStudio con el servicio de Consulta, debe instalar el controlador PostgreSQL JDBC 4.2. Puede descargar el controlador JDBC desde el [sitio oficial PostgreSQL](https://jdbc.postgresql.org/download.html).

## Cree una conexión [!DNL Query Service] en la interfaz [!DNL RStudio]

Después de instalar [!DNL RStudio], debe instalar el paquete RJDBC. Vaya al panel **[!DNL Packages]** y seleccione **[!DNL Install]**.

![](../images/clients/rstudio/install-package.png)

Aparece una ventana emergente que muestra la pantalla **[!DNL Install Packages]**. Asegúrese de que **[!DNL Repository (CRAN)]** esté seleccionado para la sección **[!DNL Install from]**. El valor de **[!DNL Packages]** debe ser `RJDBC`. Asegúrese de que **[!DNL Install dependencies]** está seleccionado. Después de confirmar que todos los valores son correctos, seleccione **[!DNL Install]** para instalar los paquetes.

![](../images/clients/rstudio/install-jrdbc.png)

Ahora que se ha instalado el paquete RJDBC, reinicie RStudio para completar el proceso de instalación.

Después de reiniciar RStudio, ahora puede conectarse al servicio de Consulta. Seleccione el paquete **[!DNL RJDBC]** en el panel **[!DNL Packages]** e introduzca el siguiente comando en la consola:

```console
pgsql <- JDBC("org.postgresql.Driver", "{PATH TO THE POSTGRESQL JDBC JAR}", "`")
```

Donde {PATH TO AL JAR JDBC POSTGRESQL} representa la ruta al JAR JDBC PostgreSQL que se instaló en el equipo.

Ahora, puede crear la conexión al servicio de Consulta introduciendo el siguiente comando en la consola:

```console
qsconnection <- dbConnect(pgsql, "jdbc:postgresql://{HOSTNAME}:{PORT}/{DATABASE_NAME}?user={USERNAME}&password={PASSWORD}&sslmode=require")
```

>[!NOTE]
>
>Para obtener más información sobre cómo encontrar el nombre de la base de datos, el host, el puerto y las credenciales de inicio de sesión, visite la [página de credenciales en la plataforma](https://platform.adobe.com/query/configuration). Para encontrar sus credenciales, inicie sesión en [!DNL Platform] y luego seleccione **[!UICONTROL Consultas]**, seguido de **[!UICONTROL Credenciales]**.

![](../images/clients/rstudio/connection-rjdbc.png)

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