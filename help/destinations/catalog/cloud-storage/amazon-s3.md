---
keywords: Amazon S3;destino S3;s3;amazon s3
title: Conexión Amazon S3
description: Cree una conexión saliente en directo al almacenamiento de Amazon Web Service (AWS) S3 para exportar periódicamente archivos de datos CSV de Adobe Experience Platform a sus propios bloques S3.
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
source-git-commit: e6dc0fb136a6f5199153630a20e8809c2c040107
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 0%

---

# [!DNL Amazon S3] connection {#s3-connection}

## Información general {#overview}

Cree una conexión de salida activa con su [!DNL Amazon Web Services] (AWS) Almacenamiento S3 para exportar periódicamente archivos de datos CSV de Adobe Experience Platform a sus propios bloques S3.

## Tipo de exportación {#export-type}

**Basado en perfiles** - está exportando todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos), tal y como se elige en la pantalla de atributos seleccionados del [flujo de trabajo de activación de destino](../../ui/activate-segment-streaming-destinations.md#mapping).

![Tipo de exportación basado en perfiles de Amazon S3](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## Conectarse al destino {#connect}

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_bucket"
>title="Nombre del depósito"
>abstract="Debe tener entre 3 y 63 caracteres de longitud. Debe comenzar y terminar con una letra o un número. Solo debe contener letras minúsculas, números o guiones ( - ). No se debe dar formato a una dirección IP (por ejemplo, 192.100.1.1)."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_folderpath"
>title="Ruta de carpeta"
>abstract="Debe contener únicamente los caracteres A-Z, a-z, 0-9 y puede incluir los siguientes caracteres especiales: `/!-_.'()"^[]+$%.*"`. Para crear una carpeta por archivo de segmento, inserte la macro /%SEGMENT_NAME% o /%SEGMENT_ID% o /%SEGMENT_NAME%/%SEGMENT_ID% en el campo de texto. Las macros solo se pueden insertar al final de la ruta de la carpeta. Vea ejemplos de macros en la documentación."
>text="Learn more in documentation"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/cloud-storage/overview.html?lang=en#use-macros" text="Utilice macros para crear una carpeta en su ubicación de almacenamiento"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_rsa"
>title="Clave pública RSA"
>abstract="Opcionalmente, puede adjuntar su clave pública con formato RSA para agregar cifrado a los archivos exportados. La clave pública debe escribirse como una cadena codificada Base64."
>text="Learn more in documentation"

While [configuración](../../ui/connect-destination.md) Para este destino, debe proporcionar la siguiente información:

* **[!DNL Amazon S3]clave de acceso** y **[!DNL Amazon S3]clave secreta**: En [!DNL Amazon S3], genere un `access key - secret access key` par para conceder acceso a Platform a su [!DNL Amazon S3] cuenta. Obtenga más información en la [Documentación de Amazon Web Service](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **[!UICONTROL Nombre]**: introduzca un nombre que le ayudará a identificar este destino.
* **[!UICONTROL Descripción]**: introduzca una descripción de este destino.
* **[!UICONTROL Nombre del depósito]**: introduzca el nombre del [!DNL Amazon S3] contenedor que utilizará este destino.
* **[!UICONTROL Ruta de carpeta]**: introduzca la ruta a la carpeta de destino que alojará los archivos exportados.

Opcionalmente, puede adjuntar su clave pública con formato RSA para agregar cifrado a los archivos exportados. La clave pública debe escribirse como un [!DNL Base64] cadena codificada.

>[!TIP]
>
>En el flujo de trabajo de conexión de destino, puede crear una carpeta personalizada en el almacenamiento de Amazon S3 por archivo de segmento exportado. Lectura [Utilice macros para crear una carpeta en su ubicación de almacenamiento](overview.md#use-macros) para obtener instrucciones.

### Requerido [!DNL Amazon S3] permissions {#required-s3-permission}

Para conectar y exportar datos correctamente a su [!DNL Amazon S3] ubicación de almacenamiento, cree un usuario de Identity and Access Management (IAM) para [!DNL Platform] en [!DNL Amazon S3] y asigne permisos para las siguientes acciones:

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

## Activar segmentos en este destino {#activate}

Consulte [Activar datos de audiencia en destinos de exportación de perfiles en lote](../../ui/activate-batch-profile-destinations.md) para obtener instrucciones sobre la activación de segmentos de audiencia en este destino.

## Datos exportados {#exported-data}

Para [!DNL Amazon S3] destinos, [!DNL Platform] crea un `.csv` en la ubicación de almacenamiento proporcionada. Para obtener más información sobre los archivos, consulte [Activar datos de audiencia en destinos de exportación de perfiles en lote](../../ui/activate-batch-profile-destinations.md) en el tutorial de activación de segmentos.
