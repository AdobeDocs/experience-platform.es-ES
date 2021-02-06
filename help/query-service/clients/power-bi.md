---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;servicio de Consulta;Power BI;Power bi;conectar al servicio de consulta;
solution: Experience Platform
title: Conectar Power BI al servicio de Consulta
topic: connect
description: Este documento recorre los pasos para conectar el Power BI con el servicio de Consulta de Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 6655714d4b57d9c414cd40529bcee48c7bcd862d
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---


# Conectar [!DNL Power BI] al servicio de Consulta (PC)

Este documento cubre los pasos para la conexión de Power BI con el servicio de Consulta de Adobe Experience Platform.

>[!NOTE]
>
> En esta guía se asume que ya tiene acceso a [!DNL Power BI] y que está familiarizado con cómo navegar por su interfaz. Puede encontrar más información sobre [!DNL Power BI] en la [documentación oficial [!DNL Power BI] ](https://docs.looker.com/).
>
> Además, Power BI **sólo** está disponible en dispositivos Windows.

Después de instalar Power BI, deberá instalar `Npgsql`, un paquete de controladores .NET para PostgreSQL. Puede encontrar más información sobre Npgsql en la [documentación de Npgsql](https://www.npgsql.org/doc/index.html).

>[!IMPORTANT]
>
>Debe descargar la versión 4.0.10 o inferior, ya que las versiones más recientes producen errores.

En &quot;[!DNL Npgsql GAC Installation]&quot; en la pantalla de configuración personalizada, seleccione **[!DNL Will be installed on local hard drive]**.

Para asegurarse de que npgsql se ha instalado correctamente, reinicie el equipo antes de continuar con los siguientes pasos.

## Conectar [!DNL Power BI] a [!DNL Query Service]

Para conectar [!DNL Power BI] a [!DNL Query Service], abra [!DNL Power BI] y seleccione **[!DNL Get Data]** en la cinta del menú superior.

![](../images/clients/power-bi/open-power-bi.png)

Seleccione **[!DNL PostgreSQL database]**, seguido de **[!DNL Connect]**.

![](../images/clients/power-bi/get-data.png)

Ahora puede introducir valores para el servidor y la base de datos. Para obtener más información sobre cómo encontrar el nombre de la base de datos, el host, el puerto y las credenciales de inicio de sesión, visite la [página de credenciales en la plataforma](https://platform.adobe.com/query/configuration). Para encontrar sus credenciales, inicie sesión en [!DNL Platform] y luego seleccione **[!UICONTROL Consultas]**, seguido de **[!UICONTROL Credenciales]**.

**[!DNL Server]** es el host que se encuentra en los detalles de la conexión. Para producción, agregue el puerto `:80` al final de la cadena de host. **[!DNL Database]** puede ser &quot;todo&quot; o un nombre de tabla de conjunto de datos.

Además, puede seleccionar su **[!DNL Data Connectivity mode]**. Seleccione **[!DNL Import]** para mostrar una lista de todas las tablas disponibles o seleccione **[!DNL DirectQuery]** para crear directamente una consulta.

Para obtener más información sobre el modo **[!DNL Import]**, lea la sección sobre [vista previa e importación de una tabla](#preview). Para obtener más información sobre el modo **[!DNL DirectQuery]**, lea la sección sobre [creación de sentencias SQL](#create). Seleccione **[!DNL OK]** después de confirmar los detalles de la base de datos.

![](../images/clients/power-bi/connectivity-mode.png)

Aparece un mensaje que solicita el nombre de usuario, la contraseña y la configuración de la aplicación. Complete estos detalles y seleccione **[!DNL Connect]** para continuar con el paso siguiente.

![](../images/clients/power-bi/import-mode.png)

## Previsualización e importación de una tabla {#preview}

Si ha seleccionado el modo **[!DNL Import]**, aparece un cuadro de diálogo que muestra una lista de todas las tablas disponibles. Seleccione la tabla que desee previsualización, seguida de **[!DNL Load]** para traer el conjunto de datos a [!DNL Power BI].

![](../images/clients/power-bi/preview-table.png)

La tabla ahora se importa en Power BI.

![](../images/clients/power-bi/import-table.png)

## Crear sentencias SQL {#create}

Si ha seleccionado el modo **[!DNL DirectQuery]**, deberá completar la sección Opciones avanzadas con la consulta SQL que desee crear.

En **[!DNL SQL statement]**, inserte la consulta SQL que desee crear. Asegúrese de que la casilla de verificación rotulada **[!DNL Include relationship columns]** está seleccionada. Una vez que haya escrito la consulta, seleccione **[!DNL OK]** para continuar.

![](../images/clients/power-bi/direct-query-mode.png)

Aparece una previsualización de la consulta. Seleccione **[!DNL Load]** para ver los resultados de la consulta.

![](../images/clients/power-bi/preview-direct-query.png)

## Pasos siguientes

Ahora que se ha conectado con [!DNL Query Service], puede utilizar [!DNL Power BI] para escribir consultas. Para obtener más información sobre cómo escribir y ejecutar consultas, lea la guía sobre [consultas en ejecución](../best-practices/writing-queries.md).