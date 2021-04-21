---
keywords: Experience Platform;inicio;temas populares;Data Explorer de Azure;explorador de datos azure
solution: Experience Platform
title: Descripción general del conector de origen de Data Explorer de Azure
topic-legacy: overview
description: Obtenga información sobre cómo conectar la Data Explorer de Azure a Adobe Experience Platform mediante API o la interfaz de usuario.
exl-id: 869bd8bb-51e6-4e0c-a3ec-ff083dda5789
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# Conector (Beta) [!DNL Azure Data Explorer]

>[!NOTE]
>
>El conector [!DNL Azure Data Explorer] está en versión beta. Consulte la [información general sobre fuentes](../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiqueta beta.

Adobe Experience Platform proporciona conectividad nativa para proveedores de bases de datos como [!DNL Microsoft], MySQL y [!DNL Azure]. Puede introducir los datos de estos sistemas en [!DNL Platform].

Se admiten diferentes tipos de bases de datos de terceros, incluidos los almacenes de datos relacionales, NoSQL o NoSQL. La compatibilidad con proveedores de bases de datos incluye [!DNL Azure Data Explorer].

## LISTA DE PERMITIDOS de direcciones IP

Se debe agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no agrega las direcciones IP específicas de su región a su lista de permitidos, puede que se produzcan errores o que no se produzca un rendimiento al utilizar fuentes. Consulte la página [lista de permitidos de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

>[!IMPORTANT]
>
>El conector de origen [!DNL Azure Data Explorer] actualmente no admite conectividad de la misma región con Platform. Esto significa que si la instancia de Azure está usando la misma región de red que Platform, no se puede establecer una conexión con orígenes de Platform. Actualmente, solo se admite la conectividad entre regiones. Póngase en contacto con el administrador de cuentas de Adobe para obtener más información.

La documentación siguiente proporciona información sobre cómo conectar [!DNL Azure Data Explorer] a [!DNL Platform] mediante API o la interfaz de usuario:

## Conectar [!DNL Azure Data Explorer] a [!DNL Platform] mediante API

- [Creación de una conexión de origen de Data Explorer de Azure mediante la API de servicio de flujo](../../tutorials/api/create/databases/data-explorer.md)
- [Explorar un sistema de base de datos mediante la API de servicio de flujo](../../tutorials/api/explore/database-nosql.md)
- [Recopilación de datos de una base de datos mediante la API de servicio de flujo](../../tutorials/api/collect/database-nosql.md)

## Conectar [!DNL Azure Data Explorer] a [!DNL Platform] mediante la interfaz de usuario

- [Crear una conexión de origen de Data Explorer de Azure en la interfaz de usuario](../../tutorials/ui/create/databases/data-explorer.md)
- [Configuración de un flujo de datos para una conexión de base de datos en la interfaz de usuario](../../tutorials/ui/dataflow/databases.md)
