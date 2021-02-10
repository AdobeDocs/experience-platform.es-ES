---
keywords: destino de almacenamiento de nube;almacenamiento de nube
title: Descripción general de los destinos de Almacenamiento de nube
description: Adobe Experience Platform puede entregar sus segmentos como archivos de datos a sus ubicaciones de Amazon S3, AWS Kinesis, Azure Evento Hubs o SFTP cloud almacenamiento.
translation-type: tm+mt
source-git-commit: 48c5f6d6a45de5f7982543f7a43cb4ece8cf3a9f
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---


# Visión general de los destinos de almacenamiento de nube {#cloud-storage-destinations}

Adobe Experience Platform puede entregar los segmentos como archivos de datos a las ubicaciones de los almacenamientos en la nube. Esto le permite enviar audiencias y sus atributos de perfil a sus sistemas internos, a través de archivos CSV o delimitados por tabuladores para [!DNL Amazon S3] y SFTP. Para los destinos [!DNL AWS Kinesis] y [!DNL Azure Event Hubs], los datos se transmiten fuera del Experience Platform en formato JSON.

![Destinos de almacenamiento de Adobe cloud](../../assets/catalog/cloud-storage/cloud-storage-destinations.png)

Para obtener información sobre cómo conectarse a destinos de almacenamiento en la nube, consulte [Flujo de trabajo para crear destinos de almacenamiento en la nube](./workflow.md).

## Tipo de exportación de datos

**Exportación**  basada en perfiles: se exportan detalles sobre las personas de la audiencia. Estos detalles son necesarios para la personalización y pueden incluir atributos, eventos, pertenencia a segmentos, etc.

## Destinos de almacenamiento en la nube disponibles

- [Conexión Amazon S3](./amazon-s3.md)
- [Conexión de blob de Azure](./azure-blob.md)
- [Conexión SFTP](./sftp.md)

## Destinos de flujo de almacenamiento en la nube disponibles

- [Conexión con Amazon Kinesis](./amazon-kinesis.md)
- [Conexión de los centros de Evento de Azure](./azure-event-hubs.md)