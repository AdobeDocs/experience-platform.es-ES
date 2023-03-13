---
keywords: Experience Platform;inicio;temas populares;Apache Cassandra;apache cassandra;Cassandra;cassandra
solution: Experience Platform
title: Creación de una conexión de origen de Apache Cassandra mediante la API de Flow Service
type: Tutorial
description: Aprenda a conectar Apache Cassandra a Adobe Experience Platform mediante la API de Flow Service.
source-git-commit: 997423f7bf92469e29c567bd77ffde357413bf9e
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 4%

---


# Crear un [!DNL Apache Cassandra] conexión de origen mediante [!DNL Flow Service] API

[!DNL Flow Service] se utiliza para recopilar y centralizar datos de clientes de varias fuentes diferentes dentro de Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde las que se pueden conectar todas las fuentes de datos admitidas.

Este tutorial utiliza el [!DNL Flow Service] API para guiarle por los pasos para conectarse [!DNL Apache Cassandra] (en lo sucesivo, &quot;Cassandra&quot;) a [!DNL Experience Platform].

## Primeros pasos

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): [!DNL Experience Platform] permite la ingesta de datos desde varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Zonas protegidas](../../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente a Cassandra mediante el [!DNL Flow Service] API.

### Recopilar credenciales necesarias

Para que [!DNL Flow Service] para conectar con [!DNL Cassandra], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `host` | La dirección IP o el nombre de host del [!DNL Cassandra] servidor. |
| `port` | El puerto TCP en el que [!DNL Cassandra] El servidor de utiliza para detectar conexiones de cliente. El puerto predeterminado es `9042`. |
| `username` | El nombre de usuario utilizado para conectarse a [!DNL Cassandra] servidor para autenticación. |
| `password` | La contraseña para conectarse a [!DNL Cassandra] servidor para autenticación. |
| `connectionSpec.id` | El identificador único necesario para crear una conexión. Identificador de especificación de conexión para [!DNL Cassandra] es `a8f4d393-1a6b-43f3-931f-91a16ed857f4`. |

Para obtener más información sobre cómo empezar, consulte [este documento de Cassandra](https://cassandra.apache.org/doc/latest/operating/security.html#authentication).

### Leer llamadas de API de muestra

Este tutorial proporciona llamadas de API de ejemplo para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) en el [!DNL Experience Platform] guía de solución de problemas.

### Recopilar valores para los encabezados obligatorios

Para realizar llamadas a [!DNL Platform] API, primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todas las [!DNL Experience Platform] Llamadas de API, como se muestra a continuación:

* Autorización: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Todos los recursos de [!DNL Experience Platform], incluidos los que pertenecen al [!DNL Flow Service], están aisladas para zonas protegidas virtuales específicas. Todas las solicitudes a [!DNL Platform] Las API requieren un encabezado que especifique el nombre de la zona protegida en la que se realizará la operación:

* x-sandbox-name: `{SANDBOX_NAME}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medios adicional:

* Content-Type: `application/json`

## Crear una conexión

Una conexión especifica un origen y contiene sus credenciales para ese origen. Solo se requiere un conector por [!DNL Cassandra] ya que se puede utilizar para crear varios conectores de origen para introducir datos diferentes.

**Formato de API**

```http
POST /connections
```

**Solicitud**

Para crear un [!DNL Cassandra] conexión, su ID de especificación de conexión único debe proporcionarse como parte de la solicitud del POST. Identificador de especificación de conexión para [!DNL Cassandra] es `a8f4d393-1a6b-43f3-931f-91a16ed857f4`.

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
| `auth.params.host` | La dirección IP o el nombre de host del [!DNL Cassandra] servidor. |
| `auth.params.port` | El puerto TCP en el que [!DNL Cassandra] El servidor de utiliza para detectar conexiones de cliente. El puerto predeterminado es `9042`. |
| `auth.params.username` | El nombre de usuario utilizado para conectarse a [!DNL Cassandra] servidor para autenticación. |
| `auth.params.password` | La contraseña para conectarse a [!DNL Cassandra] servidor para autenticación. |
| `connectionSpec.id` | El [!DNL Cassandra] ID de especificación de conexión: `a8f4d393-1a6b-43f3-931f-91a16ed857f4`. |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar los datos en el siguiente tutorial.

```json
{
    "id": "ce69aa89-1baa-4054-a9aa-891baa605425",
    "etag": "\"5a026e19-0000-0200-0000-5eac76d00000\""
}
```

## Pasos siguientes

Al seguir este tutorial, ha creado un [!DNL Cassandra] conexión mediante el [!DNL Flow Service] y han obtenido el valor de ID único de la conexión. Puede utilizar este ID en el siguiente tutorial mientras aprende a hacer lo siguiente [explorar bases de datos mediante la API de Flow Service](../../explore/database-nosql.md).
