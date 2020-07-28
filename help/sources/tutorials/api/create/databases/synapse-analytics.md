---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creación de un conector de Analytics de sincronización de Azure mediante la API de servicio de flujo
topic: overview
translation-type: tm+mt
source-git-commit: fc5cdaa661c47e14ed5412868f3a54fd7bd2b451
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 2%

---


# Creación de un [!DNL Azure Synapse Analytics] conector mediante la [!DNL Flow Service] API

>[!NOTE]
>El conector Analytics de la sinapsis de Azure está en versión beta. Consulte la descripción general [de](../../../../home.md#terms-and-conditions) Fuentes para obtener más información sobre el uso de conectores con etiquetas beta.

[!DNL Flow Service] se utiliza para recopilar y centralizar datos de clientes de distintas fuentes dentro de Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde la que se pueden conectar todas las fuentes admitidas.

Este tutorial utiliza la API de servicio de flujo para guiarle por los pasos a los que conectarse [!DNL Azure Synapse Analytics] (en adelante, &quot;[!DNL Synapse]&quot;) a [!DNL Experience Platform].

## Primeros pasos

Esta guía requiere una comprensión práctica de los siguientes componentes del Adobe Experience Platform:

* [Fuentes](../../../../home.md): [!DNL Experience Platform] permite la ingesta de datos desde varias fuentes, al tiempo que le permite estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Simuladores](../../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las siguientes secciones proporcionan información adicional que deberá conocer para conectarse correctamente a [!DNL Synapse] través de la [!DNL Flow Service] API.

### Recopilar las credenciales necesarias

Para [!DNL Flow Service] conectarse con [!DNL Synapse], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `connectionString` | La cadena de conexión utilizada para conectarse a [!DNL Synapse]. El patrón de cadena de [!DNL Synapse] conexión es `Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30`. |
| `connectionSpec.id` | Identificador único necesario para crear una conexión. El ID de especificación de conexión para [!DNL Synapse] es: `a49bcc7d-8038-43af-b1e4-5a7a089a7d79` |

Para obtener más información sobre la obtención de una cadena de conexión, consulte [este documento](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-aad-authentication-configure?toc=%2Fazure%2Fsynapse-analytics%2Fsql-data-warehouse%2Ftoc.json&amp;bc=%2Fazure%2Fsynapse-analytics%2Fsql-data-warehouse%2Fbreadcrumb%2Ftoc.json&amp;tabs=azure-powershell)de sinapsis.

### Leer llamadas de API de muestra

Este tutorial proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de ejemplo en la guía de solución de problemas [!DNL Experience Platform] .

### Recopilar valores para encabezados necesarios

Para realizar llamadas a [!DNL Platform] API, primero debe completar el tutorial [de](../../../../../tutorials/authentication.md)autenticación. Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas [!DNL Experience Platform] de API, como se muestra a continuación:

* Autorización: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de [!DNL Experience Platform], incluidos los que pertenecen al [!DNL Flow Service], están aislados en entornos limitados virtuales específicos. Todas las solicitudes a [!DNL Platform] las API requieren un encabezado que especifique el nombre del entorno limitado en el que se realizará la operación:

* x-sandbox-name: `{SANDBOX_NAME}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medio adicional:

* Content-Type: `application/json`

## Crear una conexión

Una conexión especifica un origen y contiene sus credenciales para ese origen. Solo se requiere una conexión por [!DNL Synapse] cuenta, ya que se puede utilizar para crear varios conectores de origen para introducir datos diferentes.

**Formato API**

```http
POST /connections
```

**Solicitud**

Para crear una [!DNL Synapse] conexión, debe proporcionarse su ID de especificación de conexión única como parte de la solicitud del POST. El ID de especificación de conexión para [!DNL Synapse] es `a49bcc7d-8038-43af-b1e4-5a7a089a7d79`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Connection for Azure Synapse Analytics",
        "description": "Connection for Azure Synapse Analytics",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                "connectionString": "Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        },
        "connectionSpec": {
            "id": "a49bcc7d-8038-43af-b1e4-5a7a089a7d79",
            "version": "1.0"
        }
    }'
```

| Parámetro | Descripción |
| --------- | ----------- |
| `auth.params.connectionString` | La cadena de conexión utilizada para conectarse a [!DNL Synapse]. El patrón de cadena de [!DNL Synapse] conexión es `Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30`. |
| `connectionSpec.id` | El ID de especificación de [!DNL Synapse] conexión es: `a49bcc7d-8038-43af-b1e4-5a7a089a7d79`. |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar la base de datos en el siguiente tutorial.

```json
{
    "id": "6bc13a3b-3546-455f-813a-3b3546a55fb1",
    "etag": "\"3500866c-0000-0200-0000-5e83afa30000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una [!DNL Synapse] conexión mediante la [!DNL Flow Service] API y ha obtenido el valor de ID único de la conexión. Puede utilizar este ID en el siguiente tutorial cuando aprenda a [explorar bases de datos mediante la API](../../explore/database-nosql.md)de servicio de flujo.
