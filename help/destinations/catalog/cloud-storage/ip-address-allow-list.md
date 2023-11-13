---
title: Destinos SFTP de lista de permitidos de direcciones IP
type: Documentation
description: Esta página proporciona rangos de IP que puede agregar a la lista de permitidos para exportar con seguridad datos de Experience Platform a su servidor SFTP.
exl-id: 0b8086aa-786e-4244-b2a5-a3f57ad59a8b
source-git-commit: 3d870975593313062d796601f0e19a0a3aec7854
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---

# LISTA DE PERMITIDOS de direcciones IP para destinos SFTP {#ip-address-allow-list-sftp}

>[!IMPORTANT]
>
> * El Adobe recomienda marcar esta página y volver a visitarla cada tres meses para comprobar las direcciones IP más recientes. El Adobe no notifica nuevos intervalos de IP.
> * Aunque el Adobe admite la exportación de datos a servidores SFTP, las ubicaciones de almacenamiento en la nube recomendadas para exportar datos son [!DNL Amazon S3] y [!DNL Azure Blob].

## Información general {#overview}

Esta página proporciona rangos de IP que puede agregar a la lista de permitidos para exportar con seguridad datos de Experience Platform a su [Servidor SFTP](./sftp.md).

Puede definir controles de acceso a la red a través del cortafuegos de la red. Si especifica el rango de IP adecuado, puede permitir el tráfico para el servicio de transferencia de datos.

El Adobe recomienda agregar los siguientes rangos de IP a una lista de permitidos antes de trabajar con conexiones de destino de almacenamiento en la nube. Si no agrega el intervalo de IP específico de su región a la lista de permitidos, pueden producirse errores o no rendimiento al utilizar las conexiones de destino de almacenamiento en la nube.

## Necesario para todos los clientes

* `52.247.108.70`

## clientes estadounidenses

* `52.252.71.64/29`

## Clientes de EMEA

* `51.137.8.208/29`

## Clientes de APAC

* `20.53.201.168/29`
