---
keywords: destino de almacenamiento en la nube;almacenamiento en la nube
title: Resumen de destinos de Cloud Storage
description: Adobe Experience Platform puede enviar sus segmentos como archivos de datos a sus ubicaciones de almacenamiento en la nube Amazon S3, AWS Kinesis, Azure Event Hubs o SFTP.
translation-type: tm+mt
source-git-commit: 4f636de9f0cac647793564ce37c6589d096b61f7
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---


# Resumen de destinos de almacenamiento en la nube {#cloud-storage-destinations}

Adobe Experience Platform puede entregar sus segmentos como archivos de datos a sus ubicaciones de almacenamiento en la nube. Esto le permite enviar audiencias y sus atributos de perfil a sus sistemas internos, a través de archivos CSV o delimitados por tabuladores para [!DNL Amazon S3], [!DNL Azure Blob] y SFTP. Para los destinos [!DNL Amazon Kinesis] y [!DNL Azure Event Hubs] , los datos se transmiten fuera del Experience Platform en formato JSON.

![Destinos de almacenamiento en la nube de Adobe](../../assets/catalog/cloud-storage/cloud-storage-destinations.png)

Para obtener información sobre cómo conectarse a destinos de almacenamiento en la nube, consulte [Flujo de trabajo para crear destinos de almacenamiento en la nube](./workflow.md).

## Tipo de exportación de datos

**Exportación basada en perfiles** : se exportan detalles sobre las personas de la audiencia. Estos detalles son necesarios para la personalización y pueden incluir atributos, eventos, suscripciones a segmentos, etc.

## Destinos de almacenamiento en la nube disponibles

- [Conexión Amazon S3](./amazon-s3.md)
- [Conexión de Azure Blob](./azure-blob.md)
- [Conexión SFTP](./sftp.md)

## Destinos de flujo de almacenamiento en la nube disponibles

- [Conexión de Amazon Kinesis](./amazon-kinesis.md)
- [Conexión de los centros de eventos de Azure](./azure-event-hubs.md)