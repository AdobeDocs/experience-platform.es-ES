---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Conector de Data Explorer de Azure
topic: overview
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---


# Conector (Beta) [!DNL Azure Data Explorer]

>[!NOTE]
>
>El [!DNL Azure Data Explorer] conector está en versión beta. Consulte la descripción general [de](../../home.md#terms-and-conditions) Fuentes para obtener más información sobre el uso de conectores con etiquetas beta.

Adobe Experience Platform proporciona conectividad nativa para proveedores de bases de datos como [!DNL Microsoft], MySQL y [!DNL Azure]. Puede introducir los datos de estos sistemas en [!DNL Platform].

Se admiten diferentes tipos de bases de datos de terceros, incluidos los almacenes de datos relacionales, NoSQL o NoData. La compatibilidad con proveedores de bases de datos incluye [!DNL Azure Data Explorer].

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

La documentación siguiente proporciona información sobre cómo conectarse [!DNL Azure Data Explorer] a [!DNL Platform] través de API o de la interfaz de usuario:

## Conectar [!DNL Azure Data Explorer] a [!DNL Platform] mediante API

- [Creación de un conector de Data Explorer de Azure mediante la API de servicio de flujo](../../tutorials/api/create/databases/data-explorer.md)
- [Explorar un sistema de base de datos mediante la API de servicio de flujo](../../tutorials/api/explore/database-nosql.md)
- [Recopilación de datos de una base de datos mediante la API de servicio de flujo](../../tutorials/api/collect/database-nosql.md)

## Conectar [!DNL Azure Data Explorer] a [!DNL Platform] mediante la interfaz de usuario

- [Creación de un conector de origen de Data Explorer de Azure en la interfaz de usuario](../../tutorials/ui/create/databases/data-explorer.md)
- [Configurar un flujo de datos para un conector de base de datos en la interfaz de usuario](../../tutorials/ui/dataflow/databases.md)