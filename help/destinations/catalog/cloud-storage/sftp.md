---
keywords: SFTP;sftp
title: Conexión SFTP
description: Cree una conexión saliente en directo al servidor SFTP para exportar periódicamente archivos de datos delimitados de Adobe Experience Platform.
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: b7392596c7ed96032dc8ad6bb8e423640f562394
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---

# Conexión SFTP

## Información general {#overview}

Cree una conexión saliente en directo al servidor SFTP para exportar periódicamente archivos de datos delimitados de Adobe Experience Platform.

>[!IMPORTANT]
>
> Aunque el Adobe admite las exportaciones de datos a servidores SFTP, las ubicaciones de almacenamiento en la nube recomendadas para exportar datos son [!DNL Amazon S3] y [!DNL Azure Blob].

## Tipo de exportación {#export-type}

**Basado en perfiles** : exporta todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono y apellidos), tal como se elige en la pantalla de selección de atributos del flujo de trabajo de activación de  [destino](../../ui/activate-batch-profile-destinations.md).

![Tipo de exportación basado en perfiles SFTP](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Conectarse al destino {#connect}

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

Mientras [configura](../../ui/connect-destination.md) este destino, debe proporcionar la siguiente información:

* **Host**: La dirección de la ubicación de almacenamiento SFTP
* **Nombre de usuario**: El nombre de usuario para iniciar sesión en su ubicación de almacenamiento SFTP
* **Contraseña**: La contraseña para iniciar sesión en su ubicación de almacenamiento SFTP
* **[!UICONTROL Nombre]**: introduzca un nombre que le ayudará a identificar este destino.
* **[!UICONTROL Descripción]**: introduzca una descripción de este destino.
* **[!UICONTROL Ruta de acceso]** de la carpeta: introduzca la ruta a la carpeta de destino que alojará los archivos exportados.

Opcionalmente, puede adjuntar su clave pública con formato RSA para agregar cifrado a los archivos exportados. La clave pública debe escribirse como una cadena codificada [!DNL Base64].

## Datos exportados {#exported-data}

Para destinos [!DNL SFTP], Platform crea un archivo `.csv` delimitado por tabuladores en la ubicación de almacenamiento proporcionada. Para obtener más información sobre los archivos, consulte [Activación de datos de audiencia en destinos de exportación de perfiles por lotes](../../ui/activate-batch-profile-destinations.md) en el tutorial de activación de segmentos.

## LISTA DE PERMITIDOS de direcciones IP

Consulte la [lista de permitidos de direcciones IP para destinos de almacenamiento en la nube](ip-address-allow-list.md) si necesita agregar IP de Adobe a una lista de permitidos.
