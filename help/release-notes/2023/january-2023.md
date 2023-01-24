---
title: Notas de la versión de Adobe Experience Platform, enero de 2023
description: Notas de la versión de enero de 2023 para Adobe Experience Platform.
source-git-commit: 01c220147312108649e036d93288823df5389235
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 9%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 25 de enero de 2023**

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [Fuentes](#sources)

## Fuentes {#sources}

Adobe Experience Platform puede introducir datos de fuentes externas y le permite estructurarlos, etiquetarlos y mejorarlos mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API de RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecutar la ingesta y administrar el rendimiento de ingesta de datos.

| Función | Descripción |
| --- | --- |
| Permitir el acceso del usuario a subcarpetas de orígenes de almacenamiento en la nube | Ahora puede definir el acceso a una subcarpeta específica del origen de almacenamiento en la nube al crear una cuenta nueva. Una vez creados, los usuarios solo podrán acceder a los datos de la subcarpeta permitida. Esta función está disponible para las siguientes fuentes de almacenamiento en la nube: [Almacenamiento de Azure Blob](../../sources/connectors/cloud-storage/blob.md), [Almacenamiento en la nube de Google](../../sources/connectors/cloud-storage/google-cloud-storage.md), [Google PubSub](../../sources/connectors/cloud-storage/google-pubsub.md)y [SFTP](../../sources/connectors/cloud-storage/sftp.md). |
| Disponibilidad beta de [!DNL SugarCRM] | [!DNL SugarCRM] los orígenes de ya están disponibles en la versión beta. Utilice la variable [!DNL SugarCRM Accounts & Contacts] y [!DNL SugarCRM Events] fuentes para obtener datos de [!DNL SugarCRM] cuenta al Experience Platform. Para obtener más información, lea la [[!DNL SugarCRM] información general](../../sources/connectors/crm/sugarcrm.md). |