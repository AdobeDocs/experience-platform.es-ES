---
title: Destino de Amazon S3
seo-title: Destino de Amazon S3
description: Cree una conexión directa de salida a su almacenamiento de Amazon Web Services (AWS) S3 para exportar periódicamente archivos de datos delimitados por tabuladores o CSV desde Adobe Experience Platform a sus propios cubos S3.
seo-description: Cree una conexión directa de salida a su almacenamiento de Amazon Web Services (AWS) S3 para exportar periódicamente archivos de datos delimitados por tabuladores o CSV desde Adobe Experience Platform a sus propios cubos S3.
translation-type: tm+mt
source-git-commit: f3c6c27b7ad07ada0df18aabe0e8503253b38342

---


# Destino de Amazon S3

## Información general

Cree una conexión directa de salida a su almacenamiento de Amazon Web Services (AWS) S3 para exportar periódicamente archivos de datos delimitados por tabuladores o CSV desde Adobe Experience Platform a sus propios cubos S3.

## Destino de Connect {#connect-destination}

Consulte Flujo de trabajo de destinos de almacenamiento de [Cloud ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)para obtener instrucciones sobre cómo conectarse a los destinos de almacenamiento en la nube, incluido Amazon S3.

Para los destinos de Amazon S3, introduzca la siguiente información en el flujo de trabajo de creación de destino:

* **Clave de acceso Amazon S3 y clave** secreta Amazon S3: En Amazon S3, genere una clave de acceso: par de claves de acceso secreto para otorgar acceso CDP en tiempo real de Adobe a su cuenta de Amazon S3.



>[!IMPORTANT]
>
>Adobe Real-time CDP necesita `write` permisos en el objeto bucket en el que se entregarán los archivos de exportación.
