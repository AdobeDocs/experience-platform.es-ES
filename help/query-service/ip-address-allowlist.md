---
keywords: Dirección IP, intervalo de IP, lista de permitidos, lista de permitidos
title: LISTA DE PERMITIDOS de direcciones IP para el servicio de consultas
description: Esta página proporciona rangos de IP que puede agregar a la lista de permitidos.
exl-id: f6745e0f-d387-45f2-9f72-054e721016ff
source-git-commit: 3a00f98b7463f7fb35aa53f703d67193f18400cf
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---

# LISTA DE PERMITIDOS de direcciones IP {#ip-address-allow-list}

>[!IMPORTANT]
>
> * El Adobe recomienda marcar esta página y volver a visitarla cada tres meses para comprobar las direcciones IP más recientes. El Adobe no notifica nuevos intervalos de IP.
> * Aunque el Adobe admite la exportación de datos a servidores SFTP, las ubicaciones de almacenamiento en la nube recomendadas para exportar datos son [!DNL Amazon S3] y [!DNL Azure Blob].

## Información general {#overview}

Esta página proporciona direcciones IP que puede agregar a su lista de permitidos para exportar con seguridad datos del Experience Platform a su [servidor SFTP](../destinations/catalog/cloud-storage/sftp.md).

Puede definir controles de acceso a la red a través del cortafuegos de la red. Si especifica el rango de IP adecuado, puede permitir el tráfico para el servicio de transferencia de datos.

El Adobe recomienda añadir los siguientes intervalos de IP a una lista de permitidos en función de su región. Si no agrega el intervalo de IP específico de su región a la lista de permitidos, es posible que se produzcan errores o que no se cumpla el rendimiento.

## VA7: Clientes de EE. UU. y América {#us-americas}

* 20.14.241.153

## NLD2: Clientes de EMEA {#emea}

* 20 101 233 128

## AUS5: Clientes de APAC {#apac}

* 20.248.220.69

## CAN2: Clientes canadienses {#can2}

* 4 172 1 1 139

## GBR9: Clientes de Reino Unido {#gbr9}

* 20.108.200.9

