---
keywords: Amazon S3;destino S3;s3;amazon s3
title: Conexión Amazon S3
description: Cree una conexión saliente en directo al almacenamiento de Amazon Web Services (AWS) S3 para exportar periódicamente archivos de datos CSV o delimitados por tabuladores de Adobe Experience Platform a sus propios bloques S3.
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '223'
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

>[!IMPORTANT]
>
>Platform necesita `write` permisos en el objeto de compartimento en el que se entregarán los archivos de exportación.

## Datos exportados {#exported-data}

Para destinos [!DNL Amazon S3], Platform crea un archivo `.txt` o `.csv` delimitado por tabuladores en la ubicación de almacenamiento proporcionada. Para obtener más información sobre los archivos, consulte [Destinos de marketing por correo electrónico y destinos de almacenamiento en la nube](../../ui/activate-destinations.md#esp-and-cloud-storage) en el tutorial de activación de segmentos.
