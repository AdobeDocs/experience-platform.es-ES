---
title: Crear una conexión base de Microsoft SQL Server mediante la API de Flow Service
type: Tutorial
description: Obtenga información sobre cómo conectar Adobe Experience Platform a un servidor SQL Server de Microsoft mediante la API de Flow Service.
exl-id: 00455a61-c8c1-42f4-a962-fc16f7370cbd
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 5%

---

# Crear una conexión base de SQL Server [!DNL Microsoft] mediante la API [!DNL Flow Service]

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Lea este tutorial para aprender a crear una conexión base para [!DNL Microsoft SQL Server] mediante la [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introducción 

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Experience Platform.
* [Zonas protegidas](../../../../../sandboxes/home.md): Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Experience Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que necesitará conocer para conectarse correctamente a [!DNL Microsoft SQL Server] mediante la API [!DNL Flow Service].

### Recopilar credenciales necesarias {#gather-required-credentials}

Para conectarse a [!DNL Microsoft SQL Server], debe proporcionar la siguiente propiedad de conexión:

| Credencial | Descripción | Ejemplo |
| --- | --- | --- |
| `connectionString` | La cadena de conexión asociada a su cuenta de [!DNL Microsoft SQL Server]. El patrón de la cadena de conexión depende de si está utilizando un nombre de servidor o de instancia para el origen de datos:<ul><li>Cadena de conexión con nombre de servidor: `Data Source={SERVER_NAME};Initial Catalog={DATABASE};Integrated Security=False;User ID={USER_ID};Password={PASSWORD};`</li><li>Cadena de conexión con nombre de instancia:`Data Source={INSTANCE_NAME};Initial Catalog={DATABASE};Integrated Security=False;User ID={USER_ID};Password={PASSWORD};` | `Data Source=mssqlserver.database.windows.net;Initial Catalog=mssqlserver_e2e_db;Integrated Security=False;User ID=mssqluser;Password=mssqlpassword` |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. El id. de especificación de conexión para [!DNL Microsoft SQL Server] es `1f372ff9-38a4-4492-96f5-b9a4e4bd00ec`. |

Para obtener más información sobre cómo obtener una cadena de conexión, consulte este [[!DNL Microsoft SQL Server] documento](https://docs.microsoft.com/en-us/dotnet/framework/data/adonet/sql/authentication-in-sql-server).

### Uso de API de Experience Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Experience Platform, consulte la guía sobre [introducción a las API de Experience Platform](../../../../../landing/api-guide.md).

## Crear una conexión base

Una conexión base retiene información entre el origen y Experience Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el identificador único de la conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un identificador de conexión base, realice una petición POST al extremo `/connections` y proporcione sus credenciales de autenticación [!DNL Microsoft SQL Server] como parte de los parámetros de solicitud.

**Formato de API**

```https
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para [!DNL Microsoft SQL Server]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Base connection for sql-server",
      "description": "Base connection for sql-server",
      "auth": {
          "specName": "Connection String Based Authentication",
          "params": {
              "connectionString": "Data Source=mssqlserver.database.windows.net;Initial Catalog=mssqlserver_e2e_db;Integrated Security=False;User ID=mssqluser;Password=mssqlpassword"
          }
      },
      "connectionSpec": {
          "id": "1f372ff9-38a4-4492-96f5-b9a4e4bd00ec",
          "version": "1.0"
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `auth.params.connectionString` | La cadena de conexión asociada a su cuenta de [!DNL Microsoft SQL Server]. Lea la sección [recopilación de credenciales necesarias](#gather-required-credentials) para obtener más información. |
| `connectionSpec.id` | El id. de especificación de conexión [!DNL Microsoft SQL Server] es: `1f372ff9-38a4-4492-96f5-b9a4e4bd00ec`. |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar la base de datos en el siguiente tutorial.

```json
{
    "id": "0b8224e4-0de8-4293-8224-e40de80293c6",
    "etag": "\"5802c519-0000-0200-0000-5e4d89520000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión base [!DNL Microsoft SQL Server] mediante la API [!DNL Flow Service]. Puede utilizar este ID de conexión base en los siguientes tutoriales:

* [Explore la estructura y el contenido de las tablas de datos mediante la API  [!DNL Flow Service] B](../../explore/tabular.md)
* [Cree un flujo de datos para llevar los datos de la base de datos a Experience Platform mediante la API  [!DNL Flow Service] ](../../collect/database-nosql.md)