---
keywords: Experience Platform;inicio;temas populares;PSQL;psqlconnect al servicio de consultas;servicio de consultas;servicio de consultas;
solution: Experience Platform
title: Conectar PSQL al servicio de consultas
description: PSQL es una interfaz de línea de comandos que se proporciona al instalar PostgreSQL en el equipo. Puede instalarlo siguiendo estas instrucciones.
exl-id: ceb07128-409e-42be-8143-0cf681d435de
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---

# Conectar PSQL al servicio de consultas

PSQL es una interfaz de línea de comandos que se instala al instalar [!DNL PostgreSQL] en el equipo. Este documento describe los pasos para conectar PSQL con Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> En esta guía se da por hecho que ya tiene acceso a [!DNL PSQL] y que está familiarizado con su uso. Encontrará más información sobre [!DNL PSQL] en la [documentación oficial [!DNL PSQL] 3}.](https://www.postgresql.org/docs/current/app-psql.html)

Después de instalar PSQL en el equipo, está listo para conectar PSQL con el servicio de consultas. Vuelva a la interfaz de usuario [!DNL Experience Platform] y, a continuación, seleccione **[!UICONTROL Consultas]**, seguidas de **[!UICONTROL Credenciales]**.

En la sección **[!UICONTROL Comando PSQL]**, seleccione el icono **[!UICONTROL Copiar al portapapeles]** (![Icono Copiar](/help/images/icons/copy.png)) para copiar la cadena de comandos.

![Pestaña Credenciales del panel de consultas con el icono de copia resaltado.](../images/clients/psql/connect-bi.png)

Pegue la cadena de comando en un terminal o ventana de línea de comandos y presione **Enter** en el teclado.

>[!IMPORTANT]
>
>Si está en un equipo, utilice un editor de texto para eliminar los saltos de línea en la cadena de comando y, a continuación, copie la cadena. Si usa la versión 12.0 o superior de, deberá agregar `PGGSSENCMODE=disable` a la cadena de conexión. Además, si utiliza credenciales que no caducan, asegúrese de reemplazar el campo Contraseña por la contraseña de credencial que no caduca. Para obtener más información sobre las credenciales que no caducan, lea la [guía de credenciales](../ui/credentials.md).

Debería ver un resultado como este:

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

Si no ve al menos la versión 10.5, debe descargar esa versión o más reciente.

## Pasos siguientes

Ahora que se ha conectado con [!DNL Query Service], puede usar PSQL para escribir consultas. Para obtener más información sobre cómo escribir y ejecutar consultas, lea la guía sobre [ejecutar consultas](../best-practices/writing-queries.md).
