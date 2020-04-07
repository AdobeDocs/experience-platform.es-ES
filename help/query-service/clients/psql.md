---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Conectar con PSQL
topic: connect
translation-type: tm+mt
source-git-commit: f5bc9beb59e83b0411d98d901d5055122a124d07

---


# Conectar con PSQL

PSQL es una interfaz de línea de comandos que se presenta al instalar Postgres en el equipo. Puede instalarlo siguiendo estas instrucciones.

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

## Instalar posters en un PC

Descargue e instale Postgres desde esta [ubicación](https://www.postgresql.org/download/windows/).

Edite la variable de ruta:

![Imagen](../images/clients/psql/path.png)

Añada las dos líneas que se muestran y que incluyen &quot;Posturas&quot;.

Guarde las actualizaciones y, a continuación, abra un símbolo del sistema y escriba:

```shell
psql -V
```

Deberías ver algo como esto:

```shell
psql (PostgreSQL) 9.5.14
```

## Connect PSQL y el servicio de Consulta

Vuelva a la interfaz de usuario de la plataforma en la página &quot;Herramientas de Connect BI&quot;.

Haga clic en **copiar** para &quot;Comando PSQL&quot;.

![Imagen](../images/clients/psql/connect-bi.png)

>[!IMPORTANT]:: Si está en un equipo, utilice un editor de texto para eliminar los saltos de línea en la cadena de comandos y, a continuación, copie la cadena.

Pegue la cadena de comandos en un terminal o ventana de comandos y pulse Intro.

Debería ver un resultado como este:

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

Si no ve al menos la versión 10.5, deberá descargar esa versión o una más reciente.