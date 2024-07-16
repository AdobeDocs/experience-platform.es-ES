---
keywords: destino de almacenamiento en nube;almacenamiento en nube
title: Información general sobre destinos de Cloud Storage
description: Adobe Experience Platform puede enviar audiencias como archivos de datos a sus ubicaciones de Amazon S3, AWS Kinesis, Azure Event Hubs o almacenamiento en la nube SFTP.
exl-id: d29f0a6e-b323-4f78-bbd0-dee2f1e0fedb
source-git-commit: 8b8abea65ee0448594113ca77f75b84293646146
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 6%

---

# Información general sobre destinos de almacenamiento en nube {#cloud-storage-destinations}

## Información general {#overview}

Adobe Experience Platform puede enviar sus audiencias como archivos de datos a sus ubicaciones de almacenamiento en la nube. Esto le permite enviar audiencias y sus atributos de perfil a sus sistemas internos mediante archivos CSV para [!DNL Amazon S3], [!DNL Azure Blob], [!DNL Azure Data Lake Storage Gen2], [!DNL Data Landing Zone], [!DNL Google Cloud Storage] y SFTP. Para los destinos [!DNL Amazon Kinesis] y [!DNL Azure Event Hubs], los datos se transmiten fuera del Experience Platform en formato [!DNL JSON].

![destinos de almacenamiento en la nube de Adobe](../../assets/catalog/cloud-storage/cloud-storage-destinations.png)

## Destinos de almacenamiento en la nube compatibles {#supported-destinations}

Adobe Experience Platform admite exportaciones de datos a los siguientes destinos de almacenamiento en la nube:

* [Conexión de Amazon Kinesis](amazon-kinesis.md)
* [Conexión de Amazon S3](amazon-s3.md)
* [Conexión de Azure Blob](azure-blob.md)
* [Azure Data Lake Storage Gen2](adls-gen2.md)
* [Conexión de Azure Event Hubs](azure-event-hubs.md)
* [Zona de aterrizaje de datos](data-landing-zone.md)
* [Almacenamiento en la nube de Google](google-cloud-storage.md)
* [Conexión SFTP](sftp.md)

## Conectarse a un nuevo destino de almacenamiento en la nube {#connect-destination}

Para enviar audiencias a destinos de almacenamiento en la nube para sus campañas, Platform debe conectarse primero al destino. Consulte el [tutorial de creación de destinos](../../ui/connect-destination.md) para obtener información detallada sobre cómo configurar un nuevo destino.


## Utilice macros para crear una carpeta en su ubicación de almacenamiento {#use-macros}

>[!NOTE]
>
> La funcionalidad descrita en esta sección está disponible actualmente solo para destinos de [Amazon S3](amazon-s3.md).

Para crear una carpeta personalizada por archivo de audiencia en su ubicación de almacenamiento, puede utilizar macros en el campo de entrada de la ruta de la carpeta. Inserte las macros al final del campo de entrada, como se muestra a continuación.

![Cómo usar macros para crear una carpeta en su almacenamiento](../../assets/catalog/cloud-storage/workflow/macros-folder-path.png)

Los ejemplos siguientes hacen referencia a una audiencia de muestra `Luxury Audience` con el identificador `25768be6-ebd5-45cc-8913-12fb3f348615`.

**Macro 1:`%SEGMENT_NAME%`**

Entrada: `acme/campaigns/2021/%SEGMENT_NAME%`
Ruta de la carpeta en su ubicación de almacenamiento: `acme/campaigns/2021/Luxury Audience`

**Macro 2:`%SEGMENT_ID%`**

Entrada: `acme/campaigns/2021/%SEGMENT_ID%`
Ruta de la carpeta en su ubicación de almacenamiento: `acme/campaigns/2021/25768be6-ebd5-45cc-8913-12fb3f348615`

**Macro 3:`%SEGMENT_NAME%/%SEGMENT_ID%`**

Entrada: `acme/campaigns/2021/%SEGMENT_NAME%/%SEGMENT_ID%`
Ruta de la carpeta en su ubicación de almacenamiento: `acme/campaigns/2021/Luxury Audience/25768be6-ebd5-45cc-8913-12fb3f348615`

## Tipo de exportación de datos {#export-type}

Los destinos de almacenamiento en la nube admiten los siguientes tipos de exportación:
* **Exportación basada en perfiles**. Esto significa que está exportando detalles sobre las personas en la audiencia. Estos detalles son necesarios para la personalización y pueden incluir atributos, eventos, suscripciones a audiencias, etc.
* **Exportación de conjuntos de datos**. Esta funcionalidad le permite exportar conjuntos de datos completos a destinos de almacenamiento en la nube. [Más información](/help/destinations/ui/export-datasets.md) sobre la funcionalidad.

## Pasos siguientes {#next-steps}

Después de seleccionar cuál de los [destinos en la nube compatibles](#supported-destinations) desea usar, lea el tutorial de [conectar con destinos](/help/destinations/ui/connect-destination.md) para aprender a establecer una conexión con el destino. A continuación, lea el tutorial de activación a destinos basados en archivos para aprender a empezar a [exportar](/help/destinations/ui/activate-batch-profile-destinations.md) datos a su destino de almacenamiento en la nube.
