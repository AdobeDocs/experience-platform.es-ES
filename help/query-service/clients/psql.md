---
keywords: Experience Platform;inicio;temas populares;PSQL;psqlconnect al servicio de consulta;servicio de consulta;servicio de consulta;
solution: Experience Platform
title: Conexión de PSQL al servicio de consulta
topic-legacy: connect
description: PSQL es una interfaz de línea de comandos que viene cuando instala PostgreSQL en su equipo. Puede instalarlo siguiendo estas instrucciones.
exl-id: ceb07128-409e-42be-8143-0cf681d435de
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 1%

---

# Conexión de PSQL al servicio de consulta

PSQL es una interfaz de línea de comandos que se instala al instalar [!DNL PostgreSQL] en el equipo. Este documento cubre los pasos para conectar PSQL con Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> En esta guía se da por hecho que ya tiene acceso a [!DNL PSQL] y está familiarizado con su uso. Puede encontrar más información sobre [!DNL PSQL] en la [documentación oficial [!DNL PSQL]](https://www.postgresql.org/docs/current/app-psql.html.

Después de instalar PSQL en el equipo, está listo para conectar PSQL con el servicio de consulta. Vuelva a la [!DNL Platform] interfaz de usuario y, a continuación, seleccione **[!UICONTROL Queries]**, seguido de **[!UICONTROL Credentials]**.

![Imagen](../images/clients/psql/connect-bi.png)

Seleccione el icono para copiar la sección etiquetada **[!UICONTROL PSQL Command]** y luego pegue la cadena de comandos en un terminal o ventana de línea de comandos antes de pulsar Intro.

>[!IMPORTANT]
>
>Si está en un equipo, utilice un editor de texto para eliminar los saltos de línea en la cadena de comandos y, a continuación, copie la cadena. Además, si utiliza la versión 12.0 o la buena, deberá agregar `PGGSSENCMODE=disable` a la cadena de conexión.

Debería ver un resultado como este:

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

Si no ve al menos la versión 10.5, entonces necesita descargar esa versión o más reciente.

## Pasos siguientes

Ahora que se ha conectado con [!DNL Query Service], puede utilizar PSQL para escribir consultas. Para obtener más información sobre cómo escribir y ejecutar consultas, lea la guía sobre [consultas en ejecución](../best-practices/writing-queries.md).
