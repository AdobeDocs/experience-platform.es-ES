---
keywords: Experience Platform;inicio;temas populares;servicio de consultas;servicio de consultas;RStudio;rstudio;conectarse al servicio de consultas;
solution: Experience Platform
title: Conectar RSstudio al servicio de consultas
description: Este documento explica los pasos para conectar R Studio con Adobe Experience Platform Query Service.
exl-id: 8dd82bad-6ffb-4536-9c27-223f471a49c6
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---

# Conectar [!DNL RStudio] al servicio de consultas

Este documento explica los pasos para conectar [!DNL RStudio] con Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> [!DNL RStudio] se ha cambiado a [!DNL Posit]. Se cambió el nombre de [!DNL RStudio] productos a [!DNL Posit Connect], [!DNL Posit Workbench], [!DNL Posit Package], [!DNL Posit Cloud], y [!DNL Posit Academy].
>
> En esta guía se da por hecho que ya tiene acceso a [!DNL RStudio] y que está familiarizado con su uso. Encontrará más información sobre [!DNL RStudio] en la [documentación oficial [!DNL RStudio] 3&rbrace;.](https://rstudio.com/products/rstudio/)
> 
> Además, para usar [!DNL RStudio] con el servicio de consultas, debe instalar el controlador JDBC 4.2 de [!DNL PostgreSQL]. Puede descargar el controlador JDBC desde el [[!DNL PostgreSQL] sitio oficial](https://jdbc.postgresql.org/download/).

## Crear una conexión [!DNL Query Service] en la interfaz [!DNL RStudio]

Después de instalar [!DNL RStudio], debe instalar el paquete RJDBC. Las instrucciones sobre cómo [conectar una base de datos a través de la línea de comandos](https://solutions.posit.co/connections/db/best-practices/drivers/#connecting-to-a-database-in-r) se encuentran en la documentación oficial de Posit.

Si usa un sistema operativo Mac, puede seleccionar **[!UICONTROL Herramientas]** en la barra de menús seguida de **[!UICONTROL Instalar paquetes]** en el menú desplegable. También puede seleccionar la ficha **[!DNL Packages]** en la interfaz de usuario de RStudio y seleccionar **[!DNL Install]**.

Aparece una ventana emergente que muestra la pantalla **[!DNL Install Packages]**. Asegúrese de que **[!DNL Repository (CRAN)]** esté seleccionado para la sección **[!DNL Install from]**. El valor de **[!DNL Packages]** debe ser `RJDBC`. Asegúrese de que **[!DNL Install dependencies]** esté seleccionado. Después de confirmar que todos los valores son correctos, seleccione **[!DNL Install]** para instalar los paquetes. Ahora que se ha instalado el paquete RJDBC, reinicie [!DNL RStudio] para completar el proceso de instalación.

Después de reiniciar [!DNL RStudio], ahora puede conectarse al Servicio de consultas. Seleccione el paquete **[!DNL RJDBC]** en el panel **[!DNL Packages]** e introduzca el siguiente comando en la consola:

```console
pgsql <- JDBC("org.postgresql.Driver", "{PATH TO THE POSTGRESQL JDBC JAR}", "`")
```

Donde `{PATH TO THE POSTGRESQL JDBC JAR}` representa la ruta de acceso al JAR JDBC [!DNL PostgreSQL] instalado en el equipo.

Ahora puede crear su conexión al servicio de consultas. Introduzca el siguiente comando en la consola:

```console
qsconnection <- dbConnect(pgsql, "jdbc:postgresql://{HOSTNAME}:{PORT}/{DATABASE_NAME}?user={USERNAME}&password={PASSWORD}&sslmode=require")
```

>[!IMPORTANT]
>
>Consulte la [[!DNL Query Service] documentación SSL](./ssl-modes.md) para obtener más información sobre la compatibilidad de SSL para conexiones de terceros con el servicio Adobe Experience Platform Query y cómo conectarse mediante el modo SSL `verify-full`.

Para obtener más información sobre cómo encontrar el nombre de la base de datos, el host, el puerto y las credenciales de inicio de sesión, lea la [guía de credenciales](../ui/credentials.md). Para encontrar sus credenciales, inicie sesión en [!DNL Experience Platform] y luego seleccione **[!UICONTROL Consultas]**, seguidas de **[!UICONTROL Credenciales]**.

Un mensaje en la salida de la consola confirma la conexión con el servicio de consultas.

## Escritura de consultas

Ahora que se ha conectado a [!DNL Query Service], puede escribir consultas para ejecutar y editar instrucciones SQL. Por ejemplo, puede usar `dbGetQuery(con, sql)` para ejecutar consultas, donde `sql` es la consulta SQL que desea ejecutar.

La siguiente consulta utiliza un conjunto de datos que contiene [Eventos de experiencia](../../xdm/classes/experienceevent.md) y crea un histograma de vistas de página de un sitio web, dada la altura de pantalla del dispositivo.

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

Para obtener más información sobre cómo escribir y ejecutar consultas, lea la guía sobre [ejecutar consultas](../best-practices/writing-queries.md).
