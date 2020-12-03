---
keywords: cloud storage destination;cloud storage
title: Destinos de almacenamiento de nube
seo-title: Destinos de almacenamiento de nube
description: CDP en tiempo real puede entregar sus segmentos como archivos de datos a sus ubicaciones de Amazon S3, AWS Kinesis, Azure Evento Hubs o SFTP cloud almacenamiento.
seo-description: CDP en tiempo real puede entregar sus segmentos como archivos de datos a sus ubicaciones de Amazon S3, AWS Kinesis, Azure Evento Hubs o SFTP cloud almacenamiento.
translation-type: tm+mt
source-git-commit: 0bb1622895b1e0f97fc47b5c61d456bc369746c8
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 0%

---


# Destinos de almacenamiento de nube {#cloud-storage-destinations}

CDP en tiempo real puede entregar sus segmentos como archivos de datos a sus ubicaciones de almacenamiento en la nube. Esto le permite enviar audiencias y sus atributos de perfil a sus sistemas internos, a través de archivos CSV o delimitados por tabuladores para [!DNL Amazon S3] y SFTP. Para [!DNL AWS Kinesis] y [!DNL Azure Event Hubs] los destinos, los datos se transmiten fuera del Experience Platform en formato JSON.

![Destinos de almacenamiento de Adobe Cloud](../../assets/catalog/cloud-storage/cloud-storage-destinations.png)

Para obtener información sobre cómo conectarse a destinos de almacenamiento en la nube, consulte [Flujo de trabajo para crear destinos](./workflow.md)de almacenamiento en la nube.

## Tipo de exportación de datos

**Exportación** basada en perfiles: se exportan detalles sobre las personas de la audiencia. Estos detalles son necesarios para la personalización y pueden incluir atributos, eventos, pertenencia a segmentos, etc.

## Destinos de almacenamiento de Cloud disponibles

- [Destino de Amazon S3](./amazon-s3.md)
- [Destino de SFTP](./sftp.md)

## Destinos de flujo de almacenamiento Cloud disponibles

- [Destino de Amazon Kinesis](./amazon-kinesis.md)
- [Destino de los centros de Evento de Azure](./azure-event-hubs.md)