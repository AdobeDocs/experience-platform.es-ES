---
keywords: SFTP;sftp
title: Destino de SFTP
seo-title: Destino de SFTP
description: Cree una conexión directa de salida al servidor SFTP para exportar periódicamente archivos de datos delimitados desde Experience Platform.
seo-description: Cree una conexión directa de salida al servidor SFTP para exportar periódicamente archivos de datos delimitados desde Experience Platform.
translation-type: tm+mt
source-git-commit: cbd748c1881c61f5e636567d94b68f2cf7302fa5
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---


# Destino de SFTP

## Información general

Cree una conexión directa de salida al servidor SFTP para exportar periódicamente archivos de datos delimitados desde Experience Platform.

Para exportar datos, complete los siguientes pasos:

## Destino de Connect {#connect-destination}

Consulte Flujo de trabajo de destinos de almacenamiento de [Cloud ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)para obtener instrucciones sobre cómo conectarse a los destinos de almacenamiento de nube, incluido SFTP.

Para los destinos SFTP, introduzca la siguiente información en el flujo de trabajo de creación de destino, en el paso **Autenticación** :

* **Host**: la dirección de la ubicación del almacenamiento SFTP
* **Nombre de usuario**: el nombre de usuario para iniciar sesión en la ubicación del almacenamiento SFTP
* **Contraseña**: la contraseña para iniciar sesión en la ubicación del almacenamiento SFTP

## Datos exportados {#exported-data}

Para los destinos SFTP, Adobe Real-time CDP crea un archivo `.txt` `.csv` o un archivo delimitado por tabuladores en la ubicación de almacenamiento proporcionada. Para obtener más información sobre los archivos, consulte Destinos de [correo electrónico de Marketing y Destinos](/help/rtcdp/destinations/activate-destinations.md#esp-and-cloud-storage) de almacenamiento de Cloud en el tutorial de activación de segmentos.