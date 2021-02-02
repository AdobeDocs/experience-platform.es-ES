---
keywords: Experience Platform;inicio;temas populares;PSQL;psqlconnect al servicio de consulta;servicio de Consulta;servicio de consulta;
solution: Experience Platform
title: Conectar con PSQL
topic: connect
description: 'PSQL es una interfaz de línea de comandos que se presenta al instalar PostgreSQL en el equipo. Puede instalarlo siguiendo estas instrucciones. '
translation-type: tm+mt
source-git-commit: bc1bbdddd75b11ac180b5e6faa391fd74e5f7e02
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 1%

---


# PSQL

PSQL es una interfaz de línea de comandos que se instala al instalar [!DNL PostgreSQL] en el equipo. Este documento cubre los pasos para conectar PSQL con Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Esta guía asume que ya tiene acceso a [!DNL PSQL] y está familiarizado con cómo utilizarlo. Puede encontrar más información sobre [!DNL PSQL] en la [documentación oficial [!DNL PSQL]](https://www.postgresql.org/docs/current/app-psql.html.

## Connect PSQL y [!DNL Query Service]

Después de instalar PSQL en el equipo, ya puede conectar PSQL con el servicio de Consulta. Vuelva a la [!DNL Platform] interfaz de usuario y seleccione **[!UICONTROL Consultas]**, seguido de **[!UICONTROL Credenciales]**.

![Imagen](../images/clients/psql/connect-bi.png)

Seleccione el icono para copiar la sección rotulada **[!UICONTROL Comando PSQL]** y luego pegue la cadena de comandos en una ventana de terminal o de línea de comandos antes de pulsar Intro.

>[!IMPORTANT]
>
>Si está en un equipo, utilice un editor de texto para eliminar los saltos de línea en la cadena de comandos y, a continuación, copie la cadena. Además, si utiliza la versión 12.0 o buena, deberá agregar `PGGSSENCMODE=disable` a la cadena de conexión.

Debería ver un resultado como este:

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

Si no ve al menos la versión 10.5, deberá descargar esa versión o una más reciente.

## Pasos siguientes

Ahora que se ha conectado con [!DNL Query Service], puede utilizar PSQL para escribir consultas. Para obtener más información sobre cómo escribir y ejecutar consultas, lea la guía sobre [consultas en ejecución](../best-practices/writing-queries.md).