---
keywords: Experience Platform;inicio;temas populares;Microsoft SQL;microsoft sql;SQL;sql
solution: Experience Platform
title: Información general del conector de origen de SQL Server
topic-legacy: overview
description: Obtenga información sobre cómo conectar Microsoft SQL Server a Adobe Experience Platform mediante API o la interfaz de usuario.
exl-id: 8a77f108-7e82-4e14-a470-a4ea97def89d
source-git-commit: 5821f9304a37c1a03d17f0113d09548799662a2e
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# [!DNL Microsoft] Conector de SQL Server

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante los servicios [!DNL Platform]. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

[!DNL Experience Platform] permite la ingesta de datos desde una base de datos de terceros. [!DNL Platform] puede conectarse a diferentes tipos de bases de datos, como relacional, sinSQL o data warehouse. La compatibilidad con proveedores de bases de datos incluye [!DNL Microsoft] SQL Server.

## LISTA DE PERMITIDOS de direcciones IP

Se debe agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no agrega las direcciones IP específicas de su región a su lista de permitidos, puede que se produzcan errores o que no se produzca un rendimiento al utilizar fuentes. Consulte la página [lista de permitidos de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

>[!IMPORTANT]
>
>El conector de origen [!DNL Microsoft] de SQL Server actualmente no admite conectividad de la misma región con Platform. Esto significa que si la instancia de Azure está usando la misma región de red que Platform, no se puede establecer una conexión con orígenes de Platform. Actualmente, solo se admite la conectividad entre regiones. Póngase en contacto con el administrador de cuentas de Adobe para obtener más información.

La documentación siguiente proporciona información sobre cómo conectar [!DNL Microsoft] SQL Server a [!DNL Platform] mediante API o la interfaz de usuario:

## Conectar [!DNL Microsoft] SQL Server a [!DNL Platform] mediante API

- [Creación de una conexión base de Microsoft SQL Server mediante la API de servicio de flujo](../../tutorials/api/create/databases/sql-server.md)
- [Explorar la estructura de datos y el contenido de un origen de base de datos mediante la API de servicio de flujo](../../tutorials/api/explore/database-nosql.md)
- [Creación de un flujo de datos para un origen de base de datos mediante la API de servicio de flujo](../../tutorials/api/collect/database-nosql.md)

## Conectar [!DNL Microsoft] SQL Server a [!DNL Platform] mediante la interfaz de usuario

- [Crear una conexión de origen de Microsoft SQL Server en la interfaz de usuario](../../tutorials/ui/create/databases/sql-server.md)
- [Crear un flujo de datos para una conexión de origen de base de datos en la interfaz de usuario](../../tutorials/ui/dataflow/databases.md)
