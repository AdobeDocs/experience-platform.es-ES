---
keywords: SFTP;sftp
title: Conexión SFTP
description: Cree una conexión saliente en directo al servidor SFTP para exportar periódicamente archivos de datos delimitados de Adobe Experience Platform.
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: b4810dfef7b0d437744ca14a32bd4f5746e8d002
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 0%

---

# Conexión SFTP

## Información general {#overview}

Cree una conexión saliente en directo al servidor SFTP para exportar periódicamente archivos de datos delimitados de Adobe Experience Platform.

>[!IMPORTANT]
>
> Aunque el Adobe admite la exportación de datos a servidores SFTP, las ubicaciones de almacenamiento en la nube recomendadas para exportar los datos son [!DNL Amazon S3] y [!DNL Azure Blob].

## Tipo de exportación {#export-type}

**Basado en perfiles** - está exportando todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono, apellidos), tal y como se elige en la pantalla de atributos seleccionados del [flujo de trabajo de activación de destino](../../ui/activate-batch-profile-destinations.md).

![Tipo de exportación basado en perfiles SFTP](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Conectarse al destino {#connect}

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md).

### Parámetros de conexión {#parameters}

While [configuración](../../ui/connect-destination.md) Para este destino, debe proporcionar la siguiente información:

* **Host**: La dirección de la ubicación de almacenamiento SFTP
* **Nombre de usuario**: El nombre de usuario para iniciar sesión en su ubicación de almacenamiento SFTP
* **Contraseña**: La contraseña para iniciar sesión en su ubicación de almacenamiento SFTP
* **[!UICONTROL Nombre]**: introduzca un nombre que le ayudará a identificar este destino.
* **[!UICONTROL Descripción]**: introduzca una descripción de este destino.
* **[!UICONTROL Ruta de carpeta]**: introduzca la ruta a la carpeta de destino que alojará los archivos exportados.

Opcionalmente, puede adjuntar su clave pública con formato RSA para agregar cifrado a los archivos exportados. La clave pública debe escribirse como un [!DNL Base64] cadena codificada.

## Datos exportados {#exported-data}

Para [!DNL SFTP] destinos, Platform crea un `.csv` en la ubicación de almacenamiento proporcionada. Para obtener más información sobre los archivos, consulte [Activar datos de audiencia en destinos de exportación de perfiles en lote](../../ui/activate-batch-profile-destinations.md) en el tutorial de activación de segmentos.

## LISTA DE PERMITIDOS de direcciones IP

Consulte [LISTA DE PERMITIDOS de direcciones IP para destinos de almacenamiento en la nube](ip-address-allow-list.md) si necesita agregar direcciones IP de Adobe a una lista de permitidos.
