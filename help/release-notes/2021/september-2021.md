---
title: Notas de la versión de Adobe Experience Platform de septiembre de 2021
description: Las notas de la versión de septiembre de 2021 de Adobe Experience Platform.
exl-id: 96375409-803f-45af-805e-900207d972e4
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 26%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de lanzamiento: jueves, 29 de septiembre de 2021**

Actualizaciones de las funciones existentes en Adobe Experience Platform:

- [Ingesta de datos](#ingestion)
- [[!DNL Data Prep]](#data-prep)
- [Fuentes](#sources)

## Ingesta de datos {#ingestion}

La ingesta de datos de Adobe Experience Platform representa los múltiples métodos mediante los cuales Platform ingiere datos de varias fuentes, así como la forma en que se mantienen los datos dentro del lago de datos para que los utilicen los servicios de Platform secundarios.

**Nuevas funciones**

| Función | Descripción |
|------- | -----------|
| Actualización o aplicación de parches a registros de perfil mediante la ingesta por lotes | El Perfil del cliente en tiempo real ahora permite actualizar los atributos de perfil en los datos de registro de perfil individuales mediante la ingesta por lotes. Para obtener más información, consulte la [guía para desarrolladores de ingesta por lotes](../../ingestion/batch-ingestion/api-overview.md). |

Para obtener más información acerca de la ingesta de datos en Platform, visite la [documentación de ingesta de datos](../../ingestion/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el modelo de datos de experiencia (XDM).

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Compatibilidad con flujos de datos de streaming | Ahora puede usar las funciones de preparación de datos al crear un flujo de datos de flujo continuo para [!DNL Amazon Kinesis], [!DNL Azure Event Hubs] y [!DNL Google PubSub]. Consulte el tutorial sobre [creación de un flujo de datos de flujo continuo para fuentes de almacenamiento en la nube](../../sources/tutorials/ui/dataflow/streaming/cloud-storage-streaming.md) para obtener más información. |

Para obtener más información acerca de [!DNL Data Prep], consulte la [[!DNL Data Prep] descripción general](../../data-prep/home.md).

## Fuentes {#sources}

Adobe Experience Platform puede introducir datos de fuentes externas, al tiempo que le permite estructurar, etiquetar y mejorar esos datos mediante los servicios de Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

| Función | Descripción |
| --- | --- |
| [!DNL Data Landing Zone] | Ahora puede crear una conexión de origen [!DNL Data Landing Zone] mediante la [[!DNL Flow Service] API](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) o la [interfaz de usuario](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md). [!DNL Data Landing Zone] es una interfaz de almacenamiento de [!DNL Azure Blob] aprovisionada por Platform, que le permite acceder a una función de almacenamiento de archivos segura y basada en la nube para traer archivos a Platform. Consulte la [[!DNL Data Landing Zone] descripción general](../../sources/connectors/cloud-storage/data-landing-zone.md) para obtener más información. |
| [!DNL Snowflake] | Ahora puede crear una conexión de origen de [!DNL Snowflake] mediante la [[!DNL Flow Service] API](../../sources/tutorials/api/create/databases/snowflake.md) o la [interfaz de usuario](../../sources/tutorials/ui/create/databases/snowflake.md) para llevar datos de su base de datos de [!DNL Snowflake] a Platform. Consulte la [[!DNL Snowflake] descripción general](../../sources/connectors/databases/snowflake.md) para obtener más información. |
| [!DNL SFTP] mejoras de origen | Puede establecer manualmente un número de puerto personalizado al crear una conexión de origen de [!DNL SFTP]. Consulte la [[!DNL SFTP] descripción general](../../sources/connectors/cloud-storage/sftp.md) para obtener más información. |

Para obtener más información sobre las fuentes, consulte [descripción general de las fuentes](../../sources/home.md).
