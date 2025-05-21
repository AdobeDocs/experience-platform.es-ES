---
title: Información general sobre el conector MySQL Source
description: Aprenda a conectar MySQL a Adobe Experience Platform mediante API o la interfaz de usuario.
last-substantial-update: 2025-05-20T00:00:00Z
exl-id: a18e8e69-880f-4bee-b339-726091d6f858
source-git-commit: b73ced639100c95f6c62be92d4796a206a688958
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 0%

---

# [!DNL MySQL]

[!DNL MySQL] es un sistema de administración de bases de datos relacionales de código abierto que se usa para almacenar y administrar datos estructurados. Organiza los datos en tablas y utiliza SQL (Lenguaje de consulta estructurado) para consultar y actualizar la información. [!DNL MySQL] se utiliza ampliamente en aplicaciones web, admite varias plataformas y es conocido por su velocidad, confiabilidad y facilidad de uso.

Puede usar el origen [!DNL MySQL] para conectar su cuenta e introducir datos de su base de datos [!DNL MySQL] en Adobe Experience Platform.

## Requisitos previos {#prerequisites}

Lea las siguientes secciones para completar la configuración de requisitos previos antes de conectar su cuenta de [!DNL MySQl] a Experience Platform.

### LISTA DE PERMITIDOS de direcciones IP

Debe agregar direcciones IP específicas de la región a la lista de permitidos antes de conectar las fuentes a Experience Platform en Azure o Amazon Web Service (AWS). Para obtener más información, lea la guía de [inclusión en la lista de permitidos de direcciones IP para conectarse a Experience Platform en Azure y AWS](../../ip-address-allow-list.md).

### Autenticar en Experience Platform en Azure {#azure}

Puede utilizar la autenticación de clave de cuenta o la autenticación básica para conectar su base de datos de [!DNL MySQL] a Experience Platform en Azure.

>[!BEGINTABS]

>[!TAB Autenticación de clave de cuenta]

Proporcione valores para las siguientes credenciales a fin de conectar su base de datos [!DNL MySQL] a Experience Platform mediante la autenticación de clave de cuenta.

| Credencial | Descripción |
| --- | --- |
| `connectionString` | La cadena de conexión [!DNL MySQL] asociada a su cuenta. El patrón de cadena de conexión [!DNL MySQL] es: `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y de origen. El id. de especificación de conexión para [!DNL MySQL] es `26d738e0-8963-47ea-aadf-c60de735468a`. |

Para obtener más información, lea la [[!DNL MySQL] documentación sobre cadenas de conexión](https://dev.mysql.com/doc/connector-net/en/connector-net-connections-string.html).

>[!TAB Autenticación básica]

Proporcione valores para las siguientes credenciales a fin de conectar su base de datos [!DNL MySQL] a Experience Platform mediante la autenticación básica.

| Credencial | Descripción |
| --- | --- |
| `server` | Nombre o dirección IP de la base de datos [!DNL MySQL]. |
| `username` | El nombre de usuario asociado con la autenticación de la base de datos [!DNL MySQL]. |
| `password` | La contraseña asociada con la autenticación de la base de datos [!DNL MySQL]. |
| `database` | Nombre de la base de datos [!DNL MySQL] a la que desea conectarse. |
| `sslMode` | El método [!DNL Secure Sockets Layer] (SSL) que se aplicará a su conexión. Los valores disponibles son: <ul><li>`DISABLED`: utilice esta opción para deshabilitar SSL. Si el servidor requiere una configuración SSL, la conexión fallará</li><li>`PREFERRED`: utilice esta opción para preferir las conexiones SSL, ya que el servidor las admite. Esta opción también permite conexiones no SSL.</li><li>`REQUIRED`: utilice esta opción para que las conexiones SSL sean obligatorias. Si el servidor no admite SSL, las conexiones fallarán.</li><li>`Verify-Ca`: utilice esta opción para comprobar los certificados de servidor mientras se producen errores en las conexiones si el servidor no admite SSL.</li><li>`Verify Identity`: utilice esta opción para comprobar los certificados de servidor con el nombre del host mientras se producen errores en las conexiones si el servidor no admite SSL.</li></ul> |

>[!ENDTABS]

### Autenticar en Experience Platform en Amazon Web Service (AWS) {#aws}

>[!AVAILABILITY]
>
>Esta sección se aplica a las implementaciones de Experience Platform que se ejecutan en Amazon Web Service (AWS). Experience Platform que se ejecuta en AWS está disponible actualmente para un número limitado de clientes. Para obtener más información sobre la infraestructura de Experience Platform compatible, consulte la [descripción general de la nube múltiple de Experience Platform](../../../landing/multi-cloud.md).

Debe proporcionar valores para las siguientes credenciales a fin de conectar [!DNL MySQL] a Experience Platform en AWS.

| Credencial | Descripción |
| --- | --- |
| `server` | El nombre o IP de su base de datos [!DNL MySQL]. |
| `username` | Nombre de la base de datos. |
| `password` | El nombre de usuario que corresponde con su base de datos. |
| `database` | La contraseña que corresponde a su base de datos. |
| `sslMode` | Un valor booleano que controla si SSL se aplica o no, según la compatibilidad con el servidor. El valor predeterminado de esta configuración es `false`. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. El id. de especificación de conexión para [!DNL MySQL] es `26d738e0-8963-47ea-aadf-c60de735468a`. **Nota**: esta credencial solo es necesaria cuando se conecta a través de la API [!DNL Flow Service]. |

## Conectar [!DNL MySQL] a Experience Platform mediante API

- [Conecte su base de datos  [!DNL MySQL] mediante la API de Flow Service](../../tutorials/api/create/databases/mysql.md)
- [Exploración de tablas de datos mediante la API de Flow Service](../../tutorials/api/explore/tabular.md)
- [Crear un flujo de datos para un origen de base de datos mediante la API de Flow Service](../../tutorials/api/collect/database-nosql.md)

## Conectar MySQL a Experience Platform mediante la IU

- [Conecte su base de datos  [!DNL MySQL] a Experience Platform mediante la interfaz de usuario](../../tutorials/ui/create/databases/mysql.md)
- [Crear un flujo de datos para una conexión de origen de base de datos en la IU](../../tutorials/ui/dataflow/databases.md)
