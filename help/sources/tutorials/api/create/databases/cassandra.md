---
keywords: Experience Platform;inicio;temas populares;Apache Cassandra;apache cassandra;Cassandra;cassandra
solution: Experience Platform
title: Creación de una conexión de origen de Apache Cassandra mediante la API de servicio de flujo
type: Tutorial
description: Obtenga información sobre cómo conectar Apache Cassandra a Adobe Experience Platform mediante la API de servicio de flujo.
source-git-commit: 997423f7bf92469e29c567bd77ffde357413bf9e
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 4%

---


# Cree un [!DNL Apache Cassandra] conexión de origen utilizando la variable [!DNL Flow Service] API

[!DNL Flow Service] se utiliza para recopilar y centralizar datos de clientes de diferentes fuentes dentro de Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde las que se pueden conectar todas las fuentes admitidas.

Este tutorial utiliza la variable [!DNL Flow Service] API para guiarle por los pasos para conectarse [!DNL Apache Cassandra] (en lo sucesivo denominada &quot;Cassandra&quot;) [!DNL Experience Platform].

## Primeros pasos

Esta guía requiere conocer los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): [!DNL Experience Platform] permite la ingesta de datos de varias fuentes, al mismo tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen un solo [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que debe conocer para conectarse correctamente a Cassandra mediante el [!DNL Flow Service] API.

### Recopilar las credenciales necesarias

Para [!DNL Flow Service] para conectarse con [!DNL Cassandra], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `host` | La dirección IP o el nombre de host de la variable [!DNL Cassandra] servidor. |
| `port` | El puerto TCP en el que [!DNL Cassandra] server utiliza para detectar conexiones de cliente. El puerto predeterminado es `9042`. |
| `username` | El nombre de usuario utilizado para conectarse a la variable [!DNL Cassandra] para la autenticación. |
| `password` | La contraseña para conectarse a la variable [!DNL Cassandra] para la autenticación. |
| `connectionSpec.id` | Identificador único necesario para crear una conexión. El ID de especificación de conexión para [!DNL Cassandra] es `a8f4d393-1a6b-43f3-931f-91a16ed857f4`. |

Para obtener más información sobre cómo empezar, consulte [este documento de Cassandra](https://cassandra.apache.org/doc/latest/operating/security.html#authentication).

### Leer llamadas de API de ejemplo

Este tutorial proporciona llamadas de API de ejemplo para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) en el [!DNL Experience Platform] guía de solución de problemas.

### Recopilar valores para encabezados necesarios

Para realizar llamadas a [!DNL Platform] API, primero debe completar la variable [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todos los [!DNL Experience Platform] Llamadas de API, como se muestra a continuación:

* Autorización: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Todos los recursos de [!DNL Experience Platform], incluidas las pertenecientes al [!DNL Flow Service], están aisladas para entornos limitados virtuales específicos. Todas las solicitudes a [!DNL Platform] Las API requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

* x-sandbox-name: `{SANDBOX_NAME}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medio adicional:

* Content-Type: `application/json`

## Crear una conexión

Una conexión especifica un origen y contiene sus credenciales para ese origen. Solo se requiere un conector por [!DNL Cassandra] porque se puede usar para crear varios conectores de origen para introducir datos diferentes.

**Formato de API**

```http
POST /connections
```

**Solicitud**

Para crear un [!DNL Cassandra] conexión, su ID de especificación de conexión única debe proporcionarse como parte de la solicitud del POST. El ID de especificación de conexión para [!DNL Cassandra] es `a8f4d393-1a6b-43f3-931f-91a16ed857f4`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Cassandra test connection",
        "description": "A test connection for Cassandra",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                    "host": "{HOST},
                    "port": "{PORT}",
                    "username": "{USERNAME}",
                    "password": "{PASSWORD}"
                }
        },
        "connectionSpec": {
            "id": "a8f4d393-1a6b-43f3-931f-91a16ed857f4",
            "version": "1.0"
        }
    }'
```

| Parámetro | Descripción |
| --------- | ----------- |
| `auth.params.host` | La dirección IP o el nombre de host de la variable [!DNL Cassandra] servidor. |
| `auth.params.port` | El puerto TCP en el que [!DNL Cassandra] server utiliza para detectar conexiones de cliente. El puerto predeterminado es `9042`. |
| `auth.params.username` | El nombre de usuario utilizado para conectarse a la variable [!DNL Cassandra] para la autenticación. |
| `auth.params.password` | La contraseña para conectarse a la variable [!DNL Cassandra] para la autenticación. |
| `connectionSpec.id` | La variable [!DNL Cassandra] id. de especificación de conexión: `a8f4d393-1a6b-43f3-931f-91a16ed857f4`. |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar sus datos en el siguiente tutorial.

```json
{
    "id": "ce69aa89-1baa-4054-a9aa-891baa605425",
    "etag": "\"5a026e19-0000-0200-0000-5eac76d00000\""
}
```

## Pasos siguientes

Al seguir este tutorial, ha creado un [!DNL Cassandra] conexión mediante la función [!DNL Flow Service] y han obtenido el valor de ID único de la conexión. Puede utilizar este ID en el siguiente tutorial mientras aprende a [explorar bases de datos mediante la API de servicio de flujo](../../explore/database-nosql.md).
