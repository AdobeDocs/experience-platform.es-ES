---
title: Información general sobre el conector Source PostgreSQL
description: Obtenga información sobre el origen PostgreSQL en Adobe Experience Platform.
last-substantial-update: 2025-05-20T00:00:00Z
exl-id: 27b891c5-5fc5-4539-8f98-e3a53e2eefe3
source-git-commit: f4200ca71479126e585ac76dd399af4092fdf683
workflow-type: tm+mt
source-wordcount: '667'
ht-degree: 0%

---

# [!DNL PostgreSQL]

Lea este documento para obtener más información acerca de los pasos necesarios que debe llevar a cabo antes de conectar la base de datos de [!DNL PostgreSQL] a Adobe Experience Platform.

## Requisitos previos {#prerequisites}

Lea las siguientes secciones para completar la configuración de requisitos previos antes de conectar la base de datos de [!DNL PostgreSQL] a Experience Platform.

### LISTA DE PERMITIDOS de direcciones IP

Debe agregar direcciones IP específicas de la región a la lista de permitidos antes de conectar las fuentes a Experience Platform en Azure o Amazon Web Service (AWS). Para obtener más información, lea la guía de [inclusión en la lista de permitidos de direcciones IP para conectarse a Experience Platform en Azure y AWS](../../ip-address-allow-list.md).

### Autenticar en Experience Platform en Azure {#azure}

Debe proporcionar valores para las siguientes credenciales de autenticación para conectar [!DNL PostgreSQL] a Experience Platform en Azure.

>[!BEGINTABS]

>[!TAB Autenticación de clave de cuenta]

Proporcione valores para las siguientes credenciales a fin de conectar su base de datos de [!DNL PostgreSQL] a Experience Platform en Azure mediante la autenticación de clave de cuenta.

| Credencial | Descripción |
| --- | --- |
| `connectionString` | La cadena de conexión asociada a su cuenta de [!DNL PostgreSQL]. El patrón de cadena de conexión [!DNL PostgreSQL] es: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. El id. de especificación de conexión para [!DNL PostgreSQL] es `74a1c565-4e59-48d7-9d67-7c03b8a13137`. Esta credencial solo es necesaria cuando se conecta a través de la API [!DNL Flow Service]. |

Lea la [[!DNL PostgreSQL] documentación](https://www.postgresql.org/docs/current/) para obtener más información.

>[!TAB Autenticación básica]

Proporcione valores para las siguientes credenciales a fin de conectar su base de datos de [!DNL PostgreSQL] a Experience Platform en Azure mediante la autenticación básica.

| Credencial | Descripción |
| --- | --- |
| `server` | Nombre o dirección IP de la base de datos [!DNL PostgreSQL]. |
| `port` | El puerto TCP del servidor [!DNL PostgreSQL]. |
| `username` | El nombre de usuario asociado con la autenticación de la base de datos [!DNL PostgreSQL]. |
| `password` | La contraseña asociada con la autenticación de la base de datos [!DNL PostgreSQL]. |
| `database` | Nombre de la base de datos [!DNL PostgreSQL] a la que desea conectarse. |
| `sslMode` | El método [!DNL Secure Sockets Layer] (SSL) que se aplicará a su conexión. Los valores disponibles son: <ul><li>`Disable`: utilice esta opción para deshabilitar SSL. Si el servidor requiere una configuración SSL, la conexión fallará.</li><li>`Allow`: utilice esta opción para permitir conexiones SSL. Las conexiones no SSL pueden seguir utilizándose si el servidor las admite.</li><li>`Prefer`: utilice esta opción para preferir las conexiones SSL, ya que el servidor las admite. Esta opción también permite conexiones no SSL.</li><li>`Require`: utilice esta opción para que las conexiones SSL sean obligatorias. Si el servidor no admite SSL, las conexiones fallarán.</li><li>`Verify-Ca`: utilice esta opción para comprobar los certificados de servidor mientras se producen errores en las conexiones si el servidor no admite SSL.</li><li>`Verify-Full`: utilice esta opción para comprobar los certificados de servidor con el nombre del host mientras se producen errores en las conexiones si el servidor no admite SSL.</li></ul> |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. El id. de especificación de conexión para [!DNL PostgreSQL] es `74a1c565-4e59-48d7-9d67-7c03b8a13137`. Esta credencial solo es necesaria cuando se conecta a través de la API [!DNL Flow Service]. |

Lea la [[!DNL PostgreSQL] documentación](https://www.postgresql.org/docs/current/) para obtener más información.

>[!ENDTABS]

### Autenticar en Experience Platform en Amazon Web Service (AWS) {#aws}

>[!AVAILABILITY]
>
>Esta sección se aplica a las implementaciones de Experience Platform que se ejecutan en Amazon Web Service (AWS). Experience Platform que se ejecuta en AWS está disponible actualmente para un número limitado de clientes. Para obtener más información sobre la infraestructura de Experience Platform compatible, consulte la [descripción general de la nube múltiple de Experience Platform](../../../landing/multi-cloud.md).

Proporcione valores para las siguientes credenciales a fin de conectar su base de datos [!DNL PostgreSQL] a Experience Platform en AWS mediante la autenticación básica.

| Credencial | Descripción |
| --- | --- |
| `server` | Nombre o dirección IP de la base de datos [!DNL PostgreSQL]. |
| `port` | El puerto TCP del servidor [!DNL PostgreSQL]. |
| `username` | El nombre de usuario asociado con la autenticación de la base de datos [!DNL PostgreSQL]. |
| `password` | La contraseña asociada con la autenticación de la base de datos [!DNL PostgreSQL]. |
| `database` | Nombre de la base de datos [!DNL PostgreSQL] a la que desea conectarse. |
| `sslMode` | Un valor booleano que controla si SSL se aplica o no, según la compatibilidad con el servidor. El valor predeterminado de esta configuración es `false`. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. El id. de especificación de conexión para [!DNL PostgreSQL] es `74a1c565-4e59-48d7-9d67-7c03b8a13137`. Esta credencial solo es necesaria cuando se conecta a través de la API [!DNL Flow Service]. |

Lea la [[!DNL PostgreSQL] documentación](https://www.postgresql.org/docs/current/) para obtener más información.

## Conectar [!DNL PostgreSQL] a Experience Platform mediante API

* [Crear una conexión base  [!DNL PostgreSQL] mediante la API de Flow Service](../../tutorials/api/create/databases/postgres.md)
* [Exploración de tablas de datos mediante la API de Flow Service](../../tutorials/api/explore/tabular.md)
* [Crear un flujo de datos para un origen de base de datos mediante la API de Flow Service](../../tutorials/api/collect/database-nosql.md)

## Conectar [!DNL PostgreSQL] a Experience Platform mediante la interfaz de usuario

* [Crear una  [!DNL PostgreSQL] conexión de origen en la interfaz de usuario](../../tutorials/ui/create/databases/postgres.md)
* [Crear un flujo de datos para una conexión de origen de base de datos en la IU](../../tutorials/ui/dataflow/databases.md)
