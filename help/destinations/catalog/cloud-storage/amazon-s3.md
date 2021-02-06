---
keywords: Amazon S3;S3 destino;s3;amazon s3
title: Destino de conexión Amazon S3
description: Cree una conexión directa de salida a su almacenamiento de Amazon Web Services (AWS) S3 para exportar periódicamente archivos de datos delimitados por tabuladores o CSV desde Adobe Experience Platform a sus propios cubos S3.
translation-type: tm+mt
source-git-commit: 6655714d4b57d9c414cd40529bcee48c7bcd862d
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---


# [!DNL Amazon S3] connection

Cree una conexión directa de salida a su almacenamiento [!DNL Amazon Web Services] (AWS) S3 para exportar periódicamente archivos de datos delimitados por tabuladores o CSV desde Adobe Experience Platform a sus propios cubos S3.

## Tipo de exportación {#export-type}

**Basado**  en perfiles: está exportando todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos), tal como se elige en la pantalla de selección de atributos del flujo de trabajo [ de activación de ](../../ui/activate-destinations.md#select-attributes)destino.

![Tipo de exportación basado en perfil Amazon S3](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## Destino de Connect {#connect-destination}

Consulte [Flujo de trabajo de destinos de almacenamiento de nube ](./workflow.md) para obtener instrucciones sobre cómo conectarse a los destinos de almacenamiento de nube, incluso [!DNL Amazon S3].

Para destinos [!DNL Amazon S3], introduzca la siguiente información en el flujo de trabajo de creación de destino:

* **[!DNL Amazon S3]clave de acceso y clave  [!DNL Amazon S3] secreta**: En  [!DNL Amazon S3], genere un  `access key - secret access key` par para otorgar a la plataforma acceso a su  [!DNL Amazon S3] cuenta. Obtenga más información en la [documentación de servicios Web de Amazon](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

>[!IMPORTANT]
>
>La plataforma necesita `write` permisos en el objeto de bloque donde se entregarán los archivos de exportación.

## Datos exportados {#exported-data}

Para los destinos [!DNL Amazon S3], Platform crea un archivo `.txt` o `.csv` delimitado por tabuladores en la ubicación de almacenamiento proporcionada. Para obtener más información sobre los archivos, consulte [Destinos de Marketing por correo electrónico y destinos de almacenamiento de Cloud](../../ui/activate-destinations.md#esp-and-cloud-storage) en el tutorial de activación de segmentos.
