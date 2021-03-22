---
keywords: Dirección IP, rango de IP, destinos de lista de permitidos
title: 'LISTA DE PERMITIDOS de direcciones IP para destinos de almacenamiento en la nube '
type: Documentación
description: Esta página proporciona rangos de IP que puede agregar a su lista de permitidos para exportar de forma segura los datos de Experience Platform a su servidor SFTP, Amazon S3 o al almacenamiento del blob de Azure.
translation-type: tm+mt
source-git-commit: 7d7568de57cf79843a833a05b9bdfa6eb048bdbc
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 0%

---


# LISTA DE PERMITIDOS de direcciones IP para destinos de almacenamiento en la nube {#ip-address-allow-list}

## Información general {#overview}

>[!IMPORTANT]
>
> * Adobe recomienda marcar esta página y volver a visitarla cada tres meses para buscar las últimas direcciones IP. Adobe no proporciona notificaciones de nuevos rangos de IP.
> * Aunque el Adobe admite las exportaciones de datos a servidores SFTP, las ubicaciones de almacenamiento en la nube recomendadas para exportar datos son [!DNL Amazon S3] y [!DNL Azure Blob].


Esta página proporciona rangos de IP que puede agregar a su lista de permitidos para exportar de forma segura los datos del Experience Platform a su [servidor SFTP](./sftp.md), [Amazon S3](./amazon-s3.md) o almacenamiento [Azure Blob](./azure-blob.md).

Puede definir los controles de acceso a la red a través del cortafuegos de la red. Si especifica el rango de IP adecuado, puede permitir el tráfico para el servicio de transferencia de datos.

Adobe recomienda agregar los siguientes rangos de IP a una lista de permitidos antes de trabajar con conexiones de destino de almacenamiento en la nube. Si no se añade el rango IP específico de su región a la lista de permitidos, puede que se produzcan errores o que no se produzca un rendimiento al usar las conexiones de destino de almacenamiento en la nube.

## Necesario para todos los clientes

* `52.247.108.70`

## Clientes estadounidenses

* `52.252.71.64/29`

## Clientes de EMEA

* `51.137.8.208/29`

## Clientes de APAC

* `20.53.201.168/29`