---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creación de un conector de SQL Server mediante la API de servicio de flujo
topic: overview
translation-type: tm+mt
source-git-commit: e4ed6ae3ee668cd0db741bd07d2fb7be593db4c9
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 1%

---


# Creación de un conector de Microsoft SQL Server mediante la API de servicio de flujo

>[!NOTE]
>El conector de Microsoft SQL Server está en versión beta. Consulte la descripción general [de](../../../../home.md#terms-and-conditions) Fuentes para obtener más información sobre el uso de conectores con etiquetas beta.

El servicio de flujo se utiliza para recopilar y centralizar datos de clientes de distintas fuentes dentro de Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde la que se pueden conectar todas las fuentes admitidas.

Este tutorial utiliza la API de servicio de flujo para guiarle por los pasos para conectar a un Experience Platform a Microsoft SQL Server (en adelante, &quot;SQL Server&quot;).

## Primeros pasos

Esta guía requiere una comprensión práctica de los siguientes componentes del Adobe Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos desde varias fuentes, al tiempo que le permite estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Simuladores](../../../../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente a SQL Server mediante la API de servicio de flujo.

### Recopilar las credenciales necesarias

Para conectarse a SQL Server, debe proporcionar la siguiente propiedad de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `connectionString` | La cadena de conexión asociada a su cuenta de SQL Server. El patrón de cadena de conexión de SQL Server es: `Data Source={SERVER_NAME}\\<{INSTANCE_NAME} if using named instance>;Initial Catalog={DATABASE};Integrated Security=False;User ID={USERNAME};Password={PASSWORD};`. |
| `connectionSpec.id` | ID utilizado para generar una conexión. Se ha corregido el identificador de especificación de conexión para SQL Server `1f372ff9-38a4-4492-96f5-b9a4e4bd00ec`. |

Para obtener más información sobre la obtención de una cadena de conexión, consulte [este documento](https://docs.microsoft.com/en-us/dotnet/framework/data/adonet/sql/authentication-in-sql-server)de SQL Server.

### Leer llamadas de API de muestra

Este tutorial proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener más información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de ejemplo en la guía de solución de problemas del Experience Platform.

### Recopilar valores para encabezados necesarios

Para realizar llamadas a las API de Platform, primero debe completar el tutorial [de](../../../../../tutorials/authentication.md)autenticación. La finalización del tutorial de autenticación proporciona los valores para cada uno de los encabezados necesarios en todas las llamadas de API de Experience Platform, como se muestra a continuación:

* Autorización: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de Experience Platform, incluidos los que pertenecen al servicio de flujo, están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API de Platform requieren un encabezado que especifique el nombre del entorno limitado en el que se realizará la operación:

* x-sandbox-name: `{SANDBOX_NAME}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medio adicional:

* Content-Type: `application/json`

## Crear una conexión

Una conexión especifica un origen y contiene sus credenciales para ese origen. Solo se requiere una conexión por cuenta de SQL Server, ya que se puede utilizar para crear varios conectores de origen para traer datos diferentes.

**Formato API**

```http
POST /connections
```

**Solicitud**

Para crear una conexión de SQL Server, se debe proporcionar su ID de especificación de conexión única como parte de la solicitud POST. El ID de especificación de conexión para SQL Server es `1f372ff9-38a4-4492-96f5-b9a4e4bd00ec`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Base connection for sql-server",
        "description": "Base connection for sql-server",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                "connectionString": "Data Source={SERVER_NAME}\\<{INSTANCE_NAME} if using named instance>;Initial Catalog={DATABASE};Integrated Security=False;User ID={USERNAME};Password={PASSWORD};"
            }
        },
        "connectionSpec": {
            "id": "1f372ff9-38a4-4492-96f5-b9a4e4bd00ec",
            "version": "1.0"
    }'
```

| Propiedad | Descripción |
| --------- | ----------- |
| `auth.params.connectionString` | La cadena de conexión asociada a su cuenta de SQL Server. El patrón de cadena de conexión de SQL Server es: `Data Source={SERVER_NAME}\\<{INSTANCE_NAME} if using named instance>;Initial Catalog={DATABASE};Integrated Security=False;User ID={USERNAME};Password={PASSWORD};`. |
| `connectionSpec.id` | El ID de especificación de conexión para SQL Server es: `1f372ff9-38a4-4492-96f5-b9a4e4bd00ec`. |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar la base de datos en el siguiente tutorial.

```json
{
    "id": "0b8224e4-0de8-4293-8224-e40de80293c6",
    "etag": "\"5802c519-0000-0200-0000-5e4d89520000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión de SQL Server mediante la API de servicio de flujo y ha obtenido el valor de ID único de la conexión. Puede utilizar este ID de conexión en el siguiente tutorial a medida que aprenda a [explorar bases de datos o sistemas NoSQL mediante la API](../../explore/database-nosql.md)de servicio de flujo.
