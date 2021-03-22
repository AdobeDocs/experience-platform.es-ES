---
keywords: Dirección IP, rango de IP, destinos de lista de permitidos
title: 'LISTA DE PERMITIDOS de direcciones IP para destinos de almacenamiento en la nube '
type: Documentación
description: Esta página proporciona rangos de IP que puede agregar a su lista de permitidos para exportar de forma segura los datos de Experience Platform a su servidor SFTP, Amazon S3 o al almacenamiento del blob de Azure.
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 1%

---


# LISTA DE PERMITIDOS de direcciones IP para destinos de almacenamiento en la nube {#ip-address-allow-list}

## Información general {#overview}

>[!IMPORTANT]
>
> Adobe recomienda marcar esta página y volver a visitarla cada tres meses para buscar las últimas direcciones IP. Adobe no proporciona notificaciones de nuevos rangos de IP.

Esta página proporciona rangos de IP que puede agregar a su lista de permitidos para exportar de forma segura los datos del Experience Platform a su [servidor SFTP](./sftp.md), [Amazon S3](./amazon-s3.md) o almacenamiento [Azure Blob](./azure-blob.md).

Puede definir los controles de acceso a la red a través del cortafuegos de la red. Si especifica el rango de IP adecuado, puede permitir el tráfico para el servicio de transferencia de datos.

Puede agregar los siguientes rangos de IP a una lista de permitidos antes de trabajar con conexiones de destino de almacenamiento en la nube. Si no se añade el rango IP específico de su región a la lista de permitidos, puede que se produzcan errores o que no se produzca un rendimiento al usar las conexiones de destino de almacenamiento en la nube.

## Clientes estadounidenses

* `52.252.71.64/29`

## Clientes de EMEA

* `51.137.8.208/29`

## Clientes de APAC

* `20.53.201.168/29`