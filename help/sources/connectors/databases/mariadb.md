---
title: Información general sobre el conector Source MariaDB
description: Obtenga información sobre cómo conectar MariaDB a Adobe Experience Platform mediante API o la interfaz de usuario.
exl-id: 37b8f991-dca9-4f85-9bdd-4927a015e4c0
source-git-commit: 0bf31c76f86b4515688d3aa60deb8744e38b4cd5
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 0%

---

# [!DNL MariaDB]

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de [!DNL Experience Platform]. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

Experience Platform es compatible con la ingesta de datos desde una base de datos de terceros. [!DNL Experience Platform] puede conectarse a diferentes tipos de bases de datos, como relacionales, NoSQL o almacenes de datos. La compatibilidad con los proveedores de bases de datos incluye [!DNL MariaDB].

## Requisitos previos {#prerequisites}

Lea las siguientes secciones para completar la configuración de requisitos previos antes de conectar su cuenta de [!DNL MariaDB] a Experience Platform.

### LISTA DE PERMITIDOS de direcciones IP

Debe agregar direcciones IP específicas de la región a la lista de permitidos antes de conectar las fuentes a Experience Platform en Azure o Amazon Web Service (AWS). Para obtener más información, lea la guía de [inclusión en la lista de permitidos de direcciones IP para conectarse a Experience Platform en Azure y AWS](../../ip-address-allow-list.md).

### Autenticar en Experience Platform en Azure {#azure}

Debe proporcionar valores para las siguientes credenciales para conectar [!DNL MariaDB] a Experience Platform en Azure.

>[!BEGINTABS]

>[!TAB Autenticación de clave de cuenta]

Para utilizar la autenticación de clave de cuenta, proporcione los valores adecuados para las siguientes credenciales.

| Credencial | Descripción |
| --- | --- |
| `connectionString` | La cadena de conexión asociada con su autenticación [!DNL MariaDB]. El patrón de cadena de conexión [!DNL MariaDB] es: `Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. El id. de especificación de conexión para [!DNL MariaDB] es `3000eb99-cd47-43f3-827c-43caf170f015`. **Nota**: esta credencial solo es necesaria cuando se conecta a través de la API [!DNL Flow Service]. |

Para obtener más información sobre cómo obtener una cadena de conexión, consulte este [[!DNL MariaDB] documento](https://mariadb.com/kb/en/about-mariadb-connector-odbc/).

>[!TAB Autenticación básica]

Para utilizar la autenticación básica, proporcione los valores adecuados para las siguientes credenciales.

| Credencial | Descripción |
| --- | --- |
| `server` | El nombre o IP de su base de datos [!DNL MariaDB]. |
| `username` | Nombre de la base de datos. |
| `port` | Número de puerto del extremo de comunicación al que se está conectando. |
| `password` | El nombre de usuario que corresponde con su base de datos. |
| `database` | La contraseña que corresponde a su base de datos. |
| `sslMode` | Método por el que se cifran los datos durante la transferencia de datos. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. El id. de especificación de conexión para [!DNL MariaDB] es `3000eb99-cd47-43f3-827c-43caf170f015`. **Nota**: esta credencial solo es necesaria cuando se conecta a través de la API [!DNL Flow Service]. |

Para obtener más información sobre cómo obtener una cadena de conexión, consulte este [[!DNL MariaDB] documento](https://mariadb.com/kb/en/about-mariadb-connector-odbc/).

>[!ENDTABS]

### Autenticar en Experience Platform en Amazon Web Service (AWS) {#aws}

>[!AVAILABILITY]
>
>Esta sección se aplica a las implementaciones de Experience Platform que se ejecutan en Amazon Web Service (AWS). Experience Platform que se ejecuta en AWS está disponible actualmente para un número limitado de clientes. Para obtener más información sobre la infraestructura de Experience Platform compatible, consulte la [descripción general de la nube múltiple de Experience Platform](../../../landing/multi-cloud.md).

Debe proporcionar valores para las siguientes credenciales a fin de conectar [!DNL MariaDB] a Experience Platform en AWS.

| Credencial | Descripción |
| --- | --- |
| `server` | El nombre o IP de su base de datos [!DNL MariaDB]. |
| `username` | Nombre de la base de datos. |
| `port` | Número de puerto del extremo de comunicación al que se está conectando. |
| `password` | El nombre de usuario que corresponde con su base de datos. |
| `database` | La contraseña que corresponde a su base de datos. |
| `sslMode` | Método por el que se cifran los datos durante la transferencia de datos. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. El id. de especificación de conexión para [!DNL MariaDB] es `3000eb99-cd47-43f3-827c-43caf170f015`. **Nota**: esta credencial solo es necesaria cuando se conecta a través de la API [!DNL Flow Service]. |

Para obtener más información sobre cómo obtener una cadena de conexión, consulte este [[!DNL MariaDB] documento](https://mariadb.com/kb/en/about-mariadb-connector-odbc/).

## Conectar [!DNL MariaDB] a Experience Platform mediante API

- [Crear una conexión base MariaDB mediante la API de Flow Service](../../tutorials/api/create/databases/mariadb.md)
- [Exploración de tablas de datos mediante la API de Flow Service](../../tutorials/api/explore/tabular.md)
- [Crear un flujo de datos para un origen de base de datos mediante la API de Flow Service](../../tutorials/api/collect/database-nosql.md)

## Conectar [!DNL MariaDB] a Experience Platform mediante la interfaz de usuario

- [Crear una conexión de origen MariaDB en la IU](../../tutorials/ui/create/databases/mariadb.md)
- [Crear un flujo de datos para una conexión de origen de base de datos en la IU](../../tutorials/ui/dataflow/databases.md)
