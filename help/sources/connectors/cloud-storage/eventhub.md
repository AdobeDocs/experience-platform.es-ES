---
keywords: Experience Platform;home;popular topics;Azure Event Hubs;azure event hubs;Event Hubs;event hubs
solution: Experience Platform
title: Conector de los centros de Evento de Azure
topic: overview
description: La siguiente documentación proporciona información sobre cómo conectar los centros de Evento de Azure a la plataforma mediante API o la interfaz de usuario.
translation-type: tm+mt
source-git-commit: 7b92327cfeb2410baf313dd650f68cfeb6db36e6
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---


# Conector de los centros de Evento de Azure (Beta)

>[!NOTE]
>
>El conector de los centros de Evento de Azure está en versión beta. Consulte la descripción general [de](../../home.md#terms-and-conditions) Fuentes para obtener más información sobre el uso de conectores con etiquetas beta.

Adobe Experience Platform proporciona conectividad nativa para proveedores de nube como AWS [!DNL Google Cloud Platform], y [!DNL Azure]. Puede introducir los datos de estos sistemas en [!DNL Platform].

Las fuentes de almacenamiento de nube pueden incorporar sus propios datos [!DNL Platform] sin necesidad de descargarlos, darles formato o cargarlos. Los datos introducidos se pueden formatear como JSON XDM, parquet XDM o delimitados. Cada paso del proceso se integra en el flujo de trabajo de fuentes. [!DNL Platform] le permite introducir datos desde [!DNL Azure Event Hubs] en tiempo real.

## LISTA DE PERMITIDOS de direcciones IP

Las siguientes direcciones IP deben agregarse a una lista de permitidos antes de trabajar con conectores de origen. Si no se agregan las direcciones IP específicas de su región a la lista de permitidos, puede que se produzcan errores o no se produzca un rendimiento al usar fuentes.

### Región del este de EE.UU.

- `20.41.2.0/23`
- `20.41.4.0/26`
- `20.44.17.80/28`
- `20.49.102.16/29`
- `40.70.148.160/28`
- `52.167.107.224/28`

### Región de Europa Occidental

- `13.69.67.192/28`
- `13.69.107.112/28`
- `13.69.112.128/28`
- `40.74.24.192/26`
- `40.74.26.0/23`
- `40.113.176.232/29`
- `52.236.187.112/28`

### Australia Oriental

- `13.70.74.144/28`
- `20.37.193.0/25`
- `20.37.193.128/26`
- `20.37.198.224/29`
- `40.79.163.80/28`
- `40.79.171.160/28`

## Conectar [!DNL Azure Event Hubs] a [!DNL Platform]

La documentación siguiente proporciona información sobre cómo conectarse [!DNL Azure Event Hubs] a [!DNL Platform] través de API o de la interfaz de usuario:

### Uso de API

- [Creación de un conector de concentradores de Evento de Azure mediante la API de servicio de flujo](../../tutorials/api/create/cloud-storage/eventhub.md)
- [Explorar un sistema de almacenamiento en la nube mediante la API de servicio de flujo](../../tutorials/api/explore/cloud-storage.md)
- [Recopilación de datos de almacenamiento en la nube mediante la API de servicio de flujo](../../tutorials/api/collect/cloud-storage.md)

### Uso de la interfaz de usuario

- [Creación de un conector de origen de los centros de Evento de Azure en la interfaz de usuario](../../tutorials/ui/create/cloud-storage/eventhub.md)
- [Configuración de un flujo de datos para un conector de almacenamiento de nube en la interfaz de usuario](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)