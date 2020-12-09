---
title: Notas de la versión de Adobe Experience Platform
description: Notas de la versión del Experience Platform 9 de diciembre de 2020
doc-type: release notes
last-update: December 9, 2020
author: ens60013
translation-type: tm+mt
source-git-commit: 25c162f50f0a66d77eb638dbf87893af3c543ddc
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 10%

---


# Notas de la versión de Adobe Experience Platform

**Fecha de versión: 9 de diciembre de 2020**

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [[!DNL Sources]](#sources)

## [!DNL Sources] {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas y, al mismo tiempo, puede estructurarlos, etiquetarlos y mejorarlos mediante [!DNL Platform] servicios. Puede ingestar datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

[!DNL Experience Platform] proporciona una API RESTful y una interfaz de usuario interactiva que le permite configurar fácilmente las conexiones de origen para varios proveedores de datos. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingestión y administrar el rendimiento de la ingesta de datos.

**Funciones principales**

| Función | Descripción |
| ------- | ----------- |
| Actualizar detalles de cuenta y conexión para orígenes de flujo continuo | Ahora puede actualizar los nombres, las descripciones y las credenciales de las conexiones de flujo existentes mediante la [!DNL Flow Service] API y la interfaz de usuario. Para obtener más información, consulte el tutorial sobre la [actualización de conexiones mediante la API](../../sources/tutorials/api/update.md) y la [edición de los detalles de la cuenta mediante la interfaz de usuario](../../sources/tutorials/ui/monitor.md). |
| Eliminar flujos de datos | Los flujos de datos de flujo continuo que contienen errores o que se han vuelto innecesarios ahora se pueden eliminar mediante la API y la interfaz de usuario [!DNL Flow Service] . Para obtener más información, consulte el tutorial sobre la [eliminación de flujos de datos mediante la API](../../sources/tutorials/api/delete-dataflows.md) y la [eliminación de flujos de datos mediante la interfaz de usuario](../../sources/tutorials/ui/delete.md). |

Para obtener más información sobre las fuentes, consulte la descripción general [de](../../sources/home.md)las fuentes.