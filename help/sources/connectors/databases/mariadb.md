---
title: Descripción general del conector Origen MariaDB
description: Aprenda cómo conectar MariaDB a Adobe Experience Platform utilizando API o la interfaz usuario.
exl-id: 37b8f991-dca9-4f85-9bdd-4927a015e4c0
source-git-commit: 0bf31c76f86b4515688d3aa60deb8744e38b4cd5
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 0%

---

# [!DNL MariaDB]

Adobe Experience Platform permite que los datos se ingieran de fuentes externas al tiempo que le proporciona la capacidad de estructurar, etiquetar y mejorar los datos entrantes utilizando [!DNL Experience Platform] los servicios. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe Systems, almacenamiento basadas en nube, bases de datos y muchas otras.

Experience Platform proporciona compatibilidad para la ingesta de datos de una base de datos terceros. [!DNL Experience Platform] puede conectarse a diferentes tipos de bases de datos, como relacionales, NoSQL o almacenes de datos. La compatibilidad con los proveedores de bases de datos incluye [!DNL MariaDB].

## Requisitos previos {#prerequisites}

Lea las siguientes secciones para completar la configuración de requisitos previos antes de conectar [!DNL MariaDB] el cuenta a Experience Platform.

### Lista de direcciones IP permitidas

Debe agregar direcciones IP específicas de área geográfica a la lista de permitidos antes de conectar los orígenes a Experience Platform en Azure o Amazon Web Services (AWS). Para obtener más información, lea el guía sobre [permitir que las direcciones IP se conecten a Experience Platform en Azure y AWS](../../ip-address-allow-list.md) para obtener más información.

### Autenticación en Experience Platform en Azure {#azure}

Debe proporcionar valores para las siguientes credenciales para conectar [!DNL MariaDB] a Experience Platform en Azure.

>[!BEGINTABS]

>[!TAB Autenticación de clave de cuenta]

Para usar cuenta autenticación de clave, proporcione los valores adecuados para las siguientes credenciales.

| Credencial | Descripción |
| --- | --- |
| `connectionString` | La cadena de conexión asociada a la [!DNL MariaDB] autenticación. El [!DNL MariaDB] patrón de la cadena de conexión es: `Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de un origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y de origen. El ID de especificación de conexión de [!DNL MariaDB] es `3000eb99-cd47-43f3-827c-43caf170f015`. **Nota**: Esta credencial solo es necesaria cuando se conecta a través de la [!DNL Flow Service] API. |

Para obtener más información acerca de cómo obtener una cadena de conexión, consulte este [[!DNL MariaDB] documento](https://mariadb.com/kb/en/about-mariadb-connector-odbc/).

>[!TAB Autenticación básica]

Para usar la autenticación básica, proporcione los valores adecuados para las siguientes credenciales.

| Credencial | Descripción |
| --- | --- |
| `server` | El nombre o IP de la [!DNL MariaDB] base de datos. |
| `username` | Nombre de la base de datos. |
| `port` | Número puerto del extremo de comunicación al que se está conectando. |
| `password` | El nombre de usuario que corresponde a su base de datos. |
| `database` | El contraseña que corresponde a su base de datos. |
| `sslMode` | El método mediante el cual se cifran los datos durante la transferencia de datos. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de un origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y de origen. El id. de especificación de conexión para [!DNL MariaDB] es `3000eb99-cd47-43f3-827c-43caf170f015`. **Nota**: esta credencial solo es necesaria cuando se conecta a través de la API [!DNL Flow Service]. |

Para obtener más información sobre cómo obtener una cadena de conexión, consulte este [[!DNL MariaDB] documento](https://mariadb.com/kb/en/about-mariadb-connector-odbc/).

>[!ENDTABS]

### Autenticar en Experience Platform en Amazon Web Service (AWS) {#aws}

>[!AVAILABILITY]
>
>Esta sección se aplica a las implementaciones de Experience Platform que se ejecutan en Amazon Web Services (AWS). Experience Platform que se ejecutan en AWS están disponibles actualmente para un número limitado de clientes. Para obtener más información sobre la infraestructura Experience Platform compatible, consulte la Experience Platform información general](../../../landing/multi-cloud.md) sobre varios [nube.

Debe proporcionar valores para las siguientes credenciales para conectarse [!DNL MariaDB] a Experience Platform en AWS.

| Credencial | Descripción |
| --- | --- |
| `server` | El nombre o IP de la [!DNL MariaDB] base de datos. |
| `username` | Nombre de la base de datos. |
| `port` | Número puerto del extremo de comunicación al que se está conectando. |
| `password` | El nombre de usuario que corresponde a su base de datos. |
| `database` | El contraseña que corresponde a su base de datos. |
| `sslMode` | El método mediante el cual se cifran los datos durante la transferencia de datos. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de un origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y de origen. El ID de especificación de conexión de [!DNL MariaDB] es `3000eb99-cd47-43f3-827c-43caf170f015`. **Nota**: Esta credencial solo es necesaria cuando se conecta a través de la [!DNL Flow Service] API. |

Para obtener más información acerca de cómo obtener una cadena de conexión, consulte este [[!DNL MariaDB] documento](https://mariadb.com/kb/en/about-mariadb-connector-odbc/).

## Conéctese [!DNL MariaDB] a Experience Platform mediante API

- [Crear una conexión base MariaDB mediante la API de Flow Service](../../tutorials/api/create/databases/mariadb.md)
- [Exploración de tablas de datos mediante la API de Flow Service](../../tutorials/api/explore/tabular.md)
- [Crear un flujo de datos para un origen de base de datos mediante la API de servicio Flujo](../../tutorials/api/collect/database-nosql.md)

## Conéctese [!DNL MariaDB] a Experience Platform mediante el IU

- [Crear una conexión de origen MariaDB en el IU](../../tutorials/ui/create/databases/mariadb.md)
- [Crear un flujo de datos para una conexión de origen de base de datos en el IU](../../tutorials/ui/dataflow/databases.md)
