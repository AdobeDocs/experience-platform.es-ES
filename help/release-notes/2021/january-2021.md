---
title: Notas de la versión de Adobe Experience Platform
description: Notas de la versión del Experience Platform 27 de enero de 2021
doc-type: release notes
last-update: January 27, 2021
author: ens60013
translation-type: tm+mt
source-git-commit: 2e3a6acbfaa7f733a9843068c00f31f0b7f535b6
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 7%

---


# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 27 de enero de 2021**

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el modelo de datos de experiencia (XDM).

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Funciones de expresión ordinarias | [!DNL Data Prep] Mapper ahora admite la coincidencia y extracción de parte del campo de entrada en función de expresiones regulares. |

Para obtener más información, consulte la [[!DNL Data Prep] información general](../../data-prep/home.md).

## Destinos {#destinations}

[!DNL Destinations] son integraciones prediseñadas con plataformas de destino que permiten la activación sin fisuras de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing en varios canales, campañas por correo electrónico, publicidad de destino y muchos otros casos de uso.

**Nuevos destinos**

| Destino | Descripción |
| ----------- | ----------- |
| [!DNL Azure Blob] | [!DNL Azure Blob] es la solución de almacenamiento de objetos de Microsoft para la nube. |

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Coincidencia de ID avanzada | Mejoras en las capacidades de la tasa de coincidencia de audiencias en [!DNL Facebook Custom Audiences] y [!DNL Google Customer Match], agregando compatibilidad para la coincidencia de identidades adicionales, como ID externos, números de teléfono e ID de dispositivos móviles. Consulte la siguiente documentación para obtener más información: <ul><li>[Destino de Facebook](../../destinations/catalog/social/facebook.md)</li><li>[Destino de Coincidencia de clientes de Google](../../destinations/catalog/advertising/google-customer-match.md)</li><li>[Activar perfiles y segmentos en un destino](../../destinations/ui/activate-destinations.md)</li></ul> |

Para obtener más información, visite la [descripción general de destinos](../../destinations/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform puede ingestar datos de fuentes externas y, al mismo tiempo, puede estructurarlos, etiquetarlos y mejorarlos mediante los servicios de plataforma. Puede ingestar datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API RESTful y una interfaz de usuario interactiva que le permite configurar fácilmente las conexiones de origen para varios proveedores de datos. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingestión y administrar el rendimiento de la ingesta de datos.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Mejoras en el conector de origen de Adobe Audience Manager | Ahora puede filtrar y seleccionar segmentos individuales de origen de Audience Manager a ingesta en plataforma, así como filtrar las características de origen. Consulte el tutorial sobre [creación de un conector de origen de Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) para obtener más información. |
| [!DNL Google BigQuery] mejoras en los conectores de origen | Ahora puede ingerir archivos de más de 10 GB en una ejecución de flujo mediante el conector de origen [!DNL BigQuery]. Consulte la [[!DNL BigQuery] información general del conector de origen](../../sources/connectors/databases/bigquery.md) para obtener más información. |
| Compatibilidad con tipos de datos complejos para almacenamientos en la nube | Ahora puede ingestar tipos de datos complejos, como matrices en archivos JSON, al utilizar un conector de origen de almacenamiento de nube. Consulte los tutoriales sobre la creación de un flujo de datos de almacenamiento en la nube [en la interfaz de usuario](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) o [mediante la [!DNL Flow Service] API](../../sources/tutorials/api/collect/cloud-storage.md) para obtener más información. |
| Compatibilidad con la autenticación basada en claves principales de servicio para [!DNL Microsoft Dynamics] origen | Ahora puede autenticarse en su cuenta [!DNL Dynamics] mediante una clave principal de servicio como alternativa a la autenticación basada en contraseña. Consulte la [[!DNL Dynamics] información general del conector de origen](../../sources/connectors/crm/ms-dynamics.md) para obtener más información. |
| Compatibilidad de la interfaz de usuario con separadores personalizados en orígenes de almacenamiento en la nube | Ahora puede establecer un delimitador de columna personalizado, como una coma (`,`), una ficha (`\t`) o una barra vertical (`|`), para recopilar archivos delimitados en la interfaz de usuario. Consulte el tutorial sobre [creación de un flujo de datos con un conector de origen de almacenamiento de nube](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) para obtener más información |

Para obtener más información sobre las fuentes, consulte la [información general de las fuentes](../../sources/home.md).
