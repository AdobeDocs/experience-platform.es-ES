---
keywords: Experience Platform;inicio;temas populares;Apache Cassandra;apache cassandra;Cassandra;cassandra
solution: Experience Platform
title: Creación de una conexión de Apache Cassandra Source mediante la API de Flow Service
type: Tutorial
description: Aprenda a conectar Apache Cassandra a Adobe Experience Platform mediante la API de Flow Service.
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 11%

---


# Crear una conexión de origen [!DNL Apache Cassandra] mediante la API [!DNL Flow Service]

[!DNL Flow Service] se usa para recopilar y centralizar datos de clientes de distintos orígenes dentro de Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde las que se pueden conectar todas las fuentes de datos admitidas.

Este tutorial usa la API [!DNL Flow Service] para guiarle por los pasos para conectar [!DNL Apache Cassandra] (en adelante, &quot;Cassandra&quot;) a [!DNL Experience Platform].

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): [!DNL Experience Platform] permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de [!DNL Experience Platform].
* [Zonas protegidas](../../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola instancia de [!DNL Experience Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que necesitará conocer para conectarse correctamente a Cassandra mediante la API [!DNL Flow Service].

### Recopilar credenciales necesarias

Para que [!DNL Flow Service] se conecte con [!DNL Cassandra], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `host` | Dirección IP o nombre de host del servidor [!DNL Cassandra]. |
| `port` | El puerto TCP que utiliza el servidor [!DNL Cassandra] para detectar conexiones de cliente. El puerto predeterminado es `9042`. |
| `username` | Nombre de usuario utilizado para conectarse al servidor [!DNL Cassandra] para la autenticación. |
| `password` | Contraseña para conectarse al servidor [!DNL Cassandra] para la autenticación. |
| `connectionSpec.id` | El identificador único necesario para crear una conexión. El id. de especificación de conexión para [!DNL Cassandra] es `a8f4d393-1a6b-43f3-931f-91a16ed857f4`. |

Para obtener más información sobre cómo empezar, consulte [este documento de Cassandra](https://cassandra.apache.org/doc/latest/operating/security.html#authentication).

### Lectura de llamadas de API de muestra

Este tutorial proporciona llamadas de API de ejemplo para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de la API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de ejemplo, consulte la sección sobre [cómo leer las llamadas de API de ejemplo](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas de [!DNL Experience Platform].

### Recopilación de valores para los encabezados obligatorios

Para poder realizar llamadas a las API de [!DNL Experience Platform], primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados obligatorios en todas las llamadas de API de [!DNL Experience Platform], como se muestra a continuación:

* Autorización: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Todos los recursos de [!DNL Experience Platform], incluidos los que pertenecen a [!DNL Flow Service], están aislados en zonas protegidas virtuales específicas. Todas las solicitudes a las API de [!DNL Experience Platform] requieren un encabezado que especifique el nombre de la zona protegida en la que se realizará la operación:

* x-sandbox-name: `{SANDBOX_NAME}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medios adicional:

* Tipo de contenido: `application/json`

## Crear una conexión

Una conexión especifica un origen y contiene sus credenciales para ese origen. Solo se requiere un conector por cuenta de [!DNL Cassandra], ya que se puede utilizar para crear varios conectores de origen para introducir datos diferentes.

**Formato de API**

```http
POST /connections
```

**Solicitud**

Para crear una conexión [!DNL Cassandra], se debe proporcionar su identificador de especificación de conexión único como parte de la petición POST. El id. de especificación de conexión para [!DNL Cassandra] es `a8f4d393-1a6b-43f3-931f-91a16ed857f4`.

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
| `auth.params.host` | Dirección IP o nombre de host del servidor [!DNL Cassandra]. |
| `auth.params.port` | El puerto TCP que utiliza el servidor [!DNL Cassandra] para detectar conexiones de cliente. El puerto predeterminado es `9042`. |
| `auth.params.username` | Nombre de usuario utilizado para conectarse al servidor [!DNL Cassandra] para la autenticación. |
| `auth.params.password` | Contraseña para conectarse al servidor [!DNL Cassandra] para la autenticación. |
| `connectionSpec.id` | Id. de especificación de conexión [!DNL Cassandra]: `a8f4d393-1a6b-43f3-931f-91a16ed857f4`. |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar los datos en el siguiente tutorial.

```json
{
    "id": "ce69aa89-1baa-4054-a9aa-891baa605425",
    "etag": "\"5a026e19-0000-0200-0000-5eac76d00000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión [!DNL Cassandra] mediante la API [!DNL Flow Service] y ha obtenido el valor de ID único de la conexión. Puede usar este identificador en el siguiente tutorial mientras aprende a [explorar bases de datos mediante la API de Flow Service](../../explore/database-nosql.md).
