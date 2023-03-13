---
keywords: Experience Platform;inicio;temas populares;servicio de consultas;servicio de consultas;RStudio;rstudio;conectarse al servicio de consultas;
solution: Experience Platform
title: Conectar RSstudio al servicio de consultas
description: Este documento explica los pasos para conectar R Studio con Adobe Experience Platform Query Service.
exl-id: 8dd82bad-6ffb-4536-9c27-223f471a49c6
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# Connect [!DNL RStudio] al servicio de consultas

Este documento muestra los pasos para la conexión [!DNL RStudio] con Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> [!DNL RStudio] ahora se ha cambiado de marca como [!DNL Posit]. [!DNL RStudio] productos se han renombrado a [!DNL Posit Connect], [!DNL Posit Workbench], [!DNL Posit Package] Responsable, [!DNL Posit Cloud], y [!DNL Posit Academy].
>
> En esta guía se da por hecho que ya tiene acceso a [!DNL RStudio] y están familiarizados con su uso. Más información sobre [!DNL RStudio] se puede encontrar en la [funcionario [!DNL RStudio] documentación](https://rstudio.com/products/rstudio/).
> 
> Además, para utilizar [!DNL RStudio] con el servicio de consultas, debe instalar el [!DNL PostgreSQL] Controlador JDBC 4.2. Puede descargar el controlador JDBC desde el [[!DNL PostgreSQL] sitio oficial](https://jdbc.postgresql.org/download/).

## Crear un [!DNL Query Service] conexión en el [!DNL RStudio] interfaz

Después de la instalación [!DNL RStudio], debe instalar el paquete RJDBC. Instrucciones sobre cómo [conectar una base de datos a través de la línea de comandos](https://solutions.posit.co/connections/db/best-practices/drivers/#connecting-to-a-database-in-r) se puede encontrar en la documentación oficial de Posit.

Si utiliza un sistema operativo Mac, puede seleccionar **[!UICONTROL Herramientas]** en la barra de menús, seguido de **[!UICONTROL Paquetes de instalación]** en el menú desplegable. Como alternativa, seleccione la **[!DNL Packages]** en la interfaz de usuario de RStudio y seleccione **[!DNL Install]**.

Aparece una ventana emergente que muestra el **[!DNL Install Packages]** pantalla. Asegúrese de que **[!DNL Repository (CRAN)]** está seleccionado para la **[!DNL Install from]** sección. El valor de **[!DNL Packages]** debería ser `RJDBC`. Asegurar **[!DNL Install dependencies]** está seleccionado. Después de confirmar que todos los valores son correctos, seleccione **[!DNL Install]** para instalar los paquetes. Ahora que se ha instalado el paquete RJDBC, reinicie [!DNL RStudio] para completar el proceso de instalación.

Después [!DNL RStudio] se ha reiniciado, ahora puede conectarse al servicio de consultas. Seleccione el **[!DNL RJDBC]** paquete en el **[!DNL Packages]** y escriba el siguiente comando en la consola:

```console
pgsql <- JDBC("org.postgresql.Driver", "{PATH TO THE POSTGRESQL JDBC JAR}", "`")
```

Donde `{PATH TO THE POSTGRESQL JDBC JAR}` representa la ruta al [!DNL PostgreSQL] JAR de JDBC instalado en el equipo.

Ahora puede crear su conexión al servicio de consultas. Introduzca el siguiente comando en la consola:

```console
qsconnection <- dbConnect(pgsql, "jdbc:postgresql://{HOSTNAME}:{PORT}/{DATABASE_NAME}?user={USERNAME}&password={PASSWORD}&sslmode=require")
```

>[!IMPORTANT]
>
>Consulte la [[!DNL Query Service] Documentación SSL](./ssl-modes.md) para obtener más información sobre la compatibilidad de SSL para conexiones de terceros con Adobe Experience Platform Query Service y cómo conectarse mediante `verify-full` Modo SSL.

Para obtener más información sobre cómo encontrar el nombre de la base de datos, el host, el puerto y las credenciales de inicio de sesión, lea la [guía de credenciales](../ui/credentials.md). Para encontrar sus credenciales, inicie sesión en [!DNL Platform], luego seleccione **[!UICONTROL Consultas]**, seguido de **[!UICONTROL Credenciales]**.

Un mensaje en la salida de la consola confirma la conexión con el servicio de consultas.

## Escritura de consultas

Ahora que se ha conectado a [!DNL Query Service], puede escribir consultas para ejecutar y editar instrucciones SQL. Por ejemplo, puede utilizar `dbGetQuery(con, sql)` para ejecutar consultas, donde `sql` es la consulta SQL que desea ejecutar.

La siguiente consulta utiliza un conjunto de datos que contiene [Eventos de experiencia](../../xdm/classes/experienceevent.md) y crea un histograma de las vistas de página de un sitio web, dada la altura de pantalla del dispositivo.

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

Para obtener más información sobre cómo escribir y ejecutar consultas, lea la guía sobre [ejecución de consultas](../best-practices/writing-queries.md).
