---
keywords: SFTP;sftp
title: Conexión SFTP
description: Cree una conexión saliente en directo al servidor SFTP para exportar periódicamente archivos de datos delimitados de Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 4f0047e7ac4c83e3e17ea0a077bbeb09c86d1db6
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---


# Conexión SFTP

Cree una conexión saliente en directo al servidor SFTP para exportar periódicamente archivos de datos delimitados de Adobe Experience Platform.

>[!IMPORTANT]
>
> Aunque el Adobe admite las exportaciones de datos a servidores SFTP, las ubicaciones de almacenamiento en la nube recomendadas para exportar datos son [!DNL Amazon S3] y [!DNL Azure Blob].

## Tipo de exportación {#export-type}

**Basado en perfiles** : exporta todos los miembros de un segmento, junto con los campos de esquema deseados (por ejemplo: dirección de correo electrónico, número de teléfono y apellidos), tal como se elige en la pantalla de selección de atributos del flujo de trabajo de activación de  [destino](../../ui/activate-destinations.md#select-attributes).

![Tipo de exportación basado en perfiles SFTP](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Conectar destino {#connect-destination}

Consulte el [Flujo de trabajo de destinos de almacenamiento en la nube ](./workflow.md) para obtener instrucciones sobre cómo conectarse a los destinos de almacenamiento en la nube, incluido SFTP.

Para los destinos SFTP, introduzca la siguiente información en el flujo de trabajo de creación de destino, en el paso **Autenticación**:

* **Host**: La dirección de la ubicación de almacenamiento SFTP
* **Nombre de usuario**: El nombre de usuario para iniciar sesión en su ubicación de almacenamiento SFTP
* **Contraseña**: La contraseña para iniciar sesión en su ubicación de almacenamiento SFTP

## Datos exportados {#exported-data}

Para los destinos SFTP, Platform crea un archivo `.txt` o `.csv` delimitado por tabuladores en la ubicación de almacenamiento proporcionada. Para obtener más información sobre los archivos, consulte [Destinos de marketing por correo electrónico y destinos de almacenamiento en la nube](../../ui/activate-destinations.md#esp-and-cloud-storage) en el tutorial de activación de segmentos.

## LISTA DE PERMITIDOS de direcciones IP

Consulte la [lista de permitidos de direcciones IP para destinos de almacenamiento en la nube](./ip-address-allow-list.md) si necesita agregar IP de Adobe a una lista de permitidos.