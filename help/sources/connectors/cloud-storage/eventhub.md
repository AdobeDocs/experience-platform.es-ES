---
keywords: Experience Platform;inicio;temas populares;Centros de Evento de Azure;Centros de evento de azure;Centros de Evento;Centros de evento
solution: Experience Platform
title: Conector de los centros de Evento de Azure
topic: overview
description: La siguiente documentación proporciona información sobre cómo conectar los centros de Evento de Azure a la plataforma mediante API o la interfaz de usuario.
translation-type: tm+mt
source-git-commit: 2940f030aa21d70cceeedc7806a148695f68739e
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---


# Conector de los centros de Evento de Azure (Beta)

>[!NOTE]
>
>El conector de los centros de Evento de Azure está en versión beta. Consulte la [información general de las fuentes](../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiquetas beta.

Adobe Experience Platform proporciona conectividad nativa para proveedores de nube como AWS, [!DNL Google Cloud Platform] y [!DNL Azure]. Puede traer los datos de estos sistemas a [!DNL Platform].

Las fuentes de almacenamiento de nube pueden traer sus propios datos a [!DNL Platform] sin necesidad de descargar, formatear o cargar. Los datos introducidos se pueden formatear como JSON XDM, Parquet XDM o delimitados. Cada paso del proceso se integra en el flujo de trabajo de fuentes. [!DNL Platform] permite introducir datos  [!DNL Azure Event Hubs] en tiempo real.

## LISTA DE PERMITIDOS de direcciones IP

Se debe agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no se agregan las direcciones IP específicas de su región a la lista de permitidos, puede que se produzcan errores o no se produzca un rendimiento al usar fuentes. Consulte la página [lista de permitidos de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

## Conectar [!DNL Azure Event Hubs] a [!DNL Platform]

La documentación siguiente proporciona información sobre cómo conectar [!DNL Azure Event Hubs] a [!DNL Platform] mediante API o la interfaz de usuario:

### Uso de API

- [Creación de un conector de concentradores de Evento de Azure mediante la API de servicio de flujo](../../tutorials/api/create/cloud-storage/eventhub.md)
- [Recopilación de datos de flujo mediante la API de servicio de flujo](../../tutorials/api/collect/streaming.md)

### Uso de la interfaz de usuario

- [Creación de un conector de origen de los centros de Evento de Azure en la interfaz de usuario](../../tutorials/ui/create/cloud-storage/eventhub.md)
- [Configuración de un flujo de datos para un conector de almacenamiento de nube en la interfaz de usuario](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)