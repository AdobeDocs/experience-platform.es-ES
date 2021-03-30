---
title: Notas de la versión de Adobe Experience Platform
description: Notas de la versión del Experience Platform para el 31 de marzo de 2021.
doc-type: release notes
last-update: March 31, 2021
author: ens72741
translation-type: tm+mt
source-git-commit: 8d4270d9168a570fcf92ba60d70dbc8e9af98136
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 9%

---


# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 31 de marzo de 2021**

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [[!DNL Sources]](#sources)

## [!DNL Sources] {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas, al mismo tiempo que le permite estructurarlos, etiquetarlos y mejorarlos mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API de RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecutar la ingesta y administrar el rendimiento de ingesta de datos.

Las siguientes actualizaciones de las fuentes se incluyen en la versión de Experience Platform de marzo de 2021:

| Función | Descripción |
| ------- | ----------- |
| Fuentes beta que se trasladan a GA | Se han promocionado las siguientes fuentes de beta a GA: <ul><li>[[!DNL MySQL]](../../sources/connectors/databases/mysql.md)</li><li>[[!DNL PostGres]](../../sources/connectors/databases/postgres.md)</li><li>[[!DNL Salesforce Service Cloud]](../../sources/connectors/customer-success/salesforce-service-cloud.md)</li><li>[[!DNL SFTP]](../../sources/connectors/cloud-storage/sftp.md)</li><li>[[!DNL Shopify]](../../sources/connectors/ecommerce/shopify.md)</li></ul> |
| Compatibilidad de API para la ingesta de archivos comprimidos | Ahora puede obtener una vista previa e introducir archivos JSON comprimidos o delimitados mediante fuentes de almacenamiento en la nube. Para obtener más información, consulte el tutorial sobre [recopilación de datos de almacenamiento en la nube mediante API](../../sources/tutorials/api/collect/cloud-storage.md). |
| Compatibilidad de la interfaz de usuario con la carga de archivos recursivos | Ahora puede ingerir carpetas enteras recursivamente al usar un origen de almacenamiento en la nube. Al ingerir una carpeta completa, debe asegurarse de que su contenido comparte el mismo esquema. Para obtener más información, consulte el tutorial sobre [configuración de un flujo de datos para conectores de almacenamiento en la nube en la interfaz de usuario](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md). |

Para obtener más información sobre las fuentes, consulte [sources overview](../../sources/home.md).
