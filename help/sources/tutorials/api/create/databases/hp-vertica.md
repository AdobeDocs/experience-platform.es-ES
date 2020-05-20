---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creación de un conector HP Vertica mediante la API de servicio de flujo
topic: overview
translation-type: tm+mt
source-git-commit: a015d2612bc5a72004e15dc5706c7718617a0af4
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 1%

---


# Creación de un conector HP Vertica mediante la API de servicio de flujo

>[!NOTE]
>El conector HP Vertica está en versión beta. Las funciones y la documentación están sujetas a cambios.

El servicio de flujo se utiliza para recopilar y centralizar datos de clientes de diversas fuentes en Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde la que se pueden conectar todas las fuentes admitidas.

Este tutorial utiliza la API de servicio de flujo para guiarle por los pasos para conectar HP Vertica con la plataforma de experiencia.

## Primeros pasos

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

- [Fuentes](https://docs.adobe.com/content/help/en/experience-platform/source-connectors/home.html): La plataforma de experiencia permite la ingesta de datos de diversas fuentes, al tiempo que le permite estructurar, asignar y mejorar los datos entrantes mediante los servicios de plataforma.
- [Simuladores](https://docs.adobe.com/content/help/en/experience-platform/sandbox/home.html): La plataforma de experiencia proporciona entornos limitados virtuales que dividen una instancia de plataforma única en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las siguientes secciones proporcionan información adicional que deberá conocer para conectarse correctamente a HP Vertica mediante la API de servicio de flujo.

### Recopilar las credenciales necesarias

Para que el servicio de flujo se conecte con HP Vertica, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `connectionString` | La cadena de conexión utilizada para conectarse a su instancia de HP Vertica. El patrón de cadena de conexión para HP Vertica es `Server=<server>;Port=<port>;Database=<database>;UID=<user name>;PWD=<password>` |
| `connectionSpec.id` | Identificador necesario para crear una conexión. El identificador de especificación de conexión fijo para HP Vertica es: `a8b6a1a4-5735-42b4-952c-85dce0ac38b5` |

Para obtener más información sobre la adquisición de una cadena de conexión, consulte [este documento](https://www.vertica.com/docs/9.2.x/HTML/Content/Authoring/ConnectingToVertica/ClientJDBC/CreatingAndConfiguringAConnection.htm)HP Vertica.

### Leer llamadas de API de muestra

Este tutorial proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener más información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas](https://docs.adobe.com/content/help/en/experience-platform/landing/troubleshooting.html#reading-example-api-calls) de API de ejemplo en la guía de solución de problemas de la plataforma de experiencia.

### Recopilar valores para encabezados necesarios

Para realizar llamadas a las API de plataforma, primero debe completar el tutorial [de](https://docs.adobe.com/content/help/en/experience-platform/tutorials/authentication.html)autenticación. Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas de API de la plataforma de experiencia, como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de la plataforma de experiencia, incluidos los conectores de origen, están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API de plataforma requieren un encabezado que especifique el nombre del simulador para pruebas en el que tendrá lugar la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medio adicional:

- Content-Type: `application/json`

## Crear una conexión

Una conexión especifica un origen y contiene sus credenciales para ese origen. Solo se requiere una conexión por cuenta de HP Vertica, ya que se puede utilizar para crear varios conectores de origen para traer datos diferentes.

**Formato API**

```http
POST /connections
```

**Solicitud**

Para crear una conexión HP Vertica, su ID de especificación de conexión única debe proporcionarse como parte de la solicitud POST. El ID de especificación de conexión para HP Vertica es `a8b6a1a4-5735-42b4-952c-85dce0ac38b5`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Connection for HP Vertica",
        "description": "Connection for HP Vertica",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                "connectionString": "Server=<server>;Port=<port>;Database=<database>;UID=<user name>;PWD=<password>"
            }
        },
        "connectionSpec": {
            "id": "a8b6a1a4-5735-42b4-952c-85dce0ac38b5",
            "version": "1.0"
        }
    }'
```

| Parámetro | Descripción |
| --------- | ----------- |
| `auth.params.connectionString` | La cadena de conexión asociada a su cuenta de HP Vertica. |
| `connectionSpec.id` | ID de especificación de conexión de HP Vertica: `a8b6a1a4-5735-42b4-952c-85dce0ac38b5`. |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar los datos en el siguiente tutorial.

```json
{
    "id": "6bc13a3b-3546-455f-813a-3b3546a55fb1",
    "etag": "\"3500866c-0000-0200-0000-5e83afa30000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión HP Vertica mediante la API de servicio de flujo y ha obtenido el valor de ID exclusivo de la conexión. Puede utilizar este ID en el siguiente tutorial cuando aprenda a [explorar bases de datos mediante la API](../../explore/database-nosql.md)de servicio de flujo.
