---
title: LISTA DE PERMITIDOS de direcciones IP para destinos de almacenamiento en la nube basados en archivos
type: Documentation
description: Esta página proporciona rangos de IP que puede agregar a su lista de permitidos para exportar con seguridad datos de Experience Platform a destinos de almacenamiento en la nube.
exl-id: 0b8086aa-786e-4244-b2a5-a3f57ad59a8b
source-git-commit: 4ae7ff58d02b46f1b213bd382d3e98b3f63819e8
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 1%

---

# LISTA DE PERMITIDOS de direcciones IP para destinos de almacenamiento en la nube basados en archivos {#ip-address-allow-list-cloud-storage}

>[!IMPORTANT]
>
> * Adobe recomienda marcar esta página y volver a visitarla cada tres meses para comprobar las direcciones IP más recientes. Adobe no notifica nuevos intervalos de IP.
> * Aunque Adobe admite la exportación de datos a servidores SFTP, las ubicaciones de almacenamiento en la nube recomendadas para exportar datos son [!DNL Amazon S3] y [!DNL Azure Blob].

## Aplicabilidad {#applicability}

La información del rango de IP de esta página se aplica a los siguientes conectores de almacenamiento en la nube basados en archivos en el catálogo de destinos:

* [[!UICONTROL Amazon S3]](./amazon-s3.md)
* [[!UICONTROL Almacenamiento en la nube de Google]](google-cloud-storage.md)
* [SFTP](./sftp.md)

>[!IMPORTANT]
>
>Los rangos de IP documentados en esta página son *no* compatibles con los siguientes destinos de almacenamiento en la nube basado en archivos: [!UICONTROL Azure Blob], [!UICONTROL Azure Data Lake Storage Gen2], [!UICONTROL Data Landing Zone] y servidores SFTP alojados en Microsoft Azure.

## Información general {#overview}

Esta página proporciona rangos de IP que puede agregar a su lista de permitidos para exportar con seguridad datos de Experience Platform a varios destinos de almacenamiento en la nube.

Puede definir controles de acceso a la red a través del cortafuegos de la red. Si especifica el rango de IP adecuado, puede permitir el tráfico para el servicio de transferencia de datos.

Adobe recomienda agregar los siguientes rangos de IP a una lista de permitidos antes de trabajar con conexiones de destino de almacenamiento en la nube. Si no agrega el intervalo de IP específico de su región a la lista de permitidos, pueden producirse errores o no rendimiento al utilizar las conexiones de destino de almacenamiento en la nube.

## Necesario para todos los clientes {#all-customers}

* `52.247.108.70`

## Clientes de EE. UU. que ejecutan AWS {#aws}

El rango de IP siguiente se aplica a los clientes de Experience Platform que se ejecutan en Amazon Web Service (AWS). Consulte la [descripción general de Experience Platform Multi-Cloud](../../../landing/multi-cloud.md) para obtener más información.

>[!NOTE]
>
>Este rango de IP no es compatible con los clientes que ejecutan AWS y que utilizan destinos basados en archivos para exportar datos a Amazon S3.

* `66.117.18.0/24`

## clientes estadounidenses {#us-customers}

* `52.252.71.64/29`

## Clientes de Canadá {#canada-customers}

* `20.220.135.16/29`

## Clientes de EMEA {#emea-customers}

* `51.137.8.208/29`

## clientes del Reino Unido {#uk-customers}

* `20.26.133.96/29`

## Clientes de APAC {#apac-customers}

* `20.53.201.168/29`
