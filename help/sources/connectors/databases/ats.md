---
keywords: Experience Platform;inicio;temas populares;Azure Table Storage;almacenamiento de tablas azure;ATS;ats
solution: Experience Platform
title: Descripción general del conector de origen de almacenamiento de tablas de Azure
topic-legacy: overview
description: Obtenga información sobre cómo conectar Azure Table Storage a Adobe Experience Platform mediante API o la interfaz de usuario.
exl-id: 096e01b1-7e95-4e30-87de-d0976f8b438a
source-git-commit: 5821f9304a37c1a03d17f0113d09548799662a2e
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# Conector (Beta) [!DNL Azure Table Storage]

>[!NOTE]
>
>El conector [!DNL Azure Table Storage] está en versión beta. Consulte la [información general sobre fuentes](../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiqueta beta.

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante los servicios [!DNL Platform]. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

[!DNL Experience Platform] permite la ingesta de datos desde una base de datos de terceros. [!DNL Platform] puede conectarse a diferentes tipos de bases de datos, como relacional, sinSQL o data warehouse. La compatibilidad con los proveedores de bases de datos incluye [!DNL Azure Table Storage].

## LISTA DE PERMITIDOS de direcciones IP

Se debe agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no agrega las direcciones IP específicas de su región a su lista de permitidos, puede que se produzcan errores o que no se produzca un rendimiento al utilizar fuentes. Consulte la página [lista de permitidos de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

>[!IMPORTANT]
>
>El conector de origen [!DNL Azure Table Storage] actualmente no admite conectividad de la misma región con Platform. Esto significa que si la instancia de Azure está usando la misma región de red que Platform, no se puede establecer una conexión con orígenes de Platform. Actualmente, solo se admite la conectividad entre regiones. Póngase en contacto con el administrador de cuentas de Adobe para obtener más información.

La documentación siguiente proporciona información sobre cómo conectar [!DNL Azure Table Storage] a [!DNL Platform] mediante API o la interfaz de usuario:

## Conectar [!DNL Azure Table Storage] a [!DNL Platform] mediante API

- [Creación de una conexión base de almacenamiento de tablas de Azure mediante la API de servicio de flujo](../../tutorials/api/create/databases/ats.md)
- [Explorar la estructura de datos y el contenido de un origen de base de datos mediante la API de servicio de flujo](../../tutorials/api/explore/database-nosql.md)
- [Creación de un flujo de datos para un origen de base de datos mediante la API de servicio de flujo](../../tutorials/api/collect/database-nosql.md)

## Conectar [!DNL Azure Table Storage] a [!DNL Platform] mediante la interfaz de usuario

- [Crear una conexión de origen de Azure Table Storage en la interfaz de usuario](../../tutorials/ui/create/databases/ats.md)
- [Crear un flujo de datos para una conexión de origen de base de datos en la interfaz de usuario](../../tutorials/ui/dataflow/databases.md)
