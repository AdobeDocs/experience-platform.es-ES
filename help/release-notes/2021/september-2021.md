---
title: Notas de la versión de Adobe Experience Platform
description: Las notas de la versión más recientes de Adobe Experience Platform.
exl-id: 96375409-803f-45af-805e-900207d972e4
source-git-commit: 57089cc9aa9c586f5fae70e2a7154d48ebd62447
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 11%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de versión: 29 de septiembre de 2021**

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [Ingesta de datos](#ingestion)
- [[!DNL Data Prep]](#data-prep)
- [Fuentes](#sources)

## Ingesta de datos {#ingestion}

La ingesta de datos de Adobe Experience Platform representa los múltiples métodos mediante los cuales Platform ingesta datos de varias fuentes, así como la forma en que se mantienen esos datos dentro del lago de datos para su uso por parte de los servicios de Platform descendente.

**Nuevas funciones**

| Función | Descripción |
|------- | -----------|
| Actualizar o aplicar parches registros de perfil utilizando la ingesta por lotes | El perfil del cliente en tiempo real ahora permite actualizar los atributos de perfil en datos de registro de perfil individuales mediante la ingesta por lotes. Para obtener más información, consulte la [guía para desarrolladores de ingesta por lotes](../../ingestion/batch-ingestion/api-overview.md). |

Para obtener más información sobre la ingesta de datos en Platform, visite la [Documentación sobre la ingesta de datos](../../ingestion/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el modelo de datos de Experience (XDM).

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Compatibilidad con flujos de datos de flujo continuo | Ahora puede utilizar funciones de preparación de datos al crear un flujo de datos de flujo continuo para [!DNL Amazon Kinesis], [!DNL Azure Event Hubs] y [!DNL Google PubSub]. Consulte el tutorial sobre [creación de un flujo de datos de flujo continuo para fuentes de almacenamiento en la nube](../../sources/tutorials/ui/dataflow/streaming/cloud-storage-streaming.md) para obtener más información. |

Para obtener más información sobre [!DNL Data Prep], consulte [[!DNL Data Prep] overview](../../data-prep/home.md).

## Fuentes {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas, al mismo tiempo que le permite estructurarlos, etiquetarlos y mejorarlos mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API de RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecutar la ingesta y administrar el rendimiento de ingesta de datos.

| Función | Descripción |
| --- | --- |
| [!DNL Data Landing Zone] | Ahora puede crear una conexión de origen [!DNL Data Landing Zone] utilizando la [[!DNL Flow Service] API](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) o la [interfaz de usuario](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md). [!DNL Data Landing Zone] es una interfaz de  [!DNL Azure Blob] almacenamiento de información aprovisionada por Platform, que le permite acceder a un servicio de almacenamiento de archivos seguro y basado en la nube para introducir archivos en Platform. Consulte [[!DNL Data Landing Zone] overview](../../sources/connectors/cloud-storage/data-landing-zone.md) para obtener más información. |
| [!DNL Snowflake] | Ahora puede crear una conexión de origen [!DNL Snowflake] utilizando la [[!DNL Flow Service] API](../../sources/tutorials/api/create/databases/snowflake.md) o la [interfaz de usuario](../../sources/tutorials/ui/create/databases/snowflake.md) para llevar los datos de la base de datos [!DNL Snowflake] a Platform. Consulte [[!DNL Snowflake] overview](../../sources/connectors/databases/snowflake.md) para obtener más información. |
| [!DNL SFTP] mejoras de la fuente | Puede establecer manualmente un número de puerto personalizado al crear una conexión de origen [!DNL SFTP]. Consulte [[!DNL SFTP] overview](../../sources/connectors/cloud-storage/sftp.md) para obtener más información. |

Para obtener más información sobre las fuentes, consulte [sources overview](../../sources/home.md).
