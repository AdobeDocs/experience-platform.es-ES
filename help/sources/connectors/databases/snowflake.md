---
title: Resumen del conector de origen del Snowflake
description: Obtenga información sobre cómo conectar Snowflake a Adobe Experience Platform mediante API o la interfaz de usuario.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: df066463-1ae6-4ecd-ae0e-fb291cec4bd5
source-git-commit: 8b0f6eca87deedd8090830e3375d5099bfb0dfc0
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---

# [!DNL Snowflake] origen

>[!IMPORTANT]
>
>* El [!DNL Snowflake] La fuente de está disponible en el catálogo de fuentes de para los usuarios que han adquirido Real-time Customer Data Platform Ultimate.
>* De forma predeterminada, la variable [!DNL Snowflake] source interprets `null` como una cadena vacía. Póngase en contacto con el representante del Adobe para asegurarse de que su `null` Los valores de se escriben correctamente como `null` en Adobe Experience Platform.
>* Para que el Experience Platform pueda introducir datos, las zonas horarias de todos los orígenes de lotes basados en tablas deben configurarse en UTC. La única marca de tiempo compatible con el [!DNL Snowflake] La fuente es TIMESTAMP_NTZ con la hora UTC.

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

El Experience Platform proporciona asistencia para la ingesta de datos desde una base de datos de terceros. Platform puede conectarse a diferentes tipos de bases de datos, como relacionales, NoSQL o almacenes de datos. Los proveedores de bases de datos admiten [!DNL Snowflake].

## LISTA DE PERMITIDOS de direcciones IP

Se debe agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no se agregan las direcciones IP específicas de la región a la lista de permitidos, pueden producirse errores o no rendimiento al utilizar fuentes. Consulte la [LISTA DE PERMITIDOS de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

La siguiente documentación proporciona información sobre cómo conectarse [!DNL Snowflake] Vaya a Platform mediante las API o la interfaz de usuario de:

## Connect [!DNL Snowflake] a Platform mediante API

* [Crear una conexión base de Snowflake mediante la API de Flow Service](../../tutorials/api/create/databases/snowflake.md)
* [Exploración de tablas de datos mediante la API de Flow Service](../../tutorials/api/explore/tabular.md)
* [Crear un flujo de datos para un origen de base de datos mediante la API de Flow Service](../../tutorials/api/collect/database-nosql.md)

## Connect [!DNL Snowflake] a Platform mediante la IU

* [Crear una conexión de origen de Snowflake en la interfaz de usuario](../../tutorials/ui/create/databases/snowflake.md)
* [Crear un flujo de datos para una conexión de origen de base de datos en la IU](../../tutorials/ui/dataflow/databases.md)
