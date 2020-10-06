---
keywords: Amazon S3;S3 destination;s3;amazon s3
title: Destino de Amazon S3
seo-title: Destino de Amazon S3
description: Cree una conexión directa de salida a su almacenamiento de Amazon Web Services (AWS) S3 para exportar periódicamente archivos de datos delimitados por tabuladores o CSV desde Adobe Experience Platform a sus propios cubos S3.
seo-description: Cree una conexión directa de salida a su almacenamiento de Amazon Web Services (AWS) S3 para exportar periódicamente archivos de datos delimitados por tabuladores o CSV desde Adobe Experience Platform a sus propios cubos S3.
translation-type: tm+mt
source-git-commit: 67a353c950bef11ccbaa52c49d213f08449baa96
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 0%

---


# [!DNL Amazon S3] destino

## Información general

Cree una conexión directa de salida a su almacenamiento [!DNL Amazon Web Services] (AWS) S3 para exportar periódicamente archivos de datos delimitados por tabuladores o CSV desde Adobe Experience Platform a sus propios bucket S3.

## Tipo de exportación {#export-type}

**Basado** en perfiles: está exportando todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos), tal como se elige en la pantalla de selección de atributos del flujo de trabajo [de activación de](/help/rtcdp/destinations/activate-destinations.md#select-attributes)destino.

![Tipo de exportación basado en perfil Amazon S3](/help/rtcdp/destinations/assets/aws-export-type.png)

## Destino de Connect {#connect-destination}

Consulte Flujo de trabajo de destinos de almacenamiento [Cloud ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)para obtener instrucciones sobre cómo conectarse a los destinos de almacenamiento de nube, incluidos [!DNL Amazon S3].

Para [!DNL Amazon S3] destinos, introduzca la siguiente información en el flujo de trabajo de creación de destinos:

* **[!DNL Amazon S3]clave de acceso y clave[!DNL Amazon S3]secreta**: En [!DNL Amazon S3], genere un `access key - secret access key` par para otorgar acceso CDP en tiempo real de Adobe a su [!DNL Amazon S3] cuenta. Obtenga más información en la documentación [de los servicios Web de](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)Amazon.

>[!IMPORTANT]
>
>Adobe Real-time CDP necesita `write` permisos en el objeto de bloque donde se entregarán los archivos de exportación.

## Datos exportados {#exported-data}

Para [!DNL Amazon S3] los destinos, Adobe Real-time CDP crea un archivo delimitado por tabuladores `.txt` o `.csv` en la ubicación de almacenamiento proporcionada. Para obtener más información sobre los archivos, consulte Destinos de [correo electrónico de Marketing y Destinos](/help/rtcdp/destinations/activate-destinations.md#esp-and-cloud-storage) de almacenamiento de Cloud en el tutorial de activación de segmentos.

<!--

Expect a new file to be created in your storage location every day. The file format is:

`amazon-s3_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

```
amazon-s3_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
amazon-s3_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
amazon-s3_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

The presence of these files in your storage location is confirmation of successful activation. To understand how the exported files are structured, you can [download a sample .csv file](/help/rtcdp/destinations/assets/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv). This sample file includes the profile attributes `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear`, and `personalEmail.address`.

-->
