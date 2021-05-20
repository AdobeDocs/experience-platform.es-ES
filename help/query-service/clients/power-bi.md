---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;servicio de consulta;Power BI;power bi;conexión al servicio de consulta;
solution: Experience Platform
title: Conectar Power BI al servicio de consulta
topic-legacy: connect
description: Este documento recorre los pasos para conectar la Power BI con el servicio de consulta de Adobe Experience Platform.
exl-id: 8fcd3056-aac7-4226-a354-ed7fb8fe9ad7
source-git-commit: 2109abd02b9c6c321c21a8fe3826509d22b1c2e2
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 1%

---

# Conectar [!DNL Power BI] al servicio de consulta (PC)

Este documento cubre los pasos para conectar el Power BI con el servicio de consulta de Adobe Experience Platform.

>[!NOTE]
>
> Esta guía asume que ya tiene acceso a [!DNL Power BI] y está familiarizado con cómo navegar por su interfaz. Puede encontrar más información sobre [!DNL Power BI] en la [oficial [!DNL Power BI] documentación](https://docs.microsoft.com/es-ES/power-bi/).
>
> Además, la Power BI **solo** está disponible en dispositivos Windows.

Después de instalar Power BI, deberá instalar `Npgsql`, un paquete de controladores .NET para PostgreSQL. Puede encontrar más información sobre Npgsql en la [documentación de Npgsql](https://www.npgsql.org/doc/index.html).

>[!IMPORTANT]
>
>Debe descargar la versión 4.0.10 o anterior, ya que las versiones más recientes dan como resultado errores.

En &quot;[!DNL Npgsql GAC Installation]&quot; en la pantalla de configuración personalizada, seleccione **[!DNL Will be installed on local hard drive]**.

Para asegurarse de que npgsql se haya instalado correctamente, reinicie el equipo antes de seguir los pasos siguientes.

## Conectar [!DNL Power BI] a [!DNL Query Service]

Para conectar [!DNL Power BI] a [!DNL Query Service], abra [!DNL Power BI] y seleccione **[!DNL Get Data]** en la cinta del menú superior.

![](../images/clients/power-bi/open-power-bi.png)

Seleccione **[!DNL PostgreSQL database]**, seguido de **[!DNL Connect]**.

![](../images/clients/power-bi/get-data.png)

Ahora puede introducir valores para el servidor y la base de datos. Para obtener más información sobre cómo encontrar el nombre de la base de datos, el host, el puerto y las credenciales de inicio de sesión, visite la página [credenciales de Platform](https://platform.adobe.com/query/configuration). Para encontrar sus credenciales, inicie sesión en [!DNL Platform], luego seleccione **[!UICONTROL Consultas]**, seguido de **[!UICONTROL Credenciales]**.

**[!DNL Server]** es el host que se encuentra en los detalles de conexión. Para la producción, agregue el puerto `:80` al final de la cadena de host. **[!DNL Database]** puede ser &quot;todo&quot; o un nombre de tabla de conjunto de datos.

Además, puede seleccionar su **[!DNL Data Connectivity mode]**. Seleccione **[!DNL Import]** para mostrar una lista de todas las tablas disponibles o seleccione **[!DNL DirectQuery]** para crear directamente una consulta.

Para obtener más información sobre el modo **[!DNL Import]**, lea la sección sobre [previsualización e importación de una tabla](#preview). Para obtener más información sobre el modo **[!DNL DirectQuery]**, lea la sección sobre [creación de instrucciones SQL](#create). Seleccione **[!DNL OK]** después de confirmar los detalles de la base de datos.

![](../images/clients/power-bi/connectivity-mode.png)

Aparecerá una solicitud de confirmación que solicita su nombre de usuario, contraseña y configuración de la aplicación. Complete estos detalles y luego seleccione **[!DNL Connect]** para continuar con el siguiente paso.

![](../images/clients/power-bi/import-mode.png)

## Vista previa e importación de una tabla {#preview}

Si ha seleccionado el modo **[!DNL Import]**, aparece un cuadro de diálogo que muestra una lista de todas las tablas disponibles. Seleccione la tabla de la que desea obtener una vista previa, seguida de **[!DNL Load]** para introducir el conjunto de datos en [!DNL Power BI].

![](../images/clients/power-bi/preview-table.png)

La tabla ahora se importa en Power BI.

![](../images/clients/power-bi/import-table.png)

## Crear instrucciones SQL {#create}

Si ha seleccionado el modo **[!DNL DirectQuery]**, deberá rellenar la sección Opciones avanzadas con la consulta SQL que desee crear.

En **[!DNL SQL statement]**, inserte la consulta SQL que desee crear. Asegúrese de que la casilla de verificación etiquetada **[!DNL Include relationship columns]** está seleccionada. Una vez que haya escrito la consulta, seleccione **[!DNL OK]** para continuar.

![](../images/clients/power-bi/direct-query-mode.png)

Aparecerá una vista previa de la consulta. Seleccione **[!DNL Load]** para ver los resultados de la consulta.

![](../images/clients/power-bi/preview-direct-query.png)

## Pasos siguientes

Ahora que se ha conectado con [!DNL Query Service], puede utilizar [!DNL Power BI] para escribir consultas. Para obtener más información sobre cómo escribir y ejecutar consultas, lea la guía sobre [consultas en ejecución](../best-practices/writing-queries.md).
