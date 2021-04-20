---
keywords: Experience Platform;inicio;temas populares;Azure Synapse Analytics;azure synapse analytics;Synapse;synapse
solution: Experience Platform
title: Descripción general del conector de origen de Azure Synapse Analytics
topic: overview
description: Obtenga información sobre cómo conectar Azure Synapse Analytics a Adobe Experience Platform mediante API o la interfaz de usuario.
translation-type: tm+mt
source-git-commit: 0fb97fcf5d3f8230ff86906aeef245e4a7f44f30
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 0%

---


# Conector (Beta) [!DNL Azure Synapse Analytics]

Adobe Experience Platform permite la ingesta de datos de fuentes externas, al tiempo que ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios [!DNL Platform]. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

[!DNL Experience Platform] permite la ingesta de datos desde una base de datos de terceros. [!DNL Platform] puede conectarse a diferentes tipos de bases de datos, como relacional, sinSQL o data warehouse. La compatibilidad con los proveedores de bases de datos incluye [!DNL Azure Synapse Analytics].

## Lista de permitidos de direcciones IP

Se debe agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no agrega las direcciones IP específicas de su región a la lista de permitidos, puede que se produzcan errores o que no se produzca un rendimiento al utilizar fuentes. Consulte la página [IP address allow list](../../ip-address-allow-list.md) para obtener más información.

>[!IMPORTANT]
>
>El conector de origen [!DNL Azure Synapse Analytics] actualmente no admite conectividad de la misma región con Platform. Esto significa que si la instancia de Azure está usando la misma región de red que Platform, no se puede establecer una conexión con orígenes de Platform. Actualmente, solo se admite la conectividad entre regiones. Póngase en contacto con el administrador de cuentas de Adobe para obtener más información.

La documentación siguiente proporciona información sobre cómo conectar [!DNL Azure Synapse Analytics] a [!DNL Platform] mediante API o la interfaz de usuario:

## Conectar [!DNL Azure Synapse Analytics] a [!DNL Platform] mediante API

- [Creación de una conexión de origen de Azure Synapse Analytics mediante la API de servicio de flujo](../../tutorials/api/create/databases/synapse-analytics.md)
- [Explorar un sistema de base de datos mediante la API de servicio de flujo](../../tutorials/api/explore/database-nosql.md)
- [Recopilación de datos de una base de datos mediante la API de servicio de flujo](../../tutorials/api/collect/database-nosql.md)

## Conectar [!DNL Azure Synapse Analytics] a [!DNL Platform] mediante la interfaz de usuario

- [Crear una conexión de origen de Azure Synapse Analytics en la interfaz de usuario](../../tutorials/ui/create/databases/synapse-analytics.md)
- [Configuración de un flujo de datos para una conexión de base de datos en la interfaz de usuario](../../tutorials/ui/dataflow/databases.md)