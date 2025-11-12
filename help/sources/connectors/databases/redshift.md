---
title: Información general sobre el conector Amazon Redshift Source
description: Aprenda a conectar Amazon Redshift a Adobe Experience Platform mediante API o la interfaz de usuario.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 75e577dd-a0b0-4f82-a371-5ec9255544f8
source-git-commit: 06b2108715ce368ff4ecf5c6c7dd3a327d9f61b1
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 7%

---

# Fuente de [!DNL Amazon Redshift] 

>[!IMPORTANT]
>
>- El origen [!DNL Amazon Redshift] está disponible en el catálogo de orígenes para los usuarios que han adquirido Real-Time CDP Ultimate.
>
>- Ahora puede usar el origen [!DNL Amazon Redshift] al ejecutar Adobe Experience Platform en Amazon Web Service (AWS). Experience Platform que se ejecuta en AWS está disponible actualmente para un número limitado de clientes. Para obtener más información sobre la infraestructura de Experience Platform compatible, consulte la [descripción general de la nube múltiple de Experience Platform](../../../landing/multi-cloud.md).


Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que ofrece la posibilidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Experience Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

Experience Platform es compatible con la ingesta de datos desde una base de datos de terceros. Experience Platform puede conectarse a diferentes tipos de bases de datos, como relacionales, NoSQL o almacenes de datos. La compatibilidad con los proveedores de bases de datos incluye [!DNL Amazon Redshift].

## Configurar el origen de [!DNL Amazon Redshift] para Experience Platform en Azure {#azure}

Siga los pasos a continuación para aprender a configurar su cuenta de [!DNL Amazon Redshift] para Experience Platform en Azure.

### LISTA DE PERMITIDOS de direcciones IP

Debe agregar direcciones IP específicas de la región a la lista de permitidos antes de conectar las fuentes a Experience Platform en Azure. Para obtener más información, lea la guía de [inclusión en la lista de permitidos de direcciones IP para conectarse a Experience Platform en Azure](../../ip-address-allow-list.md).

## Configurar el origen de [!DNL Amazon Redshift] para Experience Platform en Amazon Web Service {#aws}

>[!AVAILABILITY]
>
>Esta sección se aplica a las implementaciones de Experience Platform que se ejecutan en Amazon Web Service (AWS). Experience Platform que se ejecuta en AWS está disponible actualmente para un número limitado de clientes. Para obtener más información sobre la infraestructura de Experience Platform compatible, consulte la [descripción general de la nube múltiple de Experience Platform](../../../landing/multi-cloud.md).

### LISTA DE PERMITIDOS de direcciones IP para la conexión en AWS

Debe añadir direcciones IP específicas de la región a la lista de permitidos antes de conectar las fuentes a Experience Platform en AWS. Para obtener más información, lea la guía de [inclusión en la lista de permitidos de direcciones IP para conectarse a Experience Platform en AWS](../../ip-address-allow-list.md).

## Conectar [!DNL Amazon Redshift] a Experience Platform mediante API

- [Conexión de Amazon Redshift a Experience Platform mediante la API de Flow Service](../../tutorials/api/create/databases/redshift.md)
- [Exploración de tablas de datos mediante la API de Flow Service](../../tutorials/api/explore/tabular.md)
- [Crear un flujo de datos para un origen de base de datos mediante la API de Flow Service](../../tutorials/api/collect/database-nosql.md)

## Conectar [!DNL Amazon Redshift] a Experience Platform mediante la interfaz de usuario

- [Creación de una conexión de origen de Amazon Redshift en la interfaz de usuario](../../tutorials/ui/create/databases/redshift.md)
- [Crear un flujo de datos para una conexión de origen de base de datos en la IU](../../tutorials/ui/dataflow/databases.md)
