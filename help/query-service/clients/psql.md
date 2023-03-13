---
keywords: Experience Platform;inicio;temas populares;PSQL;psqlconnect al servicio de consultas;servicio de consultas;servicio de consultas;
solution: Experience Platform
title: Conectar PSQL al servicio de consultas
description: PSQL es una interfaz de línea de comandos que se proporciona al instalar PostgreSQL en el equipo. Puede instalarlo siguiendo estas instrucciones.
exl-id: ceb07128-409e-42be-8143-0cf681d435de
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# Conectar PSQL al servicio de consultas

PSQL es una interfaz de línea de comandos que se instala al instalar [!DNL PostgreSQL] en su máquina. Este documento describe los pasos para conectar PSQL con Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> En esta guía se da por hecho que ya tiene acceso a [!DNL PSQL] y están familiarizados con su uso. Más información sobre [!DNL PSQL] se puede encontrar en la [funcionario [!DNL PSQL] documentación](https://www.postgresql.org/docs/current/app-psql.html).

Después de instalar PSQL en el equipo, está listo para conectar PSQL con el servicio de consultas. Vuelva a la [!DNL Platform] IU y, a continuación, seleccione **[!UICONTROL Consultas]**, seguido de **[!UICONTROL Credenciales]**.

En el **[!UICONTROL Comando PSQL]** , seleccione la **[!UICONTROL Copiar al portapapeles]** icono (![Icono Copiar](../images/clients/psql/copy-icon.png)) para copiar la cadena de comando.

![La pestaña Credenciales del panel Consultas con el icono de copia resaltado.](../images/clients/psql/connect-bi.png)

Pegue la cadena de comandos en un terminal o ventana de línea de comandos y pulse **Entrar** en el teclado.

>[!IMPORTANT]
>
>Si está en un equipo, utilice un editor de texto para eliminar los saltos de línea en la cadena de comando y, a continuación, copie la cadena. Si utiliza la versión 12.0 o buena, debe agregar lo siguiente `PGGSSENCMODE=disable` a la cadena de conexión. Además, si utiliza credenciales que no caducan, asegúrese de reemplazar el campo Contraseña por la contraseña de credencial que no caduca. Para obtener más información sobre las credenciales que no caducan, lea la [guía de credenciales](../ui/credentials.md).

Debería ver un resultado como este:

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

Si no ve al menos la versión 10.5, debe descargar esa versión o más reciente.

## Pasos siguientes

Ahora que se ha conectado con [!DNL Query Service], puede utilizar PSQL para escribir consultas. Para obtener más información sobre cómo escribir y ejecutar consultas, lea la guía sobre [ejecución de consultas](../best-practices/writing-queries.md).
