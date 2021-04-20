---
keywords: Experience Platform;inicio;temas populares;Amazon Kinesis;amazonía;Kinesis;kinesis
solution: Experience Platform
title: Información general del conector de origen de Amazon Kinesis
topic: overview
description: Obtenga información sobre cómo conectar Amazon Kinesis a Adobe Experience Platform mediante API o la interfaz de usuario.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---


# Conector (Beta) [!DNL Amazon Kinesis]

>[!NOTE]
>
>El conector [!DNL Amazon Kinesis] está en versión beta. Consulte la [información general sobre fuentes](../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiqueta beta.

Adobe Experience Platform proporciona conectividad nativa para proveedores de nube como AWS, [!DNL Google Cloud Platform] y [!DNL Azure]. Puede introducir los datos de estos sistemas en [!DNL Platform].

Las fuentes de almacenamiento en la nube pueden traer sus propios datos a [!DNL Platform] sin necesidad de descargar, formatear o cargar. Los datos introducidos pueden tener el formato XDM JSON, XDM Parquet o delimitados. Cada paso del proceso se integra en el flujo de trabajo Orígenes . [!DNL Platform] permite introducir datos desde  [!DNL Amazon Kinesis] en tiempo real.

## Lista de permitidos de direcciones IP

Se debe agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no agrega las direcciones IP específicas de su región a la lista de permitidos, puede que se produzcan errores o que no se produzca un rendimiento al utilizar fuentes. Consulte la página [IP address allow list](../../ip-address-allow-list.md) para obtener más información.

## Conectar [!DNL Amazon Kinesis] a [!DNL Platform]

La documentación siguiente proporciona información sobre cómo conectar [!DNL Amazon Kinesis] a [!DNL Platform] mediante API o la interfaz de usuario:

### Uso de API

- [Creación de una conexión de origen de Amazon Kinesis mediante la API de servicio de flujo](../../tutorials/api/create/cloud-storage/kinesis.md)
- [Recopilación de datos de flujo continuo mediante la API del servicio de flujo](../../tutorials/api/collect/streaming.md)

### Uso de la interfaz de usuario

- [Crear una conexión de origen de Amazon Kinesis en la interfaz de usuario](../../tutorials/ui/create/cloud-storage/kinesis.md)
- [Configurar un flujo de datos para una conexión de almacenamiento en la nube en la interfaz de usuario](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)