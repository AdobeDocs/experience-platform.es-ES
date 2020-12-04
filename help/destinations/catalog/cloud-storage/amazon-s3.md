---
keywords: Amazon S3;S3 destination;s3;amazon s3
title: Destino de Amazon S3
seo-title: Destino de Amazon S3
description: Cree una conexión directa de salida a su almacenamiento de Amazon Web Services (AWS) S3 para exportar periódicamente archivos de datos delimitados por tabuladores o CSV desde Adobe Experience Platform a sus propios cubos S3.
seo-description: Cree una conexión directa de salida a su almacenamiento de Amazon Web Services (AWS) S3 para exportar periódicamente archivos de datos delimitados por tabuladores o CSV desde Adobe Experience Platform a sus propios cubos S3.
translation-type: tm+mt
source-git-commit: f2fdc3b75d275698a4b1e4c8969b1b840429c919
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---


# [!DNL Amazon S3] destino

## Información general

Cree una conexión directa de salida a su almacenamiento [!DNL Amazon Web Services] (AWS) S3 para exportar periódicamente archivos de datos delimitados por tabuladores o CSV desde Adobe Experience Platform a sus propios bucket S3.

## Tipo de exportación {#export-type}

**Basado** en perfiles: está exportando todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos), tal como se elige en la pantalla de selección de atributos del flujo de trabajo [de activación de](../../ui/activate-destinations.md#select-attributes)destino.

![Tipo de exportación basado en perfil Amazon S3](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## Destino de Connect {#connect-destination}

Consulte Flujo de trabajo de destinos de almacenamiento de [Cloud ](./workflow.md) para obtener instrucciones sobre cómo conectarse a los destinos de almacenamiento de nube, incluidos [!DNL Amazon S3].

Para [!DNL Amazon S3] destinos, introduzca la siguiente información en el flujo de trabajo de creación de destinos:

* **[!DNL Amazon S3]clave de acceso y clave [!DNL Amazon S3] secreta**: En [!DNL Amazon S3], genere un `access key - secret access key` par para otorgar acceso CDP en tiempo real a su [!DNL Amazon S3] cuenta. Obtenga más información en la documentación [de los servicios Web de](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)Amazon.

>[!IMPORTANT]
>
>CDP en tiempo real necesita `write` permisos en el objeto de bloque donde se entregarán los archivos de exportación.

## Datos exportados {#exported-data}

Para [!DNL Amazon S3] los destinos, CDP en tiempo real crea un archivo delimitado por tabuladores `.txt` o `.csv` en la ubicación de almacenamiento proporcionada. Para obtener más información sobre los archivos, consulte Destinos de [correo electrónico de Marketing y Destinos](../../ui/activate-destinations.md#esp-and-cloud-storage) de almacenamiento de Cloud en el tutorial de activación de segmentos.
