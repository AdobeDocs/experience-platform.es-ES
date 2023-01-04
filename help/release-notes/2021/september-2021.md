---
title: Notas de la versión de Adobe Experience Platform, septiembre de 2021
description: Notas de la versión de septiembre de 2021 para Adobe Experience Platform.
exl-id: 96375409-803f-45af-805e-900207d972e4
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 8%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 29 de septiembre de 2021**

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [Ingesta de datos](#ingestion)
- [[!DNL Data Prep]](#data-prep)
- [Fuentes](#sources)

## Ingesta de datos {#ingestion}

La ingesta de datos de Adobe Experience Platform representa los múltiples métodos mediante los cuales Platform ingesta datos de varias fuentes, así como la forma en que se mantienen esos datos dentro del lago de datos para su uso por parte de los servicios de Platform descendente.

**Nuevas funciones**

| Función | Descripción |
|------- | -----------|
| Actualizar o aplicar parches registros de perfil utilizando la ingesta por lotes | El perfil del cliente en tiempo real ahora permite actualizar los atributos de perfil en datos de registro de perfil individuales mediante ingesta por lotes. Para obtener más información, consulte [guía para desarrolladores sobre ingesta por lotes](../../ingestion/batch-ingestion/api-overview.md). |

Para obtener más información sobre la ingesta de datos en Platform, visite [Documentación de ingesta de datos](../../ingestion/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el modelo de datos de Experience (XDM).

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Compatibilidad con flujos de datos de flujo continuo | Ahora puede utilizar funciones de preparación de datos al crear un flujo de datos de flujo continuo para [!DNL Amazon Kinesis], [!DNL Azure Event Hubs]y [!DNL Google PubSub]. Consulte el tutorial en [creación de un flujo de datos de flujo continuo para las fuentes de almacenamiento en la nube](../../sources/tutorials/ui/dataflow/streaming/cloud-storage-streaming.md) para obtener más información. |

Para obtener más información sobre [!DNL Data Prep] consulte la [[!DNL Data Prep] información general](../../data-prep/home.md).

## Fuentes {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas, al mismo tiempo que le permite estructurarlos, etiquetarlos y mejorarlos mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API de RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecutar la ingesta y administrar el rendimiento de ingesta de datos.

| Función | Descripción |
| --- | --- |
| [!DNL Data Landing Zone] | Ahora puede crear un [!DNL Data Landing Zone] conexión de origen utilizando la variable [[!DNL Flow Service] API](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) o [interfaz de usuario](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md). [!DNL Data Landing Zone] es un [!DNL Azure Blob] interfaz de almacenamiento de información aprovisionada por Platform, lo que le permite acceder a un servicio de almacenamiento de archivos seguro y basado en la nube para introducir archivos en Platform. Consulte la [[!DNL Data Landing Zone] información general](../../sources/connectors/cloud-storage/data-landing-zone.md) para obtener más información. |
| [!DNL Snowflake] | Ahora puede crear un [!DNL Snowflake] conexión de origen utilizando la variable [[!DNL Flow Service] API](../../sources/tutorials/api/create/databases/snowflake.md) o [interfaz de usuario](../../sources/tutorials/ui/create/databases/snowflake.md) para obtener datos de su [!DNL Snowflake] a Platform. Consulte la [[!DNL Snowflake] información general](../../sources/connectors/databases/snowflake.md) para obtener más información. |
| [!DNL SFTP] mejoras de la fuente | Puede definir manualmente un número de puerto personalizado al crear un [!DNL SFTP] conexión de origen. Consulte la [[!DNL SFTP] información general](../../sources/connectors/cloud-storage/sftp.md) para obtener más información. |

Para obtener más información sobre las fuentes, consulte la [información general sobre fuentes](../../sources/home.md).
