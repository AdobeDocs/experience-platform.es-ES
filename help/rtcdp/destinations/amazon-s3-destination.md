---
title: Destino de Amazon S3
seo-title: Destino de Amazon S3
description: Cree una conexión directa de salida a su almacenamiento de Amazon Web Services (AWS) S3 para exportar periódicamente archivos de datos delimitados por tabuladores o CSV desde Adobe Experience Platform a sus propios cubos S3.
seo-description: Cree una conexión directa de salida a su almacenamiento de Amazon Web Services (AWS) S3 para exportar periódicamente archivos de datos delimitados por tabuladores o CSV desde Adobe Experience Platform a sus propios cubos S3.
translation-type: tm+mt
source-git-commit: b96286f6a06f0583b45343a513ee64f0025d79a7
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---


# [!DNL Amazon S3] destino

## Información general

Cree una conexión directa de salida a su almacenamiento [!DNL Amazon Web Services] (AWS) S3 para exportar periódicamente archivos de datos delimitados por tabuladores o CSV desde Adobe Experience Platform a sus propios bucket S3.

## Destino de Connect {#connect-destination}

Consulte Flujo de trabajo de destinos de almacenamiento [Cloud ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)para obtener instrucciones sobre cómo conectarse a los destinos de almacenamiento de nube, incluidos [!DNL Amazon S3].

Para [!DNL Amazon S3] destinos, introduzca la siguiente información en el flujo de trabajo de creación de destinos:

* **[!DNL Amazon S3]clave de acceso y clave[!DNL Amazon S3]secreta **: En[!DNL Amazon S3], genere una clave de acceso: par de claves de acceso secreto para otorgar acceso CDP en tiempo real de Adobe a su[!DNL Amazon S3]cuenta.



>[!IMPORTANT]
>
>Adobe Real-time CDP necesita `write` permisos en el objeto bucket en el que se entregarán los archivos de exportación.
