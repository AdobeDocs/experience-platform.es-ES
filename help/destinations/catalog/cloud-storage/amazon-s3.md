---
keywords: Amazon S3;destino S3;s3;amazon s3
title: Conexión Amazon S3
description: Cree una conexión saliente en directo al almacenamiento de Amazon Web Services (AWS) S3 para exportar periódicamente archivos de datos CSV o delimitados por tabuladores de Adobe Experience Platform a sus propios bloques S3.
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
source-git-commit: 70be44e919070df910d618af4507b600ad51123c
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# [!DNL Amazon S3] connection  {#s3-connection}

## Información general {#overview}

Cree una conexión saliente en directo a su almacenamiento [!DNL Amazon Web Services] (AWS) S3 para exportar periódicamente archivos de datos CSV o delimitados por tabuladores desde Adobe Experience Platform a sus propios bloques S3.

## Tipo de exportación {#export-type}

**Basado en perfiles** : exporta todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono y apellidos), tal como se elige en la pantalla de selección de atributos del flujo de trabajo de activación de  [destino](../../ui/activate-destinations.md#select-attributes).

![Tipo de exportación basado en perfiles de Amazon S3](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## Conectar destino {#connect-destination}

Consulte [Flujo de trabajo de destinos de almacenamiento en la nube ](./workflow.md) para obtener instrucciones sobre cómo conectarse a los destinos de almacenamiento en la nube, incluido [!DNL Amazon S3].

Para destinos [!DNL Amazon S3] , introduzca la siguiente información en el flujo de trabajo de creación de destino:

* **[!DNL Amazon S3]clave de acceso y clave  [!DNL Amazon S3] secreta**: En  [!DNL Amazon S3], genere un  `access key - secret access key` par para conceder a Platform acceso a su  [!DNL Amazon S3] cuenta. Obtenga más información en la [documentación de los servicios web de Amazon](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

>[!TIP]
>
>En el flujo de trabajo de conexión de destino, puede crear una carpeta personalizada en el almacenamiento de Amazon S3 por archivo de segmento exportado. Lea [Use macros para crear una carpeta en su ubicación de almacenamiento](./workflow.md#use-macros) para obtener instrucciones.

## Permisos [!DNL Amazon S3] requeridos {#required-s3-permission}

Para conectar y exportar datos correctamente a su ubicación de almacenamiento [!DNL Amazon S3], cree un usuario de Administración de identidad y acceso (IAM) para [!DNL Platform] en [!DNL Amazon S3] y asigne permisos para las siguientes acciones:

* `s3:DeleteObject`
* `s3:GetBucketLocation`
* `s3:GetObject`
* `s3:ListBucket`
* `s3:PutObject`
* `s3:ListMultipartUploadParts`


<!--

Commenting out this note, as write permissions are assigned through the s3:PutObject permission.

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->


## Datos exportados {#exported-data}

Para destinos [!DNL Amazon S3], [!DNL Platform] crea un archivo `.csv` delimitado por tabuladores en la ubicación de almacenamiento proporcionada. Para obtener más información sobre los archivos, consulte [Destinos de marketing por correo electrónico y destinos de almacenamiento en la nube](../../ui/activate-destinations.md#esp-and-cloud-storage) en el tutorial de activación de segmentos.
