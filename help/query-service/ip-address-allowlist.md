---
keywords: Dirección IP, intervalo de IP, lista de permitidos, lista de permitidos
title: LISTA DE PERMITIDOS de direcciones IP para el servicio de consultas
description: Esta página proporciona rangos de IP que puede agregar a la lista de permitidos.
source-git-commit: 89d04a98e983b5dc9f353a831cdbe21c7c7aaf36
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 2%

---

# LISTA DE PERMITIDOS de direcciones IP {#ip-address-allow-list}

>[!IMPORTANT]
>
> * El Adobe recomienda marcar esta página y volver a visitarla cada tres meses para comprobar las direcciones IP más recientes. El Adobe no notifica nuevos intervalos de IP.
> * Aunque el Adobe admite la exportación de datos a servidores SFTP, las ubicaciones de almacenamiento en la nube recomendadas para exportar datos son [!DNL Amazon S3] y [!DNL Azure Blob].

## Información general {#overview}

Esta página proporciona direcciones IP que puede añadir a la lista de permitidos para exportar datos de forma segura de Experience Platform a [Servidor SFTP](../destinations/catalog/cloud-storage/sftp.md).

Puede definir controles de acceso a la red a través del cortafuegos de la red. Si especifica el rango de IP adecuado, puede permitir el tráfico para el servicio de transferencia de datos.

El Adobe recomienda añadir los siguientes intervalos de IP a una lista de permitidos en función de su región. Si no agrega el intervalo de IP específico de su región a la lista de permitidos, es posible que se produzcan errores o que no se cumpla el rendimiento.

## VA7: Clientes de EE. UU. y América {#us-americas}

* 52.138.119.167

## NLD2: Clientes de EMEA {#emea}

* 51.124.70.4

## AUS5: Clientes de APAC {#apac}

* 20.193.36.37

## CAN2: Clientes canadienses {#can2}

* 20.104.5.248
