---
keywords: destino de almacenamiento en la nube;almacenamiento en la nube
title: Resumen de destinos de Cloud Storage
description: Adobe Experience Platform puede enviar sus segmentos como archivos de datos a sus ubicaciones de almacenamiento en la nube Amazon S3, AWS Kinesis, Azure Event Hubs o SFTP.
exl-id: d29f0a6e-b323-4f78-bbd0-dee2f1e0fedb
source-git-commit: 4a4c82cc4528fe07bbdb75ae9f795bdbab48c089
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Información general sobre los destinos de almacenamiento en la nube {#cloud-storage-destinations}

## Información general {#overview}

Adobe Experience Platform puede entregar sus segmentos como archivos de datos a sus ubicaciones de almacenamiento en la nube. Esto le permite enviar audiencias y sus atributos de perfil a sus sistemas internos, a través de archivos CSV para [!DNL Amazon S3], [!DNL Azure Blob], [!DNL Azure Data Lake Storage Gen2], [!DNL Data Landing Zone], [!DNL Google Cloud Storage]y SFTP. Para [!DNL Amazon Kinesis] y [!DNL Azure Event Hubs] destinos, los datos se transmiten fuera del Experience Platform [!DNL JSON] formato.

![Destinos de almacenamiento en la nube de Adobe](../../assets/catalog/cloud-storage/cloud-storage-destinations.png)

## Destinos de almacenamiento en la nube admitidos {#supported-destinations}

Adobe Experience Platform admite los siguientes destinos de almacenamiento en la nube:

* [Conexión de Amazon Kinesis](amazon-kinesis.md)
* [Conexión Amazon S3](amazon-s3.md)
* [Conexión de Azure Blob](azure-blob.md)
* [(Beta) Almacenamiento de Azure Data Lake Gen2](adls-gen2.md)
* [Conexión de los centros de eventos de Azure](azure-event-hubs.md)
* [(Beta) Zona de aterrizaje de datos](data-landing-zone.md)
* [(Beta) Almacenamiento en la nube de Google](google-cloud-storage.md)
* [Conexión SFTP](sftp.md)

## Conectarse a un nuevo destino de almacenamiento en la nube {#connect-destination}

Para enviar segmentos a destinos de almacenamiento en la nube para sus campañas, Platform debe conectarse primero al destino. Consulte la [tutorial de creación de destino](../../ui/connect-destination.md) para obtener información detallada sobre la configuración de un nuevo destino.


## Utilice macros para crear una carpeta en su ubicación de almacenamiento {#use-macros}

>[!NOTE]
>
> La funcionalidad descrita en esta sección está disponible actualmente para [Amazon S3](amazon-s3.md) solo destinos.

Para crear una carpeta personalizada por archivo de segmento en su ubicación de almacenamiento, puede utilizar macros en el campo de entrada de ruta de carpeta. Inserte las macros al final del campo de entrada, como se muestra a continuación.

![Cómo usar macros para crear una carpeta en el almacenamiento](../../assets/catalog/cloud-storage/workflow/macros-folder-path.png)

Los ejemplos siguientes hacen referencia a un segmento de muestra `Luxury Audience` con ID `25768be6-ebd5-45cc-8913-12fb3f348615`.

**Macro 1:`%SEGMENT_NAME%`**

Entrada: `acme/campaigns/2021/%SEGMENT_NAME%`
Ruta de carpeta en su ubicación de almacenamiento: `acme/campaigns/2021/Luxury Audience`

**Macro 2:`%SEGMENT_ID%`**

Entrada: `acme/campaigns/2021/%SEGMENT_ID%`
Ruta de carpeta en su ubicación de almacenamiento: `acme/campaigns/2021/25768be6-ebd5-45cc-8913-12fb3f348615`

**Macro 3:`%SEGMENT_NAME%/%SEGMENT_ID%`**

Entrada: `acme/campaigns/2021/%SEGMENT_NAME%/%SEGMENT_ID%`
Ruta de carpeta en su ubicación de almacenamiento: `acme/campaigns/2021/Luxury Audience/25768be6-ebd5-45cc-8913-12fb3f348615`

## Tipo de exportación de datos {#export-type}

Compatibilidad con destinos de almacenamiento en la nube **Exportación basada en perfiles**. Esto significa que está exportando detalles sobre las personas en la audiencia. Estos detalles son necesarios para la personalización y pueden incluir atributos, eventos, suscripciones a segmentos, etc.