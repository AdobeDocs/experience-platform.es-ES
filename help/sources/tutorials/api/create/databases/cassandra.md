---
keywords: Experience Platform;home;popular topics;Apache Cassandra;apache cassandra;Cassandra;cassandra
solution: Experience Platform
title: Creación de un conector Apache Cassandra mediante la API de servicio de flujo
topic: overview
type: Tutorial
description: Este tutorial utiliza la API de servicio de flujo para guiarle por los pasos necesarios para conectar Apache Cassandra (en lo sucesivo, "Cassandra") con el Experience Platform.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 3%

---


# Creación de un [!DNL Apache Cassandra] conector mediante la [!DNL Flow Service] API

[!DNL Flow Service] se utiliza para recopilar y centralizar datos de clientes de diversas fuentes dentro de Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde la que se pueden conectar todas las fuentes admitidas.

Este tutorial utiliza la [!DNL Flow Service] API para guiarle por los pasos para conectarse [!DNL Apache Cassandra] (en adelante, &quot;Casandra&quot;) a [!DNL Experience Platform].

## Primeros pasos

Esta guía requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): [!DNL Experience Platform] permite la ingesta de datos desde varias fuentes, al tiempo que le permite estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Simuladores](../../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que debe conocer para conectarse correctamente a Cassandra mediante la [!DNL Flow Service] API.

### Recopilar las credenciales necesarias

Para [!DNL Flow Service] conectarse con [!DNL Cassandra], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `host` | La dirección IP o el nombre de host del [!DNL Cassandra] servidor. |
| `port` | El puerto TCP que utiliza el [!DNL Cassandra] servidor para detectar conexiones de cliente. El puerto predeterminado es `9042`. |
| `username` | Nombre de usuario utilizado para conectarse al [!DNL Cassandra] servidor para la autenticación. |
| `password` | La contraseña para conectarse al [!DNL Cassandra] servidor para la autenticación. |
| `connectionSpec.id` | Identificador único necesario para crear una conexión. El ID de especificación de conexión para [!DNL Cassandra] es `a8f4d393-1a6b-43f3-931f-91a16ed857f4`. |

Para obtener más información sobre cómo empezar, consulte [este documento](https://cassandra.apache.org/doc/latest/operating/security.html#authentication)de Casandra.

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

Una conexión especifica un origen y contiene sus credenciales para ese origen. Solo se requiere un conector por [!DNL Cassandra] cuenta, ya que se puede utilizar para crear varios conectores de origen para introducir datos diferentes.

**Formato API**

```http
POST /connections
```

**Solicitud**

Para crear una [!DNL Cassandra] conexión, debe proporcionarse su ID de especificación de conexión única como parte de la solicitud del POST. El ID de especificación de conexión para [!DNL Cassandra] es `a8f4d393-1a6b-43f3-931f-91a16ed857f4`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `auth.params.port` | El puerto TCP que utiliza el [!DNL Cassandra] servidor para detectar conexiones de cliente. El puerto predeterminado es `9042`. |
| `auth.params.username` | Nombre de usuario utilizado para conectarse al [!DNL Cassandra] servidor para la autenticación. |
| `auth.params.password` | La contraseña para conectarse al [!DNL Cassandra] servidor para la autenticación. |
| `connectionSpec.id` | ID de especificación de [!DNL Cassandra] conexión: `a8f4d393-1a6b-43f3-931f-91a16ed857f4`. |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar los datos en el siguiente tutorial.

```json
{
    "id": "ce69aa89-1baa-4054-a9aa-891baa605425",
    "etag": "\"5a026e19-0000-0200-0000-5eac76d00000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una [!DNL Cassandra] conexión mediante la [!DNL Flow Service] API y ha obtenido el valor de ID único de la conexión. Puede utilizar este ID en el siguiente tutorial cuando aprenda a [explorar bases de datos mediante la API](../../explore/database-nosql.md)de servicio de flujo.
