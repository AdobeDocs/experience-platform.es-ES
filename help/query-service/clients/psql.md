---
keywords: Experience Platform;home;popular topics;PSQL;psqlconnect to query service;Query service;query service;
solution: Experience Platform
title: Conectar con PSQL
topic: connect
description: 'PSQL es una interfaz de línea de comandos que se presenta al instalar Postgres en el equipo. Puede instalarlo siguiendo estas instrucciones. '
translation-type: tm+mt
source-git-commit: 8ffe7c68c87cacb6b54d9634a5204fa24a9986ac
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---


# Conectar con PSQL

PSQL es una interfaz de línea de comandos que viene cuando se instala [!DNL Postgres] en el equipo. Puede instalarlo siguiendo estas instrucciones.

## Instalación de posters en un Mac

Abra una ventana de terminal y ejecute estos tres comandos:

```shell
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

```shell
brew install postgres
```

```shell
which psql
```

Después de ejecutar estos comandos, debe ver lo siguiente:

```shell
/usr/local/bin/psql
```

## Instalar [!DNL Postgres] en un PC

Descargue e instale [!DNL Postgres] desde esta [ubicación](https://www.postgresql.org/download/windows/).

Edite la variable de ruta:

![Imagen](../images/clients/psql/path.png)

Añada las dos líneas mostradas que incluyen &quot;[!DNL Postgres]&quot;.

Guarde las actualizaciones y, a continuación, abra un símbolo del sistema y escriba:

```shell
psql -V
```

Deberías ver algo como esto:

```shell
psql (PostgreSQL) 9.5.14
```

## Connect PSQL y [!DNL Query Service]

Vuelva a la [!DNL Platform] IU en la página Herramientas **[!UICONTROL de]** Connect BI.

Haga clic en **[!UICONTROL Copiar]** para el comando **[!UICONTROL PSQL]**.

![Imagen](../images/clients/psql/connect-bi.png)

>[!IMPORTANT]
>
>Si está en un equipo, utilice un editor de texto para eliminar los saltos de línea en la cadena de comandos y, a continuación, copie la cadena. Además, si utiliza la versión 12.0 o buena, deberá agregar `PGGSSENCMODE=disable` a la cadena de conexión.

Pegue la cadena de comandos en un terminal o ventana de comandos y pulse Intro.

Debería ver un resultado como este:

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

Si no ve al menos la versión 10.5, deberá descargar esa versión o una más reciente.